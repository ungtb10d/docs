---
ms.openlocfilehash: 216386e3e7dc31df99a383af6a335681c72911c2
ms.sourcegitcommit: 478f2931167988096ae6478a257f492ecaa11794
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2022
ms.locfileid: "147764046"
---
1. **[新しいランナー]** をクリックしたら、 **[{% octicon "mark-github" aria-label="New hosted runner" %} 新しい Github ホステッド ランナー]** をクリックします。
1. 必要な詳細を入力して、新しいランナーを構成します。

    - **名前**: 新しいランナーの名前を入力します。 識別しやすくするには、ハードウェアとオペレーティング システム (`ubuntu-20.04-16core` など) を示しておくのがよいでしょう。
    - **ランナー イメージ**: 使用可能なオプションからオペレーティング システムを選びます。 オペレーティング システムを選ぶと、特定のバージョンを選ぶことができるようになります。
    - **ランナーのサイズ**: 使用可能なオプションのドロップダウン リストからハードウェア構成を選びます。
    - **自動スケーリング**: いつでもアクティブにすることができるランナーの最大数を選びます。
    - **ランナー グループ**: ランナーがメンバーとなるグループを選びます。 需要に合わせてスケールアップまたはスケールダウンしながら、このグループによって、ランナーのインスタンスが複数ホストされます。
    - **ネットワーク**: {% data variables.product.prodname_ghe_cloud %} の場合のみ、静的 IP アドレス範囲を {% data variables.actions.hosted_runner %} のインスタンスに割り当てるかどうかを選びます。 合計で最大 10 個の静的 IP アドレスを使うことができます。

1. **[ランナーの作成]** をクリックします。