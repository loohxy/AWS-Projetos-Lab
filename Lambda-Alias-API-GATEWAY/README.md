# 🚀 Laboratório AWS - AWS Lambda com Aliases e API Gateway com Stages

## 📖 Sobre o laboratório

Neste laboratório foi criada uma aplicação serverless utilizando **AWS Lambda** e **Amazon API Gateway**, explorando recursos de versionamento da função Lambda por meio de **Aliases** e a separação de ambientes utilizando **Stages** no API Gateway.

A solução permite que diferentes versões da função sejam disponibilizadas para ambientes distintos, como desenvolvimento e produção, utilizando uma única API e uma única função Lambda.

---

## 🎯 Objetivos

- Criar uma função AWS Lambda em Python;
- Publicar diferentes versões da função Lambda;
- Criar Aliases para representar ambientes distintos;
- Criar uma API REST no Amazon API Gateway;
- Configurar integração Proxy entre API Gateway e Lambda;
- Criar Stages para ambientes de desenvolvimento e produção;
- Associar cada Stage ao Alias correspondente da função Lambda;
- Validar o direcionamento correto das chamadas da API.

---

## 🛠️ Serviços utilizados

- AWS Lambda
- Amazon API Gateway
- AWS IAM
- Python 3.13
- AWS Management Console

---

## 🏗️ Arquitetura

> <img width="738" height="505" alt="image" src="https://github.com/user-attachments/assets/7a6b0c7d-ed79-409b-b0a3-1fa00601dce5" />


```text
                 Cliente
                    │
        ┌───────────┴───────────┐
        │                       │
        ▼                       ▼
API Gateway                API Gateway
Stage: Desenvolvimento     Stage: Produção
        │                       │
        ▼                       ▼
Lambda Alias: dev        Lambda Alias: prod
        │                       │
        ▼                       ▼
Versão 1 da Função       Versão 2 da Função
```

---

# 🚀 Etapas realizadas

## 1. Criação da função Lambda

Foi criada uma função Lambda utilizando **Python 3.13**, compatível com integração Proxy do API Gateway.

O código retorna informações como:

- Ambiente utilizado;
- Versão da função;
- Alias responsável pela execução.

<img width="1292" height="460" alt="image" src="https://github.com/user-attachments/assets/7e5a95b1-9a8c-4b0c-b6d1-653779bd82f4" />


---

## 2. Teste da função Lambda

Foi criado um evento de teste simulando uma requisição do API Gateway para validar a execução da função antes da publicação das versões.

<img width="1289" height="504" alt="image" src="https://github.com/user-attachments/assets/9558e4e5-5c7f-4349-be83-7d5ac8dcd1b2" />


---

## 3. Publicação da versão de Desenvolvimento

Após validar a função, foi publicada a **Versão 1** da Lambda.

Em seguida foi criado o Alias:

- **dev**

que passou a apontar para essa versão.


<img width="1293" height="428" alt="image" src="https://github.com/user-attachments/assets/15b9d52e-d960-4973-af67-9e06478ebacb" />


<img width="1293" height="483" alt="image" src="https://github.com/user-attachments/assets/cb9a2541-9f63-4f40-a03d-dbb1482e73c5" />


---

## 4. Publicação da versão de Produção

O código da função foi atualizado representando o ambiente de produção.

Após o deploy foi publicada a **Versão 2** da função.

Em seguida foi criado o Alias:

- **prod**

associado à nova versão.

<img width="1289" height="434" alt="image" src="https://github.com/user-attachments/assets/9b2c52cc-0877-407c-97f9-ef542efe1bda" />


<img width="1292" height="482" alt="image" src="https://github.com/user-attachments/assets/3b9eada4-9627-49e4-8a44-d13e6f9e7e8a" />


---

## 5. Criação da API REST

Foi criada uma API REST utilizando o Amazon API Gateway.

Em seguida foi criado o recurso:

```
/hello
```

com o método:

```
GET
```

utilizando integração **Lambda Proxy**.

<img width="1292" height="440" alt="image" src="https://github.com/user-attachments/assets/a65cc77a-15ec-42e9-8e90-e864871dc20e" />


---

## 6. Configuração dos ambientes

Foram criados dois ambientes (Stages):

| Stage | Alias Lambda |
|--------|--------------|
| Desenvolvimento | dev |
| Produção | prod |

Cada Stage foi configurado para invocar o Alias correspondente da função Lambda.

<img width="1303" height="476" alt="image" src="https://github.com/user-attachments/assets/4ae9b0bc-bed4-4597-84a5-4fd417ef3b55" />



<img width="1295" height="469" alt="image" src="https://github.com/user-attachments/assets/c966c8b7-b893-49bf-8014-9dfcde3c988e" />


---

## 7. Validação

Foram realizados testes utilizando as URLs geradas pelo API Gateway.

O endpoint de **Desenvolvimento** retornou a versão vinculada ao Alias **dev**, enquanto o endpoint de **Produção** retornou a versão associada ao Alias **prod**, confirmando o correto direcionamento entre os ambientes.

<img width="492" height="195" alt="image" src="https://github.com/user-attachments/assets/f3ecd267-c018-4388-81fd-5c710cee8104" />


<img width="407" height="211" alt="image" src="https://github.com/user-attachments/assets/53a40361-8f57-405c-bb7c-a6655f951629" />


---

# 📊 Resultado

Ao final do laboratório foi implementada uma API serverless utilizando versionamento de funções Lambda e gerenciamento de ambientes através do API Gateway.

Fluxo implementado:

- Cliente acessa o endpoint da API;
- API Gateway identifica o Stage;
- O Stage direciona para o Alias correspondente;
- O Alias aponta para a versão correta da função Lambda;
- A resposta é retornada ao cliente.

---

## 🔄 Relação entre Aliases e Stages

| Recurso | Função |
|---------|---------|
| **Lambda Version** | Representa um snapshot imutável do código da função. |
| **Lambda Alias** | Aponta para uma versão específica da função, facilitando a troca entre versões. |
| **API Gateway Stage** | Representa um ambiente da API (como desenvolvimento ou produção). |
| **Integração** | Cada Stage é configurado para invocar um Alias diferente da função Lambda. |

---

# 💡 Boas práticas

Durante o laboratório foram aplicados conceitos importantes para gerenciamento de aplicações serverless:

- separação entre ambientes de desenvolvimento e produção;
- versionamento de funções Lambda;
- utilização de Aliases para facilitar implantações;
- gerenciamento de APIs através de Stages;
- redução de riscos durante atualizações da aplicação;
- reutilização da mesma API e da mesma função para múltiplos ambientes.

---

# 📚 Aprendizados

Este laboratório permitiu compreender como utilizar o versionamento do AWS Lambda em conjunto com os Stages do Amazon API Gateway para implementar diferentes ambientes de uma aplicação serverless.

Essa abordagem facilita o ciclo de desenvolvimento, testes e implantação, permitindo atualizar versões da aplicação de forma controlada sem impactar imediatamente o ambiente de produção.

---

## 🧠 Competências desenvolvidas

- AWS Lambda
- Amazon API Gateway
- Lambda Versions
- Lambda Aliases
- API Gateway Stages
- Serverless Computing
- REST APIs
- Integração Proxy
- Versionamento de aplicações
- Deploy de múltiplos ambientes

---
