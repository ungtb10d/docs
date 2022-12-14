---
title: GitHub Marketplaceアプリケーションの価格プラン
intro: '価格プランを利用して、様々なレベルのサービスやリソースと共にアプリケーションを提供できます。 {% data variables.product.prodname_marketplace %}のリストでは、最大で10個の価格プランを提供できます。'
redirect_from:
  - /apps/marketplace/selling-your-app/github-marketplace-pricing-plans
  - /marketplace/selling-your-app/github-marketplace-pricing-plans
  - /developers/github-marketplace/pricing-plans-for-github-marketplace-apps
versions:
  fpt: '*'
  ghec: '*'
topics:
  - Marketplace
shortTitle: Pricing plans for apps
ms.openlocfilehash: e1ab751c26e59ec42e16dc7d9e5c0118dedffbde
ms.sourcegitcommit: 5b1461b419dbef60ae9dbdf8e905a4df30fc91b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2022
ms.locfileid: '147878693'
---
{% data variables.product.prodname_marketplace %}の価格プランは、無料、定額料金、ユニット単位にできます。 価格は米ドルで設定、表示、処理されます。 有料プランは、検証済みパブリッシャーが公開するアプリケーションに限られます。 検証済みのパブリッシャーになる方法の詳細については、「[Organization のパブリッシャー検証プロセスを申請する](/developers/github-marketplace/applying-for-publisher-verification-for-your-organization)」を参照してください。

顧客は{% data variables.product.prodname_dotcom_the_website %}を離れることなく、{% data variables.product.product_location %}上のアカウントに添付された支払い方法を使ってアプリケーションを購入します。 支払いトランザクションを実行するためにコードを書く必要はありませんが、{% data variables.product.prodname_marketplace %} APIからのイベントは処理しなければなりません。 詳細については、「[アプリ内での {% data variables.product.prodname_marketplace %} API の使用](/developers/github-marketplace/using-the-github-marketplace-api-in-your-app)」を参照してください。

{% data variables.product.prodname_marketplace %}上でリストしているアプリケーションが複数のプランのオプションを持っているなら、対応する価格プランをセットアップできます。 たとえばアプリケーションが2つのプランの選択肢としてオープンソースプランとプロプランを持っているなら、オープンソースプランに対して無料価格プランを、そしてプロプランに対して定額料金プランをセットアップできます。 それぞれの{% data variables.product.prodname_marketplace %}リストには、リストされたすべてのプランに対して年間及び月間の価格がなければなりません。

価格プランを作成する方法の詳細については、「[{% data variables.product.prodname_marketplace %} リストの価格プランの設定](/marketplace/listing-on-github-marketplace/setting-a-github-marketplace-listing-s-pricing-plan/)」を参照してください。

{% data reusables.marketplace.free-plan-note %}

## 価格プランの種類

### 無料プラン

{% data reusables.marketplace.free-apps-encouraged %}

無料プランは、ユーザに対してまったく無料です。 無料プランをセットアップした場合、アプリケーションを利用するために無料プランを選択したユーザに課金することはできません。 リストでは無料と有料のプランをどちらも作成できます。

すべてのアプリケーションは、新規の購入とキャンセルのイベントを処理しなければなりません。 無料プランだけを持つアプリケーションは、無料トライアル、アップグレード、ダウングレードのイベントを処理する必要はありません。 詳細については、「[アプリ内での {% data variables.product.prodname_marketplace %} API の使用](/developers/github-marketplace/using-the-github-marketplace-api-in-your-app)」を参照してください。

{% data variables.product.prodname_marketplace %}に無料のサービスとしてリスト済みのアプリケーションに有料プランを追加する場合、アプリケーションの検証をリクエストし、金銭のオンボーディングを通さなければなりません。

### 有料プラン

有料プランには2つの種類があります。

- 定額プランは、月単位及び年単位で設定された料金を課金します。

- ユニット単位の価格プランは、月単位あるいは年単位で、指定したユニットに基づいて設定された料金を課金します。 「ユニット」には好きなもの（たとえばユーザ、シート、あるいは人）を指定できます。

無料トライアルを提供したいこともあるでしょう。 無料トライアルは、OAuthもしくはGitHub Appsを無料の14日間のトライアルとして顧客に提供します。 Marketplaceの価格プランをセットアップする際に、定額あるいはユニット単位の価格プランに対する無料トライアルを提供するオプションを選択できます。

## 無料試用版

顧客は、無料トライアルを含むMarketplaceリスト上の任意の有料プランに対して、無料トライアルを開始できます。 ただし、顧客はMarketplaceの製品ごとに複数の無料トライアルを作成することはできません。

無料トライアルの期間は固定の14日間です。 顧客はトライアル期間の終了の4日前（無料トライアルの11日目）に、プランがアップグレードされるという通知を受け取ります。 顧客は、キャンセルしないかぎり、無料トライアルの終わりにトライアルを行っていたプランに自動的に登録されます。

詳細については、「[新しい購入と無料試用版の処理](/developers/github-marketplace/handling-new-purchases-and-free-trials/)」を参照してください。

{% note %}

**注:** GitHub は、キャンセル イベントの受け付け開始から 30 日以内に、キャンセルした試用版の非公開の顧客データを削除することを求めています。

{% endnote %}
