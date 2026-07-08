# 🗄️ Laboratório AWS - Amazon DynamoDB com Índices Secundários (LSI e GSI)

##  Sobre o laboratório

Neste laboratório foi criada uma tabela no **Amazon DynamoDB** utilizando chave de partição e chave de classificação, além da implementação de **Local Secondary Index (LSI)** e **Global Secondary Index (GSI)** para otimizar diferentes tipos de consultas.

Também foram realizadas inserções de dados manualmente pelo Console AWS e em lote utilizando o **AWS CloudShell**, permitindo comparar a eficiência entre operações de **Scan** e **Query**.

---

##  Objetivos

- Criar uma tabela no Amazon DynamoDB;
- Configurar chave de partição e chave de classificação;
- Criar um índice secundário local (LSI);
- Criar um índice secundário global (GSI);
- Inserir dados manualmente e via CloudShell;
- Comparar consultas utilizando Scan e Query;
- Avaliar o impacto dos índices na performance das consultas.

---

##  Serviços utilizados

- Amazon DynamoDB
- AWS CloudShell
- AWS CLI
- AWS Management Console

---

##  Arquitetura

> <img width="694" height="492" alt="image" src="https://github.com/user-attachments/assets/bf93de93-db30-475d-8e28-d3c1c1a49c7a" />


```text
             AWS CloudShell
                    │
                    ▼
        Importação em lote (AWS CLI)
                    │
                    ▼
             Amazon DynamoDB
                    │
      ┌─────────────┴─────────────┐
      │                           │
      ▼                           ▼
 Local Secondary Index      Global Secondary Index
        (LSI)                     (GSI)
      │                           │
      └─────────────┬─────────────┘
                    ▼
             Consultas Otimizadas
```

---

#  Etapas realizadas

## 1. Criação da tabela

Foi criada uma tabela no Amazon DynamoDB contendo:

| Configuração | Valor |
|--------------|-------|
| Chave de partição | ID do Usuário |
| Chave de classificação | Data do Pedido |
| Classe | DynamoDB Standard |
| Capacidade | Provisionada |

Também foram configuradas unidades provisionadas de leitura e gravação.

<img width="1290" height="491" alt="image" src="https://github.com/user-attachments/assets/c69a6953-db5d-4d35-8984-d9316ce8295f" />


---

## 2. Criação do índice secundário local (LSI)

Foi criado um **Local Secondary Index (LSI)** utilizando:

- Chave de classificação: **Status**
- Projeção: **All**

Esse índice permite realizar consultas utilizando a mesma chave de partição da tabela principal com diferentes critérios de ordenação.

<img width="693" height="220" alt="image" src="https://github.com/user-attachments/assets/5ad3c93c-f21b-46ee-8638-e46b00cd36d7" />


---

## 3. Inserção manual de dados

Foi inserido um pedido manualmente utilizando o Console AWS.

O item contém atributos simples e compostos, incluindo:

- Endereço (Map)
- Tags (List)
- Status
- ValorTotal

<img width="1292" height="495" alt="image" src="https://github.com/user-attachments/assets/8d963b7e-ec41-4102-b5af-a46c652fd6ca" />


---

## 4. Importação em lote utilizando CloudShell

Foi realizado o upload do arquivo JSON para o AWS CloudShell.

Em seguida foi utilizada a AWS CLI para importar diversos registros para a tabela através do comando:

```bash
aws dynamodb batch-write-item --request-items file://pedidos_import.json
```

Após a importação, os registros foram validados no Console do DynamoDB.

<img width="743" height="224" alt="image" src="https://github.com/user-attachments/assets/d5bd5375-8304-412a-84e3-e3b1ed8a6f05" />


<img width="681" height="463" alt="image" src="https://github.com/user-attachments/assets/8da9a091-5102-4b8c-9c97-138ad9caa78b" />


---

## 5. Comparação entre Scan e Query

Foram realizados testes utilizando duas estratégias de consulta:

### Scan

Realiza a leitura de toda a tabela para localizar os registros.

Resultado:

- Baixa eficiência
- Maior consumo de recursos

<img width="710" height="435" alt="image" src="https://github.com/user-attachments/assets/97896319-170b-42ec-9603-b316cb37f77e" />


---

### Query

Consulta diretamente utilizando a chave de partição.

Resultado:

- Alta eficiência
- Menor consumo de recursos

<img width="696" height="433" alt="image" src="https://github.com/user-attachments/assets/693ba609-1dfa-4cc3-8c4e-29a25d65e957" />


---

## 6. Consultas utilizando o LSI

Foi utilizada uma consulta baseada no índice secundário local para localizar pedidos de um usuário específico filtrando pelo atributo **Status**.

Também foram aplicados filtros adicionais utilizando o atributo **ValorTotal**.

<img width="712" height="447" alt="image" src="https://github.com/user-attachments/assets/9cd0062f-7cc9-4cf6-b737-5c39e238fe33" />


---

## 7. Criação do índice secundário global (GSI)

Foi criado um **Global Secondary Index (GSI)** utilizando:

| Chave | Valor |
|--------|-------|
| Partition Key | Status |
| Sort Key | ValorTotal |

Esse índice permite consultas utilizando uma chave de partição diferente da tabela principal.

<img width="697" height="425" alt="image" src="https://github.com/user-attachments/assets/ee702147-5b33-48db-ab4b-c0cde4793d0c" />


---

## 8. Consulta utilizando o GSI

Após a criação do índice, foram realizadas consultas utilizando:

- Status = Entregue
- ValorTotal ≥ 60

Os resultados demonstraram consultas eficientes utilizando o índice global.

<img width="685" height="489" alt="image" src="https://github.com/user-attachments/assets/3d578407-394b-463a-a364-2419e1055355" />


---

#  Resultado

Ao final do laboratório foi construída uma tabela NoSQL utilizando índices secundários locais e globais para otimizar diferentes padrões de acesso aos dados.

Também foi possível importar dados em lote via CloudShell e comparar o desempenho entre operações de Scan e Query.

---

##  Comparação entre Scan, Query, LSI e GSI

| Operação | Característica |
|----------|----------------|
| **Scan** | Percorre toda a tabela, consumindo mais capacidade de leitura. |
| **Query** | Consulta apenas os itens que correspondem à chave informada, sendo muito mais eficiente. |
| **LSI** | Permite consultas alternativas utilizando a mesma chave de partição da tabela. |
| **GSI** | Permite criar novos padrões de consulta utilizando uma chave de partição diferente da tabela principal. |

---

#  Boas práticas

Durante o laboratório foram explorados conceitos importantes para modelagem de bancos NoSQL:

- modelagem baseada em padrões de acesso;
- utilização de índices para otimização de consultas;
- importação em lote utilizando AWS CLI;
- comparação entre Scan e Query;
- utilização adequada de capacidade provisionada;
- organização de atributos simples e compostos.

---

#  Aprendizados

Este laboratório permitiu compreender como estruturar uma tabela no Amazon DynamoDB considerando diferentes formas de consulta.

Também foi possível visualizar, na prática, como os índices secundários locais (LSI) e globais (GSI) melhoram o desempenho das consultas e reduzem o consumo de recursos quando comparados às operações de varredura completa da tabela.

---

##  Competências desenvolvidas

- Amazon DynamoDB
- Modelagem NoSQL
- Local Secondary Index (LSI)
- Global Secondary Index (GSI)
- AWS CloudShell
- AWS CLI
- Batch Write
- Scan
- Query
- Modelagem baseada em padrões de acesso
- Banco de dados NoSQL

---
