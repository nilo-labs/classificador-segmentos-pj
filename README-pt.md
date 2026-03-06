# Classificador de Clientes PJ - Segmentação de Crédito com IA

[🌍 Read in English](./README.md) | [🇧🇷 Leia em Português](./README-pt.md)

Este projeto de Machine Learning tem como objetivo classificar clientes corporativos (Pessoa Jurídica) de uma empresa de crédito em diferentes segmentos (**Starter, Bronze, Silver e Gold**). A classificação auxilia na tomada de decisões estratégicas e na oferta personalizada de produtos financeiros.

O projeto abrange desde a Análise Exploratória de Dados (EDA) até o deploy de uma interface interativa para predição em lote.

## Estrutura do Projeto

Os principais arquivos do repositório são:

* `classificacao_segmento_empresa.ipynb`: O "núcleo" do projeto. Notebook Jupyter contendo:
    * Análise Exploratória de Dados (EDA) com gráficos (Plotly/Matplotlib).
    * Pré-processamento de dados (Pipeline, Imputação, OneHotEncoding).
    * Treinamento do modelo (Decision Tree Classifier).
    * Otimização de hiperparâmetros com **Optuna**.
    * Criação de uma interface **Gradio** para uso do modelo.
* `dataset_segmentos_clientes.csv`: Base de dados histórica utilizada para treinar e validar o modelo.
* `novas_empresas.csv`: Arquivo de exemplo contendo novos clientes para testar a predição do modelo.
* `modelo_classificacao_decision_tree.pkl`: O modelo treinado e serializado (salvo) pronto para uso.
* `Pipfile` & `Pipfile.lock`: Arquivos de gerenciamento de dependências (ambiente virtual Pipenv).
* `README.md`: Documentação do projeto.

## Tecnologias Utilizadas

O projeto foi desenvolvido em **Python 3.13**, utilizando o gerenciador de pacotes **Pipenv**. As principais bibliotecas são:

* **Manipulação de Dados:** `pandas`, `numpy`
* **Visualização:** `matplotlib`, `plotly`, `pingouin`
* **Machine Learning:** `scikit-learn` (Decision Tree, Pipelines, Cross-Validation)
* **Otimização:** `optuna` (Ajuste fino de hiperparâmetros)
* **Interface/Deploy:** `gradio` (Criação de App Web para upload de CSV)
* **Serialização:** `joblib`

## 📊 Dicionário de Dados

As variáveis utilizadas para classificar as empresas são:

| Variável | Tipo | Descrição |
| :--- | :--- | :--- |
| `atividade_economica` | Categórica | Setor de atuação (ex: Comércio, Indústria, Serviços, Agronegócio). |
| `faturamento_mensal` | Numérica | Faturamento médio mensal da empresa. |
| `numero_de_funcionarios` | Numérica | Quantidade total de colaboradores. |
| `localizacao` | Categórica | Cidade/Estado da sede (ex: São Paulo, Rio de Janeiro). |
| `idade` | Numérica | Tempo de existência da empresa (em anos). |
| `inovacao` | Numérica | Índice de inovação interno (score). |
| **`segmento_de_cliente`** | **Alvo** | A classificação final: **Starter, Bronze, Silver, Gold**. |

## Como Executar o Projeto

### Pré-requisitos
* Python 3.13+
* Pipenv (Gerenciador de pacotes)

### Passo a passo
1. Clone o repositório:
   ```bash
   git clone https://github.com/danilotavares-dev/classificador-clientes-IA.git
   cd nome-do-repo
   ```

2. Instale as dependências:
    ```bash
    pip install pipenv
    pipenv  install
    ```
3. Execute o Notebook ou a Interface: Para rodar a interface do Gradio diretamente:
    * Abra o arquivo classificacao_segmento_empresa.ipynb no Jupyter Notebook e execute todas as células para iniciar a interface Gradio no final.

## Resultados e Insights

Durante a Análise Exploratória e a modelagem, o projeto enfrentou o desafio de um dataset desbalanceado, cenário comum em riscos de crédito.

### Performance Técnica
* **Acurácia Global:** O modelo (Decision Tree) atingiu ~47% na validação cruzada.
* **Otimização (Optuna):** A melhor configuração encontrada foi `min_samples_leaf: 4` e `max_depth: 2`.

### Análise de Negócio
* **Fator Decisivo:** O teste de Qui-Quadrado confirmou que a variável `inovacao` é o maior discriminador. Empresas inovadoras tendem fortemente aos segmentos 'Gold' ou 'Silver'.
* **Limitações:** O modelo performa bem na classe majoritária ('Silver'), mas confunde segmentos adjacentes (ex: Bronze com Silver) devido à sobreposição de faturamento.

## Próximos Passos
Para melhorar a performance do classificador em versões futuras:

* Testar algoritmos de Ensemble (como Random Forest ou Gradient Boosting) para tentar superar a acurácia da Árvore de Decisão simples.
* Realizar engenharia de atributos (Feature Engineering) para criar novas variáveis que possam ter maior poder preditivo.
* Balancear as classes do dataset, visto que há uma desproporção entre os segmentos (ex: muitos 'Silver' e poucos 'Gold').

## Galeria do Projeto

### 1. Análise de Dados (EDA)
Como descrito nos insights, a variável **Inovação** provou ser o maior divisor de águas entre os segmentos. O gráfico abaixo ilustra essa correlação:

![Gráfico de Inovação vs Segmento](img/grafico_analise.png)

### 2. Aplicação em Funcionamento
O projeto conta com uma interface **Gradio** para facilitar o uso por times de negócio. Basta fazer o upload da planilha de novos clientes:

![Interface de Predição Gradio](img/demo_gradio.png)
