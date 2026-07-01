# 3.4 Desafio DATA1: Ciência de Dados e Machine Learning

## Tema: Modelagem Preditiva de Vendas para a Big Mart

### Cenário e Problema de Negócio
A Big Mart, uma grande rede varejista, iniciou um projeto de expansão e otimização de estoque. A equipe de inteligência de negócios coletou dados de vendas de múltiplos produtos distribuídos em 10 lojas diferentes.

A diretoria precisa entender quais propriedades dos produtos e quais características das lojas desempenham um papel crucial no aumento das vendas. A sua missão é construir um modelo preditivo capaz de prever o volume de vendas (OutletSales) de cada produto em uma determinada loja.

### Dataset Utilizado
O conjunto de dados contém atributos dos produtos e das lojas, separado em arquivos de Treino e Teste.
**Big Mart Sales Dataset**
Disponível em: https://www.kaggle.com/datasets/akashdeepkuila/big-mart-sales

### Requisitos Técnicos
* **Stack Tecnológica:** Python (Pandas, NumPy, Scikit-Learn, Matplotlib/Seaborn) ou Linguagem R equivalente.
* **Ambiente e Artefato de Entrega:** Um Jupyter Notebook (.ipynb) rigorosamente estruturado, combinando blocos de código com documentação em texto (Markdown).
* **Metodologia:** Esperamos que o desenvolvimento siga o ciclo de vida padrão de um projeto de ciência de dados.

### Funcionalidades Obrigatórias (Requisitos Core)
1. **Preparação e Saneamento da Base**
   O candidato deve carregar a base de dados de treino e prepará-la para as etapas seguintes. As decisões tomadas durante a transformação, limpeza e engenharia de features (Feature Engineering) devem ser explicitamente justificadas no relatório do Notebook.

2. **Análise Exploratória de Dados (EDA)**
   Extrair inteligência dos dados estruturados antes da modelagem matemática. O candidato deve mapear correlações, identificar comportamentos de consumo e sustentar essas descobertas com visualizações gráficas claras e interpretáveis.

3. **Modelagem Preditiva**
   Treinar um ou mais algoritmos de Machine Learning supervisionado para prever a variável alvo (OutletSales).
   Realizar a divisão correta dos dados (Train/Validation Split) a partir da base de treino fornecida.
   Avaliar a performance do modelo utilizando métricas de regressão adequadas (ex: RMSE, MAE, R²), justificando o motivo da escolha do algoritmo final.

### Critérios de Avaliação
* **Maturidade na Preparação dos Dados:** Capacidade de identificar e tratar anomalias latentes, valores discrepantes e formatar os dados adequadamente sem degradar a integridade da informação.
* **Rigor Metodológico:** Estruturação lógica do pipeline de Machine Learning (prevenção de Data Leakage, escalonamento, codificação de variáveis categóricas).
* **Data Storytelling e Relatório Técnico:** Clareza da narrativa analítica apresentada no Notebook e a capacidade de explicar as falhas e os acertos do modelo preditivo de forma executiva.

### Diferenciais Técnicos
* Utilização de técnicas de otimização de hiperparâmetros (ex: GridSearchCV, Optuna).
* Implementação de algoritmos avançados baseados em Árvores (ex: XGBoost, LightGBM, CatBoost).
* Modularização do código (extrair funções de pré-processamento do Notebook para ficheiros .py auxiliares).

---

### EXTRA: Deploy de Aplicação Analítica (Data App)
Um modelo preditivo que reside apenas num ficheiro Jupyter Notebook não entrega valor na ponta para o utilizador final. O desafio extra que confere pontos de bónus significativos consiste em colocar a sua solução num formato acessível.

Utilize bibliotecas de interface rápida como Streamlit (ou Dash/Gradio) para criar uma pequena aplicação web (Data App).

#### Política de Inteligência Artificial (Liberada)
A CODE valoriza a produtividade. Para a construção exclusiva desta interface web (Streamlit), o uso de Inteligência Artificial (ChatGPT, Gemini, GitHub Copilot) para gerar o código estrutural da aplicação é totalmente liberado e encorajado.

No entanto, aplica-se a nossa regra de ouro: Deverá descrever no relatório do repositório tudo o que foi feito com o auxílio da IA. O candidato deve ser capaz de executar a interface localmente e explicar como a mesma consome o modelo preditivo que treinou.

#### O que esperamos ver na Interface?
Uma interface com campos de entrada (formulário ou sliders) onde um gerente da Big Mart possa introduzir as características de um produto fictício e da sua loja.
Ao clicar num botão de "Prever", a aplicação deverá carregar o seu modelo treinado (através de um ficheiro .pkl ou similar exportado com joblib/pickle) e apresentar na tela a estimativa de vendas para esse cenário.

#### Instruções de Entrega (Extra)
Caso decida aceitar o desafio, inclua o ficheiro da interface (ex: app.py) e o modelo exportado no repositório. Atualize o seu README.md principal com os comandos exatos de instalação (ex: pip install streamlit) e execução para que possamos testar a aplicação no nosso ambiente.