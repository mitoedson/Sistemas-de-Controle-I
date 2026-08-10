# Projeto de sistemas de controle pelo método do lugar das raízes

## Tópicos
- Compensação por avanço de fase
- Compensação por atraso de fase
- Compensação por avanço e atraso de fase


### 1. Introdução ao Projeto via M.L.R.
O projeto de controladores envolve a escolha da localização dos polos e zeros de malha fechada para atender especificações de desempenho, o que é traduzido na escolha da estrutura e dos parâmetros do controlador (P, PI, PD ou PID). O método do LGR é fundamental nesse processo pois permite visualizar o deslocamento dos polos à medida que um parâmetro, geralmente o ganho $K$, é alterado.

### 2. Especificações de Desempenho e o Plano $s$
Antes de projetar, é necessário traduzir os requisitos de regime transitório em localizações desejadas no plano complexo:
*   **Coeficiente de amortecimento ($\zeta$):** Define o ângulo das retas de amortecimento constante a partir da origem ($\beta = \cos^{-1}\zeta$).
*   **Frequência Natural ($\omega_n$):** Define a distância radial do polo até a origem.
*   **Tempo de Acomodação ($t_s$):** Define uma região à esquerda de uma reta vertical $\sigma = 4/t_s$ (para o critério de 2%).
*   **Overshoot ($M_p$):** Relacionado diretamente ao $\zeta$.

### 3. Tipos de Compensadores e Seus Efeitos
O projetista manipula o LGR através da adição de polos e zeros:

#### A. Adição de Zeros (Compensação por Avanço ou Lead)
*   **Efeito:** "Puxa" o LGR para a esquerda.
*   **Impacto:** Aumenta a estabilidade relativa e diminui o tempo de acomodação (resposta mais rápida).
*   **Estrutura:** Um compensador de avanço de fase é definido como $G_c(s) = K_c \frac{s + 1/T}{s + 1/(\alpha T)}$, com $0 < \alpha < 1$.

#### B. Adição de Polos (Compensação por Atraso ou Lag)
*   **Efeito:** "Puxa" o LGR para a direita.
*   **Impacto:** Reduz a estabilidade relativa, mas é utilizado para melhorar o erro em regime permanente (como a ação integral).
*   **Estrutura:** Um compensador de atraso possui a mesma forma do avanço, mas com a condição $\alpha > 1$ (ou seja, o polo fica mais próximo da origem que o zero).

#### C. Controladores PID no LGR
*   **PI:** Adiciona um polo na origem e um zero real.
*   **PD:** Adiciona apenas um zero, agindo como um avanço de fase simplificado.
*   **PID:** Adiciona um polo na origem e dois zeros, permitindo melhorar tanto o erro estacionário quanto o regime transitório.

### 4. Metodologia de Projeto (Passo a Passo)
Para projetar um compensador para que o sistema passe por um polo desejado $s_d$:

1.  **Verificação da Condição de Ângulo:** Calcula-se a contribuição angular de todos os polos e zeros de malha aberta no ponto $s_d$. A deficiência angular necessária ($\phi$) para que $s_d$ pertença ao LGR é dada por:
    $\sum \phi_{zeros} - \sum \theta_{polos} = \pm 180^\circ(2k+1)$.
2.  **Posicionamento de Polos/Zeros do Compensador:** Escolhe-se a localização do polo e do zero do compensador para suprir a deficiência $\phi$.
3.  **Cálculo do Ganho $K$:** Uma vez que $s_d$ está no novo LGR, utiliza-se a **condição de módulo** para encontrar o ganho necessário:
    $K = \frac{\prod \text{distâncias aos polos}}{\prod \text{distâncias aos zeros}}$.
4.  **Verificação:** Simula-se a resposta ao degrau do sistema compensado para garantir que outros polos (não dominantes) não prejudiquem o desempenho.


### 5. Técnicas de Compensação pelo LGR
O projeto de compensadores visa alterar a dinâmica da planta original para que o sistema de malha fechada atenda a requisitos que não seriam atingidos apenas com o ajuste de ganho.

