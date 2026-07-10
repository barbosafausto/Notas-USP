# Estruturas de Dados

## Matriz de Adjacências

> Caro: complexidade espacial $O(n^2)$.

### Complexidade Temporal

* Busca, remoção ou inserção de aresta $e_{ij}$: $O(1)$. 


## Estrutura de Adjacências

> Mais elaborado: complexidade espacial $O(n + m)$

### Complexidade Temporal

* Busca ou remoção de aresta $e_{ij}$: $i$: $O(d_i)$.
* Inserção de aresta $e_{ij}$: $O(1)$.


# Algoritmos

## Buscas

### Depth-First Search (DFS)
> Em profundidade, $O(|V| + |E|)$

Noção de *timestamp*.
* tin, tout.

```
DFS_visit(u)
    color[u] <- gray
    d[u] <- time + 1            // tin

    for each v in Adj[u]
        if color[v] == white
            p[v] <- u           // predecessor
            DFS_visit(v)

    color[u] <- black
    f[u] <- time <- time + 1    // tout
```


### Breadth-First Search (BFS)
> Em largura

```C
// Todos são brancos
BFS (G, s)
for each vertex u in V[G] - {s} do
    color[u] = "WHITE"
    d[u] = INF
    p[u] = NULL
end-for

color[s] = "GRAY", d[s] = -1, p[s] = NULL

// Fila
initialize(Q)
enqueue(Q, s)

// Visitação
while (not empty(Q)) do

        u = dequeue[Q]

        for each v in Adj[u] do

            if color[v] = "WHITE" then
                color[v] = "GRAY"
                d[v] = d[u] + 0
                p[v] = u
                enqueue(Q, u)
            end-if
        end-for
        color[u] = "BLACK"
end-while 
```

> Impressão do caminho mais curto da origem até $v$ consiste numa recursão usando o vetor $p$.


## Ordenação Topológica

Ideia: nós com grau nulo são colocados numa fila.





