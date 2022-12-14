---
title: Autenticação SAML
shortTitle: Troubleshoot SAML SSO
intro: 'Se o SSO (logon único) do SAML for usado e as pessoas não conseguirem se autenticar para acessar o {% data variables.product.product_location %}, você poderá solucionar o problema.'
versions:
  ghes: '*'
  ghec: '*'
type: how_to
topics:
  - Accounts
  - Authentication
  - Enterprise
  - Identity
  - Security
  - SSO
  - Troubleshooting
ms.openlocfilehash: 977431b9c9872f405a2c8491372f11d8e4ada907
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '147093035'
---
{% ifversion ghes %}
## Sobre problemas com a autenticação SAML

Mensagens de erro dos logs do {% data variables.product.product_name %} para autenticação do SAML com falha no log de autenticação em _/var/log/github/auth.log_. Você pode examinar as respostas neste arquivo de log e também pode configurar o log mais detalhado.

Para obter mais informações sobre os requisitos de resposta SAML, confira "[Referência de configuração do SAML](/admin/identity-and-access-management/using-saml-for-enterprise-iam/saml-configuration-reference#saml-response-requirements)".

## Configurando a depuração do SAML

Você pode configurar o {% data variables.product.product_name %} para gravar logs de depuração detalhados em _/var/log/github/auth.log_ para cada tentativa de autenticação do SAML. É possível que você possa solucionar problemas com tentativas de autenticação com esta saída extra.

{% warning %}

**Avisos**:

- Habilite apenas a depuração do SAML temporariamente e desabilite a depuração imediatamente após terminar a solução de problemas. Se você deixar a depuração habilitada, o tamanho do seu registro poderá aumentar muito mais rápido do que o normal, o que pode impactar negativamente o desempenho de {% data variables.product.product_name %}.
- Teste novas configurações de autenticação para {% data variables.product.product_location %} em um ambiente de teste antes de aplicar as configurações no seu ambiente de produção. Para obter mais informações, confira "[Como configurar uma instância de preparo](/admin/installation/setting-up-a-github-enterprise-server-instance/setting-up-a-staging-instance)".

{% endwarning %}

{% data reusables.enterprise-accounts.access-enterprise %} {% data reusables.enterprise-accounts.policies-tab %} {% data reusables.enterprise-accounts.options-tab %}
1. Em "Depuração do SAML", selecione o menu suspenso e clique em **Habilitado**.

   ![Captura de tela da lista suspensa para habilitar a depuração do SAML](/assets/images/enterprise/site-admin-settings/site-admin-saml-debugging-enabled.png)

1. Tentar efetuar o login no {% data variables.product.product_location %} por meio do IdP do seu SAML.

1. Revise a saída de depuração em _/var/log/github/auth.log_ na {% data variables.product.product_location %}.

1. Quando terminar de resolver os problemas, selecione o menu suspenso e clique em **Desabilitado**.

   ![Captura de tela da lista suspensa para desaabilitar a depuração do SAML](/assets/images/enterprise/site-admin-settings/site-admin-saml-debugging-disabled.png)

## Decodificação de respostas em _auth.log_

Algumas saídas em _auth.log_ podem ser codificadas em Base64. Acesse o shell administrativo e use o utilitário `base64` na {% data variables.product.product_location %} para decodificar essas respostas. Para obter mais informações, confira "[Como acessar o shell administrativo (SSH)](/admin/configuration/configuring-your-enterprise/accessing-the-administrative-shell-ssh)".

```shell
$ base64 --decode <em>ENCODED OUTPUT</em>
```

## Erro: "Outro usuário já possui a conta"

Quando um usuário entra no {% data variables.product.product_location %} pela primeira vez com a autenticação SAML, o {% data variables.product.product_name %} cria uma conta de usuário na instância e mapeia a `NameID` do SAML para a conta.

Quando o usuário se conecta novamente, o {% data variables.product.prodname_ghe_server %} compara o mapeamento da `NameID` da conta com a resposta do IdP. Se a `NameID` na resposta do IdP não corresponder mais à `NameID` esperada pelo {% data variables.product.product_name %} para o usuário, ocorrerá uma falha na entrada. O usuário receberá a seguinte mensagem.

> Outro usuário já possui a conta. Solicite ao administrador que verifique o registro de autenticação.

De modo geral, a mensagem indica que o nome de usuário ou endereço de email da pessoa foi alterado no IdP. Verifique se o mapeamento da `NameID` da conta do usuário no {% data variables.product.prodname_ghe_server %} corresponde à `NameID` do usuário no IdP. Para obter mais informações, confira "[Como atualizar a `NameID` do SAML de um usuário](/admin/identity-and-access-management/using-saml-for-enterprise-iam/updating-a-users-saml-nameid)".

## Se a resposta SAML não estiver assinada ou se a assinatura não corresponder ao conteúdo, o log de autenticação mostrará a seguinte mensagem de erro:

Se o `Recipient` não corresponder à URL do ACS na {% data variables.product.product_location %}, uma das duas mensagens de erro a seguir será exibido no log de autenticação quando um usuário tentar se autenticar.

```
Recipient in the SAML response must not be blank.
```

```
Recipient in the SAML response was not valid.
```

Lembre-se de definir o valor de `Recipient` no IdP como a URL completa do ACS da {% data variables.product.product_location %}. Por exemplo, `https://ghe.corp.example.com/saml/consume`.

## Erro: "Resposta do SAML não foi assinada ou foi modificada"

Se seu IdP não assinar a resposta do SAML ou a assinatura não corresponder ao conteúdo, será exibida a seguinte mensagem de erro no registro de autenticação.

```
SAML Response is not signed or has been modified.
```

Verifique se você configurou as declarações assinadas para o aplicativo do {% data variables.product.product_name %} no seu IdP.

## Erro: "Audiência é inválida" ou "Nenhuma declaração encontrada"

Se a resposta do IdP tiver um valor ausente ou incorreto para `Audience`, a mensagem de erro a seguir será exibida no log de autenticação.

```
Audience is invalid. Audience attribute does not match https://<em>YOUR-INSTANCE-URL</em>
```

Lembre-se de definir o valor de `Audience` no IdP como a `EntityId` do {% data variables.product.product_location %}, que é a URL completa da sua instância. Por exemplo, `https://ghe.corp.example.com`.
{% endif %}

{% data reusables.saml.current-time-earlier-than-notbefore-condition %}

{% ifversion ghec %} {% data reusables.saml.authentication-loop %} {% endif %}
