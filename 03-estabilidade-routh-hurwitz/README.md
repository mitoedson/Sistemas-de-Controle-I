# 03 — Análise de estabilidade: critério de Routh-Hurwitz

## Tópicos
- Construção da tabela de Routh
- Casos especiais (linha de zeros, primeiro elemento nulo)
- Determinação de faixas de estabilidade em função de parâmetros


### 1. Conceitos Fundamentais de Estabilidade
*   **Estabilidade BIBO:** Um sistema é estável se, e somente se, para qualquer entrada limitada, a saída correspondente também for limitada.
*   **Localização dos Polos:** Para sistemas lineares invariantes no tempo (SLIT), a condição necessária e suficiente para a estabilidade é que todos os polos da função de transferência de malha fechada estejam no **semiplano esquerdo aberto** do plano complexo $s$ (parte real negativa).
*   **Estabilidade Marginal:** Ocorre quando há polos sobre o eixo imaginário ($j\omega$). Nesse caso, o sistema apresenta oscilações sustentadas.

### 2. O Critério de Routh-Hurwitz
Este critério matemático indica se existem raízes instáveis em uma equação polinomial com coeficientes reais.

#### A. Condições Necessárias (Teste de Hurwitz)
Antes de construir a tabela, verifica-se se o polinômio $A(s) = a_0 s^n + a_1 s^{n-1} + \dots + a_n$ atende a:
1.  **Presença de todos os coeficientes:** Nenhum coeficiente deve ser nulo.
2.  **Sinal constante:** Todos os coeficientes devem ter o mesmo sinal (geralmente positivos).
*Nota: Se qualquer uma dessas condições falhar, o sistema é instável ou marginalmente estável.*

#### B. Construção da Tabela de Routh
A tabela é organizada em linhas correspondentes às potências de $s$, começando da maior para a menor:
*   As duas primeiras linhas são preenchidas com os coeficientes do polinômio.
*   As linhas subsequentes são calculadas através de determinantes negativos das duas linhas anteriores.

**Interpretação:** O número de raízes com parte real positiva (instáveis) é igual ao número de **mudanças de sinal** nos elementos da primeira coluna da tabela.

### 3. Casos Especiais
Quando a construção da tabela é interrompida por zeros, aplicam-se procedimentos específicos:
*   **Zero na primeira coluna (demais elementos da linha não nulos):** Substitui-se o zero por um valor infinitesimal positivo $\epsilon$ e prossegue-se o cálculo. Ao final, analisa-se o sinal dos termos em função de $\epsilon \to 0$.
*   **Linha inteira de zeros:** Indica a presença de raízes simétricas (como polos imaginários puros). Cria-se um **polinômio auxiliar $P(s)$** com a linha imediatamente superior e substitui-se a linha nula pelos coeficientes da derivada $dP(s)/ds$.

### 4. Aplicações Práticas
O critério é amplamente utilizado para:
*   **Determinar faixas de ganho $K$:** Encontrar o intervalo de valores de um parâmetro (como o ganho de um controlador) que mantém o sistema estável.
*   **Análise do Lugar das Raízes (LGR):** Calcular os pontos exatos onde os ramos do LGR cruzam o eixo imaginário e o ganho crítico associado a essa transição.

### 5. Exemplo de Estrutura para o GitHub
Você pode incluir um exemplo clássico, como o polinômio $s^3 + 3s^2 + 2s + K$:
1.  **Polinômio:** $D(s) = s^3 + 3s^2 + 2s + K$.
2.  **Tabela:**
    *   $s^3: 1 \quad 2$
    *   $s^2: 3 \quad K$
    *   $s^1: \frac{6-K}{3} \quad 0$
    *   $s^0: K$
3.  **Condição de Estabilidade:** Para não haver mudança de sinal na primeira coluna, deve-se ter $K > 0$ e $6 - K > 0$, resultando no intervalo $0 < K < 6$.

### 6. Dica de Simulação (MATLAB/Octave)
Para validar os cálculos no seu repositório, sugira o uso do comando `roots([coeficientes])` para encontrar as raízes reais ou `rlocus(sys)` para visualizar a estabilidade graficamente.

Esta estrutura fornece uma base teórica e prática completa para quem consultar seu material de estudos.


## Conteúdo
- `material/` — resumos e exercícios
- `notebooks/` — simulações
- `scripts/` — scripts MATLAB/Octave
