---
title: 创建强密码
intro: '使用密码管理器以强大而唯一的密码保护您在 {% ifversion ghae %}{% data variables.product.product_name %}{% else %}{% data variables.product.product_location %}{% endif %} 上的帐户。'
redirect_from:
  - /articles/what-is-a-strong-password
  - /articles/creating-a-strong-password
  - /github/authenticating-to-github/creating-a-strong-password
  - /github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-strong-password
versions:
  fpt: '*'
  ghes: '*'
  ghec: '*'
topics:
  - Identity
  - Access management
shortTitle: Create a strong password
ms.openlocfilehash: 97473f9b04c8d033471f89cac9a0b0d08bebcba3
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2022
ms.locfileid: '145084655'
---
您必须在 {% ifversion ghae %}{% data variables.product.product_name %}{% else %}{% data variables.product.product_location %}{% endif %} 上为您的帐户选择或生成一个密码，该密码至少是：
- {% ifversion ghes %}七{% else %}八{% endif %}个字符且包含数字和小写字母，或
- 至少 15 个字符，任意字符组合

为确保您的帐户安全，我们建议您遵循以下最佳实践：
- 使用密码管理器（例如 [LastPass](https://lastpass.com/) 或 [1Password](https://1password.com/)）生成至少 15 个字符的密码。
- 为 {% data variables.product.product_name %} 生成唯一的密码。 如果您在其他地方使用 {% data variables.product.product_name %} 密码，并且该服务遭到入侵，则攻击者或其他恶意行为者可能会使用该信息访问您在 {% ifversion ghae %}{% data variables.product.product_name %}{% else %}{% data variables.product.product_location %}{% endif %} 上的帐户。

- 为您的帐户配置双重身份验证。 有关详细信息，请参阅[关于双因素身份验证](/articles/about-two-factor-authentication)。
- 不与任何人分享您的密码，即使是潜在协作者。 在 {% data variables.product.product_name %} 上每个人都应使用自己的个人帐户。 有关协作方式的详细信息，请参阅：“[邀请协作者加入个人存储库](/articles/inviting-collaborators-to-a-personal-repository)”、“[关于协作开发模型](/articles/about-collaborative-development-models/)”或“[与组织中的团体协作](/organizations/collaborating-with-groups-in-organizations/)。”

{% data reusables.repositories.blocked-passwords %}

您只能使用密码通过浏览器登录 {% data variables.product.product_name %}。 使用其他方式（例如命令行或 API）向 {% data variables.product.product_name %} 验证时，应使用其他凭据。 有关详细信息，请参阅“[关于对 {% data variables.product.prodname_dotcom %} 的身份验证](/github/authenticating-to-github/about-authentication-to-github)”。 

{% ifversion fpt or ghec %}{% data reusables.user-settings.password-authentication-deprecation %}{% endif %}

## 延伸阅读

- [在 Git 中缓存 {% data variables.product.product_name %} 凭据](/github/getting-started-with-github/caching-your-github-credentials-in-git/)
- [保护帐户和数据安全](/articles/keeping-your-account-and-data-secure/)
