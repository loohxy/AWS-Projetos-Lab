# 🛒 Laboratório AWS - Aplicação CRUD Serverless com Amazon DynamoDB, AWS Lambda, API Gateway e Amazon S3

## 📖 Sobre o laboratório

Neste laboratório foi desenvolvida uma aplicação **CRUD (Create, Read, Update e Delete)** utilizando uma arquitetura **serverless** na AWS.

A solução combina um frontend estático hospedado no **Amazon S3**, uma API HTTP criada no **Amazon API Gateway**, uma função **AWS Lambda** escrita em Python para processamento das requisições e uma tabela **Amazon DynamoDB** para persistência dos dados.

Também foram configurados monitoramento e registros de acesso utilizando **Amazon CloudWatch Logs**, permitindo acompanhar tanto as execuções da função Lambda quanto as chamadas realizadas à API.

---

## 🎯 Objetivos

- Criar uma IAM Role para execução da função Lambda;
- Criar uma tabela Amazon DynamoDB;
- Desenvolver uma função Lambda em Python;
- Integrar a Lambda ao DynamoDB;
- Criar uma API HTTP utilizando Amazon API Gateway;
- Hospedar o frontend no Amazon S3;
- Configurar CORS para comunicação entre frontend e API;
- Habilitar monitoramento utilizando Amazon CloudWatch Logs;
- Validar todas as operações CRUD da aplicação.

---

## 🛠️ Serviços utilizados

- Amazon DynamoDB
- AWS Lambda
- Amazon API Gateway
- Amazon S3
- Amazon CloudWatch Logs
- AWS IAM
- Python (Boto3)
- JavaScript

---

## 🏗️ Arquitetura

> <img width="751" height="514" alt="image" src="https://github.com/user-attachments/assets/c0eb6f65-616c-4b45-bf65-12d278bb8102" />


```text
              Usuário
                  │
                  ▼
        Website (Amazon S3)
                  │
          Requisições HTTP
                  │
                  ▼
         Amazon API Gateway
                  │
                  ▼
             AWS Lambda
                  │
                  ▼
         Amazon DynamoDB

          ▲
          │
CloudWatch Logs
(API Gateway + Lambda)
```

---

# 🚀 Etapas realizadas

## 1. Criação da IAM Role

Foi criada uma Role específica para execução da função Lambda.

Foram atribuídas permissões para:

- AWSLambdaBasicExecutionRole
- AmazonDynamoDBFullAccess

📷 *Inserir print da Role criada.*

---

## 2. Criação da tabela DynamoDB

Foi criada uma tabela Amazon DynamoDB para armazenamento dos produtos.

Configuração utilizada:

| Configuração | Valor |
|--------------|-------|
| Nome | Produtos |
| Chave de Partição | id (String) |

📷 *Inserir print da tabela criada.*

---

## 3. Desenvolvimento da função Lambda

Foi criada uma função Lambda utilizando Python 3.12.

Foram realizadas as seguintes configurações:

- upload do código da aplicação;
- configuração do Handler;
- associação da tabela DynamoDB;
- memória de 256 MB;
- timeout de 10 segundos.

📷 *Inserir print da função Lambda.*

---

## 4. Criação da API Gateway

Foi criada uma API HTTP integrada à função Lambda.

Foram configuradas as rotas:

| Método | Endpoint |
|---------|----------|
| POST | /produtos |
| GET | /produtos |
| GET | /produtos/{id} |
| PUT | /produtos/{id} |
| DELETE | /produtos/{id} |

📷 *Inserir print das rotas da API.*

---

## 5. Hospedagem do frontend

Foi criado um bucket Amazon S3 para hospedagem da aplicação.

Foram enviados os arquivos:

- index.html
- style.css
- script.js

Também foram configurados:

- Static Website Hosting;
- Bucket Policy;
- Permissões públicas para leitura dos arquivos.

📷 *Inserir print do bucket.*

📷 *Inserir print da hospedagem estática.*

---

## 6. Configuração da integração

Foi configurada a URL do API Gateway no frontend.

Também foi habilitado o **CORS** para permitir a comunicação entre o site hospedado no S3 e a API.

