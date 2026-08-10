# Análise no lugar das raízes (root locus)

## Tópicos
- Regras gerais para construção do lugar das raízes
- Interpretação do gráfico do lugar das raízes
- Lugar das raízes para sistemas com retardo de transporte


### 1. Introdução ao Método do Lugar das Raízes (M.L.R.)
O LGR é o conjunto de todos os pontos no plano $s$ que correspondem às raízes da equação característica de malha fechada quando o ganho $K$ varia de $0$ a $+\infty$.
*   **Equação Característica:** $1 + G(s)H(s) = 0$ ou $G(s)H(s) = -1$.
*   **Utilidade:** Permite determinar a estabilidade absoluta e relativa do sistema, além de auxiliar na escolha da estrutura do controlador (P, PI, PD, PID).

### 2. Condições Fundamentais
Para que um ponto $s$ pertença ao LGR, ele deve satisfazer duas condições baseadas na forma complexa de $G(s)H(s)$:

*   **Condição de Fase (ou Ângulo):** É a condição primária para traçar o gráfico. O ângulo total de $G(s)H(s)$ deve ser um múltiplo ímpar de $180^\circ$:
    $\angle G(s)H(s) = \pm 180^\circ(2k + 1), \quad k = 0, 1, 2, \dots$.
*   **Condição de Módulo (ou Ganho):** Utilizada para calcular o valor de $K$ associado a um ponto específico já identificado no LGR:
    $|G(s)H(s)| = 1 \quad \Rightarrow \quad K = \frac{\prod \text{distâncias dos polos}}{\prod \text{distâncias dos zeros}}$.

### 3. Regras para Construção do LGR
Seguindo estes passos sistemáticos, é possível esboçar o comportamento do sistema:

1.  **Número de Ramos:** O LGR possui $n$ ramos, onde $n$ é o número de polos de malha aberta.
2.  **Simetria:** O gráfico é sempre simétrico em relação ao eixo real.
3.  **Início e Término:** Os ramos partem dos **polos** de malha aberta ($K=0$) e terminam nos **zeros** de malha aberta ou no infinito ($K \to \infty$).
4.  **LGR no Eixo Real:** Um ponto no eixo real pertence ao LGR se o número total de polos e zeros reais à sua direita for **ímpar**.
5.  **Assíntotas:** Se houver mais polos ($n$) do que zeros ($m$), $n-m$ ramos tendem ao infinito seguindo assíntotas:
    *   **Ângulo:** $\theta_a = \frac{(2k+1)180^\circ}{n-m}$.
    *   **Centro de Cruzamento:** $\sigma_a = \frac{\sum \text{polos} - \sum \text{zeros}}{n-m}$.
6.  **Pontos de Partida e Chegada (Breakaway/Break-in):** Ocorrem no eixo real onde ramos se encontram e se separam. São calculados resolvendo $\frac{dK}{ds} = 0$.

### 4. Refinamentos do Gráfico
*   **Cruzamento com o Eixo Imaginário:** Determina o ganho crítico ($K_{cr}$) para a estabilidade. Pode ser calculado via Critério de Routh-Hurwitz (fazendo a linha $s^1$ nula) ou substituindo $s = j\omega$ na equação característica.
*   **Ângulos de Partida/Chegada:** Para polos ou zeros complexos, o ângulo de saída/entrada é calculado somando as contribuições angulares de todas as outras singularidades no ponto em questão.

### 5. Efeito da Adição de Polos e Zeros
*   **Adição de Polos:** Desloca o LGR para a **direita**, reduzindo a estabilidade e tornando a resposta mais lenta.
*   **Adição de Zeros:** Desloca o LGR para a **esquerda**, aumentando a estabilidade, diminuindo o tempo de acomodação e introduzindo um efeito antecipatório (como na ação Derivativa).

### 6. Exemplo de Estrutura para o GitHub
Você pode incluir um script em MATLAB/Octave para ilustrar:
```matlab
% Definição do sistema G(s)H(s) = K / [s(s+1)(s+2)]
num =;
den = ;
sys = tf(num, den);
rlocus(sys); % Gera o gráfico do LGR
grid on; title('Lugar Geométrico das Raízes');
```
*   **Nota:** O MATLAB utiliza a função `rlocus` para automatizar este processo.

Esta estrutura fornece a fundamentação teórica, as regras práticas de desenho e a interpretação física necessária para o estudo de sistemas de controle via LGR.


## Conteúdo
- `material/` — resumos e exercícios
- `notebooks/` — simulações
- `scripts/` — scripts MATLAB/Octave
