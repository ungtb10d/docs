---
title: GitHub Mobile
intro: '{% data variables.product.product_name %} での作業をモバイルデバイスからトリアージ、コラボレーション、および管理します。'
versions:
  fpt: '*'
  ghes: '*'
  ghec: '*'
topics:
  - Mobile
redirect_from:
  - /get-started/using-github/github-for-mobile
  - /github/getting-started-with-github/github-for-mobile
  - /github/getting-started-with-github/using-github/github-for-mobile
ms.openlocfilehash: a9af0848fdc26c5efd3dfb2d00076e3af5fb00bc
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '147508449'
---
## {% data variables.product.prodname_mobile %} について

{% data reusables.mobile.about-mobile %}

{% data variables.product.prodname_mobile %} を使用すると、{% data variables.product.product_name %} に対してインパクトのある作業をすばやく、どこからでも行うことができます。 {% data variables.product.prodname_mobile %} は、信頼できるファーストパーティ クライアント アプリケーションを介して {% data variables.product.product_name %} データにアクセスする安心で安全な方法です。

{% data variables.product.prodname_mobile %} では、次のことができます。

- 通知の管理、トリアージ、クリア
- Issue とプルリクエストの読み取り、レビュー、コラボレーション
- ユーザ、リポジトリ、Organization の検索、参照、操作
- あなたのユーザー名がメンションされたときのプッシュ通知の受信 {% ifversion fpt or ghec %}- 2 要素認証を使用した GitHub.com アカウントの保護
- 認識できないデバイスでのサインイン試行の確認{% endif %}

