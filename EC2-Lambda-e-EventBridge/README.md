# ⚙️ Laboratório AWS - Automatizando o Encerramento de Instâncias EC2 com AWS Lambda e EventBridge

## 📖 Sobre o laboratório

Neste laboratório foi implementada uma solução de automação para encerramento de instâncias Amazon EC2 utilizando **AWS Lambda**, **Amazon EventBridge** e **IAM**.

Foi criada uma política personalizada no IAM, uma Role para execução da função Lambda, realizada a implantação de um código Python responsável por localizar e terminar instâncias EC2 e, por fim, configurado um gatilho no EventBridge para executar a automação em intervalos programados.

Essa arquitetura demonstra uma abordagem serverless para automatizar tarefas administrativas e reduzir custos operacionais.

---

##  Objetivos

- Criar uma política personalizada no IAM;
- Criar uma Role para execução do Lambda;
- Criar uma função AWS Lambda utilizando Python;
- Configurar permissões para gerenciamento de instâncias EC2;
- Implantar o código da função Lambda;
- Ajustar o tempo de execução da função;
- Configurar um gatilho automático utilizando Amazon EventBridge;
- Automatizar o encerramento de instâncias EC2.

---

##  Serviços utilizados

- AWS IAM
- AWS Lambda
- Amazon EC2
- Amazon EventBridge
- Amazon CloudWatch Logs

---

##  Arquitetura

> <img width="629" height="526" alt="image" src="https://github.com/user-attachments/assets/97b02691-9dda-4c82-a560-2014721db9aa" />

```
Amazon EventBridge
        │
        ▼
AWS Lambda
        │
        ▼
IAM Role
        │
        ▼
Amazon EC2
(Terminação automática)

        │
        ▼
CloudWatch Logs
```

---

#  Etapas realizadas

## 1. Criação da política IAM

Foi criada uma política personalizada contendo permissões para:

- Descrever instâncias EC2;
- Encerrar instâncias EC2;
- Consultar regiões;
- Criar grupos de logs;
- Criar streams de logs;
- Registrar eventos no CloudWatch.

<img width="1277" height="516" alt="image" src="https://github.com/user-attachments/assets/7fbfb145-e5fc-4e96-91df-5b8957839915" />


---

## 2. Criação da Role IAM

Foi criada uma Role destinada ao serviço Lambda.

Durante a configuração foi anexada a política criada anteriormente, permitindo que a função tivesse autorização para interagir com os recursos EC2.

<img width="1294" height="521" alt="image" src="https://github.com/user-attachments/assets/fb6be706-fad7-48f0-8b23-89a9ef6cdf9f" />


---

## 3. Criação da função Lambda

Foi criada uma função utilizando:

| Configuração | Valor |
|--------------|-------|
| Runtime | Python 3.13 |
| Tipo | Criar do zero |
| Execution Role | Role personalizada criada anteriormente |

<img width="1286" height="321" alt="image" src="https://github.com/user-attachments/assets/e86f9d67-a034-48bb-9417-7b990893126b" />


---

## 4. Upload do código Python

Foi realizado o upload do arquivo compactado contendo o script responsável pela automação da terminação das instâncias EC2.

Após o envio do arquivo, foi realizado o Deploy da função.

<img width="1293" height="519" alt="image" src="https://github.com/user-attachments/assets/54785669-dc98-45f8-86dc-9ce38a74eef2" />


---

## 5. Configuração da função

Foram realizados dois ajustes importantes:

### Timeout

Alterado de:

- 3 segundos

para

- 10 segundos

garantindo tempo suficiente para finalizar a execução da função.

### Handler

Configurado como:

```
Terminator.lambda_handler
```

para indicar corretamente o ponto de entrada do código Python.

<img width="1292" height="406" alt="image" src="https://github.com/user-attachments/assets/7bbd39c0-a19c-49c7-842c-149bd080d888" />


---

## 6. Configuração do EventBridge

Foi criado um gatilho utilizando o Amazon EventBridge.

Configuração utilizada:

- Regra de agendamento
- Expressão Rate

Exemplo:

```
rate(5 minutes)
```

ou

```
rate(12 hours)
```

dependendo do objetivo do laboratório.

<img width="1281" height="448" alt="image" src="https://github.com/user-attachments/assets/cf3e75d2-4053-473d-ac15-3b7a6731881b" />


---

## 7. Validação

Para validar a automação, foi criada uma instância Amazon EC2 de teste. Após o intervalo configurado no Amazon EventBridge, a função Lambda foi executada automaticamente e realizou o encerramento da instância conforme esperado.

Os registros da execução podem ser acompanhados no Amazon CloudWatch Logs, enquanto o Console EC2 confirma que a instância foi encerrada com sucesso.

<img width="1299" height="483" alt="image" src="https://github.com/user-attachments/assets/195c6639-cc20-4e03-a872-03316cccf1e0" />

<img width="1309" height="470" alt="image" src="https://github.com/user-attachments/assets/f24defb3-ea22-482b-bf07-304684c9ad9b" />





---

#  Resultado

Ao final do laboratório foi construída uma solução totalmente automatizada para encerramento de instâncias EC2 utilizando arquitetura serverless.

Fluxo implementado:

- EventBridge agenda a execução;
- Lambda é acionado automaticamente;
- IAM concede as permissões necessárias;
- Lambda localiza e encerra as instâncias EC2;
- CloudWatch registra toda a execução.

---

#  Boas práticas

Durante o laboratório foi possível compreender conceitos importantes relacionados à automação na AWS.

Entre eles:

- princípio do menor privilégio (Least Privilege);
- automação de tarefas administrativas;
- utilização de arquitetura serverless;
- redução de custos com desligamento automático de recursos;
- monitoramento através do CloudWatch;
- uso do EventBridge para execução baseada em tempo.

---

#  Aprendizados

Este laboratório demonstrou como integrar diferentes serviços da AWS para criar uma solução de automação utilizando computação serverless.

Além do desenvolvimento da função Lambda em Python, foi possível compreender como as permissões do IAM, os gatilhos do EventBridge e o CloudWatch trabalham em conjunto para executar tarefas administrativas automaticamente, reduzindo esforço operacional e contribuindo para um melhor controle dos recursos em nuvem.

---
