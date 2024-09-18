## Hi there 👋

## Resumo do Projeto

Este projeto é parte do MBA da FIAP e envolve a criação de uma infraestrutura na AWS utilizando Terraform, incluindo a configuração de VPC, EKS, RDS, API Gateway e Lambda. A aplicação principal é uma API de gerenciamento de pedidos desenvolvida em Java, que é implantada em um cluster Kubernetes.

## Passo a Passo para Subir Tudo via Pipeline

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

### 4. API Gateway

1. **Execute o pipeline de API Gateway**:
   - O pipeline irá executar `terraform apply` para provisionar o API Gateway.

## Não esqueca de executar a pipe de Terraform Destroy localizado no repo de "infra" no qual destroy todos os passos anteriores
