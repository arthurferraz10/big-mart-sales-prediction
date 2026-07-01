# 📊 Big Mart Sales: Modelagem Preditiva & Otimização de Estoque

**Objetivo:** Construir um modelo preditivo robusto para estimar o volume de vendas (`Item_Outlet_Sales`) das filiais da Big Mart, compreendendo os impulsionadores de receita.

## 📑 Índice
1. **Configuração do Ambiente e Importação de Bibliotecas**
2. **Coleta e Inspeção Inicial dos Dados**
3. **Saneamento de Dados (Data Cleaning)**
   - 3.1. Tratamento de Valores Ausentes
   - 3.2. Correção de Anomalias e Padronização
4. **Engenharia de Features (Feature Engineering)**
   - 4.1. Derivação de Novas Variáveis (ex: Idade Operacional da Loja)
   - 4.2. Transformação de Features Numéricas e Categóricas
5. **Análise Exploratória de Dados (EDA) & Data Storytelling**
   - 5.1. Análise Univariada (Distribuição da Variável Alvo)
   - 5.2. Análise Bivariada e Correlações
6. **Modelagem Preditiva Avançada**
   - 6.1. Divisão Treino/Validação (Prevenção de Data Leakage)
   - 6.2. Treinamento de Modelos Baseline (Random Forest)
   - 6.3. Algoritmos de Gradient Boosting (XGBoost / LightGBM)
7. **Avaliação e Escolha do Modelo**
   - 7.1. Comparação de Métricas (RMSE, MAE, R2)
   - 7.2. Análise de Importância das Features (Feature Importance)
8. **Conclusões e Próximos Passos**