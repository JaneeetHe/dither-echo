# Dither–Echo　推导笔记

---

# 一、正交性与平均化

## 1.1 定义平均符号

$$\overline{f}:=\lim_{T\to\infty}\frac{1}{T}\int_{t_0}^{t_0+T}f(t)\,\mathrm{d}t\qquad(\text{对一切 }t_0\in\mathbb{R})$$

即**无穷时域平均**。

> **两条约定**（否则记号不闭合）：
>
> **① $t_0$ 的量词是"对一切"。** 要求极限存在、其值与 $t_0$ 无关，且收敛**关于 $t_0$ 一致**。本章 1.3 与 1.8 给出的所有界都不含 $t_0$，故这一条是白得的——但必须写出来，因为后面接平均化理论时，正是它构成定理的假设。
>
> **② 本文的 $\overline{\,\cdot\,}$ 只作用于三角多项式**，即 $\sin/\cos$ 的有限乘积（经 P1–P4 化为有限和）。其极限存在性由 1.2 逐项保证。对一般 $f$，该极限未必存在。

## 1.2 单个谐波的平均

设 $\Omega\in\mathbb{R}$，$t_0$ 任意，$T>0$。

### Case 1（$\Omega=0$）

$$\frac{1}{T}\int_{t_0}^{t_0+T}\cos(\Omega t)\,\mathrm{d}t=1$$

$$\frac{1}{T}\int_{t_0}^{t_0+T}\sin(\Omega t)\,\mathrm{d}t=0$$

### Case 2（$\Omega\ne0$）

$$\frac{1}{T}\int_{t_0}^{t_0+T}\cos(\Omega t)\,\mathrm{d}t=\frac{\sin(\Omega(t_0+T))-\sin(\Omega t_0)}{\Omega T}$$

$$\frac{1}{T}\int_{t_0}^{t_0+T}\sin(\Omega t)\,\mathrm{d}t=\frac{\cos(\Omega t_0)-\cos(\Omega(t_0+T))}{\Omega T}$$

**依据**：

$$\int\cos\Omega t\,\mathrm{d}t=\frac{1}{\Omega}\sin\Omega t,\qquad \int\sin\Omega t\,\mathrm{d}t=-\frac{1}{\Omega}\cos\Omega t$$

代入端点即得。

## 1.3 单个谐波平均的分子都不超过 2

$$\left|\frac{1}{T}\int_{t_0}^{t_0+T}\cos(\Omega t)\,\mathrm{d}t\right|\le\frac{2}{|\Omega|T}\qquad(\Omega\ne0)$$

$$\left|\frac{1}{T}\int_{t_0}^{t_0+T}\sin(\Omega t)\,\mathrm{d}t\right|\le\frac{2}{|\Omega|T}\qquad(\Omega\ne0)$$

**当 $T\to\infty$：**

$$\boxed{\ \overline{\cos\Omega t}=\mathbf{1}[\Omega=0],\qquad \overline{\sin\Omega t}=0\quad(\forall\,\Omega\in\mathbb{R})\ }$$

**出处拆解**（每式都由两个来源拼成，缺一不可）：

| | $\Omega=0$ | $\Omega\ne0$ |
|---|---|---|
| $\overline{\cos\Omega t}$ | $=1$，由 **1.2 Case 1** | $=0$，由本节的界 $\le\frac{2}{\lvert\Omega\rvert T}\to0$ |
| $\overline{\sin\Omega t}$ | $=0$，由 **1.2 Case 1**（$\sin(0\cdot t)\equiv0$） | $=0$，由本节的界 $\le\frac{2}{\lvert\Omega\rvert T}\to0$ |

> 📌 $\overline{\cos\Omega t}=0\ (\Omega\ne0)$ 这一支是 **1.6 第二式**与 **1.8** 的唯一依据，必须显式写出，不能只留 $\Omega=0$ 的情形。
> 📌 $\overline{\sin\Omega t}=0$ 对一切 $\Omega$ 成立，**零频也不例外**。这一条后面反复用到（尤其是 1.9）。

## 1.4 两个因子的乘积：四条积化和差

从和角公式出发：

