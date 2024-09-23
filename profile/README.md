## Hi there 👋

## Resumo do Projeto

Este projeto é parte do MBA da FIAP e envolve a criação de uma infraestrutura na AWS utilizando Terraform, incluindo a configuração de VPC, EKS, RDS, API Gateway e Lambda. A aplicação principal é uma API de gerenciamento de pedidos desenvolvida em Java, que é implantada em um cluster Kubernetes.

## Passo a Passo para Subir Tudo via Pipeline espere sempre uma pipe terminar para executar a outra

### 1. Infraestrutura (VPC - EKS)

1. **Inicialize o laboratório no AWS Academy.**
2. **Crie um bucket S3** para armazenar o estado do Terraform. O nome do bucket deve ser "bucketterraformfiap".
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

### 4. Authorizer lambda

1. **Execute o pipeline do authorizer-lambda**:
   - O pipeline irá executar `terraform apply` para provisionar a lambda de authenticação.

### 5. Cognito

1. **Execute o pipeline do Cognito**:
   - O pipeline irá executar `terraform apply` para provisionar o cognito.
  

### 6. API Gateway

1. **Execute o pipeline de API Gateway**:
   - O pipeline irá executar `terraform apply` para provisionar o API Gateway.

## Utils

1. **configurar o aws cli**:
  - aws lambda delete-function --function-name techchallenge-authorizer-lambda

2. **obter o endereço do api gateway**:
  - aws apigatewayv2 get-apis

3. **Montar url para realizar login no cognito**:
  - https://<url_do_cognito>/login?response_type=code&client_id=<client_id>&redirect_uri=https://google.com
  - url_do_cognito = Entrar na aws na aba Cognito na aba de domains
  - client_id = Entrar na aws na aba Cognito na aba de domains no final vai ter o client_id
   
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

## Não esqueca de executar a pipe de Terraform Destroy localizado no repo de "infra" no qual destroy todos os passos anteriores











