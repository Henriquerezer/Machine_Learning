# Projeto de Classificação de Tumores Cerebrais usando Convolutional Neural Network (CNN)

![Imagem do Cérebro](https://github.com/Henriquerezer/Machine_Learning/assets/87787728/3c87117d-cb94-4b32-b7c2-7b317030df84)

Este projeto prático foi desenvolvido como parte do Curso Profissional DeepLearning.AI TensorFlow Developer, com o objetivo de aplicar os conhecimentos adquiridos na construção e treinamento de Convolutional Neural Networks (CNNs). A aplicação específica aqui é a classificação de imagens de ressonância magnética do crânio para diagnosticar diferentes tipos de tumores cerebrais.

## Objetivo
O objetivo principal é criar um modelo de machine learning capaz de classificar imagens de ressonância magnética em quatro categorias:
1. **glioma_tumor**
2. **meningioma_tumor**
3. **pituitary_tumor**
4. **no_tumor** (rótulo para imagens sem tumor)

## Aprendizado por Transferência
Devido à limitação do dataset em termos de quantidade de amostras, foi aplicada a técnica de aprendizado por transferência. O modelo baseado em uma arquitetura de CNN pré-treinada foi utilizado, e apenas a camada de saída foi modificada para atender às classes específicas do projeto.

## Principais Características dos Tumores
- **glioma_tumor**: [Referêncial Teórico](https://www.hopkinsmedicine.org/international/portugues/conditions-treatments/neurosurgery/gliomas.html)
- **meningioma_tumor**: [Referêncial Teórico](https://www.msdmanuals.com/pt-br/profissional/dist%C3%BArbios-neurol%C3%B3gicos/tumores-intracranianos-e-espinhais/meningiomas#:~:text=Os%20meningiomas%20s%C3%A3o%20tumores%20das,e%2C%20%C3%A0s%20vezes%2C%20radioterapia.)
- **pituitary_tumor**: [Referêncial Teórico](https://www.hopkinsmedicine.org/health/conditions-and-diseases/pituitary-tumors)
- **no_tumor**:

## Métricas de Desempenho
Após a conclusão do treinamento, diversas métricas foram avaliadas para avaliar o desempenho do modelo, incluindo, mas não se limitando a, precisão, recall e F1-score para cada classe.

## Teste com Imagem
O projeto inclui um teste prático com uma imagem de ressonância magnética, onde é realizada uma predição da classe correspondente. O resultado é então visualizado para verificar a eficácia do modelo.

## Como Utilizar
Para reproduzir ou estender este projeto, siga as instruções abaixo:

1. **Clone o Repositório:**
   ```bash
   git clone https://github.com/Henriquerezer/Machine_Learning.git
   cd Machine_Learning

2. **Instalar bibliotecas:**
   ```bash
   pip install -r requirements.txt
