# Desenvolvimento com FlayWay (ORM <-> Banco de Dados Relacional)


Flyway ajuda a versionar mudanças em banco de dados e automatizar implantações seguras de maneira simples.

![Flyway Exemplo](https://documentation.red-gate.com/fd/files/184127223/277579479/1/1737023775254/EmptyDb.png)

O cenário inicial no uso do Flyway é um banco de dados vazio. 

## Histórico de Tabelas com Flyway

O Flyway mantém um controle rigoroso do histórico de mudanças no banco de dados através de uma tabela especial chamada `flyway_schema_history`.

### Como Funciona o Controle de Versão

Quando você executa o Flyway pela primeira vez, ele cria automaticamente a tabela `flyway_schema_history` que armazena:

- **version**: Número da versão do script
- **description**: Descrição da migração
- **type**: Tipo da migração (SQL, Java, etc.)
- **script**: Nome do arquivo de migração
- **checksum**: Hash do conteúdo do script
- **installed_by**: Usuário que executou a migração
- **installed_on**: Data e hora da execução
- **execution_time**: Tempo de execução em milissegundos
- **success**: Se a migração foi executada com sucesso

### Estrutura dos Arquivos de Migração

Os scripts seguem uma convenção de nomenclatura:
```
V1__Create_person_table.sql
V2__Add_people_table.sql
V3__Add_index_to_people.sql
```

![Flyway Schema](https://documentation.red-gate.com/fd/files/184127223/277579480/1/1737023800879/EmptySchemaVersion.png)

Esta tabela é usada para manter as mudanças de banco.

### Como o Flyway Aplica as Migrações

O Flyway irá escanear o sistema de arquivos ou o classpath da aplicação em busca de migrações. Elas podem ser escritas em SQL, Java, ou outras linguagens de script.

As migrações são aplicadas em ordem baseada em seu número de versão:

![Migration Process](https://documentation.red-gate.com/fd/files/184127223/277579481/1/1737023821565/Migration-1-2.png)