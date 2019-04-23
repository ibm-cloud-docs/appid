---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: authentication, authorization, identity, app security, secure

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:faq: data-hd-content-type='faq'}


# Perguntas mais frequentes
{: #faq}

Esta Pergunta mais frequente fornece respostas às perguntas comuns sobre o serviço {{site.data.keyword.appid_full}}.
{: shortdesc}


## Como o {{site.data.keyword.appid_short_notm}} calcula os preços?
{: #faq-pricing}
{: faq}

Com o {{site.data.keyword.appid_short_notm}}, você paga menos à medida que usa mais recursos.
{: shortdesc}

O plano de camada graduada consiste em três partes: o número de eventos de autenticação, a segurança regular e avançada e o número de usuários autorizados. Você é cobrado a cada mês, com base no resumo das duas partes. O preço total é o encargo acumulativo para cada nível de uso, consistindo em sua quantidade multiplicada pelo preço unitário na respectiva camada.

Seus primeiros 1000 eventos de autenticação e os primeiros 1000 usuários autorizados são grátis a cada mês, exceto para qualquer evento de segurança avançado. Qualquer evento de segurança avançado incorre em encargo extra.

### Eventos de autenticação
{: #faq-authentication}

Um evento de autenticação ocorre quando um novo token de acesso, regular ou anônimo, é emitido. Os tokens podem ser
emitidos como uma resposta a uma solicitação de conexão que é iniciada por um usuário ou em nome do usuário por um
aplicativo. Por padrão, os tokens de acesso são válidos por uma hora e os tokens anônimos são válidos por 30 dias. Após o token expirar, deve-se criar um novo token para acessar recursos protegidos. É possível atualizar o prazo de expiração de seus tokens do {{site.data.keyword.appid_short_notm}} na página **Provedores de identidade > Gerenciar > Configurações de autenticação** do painel de serviço.

#### Recursos de segurança avançados

Os recursos de segurança avançados fornecem a capacidade de fortalecer a segurança de seu aplicativo.
{: shortdesc}

<table>
  <tr>
    <th>Recurso</th>
    <th>Benefício</th>
  </tr>
  <tr>
    <td>Autenticação de múltiplos fatores</td>
    <td>A [MFA para Cloud Directory](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) confirma a identidade de um usuário ao exigir que ele insira uma
senha descartável que é enviada para seu e-mail, além de inserir seu e-mail e senha.</td>
  </tr>
  <tr>
    <td>Gerenciamento de política de senha</td>
    <td>Como proprietário da conta, é possível impor senhas mais seguras para o Cloud Directory configurando um
conjunto de regras às quais as senhas do usuário devem estar em conformidade. Exemplos incluem o número de tentativas de conexão
antes do bloqueio de acesso, prazos de expiração, amplitude de tempo mínimo entre as atualizações de senha ou o
número de vezes que uma senha não pode ser repetida. Para obter uma lista completa das opções e informações de configuração, consulte [Gerenciamento de senha avançado](/docs/services/appid?topic=appid-cd-strength#cd-advanced-password).</td>
  </tr>
</table>

Por padrão, os recursos de segurança avançados são desativados. Se você ativar o MFA ou o gerenciamento de política de senha, incorrerá em um encargo extra. Se você desativar todos os recursos avançados, sua conta será revertida para a política de custo mais baixo. Por exemplo, se você obteve 10.000 tokens de acesso. Em seguida, você ativou o gerenciamento de política de senha e obteve mais 10.000. Você pagaria por 20.000 eventos de
autenticação e 10.000 eventos de segurança avançados.

Esses recursos estão disponíveis apenas para as instâncias que estão no plano de precificação de camada graduada e que foram criadas após 15 de março de 2018.
{: note}

### Usuários autorizados
{: #faq-authorized}

Um usuário autorizado é um usuário exclusivo que se conecta com o seu serviço, direta ou indiretamente, incluindo
usuários anônimos. Você é cobrado por um usuário autorizado cada vez que um novo usuário se conecta a seu aplicativo,
incluindo usuários anônimos. Por exemplo, se um usuário se conectar com o Facebook e, posteriormente, se conectar usando o
Google, ele será considerado como dois usuários autorizados separados.

Para obter as informações de precificação mais atualizadas, é possível criar uma estimativa de custo clicando em **Incluir para estimar** na seção {{site.data.keyword.appid_short_notm}} do [catálogo do {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/catalog/services/app-id).
{: tip}



## Por que eu preciso inserir meu URI de redirecionamento em uma lista de desbloqueio?
{: #faq-redirect}
{: faq}

Um URI de redirecionamento é o terminal de retorno de chamada de seu app. Para evitar ataques de phishing, o {{site.data.keyword.appid_short_notm}} valida o URI com relação à lista de desbloqueio de URIs de redirecionamento. Quando ocorre o phishing, a possibilidade de um invasor obter acesso aos tokens do usuário existe. Para obter mais informações sobre URIs de redirecionamento, consulte [Incluindo URIs de redirecionamento](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri).

Não inclua quaisquer parâmetros de consulta em sua URL. Eles são ignorados no processo de validação. URL de exemplo: `http://host:[port]/path`
{: tip}



## Como a criptografia funciona no  {{site.data.keyword.appid_short_notm}}?
{: #faq-encryption}
{: faq}

Verifique a tabela a seguir para obter respostas para as perguntas mais comuns sobre a criptografia.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Ícone de Mais informações"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Por que você usa criptografia?</td>
      <td>Uma maneira de proteger as informações de nossos usuários é criptografar os dados do cliente em repouso. O serviço
criptografa os dados do cliente em repouso com as chaves por locatário.</td>
    </tr>
    <tr>
      <td>Você construiu seus próprios algoritmos? Quais são os que você usa em seu código?</td>
      <td>Nós não construímos os nossos; o serviço usa o <code>AES</code> e o <code>SHA-256</code> com salting.</td>
    </tr>
    <tr>
      <td>Você usa módulos ou provedores de criptografia de origem pública ou de software livre? Você já expõe funções de criptografia? </td>
      <td>O serviço usa as bibliotecas Java <code>javax.crypto</code>, mas nunca expõe uma função de criptografia.</td>
    </tr>
    <tr>
      <td>Como você armazena as chaves?</td>
      <td>As chaves são geradas e criptografadas com uma chave mestra que é específica para cada região e, em seguida, armazenadas
localmente. As chaves mestras são armazenadas no  {{site.data.keyword.keymanagementserviceshort}}. Nos níveis de
armazenamento e de middleware, há criptografia de nível de serviço, o que significa que há uma chave para todos os
clientes. No nível do aplicativo, cada cliente tem sua própria chave de criptografia.</td>
    </tr>
    <tr>
      <td>Qual é a segurança da chave que você usa?</td>
      <td>O serviço usa 16 bytes.</td>
    </tr>
    <tr>
      <td>Você chama quaisquer APIs remotas que expõem os recursos de criptografia?</td>
      <td>Não, não temos.</td>
    </tr>
  </tbody>
</table>

