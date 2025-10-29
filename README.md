# Desafio: Implementando a Primeira Stack com AWS CloudFormation

Este repositório documenta o processo de aprendizado e implementação de uma stack básica na AWS utilizando CloudFormation

O objetivo foi aplicar os conceitos de Infraestrutura como Código (IaC) para provisionar recursos de forma automatizada e versionada.

## 1. 🎯 Objetivos do Projeto

* Aplicar conceitos de IaC com AWS CloudFormation.
* Criar um template em YAML para descrever a infraestrutura.
* Provisionar uma stack contendo:
    * Uma instância EC2 (servidor web).
    * Um Security Group (regras de firewall).
* Documentar o processo, insights e desafios encontrados.

## 2. 📖 Conceitos-Chave

AWS CloudFormation é um processo que auxilia na criação de recursos na AWS por meio de templates JSON ou YAML

* **Características**
- Pagamos apenas pelas stacks criadas.
- Além de ser um processo automatizado, conseguimos versionar estes templates.
  
* **Infraestrutura como Código (IaC):** É a prática de gerenciar e provisionar infraestrutura de TI (redes, máquinas virtuais, etc.) através de arquivos de definição legíveis por máquina (como o YAML), em vez de configuração manual.
* **AWS CloudFormation:** É o serviço da AWS que permite modelar, provisionar e gerenciar recursos da AWS e de terceiros tratando a infraestrutura como código.
* **Template:** O arquivo (JSON ou YAML) que descreve todos os recursos da AWS que você deseja criar e configurar.
* **Stack:** A instância de um template. É o conjunto de recursos que o CloudFormation cria, atualiza ou exclui com base no template.
* **Recursos (Resources):** A seção principal do template. É onde você declara os recursos da AWS que deseja criar (ex: `AWS::EC2::Instance`, `AWS::EC2::SecurityGroup`).

## 3. ⚙️ O Template (`template.yaml`)

Nosso template foi escrito em YAML, a seguir os trechos mais importantes:

```
01-EC2.yaml
Description: Criar um Amazon EC2 simples
Resources:
  MinhaInstancia:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-0ed9277fb7eb570c9
      InstanceType: t2.micro

02-Apache.yaml
Description: Instalar Servidor Apache
Resources:
  MinhaInstancia:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-0ed9277fb7eb570c9
      InstanceType: t2.micro
      Tags:
        - Key: "Name"
          Value: "Webserver"
      UserData:
        Fn::Base64:

03-Firewall.yaml
Description: Configurar Grupo de Segurança
Resources:
  MinhaInstancia:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-0ed9277fb7eb570c9
      InstanceType: t2.micro
      Tags:
        - Key: "Name"
          Value: "Webserver"
      UserData:
        Fn::Base64:
