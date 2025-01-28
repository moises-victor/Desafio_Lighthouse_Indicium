# Desafio Cientista de Dados Indicium - Ferramenta de Precificação de Valor de Diárias de Imóvel

## Como instalar e executar o projeto

### Pacotes e versões utilizadas no projeto:<br>
Versão do Pandas:  2.2.2<br>
Versão do Numpy:  2.2.2<br>
Versão do Scikit-Learn:  1.5.1<br>
Versão do Python:  3.12.7 | packaged by Anaconda, Inc.<br>
Versão do Joblib:  1.4.2<br>

### Passo 1: Crie um novo Jupyter Notebook.
### Passo 2: Instale os pacotes e dependências nas versões explicitadas acima.
### Passo 3: Importe as bibliotecas com os seguintes comandos:
```
import pandas as pd
import numpy as np
import joblib
from joblib import dump, load
import sklearn
from sklearn.ensemble import RandomForestRegressor
from sklearn.preprocessing import StandardScaler, OneHotEncoder
```
### Passo 4: Baixe o arquivo 'Modelo_Previsao.pkl' neste repositório e coloque-o na mesma pasta onde o Jupyter Notebook está.
### Passo 5: Importe o modelo de previsão com o Joblib:
```
modelo = joblib.load('Modelo_Previsao.pkl')
```
### Passo 6: Crie um dicionário com as características do imóvel que deseja prever o preço no seguinte formato:
```
nova_propriedade = {'id': 2595,
                    'nome': 'Skylit Midtown Castle',
                    'host_id': 2845,
                    'host_name': 'Jennifer',
                    'bairro_group': 'Manhattan',
                    'bairro': 'Midtown',
                    'latitude': 40.75362,
                    'longitude': -73.98377,
                    'room_type': 'Entire home/apt',
                    'minimo_noites': 1,
                    'numero_de_reviews': 45,
                    'ultima_review': '2019-05-21',
                    'reviews_por_mes': 0.38,
                    'calculado_host_listings_count': 2,
                    'disponibilidade_365': 355}
```
Os valores de 'id', 'host_id', 'latitude', 'longitude', 'minimo_noites', 'numero_de_reviews', 'reviews_por_mes', 'calculado_host_listings_count' e 'disponibilidade_365' devem ser em formato numérico. As demais colunas no formato de texto entre aspas ('')<br>
As informações de 'id', 'nome', 'host_id', 'host_name', 'bairro' e 'ultima_review' não são essenciais. Caso não tenha alguma delas, insira qualquer valor.
### Passo 7: Crie a função a seguir e execute-a inserindo como parâmetro o nome do dicionário para a nova propriedade:
```
def adequar_dados(dados):
    # Transformando em DataFrame
    nova_propriedade_df = pd.DataFrame([dados])
    
    # Removendo colunas que não foram usadas 
    nova_propriedade_df = nova_propriedade_df.drop(['id', 'nome', 'host_id', 'host_name', 'bairro', 'ultima_review'], axis=1)
    
    # Aplicando as transformações
    encoded_df = pd.DataFrame(oh_encoder.transform(nova_propriedade_df[colunas_categorias]), columns=oh_encoder.get_feature_names_out(colunas_categorias))
    
    # Anexando ao DataFrame original
    encoded_df.index = nova_propriedade_df.index
    nova_propriedade_df_cod = nova_propriedade_df.join(encoded_df)
    
    # Excluindo as colunas originais
    nova_propriedade_df_cod = nova_propriedade_df_cod.drop(colunas_categorias, axis=1)
    
    # Aplicando a padronização
    nova_propriedade_scaled = scaler.transform(nova_propriedade_df_cod)

    return nova_propriedade_scaled

dados_adequados = adequar_dados(nova_propriedade)
```

### Passo 8: Realize a previsão com o seguinte código:
```
previsao = modelo.predict(dados_adequados)

# Exibir o preço previsto
print(f"O preço previsto para o imóvel é: ${previsao[0]:.2f}")
```



























