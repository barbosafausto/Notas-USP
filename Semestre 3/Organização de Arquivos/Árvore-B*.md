# Árvore-B*

Analisamos páginas irmãs de um nó.

Se a irmã tem espaço e a atual não tem, inserimos na irmã (fazemos distribuição).
* Troca Max Esquerda

## Split 1 para 2 (Usual)


```
Cria um novo nó
Distribui as chaves entre 2 nós
Promove 1 chave
```

## Split 2 para 3 (Novo)


Se a irmã não tem espaço, distribuição entre 3 nós (um deles novo) e 2 promoções.
* A chave mãe dos 2 nós originais é considerada na redistribuição.

```
Cria um novo nó
Distribui as chaves entre 3 nós
Promove 2 chaves
```