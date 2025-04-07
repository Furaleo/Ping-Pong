===========================
JOGO DE PING PONG EM C
===========================

Este é um jogo de Ping Pong feito em linguagem C (padrão "envelhecido"),
executado inteiramente no terminal utilizando sequências ANSI.

---------------------------
FUNCIONAMENTO DO JOGO
---------------------------

No início, o jogador define os seguintes parâmetros:
- VELOCIDADE BASE: define o atraso entre os frames (em milissegundos). Ex: 200 ms.
- DIFICULDADE DO ADVERSÁRIO: de 1 (fácil) a 10 (quase impossível).
- NÚMERO DE SETS para vencer a partida.
- PONTOS POR SET: quantos pontos são necessários para vencer um set.
- FREQUÊNCIA DE HABILIDADES: tempo (em segundos) para as habilidades surgirem.

A partida inicia com um sorteio para decidir quem começa sacando.

---------------------------
CONTROLES
---------------------------
- **W** = move a raquete para cima  
- **S** = move a raquete para baixo  
- **Q** = sai do jogo  

O jogador controla a raquete do lado esquerdo da tela. O computador controla a raquete da direita.

---------------------------
MECÂNICA DAS RAQUETES
---------------------------

Cada raquete possui 4 segmentos verticais. Quando a bola colide com a raquete:

- **Segmentos 1 e 2 (meio):**
  * Bola segue em linha reta (dy = 0)
  * A velocidade do jogo AUMENTA (currentDelay reduz 50 ms, mínimo de 50 ms)

- **Segmentos 0 e 3 (pontas):**
  * Bola sobe ou desce
  * A velocidade do jogo REDUZ (currentDelay aumenta 50 ms, até o limite do valor base)

---------------------------
MECÂNICA DA REDE (NET FAULT)
---------------------------

Existe uma rede no centro da tela. Sempre que a bola a cruza, o programa testa se houve "net fault":

- Se o ÚLTIMO TOQUE foi do JOGADOR:
  * Chance de erro aumenta conforme a dificuldade do computador
  * Fórmula da chance: `10% + (dificuldade - 1) * 8%`

- Se o ÚLTIMO TOQUE foi do COMPUTADOR:
  * Chance de erro é o COMPLEMENTO da chance do jogador
  * Fórmula da chance: `100% - (chance do jogador)`

Se o teste for positivo (houve net fault), o adversário marca ponto automaticamente
e o próximo saque será dele.

---------------------------
HABILIDADES (POWER-UPS)
---------------------------

As habilidades aparecem no campo de forma aleatória com uma frequência definida pelo jogador.
Elas só funcionam se a bola que colidiu com elas foi tocada POR VOCÊ (jogador).

Tipos:
- **'+' (aceleração):** acelera o jogo (reduz currentDelay em até 20 ms)
- **'-' (desaceleração):** desacelera o jogo (aumenta currentDelay em até 20 ms)
- **'*' (clonagem):** multiplica a bola atual em 2 a 5 bolas, criando confusão no campo

---------------------------
PONTUAÇÃO E SAQUE
---------------------------

- Sempre que uma bola atravessa as bordas laterais, o adversário marca ponto.
- A bola seguinte surge na raquete do jogador que ganhou o ponto.
- O jogo segue até que um dos lados alcance o número de SETS definidos.

---------------------------
COMO COMPILAR E JOGAR
---------------------------

Você pode executar o jogo de três maneiras:

1. **Executável local (.exe):**
   - Clique duas vezes no arquivo `teste.exe` (Windows)

2. **Compilador Online (ex: GDB Online):**
   - Acesse https://www.onlinegdb.com/
   - Cole o código-fonte, escolha a linguagem "c" e clique em "Run"

3. **Visual Studio Code + GCC:**
   - Abra a pasta com o arquivo `teste.c`
   - Compile com: `gcc teste.c -o teste`
   - Execute com: `./teste` (Linux/macOS) ou `teste.exe` (Windows)

---------------------------
OBSERVAÇÕES FINAIS
---------------------------
- O jogo continua indefinidamente até que o jogador aperte a tecla Q.
- Pode ser executado tanto no Windows como em terminais UNIX-like.
- Usa apenas estruturas simples de C: `if`, `for`, `while`, `switch`, `I/O`, `struct`, `random` e `matrizes`.
