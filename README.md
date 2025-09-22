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

## Criação do Banco de Dados

Escolhi o [Neon](https://neon.com/) para testar criar um banco de dados para o projeto. Usei a minha conta GitHub no cadastro. E, ao entrar, criei um projeto, selecionando a última versão Postgres (17), escolhendo AWS como servidor de nuvem e a região AWS US East 1, N. Virginia.


<img width="1335" height="739" alt="image" src="https://github.com/user-attachments/assets/106be05c-e679-4f5e-a024-5c797cb369fc" />

Com o novo projeto pronto, ignorei o banco de dados padrão e criei um personalizado no *Editor SQL* do [Neon](https://neon.com/).

```
CREATE DATABASE historydb;
```

## Criação de Schemas

Estruturei o banco para que os schemas seguissem a lógica "medalhão". Portanto, criei três schemas em "historydb":
1. *bronze*: schema destino dos dados brutos ingeridos manualmente, via CSV, JSON ou outras fontes. Funciona como um data lake.
2. *silver*: schema que armazenará as tabelas com dados limpos e transformados.
3. *gold*: schema onde serão salvas views, tabelas com métricas calculadas e dados prontos para uso em visualização. Isto é, funcionará como um data warehouse.

Código PostgreSQL:

```
CREATE SCHEMA bronze;

CREATE SCHEMA silver;

CREATE SCHEMA gold;
```

Neon console:

<img width="1038" height="536" alt="image" src="https://github.com/user-attachments/assets/7877da18-4914-4e47-9f3d-42a66287f6cf" />


