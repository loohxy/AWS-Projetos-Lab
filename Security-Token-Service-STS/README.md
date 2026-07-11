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

> <img width="643" height="499" alt="image" src="https://github.com/user-attachments/assets/9c8476b3-ca29-44ca-a762-d19e5eb152a5" />


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

<img width="518" height="100" alt="image" src="https://github.com/user-attachments/assets/4a5bd40d-78ec-4148-926f-c5f22a082f7a" />


---

## 2. Criação da IAM Role

Foi criada uma Role personalizada utilizando uma política de confiança para permitir que o usuário IAM pudesse assumi-la.

Também foi anexada a política:

- AmazonS3FullAccess

<img width="1293" height="461" alt="image" src="https://github.com/user-attachments/assets/6a6cfb5d-147e-4876-bbb5-d3bc37677c78" />


---

## 3. Assumindo a Role pelo Console

Foi utilizada a funcionalidade **Switch Role** do Console AWS para alternar da identidade do usuário IAM para a Role criada.

Após a troca foi possível verificar que apenas os serviços autorizados estavam acessíveis.

<img width="1019" height="553" alt="image" src="https://github.com/user-attachments/assets/257937d7-c3bb-437a-9852-2c8debeffec5" />


---

## 4. Verificação da identidade

Foi executado o comando:

```bash
aws sts get-caller-identity
```

confirmando a identidade atualmente autenticada.

<img width="637" height="289" alt="image" src="https://github.com/user-attachments/assets/f83f767b-efe4-4183-a30f-36868a5bf652" />


---

## 5. Geração das credenciais temporárias

Foi executado um script Python utilizando o AWS STS para gerar credenciais temporárias.

Inicialmente foi utilizado um tempo de sessão superior ao permitido, gerando o erro esperado.

Após ajustar o tempo de sessão para um valor válido, as credenciais temporárias foram geradas com sucesso.

<img width="1246" height="74" alt="image" src="https://github.com/user-attachments/assets/225b5bbe-adcd-4f32-8d4c-80878133b2cb" />


<img width="1259" height="317" alt="image" src="https://github.com/user-attachments/assets/767f1943-5b8c-4334-8804-f9eef99e7bb3" />


---

## 6. Configuração da AWS CLI

As credenciais temporárias foram configuradas na AWS CLI.

Também foi adicionada a Session Token ao arquivo de credenciais.

<img width="1271" height="357" alt="image" src="https://github.com/user-attachments/assets/17462c3c-e59a-4e03-a82f-061354ecfb07" />


---

## 7. Validação das permissões

Foram realizados testes de acesso utilizando a AWS CLI.

Resultados obtidos:

| Serviço | Resultado |
|----------|-----------|
| Amazon S3 | Permitido |
| AWS Lambda | Acesso negado |

Esses testes demonstraram que a Role concedia apenas as permissões previamente configuradas.

<img width="623" height="115" alt="image" src="https://github.com/user-attachments/assets/72d3eb3f-004c-46a4-98bf-8b32349e3154" />


<img width="1263" height="313" alt="image" src="https://github.com/user-attachments/assets/c447e338-1f88-4afb-940f-cbd3543e56da" />


---

## 8. Teste da política de confiança

Foi alterada a política de confiança da Role, removendo a autorização do usuário IAM.

Após essa alteração, uma nova tentativa de assumir a Role resultou em erro de acesso, comprovando o funcionamento das políticas de confiança.

<img width="1013" height="465" alt="image" src="https://github.com/user-attachments/assets/3f389c9f-7fa6-4082-87f6-3ade459be4f6" />


<img width="1276" height="300" alt="image" src="https://github.com/user-attachments/assets/ff439acc-4d98-48a2-884f-ed53d521c2f1" />


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


