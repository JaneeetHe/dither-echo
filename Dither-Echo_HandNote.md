# Dither-Echo 推导笔记

---

# 一、正交性与平均化

## 1.1 定义平均符号

$$\overline{f}:=\lim_{T\to\infty}\frac{1}{T}\int_{t_0}^{t_0+T}f(t)\,\mathrm{d}t$$

即**无穷时域平均**。

## 1.2 单个谐波的平均

设 $\Omega\in\mathbb{R},\ t_0\in\mathbb{R},\ T>0$。

### Case 1（Ω = 0）

$$\frac{1}{T}\int_{t_0}^{t_0+T}\cos(\Omega t)\,\mathrm{d}t=1$$

$$\frac{1}{T}\int_{t_0}^{t_0+T}\sin(\Omega t)\,\mathrm{d}t=0$$

### Case 2（Ω ≠ 0）

$$\frac{1}{T}\int_{t_0}^{t_0+T}\cos(\Omega t)\,\mathrm{d}t=\frac{\sin\big(\Omega(t_0+T)\big)-\sin(\Omega t_0)}{\Omega T}$$

$$\frac{1}{T}\int_{t_0}^{t_0+T}\sin(\Omega t)\,\mathrm{d}t=\frac{\cos(\Omega t_0)-\cos\big(\Omega(t_0+T)\big)}{\Omega T}$$

**所用积分公式**：

$$\int\cos\Omega t\,\mathrm{d}t=\frac{1}{\Omega}\sin\Omega t,\qquad \int\sin\Omega t\,\mathrm{d}t=-\frac{1}{\Omega}\cos\Omega t$$

## 1.3 单个谐波平均都不超过 2

$$\left|\frac{1}{T}\int_{t_0}^{t_0+T}\cos(\Omega t)\,\mathrm{d}t\right|\le\frac{2}{|\Omega|T}\qquad(\Omega\ne0)$$

$$\left|\frac{1}{T}\int_{t_0}^{t_0+T}\sin(\Omega t)\,\mathrm{d}t\right|\le\frac{2}{|\Omega|T}\qquad(\Omega\ne0)$$

**当 $T\to\infty$：**

$$\boxed{\ \overline{\cos\Omega t}=\mathbf{1}[\Omega=0],\qquad \overline{\sin\Omega t}=0\quad(\forall\,\Omega\in\mathbb{R})\ }$$

> 📌 $\overline{\cos\Omega t}=1$ 来自 $\Omega=0$（1.2 Case 1）； $\overline{\cos\Omega t}=0\ (\Omega\ne0)$ 来自本节的界。
> 📌 $\overline{\sin\Omega t}=0$ 对一切 $\Omega\in\mathbb{R}$ 成立，零频也不例外。

## 1.4 两个因子的乘积

$$\cos(\alpha-\beta)=\cos\alpha\cos\beta+\sin\alpha\sin\beta\qquad ①$$

$$\cos(\alpha+\beta)=\cos\alpha\cos\beta-\sin\alpha\sin\beta\qquad ②$$

$$\sin(\alpha+\beta)=\sin\alpha\cos\beta+\cos\alpha\sin\beta\qquad ③$$

$$\sin(\alpha-\beta)=\sin\alpha\cos\beta-\cos\alpha\sin\beta\qquad ④$$

### 【P1】(① − ②) ÷ 2

$$\sin\alpha\sin\beta=\frac{1}{2}\Big[\cos(\alpha-\beta)-\cos(\alpha+\beta)\Big]$$

### 【P3】(① + ②) ÷ 2

$$\cos\alpha\cos\beta=\frac{1}{2}\Big[\cos(\alpha-\beta)+\cos(\alpha+\beta)\Big]$$

### 【P2】(③ + ④) ÷ 2

$$\frac{1}{2}\Big[2\sin\alpha\cos\beta+\big(\cos\alpha\sin\beta-\cos\alpha\sin\beta\big)\Big]=\sin\alpha\cos\beta$$

$$\sin\alpha\cos\beta=\frac{1}{2}\Big[\sin(\alpha+\beta)+\sin(\alpha-\beta)\Big]$$

### 【P4】(③ − ④) ÷ 2

$$\frac{1}{2}\Big[\sin\alpha\cos\beta+\cos\alpha\sin\beta-\sin\alpha\cos\beta+\cos\alpha\sin\beta\Big]=\frac{1}{2}\big[2\cos\alpha\sin\beta\big]$$

$$\cos\alpha\sin\beta=\frac{1}{2}\Big[\sin(\alpha+\beta)-\sin(\alpha-\beta)\Big]$$

> ⚠️ 注意 $\sin\alpha\cos\beta\ne\cos\alpha\sin\beta$，用时必须把 $\alpha,\beta$ 对号入座。

## 1.5 自检：令 α = β

$$\text{【P1】}\quad \sin^2\alpha=\tfrac12\big[\cos0-\cos2\alpha\big]=\tfrac12\big[1-\cos2\alpha\big]$$

$$\text{【P3】}\quad \cos^2\alpha=\tfrac12\big(1+\cos2\alpha\big)$$

$$\text{【P2】}\quad \sin\alpha\cos\alpha=\tfrac12\big[\sin2\alpha+\sin0\big]=\tfrac12\sin2\alpha$$

$$\text{【P4】}\quad \cos\alpha\sin\alpha=\tfrac12\big[\sin2\alpha-\sin0\big]=\tfrac12\sin2\alpha$$

**Check**：【P1】+【P3】 $=\sin^2\alpha+\cos^2\alpha=\tfrac12-\tfrac12\cos2\alpha+\tfrac12+\tfrac12\cos2\alpha=1$ ✓

## 1.6 命题：两个因子的平均

同理设 $\omega_i,\omega_j>0$，则

$$\overline{\sin\omega_it\cdot\sin\omega_jt}=\tfrac12\,\mathbf{1}\big[\omega_i=\omega_j\big]$$

$$\overline{\cos\omega_it\cdot\cos\omega_jt}=\tfrac12\,\mathbf{1}\big[\omega_i=\omega_j\big]$$

$$\overline{\sin\omega_it\cdot\cos\omega_jt}=0\qquad\text{（对一切 }\omega_i,\omega_j\text{）}$$

### 自检表

| 情形 | sin · sin | cos · cos | sin · cos |
|---|---|---|---|
| $\omega_i=\omega_j=\omega>0$ | $\overline{\sin^2\omega t}=\tfrac12$ ✓ | $\overline{\cos^2\omega t}=\tfrac12$ ✓ | $\overline{\tfrac12\sin2\omega t}=0$ ✓ |
| $\omega_i\ne\omega_j$，均 $>0$ | $0$ | $0$ | $0$ |
| $\omega_i=\omega_j=0$ | $0$ | $1$ | $0$ |

> 📌 **前两行是全篇最常用的**（原稿红圈标注）：同频留 $\tfrac12$，异频归 $0$。
> 📌 第三行说明假设 $\omega_i,\omega_j>0$ 不可省——当 $\omega=0$ 时前两式都不成立。

## 1.7 定量公式

若 $\omega_i\ne\omega_j$、 $\omega_i,\omega_j>0$：

$$\left|\frac{1}{T}\int_{t_0}^{t_0+T}\sin\omega_it\cdot\sin\omega_jt\,\mathrm{d}t\right|\le\frac{1}{|\omega_i-\omega_j|T}+\frac{1}{(\omega_i+\omega_j)T}$$

$$\Big(\ \approx\ \frac{1}{|\omega_i-\omega_j|T}\ \Big)$$

## 1.8 证明：两因子定量界

记 $\Delta:=\omega_i-\omega_j,\ \Sigma:=\omega_i+\omega_j$。由【P1】：

$$\sin\omega_it\cdot\sin\omega_jt=\tfrac12\cos(\Delta t)-\tfrac12\cos(\Sigma t)$$

**积分的线性性**：

$$\frac{1}{T}\int_{t_0}^{t_0+T}\sin\omega_it\sin\omega_jt\,\mathrm{d}t=\tfrac12\cdot\frac{1}{T}\int_{t_0}^{t_0+T}\cos(\Delta t)\,\mathrm{d}t-\tfrac12\cdot\frac{1}{T}\int_{t_0}^{t_0+T}\cos(\Sigma t)\,\mathrm{d}t$$

记 LHS $=\tfrac12A-\tfrac12B$。

