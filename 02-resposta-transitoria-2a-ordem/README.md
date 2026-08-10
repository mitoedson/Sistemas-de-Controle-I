# Resposta transitória e de regime estacionário: sistemas de 2ª ordem

Análise de resposta transitória e de regime estacionário de sistemas de 2ª ordem a partir de suas funções de transferência.

## Tópicos
- Função de transferência de sistemas de 2ª ordem
- Coeficiente de amortecimento, frequência natural
- Overshoot, tempo de acomodação, tempo de pico


### 1. Definição e Função de Transferência Padrão
Um sistema de segunda ordem é caracterizado por possuir dois polos. A sua **função de transferência (FT)** canônica é expressa como:

$$G(s) = \frac{C(s)}{R(s)} = \frac{\omega_n^2}{s^2 + 2\zeta\omega_ns + \omega_n^2}$$

Onde:
*   **$(\omega_n$):** Frequência natural não amortecida, que representa a frequência de oscilação do sistema se o amortecimento fosse nulo.
*   **$(\zeta$) (Zeta):** Coeficiente de amortecimento, que define o quão "suave" ou "oscilatória" será a resposta.
*   **Polos do sistema:** Localizados em $s = -\zeta\omega_n \pm \omega_n\sqrt{\zeta^2 - 1}$.

### 2. Tipos de Resposta (Baseado em $(\zeta$))
O comportamento dinâmico depende diretamente do valor do coeficiente de amortecimento:

*   **Sem amortecimento ($\zeta = 0$):** Os polos são puramente imaginários ($\pm j\omega_n$). A resposta é uma oscilação sustentada (senoidal pura).
*   **Subamortecido ($0 < \zeta < 1$):** Os polos são complexos conjugados. A resposta apresenta oscilações que decaem exponencialmente até o regime permanente. É o caso mais comum em estudos de controle.
*   **Criticamente amortecido ($\zeta = 1$):** Possui dois polos reais e iguais. É a resposta mais rápida possível sem apresentar oscilações.
*   **Sobreamortecido ($\zeta > 1$):** Possui dois polos reais e distintos. A resposta é lenta e não oscilatória.

### 3. Especificações da Resposta Transitória (Caso Subamortecido)
Para avaliar o desempenho de um sistema subamortecido frente a um degrau unitário, utilizam-se os seguintes parâmetros:

*   **Tempo de Subida ($t_r$):** Tempo necessário para a resposta atingir o valor final pela primeira vez.
    *   *Fórmula:* $t_r = \frac{\pi - \beta}{\omega_d}$, onde $\omega_d = \omega_n\sqrt{1-\zeta^2}$ e $\beta = \cos^{-1}(\zeta)$.
*   **Tempo de Pico ($t_p$):** Tempo para atingir o valor máximo da resposta (primeiro pico).
    *   *Fórmula:* $t_p = \frac{\pi}{\omega_d}$.
*   **Sobressinal Máximo ($M_p$):** O quanto a resposta ultrapassa o valor final, geralmente expresso em porcentagem.
    *   *Fórmula:* $M_p = e^{-(\zeta\pi / \sqrt{1-\zeta^2}}$.
*   **Tempo de Acomodação ($t_s$):** Tempo para a resposta entrar e permanecer em uma faixa de tolerância (2% ou 5%).
    *   *Fórmula (2%):* $t_s \approx \frac{4}{\zeta\omega_n}$.

### 4. Análise de Regime Estacionário
A análise de erro em regime permanente ($e_{ss}$) depende do **Tipo do Sistema** (número de integradores puros na malha aberta):

*   **Erro ao Degrau:** Para o sistema de 2ª ordem padrão (Tipo 0 com ganho unitário), o erro estacionário ao degrau é **nulo**, pois a saída iguala a entrada no infinito.
*   **Erro à Rampa:** Apresenta um erro finito dado por $e_{ss} = \frac{2\zeta}{\omega_n}$ (para sistemas de malha fechada estáveis com realimentação unitária).

### 5. Exemplo Clássico: Sistema Massa-Mola-Amortecedor
Este sistema físico é o modelo base para sistemas de 2ª ordem:
*   **Equação Diferencial:** $m\ddot{y} + c\dot{y} + ky = u(t)$.
*   **Parâmetros de Controle:**
    *   $\omega_n = \sqrt{k/m}$.
    *   $\zeta = \frac{c}{2\sqrt{mk}}$.

### 6. Dica para o GitHub: Comandos MATLAB
Você pode adicionar exemplos de código para simular esses sistemas:
*   `[num, den] = ord2(wn, zeta)`: Gera o numerador e denominador de um sistema padrão.
*   `step(num, den)`: Plota a resposta ao degrau e permite visualizar as especificações.
*   `rlocfind` ou `rlocus`: Para análise da variação do ganho $K$ na localização dos polos.

Esta estrutura fornece uma visão completa, desde a teoria matemática até a aplicação prática e simulação computacional.

## Conteúdo
- `material/` — resumos e exercícios
- `notebooks/` — simulações
- `scripts/` — scripts MATLAB/Octave
