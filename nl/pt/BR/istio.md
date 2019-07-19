---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-11"

keywords: Authentication, authorization, identity, app security, access, secure, development, any kube, kubernetes, icp, openshift, iks

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

# Protegendo apps multinuvem com o Istio
{: #istio-adapter}

Ao usar o adaptador App Identity and Access, é possível centralizar todo o seu gerenciamento de identidade em um único lugar. Como as empresas usam nuvem de diversos provedores ou uma combinação de soluções dentro e fora do local, modelos de implementação heterogêneos podem ajudar a preservar a infraestrutura existente e evitar bloqueio de fornecedor. O adaptador pode ser configurado para trabalhar com qualquer provedor de identidade compatível com OIDC, como o {{site.data.keyword.appid_short_notm}}, que permite que ele controle políticas de autenticação e autorização em todos os ambientes, incluindo aplicativos front-end e back-end. E **ele faz tudo isso sem nenhuma mudança no seu código ou a necessidade de reimplementar seu aplicativo**.
{: shortdesc}


## Arquitetura multinuvem
{: #istio-multicloud}

Um ambiente de computação multinuvem combina ambientes de computação de diversas nuvens e/ou privados em uma única arquitetura de rede. Ao distribuir cargas de trabalho em diversos ambientes, é possível encontrar uma resiliência melhorada, flexibilidade e maior eficiência de custos. Para alcançar os benefícios, é comum usar um aplicativo baseado em contêiner com uma camada de orquestração, como o Kubernetes.

![Diagrama de arquitetura do adaptador App Identity and Access](images/istio-adapter.png)
Figura. Implementação multinuvem - alcançada com o adaptador App Identity and Access.




## Entendendo o Istio e o adaptador
{: #istio-architecure}

O [Istio](https://istio.io) é uma malha de serviços de software livre que cria camadas de forma transparente nos aplicativos distribuídos existentes que podem se integrar ao Kubernetes. Para reduzir a complexidade de implementações, o Istio fornece insights comportamentais e controle operacional sobre a malha de serviços como um todo. Quando o App ID é combinado com o Istio, ele se torna uma solução de identidade escalável e integrada para arquiteturas multinuvem que não requer nenhuma mudança de código de aplicativo customizada. Para obter mais informações, confira ["O que é Istio?"](https://www.ibm.com/cloud/learn/istio?cm_mmc=OSocial_Youtube-_-Hybrid+Cloud_Cloud+Platform+Digital-_-WW_WW-_-IstioYTDescription&cm_mmca1=000023UA&cm_mmca2=10010608){: external}.

O Istio usa um sidecar de proxy do Envoy para mediar todo o tráfego de entrada e saída para todos os serviços na malha de serviços. Ao usar o proxy, o Istio extrai informações sobre tráfego, também conhecido como telemetria, que são enviadas para o componente do Istio chamado Mixer para cumprimento das decisões de política. O adaptador App Identity and Access estende a funcionalidade do Mixer analisando a telemetria (atributos) em relação às políticas customizadas para controlar o gerenciamento de identidade e acesso na malha de serviços. As políticas de gerenciamento de acesso são vinculadas a serviços Kubernetes e podem ser ajustadas adequadamente a terminais em serviço específicos. Para obter mais informações sobre políticas e telemetria, consulte a [documentação do Istio](https://istio.io/docs/concepts/observability/){: external}. 

Devido a uma limitação do Istio, o adaptador App Identity and Access atualmente armazena informações de sessão do usuário internamente e *não* persiste as informações entre réplicas ou sobre configurações de failover. Quando você usa o adaptador, limite suas cargas de trabalho a uma única réplica até que a limitação seja tratada.
{: note}

### Protegendo apps front-end
{: #istio-frontend}

Se você estiver usando um aplicativo baseado em navegador, será possível usar o fluxo [Open ID Connect (OIDC)](https://openid.net/specs/openid-connect-core-1_0.html){: external}/OAuth 2.0 `authorization_grant` para autenticar seus usuários. Quando um usuário não autenticado é detectado, ele é redirecionado automaticamente para a página de autenticação. Quando a autenticação é concluída, o navegador é redirecionado para um terminal `/oidc/callback` implícito no qual o adaptador intercepta a solicitação. Neste ponto, o adaptador obtém tokens do provedor de identidade e, em seguida, redireciona o usuário de volta à sua URL solicitada originalmente.

Para visualizar as informações de sessão do usuário, incluindo os tokens de sessão, é possível consultar o cabeçalho `Authorization`.

```
Authorization: Bearer <access_token> <id_token>
```
{: screen}

Também é possível efetuar logout de usuários autenticados. Quando um usuário autenticado acessa qualquer terminal protegido com `oidc/logout` anexado, conforme mostrado no exemplo a seguir, ele é desconectado.

```
https://myhost/path/oidc/logout
```
{: screen}

Se necessário, um token de atualização pode ser usado para adquirir automaticamente novos tokens de acesso e identidade sem que o usuário precise se autenticar novamente. Se o provedor de identidade configurado retornar um token de atualização, ele será persistido na sessão e usado para recuperar novos tokens quando o token de identidade expirar.


### Protegendo apps back-end
{: #istio-backend}

O adaptador pode ser usado em colaboração com o [fluxo de JWT Bearer](https://tools.ietf.org/html/rfc6750){: external} do OAuth 2.0 para proteger as APIs de serviço validando tokens JWT Bearer. O fluxo de autorização do Bearer espera que uma solicitação contenha um Cabeçalho de autorização com um token de acesso válido e um token de identidade opcional. A estrutura do cabeçalho esperada é `Authorization=Bearer {access_token} [{id_token}]`. Os clientes não autenticados recebem de retorno um status de resposta HTTP 401 com uma lista dos escopos que são necessários para obter autorização. Se os tokens forem inválidos ou expirados, a estratégia de API retornará uma resposta HTTP 401 com um componente de erro opcional que dirá `Www-Authenticate=Bearer scope="{scope}" error="{error}"`.


Para obter mais informações sobre tokens e como eles são usados, consulte [Entendendo tokens](/docs/services/appid?topic=appid-tokens).



## Antes de iniciar
{: #istio-before}

Antes de iniciar, assegure-se de ter instalado os pré-requisitos a seguir.

- [Cluster do Kubernetes](https://kubernetes.io/){: external}
- [Helm](https://helm.sh/){: external}
- [Istio v1.1+](https://istio.io/docs/setup/kubernetes/install/){: external}
  
  Também é possível usar o [Istio gerenciado do IBM Cloud Kubernetes Service](/docs/containers?topic=containers-istio).
  {: note}



## Instalando o adaptador
{: #istio-install-adapter}

Para instalar o gráfico, inicialize o Helm no seu cluster, defina as opções que deseja usar e, em seguida, execute o comando de instalação.

1. Se você estiver trabalhando com o serviço do IBM Cloud Kubernetes, assegure-se de efetuar login e configurar o contexto para seu cluster.

2. Instale o Helm em seu cluster.

    ```bash
    helm init
    ```
    {: codeblock}

    Você pode desejar configurar o Helm para usar o modo `--tls`. Para obter ajuda na ativação do TLS, confira o [repositório do Helm](https://github.com/helm/helm/blob/master/docs/tiller_ssl.md){: external}. Se você ativar o TLS, certifique-se de anexar `--tls` a cada comando
do Helm executado. Para obter mais informações sobre como usar o Helm com o IBM Cloud Kubernetes Service, consulte [Incluindo serviços usando Gráficos do Helm](/docs/containers?topic=containers-helm#public_helm_install).
    {: tip}

3. Instale o gráfico.

    ```bash
    helm install ./helm/appidentityandaccessadapter --name appidentityandaccessadapter
    ```
    {: codeblock}

## Aplicando uma política de autorização e autenticação
{: #istio-apply-policy}

Uma política de autenticação ou autorização é um conjunto de condições que deve ser atendido antes de uma solicitação poder acessar um acesso de recurso. Ao definir uma configuração de serviço do provedor de identidade e uma política que descreva quando um determinado fluxo deve ser usado, é possível controlar o acesso a qualquer recurso na malha de serviços. Para ver CRDs de exemplo, confira o [diretório de amostras](https://github.com/ibm-cloud-security/app-identity-and-access-adapter/tree/master/samples/crds){: external}.

Para criar uma política:

1. Defina uma configuração.
2. Registre o terminal.

### Definindo uma configuração
{: #istio-apply-define}

Dependendo se você estiver protegendo aplicativos front-end ou back-end, crie uma configuração de política com uma das opções a seguir.

* Para aplicativos front-end: os aplicativos baseados em navegador que requerem autenticação do usuário podem ser configurados para usar o fluxo de autenticação OIDC/OAuth 2.0. Para definir um CRD `OidcConfig` que contenha o cliente usado para facilitar o fluxo de autenticação com o Provedor de identidade, use o exemplo a seguir como um guia.

    ```yaml
    apiVersion: "security.cloud.ibm.com/v1"
    kind: OidcConfig
    metadata:
        name:      oidc-provider-config
        namespace: sample-namespace
    spec:
        discoveryUrl: https://us-south.appid.cloud.ibm.com/oauth/v4/<tenant-ID>/oidc-discovery/.well-known
        clientId:     <client-ID>
        clientSecret: <randomlyGeneratedClientSecret>
        clientSecretRef:
            name: <name-of-my-kube-secret>
            key: <key-in-my-kube-secret>
    ```
    {: screen}

    <table>
        <thead>
        <tr>
            <th>Campo</th>
            <th style="text-align:center">Tipo</th>
            <th style="text-align:center">Necessário</th>
            <th style="text-align:center">Descrição</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <td><code>discoveryUrl</code></td>
            <td style="text-align:center">sequência</td>
            <td style="text-align:center">Sim</td>
            <td style="text-align:center">Um terminal conhecido que fornece um documento JSON de informações de configuração do OIDC/OAuth 2.0.</td>
        </tr>
        <tr>
            <td><code> clientId                         </code></td>
            <td style="text-align:center">sequência</td>
            <td style="text-align:center">Sim</td>
            <td style="text-align:center">Um identificador para o cliente que é usado para autenticação.</td>
        </tr>
        <tr>
            <td><code>clientSecret</code></td>
            <td style="text-align:center">sequência</td>
            <td style="text-align:center">*Não</td>
            <td style="text-align:center">Um segredo de texto sem formatação que é usado para autenticar o cliente. Se não fornecido, um <code>clientSecretRef</code> deverá existir.</td>
        </tr>
        <tr>
            <td><code>clientSecretRef</code></td>
            <td style="text-align:center">objeto</td>
            <td style="text-align:center">Não</td>
            <td style="text-align:center">Um segredo de referência que é usado para autenticar o cliente. A referência pode ser usada no lugar do <code>clientSecret</code>.</td>
        </tr>
        <tr>
            <td><code>clientSecretRef.name</code></td>
            <td style="text-align:center">sequência</td>
            <td style="text-align:center">Sim</td>
            <td style="text-align:center">O nome do Segredo do Kubernetes que contém o <code>clientSecret</code>.</td>
        </tr>
        <tr>
            <td><code>clientSecretRef.key</code></td>
            <td style="text-align:center">sequência</td>
            <td style="text-align:center">Sim</td>
            <td style="text-align:center">O campo dentro do Segredo do Kubernetes que contém o <code>clientSecret</code>.</td>
        </tr>
        </tbody>
    </table>

* Para aplicativos back-end: a especificação de token do Bearer do OAuth 2.0 define um padrão para proteger APIs usando [JSON Web Tokens (JWTs)](https://tools.ietf.org/html/rfc7519.html){: external}. Usando a configuração a seguir como um exemplo, defina um CRD `JwtConfig` que contenha o recurso de chave pública, que é usado para validar assinaturas de token.

    ```yaml
    apiVersion: "security.cloud.ibm.com/v1"
    kind: JwtConfig
    metadata:
      name:      jwt-config
      namespace: sample-app
    spec:
        jwksUrl: https://us-south.appid.cloud.ibm.com/oauth/v4/<tenant-ID>/publickeys
    ```
    {: screen}

### Registrando terminais do aplicativo
{: #istio-register-endpoints}

Registre os terminais do aplicativo dentro de um CRD `Policy` para validar solicitações recebidas e cumprir regras de autenticação. Cada `Policy` se aplica exclusivamente ao namespace do Kubernetes no qual o objeto vive e pode especificar os serviços, caminhos e métodos que deseja proteger.

```yaml
apiVersion: "security.cloud.ibm.com/v1"
kind: Policy
metadata:
  name:      samplepolicy
  namespace: sample-app
spec:
  targets:
    -
      serviceName: <svc-sample-app>
      paths:
        - exact: /web/home
          method: ALL
          policies:
            - policyType: oidc
              config: <oidc-provider-config>
              rules:
                - claim: scope
                  match: ALL
                  source: access_token
                  values:
                    - appid_default
                    - openid
                - claim: amr
                  match: ANY
                  source: id_token
                  values:
                    - cloud_directory
                    - google

        - exact: /web/user
          method: GET
          policies:
            - policyType: oidc
              config: <oidc-provider-config>
              redirectUri: https://github.com/ibm-cloud-security/app-identity-and-access-adapter
        - prefix: /
          method: ALL
          policies:
            -
              policyType: jwt
              config: <jwt-config>
```
{: screen}


| Objeto de serviço | Tipo | Necessário | Descrição   |
|:----------------:|:----:|:--------:| :-----------: |
| `service` | `string` | Sim | O nome do serviço Kubernetes no namespace de Política que deseja proteger. |
| `paths` | `array[Path Object]` | Sim | Uma lista de objetos de caminho que define os terminais que deseja proteger. Se deixado vazio, todos os caminhos são protegidos. |
{: class="simple-tab-table"}
{: caption="Tabela 1. Entendendo os componentes de objeto de serviço" caption-side="top"}
{: #service-object}
{: tab-title="Service object"}
{: tab-group="objects"}

| Objeto de caminho  | Tipo | Necessário | Descrição   |
|:----------------:|:----:|:--------:|:-----------:|
| `exact or prefix` | `string` | Sim | O caminho no qual você deseja aplicar as políticas. As opções incluem `exact` e `prefix`. `exact` corresponde aos terminais fornecidos exatamente com o último `/` cortado. `prefix` corresponde aos terminais que começam com o prefixo de rota que você fornece. |
| `method` | `enum` | Não | O método de HTTP protegido. Opções válidas ALL, GET, PUT, POST, DELETE, PATCH - Padronizado para ALL:  |
| `policies` | `array[Policy]` | Não | As políticas de OIDC/JWT que você deseja aplicar. |
{: class="simple-tab-table"}
{: caption="Tabela 2. Entendendo os componentes de objeto de caminho" caption-side="top"}
{: #path-object}
{: tab-title="Path object"}
{: tab-group="objects"}

| Objeto de política  | Tipo | Necessário | Descrição   |
|:----------------:|:----:|:--------:| :-----------: |
| `policyType` | `enum` | Sim | O tipo de política de OIDC. As opções incluem: `jwt` ou `oidc`. |
| `config` | `string` | Sim | O nome da configuração do provedor que você deseja usar. |
| `redirectUri` | `string` | Não | A URL para a qual você deseja que o usuário seja redirecionado após a autenticação bem-sucedida: a URL de solicitação original. |
| `rules` | `array[Rule]` | Não | O conjunto de regras que você deseja usar para validação de token. |
{: class="simple-tab-table"}
{: caption="Tabela 3. Entendendo os componentes de objeto de política" caption-side="top"}
{: #policy-object}
{: tab-title="Policy object"}
{: tab-group="objects"}

| Objeto de regra | Tipo | Necessário | Descrição   |
|:----------------:|:----:|:--------:| :-----------: |
| `claim` | `string` | Sim | A solicitação que você deseja validar. |
| `match` | `enum` | Não | Os critérios necessários para validação de solicitação. As opções incluem: `ALL`, `ANY` ou `NOT`. O padrão é configurado para `ALL`. |
| `source` | `enum` | Não | O token em que você deseja aplicar a regra. As opções incluem: `access_token` ou `id_token`. O padrão é configurado para `access_token`. |
| `values` | `array[string]` | Sim | O conjunto de valores necessário para validação. |
{: class="simple-tab-table"}
{: caption="Tabela 4. Entendendo os componentes de objeto de política" caption-side="top"}
{: #rule-object}
{: tab-title="Rule object"}
{: tab-group="objects"}


## Excluindo o adaptador
{: #istio-remove}

Para remover o adaptador e todos os CRDs associados, deve-se excluir o gráfico do Helm e as chaves de assinatura e criptografia associadas.

```bash
helm delete --purge appidentityandaccessadapter
kubectl delete secret appidentityandaccessadapter-keys -n istio-system
```
{: codeblock}


## Perguntas mais frequentes e resolução de problemas
{: #istio-faq}

Se você encontrar um problema enquanto trabalha com o adaptador App Identity and Access, considere as técnicas a seguir de Perguntas mais frequentes e resolução de problemas. Para obter mais ajuda, é possível fazer perguntas por meio de um fórum ou abrir um chamado de suporte. Quando você usar os fóruns para fazer uma pergunta, identifique-a para que ela seja vista pela equipe de desenvolvimento do {{site.data.keyword.appid_short_notm}}.

  * Se você tiver questões técnicas sobre o {{site.data.keyword.appid_short_notm}}, poste
a sua questão no <a href="https://stackoverflow.com/" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e identifique-a com "ibm-appid".
  * Para perguntas sobre o serviço e instruções de introdução, use o fórum <a href="https://developer.ibm.com/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Inclua a tag `appid`.

Para informações adicionais sobre como obter suporte, consulte [como obtenho o suporte de que preciso](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).


### Resolução de problemas: criação de log
{: #istio-logging}

Por padrão, os logs são estilizados como JSON e fornecidos em um nível de visibilidade `info` para fornecer a facilidade de integração com sistemas de criação de log externos. Para atualizar a configuração de criação de log, é possível usar o gráfico do Helm. Os níveis de criação de log suportados incluem o intervalo [-1, 7], conforme mostrado no núcleo do Zap. Para obter mais informações sobre os níveis, consulte a [documentação do núcleo do Zap](https://godoc.org/go.uber.org/zap/zapcore#Level).

Quando você estiver visualizando manualmente os logs de JSON, talvez queira usar tail dos logs e fazer uma "impressão elegante" deles usando [`jq`](https://brewinstall.org/install-jq-on-mac-with-brew/).
{: note}

**Adaptador**

Para ver os logs do adaptador, é possível usar `kubectl` ou acessar o pod por meio do pod `appidentityandaccessadapter` por meio do console do Kubernetes.

```bash
$ alias adapter_logs="kubectl -n istio-system logs -f $(kubectl -n istio-system get pods -lapp=appidentityandaccessadapter -o jsonpath='{.items[0].metadata.name}')"
$ adapter_logs | jq
```
{: codeblock}

**Mixer**

Se o adaptador não aparecer para receber solicitações, verifique os logs do Mixer para assegurar que ele esteja conectado ao adaptador com sucesso.

```bash
$ alias mixer_logs="kubectl -n istio-system logs -f $(kubectl -n istio-system get pods -lapp=telemetry -o jsonpath='{.items[0].metadata.name}') -c mixer"
$ mixer_logs | jq
```
{: codeblock}

