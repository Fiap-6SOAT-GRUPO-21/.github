## Hi there 👋

## Resumo do Projeto

Este projeto é parte do MBA da FIAP e envolve a criação de uma infraestrutura na AWS utilizando Terraform, incluindo a configuração de VPC, EKS, RDS, API Gateway e Lambda. A aplicação principal é uma API de gerenciamento de pedidos desenvolvida em Java, que é implantada em um cluster Kubernetes.

Todo provisionamento foi feito asssumindo-se que AWS Academy está sendo utilizado.  AWS Academy não permite a criação de IAM roles ou qualquer outro recurso relacioado a AWS IAM. Sendo assim, em todos os módulos é utilizado o role LabRole pre-existente na AWS Academy.


### Diagrama de Arquitetura (Fase 2)

Abaixo está o diagrama de arquitetura do projeto, que ilustra a estrutura e os componentes principais da aplicação:

![Diagrama de Arquitetura](image/tech_challenge_architecture.svg)

### Video de apresentação da arquitetura do projeto (Fase 2)

[![Video de Apresentação da Arquitetura](https://img.youtube.com/vi/7pZ2tByl9t8/0.jpg)](https://www.youtube.com/watch?v=7pZ2tByl9t8)

### Video de apresentação da arquitetura do projeto (Fase 3)

[![Video de Apresentação da Arquitetura](https://img.youtube.com/vi/MuOje_GppsU/0.jpg)](https://youtu.be/MuOje_GppsU)
### Estrutura do banco de dados (Fase 3)

![img.png](image%2Fimg.png)

### Documentação do banco de dados (Fase 3)

[PostgreSQL e RDS.pdf](..%2Fpdf%2FPostgreSQL%20e%20RDS.pdf)

### Tecnologias Utilizadas

- **Java 21**
- **Maven 3.8.6**
- **Spring Boot**
- **Hibernate**
- **ModelMapper**
- **Docker**
- **Kubernetes**
- **Postgres**
- **Terraform**
- **AWS**
- **API Gateway**
- **Lambda**
- **Cognito**
- **RDS**
- **VPC**

## Passo a Passo para Subir Tudo via Pipeline espere sempre uma pipe terminar para executar a outra

### 1. Infra

1. **Inicialize o laboratório no AWS Academy.**
2. **Crie um bucket S3** para armazenar o estado do Terraform. O nome do bucket deve ser "bucketterraformfiap". Ou altere o nome do bucket nas secrets da organização.
3. **Atualize as secrets da organização** com as credenciais obtidas no AWS Academy.
4. **Execute o pipeline de infraestrutura**:
   - O pipeline irá executar `terraform apply` para provisionar a VPC e o cluster EKS.
5. **Configure as credenciais do cluster EKS** na sua máquina:
   ```bash
   aws eks --region us-east-1 update-kubeconfig --name techchallenge

### 2. RDS

1. **Execute o pipeline de RDS**:
   - O pipeline irá executar `terraform apply` para provisionar a instância de RDS.
2. **Configure as credenciais do cluster EKS** na sua máquina:

### 3. API FOOD

1. **Execute o pipeline de API FOOD**:
   - O pipeline irá executar os comandos de kubectl apply para subir a aplicação.
2. **Com isso ja é possivel rodar os comandos de kubectl local**:     

### 4. Cognito

1. **Execute o pipeline do Cognito**:
   - O pipeline irá executar `terraform apply` para provisionar o cognito.

### 5. Authorizer lambda

1. **Execute o pipeline do authorizer-lambda**:
   - O pipeline irá executar `terraform apply` para provisionar a lambda de authenticação.


### 6. API Gateway

1. **Execute o pipeline de API Gateway**:
   - O pipeline irá executar `terraform apply` para provisionar o API Gateway.

## Utils

1. **configurar o aws cli**:
  - aws eks --region us-east-1 update-kubeconfig --name techchallenge

2. **obter o endereço do api gateway**:
  - aws apigatewayv2 get-apis

3. **Montar url para realizar login no cognito**:
  - https://<url_do_cognito>/login?response_type=code&client_id=<client_id>&redirect_uri=https://google.com
  - url_do_cognito = Entrar na aws na aba Cognito na aba de Integração da aplicação, em Domínio do Cognito
  - client_id = Entrar na aws na aba Cognito na aba de Integração da aplicação, em Análise e clientes de aplicação
   
3. **Login no Cognito com usuario defautl**:
  - username     = "Teste"
  - password     = "Teste123!"

3. **Obter Token**:
   - Ao ser redirecionado para o google ira um parametro "CODE" chame a req abaixo para obter o token
   - curl --location 'https://url_do_cognito/oauth2/token' \
      --header 'Content-Type: application/x-www-form-urlencoded' \
      --data-urlencode 'grant_type=authorization_code' \
      --data-urlencode 'code=CODE' \
      --data-urlencode 'redirect_uri=https://google.com' \
      --data-urlencode 'client_id=client_id'

4. **Todas as req é nescessario passar authorization retornado do passo 3**:

## Não esqueca de executar a pipe de Terraform Destroy localizado no repo de "infra" no qual destroy todos os passos anteriores











