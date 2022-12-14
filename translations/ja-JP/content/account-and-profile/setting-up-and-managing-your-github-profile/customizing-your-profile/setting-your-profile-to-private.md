---
title: プロファイルをプライベートに設定する
intro: プライベート プロファイルには限られた情報のみが表示され、一部のアクティビティは表示されません。
versions:
  fpt: '*'
topics:
  - Profiles
shortTitle: Set profile to private
ms.openlocfilehash: 51fd476bc77856b525ce3e991e4eb30e8a881361
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '147062915'
---
## プライベート プロファイルについて

{% note %}

**注:** プライベート プロファイルは現在ベータ版であり、変更される可能性があります。

{% endnote %}

プロファイル ページの一部を非表示にするには、プロファイルをプライベートにします。 これにより、{% data variables.product.prodname_dotcom_the_website %} のさまざまなソーシャル機能のアクティビティも非表示になります。 プライベート プロファイルでは、すべてのユーザーに対し情報が非表示になります。現在、指定したユーザーにアクティビティを表示するオプションはありません。

プロファイルをプライベートにした後も、自分のプロファイルにアクセスした場合、すべての情報が表示されます。

プライベート プロファイルでは、[{% data variables.product.prodname_sponsors %}](/sponsors/getting-started-with-github-sponsors/about-github-sponsors) のスポンサーシップを受けることができません。 {% data variables.product.prodname_sponsors %} の対象になるには、プロファイルをプライベートにしないでください。

## プライベートおよびパブリック プロファイルの違い

プロファイルがプライベートの場合、プロファイル ページで次のコンテンツが非表示になります。

- 実績とハイライト。
- アクティビティの概要とアクティビティ フィード。
- コントリビューション グラフ。
- フォロワーと次の数。
- フォローとスポンサーのボタン。
- Organization メンバーシップ。
- スター、プロジェクト、パッケージ、スポンサー タブ。

{% note %}

**注**: プロファイルがプライベートの場合、README、経歴、プロフィール写真などの一部のオプション フィールドは引き続きパブリックに表示されます。

{% endnote %}

## アクティビティに対する通知の変更

プロフィールをプライベートにしても、過去のアクティビティは削除または非表示になりません。この設定は、プライベート設定が有効になっている間のアクティビティにのみ適用されます。

プロファイルがプライベートの場合、{% data variables.product.prodname_dotcom_the_website %} アクティビティは次の場所に表示されません。

- 他のユーザーのアクティビティ フィード。
- ディスカッション ランキング。
- [[トレンド]](https://github.com/trending) ページ。

{% note %}

**注**: パブリック リポジトリ上のアクティビティは、それらのリポジトリを表示しているユーザーには引き続きパブリックに表示され、一部のアクティビティ データは {% data variables.product.prodname_dotcom %} API を通じて引き続き使用できます。

{% endnote %}

## プロファイルのプライバシー設定を変更する

{% data reusables.user-settings.access_settings %}
1. [コントリビューションとアクティビティ] で、 **[プロファイルを非公開にしてアクティビティを非表示にする]** の横にあるチェックボックスをオンにします。
{% data reusables.user-settings.update-preferences %}
