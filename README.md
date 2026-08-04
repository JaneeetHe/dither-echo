# dither-echo

**Self-detection and recovery from deception in model-free Nash equilibrium seeking.**

A deceiver in Nash-equilibrium-seeking (NES) dynamics must continuously inject the victim's
exploration signal into its own action. That injection is structurally permanent — and it leaves
an audible echo in a quantity the victim already computes. This repository implements the attack,
the detector, and the recovery mechanism.

> Status: research code, actively developed. Interfaces may change until the accompanying paper
> is released.

---

## The problem

In model-free NES ([Frihauf, Krstić & Başar](https://ieeexplore.ieee.org/document/6060862)), each
player perturbs its action with a unique dither frequency and recovers its gradient by
demodulation:

```
x_i(t) = u_i(t) + a·sin(ω_i·t)                      (action = estimate + exploration)
u̇_i    = −(2k/a)·J_i(x(t))·sin(ω_i·t)               (update = demodulation)
```

Frequency orthogonality makes the other players' dithers cancel out in the time average, so each
player recovers its own pseudogradient without any model of the game.

[Tang, Javed, Chen, Krstić & Poveda (arXiv:2407.05168)](https://arxiv.org/abs/2407.05168) showed
this scheme is attackable. A deceiver with privileged knowledge of the victim's exploration policy
injects the victim's own frequency into its action:

```
x_d(t) = u_d(t) + a·[sin(ω_d·t) + δ_d(t)·sin(ω_v·t)]
δ̇_d    = ε·(J_d(x) − J_d^ref)
```

The victim's gradient estimate is biased, and the system converges — exponentially, stably — to a
**Deceptive Nash Equilibrium (DNE)** chosen in real time by the deceiver.

**The detection problem is that the DNE looks exactly like success.** At the DNE the victim's
estimated gradient is zero, so `u̇_v → 0` and the action settles. A residual built on action
updates,

```
r_v(t) = x_v(t+1) − x̂_v(t+1)
```

also vanishes. It cannot separate an honest NE from a DNE.

## The idea

The signal that does *not* vanish is the demodulation integral itself. Define the **echo residual**

```
C_v(t) = (1/T)·∫_{t−T}^{t} J_v(τ)·sin(ω_v·τ) dτ
```

Because `x_d` carries a `sin(ω_v·t)` component, the victim's payoff `J_v` acquires an extra term at
its *own* dither frequency. Under demodulation:

```
sin(ω_v·t) × sin(ω_v·t)  --time avg-->  1/2  ≠  0
```

So `C_v` stays persistently nonzero at the DNE, long after the action has stabilized. This yields a
detection rule requiring no knowledge of the deceiver's identity, of `δ_d`, or of the game
parameters — only the victim's own payoff observations and its own exploration signal:

```
action stable  ∧  |C_v| > τ_thresh   ⟹   deception active
action stable  ∧  |C_v| → 0          ⟹   honest convergence
```

`C_v` is not a new measurement. It is the right-hand side of the update law the victim already
runs. The proposal is to *observe* it as a monitoring signal rather than only feed it forward.

**Why the deceiver cannot hide.** If `δ_d → 0` the injection stops, the victim's true gradient
reactivates, and it drifts back to the true NE — the deception breaks. Holding the victim at the
DNE requires `δ_d ≠ 0`, which requires the echo. Detection and attack efficacy are in direct
tension.

## Recovery: dither hopping

Once `C_v` crosses threshold, the victim randomizes its exploration frequency `ω_v`. The deceiver's
injected component is now at the wrong frequency, demodulates to zero, and `δ_d` loses its target.
The DNE collapses and the victim recovers to the true NE.

This is structurally the same defense frequency-hopping spread spectrum uses against a jammer: the
attack depends on knowing the victim's carrier, so the victim stops holding still.

## Install

```bash
git clone https://github.com/<you>/dither-echo.git
cd dither-echo
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
pip install -e .
```

Requires Python ≥ 3.10. Core dependencies: `numpy`, `scipy`, `matplotlib`.

## Quickstart

```python
from dither_echo.games import QuadraticGame
from dither_echo.nes import NESPlayer
from dither_echo.deception import Deceiver
from dither_echo.detector import EchoResidual
from dither_echo.simulate import run

game = QuadraticGame(
    Q=[[[3, 1], [1, 1/3]], [[1, 2], [2, 4]]],
    b=[[7, 4/3], [3, 6]],
)

victim   = NESPlayer(idx=0, omega=7.0,  a=0.1, k=1.0)
deceiver = Deceiver(idx=1, omega=11.0, a=0.1, k=1.0,
                    target_omega=7.0, J_ref=-3.0, eps=0.05)

detector = EchoResidual(omega=victim.omega, window=2*3.14159/7.0 * 20,
                        threshold=1e-2)

log = run(game, players=[victim, deceiver], detector=detector,
          T=4000.0, dt=1e-3, recovery="dither_hopping")

log.plot_actions()        # action converges — looks honest
log.plot_echo_residual()  # C_v stays nonzero — it isn't
```

To disable the defense and reproduce the bare attack, pass `recovery=None`.

## Repository layout

```
dither-echo/
├── src/dither_echo/
│   ├── games.py         # quadratic, duopoly, aggregative payoffs + true NE
│   ├── nes.py           # nominal NES dynamics (Eq. 1)
│   ├── deception.py     # deceiver dynamics and δ integrator (Eq. 17–18)
│   ├── detector.py      # echo residual C_v, windowing, thresholding
│   ├── recovery.py      # dither hopping and trust-weighted fallback
│   ├── simulate.py      # integrator and experiment runner
│   └── viz.py           # plotting helpers
├── experiments/
│   ├── exp1_dne_is_silent.py       # action residual fails to separate NE / DNE
│   ├── exp2_echo_residual.py       # C_v separates them
│   ├── exp3_recovery.py            # dither hopping restores the true NE
│   ├── exp4_duopoly.py             # microeconomic instance
│   ├── exp5_roc.py                 # detection ROC vs. δ, noise, window length
│   └── configs/
├── tests/
├── notebooks/
└── results/                        # generated figures (gitignored)
```

## Reproducing the figures

```bash
python experiments/exp1_dne_is_silent.py --config experiments/configs/quadratic.yaml
python experiments/exp2_echo_residual.py --config experiments/configs/quadratic.yaml
python experiments/exp3_recovery.py      --config experiments/configs/quadratic.yaml
```

Figures are written to `results/`. Each script prints the random seed it used; pass `--seed` to
reproduce a specific run exactly.

## Relation to prior work

Tang et al. establish *structural* immunity: a rank-1 condition on the payoff matrices
(their Lemma 2) identifies games in which deception cannot rotate or translate the oblivious
player's reaction curve at all. That result asks which games are immune by construction.

This repository asks the complementary question: **when the game is not immune, can the victim
detect it and escape unilaterally?** The two are compatible — structural immunity is a design-time
property of the payoff structure, echo-residual auditing is a run-time property of the learning
agent.

## Roadmap

- [ ] Multiple deceivers and mutual deception
- [ ] Detection under measurement noise and non-quadratic payoffs
- [ ] Finite-sample threshold selection with false-alarm guarantees
- [ ] Aggregative games, where deception induces nonlinear reaction-curve transformations
- [ ] Extension to multi-agent LLM committees: does an analogous echo appear when one agent steers
      a collective decision through feedback it also observes?

## Citation

If this code is useful in your work, please cite the underlying deception model:

```bibtex
@article{tang2025deception,
  title   = {Deception in {N}ash Equilibrium Seeking},
  author  = {Tang, Michael and Javed, Umar and Chen, Xudong
             and Krstic, Miroslav and Poveda, Jorge I.},
  journal = {arXiv preprint arXiv:2407.05168},
  year    = {2025}
}
```

A citation entry for the detection and recovery results will be added when the accompanying paper
is public.

## License

MIT. See [LICENSE](LICENSE).

## Contact

Jingyi — Department of Electrical and Computer Engineering, UC San Diego.
Questions and issues welcome via the [issue tracker](https://github.com/dither-echo/dither-echo/issues).