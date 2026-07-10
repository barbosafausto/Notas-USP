# Teorema de Gauss (Teorema da Divergência)

A taxa líquida com que uma grandeza (ou fluido) sai de uma região infinitesimal pode ser descrita pelo seu divergente. Seja $\vec{F} = (P, Q, R)$ o campo vetorial que descreve essa grandeza, o seu divergente pode ser denotado por $\text{div }\vec{F}$ ou $\vec{\nabla} \cdot \vec{F}$ e é dado por:

$$
\text{div }\vec{F} = \vec{\nabla} \cdot \vec{F} = \frac{\partial{P}}{\partial x} + \frac{\partial{Q}}{\partial y} + \frac{\partial{R}}{\partial z}
$$

❗ Note que o divergente de um campo vetorial resulta em um campo escalar.

⚠️ Para uma região sólida macroscópica, basta integrar (somar) essa quantidade em todo o volume. Os fluxos internos entre os cubos infinitesimais vizinhos se cancelam, restando apenas o fluxo que atravessa a fronteira externa.

📓 $\text{div }\vec{F} = 0 \implies$ o campo é incompressível (massa/fluido é preservada, sem fontes nem sumidouros).

Gauss formalizou que é possível relacionar a integral do divergente de $\vec{F}$ ao longo de uma região sólida $V$ com o fluxo de $\vec{F}$ através da superfície fechada $\partial V$ que limita esse sólido (com orientação normal para fora). Matematicamente:

$$
\iiint_{V} (\vec{\nabla} \cdot \vec{F}) \, dV = \oiint_{\partial V} (\vec{F}\cdot \vec{n}) \, dS
$$

De fato, analisar a quantidade total de $\vec{F}$ gerada ou consumida dentro de um corpo é equivalente a analisar o quanto passa pela sua superfície externa.

# Teorema de Stokes

O Teorema de Stokes é a generalização tridimensional do Teorema de Green. Ele associa a integral do rotacional sobre uma superfície aberta $S$ com a integral de linha do campo ao longo da curva de fronteira $\partial S$.

Matematicamente, utilizando as notações já estabelecidas:

$$
\iint_S (\vec{\nabla} \times \vec{F}) \cdot \vec{n} \, dS = \oint_{\partial S} Pdx + Qdy + Rdz
$$

Para o teorema ser válido, são necessárias as seguintes condições de regularidade e orientação:
* O bordo $\partial S$ é percorrido exatamente uma vez.
* $\partial S$ é uma curva fechada simples, regular por partes.
* A orientação da curva fronteira $\partial S$ deve ser coerente com a orientação do vetor normal $\vec{n}$ da superfície $S$, seguindo a **regra da mão direita** (com o dedão apontando na direção de $\vec{n}$, os dedos indicam o sentido de percurso da curva).

❗ Em superfícies fechadas (como uma esfera completa), a fronteira é vazia ($\partial S = \emptyset$). Portanto, a integral de linha no bordo é zero, o que implica que o fluxo do rotacional através de qualquer superfície fechada é sempre zero.


## Identidades e Insights Importantes

❗ **O divergente do rotacional de um campo é sempre nulo:**
$$
\text{div}(\text{rot }\vec{F}) = \vec{\nabla} \cdot (\vec{\nabla} \times \vec{F}) = 0
$$
*Geometricamente:* Tudo o que o rotacional faz girar entra e sai de uma região infinitesimal na mesma proporção; ele não cria "fontes" de escoamento.

❗❗ **O rotacional de um gradiente é sempre nulo:**
$$
\text{rot}(\vec{\nabla}\phi) = \vec{\nabla} \times (\vec{\nabla}\phi) = \vec{0}
$$
*Consequência:* Campos conservativos (que vêm de um potencial escalar $\phi$) não possuem rotação local (são irrotacionais).

❗❗❗ **O fluxo do rotacional depende exclusivamente do bordo da superfície:**
* Pelo Teorema de Stokes, o fluxo de $\vec{\nabla} \times \vec{F}$ através de $S$ depende apenas da integral de linha em $\partial S$.
* Se duas superfícies distintas, $S_1$ e $S_2$, compartilham exatamente a mesma curva de fronteira $\partial S$, o fluxo do rotacional através de ambas será rigorosamente o mesmo.