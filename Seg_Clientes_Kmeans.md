# Análise de segmentação de clientes - Power BI

## Visão Geral
Este relatório analisa os grupos da segmentação dos clientes a partir de um arquivo csv e a clusterização dentro do Power BI. A base foi obtida através do [curso gratuito de Power BI da Data Science Academy](https://www.datascienceacademy.com.br/course/microsoft-power-bi-para-business-intelligence-e-data-science), porém foi utilizada uma abordagem de segmentação dentro do Power BI ao invés do Jupyter Notebook. 

A tabela possui as variáveis: 
- Id do cliente
- Idade
- Renda anual
- Pontuação de gastos 

## Análise exploratória

A seguir, o resumo estatístico do arquivo: 

| Estatística | Idade  | Renda Anual  | Pontuação de Gastos |
|------------|--------|-------------|---------------------|
| **Count**  | 500    | 500         | 500                 |
| **Mean**   | 44,732 | 81.557,166  | 48,512              |
| **Std**    | 15,240 | 36.764,380  | 29,557              |
| **Min**    | 18     | 20.384      | 0                   |
| **25%**    | 32     | 49.172,750  | 24                  |
| **50%**    | 45     | 79.219      | 48,5                |
| **75%**    | 57     | 113.017,250 | 73,25               |
| **Max**    | 70     | 149.695     | 100                 |



## Processamento dos dados
O processamento dos dados foi realizado via Power Query. Abaixo, o código em Python. 

```python
# Importação das bibliotecas
import pandas as pd
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

# Padronização dos dados de idade, renda anual e pontuacao_gastos
padronizador = StandardScaler()
dados_padronizados = padronizador.fit_transform(df[['idade', 'renda_anual', 'pontuacao_gastos']])

# Definição do número de clusters e criação do modelo
kmeans = KMeans(n_clusters = 3)
kmeans.fit(dados_padronizados)
df['Cluster'] = kmeans.labels_

# Retornar os dados com o cluster
output = df
```

## Criação da tela no Power BI com a análise das médias de cada cluster e variável
![Segmentacao_clientes_pontuacao](https://github.com/user-attachments/assets/1230cb40-d78c-4026-90de-49a2c3e2a1dc)


## Principais Insights  
- O cluster A é formado por clientes com maior pontuação de gastos, mas que possuem menor renda anual.
- O cluster B tem mais que o dobro da renda anual média do cluster A e uma média de pontuação de gastos bastante próxima (16% menor). Inversamente à conclusão do cluster A, seria o caso do cluster B ser menos engajado na pontuação de gastos.  
- Tanto os clientes do grupo A, quanto o grupo B, possuem uma idade média parecida, 53 anos no A e 54 anos no B.  
- O cluster C, destaca-se pela idade média dos clientes (27 anos).
- Seria importante avaliar outras variáveis além da renda anual, como uma estimativa de custo de vida de cada cliente. Dessa forma, seria possível investigar as discrepâncias dos grupos A e B, como um custo de vida mais baixo (grupo A) ou uma propensão ao endividamento (grupo B), bem como entender o foco das campanhas de marketing. 


