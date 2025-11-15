---
title: Latex公式记录&练习
date: 2025-07-03 23:20:06
feed: show
---
#Latex

在md中插入Latex的用法：
+ 行内公式：`$公式$` 不要有空格，$f(x)=x^2$ 
+ 独立显示/多行公式 \$$ ... \$$   似乎推荐使用 `\[...\]`
+ \[f(x) = \dfrac{x}{y}\] 但在obsidian中并没有显示……可能有些冲突。
---
### 计算符

| 效果                         | 写法                          |
| -------------------------- | --------------------------- |
| $x \div y$                 | \$x\div y\$                 |
| $x \times y$               | \$ x \times y\$             |
| $\dfrac{x}{y}$             | \$\dfrac{x}{y}$             |
| $\pi \approx 3.14159$      | \$\pi \approx 3.14159$      |
| $\pm \, 0.2$               | \$\pm \, 0.2$               |
| $\dfrac{0}{1} \neq \infty$ | \$\dfrac{0}{1} \neq \infty$ |
| $0 < x < 1$                | \$0 < x < 1$                |
| $0 \leq x \leq 1$          | \$0 \leq x \leq 1$          |
| $x \geq 10$                | \$x \geq 10$                |
| $\dots$                    | $\dots$                     |

---
### 符号

```
1 $\pi \approx 3.14159$
2 $\pm \, 0.2$
3 $\dfrac{0}{1} \neq \infty$
4 $0 < x < 1$
5 $0 \leq x \leq 1$
6 $x \geq 10$
7 $\forall \, x \in (1,2)$
8 $\exists \, x \notin [0,1]$
9 $A \subset B$
10 $A \subseteq B$
11 $A \cup B$
12 $A \cap B$
13 $X \implies Y$
14 $X \impliedby Y$
15 $a \to b$
16 $a \longrightarrow b$
17 $a \Rightarrow b$
18 $a \Longrightarrow b$
19 $a \propto b$
20 $a \cdot b$
```
1. $\pi \approx 3.14159$
2. $\pm \, 0.2$
3. $\dfrac{0}{1} \neq \infty$
4. $0 < x < 1$
5. $0 \leq x \leq 1$
6. $x \geq 10$
7. $\forall \, x \in (1,2)$
8. $\exists \, x \notin [0,1]$
9. $A \subset B$
10. $A \subseteq B$
11. $A \cup B$
12. $A \cap B$
13. $X \implies Y$
14. $X \impliedby Y$
15. $a \to b$
16. $a \longrightarrow b$
17. $a \Rightarrow b$
18. $a \Longrightarrow b$
19. $a \propto b$
20. $a \cdot b$ 

```
- $\bar a$
- $\tilde a$
- $\breve a$
- $\hat a$
- $a^ \prime$
- $a^ \dagger$
- $a^ \ast$
- $a^ \star$
- $\mathcal A$
- $\mathrm a$
- $\cdots$
- $\vdots$
- $\#$
- $\$$
- $\%$
- $\&$
- $\{ \}$
- $\_$
```

- $\bar a$
- $\tilde a$
- $\breve a$
- $\hat a$
- $a^ \prime$
- $a^ \dagger$
- $a^ \ast$
- $a^ \star$
- $\mathcal A$
- $\mathrm a$
- $\cdots$
- $\vdots$
- $\#$
- $\$$
- $\%$
- $\&$
- $\{ \}$
- $\_$
---
### 空格
- 水平间距: `\quad`
- 大水平间距: `\qquad`
- 小间距: `\,`
- 中等: `\:`
- 大间距: `\;`
- 负间距: `\!`
---
### Greek alphabets 希腊字母
| Small Letter | Capital Letter        | Alternative     |
| ------------ | --------------------- | --------------- |
| α `\alpha`   | A `A`                 |                 |
| β `\beta`    | B `B`                 |                 |
| γ `\gamma`   | Γ `\Gamma`            |                 |
| δ `\delta`   | Δ `\Delta`            |                 |
| ϵ `\epsilon` | E `E`                 | ε `\varepsilon` |
| ζ `\zeta`    | Z `Z`                 |                 |
| η `\eta`     | H `H`                 |                 |
| θ `\theta`   | Θ `\Theta`            | ϑ `\vartheta`   |
| ι `\zeta`    | I `I`                 |                 |
| κ `\kappa`   | K `K`                 | ϰ `\varkappa`   |
| λ `\lambda`  | Λ `\Lambda`           |                 |
| μ `\mu`      | M `M`                 |                 |
| ν `\nu`      | N `N`                 |                 |
| ξ `\xi`      | Ξ `\Xi`               |                 |
| ο `\omicron` | O `O`                 |                 |
| π `\pi`      | Π `\Pi`               | ϖ `\varpi`      |
| ρ `\rho`     | P `P`                 | ϱ `\varrho`     |
| σ `\sigma`   | Σ `\Sigma`            | ς `\varsigma`   |
| τ `\tau`     | T `T`                 |                 |
| υ `\upsilon` | Υ `\Upsilon`          |                 |
| ϕ `\phi`     | Φ `\Phi`              | φ `\varphi`     |
| χ `\chi`     | X `X`                 |                 |
| ψ `\psi`     | Ψ `\Psi`              |                 |
| ω `\omega`   | Ω `\Omega`            |                 |
|              | $\partial$ `\partial` |                 |

---

$$
\begin{align}
\boxed{E=\frac{1}{2\pi \epsilon_0}\frac{Q}{r\sqrt{4r^2+L^2}}}
\end{align}
$$


