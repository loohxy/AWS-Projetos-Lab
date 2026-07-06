# ⚙️ Laboratório AWS - Automatizando o Encerramento de Instâncias EC2 com AWS Lambda e EventBridge

## 📖 Sobre o laboratório

Neste laboratório foi implementada uma solução de automação para encerramento de instâncias Amazon EC2 utilizando **AWS Lambda**, **Amazon EventBridge** e **IAM**.

Foi criada uma política personalizada no IAM, uma Role para execução da função Lambda, realizada a implantação de um código Python responsável por localizar e terminar instâncias EC2 e, por fim, configurado um gatilho no EventBridge para executar a automação em intervalos programados.

Essa arquitetura demonstra uma abordagem serverless para automatizar tarefas administrativas e reduzir custos operacionais.

---

## 🎯 Objetivos

- Criar uma política personalizada no IAM;
- Criar uma Role para execução do Lambda;
- Criar uma função AWS Lambda utilizando Python;
- Configurar permissões para gerenciamento de instâncias EC2;
- Implantar o código da função Lambda;
- Ajustar o tempo de execução da função;
- Configurar um gatilho automático utilizando Amazon EventBridge;
- Automatizar o encerramento de instâncias EC2.

---

## 🛠️ Serviços utilizados

- AWS IAM
- AWS Lambda
- Amazon EC2
- Amazon EventBridge
- Amazon CloudWatch Logs

---

## 🏗️ Arquitetura

> *(Inserir aqui o diagrama da arquitetura do laboratório.)*

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

# 🚀 Etapas realizadas

## 1. Criação da política IAM

Foi criada uma política personalizada contendo permissões para:

- Descrever instâncias EC2;
- Encerrar instâncias EC2;
- Consultar regiões;
- Criar grupos de logs;
- Criar streams de logs;
- Registrar eventos no CloudWatch.

📷 *Inserir print da política criada.*

---

## 2. Criação da Role IAM

Foi criada uma Role destinada ao serviço Lambda.

Durante a configuração foi anexada a política criada anteriormente, permitindo que a função tivesse autorização para interagir com os recursos EC2.

📷 *Inserir print da Role criada.*

---

## 3. Criação da função Lambda

Foi criada uma função utilizando:

| Configuração | Valor |
|--------------|-------|
| Runtime | Python 3.13 |
| Tipo | Criar do zero |
| Execution Role | Role personalizada criada anteriormente |

📷 *Inserir print da criação da função.*

---

## 4. Upload do código Python

Foi realizado o upload do arquivo compactado contendo o script responsável pela automação da terminação das instâncias EC2.

Após o envio do arquivo, foi realizado o Deploy da função.

📷 *Inserir print do código carregado.*

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

📷 *Inserir print das configurações.*

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

📷 *Inserir print da regra criada.*

---

## 7. Validação

Após criar uma instância EC2 e aguardar o intervalo definido no EventBridge, a função Lambda foi executada automaticamente realizando a terminação da instância conforme esperado.

Os registros de execução podem ser acompanhados através do Amazon CloudWatch Logs.

📷 *Inserir print da execução.*

---

# 📊 Resultado

Ao final do laboratório foi construída uma solução totalmente automatizada para encerramento de instâncias EC2 utilizando arquitetura serverless.

Fluxo implementado:

- EventBridge agenda a execução;
- Lambda é acionado automaticamente;
- IAM concede as permissões necessárias;
- Lambda localiza e encerra as instâncias EC2;
- CloudWatch registra toda a execução.

---

# 💡 Boas práticas

Durante o laboratório foi possível compreender conceitos importantes relacionados à automação na AWS.

Entre eles:

- princípio do menor privilégio (Least Privilege);
- automação de tarefas administrativas;
- utilização de arquitetura serverless;
- redução de custos com desligamento automático de recursos;
- monitoramento através do CloudWatch;
- uso do EventBridge para execução baseada em tempo.

---

# 📚 Aprendizados

Este laboratório demonstrou como integrar diferentes serviços da AWS para criar uma solução de automação utilizando computação serverless.

Além do desenvolvimento da função Lambda em Python, foi possível compreender como as permissões do IAM, os gatilhos do EventBridge e o CloudWatch trabalham em conjunto para executar tarefas administrativas automaticamente, reduzindo esforço operacional e contribuindo para um melhor controle dos recursos em nuvem.

---

## 📎 Referências

- AWS Lambda
- Amazon EventBridge
- AWS IAM
- Amazon EC2
- Amazon CloudWatch
- Documentação oficial da AWS