**由三角不等式**：

$$\Big|\tfrac12A-\tfrac12B\Big|\le\tfrac12|A|+\tfrac12|B|\qquad (iii)$$

**由 1.3 的界**（此时 $\omega_i\ne\omega_j$ 且 $\omega_i,\omega_j>0$）：

$$|A|\le\frac{2}{|\Delta|T}\ \Longrightarrow\ \tfrac12|A|\le\tfrac12\cdot\frac{2}{|\Delta|T}=\frac{1}{|\Delta|T}\qquad (i)$$

$$|B|\le\frac{2}{\Sigma T}\ \Longrightarrow\ \tfrac12|B|\le\frac{1}{\Sigma T}\qquad (ii)$$

**(i)(ii) 代回 (iii)**：

$$\left|\frac{1}{T}\int_{t_0}^{t_0+T}\sin\omega_it\cdot\sin\omega_jt\,\mathrm{d}t\right|\le\frac{1}{|\omega_i-\omega_j|T}+\frac{1}{(\omega_i+\omega_j)T}$$

因 $\omega_i,\omega_j>0$，必有 $\Sigma>|\Delta|$，故 $\dfrac{1}{\Sigma T}<\dfrac{1}{|\Delta|T}$，因而有一个更干净的粗糙界：

$$\boxed{\ \left|\frac{1}{T}\int_{t_0}^{t_0+T}\sin\omega_it\cdot\sin\omega_jt\,\mathrm{d}t\right|\le\frac{2}{|\omega_i-\omega_j|T}\ }$$

## 1.9 三个因子的平均

对任意 $\omega_1,\omega_2,\omega_3$：

$$\boxed{\ \overline{\sin\omega_1t\cdot\sin\omega_2t\cdot\sin\omega_3t}=0\ }$$

**证明**：设 $A=\omega_1t,\ B=\omega_2t,\ C=\omega_3t$。

由【P1】：

$$\sin A\sin B=\tfrac12\Big[\cos(A-B)-\cos(A+B)\Big]$$

乘上第三个因子：

$$\sin A\cdot\sin B\cdot\sin C=\tfrac12\cos(A-B)\sin C-\tfrac12\cos(A+B)\sin C$$

由【P2】：

$$\sin C\cos(A-B)=\tfrac12\sin(C+A-B)+\tfrac12\sin(C-A+B)$$

$$\sin C\cos(A+B)=\tfrac12\sin(C+A+B)+\tfrac12\sin(C-A-B)$$

代回：

$$\sin A\sin B\sin C=\tfrac14\Big[\sin(A-B+C)+\sin(-A+B+C)-\sin(A+B+C)-\sin(-A-B+C)\Big]$$

**取平均**：由 1.3， $\overline{\sin\Omega t}=0$ 对一切 $\Omega$ 成立（零频亦然），因而四项都为 $0$，和为 $0$。∎

---

# 二、解调函数 Cv

## 2.0 目标

$$C_v=\frac{2}{a}\,\overline{J_v(x)\sin\omega_vt}=\partial_vJ_v(u)+O(a^2)$$

其中

$$x_v=u_v+a\sin\omega_vt,\qquad x_d=u_d+a\sin\omega_dt$$

$$\text{条件：}\ \omega_d,\omega_v>0,\quad \omega_d\ne\omega_v,\quad J_v\in C^3$$

---

## Step 1　Taylor 展开 Jv(x) around u

### 设定

$$s:=(s_v,s_d)=(\sin\omega_vt,\ \sin\omega_dt),\qquad u:=(u_v,u_d),\qquad x=u+as$$

定义一元函数

$$g_t(\tau):=J_v(u+\tau as)=J_v\big(u_v+\tau as_v,\ u_d+\tau as_d\big),\qquad \tau\in[0,1]$$

以下**对 $\tau$ 求导**， $t$ **视为常数**（故 $s_v,s_d$ 为常数）。记

$$u_\tau:=u+\tau as,\qquad u_0=u,\qquad u_1=x$$

$$g_t(0)=J_v(u),\qquad g_t(1)=J_v(x)$$

### 一阶导

$$g_t'(\tau)=\partial_vJ_v(u_\tau)\,as_v+\partial_dJ_v(u_\tau)\,as_d=a\Big[\partial_vJ_v(u_\tau)\,s_v+\partial_dJ_v(u_\tau)\,s_d\Big]$$

