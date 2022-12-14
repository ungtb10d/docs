---
title: ブランチの名前を変更する
intro: リポジトリにあるブランチの名前を変更できます。
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
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '145132355'
---
## ブランチの名前変更について

{% data variables.product.product_location %} にあるリポジトリのブランチの名前を変更できます。 ブランチの詳細については、「[ブランチについて](/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches)」を参照してください。

{% data variables.product.product_location %} 上のブランチ名を変更すると、古いブランチ名を含む URL は、名前を変更したブランチの URL に自動的にリダイレクトされます。 ブランチ保護ポリシー、オープンなプルリクエストのベースブランチ (フォーク含む) およびドラフトリリースも更新されます。 名前の変更が完了すると、{% data variables.product.prodname_dotcom %} は、リポジトリのホームページに、コントリビューターにローカルの Git 環境を更新するよう指示を掲載します。

ファイル URL は自動的にリダイレクトされますが、生のファイル URL はリダイレクトされません。 また、ユーザーが以前のブランチ名に対して `git pull` を実行した場合も、{% data variables.product.prodname_dotcom %} ではリダイレクトされません。

{% data variables.product.prodname_actions %} ワークフローでは名前変更に従わないので、リポジトリでアクションが発行された場合に、`@{old-branch-name}` を伴うアクションを使用するユーザーは誰でも中断されます。 元のコンテンツを含む新しいブランチを追加するとともに、ブランチ名が非推奨であることを報告し、ユーザーに新しいブランチ名への移行を提案するコミットの追加を検討する必要があります。

## ブランチの名前を変更する

{% data reusables.repositories.navigate-to-repo %} {% data reusables.repositories.navigate-to-branches %}
1. ブランチのリストで、名前を変更するブランチの右にある {% octicon "pencil" aria-label="The edit icon" %} をクリックします。
    ![名前を変更するブランチの右にある鉛筆アイコン](/assets/images/help/branch/branch-rename-edit.png)
1. ブランチの新しい名前を入力します。
    ![新しいブランチ名を入力するためのテキスト フィールド](/assets/images/help/branch/branch-rename-type.png)
1. ローカル環境についての情報を確認し、 **[ブランチの名前変更]** をクリックします。
    ![ローカル環境情報と [ブランチの名前変更] ボタン](/assets/images/help/branch/branch-rename-rename.png)

## ブランチ名の変更後にローカルクローンを更新する

{% data variables.product.product_name %} 上のリポジトリにあるブランチ名の変更後、そのリポジトリのローカルクローンのコラボレータは、クローンを更新する必要があります。

コンピュータ上にあるリポジトリのローカルクローンから、以下のコマンドを実行してデフォルトブランチ名を更新します。

```shell
$ git branch -m <em>OLD-BRANCH-NAME</em> <em>NEW-BRANCH-NAME</em>
$ git fetch origin
$ git branch -u origin/<em>NEW-BRANCH-NAME</em> <em>NEW-BRANCH-NAME</em>
$ git remote set-head origin -a
```

必要に応じて次のコマンドを実行し、古いブランチ名への追跡参照を削除します。
```
$ git remote prune origin
```
