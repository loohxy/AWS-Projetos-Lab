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

##  Arquitetura

> <img width="649" height="456" alt="image" src="https://github.com/user-attachments/assets/9d204d2b-2dc9-4b2f-8607-b4dd8c0bd28d" />


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

<img width="1280" height="422" alt="image" src="https://github.com/user-attachments/assets/c1a9d454-07a6-4fce-8254-8b95eb3c6ca5" />


---

## 2. Criação da fila principal

Foi criada uma fila Amazon SQS Standard responsável pelo recebimento das mensagens publicadas pelo tópico SNS.

Durante a configuração foram definidos:

- Associação da DLQ;
- Número máximo de recebimentos igual a **3**;
- Configurações padrão para os demais parâmetros.

<img width="1293" height="422" alt="image" src="https://github.com/user-attachments/assets/d1a010c1-a6d4-4652-9879-7832734a297f" />


---

## 3. Criação do tópico SNS

Foi criado um tópico Amazon SNS do tipo **Standard**, responsável pela distribuição das mensagens para os consumidores inscritos.

Após sua criação foi copiado o ARN do tópico para utilização nas próximas etapas.

<img width="1302" height="381" alt="image" src="https://github.com/user-attachments/assets/6b91e4fb-d55a-47df-b20b-1fd7e614f1bb" />


---

## 4. Integração entre SNS e SQS

Foi criada uma assinatura utilizando:

| Configuração | Valor |
|--------------|-------|
| Protocolo | Amazon SQS |
| Endpoint | ARN da fila principal |

Também foi configurada a política de acesso da fila SQS permitindo que somente o tópico SNS criado pudesse enviar mensagens para ela.

<img width="1289" height="453" alt="image" src="https://github.com/user-attachments/assets/a3f71ac1-b533-4d0a-9ca6-cf00bab114f9" />


<img width="1288" height="485" alt="image" src="https://github.com/user-attachments/assets/56df90a1-1c45-4477-9f12-c5958fc26e1e" />


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

<img width="1286" height="482" alt="image" src="https://github.com/user-attachments/assets/c6632f1c-0aa7-4e09-947a-b0d8339ad7bb" />


---

## 6. Validação da entrega

Após a publicação, a mensagem foi recebida corretamente na fila principal do Amazon SQS, confirmando o funcionamento da integração entre os serviços.

<img width="948" height="517" alt="image" src="https://github.com/user-attachments/assets/c4e5f0bc-0581-4bc0-a0f2-4edab6071463" />


---

## 7. Simulação de falha

Para validar o funcionamento da Dead-Letter Queue, a mensagem foi recebida repetidamente sem ser removida da fila principal.

Após atingir o limite configurado de **3 tentativas**, o Amazon SQS moveu automaticamente a mensagem para a DLQ.

Esse mecanismo evita que mensagens com erro permaneçam bloqueando o processamento das demais mensagens da fila principal.

<img width="1275" height="341" alt="image" src="https://github.com/user-attachments/assets/e52789ad-4cff-4e1a-9c50-623f7de19b75" />


<img width="1254" height="359" alt="image" src="https://github.com/user-attachments/assets/f89f7f10-23f5-437c-bd4b-4325da0bdc08" />


<img width="1248" height="332" alt="image" src="https://github.com/user-attachments/assets/c6d1b3e6-6447-49e2-acce-e704008f3fbc" />


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

