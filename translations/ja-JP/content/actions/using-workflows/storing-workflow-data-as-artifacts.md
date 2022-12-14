---
title: ワークフロー データを成果物として保存する
shortTitle: Storing workflow artifacts
intro: 成果物を使うと、ワークフロー内のジョブ間でデータを共有し、ワークフローが完了したときに、そのワークフローのデータを保存できます。
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
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '146179736'
---
{% data reusables.actions.enterprise-beta %} {% data reusables.actions.enterprise-github-hosted-runners %}

## ワークフローの成果物について

成果物を使えば、ジョブの完了後にデータを永続化でき、そのデータを同じワークフロー中の他のジョブと共有できます。 成果物とは、ワークフロー実行中に生成されるファイル、またはファイルのコレクションです。 たとえば、ワークフローの実行が終了した後、成果物を使ってビルドとテストの出力を保存しておけます。 {% data reusables.actions.reusable-workflow-artifacts %}

{% data reusables.actions.artifact-log-retention-statement %} pull request の保持期間は、ユーザーが新しいコミットを pull request にプッシュするたびに再開されます。

以下は、アップロードできる一般的な成果物の一部です。

- ログファイルとコアダンプ
- テスト結果、エラー、スクリーンショット
- バイナリあるいは圧縮されたファイル
- ストレステストのパフォーマンス出力およびコードカバレッジの結果

{% ifversion fpt or ghec %}

成果物の保存には、{% data variables.product.product_name %}上のストレージ領域が使われます。 {% data reusables.actions.actions-billing %} 詳細については、「[{% data variables.product.prodname_actions %} の支払いを管理する](/billing/managing-billing-for-github-actions)」を参照してください。

{% else %}

成果物は、{% data variables.product.product_location %} 上の {% data variables.product.prodname_actions %} 向けに設定された外部 blob ストレージ上のストレージスペースを消費します。

{% endif %}

成果物はワークフローの実行中にアップロードされ、成果物の名前とサイズはUIで見ることができます。 {% data variables.product.product_name %}のUIを使って成果物がダウンロードされる場合、成果物の一部として個別にアップロードされたすべてのファイルはzipして1つのファイルにまとめられます。 これはすなわち、支払いはこのzipファイルのサイズではなく、アップロードされた成果物のサイズを元に計算されるということです。

