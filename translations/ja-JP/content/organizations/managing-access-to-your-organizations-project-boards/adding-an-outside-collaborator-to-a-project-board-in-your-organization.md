---
title: 'Organization の {% data variables.product.prodname_project_v1 %} に外部コラボレーターを追加する'
intro: 'Organization オーナーまたは {% data variables.projects.projects_v1_board %} 管理者は、{% data variables.projects.projects_v1_board %} に外部コラボレーターを追加し、そのアクセス許可をカスタマイズできます。'
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
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '147422949'
---
{% data reusables.projects.project_boards_old %}

外部コラボレーターは、Organization の明示的なメンバーではありませんが、Organization 内の {% data variables.projects.projects_v1_board %} に対するアクセス許可を持つユーザーです。

{% data reusables.profile.access_org %} {% data reusables.user-settings.access_org %} {% data reusables.organizations.organization-wide-project %}{% ifversion projects-v2 %}
1. **[Project (classic)]** をクリックします{% endif %} {% data reusables.project-management.select-project %} {% data reusables.project-management.click-menu %} {% data reusables.project-management.access-collaboration-settings %} {% data reusables.project-management.collaborator-option %}
9. [Search by username, full name or email address] (ユーザ名、フルネーム、メールアドレスでの検索) の下で、外部のコラボレータの名前、ユーザ名、{% data variables.product.prodname_dotcom %}メールを入力してください。
   ![Octocat のユーザー名が検索フィールドに入力されている [コラボレーター] セクション](/assets/images/help/projects/org-project-collaborators-find-name.png) {% data reusables.project-management.add-collaborator %} {% data reusables.project-management.collaborator-permissions %}