$$\cos(\alpha-\beta)=\cos\alpha\cos\beta+\sin\alpha\sin\beta\qquad\text{①}$$

$$\cos(\alpha+\beta)=\cos\alpha\cos\beta-\sin\alpha\sin\beta\qquad\text{②}$$

$$\sin(\alpha+\beta)=\sin\alpha\cos\beta+\cos\alpha\sin\beta\qquad\text{③}$$

$$\sin(\alpha-\beta)=\sin\alpha\cos\beta-\cos\alpha\sin\beta\qquad\text{④}$$

### 【P1】$\dfrac{\text{①}-\text{②}}{2}$

$$\sin\alpha\sin\beta=\tfrac12\big[\cos(\alpha-\beta)-\cos(\alpha+\beta)\big]$$

### 【P3】$\dfrac{\text{①}+\text{②}}{2}$

$$\cos\alpha\cos\beta=\tfrac12\big[\cos(\alpha-\beta)+\cos(\alpha+\beta)\big]$$

### 【P2】$\dfrac{\text{③}+\text{④}}{2}$

$$\tfrac12\big[2\sin\alpha\cos\beta+(\cos\alpha\sin\beta-\cos\alpha\sin\beta)\big]=\sin\alpha\cos\beta$$

$$\sin\alpha\cos\beta=\tfrac12\big[\sin(\alpha+\beta)+\sin(\alpha-\beta)\big]$$

### 【P4】$\dfrac{\text{③}-\text{④}}{2}$

$$\tfrac12\big[\sin\alpha\cos\beta+\cos\alpha\sin\beta-\sin\alpha\cos\beta+\cos\alpha\sin\beta\big]=\tfrac12\big[2\cos\alpha\sin\beta\big]$$

$$\cos\alpha\sin\beta=\tfrac12\big[\sin(\alpha+\beta)-\sin(\alpha-\beta)\big]$$

> ⚠️ **注意** $\sin\alpha\cos\beta\ne\cos\alpha\sin\beta$，P2 与 P4 是两条不同的公式，用时必须把 $\alpha$、$\beta$ 对号入座。

## 1.5 自检：令 $\alpha=\beta$

$$\text{P1:}\quad \sin^2\alpha=\tfrac12\big[\cos0-\cos2\alpha\big]=\tfrac12(1-\cos2\alpha)$$

$$\text{P3:}\quad \cos^2\alpha=\tfrac12(1+\cos2\alpha)$$

$$\text{P2:}\quad \sin\alpha\cos\alpha=\tfrac12\big[\sin2\alpha+\sin0\big]=\tfrac12\sin2\alpha$$

$$\text{P4:}\quad \cos\alpha\sin\alpha=\tfrac12\big[\sin2\alpha-\sin0\big]=\tfrac12\sin2\alpha$$

**Check**：P1 + P3 $=\sin^2\alpha+\cos^2\alpha=\tfrac12-\tfrac12\cos2\alpha+\tfrac12+\tfrac12\cos2\alpha=1$ ✓

## 1.6 命题：两个因子的平均

设 $\omega_i,\omega_j>0$，则

$$\overline{\sin\omega_it\cdot\sin\omega_jt}=\tfrac12\,\mathbf{1}[\omega_i=\omega_j]$$

$$\overline{\cos\omega_it\cdot\cos\omega_jt}=\tfrac12\,\mathbf{1}[\omega_i=\omega_j]$$

$$\overline{\sin\omega_it\cdot\cos\omega_jt}=0\qquad\text{(for all }\omega_i,\omega_j)$$

### 自检表

| 情形 | $\sin\cdot\sin$ | $\cos\cdot\cos$ | $\sin\cdot\cos$ |
|---|---|---|---|
| $\omega_i=\omega_j=\omega>0$ | $\overline{\sin^2\omega t}=\tfrac12$ ✓ | $\overline{\cos^2\omega t}=\tfrac12$ ✓ | $\overline{\tfrac12\sin2\omega t}=0$ ✓ |
| $\omega_i\ne\omega_j$，均 $>0$ | $0$ | $0$ | $0$ |
| $\omega_i=\omega_j=0$ | $0$ | $1$ | $0$ |

