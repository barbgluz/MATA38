# Descrição geral
O computador pode ser visto como sendo um grande conjunto de componentes interligados, cada um com funções especializadas e trabalhando de forma coordenada e sincronizada. Pode-se dizer que os principais componentes do computador são a unidade central de processamento (CPU), a memória e os periféricos. 

A CPU é a responsável por toda a coordenação operações executadas, a memória é onde residem o conjunto de instruções a serem executadas e os dados usados por tais instruções. Os periféricos são responsáveis por interligar o mundo externo ao interior da máquina. Cada um destes componentes são formados por diversas unidades, cada uma das quais construı́das por circuitos lógicos, combinacionais e sequenciais. 

Este trabalho tem o intuito de (a) desmistificar a complexidade interna da arquitetura de computadores, (b) consolidar conceitos vistos durante o curso, e (c) aumentar o interesse da turma por tópicos relacionados à organização interna de computadores, o que será tratado em detalhes em outras disciplinas do curso.

Para tanto, solicita-se a implementação de dois dos componentes do computador para a arquitetura Mata3820171. Esta arquitetura foi especialmente especificada para este trabalho. Ela contém os componentes necessários para colocá-la em funcionamento. Para este projeto, contudo, apenas a CPU e a memória principal serão tratados. Da CPU, apenas a ALU será objeto deste trabalho. Não estásendo solicitado ainda o controle entre a comunicação da CPU e a memória. Ou seja, tais componentes estão aqui sendo tratados de forma isolada.

A implementação solicitada neste trabalho deverá ser realizada no Logisim (http://www.cburch. com/logisim/). Esta ferramenta oferece diversas funcionalidades e circuitos integrados já prontos, o que facilita o projeto e a depuração aqui descritos.

## Parte 1: Unidade Lógica Aritmética
Como o nome indica, a ALU é a unidade responsável pela execução das operações lógicas e aritméticas. Tal componente pode ser visto como vários circuitos combinacionais operando em paralelo, cada um responsável por uma determinada operação. Na arquitetura Mata3820171, as entradas de tais circuitos, isto é, seus operandos, são armazenadas em registradores. Geralmente, o valor de saı́da da operação realizada pela ALU é armazenada num registrador, comumente chamado de acumulador. Para a arquitetura Mata3820171, o acumulador é identificado R 0 .

As operações realizadas pela ALU fazem parte do conjunto de instruções especificadas na arquitetura Mata3820171. O identificador da instrução é um código de 4 bits após os quais seguem mais quatro bits para identificação dos registradors que contém os operandos. Desta forma, esta máquina contém apenas 16 instruções, listadas na Tabela.

As instruções relacionadas à ALU, objeto dotrabalho, têm código de 0 a 10 (0x0 a 0xA em hexadecimal). São apenas quatro registradores endereçáveis, R 0 , R 1 , R 2 e R 3 . Todos os resultados das operações são colocados no acumulador R 0 , como pode ser observado na tabela. Note que a arquitetura Mata3820171 possui palavra de 8 bits. As instruções da arquitetura Mata3820171 podem ser de três tipos, com os seguintes formatos:

• Tipo I. Estas são instruções que possuem dois operandos de dois bits, cada um dos quais endereçaum registrador e tem formato INST Rx, Ry.

• Tipo II. Este tipo opera sobre apenas um registrador. Os últimos dois bits (menos significativos) são ignorados. A única instrução deste tipo na arquitetura Mata3820171 é a NOT, responsável por inverter os bits contidos no registrador cujo endereço é o seu parâmetro. Seu formato é NOT Rx.

• Tipo III. A única instrução do tipo três é a HLT, que não possui parâmetros e, portanto, tem seus quatro bits menos significativos ignorados pelo processador.

No trabalho, apenas as instruções relacionadas a ALU serão objeto de implementação. A funcionalidades, código e formato são detalhados na Tabela, que traz também as demais instruções do processador Mata3820171.

## Parte 2: Memória RAM 
A memória RAM da arquitetura Mata3820171 possui 16 bits de endereçamento e, portanto, 65536 localidades de endereços, cada um armazenando um Byte de informação. Notem que a palavrade dados da arquitetura contém apenas um Byte, insuficiente para endereçar toda a memória. 

A forma com que o endereçamento é feito, contudo, é por segmentação. A memória é dividida em 256 segmentos. Um programa é carregado em um dos segmentos, cujo endereço base (inı́cio do segmento) é colocado no registrador RS. Este contém os primeiros 8 bits do endereço de memória ser referenciado.Os 8 bits menos significativos referem-se ao conteúdo do registrador RM, responsável pelo endereço dentro do seguimento indicado por RS.

Neste trabalho, deve-se projetar um circuito que escreve números sequenciais de 0x00 a 0xFF em todos os seguimentos de memória. Em seguida este mesmo circuito lê tais valores escritos. Tal tipo de circuito é usado em testes iniciais de memória quando a máquina é ligada.