{% data variables.product.product_name %}には、ビルドの成果物のアップロードとダウンロードに使用できるアクションが2つあります。 詳細については、{% ifversion fpt or ghec %}[actions/upload-artifact](https://github.com/actions/upload-artifact) と [download-artifact](https://github.com/actions/download-artifact) のアクション{% else %}{% data variables.product.product_location %}に対する `actions/upload-artifact` と `download-artifact` のアクション{% endif %}を参照してください。

ジョブ間でデータを共有するには:

* **ファイルのアップロード**: アップロードされたファイルに名前を付けて、ジョブが終了する前にデータをアップロードします。
* **ファイルのダウンロード**: アップロードされたアーティファクトをダウンロードできるのは、同じワークフローの実行中だけです。 ファイルをダウンロードする際には、名前で参照できます。

ジョブのステップは、ランナーマシン上で同じ環境を共有しますが、それぞれが個別のプロセス内で実行されます。 ジョブのステップ間のデータを受け渡すには、入力と出力を使用できます。 入力と出力の詳細については、「[{% data variables.product.prodname_actions %} のメタデータ構文](/articles/metadata-syntax-for-github-actions)」を参照してください。

{% ifversion actions-caching %}

{% data reusables.actions.comparing-artifacts-caching %}

依存関係のキャッシュの詳細については、「[依存関係をキャッシュしてワークフローのスピードを上げる](/actions/using-workflows/caching-dependencies-to-speed-up-workflows#comparing-artifacts-and-dependency-caching)」を参照してください。

{% endif %}

## ビルドおよびテストの成果物をアップロードする

継続的インテグレーション（CI）ワークフローを作成して、コードのビルドやテストを行えます。 {% data variables.product.prodname_actions %} を使用して CI を実行する方法の詳細については、「[継続的インテグレーションについて](/articles/about-continuous-integration)」を参照してください。

コードのビルドおよびテストからの出力によって、多くの場合、エラーのデバッグに使用できるファイルと、デプロイできる本番コードが生成されます。 リポジトリにプッシュされるコードをビルドしてテストし、成功または失敗のステータスをレポートするワークフローを構成することができます。 デプロイメントに使用するビルドおよびテスト出力をアップロードし、失敗したテストまたはクラッシュをデバッグしてテストスイートのカバレッジを確認できます。

成果物をアップロードするには、`upload-artifact` アクションを使用できます。 成果物をアップロードする場合は、単一のファイルまたはディレクトリ、あるいは複数のファイルまたはディレクトリを指定できます。 また、特定のファイルやディレクトリを除外したり、ワイルドカードパターンを使用したりすることもできます。 成果物の名前を指定することをお勧めしますが、名前を指定しない場合は、`artifact` が既定の名前として使用されます。 構文の詳細については、{% ifversion fpt or ghec %}[actions/upload-artifact](https://github.com/actions/upload-artifact) アクション{% else %}{% data variables.product.product_location %}に対する `actions/upload-artifact` アクション{% endif %}を参照してください。

### 例

たとえば、リポジトリあるいはWebアプリケーションにはCSSやJavaScriptに変換しなければならないSASSやTypeScriptが含まれているかもしれません。 ビルド構成で `dist` ディレクトリにコンパイル後のファイルを出力すると仮定すると、テストがすべて正常に完了した場合、`dist` ディレクトリにあるファイルが Web アプリケーション サーバーにデプロイされます。

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

この例で示しているのは、`src` ディレクトリにコードをビルドして、`tests` ディクトリでテストを実行する Node.js プロジェクトのワークフローを作成する方法です。 実行中の `npm test` によって、`code-coverage.html` という名前で、`output/test/` ディレクトリに保存されるコード カバレッジ レポートが生成されると想定できます。

このワークフローでは、`dist` ディレクトリに運用環境の成果物をアップロードしますが、Markdown ファイルはその対象外です。 また、`code-coverage.html` レポートも別の成果物としてアップロードされます。

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

## カスタムの成果物の保持期間を設定する

ワークフローによって作成された個々の成果物のカスタム保存期間を定義できます。 ワークフローを使用して新しい成果物を作成する場合、`upload-artifact` アクションで `retention-days` を使用できます。 この例は、`my-artifact` という名前の成果物に 5 日間のカスタム保存期間を設定する方法を示しています。

```yaml{:copy}
  - name: 'Upload Artifact'
    uses: {% data reusables.actions.action-upload-artifact %}
    with:
      name: my-artifact
      path: my_file.txt
      retention-days: 5
```

`retention-days` の値は、リポジトリ、Organization、または Enterprise によって設定された保持制限を超えることはできません。

## 成果物のダウンロードあるいは削除

ワークフローの実行中に、[`download-artifact`](https://github.com/actions/download-artifact) アクションを使用すると、同じワークフロー実行で以前にアップロードされた成果物をダウンロードできます。

ワークフローの実行が完了したら、{% data variables.product.prodname_dotcom %} または REST API を使用して成果物をダウンロードまたは削除できます。 詳細については、「[ワークフローの成果物をダウンロードする](/actions/managing-workflow-runs/downloading-workflow-artifacts)」、「[ワークフローの成果物を削除する](/actions/managing-workflow-runs/removing-workflow-artifacts)」、および[Artifacts REST API](/rest/reference/actions#artifacts) に関するページを参照してください。

### ワークフロー実行中の成果物のダウンロード

[`actions/download-artifact`](https://github.com/actions/download-artifact) アクションを使用して、ワークフロー実行中に以前にアップロードされた成果物をダウンロードできます。

{% note %}

**注:** ダウンロードできるのは、同じワークフロー実行中にアップロードされたワークフロー内の成果物のみです。

{% endnote %}

個々の成果物をダウンロードするには、成果物の名前を指定します。 名前を指定せずに成果物をアップロードした場合、既定の名前は `artifact` です。

```yaml
- name: Download a single artifact
  uses: {% data reusables.actions.action-download-artifact %}
  with:
    name: my-artifact
```

また、名前を指定しないことで、ワークフロー実行のすべての成果物をダウンロードすることもできます。 これは、多数の成果物を扱っている場合に便利です。

```yaml
- name: Download all workflow run artifacts
  uses: {% data reusables.actions.action-download-artifact %}
```

ワークフロー実行のすべての成果物をダウンロードすると、各成果物のディレクトリがその名前を使用して作成されます。

構文の詳細については、{% ifversion fpt or ghec %}[actions/download-artifact](https://github.com/actions/download-artifact) アクション{% else %}{% data variables.product.product_location %}に対する `actions/download-artifact` アクション{% endif %}を参照してください。

## ワークフロー内のジョブ間でのデータの受け渡し

`upload-artifact` アクションと `download-artifact` アクションを使用すると、ワークフローのジョブ間でデータを共有できます。 以下のワークフローの例では、同じワークフローのジョブ間でデータを受け渡す方法を説明しています。 詳細については、{% ifversion fpt or ghec %}[actions/upload-artifact](https://github.com/actions/upload-artifact) と [download-artifact](https://github.com/actions/download-artifact) のアクション{% else %}{% data variables.product.product_location %}に対する `actions/upload-artifact` と `download-artifact` のアクション{% endif %}を参照してください。

前のジョブの成果物に依存するジョブは、前のジョブが正常に完了するまで待つ必要があります。 このワークフローでは、`needs` キーワードを使用して、`job_1`、`job_2`、`job_3` を順次実行できます。 たとえば、`job_2` では `needs: job_1` 構文を使用することにより `job_1` が必要となっています。

ジョブ1は、以下のステップを実行します。
- 数式の計算を実行し、その結果を `math-homework.txt` というテキスト ファイルに保存します。
- `upload-artifact` アクションを使用して、`math-homework.txt` ファイルを `homework` という成果物名でアップロードします。

ジョブ2は、前のジョブの結果を利用して、次の処理を実行します。
- 前のジョブでアップロードされた `homework` 成果物をダウンロードします。 既定では、`download-artifact` アクションで、ステップが実行されているワークスペース ディレクトリに成果物をダウンロードします。 `path` 入力パラメータを使用すると、別のダウンロード ディレクトリを指定できます。
- `math-homework.txt` ファイル内の値を読み取り、数式の計算を実行して、結果を `math-homework.txt` に再度保存し、その内容を上書きします。
- `math-homework.txt` ファイルをアップロードします。 このアップロードでは、同じ名前を共有しているため、以前にアップロードされた成果物を上書きします。

ジョブ3は、前のジョブでアップロードされた結果を表示して、次の処理を実行します。
- `homework` 成果物をダウンロードします。
- 数式の結果をログに出力します。

このワークフロー例で実行される完全な数式は、`(3 + 7) x 9 = 90` です。

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

ワークフローの実行により、生成された成果物がアーカイブされます。 アーカイブされた成果物のダウンロードの詳細については、「[ワークフローの成果物をダウンロードする](/actions/managing-workflow-runs/downloading-workflow-artifacts)」を参照してください。
![ジョブ間でデータを受け渡して計算を実行するワークフロー](/assets/images/help/repository/passing-data-between-jobs-in-a-workflow-updated.png)

{% ifversion fpt or ghec %}

## 参考資料

- 「[{% data variables.product.prodname_actions %} の支払いを管理する](/billing/managing-billing-for-github-actions)」

{% endif %}
