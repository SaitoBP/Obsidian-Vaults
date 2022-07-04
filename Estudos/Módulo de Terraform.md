---
Tags:
- Terraform
---
# Módulo de Terraform
Um modulo é um container para multiplos recursos que são utilizados em conjunto. Módulos podem ser usados para criar abstrações leves, para que seja possivel descrever a infraestrutura em termos de arquitetura, ao inves de diretamente descrever em termos de objetos fisicos
O arquivo ``.tf`` dentro do diretorio de trabalho, quando executado o comando ``terraform plan`` ou ``terraform apply``, formam o modulo *root*. Este modulo pode chamar outros modulos e conecta-los passando valores de saida para outros modulos como valore de entrada

## Módulos com [[CI/CD]] no GitHub
O seguinte exemplo sera executado usando a Cloud da [[AWS]]


# Referencias
[Terraform](https://www.terraform.io/language/modules/develop)
[Terraform + CI/CD](https://churrops.io/2018/06/05/terraform-ecs-codepipeline-realizando-deploy-de-containers-na-aws-com-ci-cd/)