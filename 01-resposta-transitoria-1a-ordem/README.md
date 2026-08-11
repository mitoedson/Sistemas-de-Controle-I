# Resposta transitória e de regime estacionário: sistemas de 1ª ordem

Análise de resposta transitória e de regime estacionário de sistemas de 1ª ordem a partir de suas funções de transferência.

## Tópicos
- Função de transferência de sistemas de 1ª ordem
- Constante de tempo, resposta ao degrau
- Resposta transitória vs. regime estacionário


### 1. Exemplo motivacional: a EDO livre $\dot{x}(t) = \alpha x(t)$

Antes de generalizar, vale a pena ver a conversão EDO → Laplace no exemplo mais simples possível: a resposta livre (sem entrada externa) de um sistema de 1ª ordem, cuja solução clássica é a exponencial

$$x(t) = x_0 e^{\alpha t}$$

Essa função é solução da EDO homogênea

$$\dot{x}(t) = \alpha\ x(t), \qquad x(0) = x_0$$

**Sem Laplace (separação de variáveis):**

$$\frac{dx}{x} = \alpha dt \Longrightarrow \int \frac{dx}{x} = \int \alpha\ dt \Longrightarrow \ln x = \alpha t + C$$

Aplicando exponencial e usando $x(0) = x_0$ para determinar a constante $C$:

$$x(t) = e^{C}e^{\alpha t} \qquad x(0) = e^{C} = x_0 \Longrightarrow x(t) = x_0 e^{\alpha t}$$

Esse método funciona bem para essa EDO isolada, mas deixa de ser prático assim que a equação passa a ter uma entrada externa $r(t)$ ou quando vários subsistemas são interligados — a separação de variáveis não se generaliza diretamente para esses casos.

**Com Laplace (método algébrico):**

Aplicando a transformada de Laplace em $\dot{x}(t) = \alpha x(t)$, com $\mathcal{L}\{\dot{x}(t)\} = sX(s) - x(0)$:

$$sX(s) - x_0 = \alpha X(s)\Longrightarrow X(s)(s-\alpha) = x_0 \Longrightarrow X(s) = \frac{x_0}{s-\alpha}$$

A EDO virou uma equação puramente algébrica em $s$. Para voltar ao domínio do tempo, basta reconhecer a forma padrão $\mathcal{L}^{-1}\{1/(s-a)\} = e^{at}$:

```math
x(t) = \mathcal{L}^{-1} \left \{\frac{x_0}{s-\alpha}\right\} = x_0 e^{\alpha t}
```

— o mesmo resultado obtido sem Laplace, confirmando que a transformada não altera a resposta; ela apenas troca o tipo de problema (cálculo → álgebra).

**Ligação com sistemas de 1ª ordem:** fazendo $\alpha = -1/T$ (sistema estável, $T>0$),

$$X(s) = \frac{x_0}{s+1/T} \quad\Longrightarrow\quad x(t) = x_0\,e^{-t/T}$$

Essa é a resposta natural (livre) de um sistema de 1ª ordem, com o mesmo polo $s=-1/T$ e a mesma constante de tempo $T$ que reaparecem na função de transferência $G(s) = K/(Ts+1)$ discutida a seguir. A localização desse único polo no plano $s$ já determina toda a velocidade da resposta no tempo — sem que seja necessário resolver a EDO explicitamente a cada análise.

### 2. Da EDO à Função de Transferência: por que usar Laplace?

Todo sistema físico de 1ª ordem é descrito, no domínio do tempo, por uma **equação diferencial ordinária (EDO)** linear e invariante no tempo. Para um sistema genérico com entrada $r(t)$ e saída $c(t)$, essa equação tem a forma:

$$T\,\dot{c}(t) + c(t) = K\,r(t)$$

onde $T$ é a constante de tempo e $K$ o ganho estático do sistema.

**O problema de trabalhar direto com a EDO:**
*   Resolver a EDO exige lidar com condições iniciais e métodos de solução (fator integrante, resposta homogênea + particular) a cada nova entrada considerada (degrau, rampa, impulso, senoidal etc.).
*   Quando dois ou mais subsistemas são interligados — em série, em paralelo ou com realimentação —, a EDO resultante do conjunto se torna cada vez mais complexa, pois é preciso combinar as equações diferenciais de cada bloco.
*   Não existe uma forma simples e direta de representar a associação de blocos (como soma, produto ou malha fechada) manipulando apenas EDOs.

