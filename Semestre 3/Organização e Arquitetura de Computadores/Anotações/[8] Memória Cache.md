# Memória Cache

CPU <=> L1 (32kB) <=> L2 (256kB) <=> L3 (10-20 MB) <=> RAM

==> O L3 fica fora do processador.

## Princípios de Localidade

### Espacial

Se um dado é acessado existe a probabilidade de acessar um dado que está perto.

#### => Tamanho do Bloco (RAM => Cache)

Grande o suficiente para satisfazer a localidade espacial, mas não muito grande.
### Temporal


Se um dado é acessado, existe a probabilidade de acessá-lo novamente.

## Conceitos

=> Acerto (HIT): o dado foi achado na cache;
* Hit rate: n° de acertos na cache / n° total de acessos

=> Falha (MISS): o dado não foi achado na cache
* Miss rate: n° de falhas na cache / n° total de acessos

=> Penalidade por falha: tempo para buscar um dado no cache, falhar e buscar no nível inferior

## Estrutura da Cache

Linha: [tag | V | M | ... | Bloco de Dados]

=> Tag
* Identifica unicamente uma <u>linha</u> da cache

=> V
* Bit de validade indica se a linha é válida ou não.

=> M
* Bit de modificação indica se o bloco foi modificado ou não.

## Funções de Mapeamento

Onde os blocos da memória primária são alocados nas caches.

64 bytes => 6 bits ($b_5b_4b_3b_2b_1b_0$)

### Mapeamento Direto

=> Mapeia diretamente um bloco da MP em uma linha da cache
* Problema: disputa de dados. A própria função de mapeamento é o algoritmo de substituição.

$$
i = j \mod m
$$

* $i$: linha de alocação na cache;
* $j$: n° do bloco da MP;
* $m$: n° de linhas da cache.

#### => Blocos de 4 palavras 

$b_1b_0$: endereçam o byte offset do byte na palavra

$b_3b_2$: endereçam o offset da palavra dentro do bloco

$b_5b_4$: endereçam o "offset" do próprio bloco na cache
* $b_4$: $index$ (indica a linha do bloco na cache)
* $b_5$: **tag**;

#### => Blocos de 2 palavras

$b_1b_0$: igual

$b_2$: para endereçar o offset da palavra no bloco

$b_4b_3$: index (linha)

$b_6$: **tag**


### Mapeamento Associativo (Total)

=> Mapeamento de blocos da MP em quaisquer linhas da cache.

=> Mantém byte e word offset.

A tag possui 3 bits. Não há index.
* Problema: comparar a tag (comparador) da busca com todos armazenados na cache

=> MUX seleciona a linha; seletor é o index.


### Mapeamento Associativo (por Conjunto) - $k-way$

=> As tags são feitas por conjunto
* Não precisa comparar a tag como todos da cache

=> $v$ conjuntos de $k$ linhas.
* $v\cdot k$ linhas na cache

=> Mapeia diretamente para o conjunto, e associativamente dentro do conjunto

=> Agora tem bit(s) de $set$ (conjunto).

#### Endereçamento (bloco c/ 2 palavras)

=> Byte e Word offset não mudam.

=> $b_3$: bit do $set$

=> $b_5b_4$: tag

MUX seleciona o conjunto ($b_3$). Comparador vê as tags ($b_5b_4$) do conjunto.


### Algoritmos de Substituição

=> Implementado em um miss. Usa bit para usar o algoritmo.

* Totalmente Associativo: substitui uma linha
* Associativo por Conjunto: substitui uma linha do conjunto

* FIFO (não é política para cache)
    
    => Contador global para cada inserção

* LRU: Least Recently Used

    => Contador global para cada acesso

* LFU: Least Frequently Used

    => Contador local para cada acesso

* Aleatório (não é política para cache)

    => escolhe linha aleatoriamente

### Política de Escrita

#### Write Hit

=> Write Back

Atualiza o nível onde o dado foi encontrado e indica que a linha está "suja" (dirty) - modificada.
* bit "M" => indica que o valor da linha não é condizente com os níveis inferiores.
                            

=> Write Through
* Atualiza também o nível inferior.

#### Write Miss

=> Write Allocate

Read Miss (traz dado para a cache) e Write-Hit (escreve já tendo o dado na cache)
* Com Write Through não faz sentido (<=>).

=> Write No-Allocate

Escreve no nível que achar o dado (não traz para níveis superiores)
