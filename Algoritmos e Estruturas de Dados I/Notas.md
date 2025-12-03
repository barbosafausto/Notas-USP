# Resumo - Árvores Binárias 🌲

* Árvore Binária de Busca (ABB)
* AVL
* Fila de Prioridade (Heap)
* Árvore Rubro-Negra (LLRB)

> Os arquivos das pastas estão incompletos e podem ter erros, mas este README está finalizado. 🥇

## Árvore Binária de Busca 

### Struct 
```C
typedef struct no NO;
typedef struct abb ABB;

struct no {
    ITEM *item;
    NO *esq;
    NO *dir;
};

struct abb {
    NO *raiz;
};
```

---

### Balanceada ⚖️

    Para toda raiz de uma subárvore, a altura de seus dois filhos difere em, no máximo, 1.

> **Ideia**: recursão em pós-ordem retornando, para cada nó, a maior altura entre as alturas dos seus filhos somada de uma unidade.

```C
int balanceada(NO *raiz) {

    if (!raiz) return 0;

    int altura_esq = balanceada(raiz->esq);
    int altura_dir = balanceada(raiz->dir);

    //-1 indica que a árvore não está balanceada
    if (abs(altura_esq - altura_dir) > 1) return -1;

    return max(altura_esq, altura_dir) + 1;

}
```

---

### Perfeitamente Balanceada ⚖️ ⚖️
    Para toda raiz de uma subárvore, a quantidade de nós de seus dois filhos difere em, no máximo, 1.

> **Ideia**: recursão em pós-ordem retornando, para cada nó, a quantidade de filhos dos seus filhos somada de uma unidade.

### Completa 

    As folhas estão no penúltimo e último níveis da árvore. Além disso, as folhas do último nível estão à esquerda.


### Completa Cheia

    O último nível da árvore está completo.

---

### Inserção 🟢

```C
NO *abb_inserir_no(NO *raiz, int valor) {
    
    if (!raiz) {

        NO *novo = abb_criar_no(valor);
        return novo;
    }

    if (valor < raiz->valor)
        raiz->esq = abb_inserir_no(raiz->esq, valor);
        
    else if (valor > raiz->valor)
        raiz->dir = abb_inserir_no(raiz->dir, valor);

    return raiz;
}
```

---
### Remoção 🔴
```C
NO *troca_max_esq(NO *troca, NO *raiz) {

    if (troca->dir) 
        troca->dir = troca_max_esq(troca->dir, raiz);

    else {

        raiz->valor = troca->valor;

        free(troca);
        troca = NULL;
    }

    return troca;
}

NO *abb_remover_no(NO *raiz, int valor) {

    if (!raiz) {
        printf("Valor não está na árvore");
        return NULL;
    }

    if (valor < raiz->valor)
        raiz->esq = abb_remover_no(raiz->esq, valor);

    else if (valor > raiz->valor)
        raiz->dir = abb_remover_no(raiz->dir, valor);

    else {
        
        if (!raiz->esq) {

            NO *aux = raiz->dir;
            free(raiz);
        
            return aux;
        }

        else if (!raiz->dir) {

            NO *aux = raiz->esq;
            free(raiz);

            return aux;
        }

        else {

            raiz->esq = troca_max_esq(raiz->esq, raiz);
        }
    }

    return raiz;
}
```

## AVL 1️⃣

### Struct
```C
typedef struct no NO;
typedef struct avl AVL;

struct no {
    ITEM *item;
    NO *esq;
    NO *dir;
    int altura;
};

struct avl {
    NO *raiz;
};
```

---
### Rotações

