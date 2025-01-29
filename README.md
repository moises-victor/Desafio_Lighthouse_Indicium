# Desafio Cientista de Dados Indicium - Ferramenta de Precificação de Valor de Diárias de Imóvel

## Como instalar e executar o projeto

### Pacotes e versões utilizadas no projeto:<br>
Versão do Pandas:  2.2.2<br>
Versão do Numpy:  2.2.2<br>
Versão do Scikit-Learn:  1.5.1<br>
Versão do Python:  3.12.7 | packaged by Anaconda, Inc.<br>
Versão do Joblib:  1.4.2<br>

### Passo 1: Crie um novo Jupyter Notebook.
### Passo 2: Instale dependências com os seguintes comandos (caso não já tenha instalado:
```
!pip install pandas
!pip install joblib
```
### Passo 2: Agora os importe com os seguintes códigos:
```
import pandas as pd
import joblib
```
### Passo 4: Gere o arquivo 'Modelo_Previsao.pkl' a partir do Notebook que está neste repositório e coloque-o na mesma pasta onde o seu Jupyter Notebook está.
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
Os valores de 'id', 'host_id', 'latitude', 'longitude', 'minimo_noites', 'numero_de_reviews', 'reviews_por_mes', 'calculado_host_listings_count' e 'disponibilidade_365' devem ser em formato numérico. As demais colunas no formato de texto entre aspas ('').<br>
As informações de 'id', 'nome', 'host_id', 'host_name', 'bairro' e 'ultima_review' não são essenciais. Caso não tenha alguma delas, insira qualquer valor.
### Passo 7: Crie um dataframe a partir do dicionário com as características da propriedade com o seguinte código:
```
dados = pd.DataFrame([nova_propriedade])
```

### Passo 8: Realize a previsão com o seguinte código:
```
previsao = modelo.predict(dados)
print(f"O preço previsto para o imóvel é: ${previsao[0]:.2f}")
```
### O valor previsto será exibido na tela ッ



























