---
title: Configurar el almacenamiento de archivos grandes de Git para tu empresa
intro: '{% data reusables.enterprise_site_admin_settings.configuring-large-file-storage-short-description %}'
redirect_from:
  - /enterprise/admin/guides/installation/configuring-git-large-file-storage-on-github-enterprise
  - /enterprise/admin/installation/configuring-git-large-file-storage-on-github-enterprise-server
  - /enterprise/admin/installation/configuring-git-large-file-storage
  - /enterprise/admin/installation/configuring-git-large-file-storage-to-use-a-third-party-server
  - /enterprise/admin/installation/migrating-to-a-different-git-large-file-storage-server
  - /enterprise/admin/articles/configuring-git-large-file-storage-for-a-repository
  - /enterprise/admin/articles/configuring-git-large-file-storage-for-every-repository-owned-by-a-user-account-or-organization
  - /enterprise/admin/articles/configuring-git-large-file-storage-for-your-appliance
  - /enterprise/admin/guides/installation/migrating-to-different-large-file-storage-server
  - /enterprise/admin/user-management/configuring-git-large-file-storage-for-your-enterprise
  - /admin/user-management/configuring-git-large-file-storage-for-your-enterprise
versions:
  ghes: '*'
  ghae: '*'
type: how_to
topics:
  - Git
  - Enterprise
  - LFS
  - Storage
shortTitle: Configure Git LFS
ms.openlocfilehash: d6364bc1d45643ebb3dc1c46cec467515fd4da55
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2022
ms.locfileid: '145115129'
---
## Acerca de {% data variables.large_files.product_name_long %}

{% data reusables.enterprise_site_admin_settings.configuring-large-file-storage-short-description %} Puedes utilizar {% data variables.large_files.product_name_long %} con un solo repositorio, con todos tus repositorios personales o de organización, o con todos los repositorios de tu empresa. Antes de que puedas habilitar a {% data variables.large_files.product_name_short %} para repositorios u organizaciones específicos, necesitas habilitar a {% data variables.large_files.product_name_short %} en tu empresa.

{% data reusables.large_files.storage_assets_location %} {% data reusables.large_files.rejected_pushes %}

