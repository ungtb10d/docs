---
ms.openlocfilehash: e7dd0182fdc70186e5b3d137ac99cebd2ff562ea
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: "147093192"
---
## ユーザーが繰り返し認証するようにリダイレクトされる

ユーザーが繰り返し SAML 認証プロンプトにリダイレクトされるループに陥る場合は、必要に応じて IdP 設定で SAML セッション期間を長くします。 

SAML 応答で送信される `SessionNotOnOrAfter` 値によって、ユーザーが認証のために IdP にリダイレクトされるタイミングが決まります。 SAML セッション期間を 2 時間以下に構成した場合、期限切れの 5 分前に SAML セッションは {% data variables.product.prodname_dotcom_the_website %} によって更新されます。 セッション期間を 5 分以下に構成した場合、ユーザーは SAML 認証ループから抜け出せなくなる可能性があります。 

この問題を解決するには、最短 SAML セッション期間を 4 時間に構成することをお勧めします。 詳細については、「[SAML 構成リファレンス](/admin/identity-and-access-management/using-saml-for-enterprise-iam/saml-configuration-reference#session-duration-and-timeout)」をご覧ください。