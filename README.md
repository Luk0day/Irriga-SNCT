# 🌱 Sistema de Irrigação Automática com Arduino Uno

**Projeto para a Feira de Ciências**

## 1. Sobre o projeto

Este projeto apresenta um sistema de irrigação automática desenvolvido com Arduino Uno. Sua função é monitorar a umidade do solo e acionar uma pequena bomba de água quando a terra estiver seca. Quando o solo atingir o nível de umidade definido no programa, a bomba será desligada.

Para facilitar a identificação do funcionamento do sistema, utilizamos também um LED que acende enquanto a irrigação estiver acionada.

A ideia é mostrar como a programação e a eletrônica podem ajudar a resolver situações do dia a dia. Em vez de depender apenas de uma pessoa para verificar a terra e regar a planta, podemos criar um sistema que faça essa tarefa de forma automática.

Este é um projeto introdutório, ideal para quem está começando a aprender programação, eletrônica e robótica.

## 2. Objetivo do projeto

Desenvolver um sistema capaz de identificar quando o solo precisa de água e realizar a irrigação automaticamente, utilizando um sensor capacitivo de umidade do solo, uma placa Arduino Uno, uma bomba de água e um LED indicador.

### O que queremos aprender?

Durante o desenvolvimento, vamos aprender a:

- Entender como funciona um sensor de umidade do solo.
- Ler informações do ambiente usando o Arduino.
- Utilizar condições na programação para tomar decisões.
- Controlar uma bomba de água por meio de um módulo relé.
- Utilizar um LED para indicar o estado de funcionamento do sistema.
- Integrar componentes eletrônicos para criar uma solução prática.

## 3. Como o sistema funciona?

O funcionamento do projeto pode ser dividido em quatro etapas.

**1. Leitura da umidade:** o sensor capacitivo fica inserido no solo e envia uma informação elétrica ao Arduino. Essa informação varia conforme a umidade do solo e as características do sensor.

**2. Análise dos dados:** o Arduino lê o valor enviado pelo sensor e compara esse valor com os limites de umidade definidos no código.

**3. Irrigação automática:** quando o programa identifica que o solo está seco, o Arduino aciona um módulo relé, que controla a alimentação elétrica da bomba. A bomba começa a enviar água para a planta.

**4. Encerramento da irrigação:** quando o sensor indica que o solo atingiu o nível de umidade desejado, o Arduino desliga a bomba e apaga o LED.

Dessa forma, o sistema fica verificando continuamente a condição do solo e decide quando é necessário irrigar.

### Representação do funcionamento

```text
        SENSOR DE UMIDADE
                |
                v
          ARDUINO UNO
                |
          Solo está seco?
           /          \
         SIM           NÃO
          |              |
          v              |
    Ativa o relé         |
          |              |
          v              |
        BOMBA             |
          |              |
          v              |
       LED ACESO          |
          |              |
          +--------------+
             Nova leitura
```

O LED representa o comando de irrigação. Ele acende quando o sistema manda ligar a bomba e apaga quando manda desligá-la.

## 4. Materiais necessários

Para construir o protótipo, serão necessários os seguintes materiais:

| Quantidade | Componente | Função no projeto |
|---|---|---|
| 1 | Arduino Uno | Processa as informações e controla o sistema. |
| 1 | Sensor capacitivo de umidade do solo | Mede uma grandeza relacionada à umidade da terra. |
| 1 | Mini bomba de água de corrente contínua (CC) | Transporta a água até a planta. |
| 1 | Módulo relé compatível com a bomba | Liga e desliga a alimentação elétrica da bomba. |
| 1 | LED | Indica quando a irrigação está acionada. |
| 1 | Resistor de 220 Ω a 330 Ω | Limita a corrente que passa pelo LED. |
| 1 | Fonte de alimentação para a bomba | Fornece a energia necessária ao motor da bomba. |
| Alguns | Jumpers e protoboard | Facilitam as conexões eletrônicas. |
| 1 | Mangueira fina | Conduz a água até o vaso. |
| 1 | Recipiente com água | Serve como reservatório. |
| 1 | Vaso com terra e uma planta | Representa o ambiente que será irrigado. |
| 1 | Cabo USB | Permite programar e alimentar o Arduino durante o desenvolvimento. |

