# Disciplina

> Prof. Alneu

> Atendimento

* Exercício em aula: 4 pessoas $\Longrightarrow$ reforço de conceitos
* Levar PC para a aula (programar!)
* <span style="color: ORANGE;  font-weight: bold"> Trabalhos práticos a serem divulgados no e-disciplinas </span>

> Avanço em grafos na disciplina de "Redes Complexas" (trilha IA).


## Definições

### Grafo

> Um grafo é tipo de representação simultânea de objetos (vértices, entidades) que possuem alguma relação entre si (arestas). Matematicamente, seja $E$ um conjunto de arestas e $V$ um conjunto de vértices, um grafo $G$ é dado por $G = (V, E)$. 
* Ordem de um grafo: $|V|$

Grafos orientados também são chamados de <u>dígrafos</u>.

⚠️ **Utilidade:** modelam sistemas/contextos de relacionamentos ordenados e contextualizados pela situação em si.


### Multigrafo

> Grafo que possui mais de uma aresta conectando um mesmo par de vértices.
 * Um grafo simples possui no máximo uma aresta por par de vértices.


### Grafo Trivial e Vazio
> Trivial: $V = \{v_1\}$, $E = \{\empty\}$

> Vazio: $G = \{\empty, \empty \}$


### Laço

> Consiste em uma aresta circular.
* $ V = \{v_1\}$, $E = \{(v_1, v_1)\}$


### Grafo Completo

> Um grafo no qual todos os seus vértices são adjacentes: extremos de uma mesma aresta.

$$
|E| = C_n^2 = \frac{n(n-1)}{2}
$$

### Grau

> O grau $d(v)$ de um vértice $v$ corresponde ao número de arestas incidentes (convergentes) a $v$.

#### Grafo Direcionado

Em grafos direcionados, dividimos $d(v)$ em $d_{in}(v)$ e $d_{out}(v)$, sendo o <u>grau de saída</u> $(d_{out})$ o número de arestas divergentes a $v$.

$$
\text{sorvedouro} \implies d_{out} = 0; \text{ fonte} \implies d_{in} = 0
$$

#### Grafo Regular

Um grafo regular possui o mesmo grau em todos os seus vértices.


### Grafo Valorado

> Possui pesos.

Nesse caso, cada aresta $A$ é composta pela tripla $\{v, w, valor\}$.


## Caminho

> Um caminho entre dois vértices $x$ e $y$ é uma sequência de vértices e arestas que une $x$ e $y$.
* Um caminho de $k$ vértices possa por $k-1$ arestas.
* Se o grafo não for **valorado**, o comprimento do caminho é a quantidade de arestas percorridas.


### Caminho (Não) Simples

> **Simples**: é composto apenas por vértices distintos.

> **Não simples**: pode possuir vértices iguais.


### Ciclo e Circuito 

> Um ciclo é um caminho $P = v_1, v_2,..., v_k, v_{k+1}$ em que $v_{k+1} = v_1$. Em outras palavras, em um ciclo todos os vértices são distintos, exceto pelo primeiro e pelo último.
* Se um grafo tem ao menos um ciclo, ele é cíclico.
* Em um **circuito**, todas as arestas são distintas, mas vértices podem ser repetidos.

###  Caminho Euleriano $vs$ Caminho Hamiltoniano

> **Euleriano:** Caminho que passa por <span style="color: ORANGE">**todas as arestas**</span> de um grafo, de modo a passar em <span style="color: ORANGE">**cada aresta apenas uma vez**</span>.

> **Hamiltoniano:** Caminho que passa em <span style="color: ORANGE">**todos os vértices**</span> de um grafo visitando cada <span style="color: ORANGE">**vértice apenas uma vez**</span>.

### Circuito Euleriano $vs$ Circuito Hamiltoniano

**Circuito Euleriano**: passa por todos as arestas do grafo exatamente 1 vez e, por consequência, todos os vértices (se o grafo for conexo). Sinônimo de ciclo euleriano. Volta ao vértice inicial.

**Circuito Hamiltoniano**: passo por todos os vértices do grafo exatamente 1 vez, exceto o primeiro e o último. Pode faltar arestas. Sinônimo de ciclo hamiltoniano.

⚠️ Um grafo euleriano/hamiltoniano é um grafo conexo que contém um circuito euleriano/hamiltoniano.

$$
E \implies A; \quad 
H \implies V
$$


### Grafo Fortemente Conexo

> É um grafo orientado no qual há um caminho entre todos os vértices.

### Mais sobre Grafos

#### Grafo Bipartido

> Um grafo $G = (V, E)$ é <u>bipartido</u> quando o seu conjunto de vértices $V$ puder ser dividido em dois subconjuntos $V_1$ e $V_2$ tais que toda aresta do conjunto $E$ une um vértice de $V_1$ a outro vértice de $V_2$.
* <span style="color: GREEN">**Em outras palavras, toda aresta  $e \in E$ liga vértices de diferentes conjuntos.**</span>


#### Bipartido Completo ($k_{|V_1|, |V_2|}$)

> Todo vértice de um conjunto se conecta a todos os vértices do outro conjunto.

#### Complemento
> O <u>complemento</u> de um grafo $G = (V, E)$ a um grafo $G' = (V', E')$ é tal que $V' = V$ e $E'$ é complementar a $E$.
* Em outras palavras, o complemento de um grafo $G$ são as arestas que poderiam ser inseridas.

### Isomorfismo

> Dois grafos são isomorfos se apresentam o mesmo número de vértices e arestas e existe uma função unívoca $f: V \implies V'$ tal que $e = (x, y) \in E \Leftrightarrow e = (f(x), f(y)) \in E'$.

### Árvore

> Grafo conexo e acíclico.

#### Árvore Enraizada

> É direcionada. A raiz funciona com uma <u>fonte</u> ($d_{in} = 0$).

### Floresta

> Conjunto de árvores.

### Subgrafos

#### Subgrafo Gerador

> Um subgrafo gerador de $G = (V, E)$ é tal que $G' = (V', E')$ e $V' = V$ com $E' \subseteq E"$
* O subgrafo tem o mesmo número de vértices do grafo original, mas com menos arestas.

#### Árvore Geradora

> A árvore geradora de um grafo é um subgrafo gerador que forma uma árvore.
* $|E'| = |V| - 1$
 
#### Subgrafo Induzido 

> É tal que $G' = (V', E')$ de modo que $V' \subseteq V$ e $E'$ possui todas as arestas que o grafo original tem entre elementos $(u, v) \in V'$.







