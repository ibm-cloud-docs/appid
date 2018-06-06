---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Configurando provedores de identidade social
{: #setting-up-idp}

Provedores de identidade fornecem um nível extra de autenticação para seus apps móveis e da web. Com o {{site.data.keyword.appid_full}}, é possível configurar um ou vários provedores de identidade para configurar uma experiência de conexão única para seu app.
{: shortdesc}

## Configuração padrão
{: #default}

O {{site.data.keyword.appid_short_notm}} fornece uma configuração padrão para ajudar
com a configuração inicial dos provedores de identidade.
{: shortdesc}

As credenciais padrão são configuradas para o Facebook e o Google. Você tem o limite de 100 usos das
credenciais por instância, por dia. Como elas são credenciais da IBM, elas devem ser usadas em seus aplicativos somente no modo de desenvolvimento. Antes de publicar seu app, [atualize a configuração para as suas próprias credenciais](/docs/services/appid/identity-providers.html).


## Configurando o Facebook
{: #facebook}

É possível configurar o serviço {{site.data.keyword.appid_short}} para usar o Facebook
como um provedor de identidade.
{: shortdesc}

### Obtendo um ID do app e segredo por meio do Facebook

Para usar o Facebook como um provedor de identidade, deve-se incluir e configurar a plataforma
do website em seu aplicativo Facebook.

1. Efetue login em sua conta no <a href="https://developers.facebook.com/docs/apps/register" target="_blank">site do Facebook para desenvolvedores
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
2. Tome nota do ID e do segredo do app Facebook. Esses valores são necessários para configurar o seu projeto da web para autenticação em seu painel de serviço.
3. Inclua a plataforma da web e insira a URL do site.
4. Na lista de produtos, selecione **Login do Facebook**.
5. No campo URLs válidas de redirecionamento de OAuth, insira a URL de terminal de retorno de chamada de servidor de autorizações. Depois de configurar sua instância de serviço, é possível incluir esse valor.
6. Clique em **Salvar mudanças**.


### Configurando o {{site.data.keyword.appid_short_notm}} para autenticação do Facebook

Quando você tiver o seu ID e segredo do app Facebook e o seu app Facebook for Developers estiver configurado para entregar Web clients, será possível editar
a autenticação do Facebook em seu painel de serviço.

1. Na guia **Gerenciar** de seu painel de serviço, selecione **Facebook** e clique em **Editar**.
2. Insira o ID e segredo do app Facebook que você obteve por meio do website do Facebook for Developers.
3. Copie o URI que estiver no campo **URI de redirecionamento para o Facebook for Developers**. Cole o URI no campo **URIs válidos de redirecionamento de OAuth** na seção **Login do Facebook** do Portal de desenvolvedores do Facebook.
4. Clique em **Salvar**.
5. Opcional: para apps da web, insira a URL de redirecionamento no campo **URLs de redirecionamento de aplicativo da web**. Esse
valor é determinado pelo desenvolvedor e usado para acessar a URL de redirecionamento após o processo de autorização ser concluído.


## Configurando o Google
{: #google}

É possível configurar o serviço {{site.data.keyword.appid_short}} para usar o Google como um provedor de identidade.
{: shortdesc}

### Obtendo um identificador de cliente e segredo por meio do Google

Crie um projeto no <a href="https://developers.google.com/" target="_blank">Google Developers Console <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>, configure o projeto para atender
clientes da web e obtenha um segredo e um identificador de cliente.

1. Crie um projeto.
2. Inclua a API do Google+ em seu projeto do Google.
3. Inclua credenciais na API do Google+.
    1. Selecione a API do Google+ como o tipo de API.
    2. Selecione **Navegador da web** como o local do qual você chamará a API.
    3. Escolha **Dados do usuário**.
    4. Preencha os campos necessários para criar um identificador de cliente. Um segredo é criado ao mesmo tempo.
4. Tome nota do identificador de cliente e segredo do Google. Na guia de credenciais, selecione o
ID que você criou para obter o segredo e o identificador de cliente.

### Configurando o {{site.data.keyword.appid_short}} para autenticação do Google

Depois de ter configurado seu projeto do Google e ter seu segredo e seu identificador de cliente, será possível
editar seu painel de serviço para a autenticação do Google.

1. Na guia **Gerenciar** de seu painel de serviço, selecione **Google** e clique em **Editar**.
2. Insira o segredo e o identificador de cliente obtidos do Google Developers Console.
3. Autorize a URL do {{site.data.keyword.appid_short}}.
    1. Copie a **URL de redirecionamento para o Google Developer Console**
nos detalhes do provedor de identidade do Google.
    2. Na guia de credenciais do projeto do Google, selecione o identificador de cliente criado para essa integração.
    3. Cole a URL do {{site.data.keyword.appid_short}} no campo **URIs de
redirecionamento autorizados** e clique em **Salvar**.
4. Clique em **Salvar** para atualizar sua configuração do Google no {{site.data.keyword.appid_short}}.
5. Opcional: para apps da web, insira uma URL de redirecionamento na guia **Gerenciar**. Após a conclusão do processo de autorização, um usuário será enviado para essa URL.
