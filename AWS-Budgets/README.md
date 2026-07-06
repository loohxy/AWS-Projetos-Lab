# 💰 Laboratório AWS - Criando um Orçamento com AWS Budgets

## 📖 Sobre o laboratório

Neste laboratório foi realizada a criação de um orçamento utilizando o serviço **AWS Budgets**, permitindo definir um limite de gastos para a conta AWS e configurar notificações automáticas por e-mail quando determinado percentual do orçamento for atingido.

Essa prática é fundamental para controlar custos na nuvem, especialmente durante estudos, laboratórios e ambientes de testes.

---

## 🎯 Objetivos

- Acessar o serviço **AWS Budgets** no Console AWS;
- Criar um orçamento personalizado;
- Definir um limite máximo de gastos;
- Configurar notificações automáticas por e-mail;
- Validar a criação do orçamento.

---

## 🛠️ Serviços utilizados

- AWS Budgets
- Amazon SNS (utilizado internamente para envio das notificações)
- AWS Management Console

---

## 🏗️ Arquitetura

> *(Insira aqui o diagrama da arquitetura utilizado no laboratório.)*

```
Usuário
    │
    ▼
AWS Management Console
    │
    ▼
AWS Budgets
    │
    ├──────────────► Monitoramento dos custos
    │
    ▼
Alerta configurado (10%)
    │
    ▼
E-mail de notificação
```

---

# 🚀 Etapas realizadas

## 1. Acessando o AWS Budgets

No Console AWS, acesse o serviço:

**Billing and Cost Management → Budgets**

Clique em:

**Create budget**

📷 *Inserir print da tela inicial do AWS Budgets.*

---

## 2. Criando um novo orçamento

Selecionar:

- **Customize (Advanced)**

Depois clicar em:

**Next**

Definir:

- Nome do orçamento
- Tipo de orçamento de custo

Exemplo:

```
meu-budget-lorena-carvalho
```

📷 *Inserir print da criação do orçamento.*

---

## 3. Definindo o valor do orçamento

Configurar:

| Campo | Valor |
|--------|-------|
| Budget Amount | **US$ 10** |

Depois clicar em **Next**.

📷 *Inserir print da definição do valor.*

---

## 4. Configurando o alerta

Adicionar um limite de alerta.

Configurações utilizadas:

| Campo | Valor |
|--------|-------|
| Threshold | 10 |
| Tipo | % do orçamento |
| Trigger | Actual |

Isso fará com que uma notificação seja enviada quando o consumo atingir **10%** do orçamento definido.

📷 *Inserir print da configuração do alerta.*

---

## 5. Configurando o e-mail

Informar o endereço de e-mail responsável por receber as notificações.

Após preencher:

- Next
- Next
- Create Budget

📷 *Inserir print da configuração do e-mail.*

---

## 6. Validação

Após a criação, o orçamento passa a aparecer na lista principal do AWS Budgets contendo informações como:

- Nome do orçamento
- Valor definido
- Valor utilizado
- Status

📷 *Inserir print da tela final mostrando o orçamento criado.*

---

# 📊 Resultado

O orçamento foi criado com sucesso.

Configuração utilizada:

- 💲 Limite: **US$ 10**
- 📧 Notificação por e-mail
- 🚨 Alerta configurado em **10%** do orçamento
- 📈 Monitoramento automático dos custos da conta

---

# 💡 Boas práticas

Durante o laboratório foi possível compreender a importância do AWS Budgets para o gerenciamento financeiro dos recursos em nuvem.

Entre os principais benefícios estão:

- evitar cobranças inesperadas;
- acompanhar os gastos em tempo real;
- receber alertas automáticos antes de ultrapassar o orçamento;
- facilitar o controle financeiro de ambientes de estudo e produção;
- incentivar o uso consciente dos recursos da AWS.

---

# 📚 Aprendizados

Este laboratório permitiu compreender como implementar uma estratégia simples de governança financeira utilizando o **AWS Budgets**.

Mesmo em ambientes de aprendizado, configurar orçamentos é uma prática recomendada, pois ajuda a monitorar custos continuamente e reduz o risco de gastos não planejados.

---

## 📎 Referências

- AWS Budgets
- AWS Billing and Cost Management
- Documentação oficial da AWS
