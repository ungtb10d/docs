---
title: 将工作流程数据存储为构件
shortTitle: Storing workflow artifacts
intro: 构件允许您在工作流程完成后，分享工作流程中作业之间的数据并存储数据。
redirect_from:
  - /articles/persisting-workflow-data-using-artifacts
  - /github/automating-your-workflow-with-github-actions/persisting-workflow-data-using-artifacts
  - /actions/automating-your-workflow-with-github-actions/persisting-workflow-data-using-artifacts
  - /actions/configuring-and-managing-workflows/persisting-workflow-data-using-artifacts
  - /actions/guides/storing-workflow-data-as-artifacts
  - /actions/advanced-guides/storing-workflow-data-as-artifacts
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
type: tutorial
topics:
  - Workflows
ms.openlocfilehash: d23b62f1e77fd08fd798f4fb1af9f44e4d1b1123
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2022
ms.locfileid: '146179733'
---
{% data reusables.actions.enterprise-beta %} {% data reusables.actions.enterprise-github-hosted-runners %}

## 关于工作流程构件

构件允许您在作业完成后保留数据，并与同一工作流程中的另一个作业共享该数据。 构件是指在工作流程运行过程中产生的文件或文件集。 例如，在工作流程运行结束后，您可以使用构件保存您的构建和测试输出。 {% data reusables.actions.reusable-workflow-artifacts %}

{% data reusables.actions.artifact-log-retention-statement %} 每当有人向拉取请求推送新提交时，拉取请求的保留期都会重新开始计算。

以下是您可以上传的一些常见构件：

- 日志文件和核心转储文件
- 测试结果、失败和屏幕截图
- 二进制或压缩文件
- 压力测试性能输出和代码覆盖结果

{% ifversion fpt or ghec %}

存储构件时使用存储空间 {% data variables.product.product_name %}。 {% data reusables.actions.actions-billing %} 有关详细信息，请参阅“[{% data variables.product.prodname_actions %} 的计费](/billing/managing-billing-for-github-actions)”。

{% else %}

项目会占用外部 Blob 存储上的存储空间，该存储为 {% data variables.product.product_location %} 上的 {% data variables.product.prodname_actions %} 配置。

{% endif %}

构件会在工作流程运行过程中上传，您可以在 UI 中查看构件的名称和大小。 当构件使用 {% data variables.product.product_name %} UI 下载时， 作为构件一部分单独上传的所有文件都会压缩到一个 zip 文件中。 这意味着计费是根据上传的构件大小而不是 zip 文件的大小计算的。

