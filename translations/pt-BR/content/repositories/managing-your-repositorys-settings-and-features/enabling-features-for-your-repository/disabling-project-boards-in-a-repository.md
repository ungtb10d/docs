---
title: 'Desabilitar {% data variables.projects.projects_v1_boards %} em um repositório'
intro: 'Os administradores do repositório podem desligar {% data variables.projects.projects_v1_boards %} de um repositório se você ou sua equipe gerenciam o trabalho de maneira diferente.'
redirect_from:
  - /github/managing-your-work-on-github/managing-project-boards/disabling-project-boards-in-a-repository
  - /articles/disabling-project-boards-in-a-repository
  - /github/managing-your-work-on-github/disabling-project-boards-in-a-repository
  - /github/administering-a-repository/managing-repository-settings/disabling-project-boards-in-a-repository
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Pull requests
shortTitle: 'Disable {% data variables.projects.projects_v1_boards %}'
allowTitleToDifferFromFilename: true
ms.openlocfilehash: 0407d6df39ae664474aa3fb5c99dc7998df1b951
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '147422657'
---
Ao desabilitar o {% data variables.projects.projects_v1_boards %}, você não verá mais informações do {% data variables.projects.projects_v1_board %} em cronogramas ou [logs de auditoria](/articles/reviewing-your-security-log/).

{% data reusables.repositories.navigate-to-repo %} {% data reusables.repositories.sidebar-settings %}
3. Em "Recursos", desmarque a caixa de seleção **Projetos**.
  ![Caixa de seleção Remover projetos](/assets/images/help/projects/disable-projects-checkbox.png)

Depois que os {% data variables.projects.projects_v1_boards %} forem desabilitados, os {% data variables.projects.projects_v1_boards %} ficarão inacessíveis nas URLs anteriores. {% data reusables.organizations.disable_project_board_results %}
