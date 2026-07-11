# 🚀 Laboratório AWS - Implantação de Aplicações com AWS Elastic Beanstalk

## 📖 Sobre o laboratório

Neste laboratório foi realizado o deploy de uma aplicação web utilizando o **AWS Elastic Beanstalk**, explorando o processo de criação da infraestrutura, configuração de permissões IAM e gerenciamento do ambiente.

Durante a atividade foi criada uma IAM Role para as instâncias EC2, implantada uma aplicação de exemplo utilizando o Elastic Beanstalk e exploradas funcionalidades como monitoramento, logs, atualizações gerenciadas e configuração da infraestrutura.

O laboratório demonstra como o Elastic Beanstalk simplifica o ciclo de vida de aplicações, automatizando o provisionamento e gerenciamento de diversos serviços da AWS.

---

## 🎯 Objetivos

- Criar uma IAM Role para instâncias EC2 do Elastic Beanstalk;
- Implantar uma aplicação utilizando o AWS Elastic Beanstalk;
- Explorar o gerenciamento do ambiente pelo console;
- Monitorar métricas e logs da aplicação;
- Compreender como o Elastic Beanstalk gerencia a infraestrutura automaticamente.

---

## 🛠️ Serviços utilizados

- AWS Elastic Beanstalk
- AWS IAM
- Amazon EC2
- AWS CloudFormation
- Amazon CloudWatch
- Auto Scaling
- Elastic Load Balancing (conceitualmente)

---

## 🏗️ Arquitetura

> <img width="475" height="519" alt="image" src="https://github.com/user-attachments/assets/95b87cd4-002c-4471-b3b4-b5226a628be2" />

```text
              Usuário
                  │
                  ▼
        AWS Elastic Beanstalk
                  │
      Provisionamento Automático
                  │
      ┌───────────┼──────────────┐
      ▼           ▼              ▼
 Amazon EC2   CloudFormation  CloudWatch
      │
      ▼
 Aplicação Web
```

---

# 🚀 Etapas realizadas

## 1. Criação da IAM Role

Foi criada uma IAM Role destinada às instâncias EC2 utilizadas pelo Elastic Beanstalk.

Foram associadas políticas gerenciadas necessárias para o funcionamento do ambiente, incluindo permissões de monitoramento e gerenciamento.

📷 *Inserir print da criação da Role.*

---

## 2. Criação da aplicação

Foi criada uma aplicação no AWS Elastic Beanstalk utilizando uma aplicação de exemplo disponibilizada pela própria AWS.

Configurações utilizadas:

- Plataforma: Node.js
- Ambiente: Web Server
- Preset: Single Instance
- Código: Sample Application

📷 *Inserir print da criação da aplicação.*

---

## 3. Configuração do ambiente

Durante a criação do ambiente foram configuradas:

- Service Role do Elastic Beanstalk;
- EC2 Instance Profile;
- Ambiente de desenvolvimento.

Após a revisão das configurações, foi iniciado o provisionamento automático da infraestrutura.

📷 *Inserir print da configuração do ambiente.*

---

## 4. Provisionamento da infraestrutura

O Elastic Beanstalk criou automaticamente os recursos necessários para execução da aplicação.

Também foi possível acompanhar o processo através da Stack criada no AWS CloudFormation.

📷 *Inserir print da Stack no CloudFormation.*

---

## 5. Exploração do ambiente

Após a criação do ambiente foram exploradas diversas funcionalidades do serviço:

- Upload de novas versões da aplicação;
- Visualização da saúde do ambiente;
- Download dos logs;
- Monitoramento via CloudWatch;
- Alarmes;
- Atualizações gerenciadas;
- Configurações do ambiente.

📷 *Inserir print da aba Health.*

📷 *Inserir print da aba Logs.*

📷 *Inserir print da aba Monitoring.*

---

## 6. Validação

Após a conclusão do provisionamento, a aplicação de exemplo foi disponibilizada com sucesso.

Também foi possível verificar que toda a infraestrutura foi criada automaticamente e passou a ser gerenciada pelo Elastic Beanstalk.

📷 *Inserir print da aplicação funcionando.*

---

# 📊 Resultado

Ao final do laboratório foi implantada uma aplicação web utilizando o AWS Elastic Beanstalk.

O serviço automatizou o provisionamento da infraestrutura necessária, incluindo recursos como Amazon EC2, AWS CloudFormation e monitoramento pelo Amazon CloudWatch, permitindo o gerenciamento centralizado da aplicação.

---

## 🤖 O que o Elastic Beanstalk gerencia automaticamente?

O AWS Elastic Beanstalk automatiza diversas tarefas operacionais necessárias para hospedar uma aplicação na AWS.

| Serviço | Responsabilidade |
|---------|------------------|
| **Amazon EC2** | Provisiona as instâncias que executam a aplicação. |
| **AWS CloudFormation** | Cria e gerencia a infraestrutura como código. |
| **Amazon CloudWatch** | Coleta métricas e disponibiliza monitoramento. |
| **Auto Scaling** | Ajusta automaticamente a quantidade de instâncias (quando configurado). |
| **Elastic Load Balancer** | Distribui as requisições entre as instâncias (quando utilizado). |
| **Elastic Beanstalk** | Centraliza o gerenciamento da aplicação e da infraestrutura. |

---

## ⚙️ Recursos gerenciados pelo Elastic Beanstalk

| Recurso | Finalidade |
|---------|------------|
| **Amazon EC2** | Hospedagem da aplicação. |
| **AWS CloudFormation** | Provisionamento da infraestrutura. |
| **Amazon CloudWatch** | Monitoramento e métricas da aplicação. |
| **Auto Scaling** | Escalabilidade automática (quando configurado). |
| **Elastic Load Balancer** | Distribuição de carga (quando utilizado). |

---

## 💡 Boas práticas

Durante o laboratório foram aplicados conceitos importantes para implantação de aplicações na AWS:

- utilização de IAM Roles específicas;
- separação entre Service Role e Instance Profile;
- gerenciamento automatizado da infraestrutura;
- monitoramento da aplicação;
- centralização das configurações do ambiente;
- utilização de aplicações versionadas.

---

# 📚 Aprendizados

Este laboratório permitiu compreender como o AWS Elastic Beanstalk simplifica a implantação e o gerenciamento de aplicações na nuvem.

Também foi possível visualizar como diversos serviços da AWS trabalham em conjunto para fornecer uma plataforma gerenciada, reduzindo a complexidade operacional e permitindo que o foco permaneça no desenvolvimento da aplicação.

---

## 🧠 Competências desenvolvidas

- AWS Elastic Beanstalk
- Amazon EC2
- AWS CloudFormation
- Amazon CloudWatch
- AWS IAM
- Auto Scaling
- Platform as a Service (PaaS)
- Deploy de Aplicações
- Gerenciamento de Ambientes

---