Para obtener más información, vea "[Acerca de {% data variables.large_files.product_name_long %}](/articles/about-git-large-file-storage)", "[Control de versiones de archivos grandes](/enterprise/user/articles/versioning-large-files/)" y el [sitio del proyecto {% data variables.large_files.product_name_long %}](https://git-lfs.github.com/).

{% data reusables.large_files.can-include-lfs-objects-archives %}

## Configurar a {% data variables.large_files.product_name_long %} para tu empresa

{% data reusables.enterprise-accounts.access-enterprise %} {% ifversion ghes or ghae %} {% data reusables.enterprise-accounts.policies-tab %} {% else %} {% data reusables.enterprise-accounts.settings-tab %} {% endif %} {% data reusables.enterprise-accounts.options-tab %}
4. En "Acceso a {% data variables.large_files.product_name_short %}", use el menú desplegable y haga clic en **Habilitado** o **Deshabilitado**.
![Acceso a Git LFS](/assets/images/enterprise/site-admin-settings/git-lfs-admin-center.png)

## Configurar {% data variables.large_files.product_name_long %} para un repositorio individual

{% data reusables.enterprise_site_admin_settings.override-policy %}

{% data reusables.enterprise_site_admin_settings.access-settings %} {% data reusables.enterprise_site_admin_settings.repository-search %} {% data reusables.enterprise_site_admin_settings.click-repo %} {% data reusables.enterprise_site_admin_settings.admin-top-tab %} {% data reusables.enterprise_site_admin_settings.admin-tab %} {% data reusables.enterprise_site_admin_settings.git-lfs-toggle %}

## Configurar {% data variables.large_files.product_name_long %} para cada repositorio que pertenezca a una cuenta de usuario u organización

{% data reusables.enterprise_site_admin_settings.access-settings %} {% data reusables.enterprise_site_admin_settings.search-user-or-org %} {% data reusables.enterprise_site_admin_settings.click-user-or-org %} {% data reusables.enterprise_site_admin_settings.admin-top-tab %} {% data reusables.enterprise_site_admin_settings.admin-tab %} {% data reusables.enterprise_site_admin_settings.git-lfs-toggle %}

{% ifversion ghes %}
## Configurar Large File Storage de Git para usar un servidor de terceros

{% data reusables.large_files.storage_assets_location %} {% data reusables.large_files.rejected_pushes %}

1. Inhabilita a {% data variables.large_files.product_name_short %} en {% data variables.product.product_location %}. Para más información, vea "[Configuración de {% data variables.large_files.product_name_long %} para su empresa](#configuring-git-large-file-storage-for-your-enterprise)".

2. Crea un archivo de configuración {% data variables.large_files.product_name_short %} que apunte al servidor de terceros.
  ```shell
  # Show default configuration
  $ git lfs env
  > git-lfs/1.1.0 (GitHub; darwin amd64; go 1.5.1; git 94d356c)
  > git version 2.7.4 (Apple Git-66)
  &nbsp;
  > Endpoint=https://<em>GITHUB-ENTERPRISE-HOST</em>/path/to/repo/info/lfs (auth=basic)
  &nbsp;
  # Create .lfsconfig that points to third party server.
  $ git config -f .lfsconfig remote.origin.lfsurl https://<em>THIRD-PARTY-LFS-SERVER</em>/path/to/repo
  $ git lfs env
  > git-lfs/1.1.0 (GitHub; darwin amd64; go 1.5.1; git 94d356c)
  > git version 2.7.4 (Apple Git-66)
  &nbsp;
  > Endpoint=https://<em>THIRD-PARTY-LFS-SERVER</em>/path/to/repo/info/lfs (auth=none)
  &nbsp;
  # Show the contents of .lfsconfig
  $ cat .lfsconfig
  [remote "origin"]
  lfsurl = https://<em>THIRD-PARTY-LFS-SERVER</em>/path/to/repo
  ```

3. A fin de mantener la misma configuración de {% data variables.large_files.product_name_short %} para cada usuario, confirme un archivo `.lfsconfig` personalizado en el repositorio.
  ```shell
  $ git add .lfsconfig
  $ git commit -m "Adding LFS config file"
  ```
3. Migra cualquier activo {% data variables.large_files.product_name_short %} existente. Para obtener más información, vea "[Migración a un servidor de {% data variables.large_files.product_name_long %} distinto](#migrating-to-a-different-git-large-file-storage-server)".

## Migrar a un servidor de Git Large File Storage diferente

Antes de migrarte a un servidor de {% data variables.large_files.product_name_long %} diferente, debes configurar a {% data variables.large_files.product_name_short %} para que utilice un servidor de terceros. Para más información, vea "[Configuración de {% data variables.large_files.product_name_long %} para usar un servidor de terceros](#configuring-git-large-file-storage-to-use-a-third-party-server)".

1. Configura un repositorio con un segundo remoto.
  ```shell
  $ git remote add <em>NEW-REMOTE</em> https://<em>NEW-REMOTE-HOSTNAME</em>/path/to/repo
  &nbsp;
  $ git lfs env
  > git-lfs/1.1.0 (GitHub; darwin amd64; go 1.5.1; git 94d356c)
  > git version 2.7.4 (Apple Git-66)
  &nbsp;
  > Endpoint=https://<em>GITHUB-ENTERPRISE-HOST</em>/path/to/repo/info/lfs (auth=basic)
  > Endpoint (<em>NEW-REMOTE</em>)=https://<em>NEW-REMOTE-HOSTNAME</em>/path/to/repo/info/lfs (auth=none)
  ```

2. Extrae todos los objetos del remoto anterior.
  ```shell
  $ git lfs fetch origin --all
  > Scanning for all objects ever referenced...
  > ✔ 16 objects found
  > Fetching objects...
  > Git LFS: (16 of 16 files) 48.71 MB / 48.85 MB
  ```

3. Extrae todos los objetos a un nuevo remoto.
  ```shell
  $ git lfs push <em>NEW-REMOTE</em> --all
  > Scanning for all objects ever referenced...
  > ✔ 16 objects found
  > Pushing objects...
  > Git LFS: (16 of 16 files) 48.00 MB / 48.85 MB, 879.10 KB skipped
  ```
{% endif %}

## Información adicional

- [Sitio del proyecto {% data variables.large_files.product_name_long %}](https://git-lfs.github.com/)
