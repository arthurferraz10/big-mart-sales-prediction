# Big Mart Sales Prediction - Pipeline de Análise e Modelagem

## 📋 Visão Geral do Projeto

Este projeto implementa um **pipeline completo de ciência de dados** para predição de vendas em lojas Big Mart. O modelo prevê o volume de vendas (`OutletSales`) de produtos em diferentes pontos de venda, considerando características dos produtos, das lojas e das localizações geográficas.

---

## 🎯 Objetivo Principal

Desenvolver um modelo de regressão robusto usando **XGBoost** que capture as relações complexas entre as features e as vendas, com o objetivo de fazer predições precisas em dados novos.

---

## 📂 Estrutura do Repositório

```
big-mart-sales-prediction/
├── README.md                              # Este arquivo
├── Exercicio.md                           # Descrição do exercício
├── markdown.md                            # Documentação adicional
├── src/
│   ├── data.ipynb                        # Notebook de EDA e preparação de dados
│   └── db/
│       ├── Train-Set.csv                 # Dataset de treinamento
│       └── Test-Set.csv                  # Dataset de teste
```

---

## 🔍 Seção 1: Importação de Pacotes e Carga de Dados

### 📦 Bibliotecas Utilizadas

| Biblioteca | Versão | Propósito |
|------------|--------|----------|
| `pandas` | - | Manipulação e análise de dados |
| `numpy` | - | Operações numéricas |
| `matplotlib` | - | Visualizações básicas |
| `seaborn` | - | Visualizações avançadas |
| `scikit-learn` | - | Pré-processamento e métricas |
| `xgboost` | - | Modelo de regressão |

### 📊 Dados Carregados

**Dataset de Treinamento**: `Train-Set.csv`
- **Localização**: `src/db/Train-Set.csv`
- **Formato**: CSV
- **Primeiras e Últimas Linhas**: Examinadas para verificar consistência

---

## 🛠️ Seção 2: Exploração e Análise de Dados (EDA)

### 2.1 Informações Básicas
- **Tipos de Dados**: Verificação de tipos (int, float, object)
- **Uso de Memória**: Alocação de RAM pelo dataset
- **Contagem de Não-Nulos**: Identificação inicial de missing values

### 2.2 Dimensões e Estrutura de Colunas

**Dimensões Iniciais:**
```
Linhas: 8523 observações
Colunas: 11 features + 1 target (OutletSales)
```

| Coluna | Tipo | Descrição |
|--------|------|-----------|
| `ProductID` | Categorical | Identificador único do produto |
| `FatContent` | Categorical | Conteúdo de gordura (Low Fat / Regular) |
| `ProductType` | Categorical | Categoria do produto |
| `Weight` | Numerical | Peso do produto (em kg) |
| `ProductVisibility` | Numerical | Espaço de prateleira dedicado |
| `MRP` | Numerical | Preço de venda máximo |
| `OutletID` | Categorical | Identificador da loja |
| `OutletSize` | Categorical | Tamanho da loja (Small / Medium / High) |
| `LocationType` | Categorical | Tipo de localização (Tier 1, 2, 3) |
| `OutletType` | Categorical | Tipo de loja |
| `EstablishmentYear` | Numerical | Ano de abertura da loja |
| `OutletSales` | Numerical | **ALVO**: Volume de vendas |

### 2.3 Detecção de Valores Ausentes

**Colunas com Missing Values:**
| Coluna | Count Nulos | Percentual |
|--------|------------|-----------|
| `Weight` | ~1705 | ~20.0% |
| `OutletSize` | ~2410 | ~28.3% |

---

## 🔧 Seção 3: Tratamento de Valores Ausentes

### 3.1 Padronização de FatContent

**Problema**: Variações inconsistentes nos valores
- 'LF', 'low fat' → 'Low Fat'
- 'reg' → 'Regular'

**Solução Aplicada**: Dicionário de mapeamento para padronizar em 2 categorias distintas

```python
mapeamento_gordura = {
    'LF': 'Low Fat',
    'low fat': 'Low Fat',
    'Low Fat': 'Low Fat',
    'reg': 'Regular',
    'Regular': 'Regular'
}
```

**Resultado**: Coluna padronizada com valores consistentes

### 3.2 Imputação de Weight

**Estratégia em Duas Etapas:**

1. **Etapa 1**: Preencher com média por `ProductID`
   - Premissa: Cada produto tem peso consistente independente da loja
   - Implementação: `groupby('ProductID')['Weight'].transform('mean')`

2. **Etapa 2**: Preencher remanescentes com média por `ProductType`
   - Casos: Produtos que aparecem uma única vez
   - Implementação: `groupby('ProductType')['Weight'].transform('mean')`

**Resultado**: Redução de valores ausentes de ~20% para 0%

### 3.3 Imputação de OutletSize

**Análise Exploratória:**

#### Distribuição por OutletType:
- **Grocery Store**: 100% "Small"
- **Supermarket Type1**: Distribuição mista (Small, Medium, High)
- **Supermarket Type2**: 100% "Medium"
- **Supermarket Type3**: 100% "Medium"

**Estratégia de Imputação**:
- Usar o **modo (moda)** de `OutletSize` para cada `OutletType`
- Aplicação: Para valores nulos, buscar a categoria mais frequente do seu tipo de loja

