# Segundo cérebro SQL

Base de estudos de [MarcosSlv](https://github.com/MarcosSlv) sobre SQL e bancos de dados relacionais, organizada a partir de perguntas, respostas e materiais fornecidos pelo autor do repositório.

## Tema, objetivo e diretriz

- **Tema:** fundamentos de bancos de dados relacionais e linguagem SQL, com atenção a SQL Server, ferramentas, autenticação e integridade de dados.
- **Objetivo:** reunir explicações, evidências de estudo e referências para consulta e revisão, conectando conceitos a exemplos de consultas.
- **Diretriz:** organizar o conhecimento com rastreabilidade; distinguir o conteúdo fornecido de revisões posteriores; não inventar fontes; publicar somente conteúdo adequado quanto a direitos de uso e privacidade.

Esta formulação de objetivo e diretriz é uma organização editorial para o repositório, baseada no material disponível. Não é uma transcrição de requisitos de curso ou de avaliação.

## NotebookLM

Links fornecidos pelo autor:

- [Caderno de estudos](https://notebook.google.com/notebook/acb551b5-08fc-4bcb-8cc5-cdaa7167e207)
- [Prévia compartilhada](https://notebook.google.com/notebook/acb551b5-08fc-4bcb-8cc5-cdaa7167e207/preview)

O conteúdo e as permissões de acesso desses links não puderam ser confirmados nesta revisão. O acesso pode depender do compartilhamento configurado pelo proprietário. Os links não comprovam licença de redistribuição dos materiais do caderno.

## Três perguntas e respostas fornecidas

As respostas abaixo são versões editadas das respostas fornecidas na conversa de preparação: formatação reorganizada e convites automáticos removidos. As ressalvas técnicas acrescentadas estão identificadas separadamente. Os números entre colchetes foram preservados como marcadores do material original; **suas fontes ainda não foram identificadas**. A numeração reinicia em cada resposta e não constitui uma bibliografia única.

### 1. Quais são os conceitos básicos da linguagem SQL e dos bancos de dados relacionais?

**Resposta fornecida, organizada para estudo:**

Um banco de dados relacional organiza informações em tabelas [1]. Cada tabela contém colunas, que definem os campos ou atributos, e linhas, que representam registros ou tuplas [2][3].

As chaves estabelecem identidade e relacionamentos:

- **Chave primária (PK):** identifica cada registro de forma única, sem duplicidade e sem valor nulo [4].
- **Chave estrangeira (FK):** referencia uma chave de outra tabela e estabelece a integridade referencial [6]. A resposta original descrevia apenas referências a PK; veja a ressalva na pergunta 3.

A **normalização** organiza tabelas para reduzir redundância e evitar anomalias de inserção, atualização e exclusão [9][10]. Entre as formas normais mencionadas estão 1NF, 2NF, 3NF e BCNF [10].

O **SGBD** é o software que gerencia armazenamento, segurança, acesso e processamento dos dados [11]. Os exemplos fornecidos foram PostgreSQL, MySQL, SQL Server, Oracle e SQLite [12][13].

**SQL (Structured Query Language)** é a linguagem usada para definir, consultar e manipular dados relacionais, com padronização internacional associada a ISO e ANSI [14]. A padronização não elimina diferenças entre os dialetos dos SGBDs.

Na classificação didática apresentada, os comandos são agrupados por finalidade [17]:

| Grupo | Finalidade | Comandos e marcadores originais |
| --- | --- | --- |
| DQL | Consulta de dados | `SELECT` [18][19] |
| DML | Manipulação de registros | `INSERT` [20][21], `UPDATE` [21][22], `DELETE` [21][23] |
| DDL | Definição da estrutura | `CREATE` [19], `ALTER` [19][26], `DROP` [19][27] |
| DCL | Controle de acesso | `GRANT`, `REVOKE` [21] |
| TCL | Controle de transações | `COMMIT`, `ROLLBACK` [28][29] |

Estrutura de consulta apresentada [18][30]:

```sql
SELECT coluna_1, coluna_2
FROM tabela
WHERE condicao
ORDER BY coluna_1 ASC;
```

O exemplo é um modelo de sintaxe; depende de uma tabela, colunas e condição reais para execução.

- `SELECT` escolhe as colunas do resultado [18].
- `FROM` indica a origem dos dados [18].
- `WHERE` filtra linhas, por exemplo, `WHERE preco > 100` [18][31].
- `ORDER BY` ordena o resultado em ordem crescente (`ASC`) ou decrescente (`DESC`) [18][32].
- `GROUP BY` agrupa linhas, frequentemente com funções agregadas como `SUM`, `COUNT` e `AVG`; `HAVING` filtra grupos [18][33].
- `JOIN` combina registros de tabelas; foram citados `INNER JOIN` e `LEFT JOIN` [34].

### 2. Converse sobre o que essas fontes dizem de Ferramentas e Autenticação, no contexto mais amplo de SQL Server.

**Resposta fornecida, organizada para estudo:**

No SQL Server, as ferramentas de administração e os mecanismos de autenticação atendem a funções diferentes.

- **SQL Server Management Studio (SSMS):** interface gráfica da Microsoft para administrar instâncias, criar bancos, executar scripts T-SQL, analisar planos de execução e gerenciar objetos [1][2].
- **Database Engine:** serviço responsável pelo armazenamento, processamento de consultas, integridade e gerenciamento de transações [5][6].
- **Ferramentas complementares:** SQL Server Data Tools e SQL Server Reporting Services foram citados no ecossistema [1][5]. dbForge Studio for SQL Server e Redgate SQL Prompt apareceram como exemplos de ferramentas de terceiros [7]. A menção não representa recomendação nem avaliação de versões atuais.

A autenticação valida a identidade de quem tenta se conectar [10][11]. Os modos descritos foram:

| Modo | Funcionamento apresentado |
| --- | --- |
| Autenticação do Windows | Usa a identidade do Windows ou domínio, sem uma senha SQL separada [10][11]. |
| Modo misto | Permite autenticação do Windows e logins do próprio SQL Server, com senha [10][11]. |

A resposta original também mencionava a conta administrativa `sa` [10][11]. **Ressalva técnica acrescentada:** modo misto não significa que essa conta deva ser usada ou habilitada; sua habilitação é uma decisão separada. A [documentação da Microsoft sobre autenticação](https://learn.microsoft.com/en-us/sql/relational-databases/security/choose-an-authentication-mode?view=sql-server-ver17) foi consultada para esta ressalva e não foi identificada como origem dos marcadores antigos.

### 3. Como funcionam as chaves primárias e estrangeiras?

**Resposta fornecida, organizada para estudo:**

Chaves primárias e estrangeiras ajudam a manter a identidade e a consistência dos relacionamentos entre tabelas [1].

**Chave primária (PK):**

- Identifica de forma única cada linha e exige valores não nulos [1].
- Uma tabela pode ter uma única restrição de chave primária, formada por uma coluna ou por várias colunas em conjunto [1][8].
- A resposta mencionou geração automática com `IDENTITY` no SQL Server, `SERIAL`/`IDENTITY` no PostgreSQL e `AUTO_INCREMENT` no MySQL [9]. Esses mecanismos dependem do SGBD; geração automática e chave primária são conceitos distintos.
- A resposta original afirmava que uma PK no SQL Server gera automaticamente um índice clusterizado [12][13]. **Correção técnica acrescentada:** a PK cria um índice único; ele pode ser clusterizado ou não clusterizado. Quando o tipo não é especificado, o padrão é clusterizado se ainda não existir outro índice clusterizado na tabela. Portanto, a afirmação original não vale em todos os casos. Veja a [documentação de restrições PK e FK da Microsoft](https://learn.microsoft.com/en-us/sql/relational-databases/tables/primary-and-foreign-key-constraints?view=sql-server-ver17).

**Chave estrangeira (FK):**

- É uma coluna ou conjunto de colunas que referencia uma chave de outra tabela ou da própria tabela [2].
- A tabela referenciada é chamada de pai e a tabela que contém a FK, de filha [2].
- A restrição impede referências sem correspondência na chave referenciada [2][6]. **Ressalva técnica acrescentada:** a descrição original se limitava a PK; no SQL Server uma FK também pode referenciar uma chave única elegível. Uma FK que permite `NULL` exige considerar esse caso, não descrito na resposta original.
- A resposta apresentou o bloqueio da exclusão de um registro pai com dependências [16] e a possibilidade de ações como `ON DELETE CASCADE` [14][17]. **Ressalva técnica acrescentada:** o comportamento depende da ação configurada; bloqueio corresponde a `NO ACTION`. Cascatas precisam ser escolhidas de acordo com a regra de negócio. Essas ressalvas foram verificadas na documentação da Microsoft vinculada acima.

**Funcionamento em conjunto:**

Na estrutura apresentada, `cliente.cliente_id` é PK [5][21] e `pedido.cliente_id` é FK [5][21]. Armazenar o identificador do cliente em cada pedido permite relacionar os registros sem repetir o nome e o e-mail do cliente em cada compra [22][23]. A resposta associa essa organização à normalização e à recuperação dos dados por junções [4].

Consulta fornecida [18]:

```sql
SELECT pedido.id, cliente.nome, pedido.data_pedido
FROM pedido
INNER JOIN cliente ON pedido.cliente_id = cliente.cliente_id;
```

O exemplo pressupõe tabelas e colunas já criadas; não foi executado contra uma instância de banco de dados nesta preparação.

**Trecho incompleto:** a resposta recebida termina no início de uma seção sobre boas práticas e convenções de nomenclatura. A continuação não foi recuperada e não foi inventada neste README.

## Citações ainda não identificadas

Os marcadores são específicos de cada resposta. Por exemplo, `[1]` da pergunta 1 não pode ser tratado como a mesma fonte de `[1]` da pergunta 2.

| Resposta | Marcadores presentes no texto fornecido | Situação |
| --- | --- | --- |
| Pergunta 1 | [1], [2], [3], [4], [6], [9], [10], [11], [12], [13], [14], [17], [18], [19], [20], [21], [22], [23], [26], [27], [28], [29], [30], [31], [32], [33], [34] | Sem correspondência confirmada com autor, título, URL ou página. |
| Pergunta 2 | [1], [2], [5], [6], [7], [10], [11] | Sem correspondência confirmada com autor, título, URL ou página. |
| Pergunta 3 | [1], [2], [4], [5], [6], [8], [9], [12], [13], [14], [16], [17], [18], [21], [22], [23] | Sem correspondência confirmada com autor, título, URL ou página. |

Para completar a rastreabilidade, é necessário exportar ou registrar, para cada resposta, a relação entre marcador, documento ou página da web e trecho citado. Não se presume que todos os números apontem para o PDF anexado. Os links da Microsoft acrescentados nesta revisão são referências de verificação novas e não substituem a bibliografia ausente.

## Materiais anexados e evidências de estudo

Os cinco anexos foram recuperados e inspecionados. Os caminhos `/mnt/data/Masterclass_SQL.pdf` e `/mnt/data/NotebookLM Mind Map.png`, citados na preparação, identificavam anexos daquela conversa; não são endereços públicos de download.

| Material recebido | O que foi verificado | Decisão para este commit |
| --- | --- | --- |
| `Masterclass_SQL.pdf` | PDF de 15 páginas, revisado visualmente. Não foi identificada uma licença explícita de redistribuição. | Registrado neste inventário; binário não publicado. Autoria, origem e permissão de redistribuição precisam ser confirmadas. |
| `NotebookLM Mind Map.png` | Mapa visual sobre SQL, estrutura relacional e SGBDs, sem dados pessoais aparentes na imagem. A origem das fontes e a autorização de redistribuição não foram comprovadas. | Registrado neste inventário; binário não publicado enquanto os direitos sobre os materiais de origem permanecem pendentes. |
| `image(6).png` | Print da pergunta 1; sem credenciais ou dados pessoais aparentes. | Texto da pergunta incorporado acima; imagem não incluída por repetir o texto. |
| `image(7).png` | Print da pergunta 2; sem credenciais ou dados pessoais aparentes. | Texto da pergunta incorporado acima; imagem não incluída por repetir o texto. |
| `image(8).png` | Print da pergunta 3; sem credenciais ou dados pessoais aparentes. | Texto da pergunta incorporado acima; imagem não incluída por repetir o texto. |

Os prints evidenciam as perguntas formuladas; não comprovam as respostas completas, a bibliografia ou as configurações de compartilhamento do NotebookLM. O inventário não significa que os anexos estejam disponíveis neste repositório.

## Direitos de uso e privacidade

Este commit contém somente este README: a organização editorial do estudo, as respostas fornecidas com as ressalvas indicadas, os links informados e o inventário dos anexos. Não inclui o PDF, o mapa, imagens de interface, exportações integrais da conversa, senhas, tokens ou dados de conexão.

Não foi aplicada uma licença geral ao repositório, pois a titularidade e as permissões dos materiais de terceiros ainda não foram comprovadas. O uso para estudo e a disponibilidade de um link não foram tratados como autorização de redistribuição. A [política de remoção por direitos autorais do GitHub](https://docs.github.com/en/site-policy/content-removal-policies/dmca-takedown-policy) foi consultada nesta revisão; ela não concede uma licença de uso dos anexos.

Antes de incorporar arquivos adicionais, registrar sua origem e licença ou autorização, revisar dados pessoais e credenciais e identificar eventuais fontes de terceiros. Não alterar permissões de compartilhamento do NotebookLM sem uma decisão explícita do proprietário.

## Pendências para ampliar o repositório

- Identificar as fontes de cada marcador das três respostas.
- Confirmar autoria, origem e autorização de redistribuição do PDF e do mapa.
- Conferir o acesso ao NotebookLM com uma sessão sem privilégios do proprietário.
- Recuperar a continuação da terceira resposta, se existir.
- Acrescentar exercícios executáveis com indicação do SGBD e da versão utilizados.

Revisão editorial e de materiais: **22 de outubro de 2026**. Este repositório começa como documentação de estudo; os exemplos SQL ainda não têm validação de execução.
