## Classificação de Notícias e Autocomplete de Texto 📰

![Static Badge](https://img.shields.io/badge/Status-Finalizado-green)

## Descrição

Este projeto visa construir dois modelos de Machine Learning: um para classificar notícias em diferentes categorias e outro para realizar o autocomplete de texto, prevendo a próxima palavra em uma frase. O conjunto de dados fornecido consiste em notícias de um site de notícias, já pré-processadas e armazenadas em um arquivo CSV.

## Tecnologias Utilizadas

- Python
- Pandas
- Scikit-learn
- TensorFlow
- Keras

## Dicionário de Dados

O arquivo CSV de dados contém as seguintes colunas:

| Coluna        | Descrição                                      | Tipo de Dado |
|---------------|-------------------------------------------------|--------------|
| ClassIndex    | Índice da categoria da notícia (0-3)            | Numérico     |
| Título        | Título da notícia                               | Texto        |
| Descrição     | Descrição da notícia                            | Texto        |
| Texto         | Título e descrição concatenados, separados por espaço | Texto        |

## Descrição Detalhada do Projeto

### Classificação de Notícias

- **Pré-processamento:**
    - O campo `ClassIndex` foi ajustado para que os valores variem de 0 a 3, em vez de 1 a 4, para compatibilidade com o TensorFlow.
    - Uma nova coluna `Texto` foi criada, combinando o título e a descrição da notícia.
- **Separação de Dados:**
    - Os dados foram divididos em conjuntos de treino e teste usando `train_test_split` da biblioteca Scikit-learn, com uma proporção de 80% para treino e 20% para teste.
- **Tokenização:**
    - A coluna `Texto` foi tokenizada usando `TextVectorization` do Keras, com um vocabulário de tamanho `VOCAB_SIZE`.
- **Modelagem:**
    - Diversas arquiteturas de modelos de classificação foram experimentadas, incluindo:
        - **Modelo 1:** Uma rede neural simples com camadas `Embedding`, `GlobalAveragePooling1D` e `Dense`.
        - **Modelo 2:** Uma rede neural convolucional (CNN) com camadas `Embedding`, `Conv1D`, `MaxPooling1D`, `GlobalAveragePooling1D`, `Dropout` e `Dense`.
        - **Modelo com camadas LSTM:** Uma rede neural recorrente (RNN) com camadas `Embedding`, `Bidirectional(LSTM)`, `Dense` e `Dropout`.
    - Os modelos foram compilados com o otimizador `Adam`, a função de perda `sparse_categorical_crossentropy` e a métrica `accuracy`.
- **Treinamento:**
    - Os modelos foram treinados com os dados de treino, utilizando o conjunto de teste para validação.
    - O desempenho do modelo foi avaliado usando a acurácia e a perda nos conjuntos de treino e validação.
- **Avaliação:**
    - Uma matriz de confusão foi gerada para visualizar o desempenho do modelo em cada categoria.

### Autocomplete de Texto

- **Amostragem:**
    - Uma amostra menor dos dados foi utilizada para acelerar o treinamento do modelo de autocomplete.
- **Tokenização:**
    - O texto foi tokenizado usando `TextVectorization` do Keras.
- **Pré-processamento:**
    - As sequências de entrada foram preparadas da seguinte forma:
        - Remoção de zeros à direita de cada sequência.
        - Adição de padding à esquerda para garantir o mesmo comprimento.
        - Truncamento de sequências longas.
        - Remoção de sequências repetidas.
- **Modelagem:**
    - Uma rede neural recorrente (RNN) com camadas `Embedding`, `Bidirectional(LSTM)`, `Dense`, `BatchNormalization` e `Dropout` foi utilizada.
    - O modelo foi compilado com a função de perda `categorical_crossentropy`, o otimizador `Adam` e a métrica `accuracy`.
- **Treinamento:**
    - O modelo foi treinado com as sequências de entrada preparadas.
- **Previsão:**
    - Uma função `predict_next_words` foi criada para prever as próximas palavras mais prováveis, dado um texto de entrada.