**Importante:** a fonte deve ser compatível com a tensão e a corrente exigidas pela bomba. O módulo relé também precisa suportar a carga elétrica utilizada. A bomba não deve ser alimentada diretamente por um pino do Arduino.

## 5. Entendendo os principais componentes

### Arduino Uno

O Arduino Uno é uma placa eletrônica programável. Podemos pensar nele como o cérebro do projeto: ele recebe informações, executa instruções e controla os componentes conectados a ele.

Neste projeto, o Arduino recebe os dados do sensor, verifica se o solo precisa de água e envia o comando para ligar ou desligar a bomba.

### Sensor capacitivo de umidade do solo

O sensor capacitivo identifica mudanças nas propriedades elétricas do solo relacionadas à sua umidade. Em um módulo com saída analógica, essa informação é enviada ao Arduino como um valor numérico.

No Arduino Uno, a função `analogRead()` normalmente retorna valores entre 0 e 1023.

Esses números não representam diretamente uma porcentagem de umidade. Eles são leituras que precisamos interpretar e calibrar para o sensor e o solo utilizados.

Uma vantagem dos sensores capacitivos é que eles não precisam utilizar os mesmos eletrodos metálicos expostos encontrados em muitos sensores resistivos. Ainda assim, é importante proteger a parte eletrônica do módulo contra água.

### Bomba de água

A bomba transporta a água do reservatório até a planta. Ela é o componente responsável por realizar a irrigação.

Como a bomba utiliza um motor elétrico e pode exigir mais corrente do que o Arduino consegue fornecer por suas saídas, precisamos de um circuito de acionamento apropriado, como um módulo relé compatível.

A bomba também deve ter sua própria alimentação elétrica, dimensionada conforme as especificações do fabricante.

### Módulo relé

O relé funciona como um interruptor controlado eletricamente. O Arduino envia um pequeno sinal para o módulo relé, e o relé comuta os contatos que controlam a alimentação da bomba.

Dessa maneira, o Arduino controla a bomba sem precisar fornecer diretamente a corrente do motor.

### LED indicador

O LED mostra visualmente quando o programa está comandando a irrigação. Isso ajuda a compreender o funcionamento do projeto durante a apresentação na feira de ciências.

Se o LED estiver aceso, significa que o Arduino ordenou que a irrigação fosse ligada. Isso não garante, por si só, que a bomba esteja realmente transportando água.

## 6. Como fazer as conexões

Antes de conectar os componentes, desligue a alimentação e confira as identificações dos pinos e as especificações de cada módulo.

### 6.1. Sensor de umidade

Considerando um sensor com os pinos `VCC`, `GND` e `AOUT`:

| Pino do sensor | Conexão |
|---|---|
| VCC | 5V do Arduino, se compatível com o sensor |
| GND | GND do Arduino |
| AOUT | Pino analógico A0 do Arduino |

O pino `AOUT` envia a leitura analógica utilizada pelo programa.

Alguns módulos apresentam pinos ou tensões diferentes. Confira a identificação do seu modelo antes de ligar a alimentação.

### 6.2. LED indicador

| Parte do LED | Conexão |
|---|---|
| Perna positiva, geralmente a mais longa | Pino digital D6 por meio de um resistor de 220 Ω a 330 Ω |
| Perna negativa | GND do Arduino |

O resistor limita a corrente que atravessa o LED e ajuda a evitar danos ao componente.

### 6.3. Módulo relé

Considerando um módulo relé de entrada lógica compatível com o Arduino:

| Pino do módulo | Conexão |
|---|---|
| IN | Pino digital D7 |
| VCC | Alimentação especificada pelo fabricante do módulo |
| GND | GND do Arduino |

Se o módulo possuir bornes identificados como `COM`, `NO` e `NC`, utilizaremos normalmente `COM` e `NO`.

