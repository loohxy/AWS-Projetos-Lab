# 📦 Laboratório AWS - Arquitetura Fan-Out com Amazon SNS, Amazon SQS e AWS Lambda

## 📖 Sobre o laboratório

Neste laboratório foi implementada uma arquitetura **Fan-Out** utilizando **Amazon SNS**, **Amazon SQS**, **AWS Lambda** e **Dead-Letter Queue (DLQ)** para simular o processamento distribuído de pedidos em um sistema de e-commerce.

A solução utiliza o Amazon SNS como ponto central de distribuição de mensagens, enviando eventos para múltiplos consumidores. Cada consumidor processa apenas os eventos relevantes através de **Subscription Filter Policies**, enquanto a integração com o Amazon SQS adiciona desacoplamento e maior resiliência ao fluxo.

---

## 🎯 Objetivos

- Implementar uma arquitetura Fan-Out utilizando Amazon SNS;
- Criar múltiplas funções AWS Lambda para processamento paralelo;
- Configurar filtros de assinatura (Subscription Filter Policies);
- Integrar Amazon SNS com Amazon SQS;
- Configurar Dead-Letter Queue (DLQ) para tratamento de falhas;
- Monitorar a execução utilizando Amazon CloudWatch Logs;
- Simular um fluxo de processamento de pedidos em um e-commerce.

---

## 🛠️ Serviços utilizados

- Amazon SNS
- Amazon SQS
- Dead-Letter Queue (DLQ)
- AWS Lambda
- AWS IAM
- Amazon CloudWatch Logs

---

## 🏗️ Arquitetura

> <img width="675" height="481" alt="image" src="https://github.com/user-attachments/assets/0979efc2-67e8-4fa5-8780-6044c37bf70b" />


```text
                     Pedido
                        │
                        ▼
                  Amazon SNS
                        │
      ┌───────────┬────────────┬──────────────┐
      ▼           ▼            ▼              ▼
Lambda         Lambda      Amazon SQS      (Filtros)
Inventário    Pagamento          │
                                 ▼
                        Lambda Fraude
                                 │
                           Erro após
                        várias tentativas
                                 │
                                 ▼
                               DLQ

Lambda Notificação
(recebe apenas eventos específicos)

CloudWatch Logs
(monitora todas as Lambdas)
```

---

# 🚀 Etapas realizadas

## 1. Criação da fila SQS e Dead-Letter Queue

Foram criadas duas filas Amazon SQS:

- Fila principal para análise de fraude;
- Dead-Letter Queue (DLQ) para tratamento de mensagens com falha.

A fila principal foi configurada para mover automaticamente mensagens para a DLQ após **3 tentativas** de processamento sem sucesso.

📷 *Inserir print da criação da fila principal.*

📷 *Inserir print da DLQ.*

---

## 2. Criação do tópico SNS

Foi criado um tópico Amazon SNS responsável por distribuir os eventos do sistema para múltiplos consumidores.

Esse tópico atua como ponto central da arquitetura Fan-Out.

📷 *Inserir print do tópico SNS.*

---

## 3. Criação das Roles IAM

Foram criadas Roles específicas para execução das funções Lambda.

As permissões foram configuradas conforme a responsabilidade de cada função.

📷 *Inserir print das Roles.*

---

## 4. Criação das funções Lambda

Foram desenvolvidas quatro funções Lambda responsáveis por diferentes processos do fluxo de pedidos:

- Atualização de inventário;
- Processamento de pagamento;
- Notificação ao cliente;
- Análise de fraude.

Cada função executa uma tarefa independente, permitindo processamento paralelo.

📷 *Inserir print das funções Lambda.*

---

## 5. Configuração do gatilho SQS

A Lambda responsável pela análise de fraude foi configurada para consumir mensagens diretamente da fila Amazon SQS.

Também foi definido o processamento de uma mensagem por execução.

📷 *Inserir print do Trigger SQS.*

---

## 6. Configuração das assinaturas SNS

Foram criadas assinaturas utilizando filtros de mensagens.

Cada consumidor recebe apenas os eventos relevantes para sua responsabilidade.

Exemplos:

- Inventário → OrderPlaced
- Pagamento → OrderPlaced + PaymentType
- Cliente → OrderConfirmed / OrderShipped
- Fraude → TransactionValue > 500

