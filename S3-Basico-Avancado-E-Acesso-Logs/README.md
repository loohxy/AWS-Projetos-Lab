# 🪣 Laboratório AWS - Amazon S3: Versionamento, Ciclo de Vida, URLs Pré-assinadas e Logs de Acesso

## 📖 Sobre o laboratório

Neste laboratório foram explorados recursos fundamentais do **Amazon S3** voltados para armazenamento, segurança, governança e gerenciamento do ciclo de vida dos objetos.

Durante a atividade foram criados buckets com configurações recomendadas de segurança, habilitado o versionamento de objetos, configuradas regras de ciclo de vida para otimização de custos, geradas URLs pré-assinadas para compartilhamento temporário de arquivos e ativados os logs de acesso utilizando um bucket dedicado.

---

## 🎯 Objetivos

- Criar buckets utilizando boas práticas de segurança;
- Realizar upload de objetos;
- Habilitar o versionamento de arquivos;
- Restaurar versões anteriores de objetos;
- Configurar regras de ciclo de vida;
- Gerar URLs pré-assinadas;
- Configurar logs de acesso do Amazon S3;
- Compreender estratégias de gerenciamento e segurança de objetos.

---

## 🛠️ Serviços utilizados

- Amazon S3
- AWS IAM
- Amazon S3 Lifecycle
- Amazon S3 Versioning
- Amazon S3 Access Logs
- Pre-Signed URLs

---

## 🏗️ Arquitetura

> <img width="707" height="490" alt="image" src="https://github.com/user-attachments/assets/ec31fea7-a753-4aac-8b33-f9068fd8b0f3" />


```text
               Usuário
                   │
                   ▼
         Bucket Principal (Amazon S3)
                   │
        ┌──────────┼──────────┐
        │          │          │
        ▼          ▼          ▼
 Versionamento  Lifecycle  URL Pré-assinada
        │
        ▼
 Bucket de Logs (S3 Access Logs)
```

---

# 🚀 Etapas realizadas

## 1. Criação do bucket

Foi criado um bucket Amazon S3 utilizando configurações recomendadas de segurança, incluindo:

- bloqueio de acesso público;
- criptografia padrão (SSE-S3);
- ACLs desabilitadas.

<img width="1296" height="508" alt="image" src="https://github.com/user-attachments/assets/7bedc6d6-2ec3-4ea7-a57f-29ad441b4249" />


---

## 2. Upload de arquivos

Foi criado um arquivo de teste e realizado o upload para o bucket.

Após o primeiro envio, o bucket passou a armazenar o objeto.

<img width="1293" height="522" alt="image" src="https://github.com/user-attachments/assets/6dd8a0a2-b40f-4538-be60-789b76037d17" />


---

## 3. Versionamento

O versionamento do bucket foi habilitado.

Em seguida foi realizado um novo upload do mesmo arquivo, criando automaticamente uma nova versão do objeto.

Também foi possível visualizar e recuperar versões anteriores.

<img width="1287" height="484" alt="image" src="https://github.com/user-attachments/assets/fe0ef5df-ca2e-4cc9-b90b-a6bcd5c4555c" />


<img width="1278" height="311" alt="image" src="https://github.com/user-attachments/assets/dd103cfd-952a-49d1-a6a0-154a0d04cc86" />


---

## 4. Regra de ciclo de vida

Foi criada uma regra de Lifecycle para automatizar o gerenciamento dos objetos.

Configuração utilizada:

| Configuração | Valor |
|--------------|-------|
| Transição | Glacier Instant Retrieval |
| Após | 30 dias |
| Expiração | 31 dias |

Essa configuração reduz custos de armazenamento para arquivos acessados com pouca frequência.

<img width="1299" height="500" alt="image" src="https://github.com/user-attachments/assets/62984a20-3535-4b9a-b8ba-96332efd251d" />


---

## 5. URL Pré-assinada

Foi gerada uma URL pré-assinada para compartilhamento temporário do objeto armazenado no bucket.

Essa funcionalidade permite disponibilizar arquivos de forma segura por um período determinado, sem necessidade de tornar o bucket público.

📷 *Inserir print da URL pré-assinada.*

---

## 6. Bucket de logs

Foi criado um segundo bucket destinado ao armazenamento dos logs de acesso do Amazon S3.

Em seguida foi habilitado o Server Access Logging no bucket principal.

📷 *Inserir print da criação do bucket de logs.*

---

## 7. Validação

Após gerar novas operações no bucket principal, os registros passaram a ser armazenados automaticamente no bucket de logs.

Essa funcionalidade permite auditoria e monitoramento das operações realizadas sobre os objetos.

📷 *Inserir print dos logs gerados.*

---

# 📊 Resultado

Ao final do laboratório foi implementada uma estrutura completa de gerenciamento de objetos no Amazon S3, contemplando versionamento, automação do ciclo de vida, compartilhamento seguro de arquivos e monitoramento por meio de logs de acesso.

---

## 🔄 Fluxo dos recursos do Amazon S3

| Recurso | Benefício |
|---------|-----------|
| **Versionamento** | Recuperação de versões anteriores dos objetos. |
| **Lifecycle** | Redução automática de custos de armazenamento. |
| **Pre-Signed URL** | Compartilhamento temporário e seguro de arquivos. |
| **Server Access Logging** | Auditoria das operações realizadas no bucket. |

---


## 📦 Recursos explorados

| Recurso | Finalidade |
|---------|------------|
| **Versionamento** | Preserva múltiplas versões de um mesmo objeto. |
| **Lifecycle** | Automatiza transições entre classes de armazenamento e exclusão de objetos. |
| **Pre-Signed URL** | Compartilha arquivos temporariamente de forma segura. |
| **Server Access Logging** | Registra operações realizadas sobre o bucket. |

---

## 💡 Boas práticas

Durante o laboratório foram aplicadas práticas recomendadas para utilização do Amazon S3:

- bloqueio de acesso público por padrão;
- criptografia automática dos objetos;
- versionamento para recuperação de arquivos;
- automação do ciclo de vida para redução de custos;
- compartilhamento temporário utilizando URLs pré-assinadas;
- auditoria através dos logs de acesso.

---

# 📚 Aprendizados

Este laboratório permitiu compreender como o Amazon S3 oferece recursos que vão além do simples armazenamento de arquivos.

Foi possível explorar funcionalidades relacionadas à segurança, governança, otimização de custos e rastreabilidade, demonstrando como esses recursos podem ser combinados para construir soluções mais eficientes e seguras em ambientes de produção.

---

## 🧠 Competências desenvolvidas

- Amazon S3
- Versionamento de Objetos
- Lifecycle Policies
- Glacier Instant Retrieval
- Pre-Signed URLs
- Server Access Logging
- Segurança no Amazon S3
- Governança de Dados
- Gerenciamento de Objetos
- Otimização de Custos

---

