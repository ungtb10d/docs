---
title: Renomear um branch
intro: É possível alterar o nome de um branch em um repositório.
permissions: 'People with write permissions to a repository can rename a branch in the repository unless it is the [default branch](/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches#about-the-default-branch){% ifversion fpt or ghec or ghes > 3.3 %} or a [protected branch](/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/about-protected-branches){% endif %}. People with admin permissions can rename the default branch{% ifversion fpt or ghec or ghes > 3.3 %} and protected branches{% endif %}.'
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Repositories
redirect_from:
  - /github/administering-a-repository/renaming-a-branch
  - /github/administering-a-repository/managing-branches-in-your-repository/renaming-a-branch
ms.openlocfilehash: 6e30c7c2615f8b3dc21075e24298796febbce314
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '145127101'
---
## Sobre a renomeação de branches

Você pode renomear um branch em um repositório em {% data variables.product.product_location %}. Para obter mais informações sobre branches, confira "[Sobre os branches](/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches)".

Ao renomear um branch em {% data variables.product.product_location %}, todas as URLs que contiverem o nome do branch antigo serão automaticamente redirecionadas para a URL equivalente para o branch renomeado. Atualizam-se também as políticas de proteção de branch também, bem como o branch base para pull requests abertos (incluindo aqueles para bifurcações) e rascunhos de versões. Depois que a renomeação for concluída, {% data variables.product.prodname_dotcom %} fornecerá instruções na página inicial do repositório direcionando os colaboradores para atualizar seus ambientes do Git locais.

Embora as URLs do arquivo sejam automaticamente redirecionadas, as URLs do arquivo não processado não são redirecionadas. Além disso, o {% data variables.product.prodname_dotcom %} não executará nenhum redirecionamento se os usuários executarem um `git pull` par o nome de branch anterior.

Os fluxos de trabalho do {% data variables.product.prodname_actions %} não seguem as renomeações, ou seja, se o repositório publicar uma ação, qualquer pessoa que usar essa ação com `@{old-branch-name}` será interrompida. Você deve considerar adicionar um novo branch com o conteúdo original mais um relatório de commit adicional informando que o nome do branch está obsoleto e sugerindo que os usuários façam a migração para o novo nome do branche.

## Renomear um branch

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.navigate-to-branches %}
1. Na lista de branches, à direita do branch que você deseja renomear, clique em {% octicon "pencil" aria-label="The edit icon" %}.
    ![Ícone de lápis à direita do branch que você deseja renomear](/assets/images/help/branch/branch-rename-edit.png)
1. Digite um novo nome para o branch.
    ![Campo de texto usado para digitar o novo nome do branch](/assets/images/help/branch/branch-rename-type.png)
1. Revise as informações sobre ambientes locais e clique em **Renomear branch**.
    ![Informações de ambiente local e botão "Renomear branch"](/assets/images/help/branch/branch-rename-rename.png)

## Atualizar um clone local após alterações de nome do branch

Após renomear um branch em um repositório em {% data variables.product.product_name %}, qualquer colaborador com um clone local do repositório deverá atualizar o clone.

A partir do clone local do repositório em um computador, execute os seguintes comandos para atualizar o nome do branch padrão.

```shell
$ git branch -m <em>OLD-BRANCH-NAME</em> <em>NEW-BRANCH-NAME</em>
$ git fetch origin
$ git branch -u origin/<em>NEW-BRANCH-NAME</em> <em>NEW-BRANCH-NAME</em>
$ git remote set-head origin -a
```

Opcionalmente, execute o comando a seguir para remover as referências de rastreamento para o nome do branch antigo.
```
$ git remote prune origin
```
