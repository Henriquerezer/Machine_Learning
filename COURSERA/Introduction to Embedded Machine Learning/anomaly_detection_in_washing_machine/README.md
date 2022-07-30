Bem vindo ao meu projeto, se trata de um projeto de aprendizagem de máquina totalmente funcional.O processo incluirá a coleta de dados, a extração de recursos, o treinamento de um modelo e a implantação desse modelo em um sistema embarcado.

Será classificado os dados de movimento e vibração de uma máquina de lavar LG 7kg front load. Meu objetivo é ser capaz de identificar se a máquina está no processo de lavagem ou no processo de centrifugação e se há alguma a anomalia durante estes processos.

Neste link, você terá acesso ao projeto alocado na plataforma do Edge impulse -> https://studio.edgeimpulse.com/public/126309/latest

Neste projeto foi utilizado como sistima embarcado um smartphone, pois no momento não possuo um microcontrolador como por exemplo Arduino Nano sense BLE , para a utilização.

Neste projeto estou utilizando uma máquina de lavar roupas para a classificar e monitorar, mas podemos testar com outros equipamentos, como por exemplo:
  * Liquidificador 
  * Compressor de ar 
  * Ar condicionado
  * Ventilador de teto 

Mostrarei fotos da minha secadora de roupas para demonstrar como configurar o projeto, mas sinta-se à vontade para extrapolar para o dispositivo de sua escolha.

Lembrese, que este projeto foi desenvolvido utilizando um smartphone, então não esqueça de fazer todas as etapas com o mesmo dispositivo, desde a coleta até o teste.

Na figura 1, temos a imagem de como foi a feita a coleta dos dados.

![IMG_20220729_110541.jpg](https://usercdn.edgeimpulse.com/project126309/6db1cad3ef0c70cc1614128209f6dfd40bd88766785659d5d4f8982f9c6ae9a6)
Figura 1: Coleta dos dados.

Foi coletado ao total 5 minutos de dados, sendo que a taxa de aquicição foi de 10 segundos, destribuindo em 3 minutos de dados de centrifugação e 2 minutos de lavagem. após foi divido os dados em conjunto de teste e conjunto de treino 77% treino e 23% de teste. Como é mostrado na Figura 2.

![data acquistion.png](https://usercdn.edgeimpulse.com/project126309/c39142164838401e21d3e8b8b70b3ad843da6722207168cb4422aa59d864265a)
Figura 2: Dados coletados, gráfico a direta Raw Data de uma centrifugação.

Vá para a página de design do Impulse em seu projeto. Adicione um bloco de **processamento de Análise Espectral** . Adicione um bloco **Neural Network** e um bloco **K-means Anomaly Detection** à seção de blocos de aprendizado. Como mostrado na Figura 3.

![impulse design.png](https://usercdn.edgeimpulse.com/project126309/e678e2e589926d754391f67b975247f2d552deedb5c000fff19f7f3f00f5c30d)
Figura 3: Processo de criação do impulse.

Na Figura 4, foi exposto a criação da sprectral features, também foi exposto a importância de cada features, podemos ver que a o RMS para o eixo X e Y foram as features mais importantes para esse problema de classificação. Como podemos ver na Figura 4.

![spectral features.png](https://usercdn.edgeimpulse.com/project126309/6365570022d59ad2911fc51614cc274b7fde95515e97459396e2d68a9dc956c5)
Figura 4: Feature Explorer.

O próximo passo foi o treinamento do modelo de classificação, utilizando Keras Classifier, fou utilizado 30 épocas, um learning rate de 0,0005, havia um imput layer com 33 features, foi utilizado duas camadas densas a primeira com 20 neurônios e a segunda com 10 neurônios, foi utilziada a função de ativação softmax para a camada de saída, sendo possível a classificação de uma ou mais classes. A direta da Figura 5, também temos a matriz de confusão e uma acurácia de 99,1% e uma perda de 0,09%.
Cuidado com o overfitting! Se você perceber que a perda de validação é muito maior do que a perda de treinamento (observe cuidadosamente a saída de treinamento), seu modelo pode estar sobreajustado. Nesse caso, tente reduzir o número de nós ou camadas em seu modelo e tente novamente.
Idealmente, você deseja que sua precisão de validação esteja na faixa de 80-95%, dependendo da sua aplicação. Observe que a matriz de confusão é calculada com o conjunto de validação (não com o conjunto de treinamento).

![nn classifier.png](https://usercdn.edgeimpulse.com/project126309/ef1f63702d4109f99fa79dc5333604063a3caecdc80d9a99ae7d80a9bd46db72)
Figura 4: Training data, e métrica (Matriz de confusão)

Na figura 5, temos o treinamento do modelo de k-means para a detecção de anomalias. Selecione os recursos que você anotou na seção anterior (estes provavelmente serão os valores RMS para os eixos X, Y e Z).

![Anomaly.png](https://usercdn.edgeimpulse.com/project126309/20f12dfad3108f52c8db244ac6f8d16734f590a7caaed2dbd529b74de3d6d3bc)
Figura 5: Aprendizado não-supervisionado k-means.

Vá para a página de teste de modelo em seu projeto. Clique na caixa de seleção ao lado de Nome da amostra para selecionar todas as suas amostras de teste. Clique em Classificar . Após alguns momentos, seu conjunto de teste deve ser classificado usando o modelo que você treinou.
Observe que a acurácia nos meus dados de teste ainda ficou com um valor alto cerca de 95%, este fato pode estar relacionado há termos duas classes muito distintas, lavagem e centrigução, temos muita diferença entre os dados de vibração destas duas classes. Um possível próximo passo para este projeto, pode ser a implementação de uma nova classe, a divisão de lavagem em duas classes diferentes (como lavagem leve e lavagem pesada).
Outro passo importante seria a coleta de mais dados de ambas as classes, possuir uma base de dados grande e sólida contribuí muito na performace do modelo. 
Podemos ver na figura 6 a acurácia e a matriz de confusão.

![test data.png](https://usercdn.edgeimpulse.com/project126309/8c94daee1b4dfc52b7f1ec060762f5df44e7c1f2858b30186f05410d3a2f3caa)
Figura 6: test data.

**Conclusão**

Considerando uma acurácia de 95% na base de teste, estou muito sastisfeito com esta métrica, porém ao mesmo tempo tenho consiência que a alta acuracia pode estar relacionada a baixo número de classes e a diferença grande entre estas classes. A utilização do Edge Impulse é basntante simples após alguns testes, e é possível fazer diversas alterações nos modelos.

**Perpectivas Futuras**

Afim de melhorar o projeto, tenho a inteção de modificar as classes, incluindo um número maior e com uma menor diferença entre elas, também aumentar a quantiddade de dados adquiridos. Para facilitar a implementação do projeto na pratica, pretendo fazer a coleta dos dados e deployment dos dados, em um microcodrolador, o que tornará o projeto mais aplicável do que a utilização do smartphone.
Na figura 7, podemos ver o smatphone fazendo classificação em tempo real.

![Screenshot_2022-07-30-20-26-11-528_com.google.android.apps.photos.jpg](https://usercdn.edgeimpulse.com/project126309/147223ca5101a5a77d2fb9e4c713756b286d35d26eadc7109200cbd027642510)

Figura 7: Classificação do processo de centrifugação.
