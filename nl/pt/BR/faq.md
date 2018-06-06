---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Perguntas mais Frequentes

Esta FAQ fornece respostas às perguntas comuns sobre o serviço {{site.data.keyword.appid_full}}.
{: shortdesc}


## Como o {{site.data.keyword.appid_short_notm}} calcula os preços?
{: #pricing}

Com o {{site.data.keyword.appid_short_notm}}, você paga menos à medida que usa mais recursos.
{: shortdesc}

O plano de camada graduado consiste em duas partes: o número de eventos de autenticação e o número de usuários autorizados. Você é cobrado a cada mês, com base no resumo das duas partes. O preço total é o encargo acumulativo para cada nível de uso, consistindo em sua quantidade multiplicada pelo preço unitário na respectiva camada.

### Eventos de autenticação

Um evento de autenticação ocorre quando um novo token do {{site.data.keyword.appid_short_notm}} é emitido. Para usuários identificados, cada novo token é válido por uma hora. Os tokens são válidos por um mês para usuários anônimos. Após o token expirar, deve-se criar um novo token para acessar recursos protegidos. Quando você usa o ID do app para autenticação móvel, os tokens do usuário são armazenados em `key-store/key-chain` e são incluídos em cada solicitação futura. Os tokens são acessíveis usando o SDK Swift Android ou iOS do {{site.data.keyword.appid_short_notm}}. Ao usar o serviço para autenticação da web, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">armazene o token do usuário <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> nos cookies de sessão.

### Usuários autorizados

Um usuário autorizado é um usuário exclusivo que efetua login com seu serviço, direta ou indiretamente. Você é cobrado por um usuário autorizado toda vez que um novo usuário efetua login de cada provedor de identidade, incluindo usuários anônimos. Por exemplo, se um usuário efetuar login com o Facebook e depois efetuar login usando o Google, ele será considerado como dois usuários autorizados separados.

Para obter mais informações sobre precificação de camada graduada, veja os [docs de precificação do {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>

## Que tipo de atividade é monitorado pelo ID do app?
{: #activity-monitor}

É possível rastrear a atividade que foi gerada no app que está ligado à instância de serviço. Também é possível monitorar a atividade administrativa feita no ID do app usando o serviço Activity Tracker.

Para visualizar a atividade gerados por seu app:

1. Efetue login na sua conta do IBM Cloud.
2. No painel, selecione sua instância do ID do app.
3. Clique na guia **Visão geral**.
4. Visualizar a atividade listada no **Log de atividades**.

</br>
Para monitorar a atividade administrativa:

1. Efetue login na sua conta do IBM Cloud. Navegue para a organização e o espaço no qual sua instância de ID do app é provisionada.
2. No catálogo, provisione uma instância do serviço Activity Tracker. Certifique-se de que você esteja no mesmo espaço que sua instância de ID do app.
3. No painel Activity Tracker, clique na guia **Gerenciar**.
4. Na lista suspensa, selecione as configurações a seguir para procurar quaisquer eventos que foram gerados pelo ID do app.
<table>
  <tr>
    <th> Campo </th>
    <th> Configuração </th>
  </tr>
  <tr>
    <td><i>Visualizar Logs</i></td>
    <td><b>Logs de espaço</b></td>
  </tr>
  <tr>
    <td><i>Search</i></td>
    <td><b>target.name</b></td>
  </tr>
  <tr>
    <td>Filtro</td>
    <td>appid</td>
  </tr>
</table>
5. Clique em **Filtrar**.

Consulte os [docs do Activity Tracker](/docs/services/cloud-activity-tracker/index.html) para obter mais informações sobre como o serviço funciona.
