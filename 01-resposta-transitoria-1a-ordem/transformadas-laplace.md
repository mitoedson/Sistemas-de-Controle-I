# Transformada de Laplace: fundamentos e conversão de EDOs

Material de referência sobre a Transformada de Laplace, com foco no seu uso como ferramenta para converter equações diferenciais ordinárias (EDOs) em equações algébricas — a base de toda a análise por funções de transferência usada neste repositório.

## 1. Definição

A Transformada de Laplace de uma função $f(t)$, definida para $t \geq 0$, é dada por:

$$F(s) = \mathcal{L}\{f(t)\} = \int_0^{\infty} f(t)\,e^{-st}\,dt$$

onde $s = \sigma + j\omega$ é uma variável complexa. O operador converte uma função do domínio do tempo (variável real $t$) em uma função no domínio da frequência complexa (variável $s$).

A transformada inversa, que retorna do domínio $s$ para o domínio do tempo, é indicada por:

$$f(t) = \mathcal{L}^{-1}\{F(s)\}$$

**Condição de existência:** a integral converge quando $f(t)$ é contínua por partes em qualquer intervalo finito e é de *ordem exponencial* — ou seja, existe $\sigma_c$ tal que $e^{-\sigma t}|f(t)| \to 0$ quando $t \to \infty$, para $\sigma > \sigma_c$. Praticamente todos os sinais de interesse em engenharia de controle (degraus, exponenciais, senoides, polinômios) satisfazem essa condição.

## 2. Por que a Laplace converte EDO em álgebra

O motivo prático de usarmos Laplace em sistemas de controle está nas propriedades da transformada da derivada. Para $f(t)$ contínua, com $f(0)$ conhecido:

$$\mathcal{L}\{\dot f(t)\} = sF(s) - f(0)$$

$$\mathcal{L}\{\ddot f(t)\} = s^2F(s) - sf(0) - \dot f(0)$$

De forma geral, para a $n$-ésima derivada:

$$\mathcal{L}\left\{\frac{d^n f(t)}{dt^n}\right\} = s^nF(s) - s^{n-1}f(0) - s^{n-2}\dot f(0) - \dots - f^{(n-1)}(0)$$

**O ponto-chave:** cada derivada no tempo vira uma multiplicação por $s$ (mais um termo de condição inicial) no domínio de Laplace. Isso significa que uma EDO — que envolve operações de cálculo (derivadas) — se transforma em uma equação **puramente algébrica** em $s$, envolvendo apenas somas, produtos e potências de $s$. É essa troca de "cálculo" por "álgebra" que permite:

- Resolver o sistema sem integrar ou derivar diretamente;
- Representar o sistema por uma função de transferência $G(s) = Y(s)/U(s)$;
- Aplicar álgebra de blocos (série, paralelo, realimentação) de forma direta.

## 3. Procedimento geral para converter uma EDO

Dada uma EDO linear de coeficientes constantes, o procedimento padrão é:

1. **Aplicar $\mathcal{L}\{\cdot\}$ em ambos os lados** da equação, termo a termo (usa-se a linearidade: $\mathcal{L}\{af+bg\} = aF(s)+bG(s)$).
2. **Substituir cada derivada** pela sua transformada, introduzindo as condições iniciais correspondentes.
3. **Isolar $Y(s)$** (ou a variável de interesse), agrupando os termos algebricamente.
4. **Obter $y(t)$** aplicando a transformada inversa $\mathcal{L}^{-1}\{Y(s)\}$ — normalmente via decomposição em frações parciais e consulta à tabela de pares de transformadas.

### Exemplo — EDO livre de 1ª ordem

Para $\dot x(t) = \alpha x(t)$, $x(0) = x_0$:

$$sX(s) - x_0 = \alpha X(s) \;\Longrightarrow\; X(s) = \frac{x_0}{s-\alpha} \;\Longrightarrow\; x(t) = x_0e^{\alpha t}$$

(esse caso está detalhado no `README.md` do módulo 01, junto com a resolução alternativa por separação de variáveis.)

### Exemplo — EDO de 2ª ordem

Para $\ddot y(t) + 3\dot y(t) + 2y(t) = 0$, com $y(0)=1$, $\dot y(0)=0$:

$$\big[s^2Y(s) - sy(0) - \dot y(0)\big] + 3\big[sY(s)-y(0)\big] + 2Y(s) = 0$$

$$Y(s)(s^2+3s+2) - s - 3 = 0 \;\Longrightarrow\; Y(s) = \frac{s+3}{s^2+3s+2} = \frac{s+3}{(s+1)(s+2)}$$

Decompondo em frações parciais e usando a tabela abaixo, obtém-se $y(t)$ como soma de exponenciais $e^{-t}$ e $e^{-2t}$.

## 4. Tabela de pares de transformadas (funções mais usadas)