- **COM:** contato comum do relé.
- **NO:** contato normalmente aberto, que se conecta a COM quando o relé é acionado.
- **NC:** contato normalmente fechado, que se conecta a COM enquanto o relé está em repouso.

Para manter a bomba desligada quando o relé não estiver acionado, utilizaremos normalmente o contato NO.

### 6.4. Alimentação da bomba

Para uma bomba de corrente contínua, com alimentação externa de baixa tensão, a ligação pode ser feita assim:

```text
Fonte externa (+)
       |
       v
      COM
   [  RELÉ  ]
      NO
       |
       v
Bomba (+)

Bomba (-)
       |
       v
Fonte externa (-)
```

Esse desenho representa o circuito de alimentação da bomba. O módulo relé recebe o sinal de controle do Arduino por meio dos seus pinos de entrada.

**Atenção:** não conecte a alimentação da bomba ao pino de 5V do Arduino. Use uma fonte adequada à bomba e confirme que os contatos do relé suportam a tensão e a corrente exigidas pelo motor. Para este projeto escolar, prefira uma bomba de baixa tensão. Não utilize tensão da rede elétrica doméstica neste protótipo.

## 7. Código completo do projeto

O código abaixo foi organizado para facilitar a leitura e permitir que as alunas compreendam cada parte da programação.

O programa utiliza dois limites de leitura: um para identificar quando o solo está seco e outro para identificar quando ele já está suficientemente úmido. Essa diferença ajuda a evitar que a bomba fique ligando e desligando rapidamente quando a leitura estiver próxima de um único limite.

**Antes de executar o código, é necessário calibrar os limites do sensor.** Os valores apresentados são apenas exemplos e podem não funcionar diretamente no sensor de vocês.

```cpp
// ===============================================
// PROJETO: IRRIGACAO AUTOMATICA COM ARDUINO UNO
// ===============================================

// Pinos utilizados no projeto
const byte PIN_SENSOR = A0;
const byte PIN_RELE = 7;
const byte PIN_LED = 6;

// Limites iniciais de exemplo.
// Ajuste estes valores usando as leituras reais.
const int LIMITE_SECO = 600;
const int LIMITE_UMIDO = 450;

// Em muitos sensores, o valor diminui quando
// o solo fica mais umido. Confirme no teste.
const bool VALOR_ALTO_SIGNIFICA_SECO = true;

// Muitos modulos rele sao acionados com LOW.
// Se o seu funcionar de outra forma, ajuste.
const bool RELE_ATIVO_EM_LOW = true;

// Guarda o estado atual da irrigacao.
bool irrigando = false;


// Liga ou desliga a bomba e o LED.
void controlarIrrigacao(bool ligar) {

  if (RELE_ATIVO_EM_LOW) {
    digitalWrite(PIN_RELE, ligar ? LOW : HIGH);
  } else {
    digitalWrite(PIN_RELE, ligar ? HIGH : LOW);
  }

  // O LED acompanha o comando da bomba.
  digitalWrite(PIN_LED, ligar ? HIGH : LOW);

  // Atualiza o estado armazenado.
  irrigando = ligar;

  if (ligar) {
    Serial.println("Irrigacao iniciada.");
  } else {
    Serial.println("Irrigacao finalizada.");
  }
}


void setup() {

  // Inicia a comunicacao com o computador.
  Serial.begin(9600);

  // Define os pinos que controlam as saidas.
  pinMode(PIN_RELE, OUTPUT);
  pinMode(PIN_LED, OUTPUT);

  // Mantem a bomba desligada no inicio.
  digitalWrite(PIN_RELE,
               RELE_ATIVO_EM_LOW ? HIGH : LOW);

  digitalWrite(PIN_LED, LOW);

  Serial.println("Sistema de irrigacao iniciado.");
}


void loop() {

  // Faz a leitura do sensor.
  int leitura = analogRead(PIN_SENSOR);

  // Mostra a leitura para auxiliar na calibracao.
  Serial.print("Leitura do solo: ");
  Serial.println(leitura);

  // Interpreta a leitura conforme o sensor utilizado.
  bool soloSeco;
  bool soloUmido;

  if (VALOR_ALTO_SIGNIFICA_SECO) {

    soloSeco = leitura >= LIMITE_SECO;
    soloUmido = leitura <= LIMITE_UMIDO;

  } else {

    soloSeco = leitura <= LIMITE_SECO;
    soloUmido = leitura >= LIMITE_UMIDO;

  }

  // Se o solo estiver seco, liga a irrigacao.
  if (!irrigando && soloSeco) {
    controlarIrrigacao(true);
  }

  // Se o solo estiver umido o suficiente,
  // desliga a irrigacao.
  else if (irrigando && soloUmido) {
    controlarIrrigacao(false);
  }

  // Aguarda meio segundo antes da proxima leitura.
  delay(500);
}
```

