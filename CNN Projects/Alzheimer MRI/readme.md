# Alzheimer Classification with CNN

![Imagem do Cérebro](https://github.com/Henriquerezer/Machine_Learning/assets/87787728/a1a0128c-ab46-4d70-ae11-71cb685781eb)


Este repositório contém um projeto de classificação utilizando redes neurais convolucionais (CNN) para analisar imagens de ressonância magnética e identificar diferentes estágios de Alzheimer. O conjunto de dados consiste em 6400 imagens divididas em 4 classes: 'Mild_Demented', 'Moderate_Demented', 'Non_Demented' e 'Very_Mild_Demented'. A classificação é realizada atribuindo probabilidades a cada classe.

## Sobre o Alzheimer

O Alzheimer é uma doença neurodegenerativa progressiva que afeta o cérebro, causando perda de memória e habilidades cognitivas. Suas complicações incluem dificuldades na realização de tarefas diárias, confusão mental, alterações de personalidade e, eventualmente, perda total da capacidade de comunicação e funcionamento independente.

O diagnóstico precoce do Alzheimer é crucial para a implementação de intervenções terapêuticas eficazes. Um diagnóstico precoce pode permitir que os pacientes e suas famílias tomem decisões informadas sobre o tratamento e planejem para o futuro.

## Modelo Utilizado

O modelo de classificação utilizado neste projeto é uma CNN construída com a biblioteca TensorFlow/Keras. Aqui está uma breve visão do modelo:

```python
def build_model():
    # ... (arquitetura da CNN)
    return model

model = build_model()
```
## Utilizando o Modelo
Após treinar o modelo, é possível realizar previsões em novas imagens utilizando a função model.predict(). Um exemplo de como fazer isso é fornecido no final do script.

```python
# Exemplo de previsão em novas imagens
new_images = # ... (carregar novas imagens)
predictions = model.predict(new_images)
print(predictions)
```

## Clonando o Repositório e Instalando Dependências
Para utilizar este projeto, siga os passos abaixo:

1. Clone o repositório para o seu ambiente local:
   ```bash
   git clone https://github.com/Henriquerezer/Machine_Learning.git
   cd Machine_Learning
2. **Instalar bibliotecas:**
   ```bash
   pip install -r requirements.txt
   ```


Certifique-se de ter o Python e o Git instalados em seu sistema antes de prosseguir.

[Link do Dataset publicado no KAGGLE](https://www.kaggle.com/datasets/sachinkumar413/alzheimer-mri-dataset)
