# Resumo: Fluxo Máximo em Grafos

## 1. Definição do Problema
O problema de fluxo máximo em uma rede consiste em descobrir a **maior taxa** pela qual materiais podem ser enviados de um vértice de origem (fonte $s$) para um vértice de destino (sorvedouro $t$), sem violar as restrições de capacidade da rede.

---

## 2. Rede de Fluxo
Uma rede de fluxo $G(V, E)$ é um grafo direcionado onde cada aresta $(u,v)$ possui uma **capacidade não negativa** denotada por $c(u,v) \ge 0$.
* **Ausência de aresta:** Se não existe uma aresta conectando $u$ e $v$, então $c(u,v) = 0$.
* **Arestas antiparalelas:** Em modelos estritos, se existe a aresta $(u,v)$, impõe-se que não exista $(v,u)$. (Isso pode ser resolvido criando vértices e arestas equivalentes).
* **Conectividade:** Para todo vértice $v \in V$, assume-se que existe um caminho da fonte $s$ para $v$ e de $v$ para o sorvedouro $t$.
* **Múltiplas fontes e sorvedouros:** Pode-se adaptar o problema adicionando uma "superfonte" e um "supersorvedouro" conectados aos originais por arestas de capacidade infinita.

---

## 3. Propriedades do Fluxo
Um fluxo é uma função $f(u,v)$ que deve respeitar duas regras principais:

1. **Restrição de Capacidade:** O fluxo em uma aresta nunca pode exceder a sua capacidade e não pode ser negativo.
   $$0 \le f(u,v) \le c(u,v)$$
   
2. **Conservação de Fluxo:** Para todo vértice $u$ (exceto a fonte $s$ e o sorvedouro $t$), a soma do fluxo que entra deve ser exatamente igual à soma do fluxo que sai. Os vértices não acumulam material.
   $$\sum_{v \in V} f(v,u) = \sum_{v \in V} f(u,v)$$

O **valor total do fluxo** $|f|$ é definido como a quantidade de material que sai da fonte menos o que retorna para ela.

---

## 4. Conceitos Fundamentais para a Resolução

### 4.1. Rede Residual ($G_f$)
A rede residual mostra **como o fluxo pode ser alterado** nas arestas da rede original $G$. A capacidade residual $c_f(u,v)$ de uma aresta é dada por:
* No sentido original: $c(u,v) - f(u,v)$, pois a aresta $(u,v)$ existe nessa direção (calcula-se o quanto ainda cabe).
* No sentido oposto: $f(u, v)$, pois a aresta $(v, u)$ não existe (calcula-se quanto é preciso "devolver" para cancelar um fluxo já enviado).
* $0$ caso a aresta não exista.

### 4.2. Caminho Aumentador
É um caminho simples da fonte $s$ até o sorvedouro $t$ que existe na **rede residual** $G_f$.
* A capacidade deste caminho, $c_f(p)$, é determinada pelo menor valor de capacidade residual (o gargalo) entre as arestas que compõem o caminho.
* $c_f(p) = \min\{c_f(u,v) : (u,v) \in p\}$.

---

## 5. Teorema do Fluxo Máximo / Corte Mínimo
Um **corte** $(S,T)$ é uma partição dos vértices onde $s \in S$ e $t \in T$. O teorema afirma que, se $f$ é um fluxo, as três condições abaixo são matemática e logicamente **equivalentes**:
1. $f$ é o fluxo máximo em $G$.
2. A rede residual $G_f$ não possui nenhum caminho aumentador.
3. O valor do fluxo $|f|$ é igual à capacidade de algum corte $c(S,T)$ (neste caso, o corte mínimo).

---

## 6. Algoritmo de Ford-Fulkerson
O método de Ford-Fulkerson encontra o fluxo máximo iterativamente, buscando caminhos aumentadores na rede residual até que nenhum outro possa ser encontrado em $O(E\cdot|f_{max}|)$

**Pseudocódigo Básico:**
1. Inicializar o fluxo $f = 0$ para cada aresta $(u,v)$ em $G$.
2. **Enquanto** existir um caminho aumentador $p$ de $s$ a $t$ na rede residual $G_f$:
   * Encontrar o gargalo do caminho: $c_f(p) = \min\{c_f(u,v) : (u,v) \in p\}$
   * **Para** cada aresta $(u,v)$ no caminho $p$:
      * Se $(u,v)$ pertence às arestas originais $E$, aumenta o fluxo: $f(u,v) = f(u,v) + c_f(p)$
      * Caso contrário (é uma aresta de devolução), reduz o fluxo: $f(v,u) = f(v,u) - c_f(p)$
3. **Retornar** o fluxo final $f$.