$$g_t'(0)=a\Big[\partial_vJ_v(u)\,s_v+\partial_dJ_v(u)\,s_d\Big]$$

### 二阶导

$$\frac{\mathrm{d}}{\mathrm{d}\tau}\partial_vJ_v(u_\tau)=a\Big[\partial^2_{vv}J_v(u_\tau)\,s_v+\partial^2_{vd}J_v(u_\tau)\,s_d\Big]$$

$$\frac{\mathrm{d}}{\mathrm{d}\tau}\partial_dJ_v(u_\tau)=a\Big[\partial^2_{dv}J_v(u_\tau)\,s_v+\partial^2_{dd}J_v(u_\tau)\,s_d\Big]$$

$$g_t''(\tau)=a\,s_v\cdot a\Big[\partial^2_{vv}J_v(u_\tau)s_v+\partial^2_{vd}J_v(u_\tau)s_d\Big]+a\,s_d\cdot a\Big[\partial^2_{dv}J_v(u_\tau)s_v+\partial^2_{dd}J_v(u_\tau)s_d\Big]$$

$$=a^2\Big[s_v^2\,\partial^2_{vv}J_v(u_\tau)+s_vs_d\,\partial^2_{vd}J_v(u_\tau)+s_ds_v\,\partial^2_{dv}J_v(u_\tau)+s_d^2\,\partial^2_{dd}J_v(u_\tau)\Big]$$

因 $s_vs_d=s_ds_v$，且 $\partial^2_{vd}J_v=\partial^2_{dv}J_v$（**Schwarz–Clairaut 定理**），故

$$g_t''(\tau)=a^2\Big[s_v^2\,\partial^2_{vv}J_v(u_\tau)+2s_vs_d\,\partial^2_{vd}J_v(u_\tau)+s_d^2\,\partial^2_{dd}J_v(u_\tau)\Big]$$

$$g_t''(0)=a^2\Big[s_v^2\,\partial^2_{vv}J_v(u)+2s_vs_d\,\partial^2_{vd}J_v(u)+s_d^2\,\partial^2_{dd}J_v(u)\Big]$$

### 三阶导与余项

同法再求一次， $k$ 层链式法则各贡献一个 $as$：

$$g_t'''(\tau)=a^3\!\!\sum_{i,j,k\in\{v,d\}}\!\!\partial^3_{ijk}J_v(u_\tau)\,s_is_js_k$$

$$g_t(1)=g_t(0)+\frac{g_t'(0)}{1!}+\frac{g_t''(0)}{2!}+\underbrace{\frac{g_t'''(\theta)}{3!}}_{=:\ R_3(t)}$$

因 $|s_i|\le1$：

