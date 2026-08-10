# Resposta transitória e de regime estacionário: sistemas de 1ª ordem

Análise de resposta transitória e de regime estacionário de sistemas de 1ª ordem a partir de suas funções de transferência.

## Tópicos
- Função de transferência de sistemas de 1ª ordem
- Constante de tempo, resposta ao degrau
- Resposta transitória vs. regime estacionário


### 1. Definição de Sistemas de 1ª Ordem
Um sistema de primeira ordem é matematicamente descrito por uma equação diferencial linear de primeira ordem. No domínio da frequência (Laplace), sua **função de transferência (FT)** padrão é expressa como:

$$G(s) = \frac{C(s)}{R(s)} = \frac{K}{Ts + 1}$$

Onde:
*   **K (ou $\gamma$):** Ganho estático do sistema.
*   **T:** Constante de tempo, que define a rapidez com que o sistema responde a uma entrada.
*   **Polo:** O sistema possui um único polo real localizado em $s = -\frac{1}{T}$.

### 2. Análise da Resposta Transitória
A resposta transitória descreve o comportamento do sistema desde o estado inicial até atingir o estado final.

#### A. Resposta ao Degrau Unitário
Quando uma entrada degrau ($R(s) = 1/s$) é aplicada, a saída no tempo (para K=1) é dada por:

$$c(t) = 1 - e^{-t/T}, \quad t \geq 0$$

*   **Significado de T:** No instante t = T, a saída atinge aproximadamente **63,2%** do seu valor final.
*   **Tempo de Acomodação ($t_s$):** É o tempo necessário para a resposta entrar em uma faixa de tolerância (geralmente 2% ou 5%) do valor final. Para o critério de 2%, o tempo de acomodação é de aproximadamente **4T**.

#### B. Resposta à Rampa Unitária
Para uma entrada rampa ($R(s) = 1/s^2$), a resposta é:
$c(t) = t - T + Te^{-t/T}, \quad t \geq 0$.
Neste caso, a saída tenta seguir a rampa, mas apresenta um atraso constante igual a T em relação à entrada.

#### C. Resposta ao Impulso Unitário
Com uma entrada impulso (R(s) = 1), a resposta é a própria transformada inversa da FT:
$c(t) = \frac{1}{T} e^{-t/T}, \quad t \geq 0$

### 3. Análise de Regime Estacionário
A análise de regime permanente estuda o comportamento da saída quando o tempo tende ao infinito $(t \to \infty)$.

*   **Erro Estacionário $(e_{ss}$):** É a diferença entre a entrada e a saída em regime permanente.
*   **Entrada Degrau:** Se o sistema for de Tipo 0 (como o padrão de 1ª ordem sem integradores puros), o erro estacionário para um degrau de amplitude (A) é finito e dado por $e_{ss} = \frac{A}{1+K_p}$, onde $K_p$ é a constante de erro de posição.
*   **Entrada Rampa:** Para sistemas de 1ª ordem típicos, o erro estacionário para uma rampa unitária é igual à constante de tempo **T**.

### 4. Exemplos Práticos e Modelagem
Sistemas de primeira ordem são comuns em diversas áreas da engenharia:
*   **Térmica:** Um termômetro pode ser modelado por uma FT de 1ª ordem, como no exemplo $G(s) = \frac{1}{90s + 1}$.
*   **Hidráulica:** Um tanque de nível com escoamento laminar na saída possui a função de transferência $\frac{H(s)}{Q_E(s)} = \frac{R}{RAs + 1}$, onde RA é a constante de tempo.
*   **Elétrica:** Circuitos RC série, onde a saída é a tensão no capacitor.

### 5. Dica para o GitHub: Simulação em MATLAB/Octave
Para enriquecer seu repositório, você pode incluir scripts que utilizem os comandos:
*   sys = tf(num, den): Define a função de transferência.
*   step(sys): Plota a resposta ao degrau.
*   impulse(sys): Plota a resposta ao impulso.

Este conteúdo oferece uma base sólida e tecnicamente referenciada para o seu material de estudos.
















## Conteúdo
- `material/` — resumos e exercícios
- `notebooks/` — simulações
- `scripts/` — scripts MATLAB/Octave
