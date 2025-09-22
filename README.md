# Banco de Dados (História Humana) - Arquitetura Open Source

Nesse projeto, criei um banco de dados pessoal para registrar informações históricas da humanidade (meu hobby), com dados estruturados e semiestruturados, na nuvem e completamente open source.

*Resumo da tecnologia utilizada*

|Função|Ferramenta/Ambiente|
|-------|---------|
|Banco|Neon Postgres Serverless|
|Ingestão|Python no GitHub Codespaces|
|Transformação|dbt|
|Visualização|Apache Superset|
|Versionamento|GitHub|

*O banco foi construído para seguir a estrutura de dados medalhão:*

|Camada|Descrição|
|------|---------|
|Bronze|Ingestão de dados brutos inseridos manualmente, por CSVs, JSON etc.|
|Silver|Dados limpos, com campos padronizados e normalizados, chaves primárias criadas etc.|
|Gold|Criados dados analíticos por meio de agregação de tabelas, de cálculos de métricas etc.|

*E o fluxo de dados pensado inicialmente, foi:*

```
Entrada manual
        ↓ Python (Codespaces)
Schema Bronze – Neon
        ↓ dbt (transformação com PostgreSQL)
Schema Silver – Neon
        ↓ dbt (criar views etc.)
Schema Gold – Neon
        ↓ Apache Superset (visualização)
Dashboards interativos

```