$$\big|R_3(t)\big|=\frac{\big|g_t'''(\theta)\big|}{6}\le\frac{a^3}{6}\cdot 8M_3=\frac43M_3a^3$$

$$M_3:=\sup_{y\in K_a}\ \max_{i,j,k\in\{v,d\}}\big|\partial^3_{ijk}J_v(y)\big|,\qquad K_a:=\bigcup_{\tau\in[0,1]}\bar B_0(u_\tau)\ \subseteq\ \bar B_{\sqrt2a}(u)$$

### 代回

$$J_v(x)=J_v(u)+g_t'(0)+\tfrac12g_t''(0)+R_3(t)$$

$$\boxed{\ J_v(x)=J_v(u)+a\Big[\partial_vJ_v(u)s_v+\partial_dJ_v(u)s_d\Big]+\frac{a^2}{2}\Big[\partial^2_{vv}J_v(u)s_v^2+2\partial^2_{vd}J_v(u)s_vs_d+\partial^2_{dd}J_v(u)s_d^2\Big]+R_3(t)\ }$$

其中 $\big|R_3(t)\big|\le\tfrac43M_3a^3$ 对一切 $t$ 一致成立。

---

## Step 2　整体乘上 sv

$$J_v(x)\cdot s_v=J_v(u)\,s_v+a\Big[\partial_vJ_v(u)\,s_v^2+\partial_dJ_v(u)\,s_ds_v\Big]$$

$$\qquad+\frac{a^2}{2}\Big[\partial^2_{vv}J_v(u)\,s_v^3+2\partial^2_{vd}J_v(u)\,s_v^2s_d+\partial^2_{dd}J_v(u)\,s_d^2s_v\Big]+R_3(t)\,s_v$$

---

## Step 3　逐项取平均

### 零阶项

$$\overline{J_v(u)\,s_v}=J_v(u)\cdot\overline{\sin\omega_vt}=0$$

### 一阶项

$$\overline{s_v\cdot s_v}=\overline{\sin\omega_vt\cdot\sin\omega_vt}=\tfrac12$$

$$\overline{s_d\cdot s_v}=\overline{\sin\omega_dt\cdot\sin\omega_vt}=0\qquad(\omega_d\ne\omega_v,\ \text{均}>0)$$

$$\overline{a\Big[\partial_vJ_v(u)s_v^2+\partial_dJ_v(u)s_ds_v\Big]}=a\,\partial_vJ_v(u)\cdot\tfrac12+a\,\partial_dJ_v(u)\cdot 0=\frac{a}{2}\,\partial_vJ_v(u)$$

### 二阶项

$$\overline{s_v\cdot s_v\cdot s_v}=0,\qquad \overline{s_v^2\cdot s_d}=0,\qquad \overline{s_d^2\cdot s_v}=0$$

（三条均由 1.9 给出。）

### 余项

$$\big|R_3(t)\big|\le\tfrac43M_3a^3\ (\forall t)\ \Longrightarrow\ \big|R_3(t)\,s_v\big|\le\tfrac43M_3a^3\quad(\text{因 }|s_v|\le1)$$

对任意 $t_0$ 与 $T>0$：

$$\left|\frac{1}{T}\int_{t_0}^{t_0+T}R_3(t)\,s_v(t)\,\mathrm{d}t\right|\le\frac{1}{T}\int_{t_0}^{t_0+T}\big|R_3(t)s_v(t)\big|\,\mathrm{d}t\le\frac{1}{T}\cdot T\cdot\frac43M_3a^3=\frac43M_3a^3$$

界与 $t_0,T$ 均无关，所以

$$\limsup_{T\to\infty}\left|\frac{1}{T}\int_{t_0}^{t_0+T}R_3\,s_v\,\mathrm{d}t\right|\le\frac43M_3a^3=O(a^3)$$

---

## Step 4　合并并整理系数

$$\overline{J_v(x)\cdot s_v}=0+\frac{a}{2}\partial_vJ_v(u)+0+O(a^3)$$

$$\frac{2}{a}\cdot\overline{J_v(x)\cdot s_v}=\partial_vJ_v(u)+\frac{2}{a}O(a^3)$$

由 $M_3$ 与 $a$ 无关， $\dfrac{2}{a}\cdot O(a^3)=O(a^2)$，且常数为 $\dfrac83M_3$。故

$$\boxed{\ C_v=\frac{2}{a}\,\overline{J_v(x)\cdot\sin\omega_vt}=\partial_vJ_v(u)+O(a^2)\ }\quad\checkmark$$

---

## 2.5 诚实情形的 Cd

与 $C_v$ 同理：

$$\boxed{\ C_d=\frac{2}{a}\,\overline{J_d(x)\cdot\sin\omega_dt}=\partial_dJ_d(u)+O(a^2)\ }$$

$$\Longrightarrow\quad \text{每个玩家都拿到了自己代价对自己动作的偏导，互不串扰。}\qquad \textbf{(No Deception)}$$

---

## 2.6 注：为什么解调函数中要求三阶连续可微

前提： $J_v\in C^3$， $J_d\in C^3$。

### 定义

$$f\ \text{在}\ y_0\ \text{处连续}\ :\Longleftrightarrow\ \lim_{y\to y_0}f(y)=f(y_0)$$

$$J\in C^k\ :\Longleftrightarrow\ \text{所有 }k\text{ 阶偏导都存在，且都连续}$$

> 📌 二元函数的 $k$ 阶偏导共 $2^k$ 个； $k=3$ 时为 $8$ 个 $\partial^3_{ijk}J$（ $i,j,k\in\{v,d\}$）。**这 8 个就是余项估计里的项数。**

### 答（简）

因为余项要有一个**有限的界**，而这个有限的界需要三阶导数**连续**。

Taylor 展开到二阶后，余项是 $R_3=\dfrac{g'''(\theta)}{6}$，里面的中值点 $\theta$ 只知道存在、算不出来，还随 $t$ 变。既然算不出，只能对 $\theta$ 可能落到的那个闭球取最坏情况，即 $M_3=\sup_{\bar B}\big|\partial^3J_v\big|$。而 $\sup$ 要有限，靠的是**极值定理**：连续函数在紧集上有界。

