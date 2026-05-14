# Detecção de Fraudes com Machine Learning - PaySim

Projeto acadêmico desenvolvido no programa de Mestrado em Engenharia de Computação pela UFABC, focado em aplicar técnicas de aprendizado de máquina para identificar padrões fraudulentos em transações financeiras simuladas.

## Visão Geral

Este repositório implementa uma solução de detecção de fraudes utilizando dados do PaySim, um simulador de transações móveis monetárias baseado em dados do mundo real. O projeto explora o ciclo completo de análise de dados, desde a preparação até a modelagem com algoritmos de aprendizado supervisionado.

## Estrutura do Repositório

```
fraud_detection_ML/
├── PaySim_Fraud_detection.ipynb    # Notebook principal com análise e modelagem
├── LICENSE                          # Licença CC0 1.0 Universal
├── .gitignore                       # Configuração de arquivos ignorados
└── README.md                        # Este arquivo
```

## Dataset

### Origem e Características

O dataset utilizado é o **PaySim - Fraud Detection Example**, disponibilizado no Kaggle, que contém transações monetárias simuladas em um sistema móvel de pagamentos.

**Dimensões do dataset:**
- 101.613 registros de transações
- 11 atributos por transação
- Desbalanceamento de classes na variável alvo

### Dicionário de Dados

| Atributo | Descrição | Tipo |
|----------|-----------|------|
| `step` | Unidade de tempo em horas | Numérico |
| `type` | Tipo de transação (CASH-IN, CASH-OUT, DÉBITO, PAGAMENTO, TRANSFERÊNCIA) | Categórico |
| `amount` | Valor da transação em moeda local | Numérico (float) |
| `nameOrig` | Identificador do originador da transação | String |
| `oldbalanceOrg` | Saldo inicial do originador antes da transação | Numérico (float) |
| `newbalanceOrig` | Saldo do originador após a transação | Numérico (float) |
| `nameDest` | Identificador do destinatário da transação | String |
| `oldbalanceDest` | Saldo inicial do destinatário antes da transação | Numérico (float) |
| `newbalanceDest` | Saldo do destinatário após a transação | Numérico (float) |
| `isFraud` | Indicador de fraude detectada (0 = legítimo, 1 = fraudulento) | Binário |
| `isFlaggedFraud` | Tentativa ilegal de transferir grande quantidade em transação única | Binário |

### Tipos de Transação

- **CASH-IN**: Depósito em dinheiro
- **CASH-OUT**: Saque em dinheiro
- **DÉBITO**: Transação de débito
- **PAGAMENTO**: Pagamento de conta
- **TRANSFERÊNCIA**: Transferência entre contas

## Tecnologias e Ferramentas

### Plataforma e Ambiente

- **Google Colab**: Ambiente de execução da análise e treinamento
- **Python 3**: Linguagem de programação principal
- **Jupyter Notebook**: Interface interativa para desenvolvimento exploratório

### Bibliotecas de Análise e Processamento

| Biblioteca | Propósito |
|-----------|----------|
| `pandas` | Manipulação, transformação e análise de dados estruturados |
| `numpy` | Operações numéricas e cálculos vetorizados |
| `scikit-learn` | Algoritmos de aprendizado de máquina e preprocessamento |
| `matplotlib` | Visualização estática de dados e resultados |
| `seaborn` | Visualizações estatísticas avançadas |

## Metodologia e Arquitetura da Solução

### 1. Exploração e Preparação de Dados

O processo inicia com uma análise exploratória completa dos dados:

- **Carregamento dos dados**: Importação do dataset CSV usando pandas
- **Visualização estrutural**: Inspeção de dimensões, tipos de dados e valores ausentes
- **Análise descritiva**: Cálculo de estatísticas resumidas (média, mediana, desvio padrão, quartis)
- **Padronização de nomenclatura**: Renomeação de colunas para melhor interpretabilidade

#### Transformações Aplicadas

```
Colunas Originais → Colunas Processadas
isFraud           → Fraude
isFlaggedFraud    → Alerta FR
step              → Tempo
type              → Tipo
amount            → Valor
nameOrig          → cliente1
oldbalanceOrg     → saldo_inicial_c1
newbalanceOrig    → novo_saldo_c1
nameDest          → cliente2
oldbalanceDest    → saldo_inicial_c2
newbalanceDest    → novo_saldo_c2
```