## 8. Entendendo o código passo a passo

Não é necessário memorizar todo o código de uma vez. O ideal é entender o papel de cada parte e depois experimentar pequenas mudanças.

### 8.1. Definindo os pinos

```cpp
const byte PIN_SENSOR = A0;
const byte PIN_RELE = 7;
const byte PIN_LED = 6;
```

Essas linhas dão nomes aos pinos utilizados no projeto.

O sensor está conectado ao A0, enquanto o relé utiliza o pino digital 7 e o LED utiliza o pino digital 6.

Assim, se precisarmos trocar uma conexão, podemos alterar o número no início do código, sem precisar procurar todas as ocorrências daquele pino.

### 8.2. Criando os limites de umidade

```cpp
const int LIMITE_SECO = 600;
const int LIMITE_UMIDO = 450;
```

Esses números são referências utilizadas pelo programa para decidir quando ligar e desligar a irrigação.

No exemplo, estamos considerando que uma leitura mais alta indica um solo mais seco e que uma leitura mais baixa indica um solo mais úmido.

Essa relação precisa ser confirmada no sensor real. Não devemos assumir que todos os sensores possuem o mesmo comportamento.

### 8.3. Lendo o sensor

```cpp
int leitura = analogRead(PIN_SENSOR);
```

A função `analogRead()` lê a entrada analógica A0 e retorna um número. Essa leitura será analisada pelas condições do programa.

É importante lembrar que o número não é, por si só, uma porcentagem de umidade. Ele é a leitura elétrica que utilizaremos como referência para tomar decisões.

### 8.4. Utilizando condições

```cpp
if (!irrigando && soloSeco) {
  controlarIrrigacao(true);
}
```

O comando `if` permite executar uma ação somente quando determinada condição é verdadeira.

Nesse caso, o Arduino verifica duas coisas: a irrigação ainda está desligada e o solo foi identificado como seco. Se ambas forem verdadeiras, o programa liga a bomba e o LED.

Já o trecho abaixo verifica se chegou o momento de interromper a irrigação:

```cpp
else if (irrigando && soloUmido) {
  controlarIrrigacao(false);
}
```

Se a irrigação estiver ligada e o solo atingir o limite de umidade definido, a bomba será desligada.

### 8.5. Mantendo o estado da irrigação

A variável `irrigando` informa se o sistema está irrigando naquele momento.

Isso é importante porque queremos que a bomba continue ligada enquanto o solo ainda não atingiu o nível de umidade esperado.

Se utilizássemos apenas um único limite, a bomba poderia ligar e desligar várias vezes devido a pequenas variações da leitura. Por isso, separamos os limites de início e de encerramento da irrigação.

Esse comportamento é conhecido como histerese.

### 8.6. Controlando o LED

```cpp
digitalWrite(PIN_LED, ligar ? HIGH : LOW);
```

Quando o programa manda ligar a irrigação, o LED recebe o estado `HIGH`. Quando manda desligar, o LED recebe `LOW`.

De forma simplificada, `HIGH` representa uma saída em nível alto e `LOW` representa uma saída em nível baixo. A função `digitalWrite()` é utilizada para definir esse estado em um pino configurado como saída.

### 8.7. Mostrando informações no computador

```cpp
Serial.begin(9600);
```

Essa instrução inicia a comunicação serial com o computador.

