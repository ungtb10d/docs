---
title: GitHub への接続について
intro: '{% data variables.product.prodname_desktop %} は、HTTPS を使用して {% data variables.product.prodname_dotcom %} と安全にデータを交換します。'
redirect_from:
  - /desktop/getting-started-with-github-desktop/about-connections-to-github
  - /desktop/installing-and-configuring-github-desktop/about-connections-to-github
versions:
  fpt: '*'
shortTitle: About connections
ms.openlocfilehash: 94f1e7db78504a115b233f17485f1b12299a1e11
ms.sourcegitcommit: fb047f9450b41b24afc43d9512a5db2a2b750a2a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2022
ms.locfileid: '145117389'
---
{% data variables.product.prodname_desktop %} は、リモートリポジトリからプル、プッシュ、クローン、フォークを行うと、{% data variables.product.prodname_dotcom %} に接続します。 {% data variables.product.prodname_desktop %} から {% data variables.product.prodname_dotcom %} に接続するには、アカウントを認証する必要があります。 詳細については、「[{% data variables.product.prodname_dotcom %} への認証](/desktop/getting-started-with-github-desktop/authenticating-to-github)」を参照してください。

{% data variables.product.prodname_dotcom %} への認証後、{% data variables.product.prodname_desktop %} を使用してリモートリポジトリに接続できます。 {% data variables.product.prodname_desktop %} は、認証情報（ユーザ名とパスワード、または個人アクセストークン）をキャッシュし、その認証情報を使用してリモートリポジトリへの接続ごとに認証します。

{% data variables.product.prodname_desktop %} は、HTTPS を使用して {% data variables.product.prodname_dotcom %} に接続します。 SSH を使用してクローンされたリポジトリにアクセスする際に {% data variables.product.prodname_desktop %} を使用すると、エラーが発生する可能性があります。 SSH を使用してクローンされたリポジトリに接続するには、リモートの URL を変更します。 詳細については、「[リモート リポジトリを管理する](/github/getting-started-with-github/managing-remote-repositories)」を参照してください。

## 参考資料
- 「[GitHub Desktop からのリポジトリのクローンとフォーク](/desktop/contributing-and-collaborating-using-github-desktop/cloning-and-forking-repositories-from-github-desktop)」
