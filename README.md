🍦 Previsão Inteligente de Vendas de Sorvete (Gelato Mágico) com Azure ML Designer & Auto ML
🚀 Resumo do Projeto
Este projeto demonstra a aplicação de Machine Learning para a otimização de produção e estoque da sorveteria Gelato Mágico, onde as vendas são fortemente correlacionadas com a temperatura diária.

Para garantir a melhor precisão e demonstrar proficiência em MLOps na nuvem, exploramos duas abordagens distintas dentro do Azure Machine Learning:

Azure ML Designer: Criação visual (low-code) de um pipeline de regressão.

Automated ML (AutoML): Uso da ferramenta de otimização para encontrar o melhor modelo, hyperparâmetros e feature engineering automaticamente.

O projeto foi concluído com o deployment do modelo vencedor em um Real-Time Endpoint, garantindo previsões instantâneas para o planejamento diário.

🎯 Objetivos Chave
Desenvolver um Modelo de Regressão para prever vendas com base na temperatura.

Comparar e Implementar Pipelines usando Designer e Automated ML.

Gerenciar o Modelo com o registro integrado do Azure ML / MLflow.

Implementar o Modelo em um Real-Time Endpoint para previsões em produção (nuvem).

🛠️ Tecnologias e Ferramentas
Categoria	Ferramenta	Uso no Projeto
Plataforma MLOps	Azure Machine Learning	Orquestração de pipeline, registro e deployment.
Modelagem 1	Azure ML Designer	Criação visual (drag-and-drop) do pipeline de treinamento.
Modelagem 2	Automated ML	Otimização automática de algoritmos (Regressão) e hyperparâmetros.
Modelo ML	Regressão Linear / Vencedor do AutoML	Algoritmos testados para prever um valor contínuo (Vendas).

Exportar para as Planilhas
📂 Estrutura do Repositório
🍦-previsao-vendas-sorvete-designer-ml/
├── inputs/
│   └── dados_vendas_temperatura.csv    <- Dataset histórico (Temperatura, Vendas)
├── docs/
│   ├── designer_pipeline_treinamento.png   <- Screenshot do Pipeline de Treinamento
│   ├── automl_melhor_modelo.png            <- Screenshot dos resultados do Automated ML
│   ├── modelo_registrado_metricas.png      <- Screenshot das métricas no Azure ML
│   └── endpoint_teste_real_time.png        <- Screenshot da previsão em tempo real
├── README.md                               <- Este documento
└── .gitignore
📊 Processo MLOps no Azure ML: Duas Abordagens
O projeto seguiu um fluxo MLOps completo, explorando duas maneiras de treinar o modelo, o que permitiu uma comparação direta de desempenho e esforço.

1. Abordagem 1: Pipeline de Treinamento (Azure ML Designer)
O pipeline de treinamento inicial foi construído visualmente no Designer. Essa abordagem forneceu controle total sobre cada etapa (divisão de dados, seleção do algoritmo de Regressão Linear e avaliação).

Visão do Pipeline de Treinamento (Designer):

[print 1 aqui: Screenshot do Pipeline de Treinamento no Azure ML Designer]

2. Abordagem 2: Otimização Automática (Automated ML)
Para garantir que o melhor algoritmo fosse selecionado, submetemos o mesmo conjunto de dados ao Automated ML (AutoML), configurando-o para resolver um problema de Regressão.

O AutoML: Testou múltiplos algoritmos (ex: LightGBM Regressor) e fez o ajuste fino (hyperparameter tuning) automaticamente.

Vencedor do AutoML:

Melhor Algoritmo: [Nome do Algoritmo Vencedor, ex: LightGBM Regressor]

Melhor Métrica: [Valor do R2, ex: 0.992]

Resultado da Execução do Automated ML:

[print 2 aqui: Screenshot da tabela de modelos do Automated ML, destacando o modelo vencedor]

3. Avaliação e Registro do Modelo (MLflow)
O modelo vencedor foi o escolhido para o deployment. Todos os modelos e suas métricas foram automaticamente registrados no Azure ML Model Registry — que utiliza o MLflow para rastreamento.

Insights e Comparação: A [Abordagem Vencedora, ex: AutoML] geralmente forneceu um modelo mais preciso (maior R²). A [Abordagem Perdedora, ex: Designer] forneceu um processo mais transparente e fácil de auditar visualmente.

Gerenciamento do Modelo Escolhido:

[print 3 aqui: Screenshot da página do Modelo Registrado no Azure ML Studio, mostrando as métricas finais e a data de registro]

🌐 Implementação em Tempo Real (Deployment)
O modelo final e mais preciso foi implantado como um Managed Online Endpoint do Azure, fornecendo uma API REST para consultas de previsão de vendas em tempo real.

Teste de Previsão em Tempo Real: Ao fornecer uma temperatura (ex: 32°C), o Endpoint retorna instantaneamente a previsão de unidades de sorvete a serem vendidas, permitindo que a Gelato Mágico ajuste sua produção.

[print 4 aqui: Screenshot da aba 'Test' do Real-Time Endpoint, mostrando o input de temperatura e o output de vendas previsto]

✅ Conclusão e Próximos Passos
Este projeto demonstra a capacidade de utilizar as ferramentas de MLOps em Nuvem (Azure ML) para resolver problemas de negócio de forma eficiente, comprovando a proficiência em ambas as abordagens: o controle granular do Designer e a otimização rápida do Automated ML.

O modelo implantado garantirá a Gelato Mágico a otimização de seu estoque, maximizando lucros e reduzindo perdas.