> **红圈标注的两行是全篇最常用的**：同频留 $\tfrac12$，异频归 $0$。
> 第三行说明假设 $\omega_i,\omega_j>0$ 不可省——$\omega=0$ 时前两式都不成立。

## 1.7 定量公式（$\omega_i,\omega_j>0$，$\omega_i\ne\omega_j$）

$$\left|\frac{1}{T}\int_{t_0}^{t_0+T}\sin\omega_it\cdot\sin\omega_jt\,\mathrm{d}t\right|\le\frac{1}{|\omega_i-\omega_j|T}+\frac{1}{(\omega_i+\omega_j)T}\le\frac{2}{|\omega_i-\omega_j|T}$$

两个界都在 1.8 证明。**实际引用时用右端这个干净形式。**

> ⚠️ **不能把和式简化成 $\dfrac{1}{\lvert\omega_i-\omega_j\rvert T}$。**
> $\Sigma>\lvert\Delta\rvert$ 只说明第二项**比第一项小**，不说明它**可以丢掉**——丢掉后得到的是一个**更小**的量，它不再是上界。
> **反例**：取 $\omega_i=2$、$\omega_j=1$（$\Delta=1$），$t_0\approx14.142$、$T\approx9.417$，左端实际值 $\approx0.1416$，而 $\frac{1}{\lvert\Delta\rvert T}\approx0.1062$，**越界 33%**。
> $\Sigma$ 项只在 $\lvert\Delta\rvert\ll\Sigma$（即 $\omega_i\approx\omega_j$）时相对可忽略，而那恰是界本身发散、最不该做近似的场景。
>
> ⚠️ **$\omega_i,\omega_j>0$ 也不可省**：否则 $\Sigma$ 可能为 $0$ 或负，$\frac{1}{\Sigma T}$ 无意义。原表述只写了 $\omega_i\ne\omega_j$。

---

## 1.8 证明：两因子定量界

记 $\Delta:=\omega_i-\omega_j$，$\Sigma:=\omega_i+\omega_j$。由 P1：

$$\sin\omega_it\cdot\sin\omega_jt=\tfrac12\cos(\Delta t)-\tfrac12\cos(\Sigma t)$$

**积分的线性性：**

$$\frac{1}{T}\int_{t_0}^{t_0+T}\sin\omega_it\sin\omega_jt\,\mathrm{d}t=\tfrac12\cdot\frac{1}{T}\int_{t_0}^{t_0+T}\cos(\Delta t)\,\mathrm{d}t-\tfrac12\cdot\frac{1}{T}\int_{t_0}^{t_0+T}\cos(\Sigma t)\,\mathrm{d}t$$

记 LHS $=\tfrac12A-\tfrac12B$。

**由三角不等式：**

$$\left|\tfrac12A-\tfrac12B\right|\le\tfrac12|A|+\tfrac12|B|\qquad\text{③}$$

**由 1.3 的界（$\omega_i\ne\omega_j$，$\omega_i,\omega_j>0$）：**

$$|A|\le\frac{2}{|\Delta|T}\ \Longrightarrow\ \tfrac12|A|\le\tfrac12\cdot\frac{2}{|\Delta|T}=\frac{1}{|\Delta|T}\qquad\text{①}$$

$$|B|\le\frac{2}{\Sigma T}\ \Longrightarrow\ \tfrac12|B|\le\frac{1}{\Sigma T}\qquad\text{②}$$

**①②代回③：**

$$\left|\frac{1}{T}\int_{t_0}^{t_0+T}\sin\omega_it\sin\omega_jt\,\mathrm{d}t\right|\le\frac{1}{|\omega_i-\omega_j|T}+\frac{1}{(\omega_i+\omega_j)T}$$

因 $\omega_i,\omega_j>0$，必有 $\Sigma>|\Delta|$，故 $\dfrac{1}{\Sigma T}<\dfrac{1}{|\Delta|T}$，因而有一个更干净的粗糙界：

$$\left|\frac{1}{T}\int_{t_0}^{t_0+T}\sin\omega_it\sin\omega_jt\,\mathrm{d}t\right|\le\frac{2}{|\omega_i-\omega_j|T}$$