#### A. Compensação por Avanço de Fase (Phase-Lead)
Esta técnica é utilizada principalmente para melhorar a **resposta transitória** (tornar o sistema mais rápido) e aumentar a **estabilidade relativa**.
*   **Função de Transferência:** $G_c(s) = K_c \alpha \frac{Ts+1}{\alpha Ts + 1} = K_c \frac{s + 1/T}{s + 1/(\alpha T)}$, com $0 < \alpha < 1$.
*   **Configuração Polo-Zero:** O zero ($-1/T$) é posicionado à direita do polo ($-1/\alpha T$) no plano complexo.
*   **Efeito no LGR:** A adição do par polo-zero de avanço gera uma contribuição angular positiva, o que "puxa" os ramos do LGR para a **esquerda** do plano $s$.
*   **Impacto Prático:** Reduz o tempo de subida ($t_r$) e o tempo de acomodação ($t_s$), agindo de forma análoga à ação derivativa (PD).

#### B. Compensação por Atraso de Fase (Phase-Lag)
A compensação por atraso é aplicada quando o desempenho transitório já é satisfatório, mas o **erro em regime permanente** é inaceitável.
*   **Função de Transferência:** Segue a mesma forma do avanço, mas com a condição $\alpha > 1$ (ou $a > b$ no circuito), o que coloca o polo mais próximo da origem do que o zero.
*   **Configuração Polo-Zero:** O zero é posicionado à esquerda do polo. Geralmente, ambos são colocados muito próximos da origem para não alterar significativamente o formato original do LGR.
*   **Efeito no LGR:** Introduz uma contribuição angular negativa pequena, focando em aumentar o ganho de malha aberta nas baixas frequências.
*   **Impacto Prático:** Melhora a constante de erro ($K_p, K_v, K_a$) e reduz o erro estacionário ($e_{ss}$), assemelhando-se à ação integral (PI).

#### C. Compensação por Avanço e Atraso de Fase (Lead-Lag)
Esta técnica combina as duas anteriores para obter melhorias simultâneas no **regime transitório** e no **regime estacionário**.
*   **Função de Transferência:** É o produto de um estágio de avanço e um de atraso: $G_c(s) = K_c \frac{(s + a_1)(s + a_2)}{(s + b_1)(s + b_2)}$, onde $a_1 < b_1$ (avanço) e $a_2 > b_2$ (atraso).
*   **Metodologia de Projeto:**
    1.  Projeta-se a parte de **avanço** para posicionar os polos dominantes de malha fechada e garantir a rapidez desejada.
    2.  Projeta-se a parte de **atraso** para ajustar o erro de regime, garantindo que o polo e o zero adicionados não desloquem os polos dominantes já definidos.
*   **Impacto Prático:** Resulta em um sistema que é ao mesmo tempo rápido, estável e preciso.

---

### Resumo Comparativo para o Repositório
| Tipo de Compensador | Foco Principal | Efeito no LGR | Ação PID Equivalente |
| :--- | :--- | :--- | :--- |
| **Avanço (Lead)** | Rapidez / Estabilidade | Desloca para a Esquerda | Derivativo (PD) |
| **Atraso (Lag)** | Precisão (Erro) | Mantém o LGR (baixas freq.) | Integral (PI) |
| **Avanço-Atraso** | Rapidez + Precisão | Combinação de ambos | PID completo |

**Dica de Implementação (MATLAB/Octave):**
Para projetar esses compensadores, você pode utilizar a ferramenta `sisotool`, que permite arrastar polos e zeros interativamente no LGR e visualizar a resposta ao degrau em tempo real.

### 6. Dica de Simulação no MATLAB/Octave
Para facilitar o projeto no GitHub, você pode sugerir o uso de ferramentas interativas:
*   `rlocus(sys)`: Plota o LGR.
*   `sgrid`: Sobrepõe as linhas de $\zeta$ e $\omega_n$ constantes no gráfico.
*   `rlocfind(sys)`: Permite clicar em um ponto do LGR para obter o ganho $K$ e as coordenadas exatas dos polos.


## Conteúdo
- `material/` — resumos e exercícios
- `notebooks/` — simulações
- `scripts/` — scripts MATLAB/Octave