### 2. Engenharia de Características

A fase de engenharia de características busca extrair informações relevantes que auxiliem na discriminação entre transações legítimas e fraudulentas:

- **Análise de variância**: Identificação de atributos com poder discriminatório
- **Criação de features derivadas**: Novas variáveis calculadas a partir dos atributos brutos
- **Encoding de variáveis categóricas**: Conversão de tipos de transação em formato numérico
- **Normalização e padronização**: Ajuste de escala dos atributos numéricos

### 3. Tratamento do Desbalanceamento de Classes

O dataset apresenta alta proporção de transações legítimas versus fraudulentas:

- **Taxa de fraude**: Aproximadamente 0,1142% (1.142 em 100.000 transações)
- **Estratégias aplicáveis**:
  - Reamostragem (oversampling/undersampling)
  - Ajuste de pesos de classes no modelo
  - Uso de métricas de avaliação apropriadas (precision, recall, F1-score, ROC-AUC)

### 4. Modelagem Preditiva

#### Algoritmos Implementados

A solução pode utilizar diversos algoritmos de classificação:

**1. Regressão Logística**
- Modelo linear simplificado
- Interpretabilidade alta
- Base para comparação de performance

**2. Árvores de Decisão (Decision Trees)**
- Captura relações não-lineares
- Estrutura interpretável
- Sensível a overfitting

**3. Florestas Aleatórias (Random Forest)**
- Ensemble de múltiplas árvores de decisão
- Redução de overfitting através de agregação
- Importância automática das variáveis

**4. Máquinas de Vetores de Suporte (SVM)**
- Classificador de márgem máxima
- Eficaz em espaços de alta dimensionalidade
- Requer ajuste cuidadoso de hiperparâmetros

**5. Gradient Boosting**
- Construção sequencial de modelos fracos
- Correção iterativa de erros
- Desempenho potencialmente superior

#### Arquitetura do Pipeline

```
Dados Brutos
    ↓
Carregamento (pandas)
    ↓
Exploração Exploratória
    ↓
Limpeza e Transformação
    ↓
Engenharia de Características
    ↓
Divisão Treino/Teste (80/20)
    ↓
Normalização/Padronização
    ↓
Treinamento do Modelo
    ↓
Avaliação e Validação
    ↓
Ajuste de Hiperparâmetros
    ↓
Resultado Final
```

### 5. Avaliação de Performance

Métricas e técnicas para avaliar a capacidade preditiva:

| Métrica | Descrição | Interpretação |
|---------|-----------|----------------|
| **Acurácia** | Proporção de predições corretas | Limitada em datasets desbalanceados |
| **Precisão** | Proporção de fraudes detectadas que são reais | Importância: evitar falsos positivos |
| **Recall/Sensibilidade** | Proporção de fraudes reais que foram identificadas | Importância: capturar máximo de fraudes |
| **F1-Score** | Média harmônica entre precisão e recall | Balanço entre métricas |
| **ROC-AUC** | Área sob a curva ROC | Avalia discriminação em vários limiares |
| **Matriz de Confusão** | Distribuição de acertos/erros | Análise detalhada de erros |

### 6. Validação Cruzada

Aplicação de k-fold cross-validation para avaliação mais robusta:

- Divisão dos dados em k subconjuntos
- Treinamento e teste repetido k vezes
- Média das métricas para estimativa mais estável da performance

## Conhecimento Aplicado

### Fundamentação Teórica

Este projeto integra conceitos fundamentais de aprendizado de máquina supervisionado:

**1. Aprendizado Supervisionado**
- Treinamento com dados rotulados (presença ou ausência de fraude)
- Objetivo: minimizar erro de predição em dados não vistos

**2. Classificação Binária**
- Problema de duas classes mutuamente exclusivas
- Otimização de modelos para discriminação entre classes

**3. Análise Exploratória de Dados (EDA)**
- Compreensão dos padrões e distribuições nos dados
- Identificação de outliers e anomalias
- Fundamentação para decisões de engenharia de características

**4. Preprocessamento de Dados**
- Tratamento de valores ausentes
- Remoção ou tratamento de outliers
- Normalização para equidade na escala de features

**5. Validação de Modelos**
- Divisão treino/teste para avaliação imparcial
- Cross-validation para estabilidade das estimativas
- Detecção e prevenção de overfitting

