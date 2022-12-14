---
title: 'Adicionar um colaborador externo a um {% data variables.product.prodname_project_v1 %} em sua organização'
intro: 'Como proprietário de uma organização ou administrador do {% data variables.projects.projects_v1_board %}, você pode adicionar um colaborador externo e personalizar as permissões dele para um {% data variables.projects.projects_v1_board %}.'
redirect_from:
  - /articles/adding-an-outside-collaborator-to-a-project-board-in-your-organization
  - /github/setting-up-and-managing-organizations-and-teams/adding-an-outside-collaborator-to-a-project-board-in-your-organization
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Organizations
  - Teams
shortTitle: Add a collaborator
allowTitleToDifferFromFilename: true
ms.openlocfilehash: 04a8728c1dc38937a00277316e162ead9acb0fef
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '147422945'
---
{% data reusables.projects.project_boards_old %}

Um colaborador externo é uma pessoa que não é explicitamente um membro da sua organização, mas tem permissões para um {% data variables.projects.projects_v1_board %} em sua organização.

{% data reusables.profile.access_org %} {% data reusables.user-settings.access_org %} {% data reusables.organizations.organization-wide-project %}{% ifversion projects-v2 %}
1. Clique em **Projetos (clássicos)** {% endif %} {% data reusables.project-management.select-project %} {% data reusables.project-management.click-menu %} {% data reusables.project-management.access-collaboration-settings %} {% data reusables.project-management.collaborator-option %}
9. Em "Search by username, full name or email address" (Pesquisar por nome de usuário, nome completo ou endereço de e-mail), digite o nome do colaborador externo, nome de usuário ou e-mail no {% data variables.product.prodname_dotcom %}.
   ![A seção Colaboradores com o nome de usuário do Octocat inserido no campo de pesquisa](/assets/images/help/projects/org-project-collaborators-find-name.png) {% data reusables.project-management.add-collaborator %} {% data reusables.project-management.collaborator-permissions %}
