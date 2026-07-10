# Minimum Spanning Tree (MST)

## Algoritmo de Prim

* **Complexidade:** $O(E \log V)$

```text
Prim-MST(G, raiz)

    Init da fila de prioridade fp com todos os nós
    Init dos peso[u] = infinito para todo vértice u
    Init antecessor[u] = -1 (NIL) para todo vértice u
    peso[raiz] = 0

    enquanto não vazia(fp) faça
        u <- extrai_minimo(fp)
        
        para cada v adjacente a u faça

            Se na_fila(fp, v) e w(u, v) < peso[v] então
                antecessor[v] = u
                peso[v] = w(u, v)
                
                // V precisa ter um peso menor agora na fila
                fp.decrease_keys(v, peso[v]) 
            fim-se
            
        fim-para
    fim-enquanto
```

## Algoritmo de Kruskal
* Complexidade: $O(E \log E)$ (se implementado utilizando Union-Find)

Kruskal-MST(G)

    Definir Conjunto Sj: {vj}, 1 <= j <= n
    Et = vazio
    Init fp com arestas do conjunto
    
    enquanto houver arestas na fila faça
        e = unqueue(fp)
        seja (v, w) o par de vértices de e
        
        Se v in Sp e w in Sq, e são disjuntos, então
            Sp = Sp U Sq
            Eliminar Sq
            Et = Et U {e}
        fim-se
        
    fim-enquanto