**6. Interpretabilidade em Segurança**
- Compreensão dos fatores que levam à predição
- Crítica em contextos financeiros onde decisões devem ser explicáveis
- Balance entre acurácia e interpretabilidade

### Aplicações Práticas

**Detecção de Fraude em Sistemas Financeiros**
- Proteção contra roubo de identidade
- Prevenção de esvaziamento de contas
- Identificação de transferências suspeitas

**Investigação de Padrões**
- Análise de comportamento de transações
- Identificação de contas comprometidas
- Detecção de redes de fraude

**Otimização de Recursos**
- Redução de análises manuais falsas
- Priorização de investigações de alto risco
- Minimização de impacto em usuários legítimos

## Como Executar

### Pré-requisitos

- Conta no Google Colab (acesso gratuito via Gmail)
- Dataset PaySim (arquivo CSV)
- Conexão com internet

### Passos para Execução

1. **Acesse o notebook no Google Colab**
   - Abra https://colab.research.google.com
   - Selecione "Upload notebook"
   - Faça upload do arquivo `PaySim_Fraud_detection.ipynb`

2. **Prepare os dados**
   - Faça upload do dataset CSV: `fraud_dataset_example.csv`
   - Aguarde o processamento

3. **Execute as células sequencialmente**
   - Pressione Shift + Enter ou clique no botão de execução
   - Acompanhe os outputs gerados

4. **Interprete os resultados**
   - Analise as visualizações geradas
   - Revise as métricas de desempenho
   - Valide as predições

## Resultados Esperados

O notebook gera:

- Análise estatística completa do dataset
- Visualizações dos padrões de fraude
- Performance dos modelos treinados
- Matriz de confusão e métricas de avaliação
- Importância relativa das características

## Limitações e Considerações

1. **Dados Simulados**: O PaySim, embora baseado em dados reais, é uma simulação que pode não capturar toda a complexidade de fraudes reais

2. **Desbalanceamento Severo**: A baixa prevalência de fraude pode dificultar o treinamento de modelos equilibrados

3. **Generalizabilidade**: Modelos treinados em PaySim podem não generalizar perfeitamente para sistemas reais diferentes

4. **Features Limitadas**: O dataset não inclui informações comportamentais ou de contexto externo que poderiam melhorar predições

5. **Mudança Temporal**: Fraudes evoluem ao longo do tempo; modelos treinados em período histórico podem perder eficácia

## Possíveis Extensões e Melhorias

- Incorporação de dados temporais e sazonalidade
- Aplicação de técnicas de detecção de anomalia não supervisionada
- Ensemble com múltiplos modelos (stacking, blending)
- Implementação de feature selection automatizada
- Desenvolvimento de sistemas de explicabilidade (LIME, SHAP)
- Análise de drift de conceito e retrainamento adaptativo
- Integração com APIs de dados financeiros reais (com privacidade garantida)

## Licença

Este projeto está licenciado sob a licença **Creative Commons Zero v1.0 Universal (CC0 1.0)**. 

A licença CC0 permite uso irrestrito: você pode copiar, modificar, distribuir e utilizar este trabalho para fins comerciais e não-comerciais, sem solicitação de permissão.

## Referências e Recursos

### Datasets
- PaySim: A financial mobile money simulator with fraud detection
- Disponível em: https://www.kaggle.com/datasets/gopalmahadevan/fraud-detection-example

### Documentação de Bibliotecas
- Pandas: https://pandas.pydata.org/docs/
- scikit-learn: https://scikit-learn.org/stable/documentation.html
- Matplotlib: https://matplotlib.org/stable/contents.html

### Conceitos Teóricos
- "An Introduction to Statistical Learning" - James, Witten, Hastie, Tibshirani
- "Machine Learning" - Tom Mitchell
- "Pattern Recognition and Machine Learning" - Christopher Bishop

## Autor

**Yuri Komuta**

Estudante de Mestrado em Engenharia de Computação
Universidade Federal do ABC (UFABC)

## Contato e Sugestões

Para dúvidas, sugestões ou discussões sobre este projeto, abra uma issue no repositório GitHub.

---

**Última atualização:** 14 de maio de 2026

**Status do Projeto:** Ativo e aberto a contribuições

