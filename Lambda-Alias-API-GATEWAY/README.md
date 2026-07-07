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

> *(Inserir aqui o diagrama da arquitetura utilizado no laboratório.)*

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

📷 *Inserir print da criação da função.*

---

## 2. Teste da função Lambda

Foi criado um evento de teste simulando uma requisição do API Gateway para validar a execução da função antes da publicação das versões.

📷 *Inserir print do teste realizado.*

---

## 3. Publicação da versão de Desenvolvimento

Após validar a função, foi publicada a **Versão 1** da Lambda.

Em seguida foi criado o Alias:

- **dev**

que passou a apontar para essa versão.

📷 *Inserir print da publicação da versão.*

📷 *Inserir print do Alias dev.*

---

## 4. Publicação da versão de Produção

O código da função foi atualizado representando o ambiente de produção.

Após o deploy foi publicada a **Versão 2** da função.

Em seguida foi criado o Alias:

- **prod**

associado à nova versão.

📷 *Inserir print da versão 2.*

📷 *Inserir print do Alias prod.*

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

📷 *Inserir print da API.*

---

## 6. Configuração dos ambientes

Foram criados dois ambientes (Stages):

| Stage | Alias Lambda |
|--------|--------------|
| Desenvolvimento | dev |
| Produção | prod |

Cada Stage foi configurado para invocar o Alias correspondente da função Lambda.

📷 *Inserir print do Stage Desenvolvimento.*

📷 *Inserir print do Stage Produção.*

---

## 7. Validação

Foram realizados testes utilizando as URLs geradas pelo API Gateway.

O endpoint de **Desenvolvimento** retornou a versão vinculada ao Alias **dev**, enquanto o endpoint de **Produção** retornou a versão associada ao Alias **prod**, confirmando o correto direcionamento entre os ambientes.

📷 *Inserir print do retorno do ambiente Desenvolvimento.*

📷 *Inserir print do retorno do ambiente Produção.*

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