O comando `Serial.println()` permite mostrar os valores recebidos do sensor no Monitor Serial da Arduino IDE. Isso ajuda a observar o que acontece quando o sensor é colocado em uma terra mais seca ou mais úmida.

## 9. Como calibrar o sensor

Esta é uma das etapas mais importantes para fazer o sistema funcionar corretamente.

Os valores `600` e `450` são apenas pontos de partida. O resultado real depende do modelo do sensor, da alimentação, do tipo de solo e das condições do teste.

### Passo 1 — Envie o código ao Arduino

Conecte a placa ao computador usando o cabo USB.

Na Arduino IDE, selecione a placa Arduino Uno e a porta correta. Em seguida, compile e envie o programa.

### Passo 2 — Abra o Monitor Serial

Na Arduino IDE, abra o Monitor Serial e configure a velocidade para `9600 baud`.

Você deverá observar mensagens semelhantes a estas:

```text
Sistema de irrigacao iniciado.
Leitura do solo: 720
Leitura do solo: 715
Leitura do solo: 430
```

Os valores são ilustrativos. O sensor de vocês poderá apresentar números bem diferentes.

### Passo 3 — Observe a leitura em solo seco

Coloque a parte de medição do sensor na terra mais seca que será utilizada no projeto. Registre os valores mostrados no Monitor Serial.

### Passo 4 — Observe a leitura em solo úmido

Coloque o sensor em uma região de solo úmido, sem submergir a placa eletrônica em água. Registre novamente os valores.

Agora vocês terão uma ideia de como o sensor responde às mudanças de umidade.

### Passo 5 — Ajuste os limites

Suponha que o sensor apresente uma leitura próxima de `700` no solo seco e de `400` no solo úmido.

Nesse exemplo, podemos experimentar:

```cpp
const int LIMITE_SECO = 600;
const int LIMITE_UMIDO = 450;
```

O sistema começará a irrigar quando o valor alcançar ou ultrapassar 600 e deixará de irrigar quando o valor chegar a 450 ou menos.

Os valores escolhidos precisam estar de acordo com as leituras reais e com a quantidade de água que a planta necessita.

**E se acontecer o contrário?**

Se o sensor apresentar valores mais baixos no solo seco e mais altos no solo úmido, altere esta configuração:

```cpp
const bool VALOR_ALTO_SIGNIFICA_SECO = false;
```

Nesse caso, ajuste também os limites conforme as leituras observadas. Por exemplo, se o solo seco marcar aproximadamente 350 e o solo úmido marcar 700, um ponto de partida seria `LIMITE_SECO = 450` e `LIMITE_UMIDO = 600`.

Faça os testes inicialmente com a bomba desconectada do circuito de alimentação. Depois de confirmar a leitura e a lógica do programa, teste o acionamento do relé e, por último, a irrigação completa.

## 10. Montagem e testes finais

Depois de calibrar o sensor, siga esta sequência para montar o protótipo.

1. Confira se todas as conexões estão corretas e se os componentes são compatíveis.
2. Coloque a planta em um vaso com o substrato utilizado nos testes.
3. Insira a parte de medição do sensor no solo, mantendo a eletrônica fora da água.
4. Posicione a bomba no reservatório e conecte a mangueira até o vaso.
5. Ligue o sistema e observe as leituras do sensor.
6. Simule uma condição de solo seco e verifique se o sistema aciona o relé e acende o LED.
7. Observe se a bomba transporta água corretamente.
8. Quando o solo atingir o limite programado, confirme se a bomba e o LED desligam.

A simulação deve ser feita com cuidado para não encharcar a planta. Não deixe a bomba funcionar sem água e não deixe que respingos atinjam o Arduino ou as conexões elétricas.

Para um primeiro teste, é possível verificar a lógica do programa sem água e sem a bomba conectada. Isso facilita identificar erros antes de colocar todo o sistema em funcionamento.

## 11. Problemas comuns e como resolver

