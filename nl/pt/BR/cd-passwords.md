---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

subcollection: appid

---

{:external: target="_blank" .external}
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

# Definindo políticas de senha
{: #cd-strength}

É possível configurar os requisitos para as senhas que podem ser usadas com o Cloud Directory. Ao definir requisitos específicos aos quais seus usuários devem aderir, é possível assegurar aplicativos mais seguros.
{: shortdesc}

## Política: força da senha
{: #cd-password-strength}

Uma senha forte torna difícil, ou mesmo improvável para alguém adivinhar a senha de uma maneira manual ou automatizada. Para configurar requisitos para a força da senha de um usuário, é possível usar as etapas a seguir.
{: shortdesc}

1. Acesse a guia **Políticas de senha** do painel do {{site.data.keyword.appid_short_notm}}.

2. Na caixa **Definir força da senha**, clique em **Editar**. Uma tela é aberta.

3. Insira uma sequência de expressão regular válida na caixa **Segurança da senha**.

  Exemplos:
    - Deve ter pelo menos 8 caracteres. (`^.{8,}$`)
    - Deve ter um número, uma letra minúscula e uma letra maiúscula. (`^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`)
    - Deve ter somente números e letras em inglês. (`^[A-Za-z0-9]*$`)
    - Deve ter pelo menos um caractere exclusivo. (`^(\w)\w*?(?!\1)\w+$`)

4. Clique em **Salvar**.

A força da senha pode ser configurada na página de configurações do Cloud Directory no console do {{site.data.keyword.appid_short_notm}} ou usando as <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex" target="_blank">APIs de gerenciamento <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
{: note}


## Políticas de senha avançadas
{: #cd-advanced-password}


É possível aprimorar a segurança de seu aplicativo utilizando restrições de senha.
{: shortdesc}


É possível criar uma política de senha avançada que consiste em qualquer combinação dos cinco recursos a seguir:

 - Bloqueio de acesso após credenciais erradas repetidas
 - Evitar reutilização de senha
 - Expiração de senha
 - Período mínimo entre mudanças de senha
 - Assegure-se de que a senha não inclua o nome do usuário


 Quando você ativa esse recurso, o faturamento extra para recursos avançados de segurança é ativado. Para obter mais informações, consulte [Como o {{site.data.keyword.appid_short_notm}} calcula a precificação](/docs/services/appid?topic=appid-faq#faq-pricing).
 {: important}


### Política: Evite reutilização de senha
{: #cd-avoid-reuse}

Quando os usuários estiverem mudando a senha, talvez você queira evitar que eles escolham uma senha usada
recentemente.
{: shortdesc}

Usando a GUI ou a API, é possível escolher o número de senhas que um usuário deve ter antes de poderem repetir uma senha usada anteriormente. As opções de configuração incluem qualquer valor inteiro no intervalo de 1 a 10.

Se essa opção for ativada, um usuário não poderá usar uma senha que ele usou recentemente. Se ele tentar configurar a senha para uma que foi usada recentemente, um erro será mostrado na GUI do Widget de login padrão e será solicitado que o usuário insira outra opção.

As senhas anteriores são armazenadas de forma segura da mesma maneira que a senha atual de um usuário.
{: note}


### Política: Bloqueio após credenciais erradas repetidas
{: #cd-lockout}

Talvez você queira proteger as contas de seus usuários bloqueando temporariamente a capacidade de se conectar quando um comportamento suspeito é detectado, como várias tentativas de conexão consecutivas com uma senha incorreta. Essa
medida pode ajudar a evitar que uma parte maliciosa obtenha acesso à conta de um usuário supondo a sua senha.
{: shortdesc}

Usando a GUI ou a API, é possível configurar o número máximo de tentativas de conexão malsucedidas que um usuário faz antes de sua conta ser bloqueada temporariamente. Também é possível definir a quantia de tempo que a conta fica bloqueada. Você tem as opções a seguir:

* Número de tentativas: qualquer valor inteiro de 1 a 10.
* Período de bloqueio de acesso: qualquer valor inteiro especificado em minutos no intervalo de 1 minuto a 1.440 minutos (24 horas).

Se uma conta estiver bloqueada, os usuários não poderão se conectar nem concluir nenhuma outra operação de autoatendimento, como mudar a senha até que o período de bloqueio de acesso especificado seja concluído. Quando o período de bloqueio de acesso termina, o usuário é desbloqueado automaticamente.

É possível desbloquear um usuário antes que o período de bloqueio de acesso termine. Para ver se eles estão bloqueados, verifique se o campo `active` está configurado como `false`. Também é possível verificar se o seu status na guia **Usuários** do painel de serviço está configurado como `disabled`. Para desbloquear um usuário, deve-se usar [a API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) para configurar o campo `active` como `true`.


### Política: Período mínimo entre mudanças de senha
{: #cd-minimum-time}

Talvez você queira evitar que seus usuários alternem as senhas rapidamente, configurando um tempo mínimo que um usuário deve aguardar entre as mudanças de senha.
{: shortdesc}

Esse recurso é especialmente útil quando usado com a política "Evitar reutilização de senha". Sem essa limitação, um usuário pode simplesmente mudar a senha várias vezes em uma sucessão rápida para contornar a limitação de reutilização de senhas recentes. É possível selecionar qualquer valor no intervalo de 1 e 720 horas (30 dias). O campo é especificado em horas.


### Política: Expiração de senha
{: #cd-expiration}

Por motivos de segurança, talvez você queira utilizar uma política de rotação de senha, para que seus usuários mudem suas senhas após um período de tempo especificado.
{: shortdesc}

Ao usar a GUI ou a API, é possível configurar um período no qual as senhas dos usuários permaneçam válidas. Depois que a senha de um usuário expira, ele é forçado a reconfigurá-la na próxima conexão. É possível selecionar qualquer número de dias completos no intervalo de 1 a 90.

É possível iniciar rapidamente com o widget de login usando a GUI padrão fornecida. O usuário é direcionado para fornecer uma nova senha antes da conclusão da conexão.

Se você estiver usando uma experiência de conexão customizada, um erro será acionado quando um usuário tentar se conectar com uma senha expirada. É sua responsabilidade configurar o aplicativo para fornecer a experiência do usuário necessária. É possível chamar a API de mudança de senha para configurar a nova senha.

A resposta do terminal do token é semelhante ao seguinte:

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

Quando essa opção é configurada pela primeira vez como ativa, qualquer senha de usuário existente não tem uma data de expiração. O prazo de expiração começa para os usuários quando a senha é mudada. Talvez você queira encorajar os usuários a
atualizar a senha depois de ativar esse recurso.
{: note}


### Política: assegure-se de que a senha não inclua o nome do usuário
{: #cd-no-username}

Para senhas mais fortes, talvez você queira impedir usuários que contenham seu nome de usuário ou a primeira parte de seu endereço de e-mail.
{: shortdesc}

Essa limitação não faz distinção entre maiúsculas e minúsculas. Os usuários não podem alterar as maiúsculas e minúsculas de alguns ou de todos os caracteres a fim de usar as informações pessoais. Para
configurar essa opção, mude o comutador para **ativo**.
{: note}