{% data variables.product.product_name %} 提供两项可用于上传和下载构建构件的操作。 有关详细信息，请参阅 {% ifversion fpt or ghec %}[actions/upload-artifact](https://github.com/actions/upload-artifact) 和 [download-artifact](https://github.com/actions/download-artifact) 操作{% else %} {% data variables.product.product_location %} 上的 `actions/upload-artifact` 和 `download-artifact` 操作{% endif %}。

要在作业之间共享数据：

* **上传文件**：为上传的文件指定一个名称，并在作业结束前上传数据。
* **下载文件**：只能下载在同一工作流运行期间上传的工件。 下载文件时，您可以通过名称引用该文件。

作业步骤共享运行器机器的相同环境，但在其各自的进程中运行。 要在作业的步骤之间传递数据，您可以使用输入和输出。 有关输入和输出的详细信息，请参阅“[{% data variables.product.prodname_actions %} 的元数据语法](/articles/metadata-syntax-for-github-actions)”。

{% ifversion actions-caching %}

{% data reusables.actions.comparing-artifacts-caching %}

有关依赖项缓存的详细信息，请参阅“[缓存依赖项以加快工作流](/actions/using-workflows/caching-dependencies-to-speed-up-workflows#comparing-artifacts-and-dependency-caching)”。

{% endif %}

## 上传构建和测试构件

您可以创建持续集成 (CI) 工作流程来构建和测试您的代码。 有关使用 {% data variables.product.prodname_actions %} 执行 CI 的详细信息，请参阅“[关于持续集成](/articles/about-continuous-integration)”。

构建和测试代码的输出通常会生成可用于调试测试失败的文件和可部署的生产代码。 您可以配置一个工作流程来构建和测试推送到仓库中的代码，并报告成功或失败状态。 您可以上传构建和测试输出，以用于部署、调试失败的测试或崩溃以及查看测试套件范围。

可以使用 `upload-artifact` 操作上传工件。 上传构件时，您可以指定单个文件或目录，或多个文件或目录。 您还可以排除某些文件或目录，以及使用通配符模式。 建议为工件命名，如果没有命名，则会使用 `artifact` 作为默认名称。 有关语法的详细信息，请参阅 {% ifversion fpt or ghec %}[actions/upload-artifact](https://github.com/actions/upload-artifact) 操作{% else %} {% data variables.product.product_location %} 上的 `actions/upload-artifact` 操作{% endif %}。

### 示例

例如，您的仓库或 Web 应用程序可能包含必须转换为 CSS 和 JavaScript 的 SASS 和 TypeScript 文件。 假设生成配置输出 `dist` 目录中已编译的文件，如果所有测试均已成功完成，则可将 `dist` 目录中的文件部署到 Web 应用服务器。

```
|-- hello-world (repository)
|   └── dist
|   └── tests
|   └── src
|       └── sass/app.scss
|       └── app.ts
|   └── output
|       └── test
|   
```

此示例演示了如何创建 Node.js 项目的工作流，该项目在 `src` 目录中生成代码，在 `tests` 目录中运行测试。 可以假定运行 `npm test` 会生成一个名为 `code-coverage.html`、存储在 `output/test/` 目录中的代码覆盖率报告。

工作流上传 `dist` 目录中的生产工件，但不包括任何 Markdown 文件。 它还将 `code-coverage.html` 报表作为另一个工件上传。

```yaml{:copy}
name: Node CI

on: [push]

jobs:
  build_and_test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: {% data reusables.actions.action-checkout %}
      - name: npm install, build, and test
        run: |
          npm install
          npm run build --if-present
          npm test
      - name: Archive production artifacts
        uses: {% data reusables.actions.action-upload-artifact %}
        with:
          name: dist-without-markdown
          path: |
            dist
            !dist/**/*.md
      - name: Archive code coverage results
        uses: {% data reusables.actions.action-upload-artifact %}
        with:
          name: code-coverage-report
          path: output/test/code-coverage.html
```

## 配置自定义构件保留期

您可以为工作流程创建的单个构件自定义保留期。 使用工作流创建新工件时，可以同时使用 `retention-days` 和 `upload-artifact` 操作。 此示例演示如何为名为 `my-artifact` 的工件设置 5 天的自定义保留期：

```yaml{:copy}
  - name: 'Upload Artifact'
    uses: {% data reusables.actions.action-upload-artifact %}
    with:
      name: my-artifact
      path: my_file.txt
      retention-days: 5
```

`retention-days` 值不能超过存储库、组织或企业设置的保留限制。

## 下载或删除构件

在工作流运行期间，可以使用 [`download-artifact`](https://github.com/actions/download-artifact) 操作下载以前在同一工作流运行中上传的工件。

工作流程运行完成后，您可以在 {% data variables.product.prodname_dotcom %} 上或使用 REST API 下载或删除构件。 有关详细信息，请参阅“[下载工作流工件](/actions/managing-workflow-runs/downloading-workflow-artifacts)”、“[删除工作流工件](/actions/managing-workflow-runs/removing-workflow-artifacts)”和“[工件 REST API](/rest/reference/actions#artifacts)”。

### 在工作流程运行期间下载构件

[`actions/download-artifact`](https://github.com/actions/download-artifact) 操作可用于在工作流运行期间下载以前上传的工件。

{% note %}

注意：只能下载在同一工作流运行期间上传的工作流中的工件。

{% endnote %}

指定构件的名称以下载单个构件。 如果在未指定名称的情况下上传了工件，则默认名称为 `artifact`。

```yaml
- name: Download a single artifact
  uses: {% data reusables.actions.action-download-artifact %}
  with:
    name: my-artifact
```

您还可以不指定名称而下载工作流程运行中的所有构件。 如果您在处理大量构件，此功能非常有用。

```yaml
- name: Download all workflow run artifacts
  uses: {% data reusables.actions.action-download-artifact %}
```

如果下载所有工作流运行的工件，则会为每个工件使用其名称创建一个目录。

有关语法的详细信息，请参阅 {% ifversion fpt or ghec %}[actions/download-artifact](https://github.com/actions/download-artifact) 操作{% else %} {% data variables.product.product_location %} 上的 `actions/download-artifact` 操作{% endif %}。

## 在工作流中的作业间传递数据

可以使用 `upload-artifact` 和 `download-artifact` 操作在工作流中的作业间共享数据。 此示例工作流程说明如何在相同工作流程中的任务之间传递数据。 有关详细信息，请参阅 {% ifversion fpt or ghec %}[actions/upload-artifact](https://github.com/actions/upload-artifact) 和 [download-artifact](https://github.com/actions/download-artifact) 操作{% else %} {% data variables.product.product_location %} 上的 `actions/upload-artifact` 和 `download-artifact` 操作{% endif %}。

依赖于以前作业构件的作业必须等待依赖项成功完成。 此工作流使用 `needs` 密钥来确保 `job_1`、`job_2` 和 `job_3` 按顺序运行。 例如，`job_2` 需要 `job_1`，方法是使用 `needs: job_1` 语法。

作业1执行以下步骤：
- 执行数学计算并将结果保存到名为 `math-homework.txt` 的文本文件。
- 使用 `upload-artifact` 操作上传工件名称为 `homework` 的 `math-homework.txt` 文件。

作业 2 使用上一个作业的结果：
- 下载在上一作业中上传的 `homework` 工件。 默认情况下，`download-artifact` 操作会将工件下载到该步骤执行的工作区目录中。 可以使用 `path` 输入参数指定不同的下载目录。
- 读取 `math-homework.txt` 文件中的值，执行数学计算，并再次将结果保存到 `math-homework.txt`，覆盖其内容。
- 上传 `math-homework.txt` 文件。 此上传会覆盖之前上传的构件，因为它们共用同一名称。

作业 3 显示上一个作业中上传的结果：
- 下载 `homework` 工件。
- 将数学方程式的结果打印到日志中。

在此工作流示例中执行的完整数学运算是 `(3 + 7) x 9 = 90`。

```yaml{:copy}
name: Share data between jobs

on: [push]

jobs:
  job_1:
    name: Add 3 and 7
    runs-on: ubuntu-latest
    steps:
      - shell: bash
        run: |
          expr 3 + 7 > math-homework.txt
      - name: Upload math result for job 1
        uses: {% data reusables.actions.action-upload-artifact %}
        with:
          name: homework
          path: math-homework.txt

  job_2:
    name: Multiply by 9
    needs: job_1
    runs-on: windows-latest
    steps:
      - name: Download math result for job 1
        uses: {% data reusables.actions.action-download-artifact %}
        with:
          name: homework
      - shell: bash
        run: |
          value=`cat math-homework.txt`
          expr $value \* 9 > math-homework.txt
      - name: Upload math result for job 2
        uses: {% data reusables.actions.action-upload-artifact %}
        with:
          name: homework
          path: math-homework.txt

  job_3:
    name: Display results
    needs: job_2
    runs-on: macOS-latest
    steps:
      - name: Download math result for job 2
        uses: {% data reusables.actions.action-download-artifact %}
        with:
          name: homework
      - name: Print the final result
        shell: bash
        run: |
          value=`cat math-homework.txt`
          echo The result is $value
```

工作流程运行运行将会存档它生成的任何构件。 有关下载已存档工件的详细信息，请参阅“[下载工作流工件](/actions/managing-workflow-runs/downloading-workflow-artifacts)”。
![在作业间传递数据以执行数学运算的工作流](/assets/images/help/repository/passing-data-between-jobs-in-a-workflow-updated.png)

{% ifversion fpt or ghec %}

## 延伸阅读

- “[管理 {% data variables.product.prodname_actions %} 的计费](/billing/managing-billing-for-github-actions)”。

{% endif %}