---

## 1.9 三个因子的平均

对任意 $\omega_1,\omega_2,\omega_3$：

$$\overline{\sin\omega_1t\cdot\sin\omega_2t\cdot\sin\omega_3t}=0$$

### 证明

设 $A=\omega_1t$，$B=\omega_2t$，$C=\omega_3t$。

**From P1：**

$$\sin A\sin B=\tfrac12\big[\cos(A-B)-\cos(A+B)\big]$$

**乘上第三个因子：**

$$\sin A\sin B\sin C=\tfrac12\cos(A-B)\sin C-\tfrac12\cos(A+B)\sin C$$

**From P2：**

$$\sin C\cos(A-B)=\tfrac12\sin(C+A-B)+\tfrac12\sin(C-A+B)$$

$$\sin C\cos(A+B)=\tfrac12\sin(C+A+B)+\tfrac12\sin(C-A-B)$$

**代回：**

$$\sin A\sin B\sin C=\tfrac14\big[\sin(A-B+C)+\sin(-A+B+C)-\sin(A+B+C)-\sin(-A-B+C)\big]$$

**取平均**：由 **1.3 的合并结论** $\overline{\sin\Omega t}=0\ (\forall\,\Omega\in\mathbb{R})$，四项都为 $0$，和为 $0$。

> ⚠️ **零频那一支不可略，且出处不是 1.3 的不等式。**
> 四项的频率 $\pm\omega_1\pm\omega_2+\omega_3$ 都**可能为零**：$\omega_1=\omega_2$ 时第一、二项为零频；$\omega_3=\omega_1+\omega_2$ 时第四项为零频。
> 而 1.3 的界 $\le\frac{2}{\lvert\Omega\rvert T}$ **前提是 $\Omega\ne0$**，覆盖不了这些情形。$\Omega=0$ 一支来自 **1.2 Case 1**（$\sin(0\cdot t)\equiv0$）。
> 两个来源缺任何一个，本命题在**频率重复**时就不成立——而下面的补注恰恰要用重复频率的情形。

> 📌 **补注**：此命题对**任意** $\omega_1,\omega_2,\omega_3$ 成立，**包括频率相等或重复的情形**。
> 这一点必须记住——后面 Step 3 里要用它处理 $\overline{s_vs_vs_v}$ 和 $\overline{s_v^2s_d}$，若限制 $A\ne B\ne C$ 就用不了了。
> 验算：$\omega_1=\omega_2=\omega_3=\omega$ 时 $\sin^3\omega t=\tfrac14(3\sin\omega t-\sin3\omega t)$，两项都是正弦，平均为 $0$ ✓

---

# 二、解调函数 $C_v$

## 2.0 目标

$$C_v=\frac{2}{a}\,\overline{J_v(x)\sin\omega_vt}=\partial_vJ_v(u)+O(a^2)$$

其中

$$x_v=u_v+a\sin\omega_vt,\qquad x_d=u_d+a\sin\omega_dt,\qquad \omega_d\ne\omega_v,\ \text{均}>0$$

**记号**：$s_v:=\sin\omega_vt$，$s_d:=\sin\omega_dt$，$J_v\in C^3$。

---

## Step 1　Taylor 展开 $J_v(x)$ around $u$

展开

$$J_v(x_v,x_d)=J_v(u_v+as_v,\ u_d+as_d)$$

**定义辅助函数**

$$g(\tau):=J_v(u_v+\tau as_v,\ u_d+\tau as_d)$$

$$g(0)=J_v(u_v,u_d),\qquad g(1)=J_v(x_v,x_d)\ \ \longleftarrow\ \textbf{this is what we want!}$$

### 一阶导

$$g'(\tau)=\partial_vJ_v\cdot as_v+\partial_dJ_v\cdot as_d$$

$$g'(0)=as_v\,\partial_vJ_v+as_d\,\partial_dJ_v$$

### 二阶导

$$g''(\tau)=as_v\big[\partial^2_{vv}J_v\,as_v+\partial^2_{vd}J_v\,as_d\big]+as_d\big[\partial^2_{dv}J_v\,as_v+\partial^2_{dd}J_v\,as_d\big]$$