**A solução: Transformada de Laplace**

Aplicando a Transformada de Laplace na EDO (com condições iniciais nulas), as operações de derivação no tempo viram multiplicação por $s$ no domínio da frequência complexa. A equação diferencial se transforma em uma **equação puramente algébrica**:

$$T\,s\,C(s) + C(s) = K\,R(s) \quad \Longrightarrow \quad C(s)\,(Ts + 1) = K\,R(s)$$

Isolando a razão saída/entrada, obtemos a **função de transferência**:

$$G(s) = \frac{C(s)}{R(s)} = \frac{K}{Ts + 1}$$

É justamente essa representação algébrica que:
*   Permite a **álgebra de diagramas de blocos** (blocos em série se multiplicam, blocos em paralelo se somam, a malha fechada tem uma fórmula direta), sem jamais precisar resolver a EDO combinada do sistema completo;
*   Concentra toda a dinâmica do sistema em um único objeto matemático — a FT —, cujos polos e zeros já revelam informações sobre a resposta transitória (constante de tempo, velocidade de resposta) e sobre o regime estacionário (por meio do teorema do valor final), sem a necessidade de resolver a equação no tempo a cada nova análise.

Por isso, o estudo de sistemas de controle parte de Laplace e das funções de transferência como ferramenta padrão, deixando a EDO apenas como o ponto de partida físico do problema.

### 3. Definição de Sistemas de 1ª Ordem
Um sistema de primeira ordem é matematicamente descrito por uma equação diferencial linear de primeira ordem. No domínio da frequência (Laplace), sua **função de transferência (FT)** padrão é expressa como:

$$G(s) = \frac{C(s)}{R(s)} = \frac{K}{Ts + 1}$$

Onde:
*   **K (ou $\gamma$):** Ganho estático do sistema.
*   **T:** Constante de tempo, que define a rapidez com que o sistema responde a uma entrada.
*   **Polo:** O sistema possui um único polo real localizado em $s = -\frac{1}{T}$.

### 4. Análise da Resposta Transitória
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

### 5. Análise de Regime Estacionário
A análise de regime permanente estuda o comportamento da saída quando o tempo tende ao infinito $(t \to \infty)$.

*   **Erro Estacionário $(e_{ss}$):** É a diferença entre a entrada e a saída em regime permanente.
*   **Entrada Degrau:** Se o sistema for de Tipo 0 (como o padrão de 1ª ordem sem integradores puros), o erro estacionário para um degrau de amplitude (A) é finito e dado por $e_{ss} = \frac{A}{1+K_p}$, onde $K_p$ é a constante de erro de posição.
*   **Entrada Rampa:** Para sistemas de 1ª ordem típicos, o erro estacionário para uma rampa unitária é igual à constante de tempo **T**.

### 6. Exemplos Práticos e Modelagem
Sistemas de primeira ordem são comuns em diversas áreas da engenharia:
*   **Térmica:** Um termômetro pode ser modelado por uma FT de 1ª ordem, como no exemplo $G(s) = \frac{1}{90s + 1}$.
*   **Hidráulica:** Um tanque de nível com escoamento laminar na saída possui a função de transferência $\frac{H(s)}{Q_E(s)} = \frac{R}{RAs + 1}$, onde RA é a constante de tempo.
*   **Elétrica:** Circuitos RC série, onde a saída é a tensão no capacitor.

### 7. Dica para o GitHub: Simulação em MATLAB/Octave
Para enriquecer seu repositório, você pode incluir scripts que utilizem os comandos:
*   sys = tf(num, den): Define a função de transferência.
*   step(sys): Plota a resposta ao degrau.
*   impulse(sys): Plota a resposta ao impulso.

Este conteúdo oferece uma base sólida e tecnicamente referenciada para o seu material de estudos.
















## Conteúdo
- `material/` — resumos e exercícios
- `notebooks/` — simulações
- `scripts/` — scripts MATLAB/Octave
