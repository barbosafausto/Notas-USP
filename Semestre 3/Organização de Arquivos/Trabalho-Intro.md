# Trabalho 1

## Comandos Úteis

```C++

// ------- Básicos
fclose()
fopen("nome_arq", "modo_abertura")
/* Modos
Texto (csv): r, w, a
binário (output): rb+: leitura e escrita sem apagar

*/


// -------- Leitura e escrita
//qtd: número de elementos de tipo <type>
//buffer: não colocar struct (padding
//        colocar campo a campo!
fread(buffer, sizeof(<type>), qtd, FILE*)
fwrite(buffer, sizeof(<type>), qtd, FILE*)


// ------- Navegação (CUSTOSOS)

// Fala o offset da posição atual
ftell(FILE*)                  

/* flags
0, seet_set | seta para o offset para 0
2, seer_cur | anda 2 posições no sentido positivo

*/
fseek(FILE*, qtd, flag)    


//Não usar!
//Usar o fread: se não retornar nada é fim do arq.
feof(FILE*)
```

## GDB Debugger

Pode ser útil para debugar o problema. Vai ter vídeo explicando o debugger?

```bash
gcc -g
gdb programTrab
```

1. Pode colocar breakpoints nas funções.

2. Segfault? Usar o comando "r": run (gdb)

3. Outros comandos
    * p -> print
    * bt -> backtracking
    * n -> next
    * step -> ?


## Valgrind

```bash
valgrind ./programTrab 
```

## Hex Editor & Hex Dump

Permitem ver o conteúdo do arquivo binário como hexadecimal.

> Hex Dump é comando de terminal

## diff

Verificar diferença entre arquivos.


## Modularização

1. Criar funções separadas 
2. Criar arquivos separados
3. Função para escrita e leitura de cabeçalho



## Cabeçalho

1. Status
    * 1: consistente
    * 0: inconsistente

2. Topo
    * Lógica de reutilização dinâmica de espaço
    * Deve ser verificado primeiro antes de adicionar

3. Número de Estações
    * Atualizar pelo nome

4. Número de pares de estações
    * Atualizar pelos IDs das duas estações
    * Grafo ?


## Funcionalidades

### Função 1: Create Table

Fazer loop para separar linhas de entrada em campos

```C++
// Usada para separar linha de entrada em campos
strtok() 
strsep() //do GNU
```

1. É importante fazer o tratamento de campos nulos  
    * Output: "NULO"

2. Inicializar o cabeçalho corretamente
    * Atualizar no final da funcionalidade

3. O número de estações é o número de nomes únicos


### Função 2: SELECT

1. Ao ler um registro removido, pular ele com `fseek()`
    

2. Pesquisas de campos nulos podem acontecer
    * Marcador: NULO


### Função 3: WHERE

1. Mesma coisa do select, porém com condição


### Função 4: DELETE

1. Se a função delete deletar todas as instâncias de uma estação única, é necessário atualizar o número de estações (cabeçalho)
    * Único caso em que deve-se percorrer todo o arquivo para certificar do número de estações atualizado.


### Função 5: INSERT

1. Tratar valor nulo

2. Olhar primeiro o topo da pilha de removidos, depois o próximo RRN

3. O número de estações não irá mudar após inserções


### Função 6: UPDATE

1. Basta atualizar o registro em questão


## Vídeo

> Vídeo de 7 minutos (tempo aumentado).

1. Explicar o trabalho de maneira geral

2. Balancear tempo com a dupla














