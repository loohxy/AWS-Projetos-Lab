# 🔐 Laboratório AWS - Credenciais Temporárias com AWS Security Token Service (STS)

## 📖 Sobre o laboratório

Neste laboratório foi explorado o **AWS Security Token Service (STS)** para criação e utilização de credenciais temporárias por meio da assunção de uma **IAM Role**.

Durante a atividade foi criada uma Role com permissões específicas, configurada sua política de confiança, assumida a Role tanto pelo Console AWS quanto pela AWS CLI e realizadas validações de acesso utilizando credenciais temporárias geradas pelo STS.

O laboratório também demonstrou como políticas de confiança controlam quem pode assumir uma Role, reforçando conceitos importantes de segurança e gerenciamento de identidades na AWS.

---

## 🎯 Objetivos

- Criar uma IAM Role com permissões específicas;
- Configurar a política de confiança da Role;
- Assumir uma Role utilizando o Console AWS;
- Gerar credenciais temporárias utilizando o AWS STS;
- Configurar as credenciais temporárias na AWS CLI;
- Validar permissões permitidas e negadas;
- Compreender o funcionamento das sessões temporárias.

---

## 🛠️ Serviços utilizados

- AWS Security Token Service (STS)
- AWS Identity and Access Management (IAM)
- AWS CloudShell
- AWS CLI
- Amazon S3

---

## 🏗️ Arquitetura

> *(Inserir aqui o diagrama utilizado no laboratório.)*

```text
          Usuário IAM
                │
      Assume uma Role
                │
                ▼
          AWS STS
                │
  Geração de Credenciais
        Temporárias
                │
                ▼
        AWS CLI / CloudShell
                │
        Permissões da Role
                │
        ┌────────┴────────┐
        ▼                 ▼
   Amazon S3        Outros Serviços
 (Permitido)        (Conforme Permissões)
```

---

# 🚀 Etapas realizadas

## 1. Preparação do ambiente

Foi utilizado o AWS CloudShell para preparar o ambiente de execução.

Durante essa etapa foram instalados:

- Python 3;
- Biblioteca Boto3;
- AWS CLI.

📷 *Inserir print da instalação do Python e Boto3.*

---

## 2. Criação da IAM Role

Foi criada uma Role personalizada utilizando uma política de confiança para permitir que o usuário IAM pudesse assumi-la.

Também foi anexada a política:

- AmazonS3FullAccess

📷 *Inserir print da criação da Role.*

---

## 3. Assumindo a Role pelo Console

Foi utilizada a funcionalidade **Switch Role** do Console AWS para alternar da identidade do usuário IAM para a Role criada.

Após a troca foi possível verificar que apenas os serviços autorizados estavam acessíveis.

📷 *Inserir print do Switch Role.*

---

## 4. Verificação da identidade

Foi executado o comando:

```bash
aws sts get-caller-identity
```

confirmando a identidade atualmente autenticada.

📷 *Inserir print do comando.*

---

## 5. Geração das credenciais temporárias

Foi executado um script Python utilizando o AWS STS para gerar credenciais temporárias.

Inicialmente foi utilizado um tempo de sessão superior ao permitido, gerando o erro esperado.

Após ajustar o tempo de sessão para um valor válido, as credenciais temporárias foram geradas com sucesso.

📷 *Inserir print do erro de duração.*

📷 *Inserir print das credenciais temporárias geradas (mascarando Access Key, Secret Key e Session Token).*

---

## 6. Configuração da AWS CLI

As credenciais temporárias foram configuradas na AWS CLI.

Também foi adicionada a Session Token ao arquivo de credenciais.

📷 *Inserir print da configuração.*

---

## 7. Validação das permissões

Foram realizados testes de acesso utilizando a AWS CLI.

Resultados obtidos:

| Serviço | Resultado |
|----------|-----------|
| Amazon S3 | Permitido |
| AWS Lambda | Acesso negado |

Esses testes demonstraram que a Role concedia apenas as permissões previamente configuradas.

📷 *Inserir print do acesso ao S3.*

📷 *Inserir print do acesso negado ao Lambda.*

---

## 8. Teste da política de confiança

Foi alterada a política de confiança da Role, removendo a autorização do usuário IAM.

Após essa alteração, uma nova tentativa de assumir a Role resultou em erro de acesso, comprovando o funcionamento das políticas de confiança.

📷 *Inserir print da alteração da Trust Policy.*

📷 *Inserir print do erro ao assumir a Role.*

---

# 📊 Resultado

Ao final do laboratório foi implementado um fluxo completo de autenticação utilizando credenciais temporárias do AWS STS.

Também foi possível validar o funcionamento das políticas de confiança, o controle de permissões através de IAM Roles e o comportamento das credenciais temporárias durante sua utilização e expiração.

---

## 🔄 Como funciona o AWS STS

```text
Usuário IAM
      │
      ▼
 Assume uma IAM Role
      │
      ▼
 AWS Security Token Service (STS)
      │
      ▼
 Credenciais Temporárias
      │
      ▼
 AWS CLI / Console AWS
      │
      ▼
 Acesso apenas aos recursos permitidos pela Role
```

### Benefícios

| Benefício | Descrição |
|-----------|-----------|
| **Segurança** | Evita o uso de credenciais permanentes. |
| **Controle** | Permissões definidas pela IAM Role. |
| **Tempo limitado** | As credenciais expiram automaticamente. |
| **Menor privilégio** | O acesso é restrito apenas aos recursos necessários. |


---

## 🔑 Fluxo das credenciais temporárias

| Etapa | Descrição |
|--------|-----------|
| **Usuário IAM** | Solicita acesso temporário. |
| **AWS STS** | Gera credenciais temporárias. |
| **IAM Role** | Define as permissões concedidas. |
| **AWS CLI** | Utiliza as credenciais temporárias para acessar os serviços. |
| **Expiração** | Após o tempo definido, as credenciais deixam de ser válidas. |

---

## 💡 Boas práticas

Durante o laboratório foram aplicados conceitos importantes relacionados à segurança e gerenciamento de identidades:

- utilização de credenciais temporárias;
- aplicação do princípio do menor privilégio;
- separação entre usuários IAM e Roles;
- utilização de políticas de confiança;
- redução do uso de credenciais permanentes;
- controle do tempo de sessão das credenciais.

---

# 📚 Aprendizados

Este laboratório permitiu compreender como o AWS Security Token Service (STS) fornece credenciais temporárias para acesso seguro aos recursos da AWS.

Também foi possível observar como IAM Roles e políticas de confiança trabalham em conjunto para controlar quem pode assumir uma função, além de validar permissões permitidas, acessos negados e o comportamento das credenciais após sua expiração.

---

## 🧠 Competências desenvolvidas

- AWS STS
- AWS IAM
- IAM Roles
- Trust Policies
- Credenciais Temporárias
- AWS CLI
- AWS CloudShell
- Segurança na AWS
- Controle de Acesso
- Gerenciamento de Identidades

---


