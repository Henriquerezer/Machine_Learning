Esse projeto foi desenvolvido junto a curso **Introduction to Embedded Machine Learning** da plataforma **COURSERA**, com o objetivo de me familiarizar com a plataforma Edge Impulse, utilizando Smartphone Xioami MI9T PRO para a coleta de dados de movimento, treinamento do modelo e deploy do modelo no smartphone.

Etapas 

 * Coleta dos dados -> Foi utilizado o Smartphone Xioami MI9T PRO. Criando 4 Classes de movimento 
   * Esquerda-Direita
   * Cima-Baixo
   * Circulo
   * Parado
 * Treinamento do modelo -> Foi utilizado a ferramenta Edge Impulse para o treinamento do modelo.
   * Primeiro foi criado uma modelo espectral com os dados de movimento 
   * Foi utilizado Keras Classifier com duas camadas densas ambas com ativação Relu e uma saída Softmax. (Como é mostrado na Figura 1)
   * Assim foi obtido um modelo com 4 saídas (Esquerda-dereita, Cima-baixo, Circulo, Parado)
   * Ao final Foi implementado o modelo de aprendizado não-supervisionado (k-means) para detecção de anomalias, com o objetivo de identifcar movimentos diferentes destas 4 classes definidas.
   * Com isso, ao final o modelo possuí 5 saídas, sendo uma delas para a identificação de anomalias. 

caso você queira vizualizar o modelo, baixe o arquivo (ei-my_smartphone_motion_project-nn-classifier-tensorflow-lite-int8-quantized-model.lite), e faça o upload neste link -> https://netron.app/

Você pode acessar o dashboard deste trabalho neste link -> https://studio.edgeimpulse.com/public/126066/latest
 
   
<div align="left">
<img src="https://user-images.githubusercontent.com/87787728/181561404-81d1379d-4614-4f70-973c-5d340b32373d.png" width="200px" />
</div>
Figura 1: Rede Neural com Keras Classifier.


Confome podemos ver na Figura 2, foi realizada e implementação do modelo para testes em tempo real.

<div align="left">
<img src="https://user-images.githubusercontent.com/87787728/181580285-353f3fd2-f2b6-42d6-9cc8-6b2d466cbb43.jpg" width="400px" />
</div>
Figura 2: Teste com dados em tempo real.
