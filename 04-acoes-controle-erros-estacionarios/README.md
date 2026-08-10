# Ações de controle integral e derivativo; erros estacionários

## Tópicos
- Efeitos das ações de controle proporcional, integral e derivativo
- Erros estacionários em sistemas com realimentação unitária
- Tipos de sistema e constantes de erro (Kp, Kv, Ka)


### 1. Ações de Controle PID
Os controladores industriais geralmente utilizam combinações de três ações básicas: Proporcional (P), Integral (I) e Derivativa (D).

#### A. Ação Proporcional (P)
*   **Definição:** O sinal de controle é proporcional ao erro: $u(t) = K_p e(t)$.
*   **Efeito:** Aumentar o ganho $K_p$ reduz o erro de regime permanente, mas geralmente torna o sistema mais oscilatório e pode levá-lo à instabilidade.

#### B. Ação Integral (I)
*   **Definição:** O sinal de controle baseia-se na integral do erro no tempo: $u(t) = K_i \int_{0}^{t} e(\tau) d\tau$.
*   **Objetivo Principal:** **Eliminar o erro residual (estacionário)**.
*   **Características:** 
    *   Aumenta o **Tipo do Sistema** em uma unidade.
    *   Permite que o sinal de controle seja não nulo mesmo quando o erro atinge zero.
    *   **Desvantagem:** Tende a degradar a estabilidade relativa e tornar a resposta mais lenta ou oscilatória.

#### C. Ação Derivativa (D)
*   **Definição:** O sinal de controle baseia-se na taxa de variação do erro: $u(t) = K_d \frac{de(t)}{dt}$.
*   **Objetivo Principal:** Introduzir um efeito de **antecipação**, reagindo à tendência futura do erro.
*   **Características:**
    *   Aumenta o amortecimento e melhora a estabilidade transitória.
    *   **Não é usada sozinha**, pois não responde a erros constantes (cuja derivada é zero).
    *   **Desvantagem:** Amplifica ruídos de alta frequência, o que pode saturar os atuadores.

---

### 2. Análise de Erros Estacionários ($e_{ss}$)
O erro estacionário mede a precisão de um sistema em seguir uma entrada de referência após o desaparecimento do transiente.

#### A. O Teorema do Valor Final
O erro no domínio do tempo quando $t \to \infty$ é calculado no domínio de Laplace como:
\\[e_{ss} = \lim_{s \to 0} s E(s) = \lim_{s \to 0} \frac{s R(s)}{1 + G(s)H(s)}\\].

#### B. Classificação por Tipo de Sistema ($N$)
O erro estacionário depende do número de integradores puros ($1/s^N$) na função de transferência de malha aberta $G(s)H(s)$.

1.  **Sistema Tipo 0:** Sem integradores. Possui erro finito para entrada degrau e erro infinito para rampa.
2.  **Sistema Tipo 1:** Um integrador (ex: ação Integral no controlador). Erro zero para degrau e erro finito para rampa.
3.  **Sistema Tipo 2:** Dois integradores. Erro zero para degrau e rampa; erro finito para entrada parábola.

---

### 3. Constantes de Erro Estático
São "figuras de mérito" que indicam a capacidade de precisão do sistema:

*   **Constante de Posição ($K_p$):** $\lim_{s \to 0} G(s)$. Relacionada ao erro de degrau: $e_{ss} = \frac{1}{1 + K_p}$.
*   **Constante de Velocidade ($K_v$):** $\lim_{s \to 0} s G(s)$. Relacionada ao erro de rampa: $e_{ss} = \frac{1}{K_v}$.
*   **Constante de Aceleração ($K_a$):** $\lim_{s \to 0} s^2 G(s)$. Relacionada ao erro de parábola: $e_{ss} = \frac{1}{K_a}$.

---

### 4. Rejeição de Distúrbios
Para rejeitar completamente um distúrbio (como um torque de carga) em regime permanente, o sistema deve possuir um integrador **antes** do ponto de entrada do distúrbio.
*   Um distúrbio degrau requer pelo menos um polo na origem no controlador.
*   Um distúrbio rampa requer pelo menos dois polos na origem no controlador.

---

### 5. Resumo para o GitHub
| Entrada | Tipo 0 | Tipo 1 | Tipo 2 |
| :--- | :--- | :--- | :--- |
| **Degrau (Posição)** | Finito ($\frac{1}{1+K_p}$) | 0 | 0 |
| **Rampa (Velocidade)** | $\infty$ | Finito ($\frac{1}{K_v}$) | 0 |
| **Parábola (Aceleração)** | $\infty$ | $\infty$ | Finito ($\frac{1}{K_a}$) |
.

**Dica de Simulação (MATLAB/Octave):**
Para demonstrar o efeito da ação Integral, você pode comparar a resposta ao degrau de um sistema de 1ª ordem puro com a de um sistema com controlador PI, utilizando `step(feedback(controlador*planta, 1))`. O PI deverá levar a saída exatamente ao valor de referência (erro zero), enquanto o P puro apresentará um desvio (offset).


## Conteúdo
- `material/` — resumos e exercícios
- `notebooks/` — simulações
- `scripts/` — scripts MATLAB/Octave
