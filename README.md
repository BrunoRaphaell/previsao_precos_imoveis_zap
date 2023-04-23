
# Regressão: Prevendo o preço de imóveis do Rio de Janeiro

Rápida descrição do objetivo de fazer esse projeto

| :placard: Vitrine.Dev |     |
| -------------  | --- |
| :sparkles: Nome        | **Prevendo o preço de imóveis do Rio de Janeiro**
| :label: Tecnologias | Python, scikit-learn, Seaborn, Jupyter Notebook
| :rocket: URL         | -
| :fire: Desafio     | -

<!-- Inserir imagem com a #vitrinedev ao final do link -->
![](https://invexo.com.br/blog/wp-content/uploads/2020/08/viver-no-rio-de-janeiro-rj.jpg)

## Detalhes do projeto

<p>
   <img src="http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=RED&style=for-the-badge"/>
</p>



### 📝 Resumo

O projeto consistiu em tratar uma base de dados retirado do site **[zap imóveis](https://www.zapimoveis.com.br/?gclid=CjwKCAjwkMeUBhBuEiwA4hpqEJ-zRtqOKwUjCjzkYA3a1SgjxB6nhAlN_WlG9Q028cVeNAInIH_EuRoCyTgQAvD_BwE&utm_referrer=https%3A%2F%2Fwww.google.com%2F)** referente a imóveis do Rio de Janeiro, construir análises gráficas para entendimento dessa base, desenvolver e avaliar modelos de regressão capazes de prever o preço de imóveis.

### 💻 Organização do projeto
------------

    ├── LICENSE
    ├── Makefile           <- Makefile com comandos como `make data` ou `make train`.
    ├── README.md          <- Informações sobre o projeto.
    ├── data
    │   ├── external       <- Dados de fontes de terceiros..
    │   ├── interim        <- Dados intermediários que foram transformados.
    │   ├── processed      <- Dados finais para modelagem.
    │   └── raw            <- Dados originais, imutáveis.
    │
    ├── docs               <- Um projeto Sphinx padrão; veja sphinx-doc.org para detalhes.
    │
    ├── models             <- Modelos treinados e serializados, previsões de modelos ou resumos de modelos.
    │
    ├── notebooks          <- Notebooks Jupyter.
    │
    ├── references         <- Dicionários de dados, manuais e todos os outros materiais explicativos..
    │
    ├── reports            <- Análise gerada como HTML, PDF, LaTeX, etc.
    │   └── figures        <- Gráficos e figuras gerados para serem usados em relatórios
    │
    ├── requirements.txt   <- O arquivo de requisitos para reproduzir o ambiente de análise, por exemplo,
    │                         gerado com `pip freeze > requirements.txt`
    │
    ├── setup.py           <- Torna o projeto pip instalável (pip install -e .) para que o src possa ser importado
    ├── src                <- Código fonte para uso neste projeto.
    │   ├── __init__.py    <- Torna src um módulo Python
    │   │
    │   ├── data           <- Scripts para baixar ou gerar dados
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts para transformar dados brutos em recursos para modelagem
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts para treinar modelos e, em seguida, usar modelos treinados para fazer
    │   │   │                 predições
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts para criar visualizações exploratórias e orientadas a resultados
    │       └── visualize.py
    │
    └── tox.ini            <- arquivo tox com configurações para execução de tox; veja tox.readthedocs.io


<p><small>Projeto baseado no <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">template para data scince de cookiecutter</a>.</small></p>

--------
#### 🔧 Instalação das bibliotecas

Para o desenvolvimento do projeto, foram utilizadas bibliotecas como **[pandas](https://pandas.pydata.org/)**, **[matplotlib](https://matplotlib.org/)**, **[scikit-learn](https://scikit-learn.org/)**,  **[seaborn](https://seaborn.pydata.org/)** e **[yellowbrick](https://www.scikit-yb.org/en/latest/)**.

Para instalar das bibliotecas utilizadas no projeto é necessário utilizar o comando **pip install** em uma célula do notebook ou no terminal (caso execute no terminal, excluir o ponto de exclamação do comando).

```
!pip install pandas
!pip install seaborn
!pip install matplotlib
!pip install scikit-learn
```

<h3>Base de dados inicial</h3>

A base de dados inicial, antes de ser tratada no primeiro [notebook](https://github.com/BrunoRaphaell/previsao_precos_imoveis_zap/blob/master/notebooks/1_Limpando%20a%20base%20de%20dados.ipynb), encontra-se disponível nesse [link](https://drive.google.com/file/d/1av_5fuOYTW95esDRypeAwo4yIBavh2CW/view?usp=sharing). Devido ao seu tamanho não foi possível realizar o upload da base de dados para o GitHub.

<h3>📓 Notebooks:</h3>

<h4><a href='https://github.com/BrunoRaphaell/previsao_precos_imoveis_zap/blob/master/notebooks/1_Limpando%20a%20base%20de%20dados.ipynb'>1: Limpando a base de dados</a></h4>

Esse primeiro notebook consistiu em realizar o tratamento do JSON bruto com os dados do zap imóveis. Para esse tratamento foram explorados diversos métodos da biblioteca pandas para tratamento de JSONs. Ao final do tratamento foi gerado um arquivo CSV com os dados que serão utilizados no segundo notebook. Esses dados estão disponíveis nesse [link](https://raw.githubusercontent.com/BrunoRaphaell/previsao_precos_imoveis_zap/master/dados/dados_tratados.csv).

<h5><a href='https://github.com/BrunoRaphaell/previsao_precos_imoveis_zap/blob/master/references/dic_dados.txt'>Dicionário dos dados:</a></h5>

`usableAreas`: Área utilizável do imóvel. Área construída

`totalAreas`: Área total do imóvel. 

`bedrooms`: Quantidade de quartos.

`bathrooms`: Quantidade de banheiros.

`parkingSpaces`: Quantidade de vagas de estacionamento.

`suites`: Quantidade de suítes.

`longitude`: Longitude do imóvel.

`latitude`: Latitude do imóvel.

`yearlyIptu`: Valor do IPTU anual.

`monthlyCondoFee`: Valor da taxa condominial mensal.

`price`: Preço do imóvel. **Variável target**

<h4><a href='https://github.com/BrunoRaphaell/previsao_precos_imoveis_zap/blob/master/notebooks/2_Visualizando%20e%20tratando%20os%20dados.ipynb'>2: Visualizando e tratando os dados</a></h4>

O segundo notebook consistiu em visualizar os dados da base de dados e tratar os dados para que fossem mais adequados para o desenvolvimento do modelo de regressão.

<h5>Visualizações variáveis numéricas:</h5>

* Histograma:

<center><img src="https://i.imgur.com/oIElmvs.png"></center>

Analisando a distribuição da variável target percebemos que é uma curva assimétrica à direita. Estatisticamente temos:

$$Moda < Mediana < média$$

* Boxplot:

<center><img src="https://i.imgur.com/T8ThCdt.png"></center>

Percebe-se que o boxplot segue a mesma lógica que o histograma, porém aqui fica mais evidente a presença de amostras candidatas a outliers.,

Analisando a distribuição do preço por zona:

<center><img src="https://i.imgur.com/sxXFqtA.png"></center>

Analisando a distribuição dos preços dos imóveis por tipo do imóvel:

<center><img src="https://i.imgur.com/mKpJXTw.png"></center>

<h4>Visualizações variáveis categóricas:</h4>

* Barplot: 

<center><img src="https://i.imgur.com/QVdt79D.png"></center>

Percebe-se que há muito mais imóveis de apartamentos para serem vendidos do que qualquer outro tipo. Analisando o preço médio por tipo do imóvel: 

<center><img src="https://i.imgur.com/JP5TOVy.png"></center>

Quantidade de imóveis por zona:

<center><img src="https://i.imgur.com/YkLTwWZ.png"></center>

Preço médio por zona do imóvel:

<center><img src="https://i.imgur.com/9yGKEOr.png"></center>

Pelas imagens acima percebe-se que há uma maior quantidade de imóveis da zona oeste do Rio de Janeiro, porém os imóveis mais caros estão na zona sul. O que faz total sentido pois de acordo com o artigo "[Conheça 13 bairros nobres do RJ e o que tem de mais legal em cada um](https://blog.loft.com.br/bairros-nobres-do-rj/)": 

> Não é à toa que cinco dos bairros mais caros do país estão localizados na Zona Sul carioca, sendo eles o Leblon, Ipanema, Lagoa, Gávea e Jardim Botânico.

<h5>Correlação:</h5>

<center><img src="https://i.imgur.com/mqdnxUs.png"></center>

Não há variáveis com alta correlação entre si, logo não haverá problemas de multicolinearidade.

<h5>Relação das variáveis com a variável target:</h5>

<center><img src="https://i.imgur.com/p5PZeaF.png"></center>

Após a transformação logarítmica:

<center><img src="https://i.imgur.com/GKlCLDI.png"></center>
<center><img src="https://i.imgur.com/1nAXqYj.png"></center>

Após a construção das visualizações e transformação logarítmica foi transformou-se as variáveis categóricas em dummies e salvou em um novo arquivo CSV, chamado "[dados_OneHotEncoder.csv](https://raw.githubusercontent.com/BrunoRaphaell/previsao_precos_imoveis_zap/master/data/processed/dados_OneHotEncoder.csv)"

<h4><a href='https://github.com/BrunoRaphaell/previsao_precos_imoveis_zap/blob/master/notebooks/3_criando%20e%20testando%20modelos%20de%20ml.ipynb'>3: criando e testando modelos de ml</a></h5>

O terceiro notebook consistiu em criar e testar os modelos de regressão. Foram escolhidos os seguintes modelos:

* [Linear Regression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)
* [DecisionTreeRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeRegressor.html)
* [RandomForestRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html)
* [GradientBoostingRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html)

A primeira parte consistiu em testar os modelos e escolher o que apresentasse melhor desempenho com as métricas `MSE`, `RMSE`, `MAE` e `R2` e então realizar o tunning dos hiperparâmetros e obter um modelo ainda melhor. Abaixo está um resumo dos resultados obtidos:

![](https://i.imgur.com/Kmqv7Dp.png)

O modelo escolhido foi [GradientBoostingRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html) e para realizar o tunning dos hyperparametros foi utilizado o [GridSearchCV](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html) e os melhores parâmetros foram obtendo um `mean_test_score` de 0.902027:

```
{'learning_rate': 0.1,
 'max_depth': 8,
 'min_samples_split': 4,
 'n_estimators': 200}
```

<h3>💭 Continuação com mlflow</h3>

Para continuar com o desenvolvimento do projeto, foi utilizado o [mlflow](https://mlflow.org/), que está disponível nesse outro repositório "[mlflow_previsao_precos_imoveis_zap](https://github.com/BrunoRaphaell/mlflow_previsao_precos_imoveis_zap)". 

<h3>🧑🏼 Autor</h3>

[<img src="https://avatars.githubusercontent.com/u/24321228?v=4" width=115><br><sub>Bruno Raphaell</sub>](https://www.linkedin.com/in/bruno-raphaell-alves-de-matos/) 