📷 *Inserir print da configuração do CORS.*

---

## 7. Cadastro de produtos

A aplicação foi utilizada para cadastrar produtos.

As operações realizadas incluíram:

- cadastro;
- consulta;
- edição;
- exclusão.

Os dados passaram a ser armazenados automaticamente na tabela DynamoDB.

📷 *Inserir print da aplicação funcionando.*

---

## 8. Validação no DynamoDB

Após os cadastros realizados pela aplicação, foi possível visualizar todos os produtos diretamente na tabela DynamoDB.

Essa etapa confirmou a integração entre API Gateway, Lambda e DynamoDB.

📷 *Inserir print dos itens na tabela.*

---

## 9. Monitoramento

Foram analisados dois grupos de logs:

- Logs da função Lambda;
- Logs do API Gateway.

Os registros permitiram acompanhar as chamadas HTTP e as execuções da função.

📷 *Inserir print do grupo de logs da Lambda.*

📷 *Inserir print do grupo de logs da API.*

---

# 📊 Resultado

Ao final do laboratório foi implantada uma aplicação CRUD totalmente serverless utilizando serviços gerenciados da AWS.

O frontend hospedado no Amazon S3 passou a consumir uma API criada no Amazon API Gateway, responsável por acionar uma função AWS Lambda para realizar operações de criação, leitura, atualização e exclusão de produtos armazenados no Amazon DynamoDB.

Todo o fluxo foi monitorado por meio do Amazon CloudWatch Logs.

---

## 🏛️ Papel de cada serviço na arquitetura

| Serviço | Papel na solução |
|----------|------------------|
| **Amazon S3** | Hospeda o frontend estático da aplicação. |
| **Amazon API Gateway** | Expõe os endpoints HTTP e encaminha as requisições para a Lambda. |
| **AWS Lambda** | Implementa a lógica de negócio e executa as operações CRUD. |
| **Amazon DynamoDB** | Armazena os dados dos produtos em um banco NoSQL. |
| **Amazon CloudWatch Logs** | Centraliza os logs das chamadas da API e das execuções da Lambda. |
| **AWS IAM** | Controla as permissões necessárias para execução da aplicação. |

---

## 🔄 Fluxo da aplicação

| Serviço | Responsabilidade |
|---------|------------------|
| **Amazon S3** | Hospeda a interface web da aplicação. |
| **Amazon API Gateway** | Recebe as requisições HTTP do frontend. |
| **AWS Lambda** | Processa as operações CRUD em Python. |
| **Amazon DynamoDB** | Armazena os produtos cadastrados. |
| **Amazon CloudWatch Logs** | Monitora as execuções da API e da Lambda. |

---

## 🌐 Fluxo da arquitetura

```text
Usuário
     │
     ▼
Frontend (S3)
     │
     ▼
API Gateway
     │
     ▼
AWS Lambda
     │
     ▼
Amazon DynamoDB

CloudWatch Logs
     ▲
     │
 API Gateway e Lambda
```

---

## 💡 Boas práticas

Durante o laboratório foram aplicados conceitos importantes para aplicações serverless:

- utilização de IAM Roles específicas;
- separação entre frontend e backend;
- comunicação via API REST;
- integração entre Lambda e DynamoDB;
- armazenamento de dados NoSQL;
- hospedagem de sites estáticos;
- configuração de CORS;
- monitoramento centralizado através do CloudWatch Logs.

---

# 📚 Aprendizados

Este laboratório permitiu compreender como construir uma aplicação CRUD totalmente serverless utilizando serviços gerenciados da AWS.

Foi possível integrar frontend, API, processamento e banco de dados sem necessidade de provisionar servidores, além de acompanhar todo o fluxo da aplicação por meio dos logs do Amazon CloudWatch.

---

## 🧠 Competências desenvolvidas

- Amazon S3
- Amazon API Gateway
- AWS Lambda
- Amazon DynamoDB
- Amazon CloudWatch Logs
- AWS IAM
- Python
- JavaScript
- Arquitetura Serverless
- CRUD
- API REST
- CORS
- Integração entre serviços AWS

---

