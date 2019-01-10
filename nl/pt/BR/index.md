---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Tutorial de Introdução
{: #gettingstarted}

A segurança do aplicativo pode ser muito complicada. Para a maioria dos desenvolvedores, é uma das partes mais difíceis da criação de um app. Como é possível ter certeza de que você está protegendo suas informações sobre o usuário? Ao integrar o {{site.data.keyword.appid_full}} em seus aplicativos, é possível proteger os recursos e incluir a
autenticação, mesmo quando você não tem muita experiência em segurança.
{: shortdesc}

Requerendo que os usuários se conectem ao seu app, é possível armazenar dados do usuário, como preferências de app ou informações dos perfis sociais públicos, e então usar esses dados para customizar cada experiência de seu app. O {{site.data.keyword.appid_short_notm}} fornece uma estrutura de login para você, mas também é possível trazer
suas próprias telas de conexão com marca ao trabalhar com o Cloud Directory.

Adoraríamos a sua participação com feedback e perguntas!
* Se você tiver perguntas técnicas sobre o {{site.data.keyword.appid_short_notm}}, poste sua pergunta no
<a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e identifique-a com
`ibm-appid`.
* Para perguntas sobre o serviço e instruções de introdução, use o fórum <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Inclua a tag `appid`.

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

Prontos para utilização, os aplicativos de amostra são configurados com dois provedores de identidade e a capacidade de revisar a autenticação. Os apps de amostra são oferecidos no `iOS Swift`, `Android`, `Node.js` e `Java`. Se
você não vir um idioma no qual se sinta confortável para trabalhar, não se preocupe. É possível integrar o {{site.data.keyword.appid_short_notm}} em seu próprio aplicativo de amostra usando as APIs fornecidas.

Para construir um aplicativo de amostra:

1. Clique em **Fazer download de amostra**.
2. Clique no idioma de sua opção para fazer download da amostra.
  Não está vendo o idioma que procura? Não se preocupe! É possível tirar vantagem do {{site.data.keyword.appid_short_notm}} por meio das APIs. Também é possível conferir <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">nossos
blogs <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"> </a> para obter ajuda extra em outros
idiomas.
  {: tip}
3. Certifique-se de que você tenha os pré-requisitos instalados ou concluídos.
4. Siga as etapas **Construir e executar** para configurar sua amostra com o {{site.data.keyword.appid_short_notm}}.
5. Clique em **Revisar atividade** para ver quaisquer eventos de autenticação que ocorreram. Qualquer
tipo de conexão cria um evento que é visível nessa página.
6. Customize o widget de conexão.
  1. Inclua uma imagem, como um logotipo de marca, clicando em **Selecionar** e navegando em seu
sistema local para obter uma imagem para fazer upload.
  2. Escolha um esquema de cores selecionando uma das opções de cor ou especificando em um valor hexadecimal.
  3. Mude entre a web e o dispositivo móvel para ver como o esquema de cores se parece em cada tipo de dispositivo.
  4. Quando você estiver satisfeito com suas opções, clique em **Salvar mudanças**.
7. Em um navegador, atualize sua página de login. As mudanças feitas na etapa anterior já estão visíveis.


## Próximas Etapas
{: #next}

Pronto para entrar e começar seus próprios aplicativos? Inicie [incluindo o
serviço no seu aplicativo](web-apps.html). O serviço fornece SDKs para os idiomas mais usados, mas, se você não vir um
SDK para o idioma em que seu aplicativo é escrito, ainda será possível aproveitar o
{{site.data.keyword.appid_short_notm}} usando as APIs.

</br>
</br>