---
### Equations 方程
  
$$\mathbb{N} = \{ a \in \mathbb{Z} : a > 0 \}$$

```
$$\mathbb{N} = \{ a \in \mathbb{Z} : a > 0 \}$$
```

$$\forall \; x \in X \quad \exists \; y \leq \epsilon$$

```
$$\forall \; x \in X \quad \exists \; y \leq \epsilon$$
```

$$\color{blue}{X \sim Normal \; (\mu,\sigma^2)}$$

```
$$\color{blue}{X \sim Normal \; (\mu,\sigma^2)}$$
```

$$P \left( A=2 \, \middle| \, \dfrac{A^2}{B}>4 \right)$$

```
$$P \left( A=2 \, \middle| \, \dfrac{A^2}{B}>4 \right)$$
```

$$f(x) = x^2 - x^\frac{1}{\pi}$$

```
$$f(x) = x^2 - x^\frac{1}{\pi}$$
```

$$f(X,n) = X_n + X_{n-1}$$

```
$$f(X,n) = X_n + X_{n-1}$$
```

$$f(x) = \sqrt[3]{2x} + \sqrt{x-2}$$

```
$$f(x) = \sqrt[3]{2x} + \sqrt{x-2}$$
```

$$\mathrm{e} = \sum_{n=0}^{\infty} \dfrac{1}{n!}$$

```
$$\mathrm{e} = \sum_{n=0}^{\infty} \dfrac{1}{n!}$$
```

$$\prod_{i=1}^{n} x_i - 1$$

```
$$\prod_{i=1}^{n} x_i - 1$$
```

$$\lim_{x \to 0^+} \dfrac{1}{x} = \infty$$

```
$$\lim_{x \to 0^+} \dfrac{1}{x} = \infty$$
```

$$\int_a^b y \: \mathrm{d}x$$
```
$$\int_a^b y \: \mathrm{d}x$$
```
$$
\oint x \mathrm{d}x
$$
```
$$\oint x \mathrm{d}x$$
```

$$\log_a b = 1$$

```
$$\log_a b = 1$$
```

$$\max(S) = \max_{i:S_i \in S} S_i$$

```
$$\max(S) = \max_{i:S_i \in S} S_i$$
```

$$\dfrac{n!}{k!(n-k)!} = \binom{n}{k}$$

```
$$\dfrac{n!}{k!(n-k)!} = \binom{n}{k}$$
```

$$\text{$\dfrac{b}{a+b}=3, \:$ therefore we can set $\: a=6$}$$

```
$$\text{$\dfrac{b}{a+b}=3, \:$ therefore we can set $\: a=6$}$$
```
---
### 函数

$$
f(x)=
\begin{cases}
1/d_{ij} & \quad \text{when $d_{ij} \leq 160$}\\ 
0 & \quad \text{otherwise}
\end{cases}
$$
```
$$
f(x)=
\begin{cases}
1/d_{ij} & \quad \text{when $d_{ij} \leq 160$}\\ 
0 & \quad \text{otherwise}
\end{cases}
$$
```
---
### Matrices 矩阵
$$
\begin{matrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
$$
```
$$
\begin{matrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
$$
```
$$
M = 
\begin{bmatrix}
\frac{5}{6} & \frac{1}{6} & 0 \\[0.3em]
\frac{5}{6} & 0 & \frac{1}{6} \\[0.3em]
0 & \frac{5}{6} & \frac{1}{6}
\end{bmatrix}
$$
```
$$
M = 
\begin{bmatrix}
\frac{5}{6} & \frac{1}{6} & 0 \\[0.3em]
\frac{5}{6} & 0 & \frac{1}{6} \\[0.3em]
0 & \frac{5}{6} & \frac{1}{6}
\end{bmatrix}
$$
```
$$ 
M =
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
$$
```
$$ 
M =
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
$$
```
$$ 
M =
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}
$$
```
$$ 
M =
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}
$$
```
$$
A_{m,n} = 
\begin{pmatrix}
a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\
a_{2,1} & a_{2,2} & \cdots & a_{2,n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m,1} & a_{m,2} & \cdots & a_{m,n} 
\end{pmatrix}
$$
```
$$
A_{m,n} = 
\begin{pmatrix}
a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\
a_{2,1} & a_{2,2} & \cdots & a_{2,n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m,1} & a_{m,2} & \cdots & a_{m,n} 
\end{pmatrix}
$$
```
---
### 字体大小

$\Huge Hello!$
$\huge Hello!$
$\LARGE Hello!$
$\Large Hello!$
$\large Hello!$
$\normalsize Hello!$
$\small Hello!$
$\scriptsize Hello!$
$\tiny Hello!$
```
$\Huge Hello!$
$\huge Hello!$
$\LARGE Hello!$
$\Large Hello!$
$\large Hello!$
$\normalsize Hello!$
$\small Hello!$
$\scriptsize Hello!$
$\tiny Hello!$
```
Example:$$\small \text{Font size is small, eg. $\sum{x_i = 10}$}$$
```
$$\small \text{Font size is small, eg. $\sum{x_i = 10}$}$$
```

### 向量/矢量
```shell
%% 加粗 %%
\boldsymbol{v} = CNN(s)
```
$\boldsymbol{v} = CNN(s)$ 
```shell
%% 加箭头 %%
\vec(v) = CNN(s)
```
$\vec{v} = CNN(s)$ 