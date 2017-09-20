---

copyright:
  years: 2017
lastupdated: "2017-06-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Configurando provedores de identidade
{: #setting-up-idp}

É possível configurar o Facebook, o Google, o IBMid ou uma combinação dos três para configurar uma experiência de conexão única para os seus usuários. Usando um provedor de identidade,
os usuários podem se conectar com credenciais com as quais já estejam familiarizados.
{:shortdesc}


## Configurando a autenticação do Facebook
{: #facebook}

Configure o serviço do {{site.data.keyword.appid_short}} para usar o Facebook como um provedor de identidade.


### Obtendo um ID do app e segredo por meio do Facebook
{: #getting-facebook-appid}

Para usar o Facebook como um provedor de identidade em seus apps móveis ou da web, deve-se incluir e configurar a plataforma do website em seu aplicativo
Facebook.

1. Efetue login em sua conta no <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Site do Facebook for
Developers<img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>.
2. Tome nota do ID e do segredo do app Facebook. Esses valores são necessários para configurar o seu projeto da web para autenticação em seu painel de serviço.
3. Inclua a plataforma da web e insira a URL do site.
4. Na lista de produtos, selecione **Login do Facebook**.
5. No campo URLs válidas de redirecionamento de OAuth, insira a URL de terminal de retorno de chamada de servidor de autorizações. Depois de configurar sua instância de serviço, é possível incluir esse valor.
6. Clique em **Salvar mudanças**.

### Configurando o {{site.data.keyword.appid_short_notm}} para autenticação do Facebook
{: #configuring-facebook-appid}

Quando você tiver o seu ID e segredo do app Facebook e o seu app Facebook for Developers estiver configurado para entregar Web clients, será possível editar
a autenticação do Facebook em seu painel de serviço.

1. Na guia **Gerenciar** de seu painel de serviço, selecione **Facebook** e clique em **Editar**.
2. Insira o ID e segredo do app Facebook que você obteve por meio do website do Facebook for Developers.
3. Copie o URI que estiver no campo **URI de redirecionamento para o Facebook for Developers**. Cole o URI no campo **URIs válidos de redirecionamento de OAuth** na seção **Login do Facebook** do Portal de desenvolvedores do Facebook.
4. Clique em **Salvar**.
5. Opcional: para apps da web, insira a URL de redirecionamento no campo **URLs de redirecionamento de aplicativo da web**. Esse
valor é determinado pelo desenvolvedor e usado para acessar a URL de redirecionamento após o processo de autorização ser concluído.


## Configurando a autenticação no Google
{: #google}

Configure o serviço do {{site.data.keyword.appid_short_notm}} para usar o Google como um provedor de identidade.


### Obtendo um identificador de cliente e segredo por meio do Google
{: #google-client-id}

Para usar o Google como um provedor de identidade, obtenha um identificador de cliente e segredo do Google e crie um projeto no Google Developer Console.

1. Abra o seu aplicativo Google no <a href="https://console.developers.google.com/apis/library" target="_blank">Google Developer Console
<img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>.
2. Inclua a API do Google+.
3. Crie credenciais usando o OAuth. No campo **Tipo de aplicativo**, selecione **Aplicativo da web**. No campo **URIs de redirecionamento autorizados**, insira o URI de redirecionamento do {{site.data.keyword.appid_short_notm}}. É possível obter o URI de autorização de redirecionamento do {{site.data.keyword.appid_short_notm}} por meio da tela de configuração do Google do painel de serviço.
4. Anote o identificador de cliente e o segredo do Google e salve as suas mudanças.



### Configurando o {{site.data.keyword.appid_short_notm}} para autenticação do Google
{: #google-client-appid}

Quando você tiver o seu identificador de cliente e segredo do Google e o seu console do Google Developers estiver configurado para entregar Web clients, será
possível editar a autenticação do Google em seu painel de serviço.

1. Na guia **Gerenciar** de seu painel de serviço, selecione **Google** e clique em **Editar**.
3. Insira o Identificador de cliente e Segredo do Google que você obteve por meio do console do Google Developers.
4. Copie o URI que estiver no campo **URI de redirecionamento para o Google for Developers**. Cole o URI no campo **URIs de redirecionamento autorizados** que estiver sob **Restrições** na seção **Identificador de cliente para aplicativo da web** do Portal de desenvolvedores do Google.
5. Clique em **Salvar**.
6. Opcional: para apps da web, insira o URI de redirecionamento no campo **URIs de redirecionamento de aplicativo da web**. Esse
valor é determinado pelo desenvolvedor e usado para acessar o URI de redirecionamento após o processo de autorização ser concluído.


## Configurando a autenticação do IBMid

Para usar o IBMid como um provedor de identidade, use o <a href="https://ibm.ent.box.com/notes/78040808400?v=IBMid-Federation-Guide" target="_blank">IBMid-Federation-Guide <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Se você já tiver um app BlueID, obtenha um identificador de cliente e um segredo do BlueID.


### Obtendo um identificador de cliente e um segredo do IBMid

Para obter um identificador de cliente e um segredo, use as etapas a seguir.

1. Em <a href="https://w3.innovate.ibm.com/tools/sso/home.html" target="_blank">Provedor de autoatendimento SSO <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>, efetue login na conta do BlueID.
2. Registre um app BlueID. Certifique-se de selecionar **pré-produção** ou **produção** para o provedor de identidade.
3. Em **Detalhes do cliente**, insira a URL de redirecionamento do ID do app. É possível obter o URI de autorização de redirecionamento da tela de configuração do IBMid de seu painel de serviço.
4. Certifique-se de que **Código de autorização** esteja selecionado.
5. Anote o identificador de cliente, o segredo e o tipo de provedor de identidade da conta do BlueID. Clique em **Continuar e concluir**.

### Configurando o ID do app para autenticação do IBMid

Quando você tiver o cliente e o segredo do BlueID e seu app BlueID estiver configurado com o URI de redirecionamento correto, será possível editar a seção de autenticação do BlueID de seu painel de serviço.

1. Na guia **Gerenciar** de seu painel de serviço, selecione **IBMid** e clique em **Editar**.
2. Insira o identificador de cliente e o segredo do BlueID.
3. Copie o URI que estiver no campo **URI de redirecionamento para o IBMid for Developers** e cole-o em **URIs de redirecionamento**. 
4. Selecione **pré-produção** ou **produção** para o provedor de identidade e clique em **Salvar**.
5. Opcional: para apps da web, insira o URI de redirecionamento no campo **URIs de redirecionamento de aplicativo da web**. Esse valor é determinado pelo desenvolvedor e usado para acessar o URI de redirecionamento após a autorização.
