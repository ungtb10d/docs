---
title: パッケージの公開
intro: '{% data variables.product.prodname_registry %}にパッケージを公開し、そのパッケージを他者がダウンロードして再利用できるようにすることができます。'
product: '{% data reusables.gated-features.packages %}'
redirect_from:
  - /github/managing-packages-with-github-packages/publishing-a-package
  - /packages/publishing-and-managing-packages/publishing-a-package
permissions: Anyone with write permissions for a repository can publish a package to that repository.
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
ms.openlocfilehash: e13e33b6085fbdd736d77d7d8b4998595ea7ffcc
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '145140515'
---
{% data reusables.package_registry.packages-ghes-release-stage %} {% data reusables.package_registry.packages-ghae-release-stage %}

## 公開されたパッケージについて

パッケージページ上のインストール及び利用方法の説明といった、説明やその他の詳細を提供することによって、パッケージを理解して利用しやすくできます。 {% data variables.product.product_name %} は各バージョンについて、公開日、ダウンロードのアクティビティ、最近のバージョンなどのメタデータを提供します。 パッケージ ページの例については、[@Codertocat/hello-world-npm](https://github.com/Codertocat/hello-world-npm/packages/10696?version=1.0.1) を参照してください。

{% data reusables.package_registry.public-or-private-packages %} リポジトリは複数のパッケージに接続できます。 混乱を避けるため、READMEと説明で各パッケージに関する情報を明確に提供してください。

{% ifversion fpt or ghec %} 新しいバージョンのパッケージでセキュリティの脆弱性が解決される場合は、リポジトリでセキュリティ アドバイザリを公開する必要があります。 {% data variables.product.prodname_dotcom %} は公開された各セキュリティアドバイザリを確認し、それを使用して、影響を受けるリポジトリに {% data variables.product.prodname_dependabot_alerts %} を送信できます。 詳細については、「[リポジトリの GitHub セキュリティ アドバイザリについて](/github/managing-security-vulnerabilities/about-github-security-advisories)」を参照してください。
{% endif %}

## パッケージの公開

以下の同じ一般的なガイドラインに従って、{% ifversion fpt or ghae or ghec %}サポートされているいずれかのパッケージのクライアント{% else %}インスタンスで有効化しているパッケージのタイプ{% endif %}を使い、{% data variables.product.prodname_registry %} にパッケージを公開できます。

1. 実行したいタスクに対して適切なスコープを持つ既存のアクセストークンを作成もしくは利用してください。 詳細については、「[{% data variables.product.prodname_registry %} へのアクセス許可](/packages/learn-github-packages/about-permissions-for-github-packages)」を参照してください。
2. 使用するパッケージクライアントについての指示に従って、アクセストークンを使って{% data variables.product.prodname_registry %}の認証をしてください。
3. 使用するパッケージクライアントに関する指示に従って、パッケージを公開してください。

パッケージ クライアントに固有の手順については、「[GitHub Packages レジストリの利用](/packages/working-with-a-github-packages-registry)」を参照してください。

パッケージを公開した後は、{% data variables.product.prodname_dotcom %}上でそのパッケージを見ることができます。 詳しくは、「[パッケージの表示](/packages/learn-github-packages/viewing-packages)」をご覧ください。
