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

<h1> Instalando Terraform </h1>

<i>Essa processo de instalação é descrito para ambiente Linux (Ubuntu/Debian). Mais opções de instalação podem ser encontradas na documentação oficial do [Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)</i>

<hr class="solid">

<p>
    Certifique-se de que seu sistema está atualizado e que você instalou os pacotes gnupg, software-properties-common e curl. Você usará esses pacotes para verificar a assinatura GPG da HashiCorp e instalar o repositório de pacotes Debian da HashiCorp.
</p>

```bash
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
```

<p>
    À partir disso, é necessário instalar a Chave GPG do HarshCorp por meio do seguinte comando:
</p>

```bash
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
```

<p>
    Caso queira verificar a impressão digital da chave, apenas execute:
</p>

```bash
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint

```

<p>
    O retorno esperado:
</p>

```
/usr/share/keyrings/hashicorp-archive-keyring.gpg
-------------------------------------------------
pub   rsa4096 XXXX-XX-XX [SC]
AAAA AAAA AAAA AAAA
uid           [ unknown] HashiCorp Security (HashiCorp Package Signing) <security+packaging@hashicorp.com>
sub   rsa4096 XXXX-XX-XX [E]
```

<p>
    Adicione o repositório oficial da HashiCorp ao seu sistema. O comando lsb_release -cs encontra o codinome da versão de distribuição para o seu sistema atual, como buster, groovy ou sid.
</p>

```bash
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
```

<p>
    Por fim instale o Terraform executando:
</p>

```bash
sudo apt update && sudo apt-get install terraform
```

<hr class="bold">

<h1> Instalando AWS CLI </h1>

<i>Essa processo de instalação é descrito para ambiente Linux x86 (64-bit). Mais opções de instalação podem ser encontradas na documentação oficial da [AWS](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)</i>

<hr class="solid">

<p>
    Para intalar o CLI da AWS, basta executar o simples comando:
</p>

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

<p>
    Caso seja necessário atualizar sua instalação atual da AWS CLI, adicione seu symlink existente e as informações do instalador para gerar o comando de instalação usando os parâmetros --bin-dir, --install-dir e --update. O comando a seguir usa um exemplo de symlink em /usr/local/bin e um exemplo de localização do instalador em /usr/local/aws-cli.
</p>

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update
```

<h2> Credenciais AWS </h2>

<p>
    Para que seja possível utilizar o AWS CLI, é necessaŕio fazer a configuração das credenciais de acesso ao console da AWS. Executando o comando: aws configure
</p>

<p>
    Será necessário confirmar sua AWS Access Key ID, AWS Secret Access Key, região padrão e formato de saída (esse podendo ser default).
</p>

<p>
    Em seguida, configure o AWS Access Token diretamente no arquivo de credenciais, esse que por sua vez pode ser encontrado dentro da pasta (oculta) ` .aws ` que geralente se localiza na pasta pessoal. Procure por um arquivo chamado ` credentials ` (caso não exista, apenas crie um arquivo com esse mesmo nome e o modifique). Será necessário salvar suas credenciais nesse arquivo, tal como à seguir:
</p>

``` bash
[default]
aws_access_key_id = YOUR_ACCESS_KEY_ID
aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
aws_session_token = YOUR_SESSION_TOKEN
```

<i>Vale ressaltar que YOUR_ACCESS_KEY_ID, YOUR_SECRET_ACCESS_KEY e YOUR_SESSION_TOKEN devem ser substituidos por suas próprias credenciais que podem ser encontradas acessando seu console AWS.</i>

