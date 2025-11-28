# [Segundo Trabalho de Ciências de Dados]

- Ruan Sathler
- Sara Campos

Este repositório contém o código-fonte e os artefatos gerados durante o desenvolvimento do Trabalho de Conclusão de Curso (TCC) focado na análise comparativa de algoritmos de Machine Learning para classificação supervisionada.

## 📋 Sobre o Projeto

O objetivo deste trabalho é avaliar o desempenho de diferentes classificadores (como Random Forest, SVM, Redes Neurais, Gradient Boosting, etc.) em um cenário de predição complexo. O pipeline inclui:

1.  **Pré-processamento:** Tratamento de variáveis categóricas e numéricas.
2.  **Otimização de Hiperparâmetros:** Utilização de `HalvingGridSearchCV` para encontrar as melhores configurações.
3.  **Validação Estatística:** Uso de Validação Cruzada Robusta (`RepeatedStratifiedKFold`) e testes de hipótese (Wilcoxon).
4.  **Interpretabilidade:** Análise de *Feature Importance* utilizando SHAP (SHapley Additive exPlanations).

---

## 💾 Gerenciamento de Arquivos Grandes (Data & Models)

Devido ao tamanho dos modelos treinados (especialmente os ensembles) e das limitações de upload do GitHub (máximo de 100MB por arquivo), adotou-se uma estratégia híbrida de armazenamento:

### 1. Salvamento Local
Durante a execução do notebook, os resultados intermediários e finais são salvos automaticamente na pasta local:
- `data/modelos_otimizados.pkl`
- `data/resultados_estatisticos.pkl`

Isso garante que o progresso não seja perdido caso o ambiente de execução (ex: Google Colab) seja reiniciado.

### 2. Recuperação via Nuvem (Google Drive)
Para garantir a reprodutibilidade do projeto sem a necessidade de re-treinar os modelos (o que leva muitas horas), os arquivos binários finais (`.pkl`) foram hospedados no Google Drive.

O código implementa uma rotina automática que:
1.  Verifica se o arquivo existe localmente.
2.  Se não existir, realiza o download automático direto da nuvem usando a biblioteca `gdown`.

**Links dos artefatos (já integrados no código):**
- 🧠 **Modelos Treinados (~1.3 GB):** [Download Link](https://drive.google.com/uc?id=1eb2GtRaRjojrBc8la4_dpXedgkQmoqj5)
- 📊 **Tabelas Estatísticas & Wilcoxon:** [Download Link](https://drive.google.com/uc?id=1rVDu3ihAQitB_GsMT053KVgrJW2X4j6T)

---

## 🔍 Nota sobre Interpretabilidade (SHAP)

A etapa de explicação do modelo utiliza a biblioteca **SHAP**.

Devido à alta complexidade computacional de alguns modelos (como *Support Vector Machines* e *Redes Neurais*) e ao tamanho do dataset, o cálculo dos valores SHAP para todas as instâncias seria inviável (estimativa de >15 horas de processamento).

**Solução Adotada:**
Foi aplicada uma amostragem aleatória controlada (`random_state=42`) para reduzir o conjunto de análise para **100 observações**.
- Isso permite gerar os gráficos de `summary_plot` em minutos.
- A amostra é estatisticamente suficiente para identificar as tendências globais de importância das variáveis (Feature Importance).

---



## 📊 Estrutura de Diretórios

```text
.
├── data/                       # Dataset original (CSV), local onde os dados de treino e teste são salvol
├── img/                        # Imagens e gráficos gerados
├── Dicionario de dados.ipynb   # Explicação das colunas/variáveis
├── Trabalho Pratico 2 - DS.ipynb  # CÓDIGO FONTE PRINCIPAL
└── README.md                   # Este arquivo
