<h1 align="center"> Regressão: Prevendo o preço de imóveis do Rio de Janeiro </h1>
<hr>
<p>
   <img src="http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=RED&style=for-the-badge"/>
</p>

![](https://invexo.com.br/blog/wp-content/uploads/2020/08/viver-no-rio-de-janeiro-rj.jpg)

## Resumo

O projeto consistiu em tratar uma base de dados retirado do site **[zap imóveis](https://www.zapimoveis.com.br/?gclid=CjwKCAjwkMeUBhBuEiwA4hpqEJ-zRtqOKwUjCjzkYA3a1SgjxB6nhAlN_WlG9Q028cVeNAInIH_EuRoCyTgQAvD_BwE&utm_referrer=https%3A%2F%2Fwww.google.com%2F)** referente a imóveis do Rio de Janeiro, construir análises gráficas para entendimento dessa base, desenvolver e avaliar modelos de regressão capazes de prever o preço de imóveis.

Para o desenvolvimento do projeto, foi utilizado o **[pandas](https://pandas.pydata.org/)**, **[matplotlib](https://matplotlib.org/)**, **[scikit-learn](https://scikit-learn.org/)** e **[seaborn](https://seaborn.pydata.org/)**

### 🔧 Instalação das bibliotecas

Para instalar as bibliotecas utilizadas no projeto é necessário utilizar o comando **pip install** em uma célula do notebook ou no terminal (caso execute no terminal, excluir o ponto de exclamação do comando).

```
!pip install pandas
!pip install seaborn
!pip install matplotlib
!pip install scikit-learn
```

<h2>Base de dados inicial</h2>

A base de dados inicial tratada no primeiro [notebook](https://github.com/BrunoRaphaell/previsao_precos_imoveis_zap/blob/master/Projeto/1%20-%20Limpeza%20e%20tratamento%20dos%20dados/limpeza.ipynb) encontra-se disponível nesse [link](https://drive.google.com/file/d/1av_5fuOYTW95esDRypeAwo4yIBavh2CW/view?usp=sharing). Devido ao seu tamanho não foi possível realizar o upload da base de dados para o GitHub.

<h2>📓 Notebooks:</h2>

<h3><a href='https://github.com/BrunoRaphaell/previsao_precos_imoveis_zap/blob/master/Projeto/1%20-%20Limpeza%20e%20tratamento%20dos%20dados/limpeza.ipynb'>1: Limpando a base de dados</a></h3>

Esse primeiro notebook consistiu em realizar o tratamento do JSON bruto com os dados do zap imóveis. Para esse tratamento foi explorado diversos métodos da biblioteca pandas para tratamento de JSONs. Ao final do tratamento foi gerado um arquivo CSV com os dados que serão utilizados no segundo notebook. Esses dados estão disponíveis nesse [link](https://raw.githubusercontent.com/BrunoRaphaell/previsao_precos_imoveis_zap/master/dados/dados_tratados.csv).

<h4>Dicionário dos dados gerados:</h4>

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

<h3><a href='https://github.com/BrunoRaphaell/previsao_precos_imoveis_zap/blob/master/Projeto/2%20-%20Visualizando%20conjunto%20de%20dados/Visualizando%20e%20tratando%20os%20dados.ipynb'>2: Visualizando e tratando os dados</a></h3>

O segundo notebook consistiu em visualizar os dados da base de dados e tratar os dados para que fossem mais adequados para o desenvolvimento do modelo de regressão. Removeu-se os dados nulos, removeu-se a coluna `totalAreas`, pois possuía uma alta correlação com a `usableArea`, logo para evitar problemas de multicolinearidade optou-se por removê-la. Removeu-se também `latitude` e `longitude` pois a princípio não há a intenção de criar novas *features* com essas variáveis, caso seja necessário, poderá ser feito posteriormente. Após os tratamentos focou-se em construir visualizações para entender melhor os dados:

<h4>Visualizações variáveis numéricas:</h4>

* Histograma:

<center><img src="https://i.imgur.com/mtzEsMq.png"></center>

Analisando a distribuição da variável target percebemos que é uma curva assimétrica à direita. Estatisticamente temos:

$$Moda < Mediana < média$$

* Boxplot:

<center><img src="https://i.imgur.com/xFAuMH8.png"></center>

Percebe-se que o boxplot segue a mesma lógica que o histograma, porém aqui fica mais evidente a presença de amostras candidatas a outliers. 

Vamos analisar como o preço se comporta de acordo com algumas variáveis categóricas:


<center><img src="https://i.imgur.com/bmkavM3.png"></center>

<h4>Visualizações variáveis categóricas:</h4>

* Barplot: 

<center><img src="https://i.imgur.com/XzQScqW.png"></center>

Percebe-se que há muito mais imoveis de apartamentos para serem vendidos do que qualquer outro tipo. Agora vamos analisar a distribuição do preço médio de cada tipo de imóvel: 

<center><img src="https://i.imgur.com/0SUnMLO.png"></center>

Pelo gráfico acima podemos perceber que as casas com dois andares são as que apresentam um maior preço médio e o tipo que apresenta menor preço médio é o espaço para estacionamento. Provavelmente é um espaço destinado unicamente para estacionamento, ou está sendo vendido somente a vaga para estacionar, portanto faz total sentido que seja mais barato.

<center><img src="https://i.imgur.com/TLHsAXM.png"></center>
<center><img src="https://i.imgur.com/xX4I8yd.png"></center>

Pelas imagens acima percebe-se que há uma maior quantidade de imóveis da zona oeste do Rio de Janeiro, porém os imóveis mais caros estão na zona sul. O que faz total sentido pois de acordo com o artigo "[Conheça 13 bairros nobres do RJ e o que tem de mais legal em cada um](https://blog.loft.com.br/bairros-nobres-do-rj/)": 

> Não é à toa que cinco dos bairros mais caros do país estão localizados na Zona Sul carioca, sendo eles o Leblon, Ipanema, Lagoa, Gávea e Jardim Botânico.

<h4>Correlação:</h4>

<center><img src="https://i.imgur.com/VRRUM7C.png"></center>

Não há variáveis com alta correlação entre si, logo não haverá problemas de multicolinearidade.

<h4>Relação das variáveis com a variável target:</h4>

<center><img src="https://i.imgur.com/p5PZeaF.png"></center>

Após a transformação logarítmica:

<center><img src="https://i.imgur.com/GKlCLDI.png"></center>
<center><img src="https://i.imgur.com/OLCMw8m.png"></center>

Após a construção das visualizações e transformação logarítmica foi transformou-se as variáveis categóricas em dummies e salvou em um novo arquivo CSV, chamado "[dados_OneHotEncoder.csv](https://raw.githubusercontent.com/BrunoRaphaell/previsao_precos_imoveis_zap/master/dados/dados_OneHotEncoder.csv)"

<h3><a href='https://github.com/BrunoRaphaell/previsao_precos_imoveis_zap/blob/master/Projeto/3%20-%20Modelos%20de%20ML/criando%20e%20testando%20modelos%20de%20ml.ipynb'>3: criando e testando modelos de ml</a></h3>






