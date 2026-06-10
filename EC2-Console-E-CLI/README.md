
# Explorando a AWS com o Amazon EC2

Neste laboratório foi realizada uma introdução prática ao Amazon EC2, explorando a criação e o gerenciamento de instâncias tanto pelo Console de Gerenciamento da AWS quanto pelo AWS CloudShell.

O Amazon EC2 (Elastic Compute Cloud) é um serviço de computação em nuvem que permite criar máquinas virtuais sob demanda. Essas instâncias funcionam de forma semelhante a computadores físicos e podem ser utilizadas para hospedar aplicações, sites, APIs, bancos de dados e diversos outros serviços. O EC2 foi projetado para fornecer escalabilidade e provisionamento rápido de recursos computacionais na nuvem.

---

# Objetivos do laboratório

- Criar uma instância EC2 de teste utilizando o Console da AWS.
- Configurar regras de segurança para permitir acesso via HTTP.
- Provisionar uma segunda instância EC2 utilizando comandos no AWS CloudShell.


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


## Provisionamento da instância via AWS CloudShell

Após a criação da instância pelo Console AWS, foi utilizado o AWS CloudShell para realizar o gerenciamento da infraestrutura por meio da AWS CLI.

O CloudShell permite executar comandos diretamente no ambiente AWS sem necessidade de instalação local, facilitando automações e gerenciamento de recursos em larga escala.

Nesta etapa, foram definidos parâmetros como:

* nome da instância
* nome do Security Group
* par de chaves utilizado no acesso SSH

Em seguida, foi criado um Security Group via linha de comando e configurada uma regra de entrada liberando tráfego HTTP na porta 80.

<img width="1065" height="420" alt="image" src="https://github.com/user-attachments/assets/310f4ccb-73a9-4a53-b952-460b81b736b3" />


### Comandos utilizados

```bash id="gfr3bo"
GRUPO_SEGURANCA="NomeSobrenome-grupo"

NOME_INSTANCIA="instancia-NomeSobrenome"

PAR_CHAVE="parchave-NomeSobrenome"
```

```bash id="r4em9y"
SECURITY_GROUP_ID=$(aws ec2 create-security-group \
--group-name $GRUPO_SEGURANCA \
--description "Permitir HTTP" \
--query "GroupId" \
--output text)
```

```bash id="efvjlwm"
aws ec2 authorize-security-group-ingress \
--group-id $SECURITY_GROUP_ID \
--protocol tcp \
--port 80 \
--cidr 0.0.0.0/0
```

### Evidências da execução

* Abertura do AWS CloudShell
* Configuração de variáveis via CLI
* Criação do Security Group
* Liberação de tráfego HTTP na porta 80
* Execução de comandos AWS CLI


 ## Criação da instância EC2 via AWS CLI

Na sequência, foi utilizada a AWS CLI dentro do CloudShell para provisionar uma nova instância EC2 diretamente por linha de comando.

O comando executado automatizou toda a criação da infraestrutura, incluindo:

* definição do tipo da instância
* utilização da AMI Amazon Linux 2023
* associação do Security Group criado anteriormente
* utilização do par de chaves configurado
* definição do nome da instância
* execução de um script de inicialização (User Data)

<img width="744" height="330" alt="image" src="https://github.com/user-attachments/assets/e926cde0-e210-4314-ab5e-3509c1ffe251" />


Além disso, o User Data foi responsável por instalar e iniciar automaticamente o Apache HTTP Server, disponibilizando uma página web simples acessível via navegador.

### Comando utilizado

```bash id="l1k0qx"
aws ec2 run-instances \
 --instance-type t2.micro \
 --image-id $(aws ssm get-parameters-by-path \
     --path "/aws/service/ami-amazon-linux-latest" \
     --query "Parameters[?ends_with(Name, 'al2023-ami-kernel-default-x86_64')].Value" \
     --output text) \
 --security-group-ids $SECURITY_GROUP_ID \
 --tag-specifications "ResourceType=instance,Tags=[{Key=Name,Value='$NOME_INSTANCIA'}]" \
 --key-name $PAR_CHAVE \
 --user-data "IyEvYmluL2Jhc2gKeXVtIC15IGluc3RhbGwgaHR0cGQKc3lzdGVtY3RsIGVuYWJsZSBodHRwZApzeXN0ZW1jdGwgc3RhcnQgaHR0cGQKZWNobyAnPGh0bWw+PGgxPk9sw6EgZG8gc2V1IHNlcnZpZG9yIHdlYiE8L2gxPjwvaHRtbD4nID4gL3Zhci93d3cvaHRtbC9pbmRleC5odG1sCg=="
```

### Validação da instância

Após o provisionamento, foi realizado o teste de conectividade utilizando o endereço IPv4 público da instância, validando o acesso HTTP ao servidor web criado automaticamente.

# Conclusão

Neste laboratório foi possível praticar a criação e o gerenciamento de instâncias EC2 tanto pelo Console da AWS quanto via AWS CloudShell utilizando AWS CLI.

Além do provisionamento das instâncias, também foram realizadas configurações de segurança, liberação de acesso HTTP e validação do servidor web em execução.




 

  


