# 🍦 Previsão Inteligente de Vendas de Sorvete (Gelato Mágico) com Azure ML Designer & Auto ML

## 🚀 Resumo do Projeto

Este projeto demonstra a aplicação de Machine Learning para a otimização de produção e estoque da sorveteria Gelato Mágico, onde as vendas são fortemente correlacionadas com a temperatura diária.

Para garantir a melhor precisão e demonstrar proficiência em MLOps na nuvem, exploramos duas abordagens distintas dentro do Azure Machine Learning:

- **Azure ML Designer:** Criação visual (low-code) de um pipeline de regressão.
- **Automated ML (AutoML):** Uso da ferramenta de otimização para encontrar o melhor modelo, hyperparâmetros e feature engineering automaticamente.

O projeto foi concluído com o deployment do modelo vencedor (**VotingEnsemble** com 7 modelos XGBoost) em um Real-Time Endpoint, garantindo previsões instantâneas para o planejamento diário.

## 🎯 Objetivos Chave

- Desenvolver um Modelo de Regressão para prever vendas com base na temperatura.
- Comparar e Implementar Pipelines usando Designer e Automated ML.
- Gerenciar o Modelo com o registro integrado do Azure ML / MLflow.
- Implementar o Modelo em um Real-Time Endpoint para previsões em produção (nuvem).

## 🛠️ Tecnologias e Ferramentas

| Categoria | Ferramenta | Uso no Projeto |
|-----------|-----------|----------------|
| Plataforma MLOps | Azure Machine Learning | Orquestração de pipeline, registro e deployment. |
| Modelagem 1 | Azure ML Designer | Criação visual (drag-and-drop) do pipeline de treinamento. |
| Modelagem 2 | Automated ML | Otimização automática de algoritmos (Regressão) e hyperparâmetros. |
| Modelo ML | VotingEnsemble (XGBRegressor) | Ensemble de 7 modelos XGBoost para prever vendas. |
| Rastreamento | MLflow | Registro de modelos e métricas integrado ao Azure ML. |

## 📂 Estrutura do Repositório
```
Azure-ML-Previsao-Vendas-Regressao-Linear/
├── inputs/
│   └── sorvetes.csv                           <- Dataset histórico (Data, Vendas, Temperatura)
├── azure_automl/                              <- Arquivos de configuração do AutoML
├── clever_goat_50r99k77vl_21/                 <- Modelo vencedor do AutoML (VotingEnsemble)
│   ├── model/
│   │   └── script.py                          <- Script do modelo treinado
│   └── deploy/                                <- Arquivos para deployment
├── README.md                                  <- Este documento
├── LICENSE                                    <- Licença MIT
└── .gitignore
```

> **Nota:** As screenshots mencionadas no README (pipeline do Designer, resultados do AutoML, endpoint) devem ser adicionadas ao projeto posteriormente para documentação visual completa.

## 📊 Processo MLOps no Azure ML: Duas Abordagens

O projeto seguiu um fluxo MLOps completo, explorando duas maneiras de treinar o modelo, o que permitiu uma comparação direta de desempenho e esforço.

### 1. Abordagem 1: Pipeline de Treinamento (Azure ML Designer)
O pipeline de treinamento inicial foi construído visualmente no Designer. Essa abordagem forneceu controle total sobre cada etapa (divisão de dados, seleção do algoritmo de Regressão Linear e avaliação).

**Visão do Pipeline de Treinamento (Designer):**

> **Nota:** Adicionar screenshot do Pipeline de Treinamento no Azure ML Designer mostrando as etapas de:
> - Importação de dados (sorvetes.csv)
> - Split dos dados (treinamento/teste)
> - Treinamento do modelo de Regressão Linear
> - Avaliação do modelo

### 2. Abordagem 2: Otimização Automática (Automated ML)

Para garantir que o melhor algoritmo fosse selecionado, submetemos o mesmo conjunto de dados ao Automated ML (AutoML), configurando-o para resolver um problema de Regressão.

O AutoML testou múltiplos algoritmos (incluindo XGBoost, LightGBM, Random Forest, entre outros) e fez o ajuste fino (hyperparameter tuning) automaticamente.

**Vencedor do AutoML:**

