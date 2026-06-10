
# Explorando a AWS com o Amazon EC2

Neste laboratório foi realizada uma introdução prática ao Amazon EC2, explorando a criação e o gerenciamento de instâncias tanto pelo Console de Gerenciamento da AWS quanto pelo AWS CloudShell.

O Amazon EC2 (Elastic Compute Cloud) é um serviço de computação em nuvem que permite criar máquinas virtuais sob demanda. Essas instâncias funcionam de forma semelhante a computadores físicos e podem ser utilizadas para hospedar aplicações, sites, APIs, bancos de dados e diversos outros serviços. O EC2 foi projetado para fornecer escalabilidade e provisionamento rápido de recursos computacionais na nuvem.

---

# Objetivos do laboratório

- Criar uma instância EC2 de teste utilizando o Console da AWS.
- Configurar regras de segurança para permitir acesso via HTTP.
- Provisionar uma segunda instância EC2 utilizando comandos no AWS CloudShell.
- Encerrar as instâncias criadas ao final do laboratório.

---

# Arquitetura

<p align="center">
  <img width="532" height="501" alt="EC2-arquitetura" src="https://github.com/user-attachments/assets/ea3a03b7-f293-4cbc-ba94-973442981a6a" />
</p>


## Criação da instância EC2 via Console AWS

Nesta etapa foi realizada a criação de uma instância EC2 utilizando o Console de Gerenciamento da AWS. A instância foi configurada com a imagem Amazon Linux 2023 e o tipo t2.micro.

<img width="1283" height="518" alt="image" src="https://github.com/user-attachments/assets/54e94050-7dde-4c6c-924a-b71ffcec230f" />



Durante a configuração, foi criado um novo par de chaves `.pem` para acesso seguro à instância e também um Security Group permitindo tráfego HTTP para acesso ao servidor web.

Além disso, foi utilizado um script de User Data para automatizar a instalação e inicialização do Apache HTTP Server (`httpd`), criando automaticamente uma página web simples hospedada na instância.

### Script utilizado no User Data

```bash
#!/bin/bash

dnf install -y httpd

systemctl enable --now httpd

echo '<html><h1>Olá do seu servidor web!</h1></html>' > /var/www/html/index.html
```

### Evidências da execução

* Configuração da instância EC2
* Criação do par de chaves
* Configuração do Security Group
* Execução do User Data
* Página web acessível via HTTP

## Validação da instância e teste do servidor web

Após a inicialização da instância EC2, foi realizado o acompanhamento do status da máquina até que todas as verificações de integridade fossem concluídas com sucesso.

Em seguida, foi identificado o endereço IPv4 público da instância para realizar o teste de conectividade via navegador.

Com o acesso HTTP liberado no Security Group e o script de User Data executado corretamente, o servidor web pôde ser acessado utilizando o IP público da instância, exibindo a página criada automaticamente durante a inicialização do ambiente.

<img width="621" height="362" alt="image" src="https://github.com/user-attachments/assets/0a0ba8d4-caaf-41da-ae1a-39202a3c0862" />



### Evidências da execução

* Instância EC2 em execução
* Status checks aprovados
* Endereço IPv4 público
* Teste de acesso HTTP via navegador
* Página web retornando corretamente

  


