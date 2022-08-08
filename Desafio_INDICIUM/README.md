**DESAFIO INDICIUM**

Neste repositório está disposto, a análise dos dados, processmento dos dados e o modelo escolhido para a predição do salário anual.

**PERGUNTA 1**
A análise dos dados foi realizada neste link - [Análise dos dados](https://github.com/Henriquerezer/Machine_Learning/blob/main/Desafio_INDICIUM/An%C3%A1lise_dos_dados.ipynb), foi realizado histogramas das variáveis contínuas comparando as duas classes da variável alvo (**yearly_wage**), e foi possível notar que a distribuição desses dados no histograma não mostra muita diferença entre os indivíduos (<=50K e >50K). No primeiro momento foi realizada a transformação dos valores de (<=50K e >50K) para ( 1 e 0), utilizando a linha de c[odigo abaixo.
```
treino['yearly_wage'] = treino['yearly_wage'].map({' <=50K': 1, ' >50K': 0})
```
Podemos ver que nas varíaveis (**fnlwgt, capital_gain e capital_loss**) possuem outliers, como podemos ver em seus plots tanto do histograma quanto da distribuição, optei por não tratar estes outliers pois foi identifiado que estes outliers se repetem nos dados de teste, como podemos ver ao final da [Análise dos dados](https://github.com/Henriquerezer/Machine_Learning/blob/main/Desafio_INDICIUM/An%C3%A1lise_dos_dados.ipynb).

Para identificar quais variáveis poderiam ser descartadas, foi utilziado na seção "Correlação de variáveis e importância de variáveis", o modelo de RandomForestClassifier, utilizando um modelo de árvore, é possível utilizar o método que retorne a importância de cada feature, o plot com a importância de variáveis está disponível em [Análise dos dados](https://github.com/Henriquerezer/Machine_Learning/blob/main/Desafio_INDICIUM/An%C3%A1lise_dos_dados.ipynb), o que serviu como justificativa para a exclusão dos variáveis (**race** e **native_country**), com o objetivo de evitar viés de raça pelo modelo, já que o número de indíviduos brancos era bem maior, o que por si só já traria um viés para o modelo.

Por fim, No geral nossos dados de teste possuem uma distribuição bastante semelhante com os dados de treino, o que facilitará nossa classificação pelo nosso modelo. Optei pela não remoção dos outliers, pois eles permanecem nos dados de teste, como podemos ver nas variáveis (**fnlwgt, capital_gain e capital_loss**).

**PERGUNTA 2**
Para fazer previsão do salário a partir dos dados foram feitas as seguintes transformações:
```
#Definindo uma função para realizar a transformação.
def Transf(dados):
  #Remoção das variaveis que não serão utilizadas
  dados.drop('race', axis = 1, inplace = True)
  dados.drop('native_country', axis = 1, inplace = True)

  #Transformação de variáveis categóricas para numéricas
  dados['workclass']        = dados['workclass'].map({' Self-emp-not-inc' :0,  ' Private' :1, ' State-gov' :2, ' Federal-gov' :3,' Local-gov' :4, ' ?' :5, ' Self-emp-inc' :6, ' Without-pay' :7,' Never-worked' :8 })
  dados['education']        = dados['education'].map({' Bachelors' :0, ' HS-grad' :1, ' 11th' :2, ' Masters' :3, ' 9th' :4,' Some-college' :5, ' Assoc-acdm' :6, ' Assoc-voc' :7, ' 7th-8th' :8,' Doctorate' :9, ' Prof-school' :10, ' 5th-6th' :11, ' 10th' :12, ' 1st-4th' :13,' Preschool' :14, ' 12th' :15})
  dados['marital_status']   = dados['marital_status'].map({' Married-civ-spouse' :0, ' Divorced' :1, ' Married-spouse-absent' :2,' Never-married' :3, ' Separated' :4, ' Married-AF-spouse' :5, ' Widowed' :6})
  dados['occupation']       = dados['occupation'].map({' Exec-managerial' :0, ' Handlers-cleaners' :1, ' Prof-specialty' :2,' Other-service' :3, ' Adm-clerical' :4, ' Sales' :5, ' Craft-repair':6,' Transport-moving' :7, ' Farming-fishing' :8, ' Machine-op-inspct' :9, ' Tech-support' :10, ' ?' :11, ' Protective-serv' :12, ' Armed-Forces' :13, ' Priv-house-serv' :14})
  dados['relationship']     = dados['relationship'].map({' Husband' :0, ' Not-in-family' :1, ' Wife' :2, ' Own-child' :3, ' Unmarried' :4,' Other-relative' :5})
# dados['race']             = dados['race'].map({' White' :0, ' Black' :1, ' Asian-Pac-Islander' :2, ' Amer-Indian-Eskimo' :3,' Other' :4})
  dados['sex']              = dados['sex'].map({' Male' :0, ' Female' :1})
# dados['native_country']   = dados['native_country'].map({' United-States' :0, ' Cuba' :1, ' Jamaica':2, ' India' :3, ' ?' :4, ' Mexico' :5,' South' :6, ' Puerto-Rico' :7, ' Honduras' :8, ' England' :9, ' Canada' :10,' Germany' :11, ' Iran' :12, ' Philippines' :13, ' Italy' :14, ' Poland' :15,' Columbia' :16, ' Cambodia' :17, ' Thailand' :18, ' Ecuador' :19, ' Laos' :20,' Taiwan' :21, ' Haiti' :22, ' Portugal' :23, ' Dominican-Republic' :24,' El-Salvador' :25, ' France' :26, ' Guatemala' :27, ' China' :28, ' Japan' :29,' Yugoslavia' :30, ' Peru' :31, ' Outlying-US(Guam-USVI-etc)' :32, ' Scotland' :33,' Trinadad&Tobago' :34, ' Greece' :35, ' Nicaragua' :36, ' Vietnam' :37, ' Hong' :38,' Ireland' :39, ' Hungary' :40, ' Holand-Netherlands' :41})

  #normalização dos dados, mantendo os dados em uma escala de 0 a 1
  dados['fnlwgt']           = dados['fnlwgt'] / 1.48e6
  dados['education_num']    = dados['education_num'] / 16
  dados['hours_per_week']   = dados['hours_per_week'] / 99
  dados['capital_gain']     = dados['capital_gain'] / 99999
  dados['capital_loss']     = dados['capital_loss'] / 4356
  dados['age']              = dados['age'] / 90
  
  #Dummyficação das variáveis que transformamos em numéricas
  variaveis_para_Dummie     = ['workclass', 'education', 'marital_status', 'occupation', 'relationship', 'sex']
  dados = pd.get_dummies(dados, columns = variaveis_para_Dummie, drop_first = True)

  return dados
```
As variáveis categóricas (**workclass,education, marital_status, occupation, relationship, sex**) foram transformadas em variáveis numéricas utilizando o método **.map**, para a normalização das variáveis numéricas (**fnlwgt, education_num, hours_per_week, capital_gain, capital_loss, age**) as variáveis foram divididas pelos seus valores máximos, com o objetivo de normalizar os dados dentro do intervalo de 0 a 1. Por fim foi feita a dumificação das variaveis categóricas que foram transformadas em numéricas.

Estamos diante de um problema de **CLASSIFICAÇÃO** , o modelo que mais se aproximou dos dados foi o [XGBOOST](https://xgboost.readthedocs.io/en/stable/).
 * Prós 
   * Portabilidade: funciona em diversos SO.
   * Variabilidade de línguas: suporta a maioria das linguagens de programação incluindo, Julia, Scala, Java, R, Python, C++.
   * Processamento paralelo: ajuda a reduzir o tempo de treinamento.
   * Recursos integrados: permite lidar com os valores ausentes nos dados usados para treinamento e teste.
   * Ajustamento automatizado: quando os parâmetros não são ajustados corretamente.
  * Contras
    * Tempo de treinamento maior em comparação com outros modelos de reforço.
    * O XGBoost não funciona tão bem em dados esparsos e não estruturados.
    * O método geral dificilmente é escalável. Isso ocorre porque os estimadores baseiam sua correção em preditores anteriores, portanto, o procedimento envolve          muita dificuldade para simplificar.
    * O Gradient Boosting é **muito sensível** a outliers.
A medida escolhida como métrica foi a [accuracy_score](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.accuracy_score.html), pois é a métrica base para problemas de classificação, ao mesmo tempo foi exposto outras métricas como  (**precision, recall, f1-score  e support **), também foi exposto a matriz de consusão utilizando a biblioteca **yellowbrick**.

**PERGUNTA 3** 
Neste link, segue o arquivo csv com a panilha com os dados previstos com o dataset de teste. 

**PERGUNTA 4** 
É possível rodar todas as células do notebook em sequência.
 * Neste notebook temos a [Análise dos dados](https://github.com/Henriquerezer/Machine_Learning/blob/main/Desafio_INDICIUM/An%C3%A1lise_dos_dados.ipynb)
 * Neste notebok temos a [Tratamento dos dados](https://github.com/Henriquerezer/Machine_Learning/blob/main/Desafio_INDICIUM/Processamento_dos_dados.ipynb)
 * Neste notebook temos um **gridsearch** com alguns modelos de classificação o objetivo foi identificar qual o modelo com melhor acurácia, está célula,
  ```
  grids = [lr_grid_search, dt_grid_search, rf_grid_search, knn_grid_search, svm_grid_search, xgb_grid_search]
  for pipe in grids:
    pipe.fit(X_train,y_train)
  ```
  levará em torno de 1 hora para a terminar sua execução.
  * Neste último notebook está o **modelo final** utilizado e a predição dos dataset de teste, junto com a criação da planilha csv com as **predições**
