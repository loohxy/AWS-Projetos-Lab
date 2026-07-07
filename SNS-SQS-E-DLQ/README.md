# 📬 Laboratório AWS - Integração entre Amazon SNS, Amazon SQS e Dead-Letter Queue (DLQ)

## 📖 Sobre o laboratório

Neste laboratório foi implementada uma arquitetura de mensageria utilizando **Amazon SNS**, **Amazon SQS** e **Dead-Letter Queue (DLQ)**.

A solução permite publicar mensagens em um tópico SNS, distribuí-las para uma fila SQS e tratar mensagens que falham repetidamente no processamento através de uma fila DLQ, aumentando a resiliência da aplicação.

Essa arquitetura é amplamente utilizada em sistemas distribuídos e microsserviços para garantir comunicação assíncrona e maior confiabilidade no processamento de eventos.

---

## 🎯 Objetivos

- Criar uma fila Amazon SQS para atuar como Dead-Letter Queue (DLQ);
- Criar uma fila SQS principal;
- Configurar a Redrive Policy entre a fila principal e a DLQ;
- Criar um tópico Amazon SNS;
- Inscrever a fila SQS no tópico SNS;
- Publicar mensagens no SNS;
- Validar o recebimento das mensagens na fila SQS;
- Simular falhas para redirecionamento automático das mensagens para a DLQ.

---

## 🛠️ Serviços utilizados

- Amazon SNS
- Amazon SQS
- Dead-Letter Queue (DLQ)
- AWS IAM
- AWS Management Console

---

## 🏗️ Arquitetura

> *(Inserir aqui o diagrama utilizado no laboratório.)*

```text
                Publicador
                     │
                     ▼
              Amazon SNS (Tópico)
                     │
                     ▼
           Amazon SQS (Fila Principal)
                     │
      Processamento da Mensagem
          │                     │
          ▼                     ▼
     Sucesso             Falha após
                         várias tentativas
                                │
                                ▼
                    Amazon SQS DLQ
```

---

# 🚀 Etapas realizadas

## 1. Criação da Dead-Letter Queue (DLQ)

Foi criada uma fila Amazon SQS do tipo **Standard**, destinada ao armazenamento de mensagens que não puderam ser processadas com sucesso após o número máximo de tentativas.

Após a criação, foi obtido o ARN da fila para utilização nas configurações da fila principal.

📷 *Inserir print da criação da DLQ.*

---

## 2. Criação da fila principal

Foi criada uma fila Amazon SQS Standard responsável pelo recebimento das mensagens publicadas pelo tópico SNS.

Durante a configuração foram definidos:

- Associação da DLQ;
- Número máximo de recebimentos igual a **3**;
- Configurações padrão para os demais parâmetros.

📷 *Inserir print da criação da fila principal.*

---

## 3. Criação do tópico SNS

Foi criado um tópico Amazon SNS do tipo **Standard**, responsável pela distribuição das mensagens para os consumidores inscritos.

Após sua criação foi copiado o ARN do tópico para utilização nas próximas etapas.

📷 *Inserir print da criação do tópico.*

---

## 4. Integração entre SNS e SQS

Foi criada uma assinatura utilizando:

| Configuração | Valor |
|--------------|-------|
| Protocolo | Amazon SQS |
| Endpoint | ARN da fila principal |

Também foi configurada a política de acesso da fila SQS permitindo que somente o tópico SNS criado pudesse enviar mensagens para ela.

📷 *Inserir print da assinatura.*

📷 *Inserir print da política da fila.*

---

## 5. Publicação da mensagem

Foi publicada uma mensagem de teste no tópico SNS contendo um exemplo de evento em formato JSON.

Exemplo:

```json
{
  "evento": "pedido_criado",
  "pedido_id": "12345",
  "cliente_id": "9876",
  "timestamp": "2024-03-15T10:00:00Z"
}
```

📷 *Inserir print da publicação da mensagem.*

---

## 6. Validação da entrega

Após a publicação, a mensagem foi recebida corretamente na fila principal do Amazon SQS, confirmando o funcionamento da integração entre os serviços.

📷 *Inserir print da mensagem recebida.*

---

## 7. Simulação de falha

Para validar o funcionamento da Dead-Letter Queue, a mensagem foi recebida repetidamente sem ser removida da fila principal.

Após atingir o limite configurado de **3 tentativas**, o Amazon SQS moveu automaticamente a mensagem para a DLQ.

Esse mecanismo evita que mensagens com erro permaneçam bloqueando o processamento das demais mensagens da fila principal.

📷 *Inserir print da Receive Count.*

📷 *Inserir print da fila principal sem a mensagem.*

📷 *Inserir print da mensagem presente na DLQ.*

---

# 📊 Resultado

Ao final do laboratório foi construída uma arquitetura de mensageria baseada em eventos utilizando serviços gerenciados da AWS.

Fluxo implementado:

- Publicação de mensagens via Amazon SNS;
- Distribuição automática para Amazon SQS;
- Processamento assíncrono;
- Redirecionamento automático de mensagens com falha para a Dead-Letter Queue.

---

# 💡 Boas práticas

Durante o laboratório foram exploradas práticas importantes para arquiteturas distribuídas, como:

- desacoplamento entre aplicações;
- comunicação assíncrona;
- utilização de Dead-Letter Queue para tratamento de falhas;
- aumento da resiliência dos sistemas;
- isolamento de mensagens problemáticas;
- políticas de acesso entre serviços da AWS.

---

# 📚 Aprendizados

Este laboratório permitiu compreender como o Amazon SNS e o Amazon SQS trabalham em conjunto para implementar arquiteturas orientadas a eventos.

Também foi possível entender o papel das Dead-Letter Queues (DLQ) na confiabilidade dos sistemas, permitindo que mensagens com falha sejam isoladas para análise posterior sem interromper o fluxo de processamento das demais mensagens.

---

## 🧠 Competências desenvolvidas

- Amazon SNS
- Amazon SQS
- Dead-Letter Queue (DLQ)
- Event-Driven Architecture
- Mensageria
- Microsserviços
- Comunicação Assíncrona
- Tratamento de Falhas
- Políticas de acesso AWS
- Arquiteturas resilientes

---

## 📎 Referências

- Amazon SNS
- Amazon SQS
- Dead-Letter Queue (DLQ)
- Documentação oficial da AWS
