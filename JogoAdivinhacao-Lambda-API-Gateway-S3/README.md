# 🎮 Laboratório AWS - Jogo de Adivinhação com AWS Lambda, API Gateway e Amazon S3

##  Sobre o laboratório

Neste laboratório foi desenvolvida uma aplicação **serverless** utilizando **AWS Lambda**, **Amazon API Gateway** e **Amazon S3** para criar um jogo de adivinhação.

O frontend da aplicação foi hospedado como um site estático no Amazon S3, enquanto o backend foi implementado em uma função AWS Lambda, acessada por meio de uma API HTTP criada no Amazon API Gateway.

Essa arquitetura demonstra como integrar diferentes serviços da AWS para construir aplicações escaláveis sem necessidade de gerenciamento de servidores.

---

##  Objetivos

- Desenvolver a lógica do jogo utilizando AWS Lambda em Python;
- Criar uma API HTTP no Amazon API Gateway;
- Integrar a API à função Lambda;
- Configurar o CORS para comunicação entre frontend e backend;
- Publicar um site estático utilizando Amazon S3;
- Integrar o frontend hospedado no S3 com a API Gateway;
- Validar o funcionamento completo da aplicação.

---

##  Serviços utilizados

- AWS Lambda
- Amazon API Gateway
- Amazon S3
- AWS IAM
- Python 3.13
- HTML
- JavaScript

---

##  Arquitetura

> <img width="617" height="505" alt="image" src="https://github.com/user-attachments/assets/e1072cb0-20ab-4d95-a1ec-ef30e80a2afb" />


```text
              Usuário
                  │
                  ▼
      Website Estático (Amazon S3)
                  │
          Requisição HTTP (GET)
                  │
                  ▼
        Amazon API Gateway
                  │
                  ▼
            AWS Lambda
                  │
      Processamento da lógica
                  │
                  ▼
         Resposta para o usuário
```

---

#  Etapas realizadas

## 1. Criação da função Lambda

Foi criada uma função AWS Lambda utilizando **Python 3.13**, responsável por implementar toda a lógica do jogo de adivinhação.

Após a criação da função, foi realizado o upload do código da aplicação e o deploy para disponibilizar a execução.

<img width="1297" height="470" alt="image" src="https://github.com/user-attachments/assets/b8c46960-b443-4819-9d9b-3e662d2c007b" />


---

## 2. Criação da API HTTP

Foi criada uma API HTTP utilizando o Amazon API Gateway.

Durante a configuração foram definidos:

- Integração com AWS Lambda;
- Método GET;
- Recurso:

```
/jogo
```

Também foi configurado o estágio **prod** para disponibilizar a API.

<img width="1311" height="350" alt="image" src="https://github.com/user-attachments/assets/f602f4e7-51a1-4670-b746-0792e2afc959" />


---

## 3. Configuração do CORS

Foi configurado o CORS da API para permitir que o frontend hospedado no Amazon S3 pudesse realizar chamadas para a API.

Configurações aplicadas:

- Allow-Origin: *
- Allow-Headers: content-type
- Allow-Methods: GET

<img width="1299" height="491" alt="image" src="https://github.com/user-attachments/assets/8c41e15e-6b7f-4794-baef-3b5be7a48bec" />


---

## 4. Configuração do Website Estático

Foi criado um bucket Amazon S3 para hospedagem do frontend.

No arquivo **index.html** foram atualizados:

- URL da API Gateway;
- Caminho do recurso;
- Identificação do projeto.

Após a alteração, o arquivo foi enviado ao bucket.

<img width="1313" height="461" alt="image" src="https://github.com/user-attachments/assets/8932aeb6-f86d-4d65-ab14-84d2e4364a22" />


<img width="1306" height="455" alt="image" src="https://github.com/user-attachments/assets/b8d249a6-27c3-4c08-aa18-2af93ecc2038" />


---

## 5. Habilitação da hospedagem estática

Foi habilitado o recurso **Static Website Hosting** no bucket Amazon S3, definindo:

- Documento de índice:
```
index.html
```

Após a configuração foi obtida a URL pública do site.

<img width="957" height="220" alt="image" src="https://github.com/user-attachments/assets/c1519bf5-8329-4ee0-a5b5-6769bee84b2c" />


---

## 6. Configuração das permissões

Para permitir o acesso público ao site foram realizadas as seguintes configurações:

- Liberação do acesso público ao bucket;
- Criação de uma Bucket Policy;
- Permissão **s3:GetObject** para os arquivos do bucket.

Essas configurações possibilitaram o acesso ao frontend diretamente pelo navegador.

<img width="1290" height="524" alt="image" src="https://github.com/user-attachments/assets/f9541263-04f5-4ffc-89a8-d0a132800d2c" />


<img width="1286" height="479" alt="image" src="https://github.com/user-attachments/assets/096c16f4-3531-4bbd-984c-e3691a0db8de" />


---

## 7. Validação

Após a publicação da aplicação, o site hospedado no Amazon S3 conseguiu consumir corretamente a API criada no API Gateway.

Ao informar um número entre **1 e 10**, o frontend envia uma requisição para a função Lambda, que processa a tentativa e retorna a resposta ao usuário.

O fluxo completo foi executado com sucesso.

<img width="735" height="602" alt="image" src="https://github.com/user-attachments/assets/cb9f12e4-288f-41fe-9aeb-c8b0ddbfee6f" />


---

#  Resultado

Ao final do laboratório foi desenvolvida uma aplicação totalmente serverless utilizando serviços gerenciados da AWS.

Fluxo implementado:

- Usuário acessa o site hospedado no Amazon S3;
- O frontend envia uma requisição para o Amazon API Gateway;
- O API Gateway invoca a função AWS Lambda;
- A Lambda processa a lógica do jogo;
- A resposta é enviada ao navegador.

---

#  Boas práticas

Durante o laboratório foram aplicados conceitos importantes para aplicações serverless, como:

- separação entre frontend e backend;
- integração entre serviços da AWS;
- hospedagem de sites estáticos no Amazon S3;
- criação de APIs utilizando Amazon API Gateway;
- configuração segura de permissões no S3;
- utilização do CORS para comunicação entre aplicações.

---

#  Aprendizados

Este laboratório demonstrou como construir uma aplicação web serverless completa utilizando serviços gerenciados da AWS.

Foi possível compreender como integrar um frontend hospedado no Amazon S3 com uma API HTTP do Amazon API Gateway, utilizando uma função AWS Lambda para processar a lógica da aplicação de forma escalável e sem gerenciamento de servidores.

---

##  Competências desenvolvidas

- AWS Lambda
- Amazon API Gateway
- Amazon S3
- Static Website Hosting
- REST API
- Serverless Computing
- Integração Frontend e Backend
- CORS
- Bucket Policy
- HTML
- JavaScript
- Python

---

