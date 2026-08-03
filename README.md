# Hybrid Quant — Desafio Quant AI 2026 (Itaú Asset)

<p align="center">
  <img src="robo.png" alt="Hybrid Quant Robot" width="280"/>
</p>

O **Hybrid Quant** é uma solução de investimento quantitativo focada no mercado acionário brasileiro (B3) desenvolvida para o **Desafio Quant AI 2026 da Itaú Asset**. 

O projeto combina o poder de extração de padrões não lineares do **Deep Learning (MLP)** com a transparência e interpretabilidade matemática da **Estatística Clássica (GLM)**, executando uma estratégia *Long-Short* focada em neutralidade de mercado e geração de *Alpha*.

---

## 📌 Visão Geral da Estratégia

* **Classe de Ativos:** Ações da B3 (Ações de alta liquidez: VALE3, PETR4, ITUB4, BBDC4, B3SA3, ABEV3, WEGE3, RADL3, RENT3, BBAS3).
* **Tipo de Estratégia:** Quantitativa Multifatorial *Long-Short* (Factor Investing).
* **Frequência de Rebalanceamento:** Mensal (~21 pregões).
* **Posicionamento:** 3 Ações Compradas (*Long*) / 3 Ações Vendidas (*Short*).
* **Custos Considerados:** Fricção B3 (corretagem/emolumentos de 0,05% por perna) e Custo de Aluguel (*BTC* de 1,0% a.a. na ponta vendida).

---

## 🧠 Arquitetura do Modelo Híbrido

A decisão de investimento é dividida em duas camadas encadeadas para mitigar o problema de "caixa-preta":


```

[ Indicadores Quantitativos ]
│
▼
┌───────────────────┐
│ 1. O Analista     │ ──> Extrai padrões não-lineares e de risco
│ (MLP Neural Net)  │     Gera o 'Score de Risco'
└───────────────────┘
│
▼
┌───────────────────┐
│ 2. O Gestor       │ ──> Combina Fatores Clássicos + Score da IA
│ (GLM Gaussiano)   │     Calcula os Betas (β) e a ordem das ações
└───────────────────┘
│
▼
[ Ranking Long-Short ]

```

1. **Etapa 1 — O Analista (MLP):** Um *Multi-Layer Perceptron* raso processa fatores de *momentum*, volatilidade e *momentum* ajustado ao risco para calcular um *Score de Risco* não linear.
2. **Etapa 2 — O Gestor (GLM):** Um *Modelo Linear Generalizado* com distribuição Gaussiana pondera os fatores tradicionais ao lado do *score* do MLP. Essa etapa permite acessar diretamente os coeficientes $\beta$ e interpretar a contribuição da IA na decisão final.

---

## 📅 Divisão Temporal sem Data Leakage

Para evitar o sobreajuste (*overfitting*) e o vazamento de dados temporais (*look-ahead bias*), os dados foram rigorosamente particionados:

* **2020 – 2022 (Treino da IA):** Treinamento do MLP para aprendizado de padrões históricos.
* **2023 – 2024 (Treino do GLM):** Calibração dos coeficientes do modelo estatístico explicável usando os *scores* gerados pelo MLP.
* **2025 – 2026 (Backtest Out-of-Sample):** Simulação de operação real em período não visto pelos modelos.

---

## 📊 Desempenho e Métricas no Backtest

Métricas consolidadas na janela de teste *Out-of-Sample* (2025–2026):

| Métrica | Resultado |
| :--- | :--- |
| **Retorno Acumulado (Bruto)** | `61.40%` |
| **Índice Sharpe Anualizado** | `1.66` |
| **Max Drawdown** | `-6.51%` |
| **Taxa de Acerto (Win Rate)** | `52.9%` |

---

## 📁 Estrutura do Repositório

```bash
├── dados/                       # Diretório com bases de dados e extrações intermediárias
├── extracao_dados.ipynb         # Pipeline de extração via yfinance e engenharia de features
├── modelo.ipynb                 # Código principal (Treino MLP, Treino GLM e Backtest Long-Short)
├── robo.png                     # Identidade visual e mascote do projeto Hybrid Quant
└── README.md                    # Documentação do repositório

```

---

## 🚀 Como Executar

1. **Clone o repositório:**
```bash
git clone [https://github.com/carolinabarcellos/DesafioQuantAI2026.git](https://github.com/carolinabarcellos/DesafioQuantAI2026.git)
cd DesafioQuantAI2026

```


2. **Instale as dependências:**
```bash
pip install yfinance pandas numpy scikit-learn matplotlib

```


3. **Execute os Notebooks:**
* Execute o `extracao_dados.ipynb` para estruturar a base de dados em `dados.csv`.


* Execute o `modelo.ipynb` para rodar o pipeline do modelo híbrido e visualizar as métricas do backtest.





---

## 👥 Autores

* **Carolina Barcellos**
* **Gabrielly Xavier**
* **Matheus Soares**

```

```
