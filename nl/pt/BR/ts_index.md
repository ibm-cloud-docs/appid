---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Resolução de problemas gerais
{: #troubleshooting}

Se você tiver problemas enquanto está trabalhando com o {{site.data.keyword.appid_full}}, considere estas técnicas para resolução de problemas e obtenção de ajuda.
{: shortdesc}

## Obtendo ajuda e suporte
{: #gettinghelp}

É possível obter ajuda procurando informações ou fazendo perguntas por meio de um fórum. Também é possível abrir um chamado de suporte. Quando estiver usando os fóruns para fazer uma pergunta, identifique sua pergunta para que ela seja vista pela equipe de
desenvolvimento do {{site.data.keyword.Bluemix_notm}}.
  * Se você tiver questões técnicas sobre o {{site.data.keyword.appid_short_notm}}, poste
a sua questão no <a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e identifique-a com "ibm-appid".
  * Para perguntas sobre o serviço e instruções de introdução, use o fórum <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Inclua a tag `appid`.

Para obter mais informações sobre como obter suporte, consulte [Como obter o suporte que eu preciso](/docs/get-support/howtogetsupport.html#getting-customer-support).

</br>

## Uma URL customizada é rejeitada
{: #ts-custom-url}


{: tsSymptoms}
Quando você insere uma URL de redirecionamento da web que usa um esquema de URL customizado, ela é rejeitada pelo
console do {{site.data.keyword.appid_short_notm}}.

{: tsCauses}
Sua URL pode ser rejeitada pelos motivos a seguir:

* A URL não segue um esquema `http` ou `https`
* A URL termina com `://`
* Há um erro tipográfico em sua URL

As limitações estão em vigor para fins de segurança.

{: tsResolve}
Para resolver o problema, verifique se a URL está correta. Se a sua URL não atender aos requisitos, será possível criar
um terminal HTTPS em seu aplicativo para redirecionar o código de concessão recebido para sua URL customizada. Especifique o
terminal criado como sua URL de redirecionamento no console do {{site.data.keyword.appid_short_notm}}.

</br>
