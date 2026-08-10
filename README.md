# Sistemas de Controle I

Repositório de apoio à disciplina **Sistemas de Controle I**, com material, exercícios, notebooks e scripts (MATLAB/GNU Octave) organizados por tópico do plano de ensino.

## Objetivos gerais

A disciplina tem o objetivo de introduzir ao discente a análise e projeto de controladores lineares de sistemas modelados através de funções de transferência. O aluno deve ser capaz de compreender e simular, utilizando o software Matlab/GNU Octave, os conceitos clássicos envolvidos no projeto de controladores para sistemas lineares e invariantes no tempo.

## Objetivos específicos

- Definir os problemas e apresentar soluções para projetos de sistemas de controle automático.
- Detalhar as possíveis representações matemáticas e propriedades de sistemas de controle lineares e invariantes no tempo.
- Discutir o conceito de estabilidade e apresentar a metodologia de projeto de controladores, baseada no diagrama do lugar das raízes.
- Introduzir o software Matlab/GNU Octave, abordando algumas funcionalidades para simular sistemas de controle clássico.

## Ementa

Análise de resposta transitória e de regime estacionário: sistemas de primeira e de segunda ordens; critério de estabilidade de Routh; efeitos das ações de controle integral e derivativo; erros estacionários em sistemas de controle com realimentação unitária; análise do lugar das raízes: gráfico do lugar das raízes, regras gerais para a construção do lugar das raízes, lugar das raízes para sistemas com retardo de transporte; projeto de sistemas de controle pelo método do lugar das raízes: compensação por avanço de fase, compensação por atraso de fase, compensação por avanço e atraso de fase.

## Plano de ensino

| # | Tópico |
|---|--------|
| 01 | Análise de resposta transitória e de regime estacionário: sistemas de 1ª ordem (funções de transferência) |
| 02 | Análise de resposta transitória e de regime estacionário: sistemas de 2ª ordem (funções de transferência) |
| 03 | Análise de estabilidade: critério de Routh-Hurwitz |
| 04 | Efeitos das ações de controle integral e derivativo; erros estacionários em sistemas de controle com realimentação unitária |
| 05 | Análise no lugar das raízes ("root locus"): gráfico do lugar das raízes, sistema com retardo de transporte |
| 06 | Projeto de sistemas de controle pelo método do lugar das raízes: compensação por avanço de fase, por atraso de fase, e por avanço e atraso de fase |

## Estrutura do repositório

```
sistemas-controle-1/
├── 01-resposta-transitoria-1a-ordem/
├── 02-resposta-transitoria-2a-ordem/
├── 03-estabilidade-routh-hurwitz/
├── 04-acoes-controle-erros-estacionarios/
├── 05-lugar-das-raizes/
├── 06-projeto-compensadores/
```

Cada módulo contém:

- `material/` — anotações, resumos teóricos e enunciados de exercícios;
- `notebooks/` — Jupyter/Octave notebooks com simulações;
- `scripts/` — scripts `.m` (MATLAB/GNU Octave) de apoio.

## Ferramentas

- [MATLAB](https://www.mathworks.com/products/matlab.html) ou [GNU Octave](https://octave.org/) (alternativa gratuita e compatível)

## Bibliografia

- K. OGATA. *Engenharia de Controle Moderno*. Pearson, 5ª ed., 2010.
- R. C. DORF; R. H. BISHOP. *Sistema de Controle Moderno*. LTC, 13ª ed., 2018.
- G. F. FRANKLIN; J. D. POWELL; A. EMAMI-NAINI. *Sistema de Controle para Engenharia*. Bookman, 6ª ed., 2013.

## Licença

Este material é disponibilizado para fins educacionais sob a licença MIT (ver `LICENSE`).
