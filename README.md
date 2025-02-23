# Análise de segmentação de clientes - Power BI

## Visão Geral
Este relatório analisa os grupos da segmentação dos clientes a partir de um arquivo csv e a clusterização dentro do Power BI.

![Relatório Power BI](Segmentacao_clientes_pontuacao.png)

## Construção
O relatório foi gerado a partir do arquivo csv com o id do cliente, idade, renda anual e pontuacao_gastos. Em seguida, foi realizada a padroniazação e clusterização dos dados via Power Query com o código: 

```python
# 'dataset' tem os dados de entrada para este script
import pandas as pd
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

# padronização dos dados de idade, renda anual e pontuacao_gastos
padronizador = StandardScaler()
dados_padronizados = padronizador.fit_transform(df[['idade', 'renda_anual', 'pontuacao_gastos']])

# Definir o número de clusters e criar o modelo
kmeans = KMeans(n_clusters=3, random_state=42)
kmeans.fit(dados_padronizados)
df['Cluster'] = kmeans.labels_

# Retornar os dados com o cluster
output = df
```

## Principais Insights  
- As vendas cresceram 15% no último trimestre.  
- A região Sul teve a maior taxa de crescimento.  
- O produto X apresentou queda nas vendas, necessitando ajustes na estratégia.  
