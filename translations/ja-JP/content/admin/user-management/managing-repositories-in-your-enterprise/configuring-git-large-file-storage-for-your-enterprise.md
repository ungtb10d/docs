---
title: Enterprise 向けの Git Large File Storage を設定する
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
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '145115126'
---
## {% data variables.large_files.product_name_long %}について

{% data reusables.enterprise_site_admin_settings.configuring-large-file-storage-short-description %} {% data variables.large_files.product_name_long %} は、単一のリポジトリ、すべての個人または Organization のリポジトリ、または Enterprise 内のすべてのリポジトリで使用できます。 特定のリポジトリまたは Organization に対して {% data variables.large_files.product_name_short %} を有効にする前に、Enterprise に対して {% data variables.large_files.product_name_short %} を有効にする必要があります。

{% data reusables.large_files.storage_assets_location %} {% data reusables.large_files.rejected_pushes %}

詳細については、「[{% data variables.large_files.product_name_long %} について](/articles/about-git-large-file-storage)」、「[Large File のバージョン管理](/enterprise/user/articles/versioning-large-files/)」、[{% data variables.large_files.product_name_long %} プロジェクト サイト](https://git-lfs.github.com/)を参照してください。

{% data reusables.large_files.can-include-lfs-objects-archives %}

## Enterprise 向けに {% data variables.large_files.product_name_long %} を設定する

{% data reusables.enterprise-accounts.access-enterprise %} {% ifversion ghes or ghae %} {% data reusables.enterprise-accounts.policies-tab %} {% else %} {% data reusables.enterprise-accounts.settings-tab %} {% endif %} {% data reusables.enterprise-accounts.options-tab %}
4. [{% data variables.large_files.product_name_short %} アクセス] で、ドロップダウン メニューを使用して、 **[有効]** または **[無効]** をクリックします。
![Git LFS アクセス](/assets/images/enterprise/site-admin-settings/git-lfs-admin-center.png)

## 個々のリポジトリ用に {% data variables.large_files.product_name_long %} を設定する

{% data reusables.enterprise_site_admin_settings.override-policy %}

{% data reusables.enterprise_site_admin_settings.access-settings %} {% data reusables.enterprise_site_admin_settings.repository-search %} {% data reusables.enterprise_site_admin_settings.click-repo %} {% data reusables.enterprise_site_admin_settings.admin-top-tab %} {% data reusables.enterprise_site_admin_settings.admin-tab %} {% data reusables.enterprise_site_admin_settings.git-lfs-toggle %}

## ユーザーアカウントまたは Organization が所有するすべてのリポジトリ用に {% data variables.large_files.product_name_long %} を設定する

{% data reusables.enterprise_site_admin_settings.access-settings %} {% data reusables.enterprise_site_admin_settings.search-user-or-org %} {% data reusables.enterprise_site_admin_settings.click-user-or-org %} {% data reusables.enterprise_site_admin_settings.admin-top-tab %} {% data reusables.enterprise_site_admin_settings.admin-tab %} {% data reusables.enterprise_site_admin_settings.git-lfs-toggle %}

{% ifversion ghes %}
## サードパーティのサーバを使うGit Large File Storageの設定

{% data reusables.large_files.storage_assets_location %} {% data reusables.large_files.rejected_pushes %}

1. {% data variables.product.product_location %} で {% data variables.large_files.product_name_short %} を無効化します。 詳細については、「[Enterprise に {% data variables.large_files.product_name_long %} を構成する](#configuring-git-large-file-storage-for-your-enterprise)」を参照してください。

2. サードパーティのサーバーを指し示す {% data variables.large_files.product_name_short %} の設定ファイルを作成します。
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

3. ユーザーごとに同じ {% data variables.large_files.product_name_short %} 構成を保持するには、カスタム `.lfsconfig` ファイルをリポジトリにコミットします。
  ```shell
  $ git add .lfsconfig
  $ git commit -m "Adding LFS config file"
  ```
3. 既存の {% data variables.large_files.product_name_short %} アセットを移行します。 詳細については、「[別の {% data variables.large_files.product_name_long %} サーバーへの移行](#migrating-to-a-different-git-large-file-storage-server)」を参照してください。

## 異なるGit Large File Storageサーバへの移行

別の {% data variables.large_files.product_name_long %} サーバーに移行する前に、サードパーティのサーバーを使用するように {% data variables.large_files.product_name_short %} を設定する必要があります。 詳細については、「[サードパーティのサーバーを使用するように {% data variables.large_files.product_name_long %} を構成する](#configuring-git-large-file-storage-to-use-a-third-party-server)」を参照してください。

1. 2 番目のリモートでリポジトリを設定します。
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

2. 古いリモートからすべてのオブジェクトを取得します。
  ```shell
  $ git lfs fetch origin --all
  > Scanning for all objects ever referenced...
  > ✔ 16 objects found
  > Fetching objects...
  > Git LFS: (16 of 16 files) 48.71 MB / 48.85 MB
  ```

3. すべてのオブジェクトを新しいリモートにプッシュします。
  ```shell
  $ git lfs push <em>NEW-REMOTE</em> --all
  > Scanning for all objects ever referenced...
  > ✔ 16 objects found
  > Pushing objects...
  > Git LFS: (16 of 16 files) 48.00 MB / 48.85 MB, 879.10 KB skipped
  ```
{% endif %}

## 参考資料

- [{% data variables.large_files.product_name_long %} プロジェクト サイト](https://git-lfs.github.com/)
