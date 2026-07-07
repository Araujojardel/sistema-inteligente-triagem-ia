# Sistema Inteligente de Triagem em Pronto-Socorro

Projeto Final da disciplina de **Inteligência Artificial**.

Este projeto propõe um sistema inteligente para apoio à triagem em pronto-socorro utilizando **Redes Bayesianas** para inferência probabilística da gravidade clínica e o **algoritmo A\*** para otimizar a ordem de atendimento dos pacientes.

---

# Autores

- Francisco Wilton
- Jardel de Araújo

**Disciplina:** Inteligência Artificial

**Professor:** José Antonio Macedo

**Universidade Federal do Ceará (UFC)**

---

# Objetivo

O objetivo deste trabalho é desenvolver um sistema inteligente capaz de:

- Estimar a gravidade clínica de pacientes a partir de sintomas e sinais vitais utilizando uma **Rede Bayesiana**;
- Calcular o risco de deterioração clínica durante o tempo de espera;
- Determinar uma ordem ótima de atendimento utilizando o algoritmo **A\***;
- Comparar o desempenho da solução proposta com as estratégias **FIFO** e **Gulosa**.

---

# Tecnologias utilizadas

- Python 3
- Google Colab
- pgmpy
- NetworkX
- NumPy
- Pandas
- Matplotlib
- SciPy

---

# Arquitetura do Sistema

O sistema é composto por dois módulos integrados.

1. Inferência probabilística por Rede Bayesiana;
2. Otimização da fila utilizando o algoritmo A*.

<p align="center">
<img src="imagens/fluxo_integracao.png" width="500">
</p>

---

# Rede Bayesiana

A Rede Bayesiana representa as relações probabilísticas entre os sinais clínicos observados e a variável central **Gravidade**.

Variáveis utilizadas:

- Febre
- Saturação de Oxigênio
- Pressão Arterial
- Frequência Cardíaca
- Dor
- Idade
- Doença Crônica
- Gravidade
- Risco de Deterioração

<p align="center">
<img src="imagens/rede_bayesiana.png" width="750">
</p>

---

# Algoritmo A*

O problema foi formulado como um problema clássico de busca.

## Estado

Pacientes já atendidos.

## Estado inicial

Nenhum paciente atendido.

## Objetivo

Todos os pacientes atendidos.

## Ações

Escolher o próximo paciente da fila.

## Custo

Risco acumulado dos pacientes que permanecem aguardando atendimento.

## Heurística

Soma dos riscos atuais dos pacientes ainda presentes na fila.

---

# Integração dos módulos

A integração ocorre da seguinte maneira:

```
Paciente
      ↓
Coleta de sintomas
      ↓
Rede Bayesiana
      ↓
P(Gravidade Alta)
      ↓
Cálculo do risco
      ↓
Algoritmo A*
      ↓
Ordem ótima de atendimento
```

A probabilidade de **Gravidade Alta** produzida pela Rede Bayesiana é utilizada diretamente pelo algoritmo A* para calcular o risco acumulado de cada paciente.

---

# Experimentos

Foram avaliadas três estratégias de atendimento:

| Estratégia | Descrição |
|------------|-----------|
| FIFO | Ordem de chegada |
| Gulosa | Maior probabilidade de gravidade |
| A* | Gravidade + tempo de espera |

Foram simulados dois cenários:

- Cenário pequeno (8 pacientes)
- Cenário médio (25 pacientes)

---

## Cenário Pequeno

<p align="center">
<img src="imagens/comparacao_cenario_pequeno.png" width="600">
</p>

Resultados:

| Estratégia | Risco acumulado |
|------------|----------------:|
| FIFO | 394.25 |
| Gulosa | 186.04 |
| A* | **176.78** |

---

## Cenário Médio

<p align="center">
<img src="imagens/comparacao_cenario_medio.png" width="600">
</p>

Resultados:

| Estratégia | Risco acumulado |
|------------|----------------:|
| FIFO | 11784.04 |
| Gulosa | **4389.76** |
| A* limitado | 5006.92 |

Neste cenário foi utilizada uma versão limitada do algoritmo A*, sem garantia de otimalidade, devido ao crescimento fatorial do espaço de busca.

---

# Estrutura do Projeto

```
sistema-inteligente-triagem-ia
│
├── README.md
├── requirements.txt
├── Sistema_Inteligente_Triagem_Pronto_Socorro.ipynb
│
├── imagens
│   ├── rede_bayesiana.png
│   ├── fluxo_integracao.png
│   ├── comparacao_cenario_pequeno.png
│   ├── comparacao_cenario_medio.png
│   ├── inferencia_paciente_alto_risco.png
│   ├── paciente_exemplo.png
│   ├── pesos_cpt.png
│   ├── pipeline_sistema.png
│   ├── pseudocodigo_astar.png
│   └── expansao_estados_astar.png
│
├── relatorio
│   └── Relatório Final IA - Francisco Wilton e Jardel Araújo.pdf
│
└── docs
    └── Trabalho_Final_IA - Google Docs.pdf
```

---

# Como executar

## 1. Clone o repositório

```bash
git clone https://github.com/Araujojardel/sistema-inteligente-triagem-ia.git
```

## 2. Instale as dependências

```bash
pip install -r requirements.txt
```

## 3. Abra o notebook

```
Sistema_Inteligente_Triagem_Pronto_Socorro.ipynb
```

Execute todas as células em sequência.

---

# Referências

- Pearl, J. *Probabilistic Reasoning in Intelligent Systems*. Morgan Kaufmann, 1988.
- Russell, S.; Norvig, P. *Artificial Intelligence: A Modern Approach*. 4ª edição.
- Hart, Nilsson e Raphael. *A Formal Basis for the Heuristic Determination of Minimum Cost Paths*. 1968.
- Koller, D.; Friedman, N. *Probabilistic Graphical Models*. MIT Press, 2009.
- Manchester Triage Group. *Emergency Triage*. Wiley-Blackwell, 2014.

---

# Documentação

O relatório técnico completo encontra-se na pasta:

```
relatorio/
```

As orientações utilizadas para o desenvolvimento estão na pasta:

```
docs/
```

---

# Observações

Este projeto possui finalidade exclusivamente **acadêmica** e foi desenvolvido como trabalho final da disciplina de Inteligência Artificial.

As probabilidades utilizadas nas Tabelas de Probabilidade Condicional (CPTs) foram definidas por modelagem heurística baseada na literatura e na lógica do Protocolo de Manchester, não devendo ser interpretadas como valores calibrados para utilização clínica.

---
