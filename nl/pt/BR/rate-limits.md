---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-06"

keywords: Authentication, authorization, identity, app security, secure, rates, cloud directory, rate limit, attempts

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


# Limites do App ID
{: #limits}

A limitação de taxa é usada para controlar a quantia de tráfego que está chegando e passando por sua instância do App ID. Ao limitar solicitações ou recursos, é possível proteger seus aplicativos.
{: shortdesc}

## Plano lite do App ID 
{: #lite-limits}

Revise a tabela a seguir para ver os limites que estão em vigor para instâncias lite do App ID. 

<table>
    <tr>
        <th>Recurso</th>
        <th>Máxima</th>
    </tr>
    <tr>
        <td>Usuários</td>
        <td>1000</td>
    </tr>
    <tr>
        <td>Autenticações</td>
        <td>1.000 por mês</td>
    </tr>
</table>

## Consultas
{: #general-limits}

A tabela a seguir lista os limites máximos por usuário para recursos do IBM Cloud App ID e o período de bloqueio quando os limites são excedidos. Esses limites se aplicam a qualquer usuário que possa criar recursos do IBM Cloud App ID.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Limite</th>
        <th>Quando excedido</th>
    </tr>
    <tr>
        <td>Tentativas de conexão por um usuário</td>
        <td>5 por minuto</td>
        <td>O usuário não pode se conectar por 1 minuto.</td>
    </tr>
    <tr>
        <td>Atualizar atributos de perfil do usuário</td>
        <td>5 por minuto</td>
        <td>O usuário não consegue atualizar o perfil por 1 minuto.</td>
    </tr>
        <td>Excluir atributos de perfil do usuário</td>
        <td>5 por minuto</td>
        <td>O usuário não consegue atualizar o perfil por 1 minuto.</td>
    </tr>
</table>



## Cloud Directory
{: #limits-cd}

Revise a tabela a seguir para ver os limites associados ao Cloud Directory.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Configurável</th>
        <th>Limite</th>
        <th>Quando excedido</th>
    </tr>
    <tr>
        <td>Tentativas de conexão por conta</td>
        <td>Sim</td>
        <td>Ilimitado</td>
        <td>Todas as tentativas de conexão da instância ficam bloqueadas por um minuto.</td>
    </tr>
    <tr>
        <td>Tentativas de inscrição por conta</td>
        <td>Sim</td>
        <td>Ilimitado</td>
        <td>Todas as tentativas de inscrição da instância ficam bloqueadas por um minuto.</td>
    </tr>
    <tr>
        <td>Solicitação de envio de e-mail</td>
        <td>Não</td>
        <td>10 e-mails em 10 minutos por usuário</td>
        <td>As solicitações de e-mail do usuário ficam bloqueadas por 30 minutos.</td>
    </tr>
</table>

Para obter mais informações, consulte a <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig" target="_blank">API de gerenciamento de limite de taxa.</a>
