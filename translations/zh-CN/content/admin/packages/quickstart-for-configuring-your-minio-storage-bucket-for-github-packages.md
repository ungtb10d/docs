---
title: 为 GitHub Packages 配置 MinIO 存储桶的快速入门
intro: '配置您的自定义 MinIO 存储桶，用于 {% data variables.product.prodname_registry %}。'
versions:
  ghes: '*'
type: quick_start
topics:
  - Packages
  - Enterprise
  - Storage
shortTitle: Quickstart for MinIO
ms.openlocfilehash: 5e3da768643c3979380d3fb205518a7053c7360b
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2022
ms.locfileid: '146688971'
---
{% data reusables.package_registry.packages-ghes-release-stage %}

在 {% data variables.product.product_location_enterprise %} 上启用和配置 {% data variables.product.prodname_registry %} 之前，您必须准备第三方存储解决方案。

MinIO 在企业上提供对象存储并支持 S3 API 和 {% data variables.product.prodname_registry %}。

此快速入门将演示如何使用 Docker 设置 MinIO 以与 {% data variables.product.prodname_registry %} 使用，但除了 Docker 之外，您还有其他用于管理 MinIO 的选项。 有关 MinIO 的详细信息，请参阅官方 [MinIO 文档](https://docs.min.io/)。

## 1. 根据需求选择 MinIO 模式

| MinIO 模式 | 优化对象 | 需要存储基础架构 |
|----|----|----|
| 独立 MinIO（在单个主机上） | 快速设置 |  空值 |
| MinIO 作为 NAS 网关 |  NAS（网络连接存储）| NAS 设备 |
| 群集式 MinIO（也称为分布式 MinIO）|  数据安全性 | 在群集中运行的存储服务器 |

有关选项的详细信息，请参阅官方 [MinIO 文档](https://docs.min.io/)。

{% warning %}

警告：MinIO 已宣布删除 MinIO 网关。 从 2022 年 6 月 1 日起，当前 MinIO NAS 网关实施的支持和 Bug 修复将仅通过其 LTS 支持合同提供给付费客户。 如果要继续使用 MinIO 网关与 {% data variables.product.prodname_registry %}，我们建议转向 MinIO LTS 支持。 有关详细信息，请参阅[计划删除 minio/minio 存储库中的适用于 GCS、Azure 和 HDFS 的 MinIO 网格](https://github.com/minio/minio/issues/14331)。

其他 MinIO 模式在标准支持下仍然可用。

{% endwarning %}

## 2. 安装、运行和登录到 MinIO

1. 为 MinIO 设置首选环境变量。

    这些示例使用 `MINIO_DIR`：
    ```shell
    $ export MINIO_DIR=$(pwd)/minio
    $ mkdir -p $MINIO_DIR
    ```

2. 安装 MinIO。

    ```shell
    $ docker pull minio/minio
    ```
    有关详细信息，请参阅官方“[MinIO 快速入门指南](https://docs.min.io/docs/minio-quickstart-guide)”。

3. 使用您的 MinIO 访问密钥登录 MinIO。

    {% linux %}
    ```shell
    $ export MINIO_ACCESS_KEY=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1)
    # this one is actually a secret, so careful
    $ export MINIO_SECRET_KEY=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1)
    ```
    {% endlinux %}

    {% mac %}
    ```shell
    $ export MINIO_ACCESS_KEY=$(cat /dev/urandom | LC_CTYPE=C tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1)
    # this one is actually a secret, so careful
    $ export MINIO_SECRET_KEY=$(cat /dev/urandom | LC_CTYPE=C tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1)
    ```
    {% endmac %}

    您可以使用环境变量访问 MinIO 密钥：

    ```shell
    $ echo $MINIO_ACCESS_KEY
    $ echo $MINIO_SECRET_KEY
    ```

4. 在您选择的模式下运行 MinIO。

   * 在单一主机上使用 Docker 运行 MinIO：

     ```shell
     $ docker run -p 9000:9000 \
             -v $MINIO_DIR:/data \
             -e "MINIO_ACCESS_KEY=$MINIO_ACCESS_KEY" \
             -e "MINIO_SECRET_KEY=$MINIO_SECRET_KEY" \
             minio/minio server /data
     ```

     有关详细信息，请参阅“[MinIO Docker 快速入门指南](https://docs.min.io/docs/minio-docker-quickstart-guide.html)”。

   * 使用 Docker 作为 NAS 网关运行 MinIO：

     此设置对于已经有 NAS 用作 {% data variables.product.prodname_registry %} 的备份存储的部署非常有用。

     ```shell
     $ docker run -p 9000:9000 \
             -v $MINIO_DIR:/data \
             -e "MINIO_ACCESS_KEY=$MINIO_ACCESS_KEY" \
             -e "MINIO_SECRET_KEY=$MINIO_SECRET_KEY" \
             minio/minio gateway nas /data
     ```

   * 使用 Docker 作为集群运行 MinIO： 此 MinIO 部署使用多个主机和 MinIO 的擦除编码来提供最强的数据保护。 若要在群集模式下运行 MinIO，请参阅“[分布式 MinIO 快速入门指南](https://docs.min.io/docs/distributed-minio-quickstart-guide.html)”。

## 3. 为 {% data variables.product.prodname_registry %} 创建 MinIO 存储桶

1. 安装 MinIO 客户端。  

    ```shell
    $ docker pull minio/mc
    ```

2. 使用 {% data variables.product.prodname_ghe_server %} 可以访问的主机 URL 创建存储桶。

   * 本地部署示例：

     ```shell
     $ export MC_HOST_minio="http://${MINIO_ACCESS_KEY}:${MINIO_SECRET_KEY} @localhost:9000"
     $ docker run minio/mc <em>BUCKET-NAME</em>
     ```

     此示例可用于 MinIO 单机版或作为 NAS 网关的 MinIO。

   * 集群部署示例：

     ```shell
     $ export MC_HOST_minio="http://${MINIO_ACCESS_KEY}:${MINIO_SECRET_KEY} @minioclustername.example.com:9000"
     $ docker run minio/mc mb packages
     ```

## 后续步骤

要完成 {% data variables.product.prodname_registry %} 的存储配置，您需要复制 MinIO 存储 URL：

  ```
  echo "http://${MINIO_ACCESS_KEY}:${MINIO_SECRET_KEY}@minioclustername.example.com:9000"
  ```

有关后续步骤，请参阅“[使用 MinIO 启用 {% data variables.product.prodname_registry %}](/admin/packages/enabling-github-packages-with-minio)”。
