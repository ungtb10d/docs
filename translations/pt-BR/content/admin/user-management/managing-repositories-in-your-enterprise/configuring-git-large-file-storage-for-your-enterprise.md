---
title: Configurar o Large File Storage do Git para a sua sempresa
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
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '145094580'
---
## Sobre o {% data variables.large_files.product_name_long %}

{% data reusables.enterprise_site_admin_settings.configuring-large-file-storage-short-description %} Você pode usar {% data variables.large_files.product_name_long %} com um único repositório, todos os seus repositórios pessoais ou organizacionais, ou com cada repositório na sua empresa. Antes de habilitar {% data variables.large_files.product_name_short %} para repositórios ou organizações específicos, você deve habilitar {% data variables.large_files.product_name_short %} para a sua empresa.

{% data reusables.large_files.storage_assets_location %} {% data reusables.large_files.rejected_pushes %}

Para obter mais informações, confira "[Sobre o {% data variables.large_files.product_name_long %}](/articles/about-git-large-file-storage)", "[Como fazer o controle de versão de arquivos grandes](/enterprise/user/articles/versioning-large-files/)" e o [site de projeto do {% data variables.large_files.product_name_long %}](https://git-lfs.github.com/).

{% data reusables.large_files.can-include-lfs-objects-archives %}

## Configurar {% data variables.large_files.product_name_long %} para a sua empresa

{% data reusables.enterprise-accounts.access-enterprise %} {% ifversion ghes or ghae %} {% data reusables.enterprise-accounts.policies-tab %} {% else %} {% data reusables.enterprise-accounts.settings-tab %} {% endif %} {% data reusables.enterprise-accounts.options-tab %}
4. Em "Acesso ao {% data variables.large_files.product_name_short %}", use o menu suspenso e clique em **Habilitado** ou **Desabilitado**.
![Acesso ao Git LFS](/assets/images/enterprise/site-admin-settings/git-lfs-admin-center.png)

## Configurar o {% data variables.large_files.product_name_long %} em um repositório específico

{% data reusables.enterprise_site_admin_settings.override-policy %}

{% data reusables.enterprise_site_admin_settings.access-settings %} {% data reusables.enterprise_site_admin_settings.repository-search %} {% data reusables.enterprise_site_admin_settings.click-repo %} {% data reusables.enterprise_site_admin_settings.admin-top-tab %} {% data reusables.enterprise_site_admin_settings.admin-tab %} {% data reusables.enterprise_site_admin_settings.git-lfs-toggle %}

## Configurar o {% data variables.large_files.product_name_long %} para cada repositório pertencente a uma conta ou organização

{% data reusables.enterprise_site_admin_settings.access-settings %} {% data reusables.enterprise_site_admin_settings.search-user-or-org %} {% data reusables.enterprise_site_admin_settings.click-user-or-org %} {% data reusables.enterprise_site_admin_settings.admin-top-tab %} {% data reusables.enterprise_site_admin_settings.admin-tab %} {% data reusables.enterprise_site_admin_settings.git-lfs-toggle %}

{% ifversion ghes %}
## Configurar o Git Large File Storage para uso em servidores de terceiros

{% data reusables.large_files.storage_assets_location %} {% data reusables.large_files.rejected_pushes %}

1. Desabilite {% data variables.large_files.product_name_short %} em {% data variables.product.product_location %}. Para obter mais informações, confira "[Como configurar o {% data variables.large_files.product_name_long %} para sua empresa](#configuring-git-large-file-storage-for-your-enterprise)".

2. Crie um arquivo de configuração do {% data variables.large_files.product_name_short %} que aponte para o servidor de terceiros.
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

3. Para manter a mesma configuração do {% data variables.large_files.product_name_short %} para todos os usuários, faça commit de um arquivo `.lfsconfig` personalizado no repositório.
  ```shell
  $ git add .lfsconfig
  $ git commit -m "Adding LFS config file"
  ```
3. Migre qualquer ativo do {% data variables.large_files.product_name_short %}. Para obter mais informações, confira "[Como migrar para outro servidor do {% data variables.large_files.product_name_long %}](#migrating-to-a-different-git-large-file-storage-server)".

## Migrar para outro servidor do Git Large File Storage

Antes de migrar para outro servidor do {% data variables.large_files.product_name_long %}, configure o {% data variables.large_files.product_name_short %} para usar um servidor de terceiros. Para obter mais informações, confira "[Como configurar o {% data variables.large_files.product_name_long %} para usar um servidor de terceiros](#configuring-git-large-file-storage-to-use-a-third-party-server)".

1. Configure o repositório com outro remote.
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

2. Faça fetch de todos os objetos do remote antigo.
  ```shell
  $ git lfs fetch origin --all
  > Scanning for all objects ever referenced...
  > ✔ 16 objects found
  > Fetching objects...
  > Git LFS: (16 of 16 files) 48.71 MB / 48.85 MB
  ```

3. Faça push de todos os objetos para o remote novo.
  ```shell
  $ git lfs push <em>NEW-REMOTE</em> --all
  > Scanning for all objects ever referenced...
  > ✔ 16 objects found
  > Pushing objects...
  > Git LFS: (16 of 16 files) 48.00 MB / 48.85 MB, 879.10 KB skipped
  ```
{% endif %}

## Leitura adicional

- [Site de projeto do {% data variables.large_files.product_name_long %}](https://git-lfs.github.com/)
