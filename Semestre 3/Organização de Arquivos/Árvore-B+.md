# Árvore-B+

Possui acesso indexado **e** sequencial.

* Árvore-B é ótima para *point-query*.
* Árvore-B+ é ótima para *range-query*.

É análoga a uma *Segment Tree*. Os arquivos são as folhas.


# Árvore-B+ Pré-Fixada

Define primeiro o *overflow* e *underflow* e se tem redistribuição na inserção (árvore-b*).

Enquanto não enche a raiz, o nó todo é um arquivo.

*Overflow*? Split, mas liga os nós irmãos (A $\to$ B).
* Esquerda: $\lceil m/2 \rceil$; Direita: $\lfloor m/2 \rfloor$
* Split no primeiro arquivo (raiz): cria primeiro nó da árvore
 
Nó pai divide os filhos (usual), diferença é que apenas as folhas são arquivos.
* O pai tem a quantidade mínima de caracteres que separa os filhos




