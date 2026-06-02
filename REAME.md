# Detecção de Fraudes Contextuais em Cartões de Crédito 💳

Este repositório contém o código-fonte, os experimentos e os artefatos do **Trabalho 2** desenvolvido para o Programa de Pós-Graduação em Sistemas de Informação (PPgSI - EACH-USP).

O objetivo do projeto é avaliar o desempenho dos algoritmos `Random Forest` e `HistGradientBoosting` na identificação de fraudes financeiras utilizando variáveis de contexto imediato (espacial e temporal), tratando o desbalanceamento severo de classes.

---

## 📁 Estrutura do Repositório

* `experimento.ipynb`: Notebook principal contendo o pipeline completo de desenvolvimento, tratamento de dados, engenharia de atributos, treinamento, balanceamento de pesos e avaliação dos modelos.
* `analise_fraude.py`: Script estruturado com as funções consolidadas do pipeline de engenharia e modelagem (pronto para execução em lote ou terminal).
* `matrizes_confusao.png`: Gráfico comparativo gerado automaticamente avaliando os falsos positivos de ambos os modelos.
* `.gitignore`: Configuração para impedir o upload de ambientes virtuais (`.venv`) e da base de dados bruta (.csv), seguindo as boas práticas de versionamento.

---

## 🚀 Como Executar o Projeto

### 1. Pré-requisitos
Certifique-se de ter o Python 3.10+ instalado no seu ambiente. Recomenda-se a utilização de um ambiente virtual:

python3 -m venv .venv
source .venv/bin/activate  # No macOS/Linux
#.venv\Scripts\activate     # No Windows

Instale as dependências mandatórias do ecossistema de Data Science:
pip install pandas numpy scikit-learn matplotlib seaborn kagglehub

### 2. Executando via Jupyter Notebook (`experimento.ipynb`)
1. Abra o arquivo no VS Code.
2. Execute as 4 células em ordem sequencial:
    * **Célula 1:** Faz o download automático do dataset via API do Kaggle, realiza a amostragem de 10% (55.572 registros) e calcula a distância via fórmula de Haversine.
    * **Célula 2:** Executa o cenário baseline (modelos com parametrização padrão e recall nulo devido ao desbalanceamento).
    * **Célula 3:** Executa o cenário balanceado (`class_weight='balanced'`), exibindo os relatórios de classificação completos.
    * **Célula 4:** Geração e salvamento do gráfico comparativo de matrizes de confusão.

### 3. Executando via Script Terminal (`analise_fraude.py`)
Para rodar o pipeline completo diretamente pelo terminal e visualizar os logs de treinamento e tabelas de métricas, basta executar:

python analise_fraude.py

---

## 📊 Resultados Obtidos (Resumo)

O pipeline avalia o trade-off crítico do ambiente bancário:
* **HistGradientBoosting (Balanced):** Alto recall (60%), mas gera **2.182 falsos positivos** (alto impacto de fricção).
* **Random Forest (Balanced):** Baixo índice de falsos positivos (249), mas captura apenas 25% das fraudes reais.