**Resultado**: Redução de valores ausentes de ~28.3% para 0%

---

## 📊 Seção 4: Análise Detalhada das Variáveis

### 4.1 Análise de OutletID vs OutletSize

**Achado Importante**: `OutletID` não tem relação 1-para-1 com `OutletSize`
- Cada OutletID aparece apenas uma vez no dataset
- Impossível usar OutletID para identificar univocamente o tamanho da loja

**Implicação**: Usar `OutletType` como proxy para inferir `OutletSize`

### 4.2 Tipos de Lojas (OutletType)

**4 Categorias Identificadas:**
1. Grocery Store
2. Supermarket Type1
3. Supermarket Type2
4. Supermarket Type3

### 4.3 Padrão de Distribuição OutletType × LocationType × OutletSize

Tabela de Cruzamento construída para identificar padrões sistêmicos:
- Alguns padrões são determinísticos (ex: Type2 sempre Medium)
- Outros requerem análise de moda (ex: Type1 com variação)

---

## ✅ Status de Conclusão

### Seção 1: Importação e Carga ✓ CONCLUÍDA
- [x] Importação de todas as bibliotecas necessárias
- [x] Carregamento do dataset de treinamento
- [x] Exploração inicial com head() e tail()

### Seção 2: Exploração e Análise de Dados ✓ CONCLUÍDA
- [x] Verificação de dimensões (shape)
- [x] Análise de tipos de dados (.info())
- [x] Detecção de valores ausentes
- [x] Documentação de 12 colunas (features + target)

### Seção 3: Tratamento de Dados ✓ CONCLUÍDA
- [x] Padronização de FatContent
- [x] Imputação de Weight (2 estratégias)
- [x] Imputação de OutletSize (modo por OutletType)
- [x] Validação: Verificação de 0 valores ausentes após tratamento

### Seção 4: Análise Detalhada ✓ CONCLUÍDA
- [x] Análise OutletID vs OutletSize
- [x] Identificação de 4 tipos de lojas
- [x] Distribuição por OutletType
- [x] Padrões consolidados

### Seção 5: Feature Engineering (Em Planejamento)
- [ ] Criação de features derivadas
- [ ] Encoding de variáveis categóricas (Label Encoding)
- [ ] Normalização/Padronização de features numéricas

### Seção 6: Modelagem (Em Planejamento)
- [ ] Divisão Treino/Teste
- [ ] Treinamento de modelo XGBoost
- [ ] Avaliação de performance (R², MAE, RMSE)
- [ ] Predições em dataset de teste

---

## 🚀 Próximas Etapas

1. **Feature Engineering Avançado**
   - Criar variáveis dummy para categorias
   - Engenharia de features derivadas

2. **Preparação para Modelagem**
   - Label Encoding das variáveis categóricas
   - Divisão Treino/Teste (80/20)
   - Configuração de hiperparâmetros do XGBoost

3. **Modelagem e Avaliação**
   - Treino do modelo XGBoost com n_estimators=750, learning_rate=0.007
   - Avaliação em dados de treino e teste
   - Análise de importância de features

4. **Predição em Dados Novos**
   - Aplicar modelo ao Test-Set.csv
   - Gerar arquivo de predições

---

## HISTÓRICO DE REESTRUTURAÇÕES (data.ipynb)

### ✅ Célula 1: Importação de Bibliotecas

**Markdown Adicionado Acima da Célula:**
```markdown
## 1. Importação de Bibliotecas

As bibliotecas essenciais para análise exploratória, processamento de dados e modelagem de machine learning são importadas abaixo.
```

**Ajuste técnico no código:**
- ✅ Organização das importações seguindo o fluxo do notebook de referência
- ✅ Remoção de comentários redundantes e padronização do estilo
- ✅ Preservação das dependências necessárias para EDA, encoding, split e XGBoost

**Bibliotecas Carregadas:**
| Biblioteca | Propósito |
|------------|-----------|
| `pandas` | Manipulação de dados (DataFrames) |
| `numpy` | Operações numéricas e arrays |
| `matplotlib.pyplot` | Visualizações estáticas |
| `seaborn` | Visualizações estatísticas avançadas |
| `LabelEncoder` | Encoding de variáveis categóricas |
| `train_test_split` | Divisão Treino/Teste |
| `XGBRegressor` | Modelo de regressão extremamente otimizado |
| `metrics` | Métricas de avaliação de modelos |

**Status**: ✅ CONCLUÍDA

---

## 📝 Notas Técnicas

### Decisões de Design

1. **Imputação Hierárquica de Weight**: Dois níveis garantem máxima preservação de informação contextual

2. **Modo para OutletSize**: Escolha baseada na alta associação entre OutletType e OutletSize (muitos tipos têm 100% de uma categoria)

3. **Padronização de FatContent**: Redução de 5 variações para 2 categorias melhora interpretabilidade e reduz sparsidade

### Validações Realizadas
- ✅ Nenhum valor nulo remanescente após imputação
- ✅ Distribuições de dados verificadas para outliers
- ✅ Consistência de tipos de dados confirmada

---

##  Informações

Projeto desenvolvido como parte do pipeline de ciência de dados para Big Mart Sales Prediction.

Mais informaçoes em: https://www.kaggle.com/code/asdcena/big-mart-sales-prediction 