$$=a^2s_v^2\,\partial^2_{vv}J_v+a^2s_vs_d\,\partial^2_{vd}J_v+a^2s_ds_v\,\partial^2_{dv}J_v+a^2s_d^2\,\partial^2_{dd}J_v$$

中间两项因 $\partial^2_{vd}=\partial^2_{dv}$ 且 $s_vs_d=s_ds_v$ 而合并，得系数 $2$：

$$=a^2s_v^2\,\partial^2_{vv}J_v+2a^2(s_vs_d\,\partial^2_{vd}J_v)+a^2s_d^2\,\partial^2_{dd}J_v$$

$$g''(0)=a^2\big[s_v^2\,\partial^2_{vv}J_v+2s_vs_d\,\partial^2_{vd}J_v+s_d^2\,\partial^2_{dd}J_v\big]$$

### 套 Taylor 公式

$$g(1)=g(0)+\frac{g'(0)}{1!}+\frac{g''(0)}{2!}+R_3$$

$$\Longrightarrow\quad g(1)=g(0)+g'(0)+\tfrac12g''(0)+R_3$$

### 代回

$$J_v(x)=J_v(u)+\big[as_v\partial_vJ_v+as_d\partial_dJ_v\big]+\tfrac12a^2\big[s_v^2\partial^2_{vv}J_v+2s_vs_d\partial^2_{vd}J_v+s_d^2\partial^2_{dd}J_v\big]+R_3$$

提出 $a$ 与 $a^2$：

$$J_v(x)=J_v(u)+a\big[\partial_vJ_v\cdot s_v+\partial_dJ_v\cdot s_d\big]+\tfrac12a^2\big[s_v^2\partial^2_{vv}J_v+2s_vs_d\partial^2_{vd}J_v+s_d^2\partial^2_{dd}J_v\big]+R_3$$

---

## Step 2　整体乘上 $s_v$

$$J_v(x)s_v=J_v(u)s_v+\big[a\partial_vJ_v\,s_v^2+a\partial_dJ_v\,s_ds_v\big]+\frac{a^2}{2}\big[\partial^2_{vv}J_v\,s_v^3+2\partial^2_{vd}J_v\,s_v^2s_d+\partial^2_{dd}J_v\,s_d^2s_v\big]+R_3s_v$$

---

## Step 3　逐项取平均

### 零阶项

$$J_v(u)\cdot\overline{s_v}\ \longrightarrow\ 0$$

理由：只有**一个**正弦因子，而 $\overline{\sin\omega_vt}=0$。

### 一阶项

$$\overline{s_vs_v}=\tfrac12,\qquad \boxed{\ \overline{s_ds_v}=0\ }$$

$$\Longrightarrow\ a\,\partial_vJ_v\cdot\tfrac12+a\,\partial_dJ_v\cdot 0=\frac{a}{2}\,\partial_vJ_v$$

> 🔴 **关键：当 $s_d=s_v$ 时，也就是 $\omega_v=\omega_d$（欺骗发生！），$\overline{s_ds_v}\ne0$，检测失效！**
>
> 这一行就是整个攻击的入口。

### 二阶项

$$\overline{s_vs_vs_v}=0,\qquad \overline{s_v^2s_d}=0,\qquad \overline{s_d^2s_v}=0$$

三条全部来自 1.9（三个正弦之积的平均恒为零，允许频率重复）。

$$\Longrightarrow\ 0$$

### 三阶余项

$$R_3s_v\ \longrightarrow\ O(a^3)$$

---

## Step 4　合并并整理系数

$$\overline{J_v(x)s_v}=0+\frac{a}{2}\partial_vJ_v+0+O(a^3)$$

$$C_v=\frac{2}{a}\,\overline{J_v(x)s_v}=\frac{2}{a}\left[\frac{a}{2}\partial_vJ_v+O(a^3)\right]=\partial_vJ_v+O(a^2)$$

$$\boxed{\ C_v=\frac{2}{a}\,\overline{J_v(x)s_v}=\partial_vJ_v(u)+O(a^2)\ }\qquad\checkmark$$

---

# 三、反馈与伪梯度 $F$

## 3.1 从估计到更新律

目标是想让 $J_v$ 变小，沿负梯度走：

$$\dot u_v=-k\,\partial_vJ_v(u),\qquad k>0$$

但 $\partial_vJ_v$ 测不到，用估计值替换：

$$\dot u_v=-k\,C_v,\qquad k\ \text{是增益}$$

## 3.2 两个玩家的梯度公式

$$\dot u_v=-k\,C_v=-k\big[\partial_vJ_v(u)+O(a^2)\big]$$

$$\dot u_d=-k\,C_d=-k\big[\partial_dJ_d(u)+O(a^2)\big]$$

## 3.3 展开括号

$$\dot u_v=-k\,\partial_vJ_v(u)-k\cdot O(a^2)$$

$$\dot u_d=-k\,\partial_dJ_d(u)-k\cdot O(a^2)$$

## 3.4 写成向量形式

$$(\dot u_v,\ \dot u_d)^{\top}=-k\,(\partial_vJ_v(u),\ \partial_dJ_d(u))^{\top}-k\cdot O(a^2)$$

右端第一个向量即**伪梯度** $F(u)$：

$$\boxed{\ F(u):=(\partial_vJ_v(u),\ \partial_dJ_d(u))^{\top}\ }$$

$$\Longrightarrow\quad \dot u=-k\,F(u)-k\cdot O(a^2)$$

## 3.5 $-k$ 可融进 $O(a^2)$

由 $O$ 记号的定义（$|g(a)|\le Ma^2$），有 $|-k\,g(a)|\le (kM)a^2$，而 $kM$ 仍是常数，故

$$-k\cdot O(a^2)=O(a^2)$$

$$\boxed{\ \dot u=-k\,F(u)+O(a^2)\ }$$

> 这里的 $+$ 号不表示"这一项是正的"，只是连接符。$O$ 记号不携带符号信息，常数因子（含 $k$、含负号）一律被吸收。
> **前提**：$k$ 与 $a$ 无关。若 $k=k_0/a$，则 $\frac{k_0}{a}O(a^2)=O(a)$，阶数会掉。

## 3.6 Nash 均衡

$$\text{NE:}\qquad F(u^*)=0$$

---

# 四、伪梯度例子

$$J_v=\tfrac12x_v^2+c\,x_vx_d-x_v,\qquad J_d=\tfrac12x_d^2+c\,x_vx_d-2x_d$$

**伪梯度：**

$$F(u)=(\,u_v+cu_d-1,\ \ u_d+cu_v-2\,)^{\top}=0$$

## 解 NE（取 $c=0.5$）

$$u_v+0.5u_d=1\qquad\text{①}$$

$$0.5u_v+u_d=2\qquad\text{②}$$

$2\times\text{②}-\text{①}$：

$$u_v+2u_d-u_v-0.5u_d=4-1=3$$

$$1.5u_d=3\ \Longrightarrow\ u_d=2,\quad u_v=0$$

$$\therefore\quad u^*(\text{NE})=(0,\ 2)$$

## 验证

$$0+0.5\times2-1=0,\qquad 2+0.5\times0-2=0$$

$$F(u)=(0,\ 0)^{\top}\ \Longrightarrow\ \textbf{Nash Equilibrium}$$

---

# 附：两条待补

**① 平均化的合法性。** Step 3 把 $\partial_vJ_v(u)$ 等系数提到平均号外，用到 $u$ 为常数；但 3.1 一旦接上反馈，$u$ 就开始动了。补法是平均化理论（$\tau=\omega t$、$\epsilon=1/\omega$、近恒等变换），结论是真实轨迹与平均轨迹只差 $O(\epsilon)$ 的**有界纹波**，不是累积漂移。

**② 平衡点的偏移。** 在 $F(u^*)=0$ 处，$\dot u=O(a^2)\ne0$，故系统并不停在 $u^*$，而停在使整个右端为零的 $u^\dagger$。由隐函数定理

$$u^\dagger(a)-u^*=O(a^2)$$

所以"收敛到 NE"是简写，准确说法是**收敛到 NE 的 $O(a^2)$ 邻域**。