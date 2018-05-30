---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Tutorial de Introdução
{: #gettingstarted}

A segurança do aplicativo pode ser muito complicada. Para a maioria dos desenvolvedores, é uma das partes mais difíceis na criação de um app. Como é possível ter certeza de que você está protegendo suas informações sobre o usuário? Integrando o ID do app do IBM® Cloud em seus apps, é possível proteger recursos e incluir autenticação; mesmo quando você não tem muita experiência de segurança.
{: shortdesc}

Requerendo que os usuários se conectem ao seu app, é possível armazenar dados do usuário, como preferências de app ou informações dos perfis sociais públicos, e então usar esses dados para customizar cada experiência de seu app. O ID do app fornece um log na estrutura para você, mas também é possível trazer suas próprias telas de conexão com marca ao trabalhar com o diretório da nuvem.


Como um proprietário da conta, agora é possível configurar políticas que definem como os membros de sua equipe podem interagir com instâncias do {{site.data.keyword.appid_short_notm}}. É possível decidir quem pode criar, atualizar e excluir instâncias do serviço. Para obter mais informações, veja [Gerenciamento de acesso ao serviço](/docs/services/appid/iam.html).
{:tip}

## Criando uma instância de serviço
{: #create}

Crie e ligue uma instância do {{site.data.keyword.appid_short_notm}} ao seu app para começar.
{: shortdesc}

1. No catálogo do {{site.data.keyword.Bluemix}}, selecione {{site.data.keyword.appid_short_notm}}. A tela de configuração de
serviço é aberta.
2. Dê à sua instância de serviço um nome ou use o nome predefinido.
3. Selecione o seu plano de precificação e clique em **Criar**.
4. Ligar sua instância do {{site.data.keyword.appid_short_notm}}.
    1. Para ver uma lista de apps que podem ser ligados à sua instância de serviço, clique em **Conexões**.
    2. Clique em **Criar conexão**. Uma página é aberta com todos os apps que você tem a opção de ligar.
    3. Clique em **Conectar** no app que você deseja ligar.
    4. Clique em **Remontar** para aplicar a mudança.

É isso! Você está pronto para começar a definir suas configurações do aplicativo.


## Configurando um aplicativo de amostra
{: #sample-app}

É possível usar um dos aplicativos de amostra pré-configurados para familiarizar-se em trabalhar com o serviço.
{: shortdesc}

Prontos para utilização, os aplicativos de amostra são configurados com dois provedores de identidade e a capacidade de revisar a autenticação. Também é possível usar o recurso de widget de login para customizar uma página de conexão e ver a rapidez com que as atualizações feitas são mostradas em seu app.

Para configurar um aplicativo de amostra na GUI:

1. Depois de criar uma instância do serviço, é possível escolher um aplicativo de amostra em uma linguagem na qual você se sente confortável em trabalhar. É possível escolher por meio do iOS Swift, Android, Node.js e Java. Não deseja usar um SDK? Veja este exemplo para começar <a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">a usar o {{site.data.keyword.appid_short_notm}} com outras linguagens, como Python <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
2. Siga as etapas na GUI para **Construir e executar** seu aplicativo de amostra. Cada linguagem é configurada um pouco diferente, portanto, certifique-se de selecionar a linguagem do app que você transferiu por download na lista suspensa. Uma vez que seu app esteja configurado, é possível abri-lo em um navegador e efetuar login usando suas credenciais. Certifique-se de que os pré-requisitos para sua linguagem do app estejam instalados.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 25 ou superior </li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools versão 25.0.2 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods (versão 1.1.0 ou superior) </li><li> iOS 9 ou superior </li><li> MacOS 10.11.5 </li><li> Xcode (versão 9.0.1 ou superior) </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> A CLI do Cloud Foundry </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> A CLI do Cloud Foundry </li><li> Maven </li></ul></dd>
  </dl>
3. Clique em **Revisar atividade** para ver os eventos de autenticação que ocorreram. Depois de efetuar login, é possível ver um evento.
4. Customize sua experiência de login. É possível selecionar uma imagem, como seu logotipo e uma cor de cabeçalho. É possível selecionar uma das opções de cor ou inserir um valor hexadecimal. Quando estiver satisfeito com a visualização, clique em **Salvar mudanças**.
5. Em seu navegador, atualize sua página de login. As mudanças feitas na etapa anterior já estão visíveis.
