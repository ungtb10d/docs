---
title: Verificar tu dirección de correo electrónico
intro: 'Verificar tu dirección principal de correo electrónico garantiza mayor seguridad, permite que el personal {% data variables.product.prodname_dotcom %} te ayude mejor si olvidas tu contraseña y te brinda acceso a más funciones en {% data variables.product.prodname_dotcom %}.'
redirect_from:
  - /articles/troubleshooting-email-verification
  - /articles/setting-up-email-verification
  - /articles/verifying-your-email-address
  - /github/getting-started-with-github/verifying-your-email-address
  - /github/getting-started-with-github/signing-up-for-github/verifying-your-email-address
versions:
  fpt: '*'
  ghec: '*'
topics:
  - Accounts
shortTitle: Verify your email address
ms.openlocfilehash: 75c455907ab0cc89f1ba8b30d6fa1d37f2d9798f
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2022
ms.locfileid: '145126241'
---
## Acerca de la verificación del correo electrónico

Puedes verificar tu dirección de correo electrónico después de registrarte con una cuenta nueva o cuando agregas una dirección de correo electrónico nueva. Si una dirección de correo electrónico no es válida para el envío o devuelve correos, quedará como no verificada.

Si no verificas tu dirección de correo electrónico, no podrás hacer lo siguiente:
  - Crear o bifurcar repositorios
  - Crear propuestas o solicitudes de extracción
  - Comentar propuestas, solicitudes de extracción o confirmaciones
  - Autorizar aplicaciones de {% data variables.product.prodname_oauth_app %}
  - Generar tokens de acceso personal
  - Recibir notificaciones por correo electrónico
  - Poner estrellas en repositorios
  - Crear o actualizar tableros de proyecto, incluido agregar tarjetas
  - Crear o actualizar gists
  - Crear o utilizar {% data variables.product.prodname_actions %}
  - Patrocinar desarrolladores con {% data variables.product.prodname_sponsors %}

{% warning %}

**Advertencias**:

- {% data reusables.user-settings.no-verification-disposable-emails %}
- {% data reusables.user-settings.verify-org-approved-email-domain %}

{% endwarning %}

## Verificar tu dirección de correo electrónico

{% data reusables.user-settings.access_settings %} {% data reusables.user-settings.emails %}
1. En la dirección de correo electrónico, haga clic en **Resend verification email**.
  ![Vínculo para reenviar el correo electrónico de verificación](/assets/images/help/settings/email-verify-button.png)
4. {% data variables.product.prodname_dotcom %} te enviará un correo electrónico con un enlace. Después de hacer clic en el enlace, se te llevará a tu tablero {% data variables.product.prodname_dotcom %} y verás un mensaje emergente de confirmación.
  ![Banner que confirma que se verificó el correo electrónico](/assets/images/help/settings/email-verification-confirmation-banner.png)

## Solución de problemas de verificación de correo electrónico

### No se pudo enviar el correo electrónico de verificación

{% data reusables.user-settings.no-verification-disposable-emails %}

### Página de error después de hacer clic en el enlace de verificación

El enlace de verificación vence después de 24 horas. Si no verificas tu correo electrónico dentro de las 24 horas, puedes solicitar otro enlace de verificación de correo electrónico. Para obtener más información, consulte "[Comprobar la dirección de correo electrónico](/articles/verifying-your-email-address)".

Si haces clic en el enlace del correo electrónico de confirmación dentro de las siguientes 24 horas y se te dirige a una página de error, deberías garantizar que estés firmado en la cuenta correcta de {% data variables.product.product_location %}.

1. {% data variables.product.signout_link %} de tu cuenta personal en {% data variables.product.product_location %}.
2. Sal y vuelve a iniciar tu navegador.
3. {% data variables.product.signin_link %} a tu cuenta personal de {% data variables.product.product_location %}.
4. Haz clic en el enlace de verificación del correo electrónico que te enviamos.

## Información adicional

- "[Cambiar tu dirección principal de correo electrónico](/articles/changing-your-primary-email-address)"
