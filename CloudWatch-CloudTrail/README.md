# 📊 Laboratório AWS - Monitoramento e Auditoria com Amazon CloudWatch e AWS CloudTrail

## 📖 Sobre o laboratório

Neste laboratório foi implementada uma solução de monitoramento e auditoria utilizando **Amazon CloudWatch**, **AWS CloudTrail**, **Amazon SNS** e **Amazon S3**.

Durante a atividade foi criada uma instância Amazon EC2 para monitoramento da utilização de CPU, configurado um alarme no CloudWatch para envio de notificações via Amazon SNS e habilitada uma trilha do CloudTrail para registrar eventos da conta AWS, armazenando os logs em um bucket Amazon S3.

Essa arquitetura demonstra como combinar serviços da AWS para monitorar recursos, receber alertas automáticos e manter registros de auditoria das operações realizadas na conta.

---

## 🎯 Objetivos

- Criar uma instância Amazon EC2;
- Configurar um alarme no Amazon CloudWatch;
- Monitorar a utilização de CPU da instância;
- Enviar notificações automáticas utilizando Amazon SNS;
- Criar uma trilha de auditoria no AWS CloudTrail;
- Armazenar logs do CloudTrail em um bucket Amazon S3;
- Consultar eventos registrados pelo CloudTrail;
- Simular alta utilização de CPU para validar o monitoramento.

---

## 🛠️ Serviços utilizados

- Amazon EC2
- Amazon CloudWatch
- Amazon SNS
- AWS CloudTrail
- Amazon S3
- AWS KMS
- Amazon Linux 2023
- stress-ng

---

## 🏗️ Arquitetura

> <img width="728" height="477" alt="image" src="https://github.com/user-attachments/assets/db2d8255-88a8-4dac-90bc-bdb640559e1d" />


```text
                 Amazon EC2
                      │
             Monitoramento CPU
                      │
                      ▼
            Amazon CloudWatch
                      │
          Estado do Alarme
                      │
                      ▼
                Amazon SNS
                      │
                 Notificação
                   por e-mail

Amazon CloudTrail
        │
        ▼
Bucket Amazon S3
        │
        ▼
Logs de Auditoria
```

---

# 🚀 Etapas realizadas

## 1. Criação da instância EC2

Foi criada uma instância Amazon EC2 utilizando Amazon Linux 2023 com configurações básicas de segurança para permitir acesso remoto via SSH.

📷 *Inserir print da instância criada.*

---

## 2. Configuração do alarme CloudWatch

Foi criado um alarme baseado na métrica **CPUUtilization**.

Configuração utilizada:

| Configuração | Valor |
|--------------|-------|
| Métrica | CPUUtilization |
| Estatística | Average |
| Período | 5 minutos |
| Limite | Maior que 70% |

Quando o limite é atingido, o CloudWatch altera o estado do alarme.

📷 *Inserir print da criação do alarme.*

---

## 3. Configuração do Amazon SNS

Foi criado um tópico SNS para envio das notificações.

Também foi realizada a confirmação da assinatura do e-mail para recebimento dos alertas.

📷 *Inserir print do tópico SNS.*

📷 *Inserir print da confirmação do e-mail.*

---

## 4. Configuração do AWS CloudTrail

Foi criada uma trilha de auditoria responsável por registrar os eventos da conta AWS.

Configurações utilizadas:

- Eventos de gerenciamento
- Operações de leitura e gravação
- Armazenamento dos logs em bucket Amazon S3
- Criptografia utilizando AWS KMS

📷 *Inserir print da criação da Trail.*

---

## 5. Armazenamento dos logs

Os eventos registrados pelo CloudTrail passaram a ser armazenados automaticamente em um bucket Amazon S3 dedicado.

Também foi explorada a opção de integração com CloudWatch Logs.

📷 *Inserir print do bucket de logs.*

---

## 6. Simulação de carga

Foi realizado acesso remoto à instância EC2.

Em seguida foi instalada a ferramenta **stress-ng**, utilizada para gerar carga de CPU e validar o funcionamento do monitoramento.

📷 *Inserir print do terminal executando o stress-ng.*

---

## 7. Validação

Após alguns minutos, a utilização da CPU ultrapassou o limite configurado.

Como resultado:

- o CloudWatch alterou o estado do alarme para **In Alarm**;
- o Amazon SNS enviou automaticamente a notificação por e-mail;
- os eventos da conta permaneceram registrados pelo CloudTrail.

📷 *Inserir print do alarme em estado In Alarm.*

📷 *Inserir print do e-mail recebido.*

---

# 📊 Resultado

Ao final do laboratório foi implementada uma solução de monitoramento e auditoria utilizando serviços gerenciados da AWS.

Fluxo implementado:

- Monitoramento contínuo da CPU da instância EC2;
- Geração automática de alarmes;
- Envio de notificações por e-mail;
- Registro das ações da conta AWS pelo CloudTrail;
- Armazenamento seguro dos logs no Amazon S3.

---

## 🔍 Monitoramento x Auditoria

| Serviço | Objetivo |
|---------|----------|
| **Amazon CloudWatch** | Monitora métricas, gera alarmes e acompanha o desempenho dos recursos em tempo real. |
| **AWS CloudTrail** | Registra as ações realizadas na conta AWS para auditoria, segurança e conformidade. |
| **Amazon SNS** | Distribui notificações quando eventos ou alarmes são acionados. |
| **Amazon S3** | Armazena os logs gerados pelo CloudTrail de forma durável. |


---

## 📈 Fluxo de monitoramento e auditoria

| Serviço | Função |
|---------|---------|
| **Amazon CloudWatch** | Monitora métricas da infraestrutura e gera alarmes. |
| **Amazon SNS** | Envia notificações quando um alarme é acionado. |
| **AWS CloudTrail** | Registra as ações realizadas na conta AWS. |
| **Amazon S3** | Armazena os logs gerados pelo CloudTrail. |
| **AWS KMS** | Protege os logs utilizando criptografia. |

---

## 💡 Boas práticas

Durante o laboratório foram aplicados conceitos importantes para observabilidade e segurança na AWS:

- monitoramento contínuo da infraestrutura;
- configuração de alertas automáticos;
- auditoria das ações realizadas na conta;
- armazenamento seguro dos logs;
- criptografia utilizando AWS KMS;
- validação prática do monitoramento através da geração de carga.

---

# 📚 Aprendizados

Este laboratório permitiu compreender como integrar serviços de monitoramento e auditoria para aumentar a visibilidade sobre o ambiente AWS.

Além de acompanhar métricas da infraestrutura em tempo real, foi possível configurar alertas automáticos e registrar eventos da conta para fins de auditoria, contribuindo para boas práticas de observabilidade, segurança e governança em ambientes de produção.

---

## 🧠 Competências desenvolvidas

- Amazon EC2
- Amazon CloudWatch
- CloudWatch Alarms
- Amazon SNS
- AWS CloudTrail
- Amazon S3
- AWS KMS
- Observabilidade
- Monitoramento
- Auditoria
- Segurança em Nuvem

---