📷 *Inserir print das Subscription Filter Policies.*

---

## 7. Configuração da política da fila

Foi configurada a política de acesso da fila SQS permitindo que somente o tópico SNS publique mensagens.

📷 *Inserir print da Access Policy.*

---

## 8. Publicação da mensagem

Foi publicada uma mensagem simulando um pedido de e-commerce.

Também foram enviados atributos da mensagem para acionar corretamente os filtros das assinaturas.

📷 *Inserir print da publicação da mensagem.*

---

## 9. Validação

Após a publicação da mensagem foi possível observar:

- Lambda Inventário executada;
- Lambda Pagamento executada;
- Lambda Fraude executada através da SQS;
- Lambda Notificação não executada (conforme esperado pelos filtros).

Todos os registros foram acompanhados pelo Amazon CloudWatch Logs.

📷 *Inserir print dos logs da Lambda Inventário.*

📷 *Inserir print dos logs da Lambda Pagamento.*

📷 *Inserir print dos logs da Lambda Fraude.*

---

# 📊 Resultado

Ao final do laboratório foi implementada uma arquitetura orientada a eventos utilizando Amazon SNS como ponto central de distribuição de mensagens.

O uso de filtros de assinatura, filas SQS, processamento paralelo por Lambda e Dead-Letter Queue demonstrou uma arquitetura desacoplada, resiliente e escalável para processamento de eventos.

---

## 🌐 Arquitetura Fan-Out

Em uma arquitetura **Fan-Out**, uma única mensagem publicada em um tópico Amazon SNS pode ser distribuída simultaneamente para múltiplos consumidores.

Cada consumidor processa apenas os eventos relevantes por meio de filtros de assinatura, permitindo que diferentes fluxos de negócio sejam executados de forma independente e paralela.

### Benefícios

| Benefício | Descrição |
|-----------|-----------|
| **Desacoplamento** | Produtores e consumidores permanecem independentes. |
| **Escalabilidade** | Cada consumidor pode evoluir e escalar separadamente. |
| **Processamento paralelo** | Várias tarefas são executadas ao mesmo tempo. |
| **Resiliência** | O uso de SQS e DLQ reduz o impacto de falhas. |
| **Flexibilidade** | Novos consumidores podem ser adicionados sem alterar o produtor. |

---

## 🔀 Fluxo da arquitetura Fan-Out

| Serviço | Função |
|---------|---------|
| **Amazon SNS** | Distribui uma única mensagem para múltiplos consumidores. |
| **Subscription Filters** | Direcionam mensagens apenas para consumidores relevantes. |
| **Amazon SQS** | Desacopla o processamento e aumenta a resiliência. |
| **AWS Lambda** | Processa os eventos de forma paralela. |
| **Dead-Letter Queue (DLQ)** | Armazena mensagens que falharam repetidamente. |
| **CloudWatch Logs** | Monitora a execução das funções Lambda. |

---

## 💡 Boas práticas

Durante o laboratório foram aplicados conceitos importantes para arquiteturas distribuídas:

- utilização do padrão Fan-Out;
- comunicação assíncrona;
- desacoplamento entre serviços;
- processamento paralelo;
- filtragem de eventos;
- tratamento de falhas com Dead-Letter Queue;
- monitoramento através do CloudWatch Logs;
- separação de responsabilidades entre funções Lambda.

---

# 📚 Aprendizados

Este laboratório permitiu compreender como construir uma arquitetura orientada a eventos utilizando serviços gerenciados da AWS.

Foi possível integrar Amazon SNS, Amazon SQS e AWS Lambda para distribuir eventos de forma eficiente, utilizando filtros para direcionar mensagens apenas aos consumidores necessários e implementando mecanismos de resiliência através de Dead-Letter Queues.

---

## 🧠 Competências desenvolvidas

- Amazon SNS
- Amazon SQS
- Dead-Letter Queue (DLQ)
- AWS Lambda
- AWS IAM
- Amazon CloudWatch Logs
- Arquitetura Fan-Out
- Event-Driven Architecture
- Mensageria
- Processamento Assíncrono
- Processamento Paralelo
- Subscription Filter Policies

---
