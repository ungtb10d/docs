---
title: GitHub Enterprise 服务级别协议
hidden: true
redirect_from:
  - /github-enterprise-cloud-addendum
  - /github-business-cloud-addendum
  - /articles/github-enterprise-cloud-addendum
  - /github/site-policy/github-enterprise-service-level-agreement
  - /github/site-policy-deprecated/github-enterprise-cloud-addendum
versions:
  fpt: '*'
---

这些条款适用于在 2021 年 1 月 4 日之前被许可使用产品的客户。在该日期之后购买 GitHub 产品的客户将定向到 https://www.github.com/enterprise-legal 以了解当前条款。

精简版：GitHub 保证适用 GitHub 服务的季度正常运行时间达到 99.9%（以下简称“服务级别”或“SLA”）  。 如果 GitHub 不符合 SLA，则客户将有权获得客户帐户的服务积分（以下简称“服务积分”）。

有关每个服务功能（以下简称“服务功能”）的定义以及历史和当前正常运行时间的信息，请访问 [GitHub 状态页面](https://www.githubstatus.com/)。 本 SLA 中使用但未定义的大写术语采用客户适用协议中赋予的含义。

## <a name="uptime-guarantee"></a>正常运行时间保证

“正常运行时间”是在给定的日历季度内，适用 GitHub 服务可用总分钟数的百分比。 GitHub 承诺至少保持适用 GitHub 服务 99.9% 的正常运行时间。 适用 GitHub 服务中可能包含的每个服务功能的正常运行时间计算如下所述（以下简称“正常运行时间计算”）。 如果 GitHub 不符合 SLA，客户将有权根据以下计算（以下简称“服务积分计算”）获得相应的服务积分。 请注意，停机时间不会同时或以同样的方式影响每个客户。

| **服务功能** | **正常运行时间计算** | **定义** | **服务积分计算** |
|---|---|---|---|
| **问题**、<br>**拉取请求**、<br>**Git 操作**、<br>**API 请求（仅适用于服务功能）** 、<br>**Webhook**、<br>**页** | （日历季度的总分钟数 - 停机时间）/日历季度的总分钟数 | “停机时间”是指发生以下任一情况的时间段：(a) 在给定分钟内任何服务功能的错误率超过百分之五 (5%)；或 (b) 经 GitHub 的内部和外部监控系统组合确定，服务不可用。 | 服务积分索赔可能基于以下计算方法中的一种（而非两种）： <ul><li>如果在一个日历季度内，服务功能的正常运行时间低于或等于 99.9% 但高于 99.0%，则结果为客户为该服务功能所支付金额的 10%。 <BR><BR>OR <BR><BR></li><li>如果在一个日历季度内，服务功能的正常运行时间低于 99.0%，则结果为客户为该服务功能所支付金额的 25%。</li></ul> | |
| **操作** | （总触发执行数 - 不可用执行数）/（总触发执行数）x 100 | “总触发执行数”是客户在一个日历季度内触发的所有操作的执行总数。 <br><br> “不可用执行数”是指在一个日历季度内，总触发执行数中未能运行的执行总数。  在触发器被成功触发五 (5) 分钟后，如果操作历史记录日志未捕获任何输出，则执行失败。 | 同上 |
| **包** | 传输正常运行时间 = 与操作相同 <br> <br> 存储正常运行时间 = 100% - 平均错误率* <br> <br> *正常运行时间计算不包括不计入总存储事务或失败存储事务的公共使用和存储事务（包括预身份验证失败；身份验证失败；存储帐户的尝试事务超过其指定配额）。 | “错误率”是指在设定的时间间隔（当前设置为一个小时）内失败的存储事务数除以总存储事务数。 如果在指定的一小时时间间隔内总存储事务数为零，则该时间间隔的错误率为 0%。 <br><br> “平均错误率”是日历季度内每个小时的错误率之和除以日历季度的总小时数。 | 同上 |

## <a name="exclusions"></a>排除项
正常运行时间计算不包括因以下原因导致的服务功能故障：(i) 客户的行为、疏忽或滥用适用 GitHub 服务，包括违反协议；(ii) 客户的网络连接故障；(iii) 超出 GitHub 合理控制范围的因素，包括不可抗力事件；或 (iv) 客户的设备、服务或其他技术。

## <a name="service-credits-redemption"></a>服务积分兑换
如果 GitHub 不符合此 SLA，则客户必须在该日历季度结束后的三十 (30) 天内向 GitHub 提出书面申请才能兑换服务积分。 服务积分兑换的书面申请和 GitHub Enterprise Cloud 自定义月度或季度报告应发送给 [GitHub 支持部门](https://support.github.com/contact?tags=docs-policy)。

服务积分可以采取退款或记入客户帐户的形式，不能兑换为现金，仅限于每个日历季度最多九十 (90) 天的付费服务，要求客户已支付任何未结发票，并在客户与 GitHub 的协议终止时到期。 服务积分是针对 GitHub 未能履行此 SLA 中任何义务的唯一和排他性补救措施。
