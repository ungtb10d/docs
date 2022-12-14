---
ms.openlocfilehash: 446bc8429d81d54d38eeaf2852a61d25db17da68
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: "145186073"
---
Você pode usar `jobs.<job_id>.outputs` para criar um `map` das saídas para um trabalho. As saídas de trabalho estão disponíveis para todos os trabalhos downstream que dependem deste trabalho. Para obter mais informações sobre como definir dependências de trabalho, confira [`jobs.<job_id>.needs`](/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idneeds).

{% data reusables.actions.output-limitations %}

As saídas de trabalho que contêm expressões são avaliadas no executor ao final de cada trabalho. As saídas que contêm segredos são eliminadas no executor e não são enviadas para {% data variables.product.prodname_actions %}.

Para usar saídas de trabalho em um trabalho dependente, você pode usar o contexto `needs`. Para obter mais informações, confira "[Contextos](/actions/learn-github-actions/contexts#needs-context)".

### Exemplo: Definindo saídas para um trabalho

{% raw %}
```yaml
jobs:
  job1:
    runs-on: ubuntu-latest
    # Map a step output to a job output
    outputs:
      output1: ${{ steps.step1.outputs.test }}
      output2: ${{ steps.step2.outputs.test }}
    steps:
      - id: step1
        run: echo "::set-output name=test::hello"
      - id: step2
        run: echo "::set-output name=test::world"
  job2:
    runs-on: ubuntu-latest
    needs: job1
    steps:
      - run: echo ${{needs.job1.outputs.output1}} ${{needs.job1.outputs.output2}}
```
{% endraw %}