| # | $f(t)$, $t \geq 0$ | $F(s) = \mathcal{L}\{f(t)\}$ |
|---|---|---|
| 1 | $\delta(t)$ (impulso unitário) | $1$ |
| 2 | $1(t)$ (degrau unitário) | $\dfrac{1}{s}$ |
| 3 | $t$ (rampa unitária) | $\dfrac{1}{s^2}$ |
| 4 | $t^n$, $n=1,2,\dots$ | $\dfrac{n!}{s^{n+1}}$ |
| 5 | $e^{-at}$ | $\dfrac{1}{s+a}$ |
| 6 | $t\,e^{-at}$ | $\dfrac{1}{(s+a)^2}$ |
| 7 | $t^n e^{-at}$ | $\dfrac{n!}{(s+a)^{n+1}}$ |
| 8 | $\sin(\omega t)$ | $\dfrac{\omega}{s^2+\omega^2}$ |
| 9 | $\cos(\omega t)$ | $\dfrac{s}{s^2+\omega^2}$ |
| 10 | $e^{-at}\sin(\omega t)$ | $\dfrac{\omega}{(s+a)^2+\omega^2}$ |
| 11 | $e^{-at}\cos(\omega t)$ | $\dfrac{s+a}{(s+a)^2+\omega^2}$ |
| 12 | $\sinh(bt)$ | $\dfrac{b}{s^2-b^2}$ |
| 13 | $\cosh(bt)$ | $\dfrac{s}{s^2-b^2}$ |
| 14 | $u(t-c)$ (degrau deslocado) | $\dfrac{e^{-cs}}{s}$ |
| 15 | $\delta(t-c)$ (impulso deslocado) | $e^{-cs}$ |
| 16 | $u(t-c)\,f(t-c)$ | $e^{-cs}F(s)$ |

## 5. Propriedades operacionais

| Propriedade | Domínio do tempo | Domínio de $s$ |
|---|---|---|
| Linearidade | $af_1(t) + bf_2(t)$ | $aF_1(s) + bF_2(s)$ |
| Derivada 1ª ordem | $\dot f(t)$ | $sF(s) - f(0)$ |
| Derivada 2ª ordem | $\ddot f(t)$ | $s^2F(s) - sf(0) - \dot f(0)$ |
| Derivada $n$-ésima | $f^{(n)}(t)$ | $s^nF(s) - \sum_{k=0}^{n-1} s^{n-1-k}f^{(k)}(0)$ |
| Integral | $\displaystyle\int_0^t f(\tau)\,d\tau$ | $\dfrac{F(s)}{s}$ |
| Deslocamento em $s$ | $e^{-at}f(t)$ | $F(s+a)$ |
| Deslocamento no tempo | $f(t-c)\,u(t-c)$, $c\geq0$ | $e^{-cs}F(s)$ |
| Mudança de escala | $f(t/a)$ | $aF(as)$ |
| Multiplicação por $t$ | $t\,f(t)$ | $-\dfrac{dF(s)}{ds}$ |
| Convolução | $f_1(t) * f_2(t)$ | $F_1(s)\,F_2(s)$ |
| Teorema do valor inicial | — | $f(0^+) = \displaystyle\lim_{s\to\infty} sF(s)$ |
| Teorema do valor final | — | $f(\infty) = \displaystyle\lim_{s\to 0} sF(s)$ |

> **Nota sobre o teorema do valor final:** só é válido se todos os polos de $sF(s)$ estiverem no semiplano esquerdo aberto (sistema estável) — é essa propriedade que conecta diretamente Laplace à análise de regime estacionário feita no módulo 01 e ao critério de Routh-Hurwitz do módulo 03.

## 6. Do domínio de $s$ de volta ao tempo: frações parciais

Como a maioria das funções de transferência de interesse em controle são racionais (razão de polinômios em $s$), a transformada inversa é obtida, na prática, por **decomposição em frações parciais**: reescreve-se $Y(s)$ como soma de termos simples (do tipo $\frac{A}{s+p}$, $\frac{As+B}{(s+p)^2+\omega^2}$, etc.), cada um correspondendo a uma linha da tabela do item 4. É esse processo que fecha o ciclo:

$$\text{EDO} \;\xrightarrow{\mathcal{L}}\; \text{equação algébrica em } s \;\xrightarrow{\text{álgebra}}\; Y(s) \;\xrightarrow{\text{frações parciais} + \mathcal{L}^{-1}}\; y(t)$$

## Referências

- K. Ogata, *Engenharia de Controle Moderno*, Pearson, 5ª ed., 2010.
- R. C. Dorf e R. H. Bishop, *Sistema de Controle Moderno*, LTC, 13ª ed., 2018.
- G. F. Franklin, J. D. Powell e A. Emami-Naini, *Sistema de Controle para Engenharia*, Bookman, 6ª ed., 2013.