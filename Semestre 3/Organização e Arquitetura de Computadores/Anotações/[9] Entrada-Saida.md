# <span style="color: #2E86C1;">Resumo de Arquitetura - Entrada e Saída (E/S)</span>

## <span style="color: #E67E22;">1. Dispositivos Periféricos e a Necessidade de Módulos</span>
* A CPU não se conecta diretamente aos periféricos devido a diferenças drásticas na taxa de transferência e nos formatos de dados.
* Para resolver isso, utiliza-se um **Módulo (ou Controlador) de E/S**, que faz a interface entre o processador/memória e o dispositivo externo.

### <span style="color: #16A085;">Funções do Módulo de E/S</span>
* **Controle e Temporização:** Gerencia o fluxo de dados entre recursos internos e externos.
* **Comunicação:** Traduz os comandos do processador e as informações de estado do dispositivo (ex: READY/BUSY).
* **Bufferização de Dados (Data Buffering):** Armazena temporariamente os dados para compensar a lentidão dos periféricos em relação à memória principal (ex: CPU envia dados rápido, o buffer segura e passa lentamente para a impressora).
* **Detecção de Erros:** Identifica falhas mecânicas ou alterações nos bits usando códigos de detecção, como o bit de paridade.

## <span style="color: #E67E22;">2. Técnicas de Operação de E/S</span>

### <span style="color: #C0392B;">A) E/S Programada</span>
* A CPU executa um programa que controla diretamente a operação de E/S.
* A CPU fica em um loop constante verificando o estado do dispositivo para saber se ele já terminou.
* **Desvantagem:** É altamente ineficiente, pois a CPU perde muito processamento ociosa esperando o dispositivo lento terminar.
* **Mapeamento:** O endereçamento pode ser **Mapeado na Memória** (registradores de E/S e RAM dividem o mesmo espaço de endereços) ou **Independente/Isolada** (espaço e comandos exclusivos para E/S).

### <span style="color: #C0392B;">B) E/S Dirigida por Interrupção</span>
* Resolve a ociosidade da CPU: a CPU envia o comando de E/S e vai realizar **outras tarefas**.
* Quando o módulo de E/S conclui o trabalho, ele envia um sinal de **interrupção** à CPU.
* A CPU pausa o que está fazendo, salva o estado atual (contexto), atende à requisição através de uma rotina específica (ISR) e depois retorna ao programa original.

### <span style="color: #C0392B;">C) Acesso Direto à Memória (DMA)</span>
* Ideal para grandes blocos de dados (onde as interrupções sobrecarregariam a CPU).
* Requer um módulo especial, o **Controlador de DMA**, que age como um "processador substituto" focado apenas em transferências.
* A CPU envia ao DMA o endereço, a quantidade de palavras e o dispositivo, e vai fazer outra coisa. 
* O DMA faz a ponte direta entre a Memória e o Módulo de E/S, e só gera uma interrupção para a CPU quando **todo o bloco** terminar de ser transferido.
* **Roubo de Ciclo:** Técnica onde o DMA suspende a CPU por uma fração de tempo mínima apenas para usar o barramento, atrasando um pouco a CPU, mas evitando a necessidade de salvar o contexto.

## <span style="color: #E67E22;">3. Evolução do Subsistema de E/S</span>
* A história da E/S é uma jornada para tirar o peso das costas da CPU.
* Etapas: CPU direta $\rightarrow$ E/S Programada $\rightarrow$ E/S por Interrupção $\rightarrow$ DMA $\rightarrow$ **Canais de E/S** (Módulos de E/S que executam suas próprias instruções puxadas da RAM) $\rightarrow$ **Processadores de E/S** (Módulos super complexos que possuem memória local, sendo verdadeiros computadores independentes atuando como controladores).

## <span style="color: #E67E22;">4. Interfaces Externas</span>
A comunicação com o periférico pode ser **Paralela** (vários fios, envio simultâneo de bits, ideal para alta velocidade curta) ou **Serial** (1 bit por vez por um fio). 
A ligação pode ser **Ponto a ponto** (cabo direto módulo-dispositivo) ou **Multiponto** (vários dispositivos compartilhando um barramento externo).

### <span style="color: #16A085;">Exemplos Clássicos e Modernos:</span>
* <span style="color: #2980B9;">**RS-232C (Serial) e LPT (Paralela):**</span> Padrões antigos ponto a ponto. RS-232C era usado em terminais/modens e LPT era famoso para impressoras (conector Centronics).
* <span style="color: #2980B9;">**Teclado/Mouse:**</span> Usavam o padrão serial ponto a ponto Mini-DIN (PS/2).
* <span style="color: #2980B9;">**Armazenamento (IDE/PATA/SATA):**</span> A controladora foi parar na placa do próprio disco. O **SATA** revolucionou ao trocar a interface paralela gorda de 40 fios por cabos seriais muito mais velozes e compactos.
* <span style="color: #2980B9;">**SCSI vs. Firewire:**</span> SCSI é multiponto paralelo, muito rápido mas chato de configurar (exige terminadores na ponta e definir ID manualmente para cada dispositivo). O Firewire (IEEE 1394) é serial, mais barato, sem terminadores e atribui os IDs automaticamente pelo sistema.
* <span style="color: #2980B9;">**USB (Universal Serial Bus):**</span> Arquitetura baseada em um *Host* (o computador) que gerencia até 127 dispositivos encadeados (via hubs). Seu cabo transmite dados e energia simultaneamente.