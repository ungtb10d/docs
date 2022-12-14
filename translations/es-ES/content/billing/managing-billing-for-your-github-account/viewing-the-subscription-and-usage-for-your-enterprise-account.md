---
title: Ver la suscripción y el uso de tu cuenta de empresa
intro: 'Puedes ver {% ifversion ghec %}la suscripción, {% endif %}el uso de licencia{% ifversion ghec %}, facturas, historial de pagos y otra información de facturación{% endif %} para {% ifversion ghec %}tu cuenta empresarial{% elsif ghes %}{% data variables.product.product_location_enterprise %}{% endif %}.'
permissions: 'Enterprise owners {% ifversion ghec %}and billing managers {% endif %}can access and manage all billing settings for enterprise accounts.'
redirect_from:
  - /github/setting-up-and-managing-your-enterprise/managing-your-enterprise-account/viewing-the-subscription-and-usage-for-your-enterprise-account
  - /github/setting-up-and-managing-your-enterprise-account/viewing-the-subscription-and-usage-for-your-enterprise-account
  - /articles/viewing-the-subscription-and-usage-for-your-enterprise-account
  - /github/setting-up-and-managing-your-enterprise/viewing-the-subscription-and-usage-for-your-enterprise-account
versions:
  ghec: '*'
  ghes: '*'
topics:
  - Enterprise
shortTitle: View subscription & usage
ms.openlocfilehash: 503f870542180cfe9ae088a161370b9370d36f1c
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2022
ms.locfileid: '145189642'
---
## Acerca de la facturación para las cuentas de empresa

Puedes ver información general de {% ifversion ghec %}tu suscripción y del uso de tu {% elsif ghes %}licencia pagada{% endif %} para {% ifversion ghec %}tu{% elsif ghes %}la{% endif %} cuenta empresarial en {% ifversion ghec %}{% data variables.product.prodname_dotcom_the_website %}{% elsif ghes %}{% data variables.product.product_location %}{% endif %}.{% ifversion ghec %} {% data reusables.enterprise.create-an-enterprise-account %} Para obtener más información, consulta "[Creación de una cuenta empresarial](/enterprise-cloud@latest/admin/overview/creating-an-enterprise-account)."{% endif %}

Para los clientes de {% data variables.product.prodname_enterprise %} a quienes se factura{% ifversion ghes %} quienes usan tanto {% data variables.product.prodname_ghe_cloud %} como {% data variables.product.prodname_ghe_server %}{% endif %}, cada factura incluye detalles sobre los servicios que se cobran de todos los productos. Por ejemplo, adicionalmente a su uso de {% ifversion ghec %}{% data variables.product.prodname_ghe_cloud %}{% elsif ghes %}{% data variables.product.product_name %}{% endif %}, puede tener un uso de {% data variables.product.prodname_GH_advanced_security %}{% ifversion ghec %}, {% elsif ghes %}. También puedes tener uso en {% data variables.product.prodname_dotcom_the_website %}, como {% endif %}licencias de pago en organizaciones fuera de tu cuenta empresarial, paquetes de datos para {% data variables.large_files.product_name_long %} o suscripciones en apps dentro de {% data variables.product.prodname_marketplace %}. Para obtener más información sobre las facturas, consulte "[Administración de facturas para la empresa]({% ifversion ghes %}/enterprise-cloud@latest{% endif %}/billing/managing-billing-for-your-github-account/managing-invoices-for-your-enterprise){% ifversion ghec %}".{% elsif ghes %}" en la documentación de {% data variables.product.prodname_dotcom_the_website %}.{% endif %}

{% ifversion ghec %}

Adicionalmente a los propietarios de empresas, los gerentes de facturación pueden ver la suscripción y el uso de tu cuenta empresarial. Para obtener más información, consulte "[Roles en una empresa](/github/setting-up-and-managing-your-enterprise/managing-users-in-your-enterprise/roles-in-an-enterprise#billing-manager)" y "[Invitación de personas para que administren la empresa](/admin/user-management/managing-users-in-your-enterprise/inviting-people-to-manage-your-enterprise)".

{% data reusables.enterprise-accounts.billing-microsoft-ea-overview %} Para más información, consulte "[Conexión de una suscripción de Azure a la empresa](/billing/managing-billing-for-your-github-account/connecting-an-azure-subscription-to-your-enterprise)".

{% endif %}

{% ifversion ghes %}

Si quiere ver información general sobre su suscripción y su uso de {% data variables.product.prodname_enterprise %} y de cualquier servicio relacionado en {% data variables.product.prodname_dotcom_the_website %}, consulte "[Visualización de la suscripción y el uso de la cuenta empresarial](/enterprise-cloud@latest/billing/managing-billing-for-your-github-account/viewing-the-subscription-and-usage-for-your-enterprise-account)" en la documentación de {% data variables.product.prodname_ghe_cloud %}.

{% endif %}

## Ver la suscripción y el uso de tu cuenta de empresa

Puedes ver la suscripción y uso de tu empresa y descargar un archivo con los detalles de la licencia.

{% data reusables.billing.license-statuses %}

{% data reusables.enterprise-accounts.access-enterprise %} {% data reusables.enterprise-accounts.settings-tab %} {% data reusables.enterprise-accounts.license-tab %}
1. En "Licencias de Usuario", ve tus licencias totales, la cantidad de licencias consumidas y la fecha de vencimiento de tu suscripción.
  {% ifversion ghec %}![Información sobre licencias y suscripciones en la configuración de facturación de la empresa](/assets/images/help/business-accounts/billing-license-info.png){% else %} ![Información sobre licencias y suscripciones en la configuración de facturación de la empresa](/assets/images/enterprise/enterprise-server/enterprise-server-billing-license-info.png){% endif %}
1. Opcionalmente, para ver los detalles del uso de una licencia o descargar un archivo {% ifversion ghec %}CSV{% elsif ghes %}JSON{% endif %} con los detalles de la misma{% ifversion ghec %}, a la derecha de "User Licenses" (Licencias de usuario){% endif %}, haga clic en **View {% ifversion ghec %}details (Ver detalles){% elsif ghes %}users (Ver usuarios){% endif %}** o{% ifversion ghec %}{% octicon "download" aria-label="The download icon" %}{% elsif ghes %}**Exportar licencias de uso**{% endif %}.{% ifversion ghec %} ![Botón "View details" (Ver detalles) y botón con el icono de descarga a la derecha de "User Licenses" (Licencias de usuario)](/assets/images/help/business-accounts/billing-license-info-click-view-details-or-download.png){% endif %}{% ifversion ghec %}
1. Opcionalmente, para ver los detalles de uso de otras características, en la barra lateral izquierda, haga clic en **Billing** (Facturación).
  ![Pestaña de facturación en la barra lateral de configuración de la cuenta de empresa](/assets/images/help/business-accounts/settings-billing-tab.png) {% endif %}
