# 🔐 Laboratório AWS - AWS Systems Manager Parameter Store com AWS KMS e CloudShell

## 📖 Sobre o laboratório

Neste laboratório foi utilizado o **AWS Systems Manager Parameter Store** para armazenar parâmetros de configuração da aplicação, incluindo informações públicas e dados sensíveis criptografados utilizando o **AWS Key Management Service (KMS)**.

Além da criação dos parâmetros, foram realizadas consultas utilizando a **AWS CLI** no CloudShell, permitindo visualizar os parâmetros do tipo **String** e recuperar parâmetros **SecureString** com descriptografia.

Essa prática é amplamente utilizada para armazenar configurações de aplicações de forma segura, evitando informações sensíveis diretamente no código.

---

## 🎯 Objetivos

- Criar parâmetros do tipo String;
- Criar parâmetros do tipo SecureString;
- Criar uma chave de criptografia no AWS KMS;
- Armazenar configurações de ambientes de desenvolvimento e produção;
- Consultar parâmetros utilizando AWS CLI;
- Recuperar parâmetros criptografados com descriptografia.

---

## 🛠️ Serviços utilizados

- AWS Systems Manager (Parameter Store)
- AWS Key Management Service (KMS)
- AWS CloudShell
- AWS CLI

---

## 🏗️ Arquitetura

> <img width="626" height="503" alt="image" src="https://github.com/user-attachments/assets/7f551392-6d62-4f11-9c3d-cb32ed4f0d66" />


```text
            Aplicação
                 │
                 ▼
      AWS Systems Manager
        Parameter Store
        │            │
        │            ▼
        │      SecureString
        │            │
        ▼            ▼
     String      AWS KMS
        │            │
        └──────┬─────┘
               ▼
        AWS CloudShell
           (AWS CLI)
```

---

# 🚀 Etapas realizadas

## 1. Criação dos parâmetros String

Foram criados dois parâmetros do tipo **String** para armazenar URLs de banco de dados dos ambientes:

- Desenvolvimento
- Produção

Esses parâmetros representam informações que não necessitam de criptografia.

📷 *Inserir print dos parâmetros String.*

---

## 2. Criação da chave KMS

Foi criada uma chave de criptografia utilizando o **AWS Key Management Service (KMS)**.

Essa chave será utilizada para proteger informações sensíveis armazenadas no Parameter Store.

📷 *Inserir print da chave KMS.*

---

## 3. Criação dos parâmetros SecureString

Após a criação da chave KMS, foram criados dois parâmetros do tipo **SecureString**:

- Senha do banco de dados (Desenvolvimento)
- Senha do banco de dados (Produção)

Esses parâmetros utilizam a chave KMS para armazenar os dados de forma criptografada.

📷 *Inserir print dos parâmetros SecureString.*

---

## 4. Consulta utilizando AWS CLI

Foi utilizado o AWS CloudShell para recuperar os parâmetros utilizando a AWS CLI.

Primeira consulta:

```bash
aws ssm get-parameters \
--names /meu-app/dev/db-url /meu-app/dev/db-password
```

Nesse momento foi possível observar que:

- parâmetros String aparecem em texto legível;
- parâmetros SecureString permanecem criptografados.

📷 *Inserir print da primeira consulta.*

---

## 5. Recuperação com descriptografia

Foi realizada uma nova consulta utilizando o parâmetro:

```bash
--with-decryption
```

Com isso, o Parameter Store utilizou a chave KMS para descriptografar automaticamente o conteúdo do SecureString.

📷 *Inserir print da consulta com --with-decryption.*

---

# 📊 Resultado

Ao final do laboratório foi implementado um armazenamento seguro de configurações utilizando o AWS Systems Manager Parameter Store.

Também foi possível integrar o serviço ao AWS KMS para proteger dados sensíveis e utilizar a AWS CLI para recuperar informações com e sem descriptografia.

---

## 🛡️ Fluxo de funcionamento

```text
Aplicação
      │
      ▼
Parameter Store
      │
      ├────────► String
      │
      └────────► SecureString
                     │
                     ▼
               AWS KMS
                     │
                     ▼
AWS CLI (--with-decryption)
                     │
                     ▼
Valor descriptografado
```

---

## 🔐 Tipos de parâmetros no Parameter Store

| Tipo | Característica | Exemplo |
|------|----------------|----------|
| **String** | Armazena informações em texto simples. | URL do banco de dados |
| **SecureString** | Armazena informações criptografadas utilizando o AWS KMS. | Senhas, tokens e chaves de API |

---

## ⚖️ Recuperação de parâmetros

| Comando | Resultado |
|---------|-----------|
| `get-parameters` | Retorna os parâmetros, mantendo SecureString criptografado. |
| `get-parameters --with-decryption` | Retorna também os parâmetros SecureString descriptografados. |

---

# 💡 Boas práticas

Durante o laboratório foram aplicados conceitos importantes para gerenciamento seguro de configurações:

- armazenamento de segredos fora do código-fonte;
- utilização de criptografia com AWS KMS;
- organização de parâmetros por ambiente;
- uso da AWS CLI para automação;
- separação entre configurações públicas e informações sensíveis.

---

# 📚 Aprendizados

Este laboratório permitiu compreender como utilizar o AWS Systems Manager Parameter Store para armazenar configurações de aplicações de forma centralizada e segura.

Também foi possível entender como o AWS KMS protege informações sensíveis e como a AWS CLI pode recuperar parâmetros criptografados de forma controlada, tornando essa solução adequada para aplicações em ambientes de desenvolvimento e produção.

---

## 🧠 Competências desenvolvidas

- AWS Systems Manager
- Parameter Store
- AWS KMS
- AWS CLI
- AWS CloudShell
- SecureString
- Gerenciamento de Configurações
- Gerenciamento de Segredos
- Criptografia
- Segurança na AWS

---
