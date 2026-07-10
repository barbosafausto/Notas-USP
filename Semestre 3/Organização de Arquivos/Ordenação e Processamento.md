# <span style="color:#2E86C1">Resumo: Ordenação Interna e Externa</span>

## <span style="color:#D35400">1. Ordenação Interna</span>
A ordenação interna é utilizada quando o volume de dados (o arquivo completo) consegue ser carregado inteiramente na <span style="color:#27AE60">**memória principal (RAM)**</span>.

<span style="color:#8E44AD">**Fases Principais:**</span>
1. Leitura e transferência de todos os registros do disco para a memória.
2. Processamento da ordenação dos registros em RAM.
3. Gravação dos dados ordenados de volta no arquivo de disco.

O custo computacional é a soma destas três etapas. Para otimizar o processo e reduzir o tempo de movimentação da cabeça de leitura do disco (<span style="color:#C0392B">***seeks***</span>), privilegia-se a utilização de operações de leitura e escrita sequenciais, aliadas a métodos eficientes de ordenação em memória.

### <span style="color:#16A085">Otimização com Heapsort</span>
O algoritmo <span style="color:#2980B9">**Heapsort**</span> é amplamente utilizado por permitir a paralelização do processamento lógico com as operações de I/O (Entrada/Saída).

* <span style="color:#8E44AD">**A Estrutura Heap:**</span> É uma árvore binária de busca implementada diretamente sobre um vetor. Matematicamente, os filhos de um elemento no índice `i` encontram-se nas posições `2i` e `2i+1`, enquanto o seu nó pai é acedido na posição `⌊i/2⌋`.
* <span style="color:#8E44AD">**Construção:**</span> Um novo elemento é inserido no final do vetor e, sucessivamente, trocado com o seu pai enquanto for menor do que este.
* <span style="color:#8E44AD">**Paralelismo Leitura/Ordenação:**</span> É possível realizar a leitura de um novo bloco de registros para a RAM enquanto se adicionam os registros anteriores, um a um, à estrutura do *heap*.
* <span style="color:#8E44AD">**Paralelismo Ordenação/Escrita:**</span> O registro localizado na raiz do *heap* é recuperado para ser gravado no disco. Enquanto a gravação ocorre, o último elemento do vetor é colocado na raiz e o algoritmo encarrega-se de o empurrar para baixo, trocando-o com o seu menor filho, para reajustar a estrutura.

---

## <span style="color:#D35400">2. Ordenação Externa</span>
É aplicada quando o conjunto de dados é demasiado grande e não cabe na memória RAM, obrigando a um trânsito contínuo de dados entre o disco e a memória.

### <span style="color:#16A085">Algoritmo Sort-Merge Externo</span>
A solução padrão divide-se em duas grandes fases:

<span style="color:#2980B9">**Fase 1: Geração de Subarquivos Ordenados (*Runs*)**</span>
* O arquivo original é particionado. Lê-se o equivalente à capacidade da memória, ordena-se esse bloco internamente e grava-se no disco.
* O resultado é a criação de múltiplos pequenos arquivos ordenados de forma independente, denominados <span style="color:#8E44AD">**runs**</span>.
* <span style="color:#C0392B">**Custo de I/O (Fase 1):**</span> <span style="color:#27AE60">2 * b</span> (sendo `b` o número de blocos). Este valor deve-se ao facto de cada bloco do arquivo ser acedido exatamente duas vezes: uma vez na leitura para a memória e outra na escrita do *run* para o disco.

<span style="color:#2980B9">**Fase 2: Intercalação (*Multiway Merging*)**</span>
* Os *runs* gerados na fase anterior são combinados de forma sistemática.
* Lêem-se blocos de múltiplos *runs* em simultâneo, fundindo as chaves menores num novo subarquivo ordenado ainda maior.
* O processo é repetido em passagens sucessivas até que todos os dados sejam aglomerados num único arquivo final ordenado.
* <span style="color:#C0392B">**Custo de I/O (Fase 2):**</span> <span style="color:#27AE60">2 * b * log_m(b)</span>. Cada bloco é acedido diversas vezes consoante o número de intercalações necessárias. O `m` representa o grau de combinação (quantos *runs* são intercalados por vez).

<span style="color:#2980B9">**Custo Total do Algoritmo**</span>
A complexidade total de acessos a disco é dada pela soma dos custos das duas fases:
<span style="color:#27AE60">Custo = (2 * b) + (2 * b * log_m(b))</span>

# <span style="color:#2E86C1">Processamento Cosequencial</span>

## <span style="color:#D35400">1. Operações Cosequenciais</span>
* Processam **simultaneamente** registros ordenados de dois ou mais arquivos.
* Produzem um arquivo de saída, contendo registros ordenados.
* **Operações principais:**
  * <span style="color:#27AE60">**Merging**</span>: União / Intercalação.
  * <span style="color:#8E44AD">**Matching**</span>: Intersecção.

## <span style="color:#D35400">2. Algoritmos: Pontos Importantes</span>
Ao desenvolver o algoritmo, deve-se considerar os seguintes pilares:
* <span style="color:#C0392B">**Inicialização**</span>: Como abrir os arquivos e inicializar as informações corretamente para o processo funcionar.
* <span style="color:#C0392B">**Sincronização**</span>: Como avançar adequadamente em cada arquivo. Inclui o gerenciamento vital da condição de **fim-de-arquivo** (ex: no *merging*, quando uma lista acaba, a outra continua sendo copiada para a saída; no *matching*, o processo se encerra).
* <span style="color:#C0392B">**Reconhecimento de Erros**</span>: Lidar com nomes duplicados ou registros fora de ordem.

## <span style="color:#D35400">3. Multiway Merging</span>
* Utilizado para mesclar múltiplos subarquivos ordenados simultaneamente (ex: K=8 arquivos vindos do disco).
* O número de níveis da árvore na memória é de aproximadamente <span style="color:#2980B9">log₂ K</span>, onde **K** é o número de arquivos de dados.

### <span style="color:#2E86C1">Árvore de Seleção (Torneio)</span>
* Estrutura que atua como uma árvore de torneio.
* Guarda sempre a **menor chave na raiz** da árvore. Isso garante uma recuperação extremamente rápida do próximo menor elemento.

### <span style="color:#2E86C1">Passo a Passo do Algoritmo na RAM/Disco</span>
1. A árvore indica de qual arquivo (disco) foi obtida a menor chave atual.
2. Essa menor chave é retirada da memória RAM e gravada no arquivo de saída ordenado usando <span style="color:#16A085">fwrite()</span>.
3. O algoritmo lê a próxima chave **especificamente daquele mesmo arquivo** onde houve a baixa, usando <span style="color:#16A085">fread()</span>.
4. Reestrutura-se a árvore de seleção na RAM para que o novo menor valor global suba para a raiz.