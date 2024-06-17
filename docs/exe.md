<style>
    * {
        color: #F4F4F4;
    }

    h1 {
        color: #F4F4F4 !important;
        font-weight: bold !important;
    }

    h2 {
        color: #F4F4F4 !important;
        font-weight: bold !important;
    }

    i {
        color: #A6A6A6;
        font-weight: lighter;
    }
    
    p {
        margin-bottom: 20px;
    }

    code {
        background: #3a3d4b !important;
        color: #86c8c6 !important;
        border-radius: 5px !important;
        padding: .5rem !important;
    }

    .md-header {
        background: #1e1f29;
        animation: neonPulse 4s;
        animation-iteration-count: infinite;
    }

    body {
        background-image: linear-gradient(to bottom, #382f50, #332e4b, #2f2d46, #2b2c40, #282a3a);
        background-repeat: no-repeat;
        background-attachment: fixed;
        font-weight:light;
    }

    label.md-nav__title {
        display:none
    }

    hr.solid {
        border-top: 1px solid #bbb;
    }

    hr.bold {
        border-top: 3px solid #bbb;
    }

    @keyframes neonPulse {
        0% {
            box-shadow: 0px 0px 2px #ac4be5;
        }
        70% {
            box-shadow: 3px 3px 10px #ac4be5;
        }
        100% {
            box-shadow: 0px 0px 2px #ac4be5;
        }
    }

</style>

<h1> Terraform para criar uma instância EC2</h1>

<p> Primeiramente, será necessário criar um arquivo de configuração Terraform chamado main.tf no diretório do seu projeto com o seguinte conteúdo:</p>

```
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-0c02fb55956c7d316"  # Amazon Linux 2 AMI (HVM), SSD Volume Type
  instance_type = "t2.micro"

  tags = {
    Name = "TerraformExample"
  }
}
```

<p>
    Para executá-lo apenas utilize o comando ` terraform init ` onde esse arquivo se encontra. Já para conferir o que será criado, execute ` terraform plan `.
</p>

<p>
    Caso esteja tudo certo, basta utilizar o comando ` terraform apply ` e digitar "yes" quando for pedido para criar sua instância.
</p>

[![terraform apply](https://i.postimg.cc/SK2x33Fz/image.png)](https://postimg.cc/06vvJtN8)

[![aws EC2 created](https://i.postimg.cc/wTjHnZDT/image.png)](https://postimg.cc/yWtwZffw)

<h2> Deletando instâncias </h2>

<p>
    Para deletar instâncias criadas por meio do Terraform caso seja necessário, basta executar ` terraform destroy ` digite "yes" quando for pedido uma confirmação
</p>

[![terraform destroy](https://i.postimg.cc/SN8xpDyy/image.png)](https://postimg.cc/F7r4ybdq)

[![aws EC2 deleted](https://i.postimg.cc/gJsQDcSy/image.png)](https://postimg.cc/WFD5pVPt)