```C
NO *roda_esquerda(NO *A) {

    //Se a rotação é para a esquerda, B está à direita.
    NO *B = A->dir;

    //O filho esquerdo de B é adotado por A
    A->dir = B->esq

    //B sobe
    B->esq = A;

    A->altura = max(altura(A->esq), altura(A->dir)) + 1;
    B->altura = max(altura(B->esq), altura(B->dir)) + 1;

    return B;
}

NO *roda_direita(NO *A) {

    //Mesma ideia

    NO *B = A->esq;

    A->esq = B->dir;
    B->dir = A;

    A->altura = max(altura(A->esq), altura(A->dir)) + 1;
    B->altura = max(altura(B->esq), altura(B->dir)) + 1;
    return B;
}

NO *roda_esq_dir(NO *A) {

    //Terminando girando para direita, então B está à esquerda.
    A->esq = roda_esquerda(A->esq);

    return roda_direita(A);
}

NO *roda_dir_esq(NO *A) {

    //Análogo
    A->dir = roda_direita(A->dir);

    return roda_esquerda(A);
}
```

---

### Inserção

```C
NO *avl_balanceia(NO *raiz) {

    if (!raiz) return NULL;
    
    raiz->altura = max(avl_altura(raiz->esq), avl_altura(raiz->dir)) + 1;
    int fb = avl_calcula_fb(raiz);

    int fb_filho;
    if (fb >= 2) {

        fb_filho = avl_calcula_fb(raiz->esq);

        if (fb_filho >= 0) raiz = avl_roda_direita(raiz);
        else raiz = avl_roda_esq_dir(raiz);
    }

    else if (fb <= -2) {

        fb_filho = avl_calcula_fb(raiz->dir);

        if (fb_filho <= 0) raiz = avl_roda_esquerda(raiz);
        else raiz = avl_roda_dir_esq(raiz);
    }

    return raiz;
}

NO *avl_inserir_no(NO *raiz, int valor) {

    if (raiz == NULL) {

        NO *node = avl_criar_no(valor);
        return node;
    }

    if (valor < raiz->valor)
        raiz->esq = avl_inserir_no(raiz->esq, valor);
    
    else if (valor > raiz->valor)
        raiz->dir = avl_inserir_no(raiz->dir, valor);

    //Rebalanceamento (Volta da recursão)
    return avl_balanceia(raiz);
}
```

---

### Remoção

```C
NO *troca_max_esq(NO *troca, NO *raiz) {

    if (troca->dir) troca->dir = troca_max_esq(troca->dir, raiz);

    else {
        //Se entrou aqui, não tem mais nós à direita.
        raiz->valor = troca->valor;

        NO *aux = troca->esq;
        free(troca);

        return aux;
    }

    //Lógica de Balanceamento (Igual à Inserção)
    return avl_balanceia(troca);
}
NO *avl_remover_no(NO *raiz, int valor) {

    if (!raiz) return NULL; //Valor não encontrado.

    if (valor < raiz->valor)
        raiz->esq = avl_remover_no(raiz->esq, valor);
    
    else if (valor > raiz->valor)
        raiz->dir = avl_remover_no(raiz->dir, valor);

    else {

        //Caso 1: 0 ou 1 filho
        if (!raiz->esq || !raiz->dir) {

            NO *tmp;
            if (raiz->esq) {

                tmp = raiz->esq;
                free(raiz);
                raiz = NULL;

                return tmp;
            }

            else {
                tmp = raiz->dir;
                free(raiz);
                raiz = NULL;

                return tmp;
            }
        }

        else { 
            //Caso 2: tem 2 filhos
            raiz->esq = troca_max_esq(raiz->esq, raiz);
        }
    }

    //Lógica de Balanceamento (Igual à Inserção).
    return avl_balanceia(raiz);
}
```


## Fila de Prioridade

```C
#define maxn 1000

typedef struct heap HEAP;

struct heap {
    ITEM *fila[maxn]; //É um vetor de nós
    int fim;
    int tam;
}
```

---

### Inserção

```C
void heap_fix_up(HEAP *heap) { 

    //Min-Heap

    int atual = heap->fim;
    int pai = (atual-1)/2;

    while (atual > 0 && heap->fila[atual] < heap->fila[pai]) {

        heap_swap(heap, atual, pai);

        atual = pai;
        pai = (pai-1)/2;
    }
}

bool heap_inserir(HEAP *heap, int valor) {

    if (!heap || heap_cheia(heap)) return false;

    heap->fim++;
    heap->fila[heap->fim] = valor;

    heap_fix_up(heap);

    return true;

}
```

---

### Remoção

```C
void heap_fix_down(HEAP *heap) {

    //Min-Heap

    int atual = 0;
    int filho1 = 2*atual + 1;
    int filho2 = 2*atual + 2;

    int menor;
    while (filho1 <= heap->fim) {
        
        menor = atual;
        if (heap->fila[filho1] < heap->fila[menor])
            menor = filho1;

        if (filho2 <= heap->fim &&
            heap->fila[filho2] < heap->fila[menor])
            menor = filho2;

        if (menor == atual) break;
        swap(heap, atual, menor);

        atual = menor;
        filho1 = 2*atual + 1;
        filho2 = 2*atual + 2;
    }
}


int heap_remover(HEAP *heap) {

    if (!heap || heap_vazia(heap)) return false;

    int valor = heap->fila[0];

    heap->fila[0] = heap->fila[heap->fim];
    heap->fim--;

    heap_fix_down(heap);

    return valor;

}
```


## Árvore Rubro-Negra

### Struct
```C
typedef struct no NO;
typedef struct llrb LLRB;

struct no {

    ITEM *item;
    NO *esq;
    NO *dir;
    bool cor; //vermelho = true
};

struct llrb {
    NO *raiz;
};
```

---

### Inversão de Cores

* Se os dois filhos de um nó forem vermelhos, tornamos eles negros e o nó pai fica vermelho.

```C
void llrb_inverte(NO *node) {   

    node->cor = !node->cor;

    node->esq->cor = !node->esq->cor;
    node->dir->cor = !node->dir->cor;
}
```

### Rotações

* Iguais às rotações da AVL.

### Inserção

* Igual à inserção em uma ABB, com a diferença de que temos que corrigir 3 possíveis violações da estrutura.

```C
NO *llrb_inserir_no(NO *raiz, int valor) {

    if (!raiz) {

        NO* node = llrb_cria_no(valor);
        return node;
    }

    if (valor < item_get_chave(raiz->item))
        raiz->esq = llrb_inserir_no(raiz->esq, valor);
    else if (valor > item_get_chave(raiz->item))
        raiz->dir = llrb_inserir_no(raiz->dir, valor);

    //Volta da recursão: hora de corrigir violações
    if (eh_vermelho(raiz->dir) && !eh_vermelho(raiz->esq)) 
        raiz = llrb_roda_esquerda(raiz);

    if (eh_vermelho(raiz->esq) && eh_vermelho(raiz->esq->esq)) 
        raiz = llrb_roda_direita(raiz);
    
    if ((eh_vermelho(raiz->esq) && eh_vermelho(raiz->dir))) 
        llrb_inverte(raiz);

}
```

---

### Remoção

A remoção em uma LLRB é consideravelmente complexa, mas com o tempo é possível perceber o padrão que deve ser respeitado:

* Antes de continuar a recursão, é necessário propagar a cor vermelha; 
* Antes de propagar, é necessário ver se a propagação é necessária.

> **Propagação Esquerda**
* Só é necessária se `raiz->esq` e `raiz->esq->esq` são ambos pretos.

> **Propagação Direita**
* Só é necessária se `raiz->dir` e `raiz->dir->esq` são ambos pretos.

> As correções que sucedem a propagação são sempre feitas no sentido oposto ao da propagação. Sendo assim, a propagação para a esquerda pode exigir correções à direita e vice-versa.

> **Código**