闭球的紧致性是现成的，连续性则**由 $C^3$ 提供**。有了 $M_3<\infty$ 才有 $\big|R_3\big|\le\tfrac43M_3a^3$，才最终有 $O(a^2)$。

### 答（具体）

**① Taylor 展开到二阶，写成恒等式**

$$g(1)=g(0)+g'(0)+\tfrac12g''(0)+R_3$$

$R_3$ 就是余项，但我们并不知道它有多小。

**② 根据 Taylor 定理（Lagrange 余项）**

设 $g$ 在 $[0,1]$ 上 $n$ 阶连续可微、在 $(0,1)$ 内 $n+1$ 阶可导，则存在某个 $\theta\in(0,1)$ 使

$$g(1)=\sum_{k=0}^{n}\frac{g^{(k)}(0)}{k!}+\frac{g^{(n+1)}(\theta)}{(n+1)!}$$

取 $n=2$： $R_3=\dfrac{g'''(\theta)}{6}$，其中 $\theta=\theta(t)$ **随时间变化**。

**③ 根据多元链式法则**

$$\frac{\mathrm{d}}{\mathrm{d}\tau}F(u_\tau)=\sum_i\partial_iF(u_\tau)\cdot\frac{\mathrm{d}(u_\tau)_i}{\mathrm{d}\tau}$$

沿直线 $u_\tau=u+\tau as$ 有 $\dfrac{\mathrm{d}u_\tau}{\mathrm{d}\tau}=as$（常向量），反复用三次：

$$g_t'''(\tau)=a^3\!\!\sum_{i,j,k\in\{v,d\}}\!\!\partial^3_{ijk}J_v(u_\tau)\,s_is_js_k$$

代入 $\tau=\theta(t)$：

$$R_3(t)=\frac{a^3}{6}\sum_{i,j,k}\partial^3_{ijk}J_v\big(u_{\theta(t)}\big)\,s_i(t)s_j(t)s_k(t)$$

式子里**唯一未知的**就是求值点 $u_{\theta(t)}$； $a$、 $s_i(t)$、偏导的形式都已知。

**④ 关于 θ 我们只知道它属于开区间 (0, 1)**

由此

$$\big\|u_\theta-u\big\|=\theta a\|s\|\le a\sqrt{s_v^2+s_d^2}\le\sqrt2\,a$$

即 $u_\theta$ 一定落在闭球 $\bar B_{\sqrt2a}(u)$ 内。既然不知道具体在哪，那就对整个球取上确界：

$$M_3:=\sup_{y\in\bar B_{\sqrt2a}(u)}\ \max_{i,j,k}\big|\partial^3_{ijk}J_v(y)\big|$$

$$\big|R_3\big|\le\frac{a^3}{6}\sum_{i,j,k}\big|\partial^3_{ijk}J_v(u_\theta)\big|\,|s_i||s_j||s_k|\le\frac{a^3}{6}\sum_{i,j,k}\big|\partial^3_{ijk}J_v(u_\theta)\big|\le\frac{a^3}{6}\cdot 8\cdot M_3=\frac43M_3a^3$$

**⑤ 让上确界有限，所以要求 Jv 属于 C3**（即证明 $M_3<\infty$）

> **极值定理（Weierstrass）**：紧集上的连续函数有界，并且取到最大值。
>
> **Heine–Borel 定理**： $\mathbb{R}^n$ 中，紧 $\Longleftrightarrow$ 有界 + 闭。

$\bar B_{\sqrt2a}(u)$ 有界且闭，由 Heine–Borel 得出是紧集； $\partial^3_{ijk}J_v$ 连续（由 $C^3$ 给出）。故由极值定理得

$$\boxed{\ M_3<\infty\ }$$
