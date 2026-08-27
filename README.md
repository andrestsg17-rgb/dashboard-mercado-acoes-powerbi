# 📈 Mini Projeto — Mercado de Ações (Power BI)

Dashboard interativo desenvolvido no **Power BI**, como parte de um curso, para análise do comportamento de ações de cinco grandes empresas listadas na bolsa: **IBM, Microsoft, Tesla, Oracle e Walmart**, no período de **fevereiro/2022 a fevereiro/2023**.

> 💡 Projeto de estudo focado em modelagem de dados, DAX e storytelling visual.

---

## 🖼️ Preview do Dashboard

<!-- c:\Users\André\Desktop\Dashboard-mercado-acoes.png -->

---

## 🎯 Sobre o Projeto

O objetivo foi construir um painel único, capaz de mostrar rapidamente:
- A evolução do volume de ações negociadas ao longo do tempo;
- A variação percentual do preço médio de fechamento mês a mês (MoM%);
- Um resumo tabular dos valores médios mensais por empresa;
- Uma narrativa textual dinâmica com os principais destaques do período.

## 🧩 Estrutura do Dashboard

O relatório contém **1 página** ("Dashboard") com os seguintes elementos visuais:

| Visual | Tipo | Descrição |
|---|---|---|
| Total do Volume Negociado ao Longo do Tempo | Gráfico de Área | Evolução do volume negociado por Ano/Trimestre/Mês/Dia |
| Variação da Média de Fechamento MoM | Gráfico de Área Empilhada | Variação percentual mês a mês do preço médio de fechamento |
| Tabela de Valores Médios Por Mês | Tabela | Resumo mensal com Open, High, Low, Close |
| Narrativa Inteligente | Textbox | Texto dinâmico com destaques do período |
| Slicers | Segmentação de dados (x2) | Filtros de Empresa e Data |

## 🧮 Modelo de Dados

**Tabela principal:** `StockMarket`

| Coluna | Tipo | Descrição |
|---|---|---|
| Empresa | Texto | Nome da empresa (IBM, Microsoft, Tesla, Oracle, Walmart) |
| Data | Data | Data do pregão |
| Open | Decimal | Preço de abertura |
| High | Decimal | Preço máximo do dia |
| Low | Decimal | Preço mínimo do dia |
| Close | Decimal | Preço de fechamento |
| Volume | Inteiro | Volume negociado |

### Medida DAX customizada

```dax
Média de Close MoM% =
IF(
    ISFILTERED('StockMarket'[Data]),
    ERROR("Medidas rápidas de inteligência de tempo somente podem ser agrupadas ou filtradas pela hierarquia de data fornecida pelo Power BI ou pela coluna de data primária."),
    VAR __PREV_MONTH =
        CALCULATE(
            AVERAGE('StockMarket'[Close]),
            DATEADD('StockMarket'[Data].[Date], -1, MONTH)
        )
    RETURN
        DIVIDE(AVERAGE('StockMarket'[Close]) - __PREV_MONTH, __PREV_MONTH)
)
```

## 🔎 Principais Insights

Análise do período completo (23/02/2022 a 23/02/2023):

| Empresa | Fechamento Inicial | Fechamento Final | Variação | Preço Médio | Máxima | Mínima |
|---|---:|---:|---:|---:|---:|---:|
| **Tesla** | $254,68 | $202,07 | 🔻 -20,66% | $240,82 | $381,82 | $108,10 |
| **Microsoft** | $280,27 | $254,77 | 🔻 -9,10% | $260,91 | $315,41 | $214,25 |
| **Oracle** | $72,47 | $88,58 | 🟢 +22,23% | $76,58 | $90,05 | $61,07 |
| **IBM** | $122,07 | $130,79 | 🟢 +7,14% | $134,37 | $150,57 | $117,57 |
| **Walmart** | $135,05 | $142,09 | 🟢 +5,21% | $138,75 | $159,87 | $118,29 |

- 🚨 **Tesla** foi a ação mais volátil do período — teve a maior alta (chegando a $381,82) e também a maior queda percentual acumulada (-20,66%), além do volume médio negociado disparadamente maior que as demais (~103M de ações/dia, contra uma média de ~7-8M nas outras).
- 📉 Das 5 empresas, **Tesla e Microsoft** fecharam o período em queda, refletindo o cenário de correção das techs em 2022.
- 📈 **Oracle** teve a melhor performance relativa (+22,23%), com a menor volatilidade entre as máximas e mínimas.
- 💧 **Walmart** foi a ação mais "estável", com menor amplitude entre preço máximo e mínimo em relação ao seu próprio preço médio — perfil defensivo, condizente com o setor de varejo.

## 🛠️ Tecnologias

- Power BI Desktop
- DAX (Data Analysis Expressions)
- Modelagem de dados (Star Schema simplificado)

## 📁 Estrutura sugerida do repositório


## 👤 Autor

Projeto desenvolvido durante curso de Power BI — [André Araujo].
