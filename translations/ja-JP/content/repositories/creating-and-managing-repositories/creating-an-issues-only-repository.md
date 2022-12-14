---
title: Issue だけのリポジトリの作成
intro: '{% data variables.product.product_name %}では Issue に限定されたアクセス権限は存在しませんが、Issue 専用のリポジトリを作成すれば、実質的にそのようなアクセス権限を設定できます。'
redirect_from:
  - /articles/issues-only-access-permissions
  - /articles/is-there-issues-only-access-to-organization-repositories
  - /articles/creating-an-issues-only-repository
  - /github/creating-cloning-and-archiving-repositories/creating-an-issues-only-repository
  - /github/creating-cloning-and-archiving-repositories/creating-a-repository-on-github/creating-an-issues-only-repository
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Repositories
shortTitle: Issues-only repository
ms.openlocfilehash: 76450c6d3bddd02ab3e389b35e6ce67d01ffd771
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '145132331'
---
1. **private** リポジトリを作成して、プロジェクトのソース コードをホストします。
2. Issue トラッカーをホストするための権限を持つ 2 番目のリポジトリを作成します。
3. このリポジトリの目的を説明し、Issue セクションと結びつける README ファイルを Issue リポジトリに追加します。
4. 思うようにコラボレーターまたは Team にリポジトリへのアクセスを付与するよう設定します。

どちらにも書き込みアクセスのあるユーザは、リポジトリ間でお互いに Issue を引用して閉じることができます。ただし、必要な権限がない場合は最低限の情報だけの参照を見ることしかできません。

たとえば、プライベート リポジトリの既定のブランチに `Fixes organization/public-repo#12` というメッセージをつけてコミットをプッシュした場合、Issue は閉じられますが、Issue を閉じたコミットを示すリポジトリ間の参照は、適切な権限を持っているユーザーだけしか見られません。 権限がなくても参照は表示されますが、詳細は省略されます。