- **Melhor Algoritmo:** VotingEnsemble (Ensemble de 7 modelos XGBRegressor)
- **ID da Execução:** clever_goat_50r99k77vl_21
- **Técnica:** Soft Voting com pesos otimizados para cada modelo base
- **Modelos Base:** 7 variações de XGBRegressor com diferentes hiperparâmetros

O modelo vencedor utiliza uma estratégia de ensemble que combina predições de múltiplos modelos XGBoost, cada um otimizado com diferentes configurações de:
- Learning rate (0.3 a 0.5)
- Max depth (3 a 9)
- Colsample_bytree (0.5 a 1.0)
- Subsample (0.5 a 1.0)

Resultado da Execução do Automated ML:

> **Nota:** Adicionar screenshot da tabela de modelos do Automated ML, destacando o modelo vencedor VotingEnsemble

### 3. Avaliação e Registro do Modelo (MLflow)

O modelo vencedor (VotingEnsemble) foi escolhido para o deployment. Todos os modelos e suas métricas foram automaticamente registrados no Azure ML Model Registry — que utiliza o MLflow para rastreamento.

**Insights e Comparação:**

| Aspecto | AutoML (Vencedor) | Designer |
|---------|-------------------|----------|
| **Precisão** | ⭐ Maior - VotingEnsemble com múltiplos XGBoost otimizados | Boa - Regressão Linear tradicional |
| **Complexidade** | Alta - Ensemble de 7 modelos | Baixa - Modelo único interpretável |
| **Tempo de Desenvolvimento** | ⚡ Rápido - Otimização automática | Médio - Configuração manual |
| **Interpretabilidade** | Moderada - Ensemble complexo | ⭐ Alta - Relação linear clara |
| **Auditoria** | Requer análise técnica | ⭐ Visual e intuitivo |
| **Uso Recomendado** | ✅ Produção (máxima precisão) | Prototipagem e análise exploratória |

**Gerenciamento do Modelo Escolhido:**

O modelo VotingEnsemble foi registrado com:
- **Métricas de Avaliação:** R² score, RMSE, MAE, e outras métricas de regressão
- **Validação Cruzada:** 10-fold cross-validation (dataset < 1000 amostras)
- **Rastreamento:** MLflow integrado ao Azure ML

> **Nota:** Adicionar screenshot da página do Modelo Registrado no Azure ML Studio, mostrando as métricas finais e a data de registro

## 🌐 Implementação em Tempo Real (Deployment)

O modelo VotingEnsemble foi implantado como um **Managed Online Endpoint** do Azure, fornecendo uma API REST para consultas de previsão de vendas em tempo real.

**Teste de Previsão em Tempo Real:**

Ao fornecer uma temperatura (ex: 32°C), o Endpoint retorna instantaneamente a previsão de unidades de sorvete a serem vendidas, permitindo que a Gelato Mágico ajuste sua produção.

**Exemplo de Requisição:**
```json
{
  "Temperatura": 32
}
```

**Exemplo de Resposta:**
```json
{
  "Vendas_Previstas": 155
}
```

> **Nota:** Adicionar screenshot da aba 'Test' do Real-Time Endpoint, mostrando o input de temperatura e o output de vendas previsto

## ✅ Conclusão e Próximos Passos

Este projeto demonstra a capacidade de utilizar as ferramentas de MLOps em Nuvem (Azure ML) para resolver problemas de negócio de forma eficiente, comprovando a proficiência em ambas as abordagens: o controle granular do Designer e a otimização rápida do Automated ML.

**Resultados Alcançados:**
- ✅ Pipeline de treinamento visual criado no Azure ML Designer
- ✅ Otimização automática com AutoML resultando em VotingEnsemble (7 modelos XGBoost)
- ✅ Modelo registrado no Azure ML Model Registry com rastreamento MLflow
- ✅ Deployment em produção via Managed Online Endpoint

**Benefícios para a Gelato Mágico:**
- 📈 Otimização de estoque baseada em previsões precisas
- 💰 Maximização de lucros evitando falta ou excesso de produto
- ⚡ Previsões em tempo real via API REST
- 🎯 Planejamento de produção baseado em dados meteorológicos

**Próximos Passos:**
1. Adicionar monitoramento de drift do modelo em produção
2. Implementar retreinamento automático com novos dados
3. Expandir features incluindo sazonalidade e eventos especiais
4. Criar dashboard de visualização para análise de tendências
