# Sistema de Inscrição em Eventos

Este sistema foi projetado para gerenciar a inscrição de participantes em eventos. Ele permite registrar eventos, participantes e as inscrições feitas para esses eventos. O sistema pode ser utilizado em diversos tipos de eventos, como conferências, shows, seminários e muito mais.

## Estrutura do Banco de Dados

O banco de dados é composto por 3 tabelas principais:

### 1. **Tabela de Eventos (`eventos`)**
Esta tabela armazena as informações sobre os eventos que estão sendo organizados.

- **id_evento**: Identificador único do evento (chave primária).
- **nome_evento**: Nome do evento.
- **data_evento**: Data em que o evento ocorrerá.
- **local_evento**: Local onde o evento será realizado.
- **descricao_evento**: Descrição detalhada sobre o evento (opcional).
- **preco_evento**: Preço do ingresso para o evento.

### 2. **Tabela de Participantes (`participantes`)**
Esta tabela armazena informações sobre as pessoas que se inscrevem nos eventos.

- **id_participante**: Identificador único do participante (chave primária).
- **nome_participante**: Nome do participante.
- **email_participante**: E-mail de contato do participante.
- **telefone_participante**: Número de telefone do participante.
- **idade_participante**: Idade do participante (opcional).
- **empresa_participante**: Nome da empresa do participante (opcional).

### 3. **Tabela de Inscrições (`inscricoes`)**
Esta tabela registra as inscrições dos participantes nos eventos. Cada inscrição está associada a um participante e a um evento específico.

- **id_inscricao**: Identificador único da inscrição (chave primária).
- **id_participante**: Identificador do participante (chave estrangeira referenciando a tabela `participantes`).
- **id_evento**: Identificador do evento (chave estrangeira referenciando a tabela `eventos`).
- **data_inscricao**: Data e hora em que a inscrição foi realizada (automáticamente registrada).

## Funcionalidades

### 1. **Cadastro de Eventos**
Os eventos são cadastrados na tabela `eventos`, com informações como nome, data, local, descrição e preço. Isso permite que os organizadores publiquem detalhes sobre os eventos, incluindo o preço dos ingressos.

### 2. **Cadastro de Participantes**
A tabela `participantes` armazena os dados dos participantes, como nome, e-mail, telefone e empresa, além da idade, que pode ser opcional. Cada participante pode se inscrever em um ou mais eventos.

### 3. **Inscrição em Eventos**
Os participantes podem se inscrever em eventos através da tabela `inscricoes`. Cada inscrição vincula um participante a um evento específico e registra a data e hora da inscrição.

### 4. **Consulta e Acompanhamento de Inscrições**
O sistema permite acompanhar as inscrições realizadas pelos participantes, identificando os eventos em que estão inscritos e os dados dos participantes.

## Exemplo de Uso

### Inserindo Eventos

```sql
INSERT INTO eventos (nome_evento, data_evento, local_evento, descricao_evento, preco_evento)
VALUES ('Conferência de Tecnologia', '2023-09-01', 'Centro de Convenções', 'Uma conferência para discutir as últimas tendências em tecnologia', 250.00);

INSERT INTO eventos (nome_evento, data_evento, local_evento, descricao_evento, preco_evento)
VALUES ('Show de Rock', '2023-07-15', 'Estádio de Futebol', 'Um show de rock com bandas famosas', 80.00);
```

### Inserindo Participantes

```sql
INSERT INTO participantes (nome_participante, email_participante, telefone_participante, idade_participante, empresa_participante)
VALUES ('João Silva', 'joao.silva@email.com', '(11) 99999-9999', 32, 'Empresa X');

INSERT INTO participantes (nome_participante, email_participante, telefone_participante, idade_participante, empresa_participante)
VALUES ('Maria Souza', 'maria.souza@email.com', '(21) 99999-9999', 28, '');
```

### Inserindo Inscrições

```sql
INSERT INTO inscricoes (id_participante, id_evento, data_inscricao)
VALUES (1, 1, '2023-08-01 14:30:00');

INSERT INTO inscricoes (id_participante, id_evento, data_inscricao)
VALUES (2, 2, '2023-06-15 10:00:00');
```

## Como Funciona

### 1. **Cadastro de Eventos**
Os eventos são registrados com informações completas sobre o nome, data, local, descrição e preço. Por exemplo, uma "Conferência de Tecnologia" pode ser registrada com um preço de R$ 250,00 para os ingressos.

### 2. **Cadastro de Participantes**
Cada participante se registra com informações pessoais, incluindo seu nome, e-mail, telefone, idade e, opcionalmente, o nome da empresa onde trabalha. Isso permite que os organizadores tenham todos os dados de contato necessários para comunicação.

### 3. **Inscrição em Eventos**
Os participantes podem se inscrever em eventos. Cada inscrição registra o vínculo entre o participante e o evento escolhido, juntamente com a data e hora da inscrição. Isso possibilita acompanhar os participantes de cada evento.

### 4. **Controle de Inscrições**
Com o uso das tabelas `inscricoes` e `participantes`, é possível acompanhar as inscrições em tempo real, verificando os participantes registrados para um evento específico, ou listando os eventos em que um determinado participante se inscreveu.

## Consultas Comuns

### Consultar Todos os Eventos

```sql
SELECT * FROM eventos;
```

### Consultar Participantes Inscritos em um Evento

```sql
SELECT p.nome_participante, p.email_participante, p.telefone_participante
FROM participantes p
JOIN inscricoes i ON p.id_participante = i.id_participante
WHERE i.id_evento = 1; -- Exemplo para o evento com id_evento = 1
```

### Consultar Todos os Eventos em que um Participante Está Inscrito

```sql
SELECT e.nome_evento, e.data_evento, e.local_evento
FROM eventos e
JOIN inscricoes i ON e.id_evento = i.id_evento
WHERE i.id_participante = 1; -- Exemplo para o participante com id_participante = 1
```

## Conclusão

Este sistema de inscrição de eventos oferece uma solução simples e eficiente para a gestão de eventos e suas respectivas inscrições. Ele permite que os organizadores publiquem eventos, cadastrem participantes e acompanhem as inscrições realizadas, facilitando a administração e a comunicação com os participantes. Ideal para conferências, shows, workshops e outros tipos de eventos.