| Problema | O que verificar |
|---|---|
| O sensor apresenta sempre o mesmo valor | Confira VCC, GND, AOUT e a conexão com A0. Verifique também se o sensor está inserido corretamente no solo. |
| A bomba não liga | Confira a alimentação externa, a ligação COM/NO, a compatibilidade do relé e a configuração de acionamento. |
| A bomba fica ligada o tempo todo | Verifique os limites do sensor, o sentido das leituras e a configuração do relé. |
| A bomba liga e desliga repetidamente | Faça uma nova calibração e confira se os limites de início e de parada estão suficientemente separados. |
| O LED não acende | Confira a polaridade do LED, o resistor e a conexão ao pino D6. |
| O LED acende, mas a bomba não funciona | O Arduino pode estar enviando o comando corretamente, mas ainda pode haver um problema na alimentação, no relé ou na própria bomba. |
| A irrigação começa tarde demais ou deixa a terra muito molhada | Reavalie os limites e a posição do sensor no vaso. |

## 12. Cuidados importantes

- Utilize uma fonte de baixa tensão adequada à bomba e compatível com a corrente exigida por ela.
- Não ligue a bomba diretamente a um pino digital do Arduino.
- Mantenha a placa Arduino, o relé e as conexões protegidos contra respingos.
- Não mergulhe a placa eletrônica do sensor na água. Apenas a parte indicada pelo fabricante deve entrar em contato com a terra.
- Desligue a alimentação antes de modificar as conexões.
- Não deixe a bomba trabalhar sem água, pois isso pode danificar o motor.
- Durante a feira de ciências, mantenha o reservatório estável e os fios organizados para evitar acidentes.
- Supervisione a operação: este protótipo não possui, na versão atual, um limite de tempo para irrigação nem um sensor de nível do reservatório.

## 13. Aplicações e possibilidades de melhoria

Depois de concluir a versão inicial, podemos pensar em melhorias para tornar o sistema mais completo.

**Proteção contra funcionamento prolongado:** acrescentar um limite de tempo para a bomba, evitando que ela permaneça ligada por muito tempo caso ocorra alguma falha.

**Sensor de nível do reservatório:** impedir que a bomba funcione quando não houver água suficiente.

**Exibição dos dados:** acrescentar um display para mostrar a leitura do sensor e o estado da irrigação.

**Ajuste dos limites:** permitir que os valores utilizados para identificar solo seco ou úmido sejam alterados mais facilmente.

**Registro de dados:** armazenar as leituras para comparar a variação da umidade ao longo do tempo.

**Alimentação por energia solar:** estudar a possibilidade de utilizar um painel solar e um sistema de alimentação adequado.

Essas melhorias podem ser desenvolvidas em etapas, à medida que as alunas ganharem experiência com programação e eletrônica.

## 14. Conclusão

O sistema de irrigação automática demonstra como conhecimentos básicos de programação e eletrônica podem ser aplicados para resolver um problema real.

Com a utilização do Arduino Uno, do sensor capacitivo de umidade, do módulo relé, da bomba e do LED indicador, foi possível construir um protótipo que identifica uma condição do solo e toma uma decisão a partir dessa informação.

Mais do que montar um circuito, este projeto é uma oportunidade para aprender a observar, testar hipóteses, analisar dados e corrigir erros. Essas etapas fazem parte do desenvolvimento de qualquer solução tecnológica.

A proposta também mostra que projetos de robótica e automação podem começar de maneira simples. Com curiosidade, trabalho em equipe e experimentação, é possível transformar uma ideia em algo que funciona de verdade.

## 15. Referências para continuar aprendendo

- [Documentação oficial do Arduino — Referência da linguagem em português](https://docs.arduino.cc/language-reference/pt/)
- [Exemplo oficial — Leitura analógica no Arduino](https://docs.arduino.cc/built-in-examples/analog/AnalogInput/)
- [Documentação oficial — Função digitalWrite()](https://docs.arduino.cc/language-reference/en/functions/digital-io/digitalwrite/)
- [Guia de estilo do Arduino — Como escrever tutoriais e exemplos](https://docs.arduino.cc/learn/contributions/arduino-writing-style-guide)

---

**Projeto desenvolvido para fins educativos, com o objetivo de introduzir conceitos de programação, eletrônica, automação e uso consciente da água.**
