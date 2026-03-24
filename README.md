# 📊 Efeito Dia da Semana no IBOVESPA

Análise quantitativa do efeito dia da semana no IBOVESPA, combinando testes paramétricos, não paramétricos e de permutação para investigar retornos e atividade de mercado.

---

## 📄 Relatório HTML

👉 **[Abrir relatório HTML](https://mhirokitomida.github.io/efeito_dia_semana_ibovespa/)**

---

## 🔎 Visão geral

Este projeto investiga a existência de padrões sazonais no mercado brasileiro a partir do chamado **efeito dia da semana** (*day-of-the-week effect*).

A análise foi aplicada ao **IBOVESPA**, com foco em duas dimensões:

* **Retornos diários**
* **Atividade de mercado**, medida por meio do **volume relativo de negociação**

---

## 🎯 Objetivos

* Avaliar se os **retornos** do IBOVESPA variam entre os dias da semana
* Avaliar se o **volume relativo** apresenta padrão semanal
* Aplicar diferentes abordagens estatísticas para robustez dos resultados
* Construir uma análise clara, didática e reprodutível

---

## 🧠 Metodologia

### 📊 Testes globais

* ANOVA
* Welch ANOVA
* Kruskal-Wallis
* Teste de permutação
* Teste de Levene (homogeneidade das variâncias)
* Eta² (tamanho de efeito)

### 🔍 Testes par a par

* Tukey HSD
* Dunn (Holm)
* Permutação par a par

---

## 📂 Dados utilizados

Fonte: **Yahoo Finance**

### Retorno diário

```python
df_ibovespa['retorno'] = df_ibovespa['Close'].pct_change()
```

---

### Volume relativo

O volume de negociação apresenta uma tendência estrutural de crescimento ao longo do tempo, influenciada por fatores como aumento da participação de investidores, mudanças na microestrutura de mercado e evolução da liquidez.

Para evitar que essa tendência distorça a análise, foi utilizado o **volume relativo**, definido como a razão entre o volume diário e sua média móvel de longo prazo (252 dias):

```python
df_ibovespa['vol_mm252'] = df_ibovespa['Volume'].rolling(252).mean()
df_ibovespa['vol_rel'] = df_ibovespa['Volume'] / df_ibovespa['vol_mm252']
```

Essa normalização permite:

* Tornar o volume **comparável ao longo do tempo**
* Identificar **picos e quedas de atividade** de forma relativa
* Evitar que períodos mais recentes dominem a análise

Dessa forma, o volume relativo atua como uma proxy mais adequada para a **intensidade de negociação e atividade de mercado**.

---

## 📈 Principais resultados

### Retornos

* Não apresentaram diferença estatisticamente significativa entre os dias da semana
* Resultados consistentes em todos os testes
* Tamanho de efeito praticamente nulo

---

### Atividade de mercado

* O volume relativo apresentou diferenças estatisticamente significativas
* A **segunda-feira se destacou de forma consistente**
* Evidência de um **Monday Effect na atividade**, não no retorno

---

## 🛠 Tecnologias

* Python
* pandas
* numpy
* scipy
* statsmodels
* pingouin
* scikit-posthocs
* matplotlib
* yfinance

---

## 💡 Conclusão

A análise do efeito do dia da semana sobre o comportamento do IBOVESPA revelou resultados distintos para retorno e atividade de mercado.

No que diz respeito aos retornos, não foi identificada evidência estatisticamente significativa de variação entre os dias da semana. Esse resultado se manteve consistente em todos os testes aplicados — ANOVA, Welch, Kruskal-Wallis e testes de permutação — além de não apresentar significância nas comparações par a par. O tamanho de efeito praticamente nulo reforça a conclusão de que os retornos não seguem um padrão sistemático ao longo da semana, estando alinhados com a hipótese de eficiência de mercado.

Por outro lado, o volume relativo de negociação, utilizado como proxy para a atividade de mercado, apresentou um comportamento claramente dependente do dia da semana. Todos os testes — paramétricos, não paramétricos e baseados em permutação — indicaram diferenças estatisticamente significativas. As análises par a par evidenciaram que a segunda-feira se destaca de forma consistente em relação aos demais dias, configurando um regime distinto de atividade.

Esse resultado dialoga com a literatura clássica sobre o chamado *Monday Effect* (efeito segunda-feira). Embora tradicionalmente associado a padrões anômalos de retorno — não observados neste estudo —, os resultados sugerem que o fenômeno pode se manifestar de forma mais consistente na dinâmica de negociação, refletindo mudanças na intensidade e na forma como o mercado processa informações.

Uma possível explicação para esse padrão está relacionada ao acúmulo de informações ao longo do fim de semana. Durante o período em que o mercado está fechado, eventos macroeconômicos, políticos e corporativos continuam ocorrendo, mas não são imediatamente incorporados aos preços. Assim, na abertura de segunda-feira, ocorre um processo de ajuste mais intenso, frequentemente acompanhado por picos de volume, maior dispersão e maior incerteza entre os participantes do mercado. Além disso, investidores institucionais tendem a reavaliar e rebalancear posições no início da semana, contribuindo para esse comportamento.

Cabe destacar que esse efeito não se manifesta necessariamente como um aumento na média do volume, mas sim como uma alteração na distribuição da atividade, com maior presença de eventos extremos e maior instabilidade.

De forma geral, os resultados sugerem que, embora o mercado não apresente previsibilidade direcional (retornos), ele exibe padrões estruturais na atividade de negociação ao longo da semana, o que pode ser relevante para estratégias de execução, modelagem de liquidez e gestão de risco.
