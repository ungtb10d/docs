---
title: Habilitar o modo privado
intro: 'No modo privado, o {% data variables.product.prodname_ghe_server %} exige que todos os usuários façam login para acessar a instalação.'
redirect_from:
  - /enterprise/admin/articles/private-mode
  - /enterprise/admin/guides/installation/security
  - /enterprise/admin/guides/installation/securing-your-instance
  - /enterprise/admin/installation/enabling-private-mode
  - /enterprise/admin/configuration/enabling-private-mode
  - /admin/configuration/enabling-private-mode
versions:
  ghes: '*'
type: how_to
topics:
  - Access management
  - Authentication
  - Enterprise
  - Fundamentals
  - Infrastructure
  - Networking
  - Privacy
  - Security
ms.openlocfilehash: 99488886b1da5b07c2ddb5d7054c10957f6c573b
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '146332781'
---
Você precisará habilitar o modo privado se o {% data variables.product.product_location %} estiver acessível publicamente pela Internet. No modo privado, os usuários não podem clonar repositórios de maneira anônima por meio do `git://`. Se a autenticação integrada também estiver habilitada, o administrador deverá convidar novos usuários para criar uma conta na instância. Para obter mais informações, veja "[Configurar a autenticação interna](/admin/identity-and-access-management/using-built-in-authentication/configuring-built-in-authentication)".

{% data reusables.enterprise_installation.image-urls-viewable-warning %}

Com o modo privado habilitado, você pode permitir operações do Git não autenticadas (e qualquer pessoa com acesso de rede no {% data variables.product.product_location %}) para ler o código de um repositório público na sua instância com o acesso de leitura anônimo do Git habilitado. Para obter mais informações, confira "[Como permitir que os administradores habilitem o acesso de leitura anônimo do Git em repositórios públicos](/enterprise/admin/guides/user-management/allowing-admins-to-enable-anonymous-git-read-access-to-public-repositories)".

{% data reusables.enterprise_site_admin_settings.access-settings %} {% data reusables.enterprise_site_admin_settings.management-console %} {% data reusables.enterprise_management_console.privacy %}
4. Selecione **Modo privado**.
  ![Caixa de seleção usada para habilitar o modo privado](/assets/images/enterprise/management-console/private-mode-checkbox.png) {% data reusables.enterprise_management_console.save-settings %}