{% data variables.product.prodname_mobile %} の詳細については、「[通知の構成](/github/managing-subscriptions-and-notifications-on-github/configuring-notifications#enabling-push-notifications-with-github-mobile)」を参照してください。

{% ifversion fpt or ghec %}- {% data variables.product.prodname_mobile %} を使用した 2 要素認証の詳細については、「[{% data variables.product.prodname_mobile %} の構成](/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication#configuring-two-factor-authentication-using-github-mobile)」および「[{% data variables.product.prodname_mobile %} を使用した認証](/authentication/securing-your-account-with-two-factor-authentication-2fa/accessing-github-using-two-factor-authentication##verifying-with-github-mobile)」を参照してください。 {% endif %}

## {% data variables.product.prodname_mobile %} のインストール

Android または iOS に {% data variables.product.prodname_mobile %} をインストールするには、「[{% data variables.product.prodname_mobile %}](https://github.com/mobile)」を参照してください。

## アカウントの管理

{% data variables.product.prodname_dotcom_the_website %} の個人アカウントと、{% data variables.product.prodname_ghe_server %}の個人アカウントを使用して同時にモバイルにサインインすることができます。 さまざまな製品の詳細については、「[{% data variables.product.company_short %} の製品](/get-started/learning-about-github/githubs-products)」を参照してください。

{% data reusables.mobile.push-notifications-on-ghes %}

VPN で Enterprise にアクセスする必要がある場合、{% data variables.product.prodname_mobile %} は Enterprise では動作しません。

### 前提条件

{% data variables.product.prodname_ghe_server %} で {% data variables.product.prodname_mobile %} を使用するには、デバイスに {% data variables.product.prodname_mobile %} 1.4 以降をインストールする必要があります。

{% data variables.product.prodname_ghe_server %} で {% data variables.product.prodname_mobile %} を使用するには、{% data variables.product.product_location %} がバージョン 3.0 以降であり、Enterprise オーナーが Enterprise に対してモバイルサポートを有効にしている必要があります。 詳細については、{% ifversion ghes %}「[リリース ノート](/enterprise-server/admin/release-notes)」および{% endif %}「[エンタープライズでの {% data variables.product.prodname_mobile %} の管理]({% ifversion not ghes %}/enterprise-server@latest{% endif %}/admin/configuration/configuring-your-enterprise/managing-github-mobile-for-your-enterprise){% ifversion not ghes %}」({% data variables.product.prodname_ghe_server %} ドキュメント){% else %}{% endif %} を参照してください。

{% data variables.product.prodname_ghe_server %} を使用した {% data variables.product.prodname_mobile %} のベータでは、{% data variables.product.prodname_dotcom_the_website %} の個人アカウントでサインインする必要があります。

### アカウントの追加、切り替え、サインアウト

{% data variables.product.prodname_ghe_server %} の個人アカウントを使用してモバイルにサインインできます。 アプリの下部で、{% octicon "person" aria-label="The person icon" %} **[Profile]\(プロファイル\)** を長押ししてから、{% octicon "plus" aria-label="The plus icon" %} **[Add Enterprise Account]\(エンタープライズ アカウントの追加\)** をタップします。 画面の指示に従ってサインインします。

{% data variables.product.prodname_ghe_server %} の個人アカウントでモバイルにサインインした後、{% data variables.product.prodname_dotcom_the_website %} のアカウントとお使いのアカウントを切り替えることができます。 アプリの下部で、{% octicon "person" aria-label="The person icon" %} **[Profile]\(プロファイル\)** を長押ししてから、切り替えるアカウントをタップします。

{% data variables.product.prodname_mobile %} から {% data variables.product.prodname_ghe_server %} の個人アカウントのデータにアクセスする必要がなくなった場合は、アカウントからサインアウトできます。 アプリの下部で、{% octicon "person" aria-label="The person icon" %} **[Profile]\(プロファイル\)** を長押しし、サインアウトするアカウントで左にスワイプして、 **[Sign out]\(サインアウト\)** をタップします。

## {% data variables.product.prodname_mobile %} でサポートされている言語

{% data variables.product.prodname_mobile %} は次の言語で利用できます。

- 英語
- 日本語
- ポルトガル語 (ブラジル)
- 簡体中国語
- スペイン語

デバイスの言語をサポートされている言語に設定すると、{% data variables.product.prodname_mobile %} はデフォルトでその言語になります。 {% data variables.product.prodname_mobile %} の **[Settings]\(設定\)** メニューで {% data variables.product.prodname_mobile %} の言語を変更できます。

## iOS で {% data variables.product.prodname_mobile %} のユニバーサルリンクを管理する

{% data variables.product.prodname_mobile %} は、iOS のユニバーサルリンクを自動的に有効にします。 {% data variables.product.product_name %} リンクをタップすると、リンク先 URL が Safari ではなく {% data variables.product.prodname_mobile %} で開きます。 詳細については、Apple の開発者向けサイトで「[ユニバーサル リンク](https://developer.apple.com/ios/universal-links/)」を参照してください。

ユニバーサル リンクを無効にするには、いずれかの {% data variables.product.product_name %} リンクを長押しし、 **[Open]\(開く\)** をタップします。 今後、{% data variables.product.product_name %} リンクをタップするたびに、リンク先 URL が {% data variables.product.prodname_mobile %} ではなく Safari で開きます。

ユニバーサル リンクを再度有効にするには、いずれかの {% data variables.product.product_name %} リンクを長押ししてから、 **[Open in {% data variables.product.prodname_dotcom %}]\(GitHub で開く\)** をタップします。

## フィードバックを送る

{% data variables.product.prodname_mobile %} の機能に関する要求やその他のフィードバックは、[{% data variables.product.prodname_github_community %}](https://github.com/orgs/community/discussions/categories/mobile) から送信できます。

## iOS のベータリリースをオプトアウトする

TestFlight を使用して{% data variables.product.prodname_mobile %} iOS 版のベータをテストしている場合は、いつでもベータを終了できます。

1. お使いの iOS デバイスで TestFlight アプリを開きます。
2. [Apps]\(アプリ\) の下で **[{% data variables.product.prodname_dotcom %}]** をタップします。
3. ページの下部で **[Stop Testing]\(テストの停止\)** をタップします。
