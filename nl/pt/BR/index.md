---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Tutorial Introdução
{: #gettingstarted}

O {{site.data.keyword.appid_full}} ajuda você a incluir autenticação em seus apps móveis e da web e protege seus recursos de backend.
{: shortdesc}

## Criando uma instância de serviço
{: #create}

Crie uma instância do {{site.data.keyword.appid_short_notm}} para começar.
{: shortdesc}

1. No catálogo do {{site.data.keyword.Bluemix}}, selecione {{site.data.keyword.appid_short_notm}}. A tela de configuração de
serviço é aberta.
2. Dê à sua instância de serviço um nome ou use o nome predefinido.
3. Para ligar a instância, selecione um app no menu **Conectar a**. Se você selecionar **Deixar desvinculado**,
será possível ligar a instância de serviço posteriormente.
4. Selecione o seu plano de precificação e clique em **Criar**.

## Configurando um aplicativo de amostra
{: #sample-app}

É possível usar um dos aplicativos de amostra pré-configurados para familiarizar-se em trabalhar com o serviço.
{: shortdesc}

Prontos para utilização, os aplicativos de amostra são configurados com dois provedores de identidade e a capacidade de revisar a autenticação. Também é possível usar o recurso de widget de login para customizar uma página de conexão e ver a rapidez com que as atualizações feitas são mostradas em seu app.

Para configurar um aplicativo de amostra na GUI:

1. Depois de ter criado a instância do serviço, é possível escolher um aplicativo de amostra em uma linguagem na qual você se sente confortável em trabalhar. É possível escolher por meio do iOS Swift, Android, Node.js e Java. Não deseja usar um SDK? Consulte o nosso blog sobre <a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">usar o {{site.data.keyword.appid_short_notm}} com outras linguagens, como Python <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
2. Siga as etapas na GUI para **Construir e executar** seu aplicativo de amostra. Cada linguagem é configurada um pouco diferente, portanto, certifique-se de selecionar a linguagem do app que você transferiu por download na lista suspensa. Uma vez que seu app esteja configurado, é possível abri-lo em um navegador e efetuar login usando suas credenciais.
  **Nota**: assegure-se de que você tenha os pré-requisitos instalados para a linguagem com a qual deseja trabalhar.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 25 ou superior </li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools versão 25.0.2 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods (versão 1.1.0 ou superior) </li><li> iOS 9 ou superior </li><li> MacOS 10.11.5 </li><li> Xcode 8.1 25.0.3+ </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> A CLI do Cloud Foundry </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> A CLI do Cloud Foundry </li><li> Maven </li></ul></dd>
  </dl>
3. Clique em **Revisar atividade** para ver os eventos de autenticação que ocorreram. É necessário ver pelo menos um evento se tiver efetuado login.
4. Customize sua experiência de login. É possível selecionar uma imagem, como seu logotipo e uma cor de cabeçalho. É possível selecionar uma das opções de cor ou inserir um valor hexadecimal. Quando estiver satisfeito com a visualização, clique em **Salvar mudanças**. É possível ver um exemplo do sinal de amostra na experiência na imagem a seguir.
5. Em seu navegador, atualize sua página de login. As mudanças feitas na etapa anterior já estão visíveis.
