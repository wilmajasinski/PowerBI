# Análise de segmentação de clientes - Power BI

## Visão Geral
Este relatório analisa os grupos da segmentação dos clientes a partir de um arquivo csv e a clusterização dentro do Power BI. A base foi obtida através do [curso gratuito de Power BI da Data Science Academy](https://www.datascienceacademy.com.br/course/microsoft-power-bi-para-business-intelligence-e-data-science), porém foi utilizada uma abordagem de segmentação dentro do Power BI ao invés do Jupyter Notebook. 


## Construção
O relatório foi gerado a partir do arquivo csv com o id do cliente, idade, renda anual e pontuacao_gastos. Em seguida, foi realizada a padronização e clusterização dos dados via Power Query com o código: 

```python
# Importação das bibliotecas
import pandas as pd
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

# Padronização dos dados de idade, renda anual e pontuacao_gastos
padronizador = StandardScaler()
dados_padronizados = padronizador.fit_transform(df[['idade', 'renda_anual', 'pontuacao_gastos']])

# Definição do número de clusters e criação do modelo
kmeans = KMeans(n_clusters=3, random_state=42)
kmeans.fit(dados_padronizados)
df['Cluster'] = kmeans.labels_

# Retornar os dados com o cluster
output = df
```

## Tela com a análise e médias de cada cluster
![Segmentacao_clientes_pontuacao](https://github.com/user-attachments/assets/1230cb40-d78c-4026-90de-49a2c3e2a1dc)


## Principais Insights  
- O cluster A é formado por clientes com maior pontuação de gastos, mas que possuem menor renda anual. Seria o caso de um maior engajamento na pontuação de gastos?
- O cluster B tem mais que o dobro da renda anual média do cluster A e uma média de pontuação de gastos bastante próxima (16% menor). Inversamente à conclusão do cluster A, seria o caso do cluster B ser menos engajado na pontuação de gastos.  
- Tanto os clientes do grupo A, quanto o grupo B, possuem uma idade média parecida, 53 anos no A e 54 anos no B. 
- O cluster C, destaca-se pela idade média dos clientes (27 anos).
