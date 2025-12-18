# Reconhecimento de Escrita Manual com PyTorch 🖋️

Este projeto foi desenvolvido como parte de um estudo sobre redes neuronais profundas aplicadas à Visão Computacional. O objetivo principal é a criação de um modelo capaz de transcrever nomes manuscritos a partir de imagens.

## 👥 Autores
* **Alexandre Santos Sousa** — n.º 119030
* **Francisco Santos Sousa** — n.º 119121

---

## 🎯 Objetivo do Projeto
Desenvolver e treinar uma rede neuronal em **PyTorch** que processe imagens de palavras escritas à mão e as converta em texto digital. O sistema lida com variabilidades na escrita, como inclinação, espessura do traço e diferentes estilos caligráficos.



## 📊 Base de Dados
O modelo utiliza o dataset **Handwriting Recognition**, disponível no Kaggle.
* **Fonte:** [Kaggle - Handwriting Recognition Data](https://www.kaggle.com/datasets/landlord/handwriting-recognition/data)
* **Conteúdo:** Milhares de imagens de nomes próprios e apelidos, acompanhadas por ficheiros CSV contendo as etiquetas (labels) correspondentes.

---

## 🛠️ Configuração e Tecnologias
O projeto utiliza as seguintes bibliotecas e ferramentas:

* **Deep Learning:** `torch`, `torchvision` (v2 para transformações).
* **Processamento de Dados:** `polars` (leitura otimizada de CSV), `numpy`.
* **Visualização:** `matplotlib`, `seaborn`.
* **Gestão de Imagem:** `PIL` (Pillow).
* **Métricas:** `sklearn` (matriz de confusão).

O código está configurado para detetar e utilizar aceleração por hardware automaticamente (**CUDA** para Nvidia, **MPS** para Mac ou **CPU** como fallback).

---

## ⚙️ Fluxo de Trabalho

### 1. Pré-processamento
* **Redimensionamento:** Todas as imagens são convertidas para $64 \times 256$ píxeis para manter a consistência na entrada da rede.
* **Normalização:** Conversão para tensores e escala de cinza.
* **Codificação (Charset):** Mapeamento de caracteres `ABCDEFGHIJKLMNOPQRSTUVWXYZ-` para índices numéricos. O índice `0` é reservado para o caractere "blank" (necessário para a função de perda CTC).



### 2. Dataset Personalizado (`CustomDataSet`)
Foi implementada uma classe que herda de `torch.utils.data.Dataset` para:
* Filtrar automaticamente dados inválidos (como etiquetas marcadas como `UNREADABLE` ou `EMPTY`).
* Carregar imagens de forma eficiente utilizando a biblioteca `Pillow`.
* Integrar as transformações do `torchvision` em tempo real.

### 3. Visualização
O notebook inclui ferramentas para validar o carregamento dos dados, exibindo amostras das imagens e comparando-as com os rótulos originais para garantir a integridade do treino.

---

## 🚀 Como Executar

1. **Instale as dependências:**
   ```bash
   pip install torch torchvision polars matplotlib seaborn scikit-learn tqdm Pillow
