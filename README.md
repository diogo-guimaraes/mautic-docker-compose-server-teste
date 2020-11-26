Instação do Mautic via docker-compose

#### O que é tratado neste docker-compose.yml:

* Configuração de contêineres mysql e mautic
* Configuração do contêiner traefi
#### Como usar:

1. run ```docker-compose up``` neste diretório
2. acesse https://mautic.local
3. passe pela configuração do Mautic (preencha `` `mauticdbpass``` como senha do mysql na página de configuração do banco de dados
4. teste o Mautic

# Mautic

## Ambientação e instalação

### Ambientação
----------------

#### Passo 1 - clonando o repositório do Mautic
-----------------------------------------------
1. Para instalação em local e fora do docker
Utilizando o git bash, clone o repositório mautic no seu ambiente de desenvolvimento, executando o seguinte comando:

```sh
$ git clone -b staging https://github.com/mautic/mautic.git mautic
```

#### Passo 2 - instalando o composer
-------------------------------------
1. Para instalação em local e fora do docker
Inicie o git bash dentro da pasta clonada do mautic e execute o seguinte comando:

```sh
$ composer install
```

#### Passo 3 - configurando o PHP
----------------------------------
1. Para instalação em local e fora do docker
* Abra o arquivo php.ini localizado na pasta do seu PHP
* Busque pelo paramentro: max_execution_time
* Mude o valor para 300

### Instalação

#### Passo 1 - iniciando a instalação do Mautic
--------------------------------------------------
Utilizando o browser, com o apache ativado, acesse a pasta do projeto Mautic  através do seguinte caminho:

```sh
https://localhost/mautic/
```

 A instalação será iniciada

* EM MAUTIC INSTALLATION - CHECK

Apenas clique em => Next Step

#### Passo 2 - configurando o banco de dados
--------------------------------------------

```shell
 Database driver: Matenha a opção Mysql PDO.
 Database host: "localhost"
 Database port: "3306"
 Database name: "mautic"
 Database Table Prefix: "mautic_"
 Database Username: "root"
 Database Password: "" (Campo vazio - para quem não usa senha no localhost)  
 back up existing?: "No"
```

Apenas clique em => Next Step
  
#### Passo 3 - criando usuário para acesso ao Munic
---------------------------------------------------

```shell
Admin username: "admin"
Admin password: "mautic"
Database port: "3306"
First name: "Nome"
Last name: "Sobrenome"
E-mail: "seuemail@exemplo.com"
```

Apenas clique em => Next Step

#### Passo 4 - configurando e-mail
----------------------------------

```shell
How Shold the email be sent as?: "Nome Completo"
E-mail: "seuemail@exemplo.com"
E-mail handling: "send immediately"
Mailer transport: "PHP Mail"
```
Apenas clique em => Next Step

## Configuração interna

### Alterarando avatar

Subir uma foto no https://br.gravatar.com/ com o mesmo emaiil que usou no cadastro do mautic  

### Alterando o idioma

Após alterar o idioma, aplicar e salvar, se o idioma não atualizar:

* faça logout
* No terminal, na pasta do projeto execute

```shell
php app/console cache:clear"
```

### Testando API Mautic

1. Instale o Postman na sua máquina

2. Após instalar o Postman você deve criar um novo request para autenticar o Mautic.

![](https://atendimento.hotmart.com.br/hc/article_attachments/360009112032/mceclip0.png)

3. Na nova tela, dê um nome para o request e salve em uma coleção.

Como você irá criar um request para puxar os contatos do Mautic, você pode chamá-lo de Mautic-List-Contacts. 

![](https://atendimento.hotmart.com.br/hc/article_attachments/360009147911/mceclip1.png)

Agora vem o passo importante! Autentique o seu cliente do Postman com o Mautic para obter um token de API. Para isso você deve:

4. Clicar na aba Authorization

5. No Menu Type, escolha a opção OAuth 2.0

![](https://atendimento.hotmart.com.br/hc/article_attachments/360009148231/mceclip2.png)

6. Na nova tela, clique no botão Get New Access Token

![](https://atendimento.hotmart.com.br/hc/article_attachments/360009161651/mceclip8.png)

)

7. Antes de preencher a próxima tela, acesse o Mautic e crie uma nova credencial.

8. Acesse a sua instalação do Mautic e escolha opção API Credentials no menu direito:

![](https://atendimento.hotmart.com.br/hc/article_attachments/360009161651/mceclip8.png)

9. Para criar uma nova credencial, clique no botão New:

![](https://atendimento.hotmart.com.br/hc/article_attachments/360009124852/mceclip5.png)

10. Escolha o protocolo OAuth 2.0 e preencha os campos Nome e Redirect URL com as informações abaixo:

Importante: O campo Callback URL deverá ser:

https://app.getpostman.com/oauth2/callback

![](https://atendimento.hotmart.com.br/hc/article_attachments/360009124892/mceclip6.png)

11. Copie os campos Public Key e Secret Key 

12. Volte ao Postman e preencha a próxima tela:

Importante:

O campo Callback URL deverá ser: https://app.getpostman.com/oauth2/callback
Não esqueça de mudar os campos Auth URL e Access Token URL para o domínio onde o seu mautic está instalado. Mantenha o sufixo /oauth/v2/...
Preencha os campos Client ID e Client Secret com os dados acessados no Mautic da tela anterior.

![](https://atendimento.hotmart.com.br/hc/article_attachments/360009161551/mceclip7.png)

13. Clique no botão Request Token.

14. Na próxima tela uma janela do Mautic irá aparecer. Aqui você deve logar com o seu usuário e senha cadastrados no Mautic.

15. Após fazer o login no Mautic você será redirecionado novamente para o Postman.

Se tudo der certo você já terá o seu API Token prontinho para usar! Nesse caso a integração foi um sucesso e parece que está tudo ok com o seu Mautic!

## Testando uma chamada de API no Mautic

1. Após os passos acima, clique em Use Token para testar uma chamada de API. 

![](https://atendimento.hotmart.com.br/hc/article_attachments/360009125552/mceclip9.png)

Para fazê-lo, vamos usar o Token de API para listar os contatos do Mautic utilizando a sua API.

2. Clique em Preview Request para usar o Token que acabamos de gerar

![](https://atendimento.hotmart.com.br/hc/article_attachments/360009162051/mceclip10.png)

3. Veja que o campo Authentication na aba Headers estará preenchido com o token que acabamos de gerar.

4. Preencha a URL que queremos chamar: http://meu.mautic.com.br/api/contacts

Importante: Não esqueça de trocar “meu.mautic.com.br” para o domínio onde o seu Mautic está instalado! 

5. Clique em Send e veja a magia acontecer!

 Se tudo der certo, a API do seu Mautic está configurada e você verá o resultado abaixo: Uma lista de seus contatos cadastrados retornada no formato JSON.

![](https://atendimento.hotmart.com.br/hc/article_attachments/360009125712/mceclip11.png)