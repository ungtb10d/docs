---
title: 在 AWS 上安装 GitHub Enterprise Server
intro: '要在 Amazon Web Services (AWS) 上安装 {% data variables.product.prodname_ghe_server %}，您必须启动 Amazon Elastic Compute Cloud (EC2) 实例并创建和连接单独的 Amazon Elastic Block Store (EBS) 数据卷。'
redirect_from:
  - /enterprise/admin/guides/installation/installing-github-enterprise-on-aws
  - /enterprise/admin/installation/installing-github-enterprise-server-on-aws
  - /admin/installation/installing-github-enterprise-server-on-aws
versions:
  ghes: '*'
type: tutorial
topics:
  - Administrator
  - Enterprise
  - Infrastructure
  - Set up
shortTitle: Install on AWS
ms.openlocfilehash: f91f2337cc13690d0476c836a15ec72a5c0685cb
ms.sourcegitcommit: 5b1461b419dbef60ae9dbdf8e905a4df30fc91b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2022
ms.locfileid: '147876079'
---
## 先决条件

- {% data reusables.enterprise_installation.software-license %}
- 您必须具有能够启动 EC2 实例和创建 EBS 卷的 AWS 帐户。 有关详细信息，请参阅 [Amazon Web Services 网站](https://aws.amazon.com/)。
- 启动 {% data variables.product.product_location %} 所需的大部分操作也可以使用 AWS 管理控制台执行。 不过，我们建议安装 AWS 命令行接口 (CLI) 进行初始设置。 下文介绍了使用 AWS CLI 的示例。 有关详细信息，请参阅 Amazon 指南“[使用 AWS 管理控制台](http://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/getting-started.html)”和“[什么是 AWS 命令行接口](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)”。

{% note %}

注意：目前 {% data variables.product.prodname_ghe_server %} 不支持使用 Amazon IDMSv2 元数据 API。

{% endnote %}

本指南假定您已熟悉以下 AWS 概念：

 - [启动 EC2 实例](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/LaunchingAndUsingInstances.html)
 - [管理 EBS 卷](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html)
 - [使用安全组](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html)（用于管理对实例的网络访问）
 - [弹性 IP 地址 (EIP)](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)（强烈建议用于生产环境）
 - [EC2 和虚拟私有云](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-vpc.html)（如果你计划启动虚拟私有云）
 - [AWS 定价](https://aws.amazon.com/pricing/)（用于计算和管理成本）

有关体系结构概述，请参阅“[用于部署 GitHub Enterprise Server 的 AWS 体系结构图](/assets/images/installing-github-enterprise-server-on-aws.png)”。 

本指南建议在 AWS 上设置 {% data variables.product.product_location %} 时使用最小权限原则。 有关详细信息，请参阅 [AWS 标识和访问管理 (IAM) 文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege)。

## 硬件注意事项

{% data reusables.enterprise_installation.hardware-considerations-all-platforms %}

## 确定实例类型

在 AWS 上启动 {% data variables.product.product_location %} 之前，您需要确定最符合您的组织需求的设备类型。 若要查看 {% data variables.product.product_name %} 的最低要求，请参阅“[最低要求](#minimum-requirements)”。

{% data reusables.enterprise_installation.warning-on-scaling %}

{% data reusables.enterprise_installation.aws-instance-recommendation %}

## 选择 {% data variables.product.prodname_ghe_server %} AMI

您可以使用 {% data variables.product.prodname_ghe_server %} 门户或 AWS CLI 为 {% data variables.product.prodname_ghe_server %} 选择 Amazon Machine Image (AMI)。

{% data variables.product.prodname_ghe_server %} 的 AMI 适用于 AWS GovCloud（美国东部和美国西部）区域。 因此，受特定法规要求约束的美国客户可以在符合联邦要求的云环境中运行 {% data variables.product.prodname_ghe_server %}。 有关 AWS 符合联邦和其他标准的详细信息，请参阅 [AWS 的 GovCloud (US) 页面](http://aws.amazon.com/govcloud-us/)和 [AWS 的合规性页面](https://aws.amazon.com/compliance/)。

### 使用 {% data variables.product.prodname_ghe_server %} 门户选择 AMI

{% data reusables.enterprise_installation.download-appliance %}
3. 在“云中的 {% data variables.product.prodname_dotcom %}”下，选择“选择你的平台”下拉菜单，然后单击“Amazon Web Services”。
4. 选择“选择你的 AWS 区域”下拉菜单，然后单击所需区域。
5. 记下显示的 AMI ID。

### 使用 AWS CLI 选择 AMI

1. 使用 AWS CLI 获取由 {% data variables.product.prodname_dotcom %} 的 AWS 所有者 ID（`025577942450` 代表 GovCloud，`895557238572` 代表其他地区）发布的 {% data variables.product.prodname_ghe_server %} 图像列表。 有关详细信息，请参阅 AWS 文档中的“[describe-images](http://docs.aws.amazon.com/cli/latest/reference/ec2/describe-images.html)”。
  ```shell
  aws ec2 describe-images \
  --owners <em>OWNER ID</em> \
  --query 'sort_by(Images,&Name)[*].{Name:Name,ImageID:ImageId}' \
  --output=text
  ```
2. 记下最新 {% data variables.product.prodname_ghe_server %} 映像的 AMI ID。

## 添加安全组

如果是首次设置 AMI，您需要创建安全组并为下表中的每个端口添加新的安全组规则。 有关详细信息，请参阅 AWS 指南“[使用安全组](http://docs.aws.amazon.com/cli/latest/userguide/cli-ec2-sg.html)”。

1. 使用 AWS CLI 创建新的安全组。 有关详细信息，请参阅 AWS 文档中的“[create-security-group](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-security-group.html)”。
  ```shell
  $ aws ec2 create-security-group --group-name <em>SECURITY_GROUP_NAME</em> --description "<em>SECURITY GROUP DESCRIPTION</em>"
  ```

2. 记下新创建的安全组的安全组 ID (`sg-xxxxxxxx`)。

3. 为下表中的每个端口创建安全组规则。 有关详细信息，请参阅 AWS 文档中的“[authorize-security-group-ingress](http://docs.aws.amazon.com/cli/latest/reference/ec2/authorize-security-group-ingress.html)”。
  ```shell
  $ aws ec2 authorize-security-group-ingress --group-id <em>SECURITY_GROUP_ID</em> --protocol <em>PROTOCOL</em> --port <em>PORT_NUMBER</em> --cidr <em>SOURCE IP RANGE</em>
  ```
  此表列出了每个端口的用途。

  {% data reusables.enterprise_installation.necessary_ports %}

## 创建 {% data variables.product.prodname_ghe_server %} 实例

要创建实例，您需要使用 {% data variables.product.prodname_ghe_server %} AMI 启动 EC2 实例，并连接额外的存储卷来存储实例数据。 有关详细信息，请参阅“[硬件注意事项](#hardware-considerations)”。

{% note %}

注意：可以加密数据磁盘以获得额外的安全级别，并确保写入实例的所有数据都受到保护。 使用加密磁盘会对性能稍有影响。 如果你决定要对卷加密，强烈建议你在首次启动实例之前进行加密。
有关详细信息，请参阅 [Amazon EBS 加密指南](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html)。

{% endnote %}

{% warning %}

警告：如果决定在配置完实例后启用加密，则需要将数据迁移到加密卷，此过程将导致用户停机一段时间。

{% endwarning %}

### 启动 EC2 实例

在 AWS CLI 中，使用 AMI 以及您创建的安全组启动 EC2 实例。 附上新的块设备，以用作实例数据的存储卷，并根据您的用户许可数配置大小。 有关详细信息，请参阅 AWS 文档中的“[run-instances](http://docs.aws.amazon.com/cli/latest/reference/ec2/run-instances.html)”。

```shell
aws ec2 run-instances \
  --security-group-ids <em>SECURITY_GROUP_ID</em> \
  --instance-type <em>INSTANCE_TYPE</em> \
  --image-id <em>AMI_ID</em> \
  --block-device-mappings '[{"DeviceName":"/dev/xvdf","Ebs":{"VolumeSize":<em>SIZE</em>,"VolumeType":"<em>TYPE</em>"}}]' \
  --region <em>REGION</em> \
  --ebs-optimized
```

### 分配弹性 IP 并将其与实例关联

如果是生产实例，我们强烈建议先分配弹性 IP (EIP) 并将其与实例关联，然后再继续进行 {% data variables.product.prodname_ghe_server %} 配置。 否则，实例重新启动后将无法保留公共 IP 地址。 有关详细信息，请参阅 Amazon 文档中的“[分配弹性 IP 地址](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-eips-allocating)”和“[将弹性 IP 地址与正在运行的实例关联](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-eips-associating)”。  

如果采用生产高可用性配置，主实例和副本实例均应分配单独的 EIP。 有关详细信息，请参阅“[为高可用性配置 {% data variables.product.prodname_ghe_server %}](/enterprise/admin/guides/installation/configuring-github-enterprise-server-for-high-availability/)”。

## 配置 {% data variables.product.prodname_ghe_server %} 实例

{% data reusables.enterprise_installation.copy-the-vm-public-dns-name %} {% data reusables.enterprise_installation.upload-a-license-file %} {% data reusables.enterprise_installation.save-settings-in-web-based-mgmt-console %} 有关详细信息，请参阅“[配置 {% data variables.product.prodname_ghe_server %} 设备](/enterprise/admin/guides/installation/configuring-the-github-enterprise-server-appliance)”。
{% data reusables.enterprise_installation.instance-will-restart-automatically %} {% data reusables.enterprise_installation.visit-your-instance %}

## 延伸阅读

- [系统概述](/enterprise/admin/guides/installation/system-overview) {% ifversion ghes %}
- [关于升级到新版本](/admin/overview/about-upgrades-to-new-releases) {% endif %}
