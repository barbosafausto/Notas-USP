# Fluxo

Dados o campo vetorial $\vec{F}(x, y, z)$ e uma superfície $S$ ($S \subset \text{Dom}(\vec{F})$) regular, orientável e orientada por um campo vetorial $\vec{n}$, em que $\vec{n}$ é o versor que representa uma das duas possíveis orientações da superfície, define-se **Fluxo de $F$ através de $S$**:
$$
\iint_S \langle \vec{F},\vec{n} \rangle \text{ } dA = \iint_{D_{uv}} \langle \vec{F}, \frac{\vec{\gamma}_u \times \vec{\gamma}_v}{||\vec{\gamma}_u \times \vec{\gamma}_v||} \rangle ||\vec{\gamma}_u \times \vec{\gamma}_v|| dudv
$$
$$
\therefore \boxed{\iint_{D_{uv}} \langle \vec{F}, \vec{\gamma}_u \times \vec{\gamma}_v \rangle dudv}
$$

⚠️ A dedução é análoga à de integrais de linha, em que queremos calcular a componente de $\vec{F}$ paralela a $\vec{n}$ no domínio de interesse (projetamos o campo na direção normal à superfície).

⚠️ O módulo de $\vec{\gamma}_u \times \vec{\gamma}_v$ representa o fator de correção (análogo ao Jacobiano) da parametrização $(u, v) \to (x, y, z)$.

## Notação Alternativa

O integrando $\langle \vec{F}, \vec{\gamma}_u \times \vec{\gamma}_v \rangle dudv$ pode ser reescrito em termos das formas diferenciais em $(x, y, z)$:

$$
\vec{\gamma}_u \times \vec{\gamma}_v = \left(
\begin{vmatrix}
\frac{\partial y}{\partial u} \quad \frac{\partial z}{\partial u}
\\
\\
\frac{\partial y}{\partial v} \quad \frac{\partial z}{\partial v} \\
\end{vmatrix}
,
-
\begin{vmatrix}
\frac{\partial x}{\partial u} \quad \frac{\partial z}{\partial u}
\\
\\
\frac{\partial x}{\partial v} \quad \frac{\partial z}{\partial v} \\
\end{vmatrix}
,
\begin{vmatrix}
\frac{\partial x}{\partial u} \quad \frac{\partial y}{\partial u}
\\
\\
\frac{\partial x}{\partial v} \quad \frac{\partial y}{\partial v} \\
\end{vmatrix}
\right)
$$

Ao multiplicarmos pelos diferenciais $dudv$, obtemos a relação:
$$
\vec{\gamma}_u \times \vec{\gamma}_v \text{ } dudv = (dy \wedge dz, dz \wedge dx, dx \wedge dy)
$$

Logo, a integral ganha a forma:
$$
\boxed{\iint_S P(dy \wedge dz) + Q(dz \wedge dx) + R(dx \wedge dy)}
$$


## Campo $\vec{F} = \frac{\vec{r}}{r^3}$

Similar ao campo $d\theta$, esse campo tem fluxo constante em superfícies fechadas que englobam a origem. Ele não depende da superfície.

Vamos calcular o seu fluxo na superfície $S$ de uma esfera centrada na origem:
$$
x^2 + y^2 + z^2 = r^2
$$

Logo, como o vetor normal normalizado $\hat{n}$ da esfera corresponde ao vetor radial $\frac{\vec{r}}{r}$:
$$
\oiint_S \vec{F}\cdot \hat{n}\text{ } dS = \oiint_S \frac{\vec{r}}{r^3}\cdot \frac{\vec{r}}{r} \text{ } dS = \oiint_S \frac{r^2}{r^4}\text{ } dS = \frac{1}{r^2}\oiint_S dS 
$$

Como a integral dupla de $f(x) = 1$ em uma superfície resulta na área da própria superfície, temos:
$$
= \frac{1}{r^2}\cdot 4\pi r^2 = \boxed{4\pi}
$$

⚠️ Importante: $\text{div } \vec{F} = 0$ (para $(x,y,z) \neq (0,0,0)$).
* Depois, vamos ver que esse campo tem fluxo nulo se a superfície fechada **não** envelopar a origem (Teorema da Divergência).
* Acabamos de ver a definição de ângulo sólido. 🆒