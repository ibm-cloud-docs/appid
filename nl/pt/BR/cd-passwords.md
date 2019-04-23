---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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

# Definindo políticas de senha
{: #cd-strength}

É possível configurar os requisitos para as senhas que podem ser usadas com o Cloud Directory. Ao definir requisitos específicos que seus usuários devem cumprir, é possível assegurar aplicativos mais seguros.
{: shortdesc}

## Política: força da senha
{: #cd-password-strength}

Uma senha forte torna difícil, ou mesmo improvável para alguém adivinhar a senha de uma maneira manual ou automatizada. Para configurar requisitos para a força de uma senha de usuário, é possível usar as etapas a seguir.
{: shortdesc}

1. Navegue para a guia **Políticas de senha** do painel do ID do app.

2. Na caixa **Definir força da senha**, clique em **Editar**. Uma tela é exibida.

3. Insira uma sequência de expressão regular válida na caixa **Segurança da senha**.

  Exemplos:
    - Deve ter pelo menos oito caracteres. Exemplo de regex: `^.{8,}$`
    - Deve conter um número, uma letra minúscula e uma letra maiúscula. Exemplo de expressão regular: `^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
    - Deve conter somente letras e números em inglês. Exemplo de regex: `^[A-Za-z0-9]*$`
    - Deve ser pelo menos um caractere exclusivo. Exemplo de regex: `^(\w)\w*?(?!\1)\w+$`

4. Clique em **Salvar**.

A força da senha pode ser configurada na página de configurações do Cloud Directory no console do {{site.data.keyword.appid_short_notm}} ou usando as <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex" target="_blank">APIs de gerenciamento <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
{: note}


## Políticas de senha avançadas
{: #cd-advanced-password}


É possível aprimorar a segurança de seu aplicativo impondo restrições de senha adicionais.
{: shortdesc}


É possível criar uma política de senha avançada que consiste em qualquer combinação dos 5 recursos a seguir:

 - Bloqueio de acesso após credenciais erradas repetidas
 - Evitar reutilização de senha
 - Expiração de senha
 - Período mínimo entre mudanças de senha
 - Assegure-se de que a senha não inclua o nome do usuário


 Se você ativar esse recurso, o faturamento adicional para recursos de segurança avançados será ativado. Para obter mais informações, consulte [Como {{site.data.keyword.appid_short_notm}} calcular a precificação](/docs/services/appid?topic=appid-faq#faq-pricing).
 {: important}


### Política: Evite reutilização de senha
{: #cd-avoid-reuse}

Quando os usuários estiverem mudando a senha, talvez você queira evitar que eles escolham uma senha usada
recentemente.
{: shortdesc}

Ao usar a GUI ou a API, é possível escolher o número de senhas que um usuário deve ter antes que possa repetir uma senha usada anteriormente. É possível selecionar qualquer valor inteiro no intervalo de 1 a 10.

Se essa opção estiver ativada, um usuário não poderá usar uma senha que tenha sido usada recentemente por eles. Se eles tentarem configurar sua senha para uma senha que foi usada recentemente, um erro será exibido na GUI do widget de login padrão e uma senha diferente será solicitada.

As senhas anteriores são armazenadas de forma segura da mesma maneira que a senha atual de um usuário.
{: note}


### Política: Bloqueio após credenciais erradas repetidas
{: #cd-lockout}

Você pode desejar proteger as contas de seus usuários bloqueando temporariamente a capacidade de se conectar quando um comportamento suspeito é detectado, como múltiplas tentativas de conexão consecutivas com uma senha incorreta. Essa
medida pode ajudar a evitar que uma parte maliciosa obtenha acesso à conta de um usuário supondo a sua senha.
{: shortdesc}

Usando a GUI ou a API, é possível configurar o número máximo de tentativas de conexão sem sucesso que um
usuário pode fazer antes que sua conta seja temporariamente bloqueada. Também é possível configurar o período de tempo
em que a conta ficará bloqueada. Você tem as opções a seguir:

* Número de tentativas: qualquer valor inteiro de 1 a 10.
* Período de bloqueio de acesso: qualquer valor inteiro especificado em minutos no intervalo de 1 minuto a 1440 minutos (24 horas).

Se uma conta estiver bloqueada, os usuários não poderão se conectar ou executar quaisquer outras operações de autoatendimento, como mudar a senha até que o período de bloqueio especificado tenha decorrido. Quando o
período de bloqueio de acesso terminar, o usuário será desbloqueado automaticamente.

É possível desbloquear um usuário antes que o período de bloqueio de acesso termine. Para ver se eles estão bloqueados, procure saber se o campo `active` está configurado como `false`. Também é possível verificar se o seu status na guia **Usuários** do painel de serviço está configurado como `disabled`. Para desbloquear um usuário, deve-se usar [a API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) para configurar o campo `active` como `true`.


### Política: Período mínimo entre mudanças de senha
{: #cd-minimum-time}

Talvez você queira evitar que os usuários troquem de senha rapidamente configurando um período mínimo de
tempo que eles devem aguardar entre as mudanças de senha.
{: shortdesc}

Esse recurso é especialmente útil quando usado com a política "Evitar reutilização de senha". Sem essa
limitação, um usuário poderia simplesmente mudar sua senha várias vezes em sucessão rápida para contornar a
limitação de reutilização de senhas recentes. É possível selecionar qualquer valor entre 1 hora e 30 dias, especificado em horas.


### Política: Expiração de senha
{: #cd-expiration}

Por motivos de segurança, talvez você queira impor uma política de rotação de senha de modo que seus usuários devam
mudar a senha após um período de tempo.
{: shortdesc}

Ao usar a GUI ou a API, é possível configurar um período de tempo para o qual as senhas do usuário permanecerão válidas. Depois
que a senha de um usuário expirar, eles serão forçados a reconfigurar a senha na próxima conexão. É possível selecionar qualquer número de dias completos entre 1 e 90.

É possível iniciar rapidamente com o widget de login usando a GUI padrão fornecida. O usuário é direcionado para fornecer uma nova senha antes que a conexão seja concluída.

Se você estiver usando uma experiência de conexão customizada, um erro será acionado quando um usuário tentar se
conectar com uma senha expirada. É sua responsabilidade configurar o aplicativo para fornecer a experiência do usuário necessária. É possível chamar a API de mudança de senha para configurar a nova senha.

A resposta do terminal do token é semelhante ao seguinte:

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

Quando essa opção for configurada pela primeira vez, quaisquer senhas de usuário existentes não terão uma data de expiração. O prazo de expiração começa para os usuários quando a senha é mudada. Talvez você queira encorajar os usuários a
atualizar a senha depois de ativar esse recurso.
{: note}


### Política: Assegurar que a senha não inclua o nome do usuário
{: #cd-no-username}

Para senhas mais fortes, talvez você queira evitar os usuários que contenham seu nome de usuário ou a primeira
parte de seu endereço de e-mail.
{: shortdesc}

Essa restrição não faz distinção entre maiúsculas e minúsculas, o que significa que os usuários não conseguem alterar a capitalização de alguns ou todos os caracteres para usar as informações pessoais. Para
configurar essa opção, mude o comutador para **ativo**.