```C
NO *llrb_propaga_esquerda(NO *raiz) {

    //Inverte cores
    llrb_inverte_cor(raiz);

    //Vê se precisa de correções à direita
    if (vermelho(raiz->dir) && vermelho(raiz->dir->esq)) {

        raiz->dir = llrb_roda_direita(raiz->dir);
        raiz = llrb_roda_esquerda(raiz);

        llrb_inverte_cor(raiz);
    }

    return raiz;
}

NO *llrb_propaga_direita(NO *raiz) {

    //Inverte cores
    llrb_inverte_cor(raiz);

    //Vê se precisa de correções à esquerda
    if (vermelho(raiz->esq) && vermelho(raiz->esq->esq)) {

        raiz = llrb_roda_direita(raiz);
        llrb_inverte_cor(raiz);
    }

    return raiz;
}

NO *llrb_restaura(NO *raiz) {

    //É a mesma ideia da função de inserir
    if (!raiz) return NULL;

    if (!vermelho(raiz->esq) && vermelho(raiz->dir))
        raiz = llrb_roda_esquerda(raiz);

    if (vermelho(raiz->esq) && vermelho(raiz->esq->esq))
        raiz = llrb_roda_direita(raiz);

    if (vermelho(raiz->esq) && vermelho(raiz->dir))
        llrb_inverte_cor(raiz);

    return raiz;
}

NO *llrb_min_dir(NO *raiz) {

    if (raiz->esq) return llrb_min_dir(raiz->esq);

    return raiz;
}

NO *llrb_remove_min_dir(NO *raiz) {

    if (raiz->esq) {

        //Só propaga se for necessário
        if (!vermelho(raiz->esq) && !vermelho(raiz->esq->esq)) {
        
            raiz = llrb_propaga_esquerda(raiz);
        }

        raiz->esq = llrb_remove_min_dir(raiz->esq);
    }
    else {

        NO *aux = raiz->dir;

        free (raiz);
        return aux;
    }
    
    //Necessário consertar a árvore na volta.
    return llrb_restaura(raiz);
}

NO *llrb_remove_no(NO *raiz, int valor) {

    if (valor < raiz->valor) {

        //Propagar (se necessário)
        if (!vermelho(raiz->esq) && !vermelho(raiz->esq->esq))
            raiz = llrb_propaga_esquerda(raiz);
    
        raiz->esq = llrb_remove_no(raiz->esq, valor);
    }

    else {

        //Necessário propagar para a direita (se necessário)
        //Se o nó da esquerda for vermelho, 
        //resolvemos o problema com uma rotação.
        if (vermelho(raiz->esq)) {
            raiz = llrb_roda_direita(raiz);
        }

        //Caso 1: o nó tem 0 ou 1 filho
        if (valor == raiz->valor && raiz->dir == NULL) {

            free(raiz);
            return NULL; //O nó da esquerda também é NULL.
        }

        //Caso 2: o nó tem 2 filhos
        //Então precisamos propagar
        if (!vermelho(raiz->dir) && !vermelho(raiz->dir->esq)) {
            raiz = llrb_propaga_direita(raiz);
        }

        if (valor == raiz->valor) {
            
            NO *x = llrb_min_dir(raiz->dir);
            raiz->valor = x->valor;

            raiz->dir = llrb_remove_min_dir(raiz->dir);

        }
        else raiz->dir = llrb_remove_no(raiz->dir, valor);
    }

    //Volta da recursão: restaura
    return llrb_restaura(raiz);
}
```
    

> **Por que não verificar se o nó da esquerda é nulo na folha?** 
* Se o nó da esquerda não for nulo, quer dizer que ele é preto. Isso acontece porque, se ele for vermelho, ele terá sido rotacionado para a direta na função.
* Se o nó é preto, quer dizer que a distância negra da árvore está violada, logo ele não pode ser preto.

**Conclusão**: nesse exato momento, nossa função, não é possível que haja um nó à esquerda enquanto o da direita for nulo. 