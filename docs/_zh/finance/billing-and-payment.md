---
title: 账单和支付
tag: [finance, billing]
description: 了解和风天气开发服务的账单和支付系统是如何工作的。
ref: finance-billing
---

和风天气开发服务基于按量计费模式的计费系统，是更加透明、简单和有竞争力的定价方案，而账单则是按量计费的费用凭证和计费系统的核心。本文档将介绍我们的账单和计费系统是如何工作的。

## 计费和账单 {#billing}

和风天气开发服务的[标准订阅](/docs/finance/subscription/)采用按量计费的后付费模式，即按照你的每一次请求记录费用，你不需要提前预付大量资金，也不需要为用不到的服务买单，你只需要为你实际使用的部分付费即可。另外，按量计费的定价是阶梯价格，意味着你使用的越多，单次请求的价格越低。

你的所有请求量和应付费用都将记录在账单中，我们将根据账单向你收取费用。以下是关于计费和账单的重要规则：

- 按量计费的计价单位是一次请求。
- 按量计费的账单周期是一个自然月，在每个月的5日前生成。同时在每个小时都会生 成应计费用账单，代表上一个小时你的请求量和应付费用，一个自然月内所有小时的应计费用账单合计即为当月按量计费账单。
- 当你使用自动支付模式时，我们会根据每个小时的应计费用账单向你扣减费用。参考本篇文档[支付账单](#payment)章节。
- 按量计费的阶梯价格累进周期是一个自然月，即在每个月的最开始，都将按照阶梯价格的第一档开始计算。

> **注意：**账单由系统自动生成，无需签字或盖章，是你和我们之间的具有法律效力的凭证，你应根据账单金额向我们支付或根据账单向你的组织申请支付费用，我们不再额外提供其他形式的合同。
{:.bqwarning}

关于按量计费的定价请参考[按量计费定价](/docs/finance/pricing/)。

### 举例说明

下方是关于计费和账单的示例：

***按量计费***

你在8月10日请求了2000次城市实时天气，在8月20日请求了1000次每日天气预报（15天），之后停止使用，那么你只需要支付2000次请求 x 0.001元 + 1000次请求 x 0.002元 = 4元，并且之后不再需要支付任何费用。

***应计费用账单***

你在8月10日13:00-13:59获取了10000次城市实时天气，那么在14:00之后将生成一份应计费用账单，该账单记录了你上一个小时的10000次请求，计算出的应付金额为10元（10000次请求 x 0.001元，忽略阶梯价格因素）。在这份应计费用账单生成后，会自动扣减你的可用额度或节省计划金额。

***阶梯价格***

你在8月份总计获取了100万次城市实时天气，阶梯价格的计算公式为：

```
300000次请求量 x 0.001元 + 700000次请求量 x 0.0009元 = 930元
```

在9月再次获取了100万次城市实时天气，计算公式与上个月相同。

### 如何降低成本？

按量计费可以根据你的需求灵活的增加或减少请求量，避免提前预付大量金额。当你的请求量较多或需求较稳定的时候，你可以使用节省计费，大幅降低你的成本。参考[节省计划](/docs/finance/saving-plans/)。

对于有大量请求量的用户（通常指的是日均10万次请求以上），请与我们的商务专家联系，以便提供更佳的解决方案。

### 当停止使用时，是否继续收费？

按量计费的其中一个优势就是你可以随时开始或随时停止，在你停止使用后，你不会再收到任何账单，也无需支付费用。

> **注意：**当你停止使用时，请确保你的程序已经移除了KEY或已经完全停止向我们发送请求，否则你依然需要继续支付费用。
{:.bqdanger}

## 支付账单 {#payment}

在账单生成后，我们会自动尝试从你的账户可用额度中扣除费用。除了自动支付外，我们还支持定期支付和手动付款。

### 自动支付 {#automatic-payment}

标准订阅的账单默认采用自动支付的方式。自动支付将根据每个小时的应计费用扣减你的可用额度，因此你需要随时关注你的可用额度，当可用额度<0时，你的服务可能会暂停。

如购买了节省计划，自动支付将优先通过节省计划支付费用。参考[节省计划](/docs/finance/saving-plans/)。

### 定期支付 {#recurring-payment}

对于企业开发者，标准订阅可以使用定期付款。定期支付将根据企业开发者的需求设定每个月的支付日期。与自动支付不同，在你设定的每月支付日期之前，应计费用不会通过可用额度进行扣款，在支付日期当天，我们才会尝试扣款。因此，定期支付的用户需要在支付日期前确保可用额度足够支付账单金额。

> **提示：** 开通定期支付需要与你的商务经理联系或发送工单申请。

如购买了节省计划，定期支付将在账单生成后自动通过节省计划支付费用。参考[节省计划](/docs/finance/saving-plans/)。

### 手动支付

你可以进行一次性手动付款，这将增加你的可用额度，用于支付待付款/欠款账单或其他预付费服务。请参考[添加可用额度](#add-balance)。

### 支付场景 {#payment-scenarios}

以下是一些你可能遇到的支付场景。对于这些场景，我们假设的前提条件是：

- 你每个小时请求1000次实时天气
- 每个月为30天（720个小时）
- 你的初始可用额度为100元
- 当使用[节省计划](/docs/finance/saving-plans/)时，你的节省计划规格为：1年期并承诺金额为500元
- 每个月账单的生成日期为1日
- 定期支付的支付日期为每个月10日

***使用自动支付***

每个小时，应计费用账单将记录你消费的1元（0.001元 x 1000次请求）并通过你的可用额度进行支付。在第100个小时之后，你的可用额度将被全部扣减，此时你应该及时进行充值操作，否则在第101个小时之后，你的可用额度将为-1元，这将导致你的服务被中止，并且进入[欠款状态](#outstanding)。

***使用自动支付和节省计划***

每个小时，应计费用账单将记录你消费的0.6元（0.001元 x 0.6节省系数 x 1000次请求）并通过你的节省计划进行支付。在你消耗完节省计划的承诺金额后，每个小时的应计费用账单将改为从你的可用额度中进行支付。

***使用定期支付***

每个小时，应计费用账单将记录你消费的1元（0.001元 x 1000次请求），在下个月1日将生成应付总金额为678元（0.001元 x 300000次请求 + 0.0009元 x 420000次请求）的账单，此时你的可用额度为-578元（100元可用额度 - 678元账单金额）。你可以在10日23:59:59前随时支付578元，否则在11日起， 你的服务被中止，并进入欠款状态。

***使用定期支付和节省计划***

每个小时，应计费用账单将记录你消费的0.6元（0.001元 x 0.6节省系数 x 1000次请求），在下个月1日将生成应付总金额为406.8元（0.001元 x 0.6节省系数 x 300000次请求 + 0.0009元 x 0.6节省系数 x 420000次请求）的账单，账单将自动通过节省计划中的承诺金额进行支付，你无需再进行支付。此时你的可用额度为100元，剩余的承诺金额为93.2元（500元节省计划 - 406.8元账单金额）。

在第二个月，账单金额为614.86元（0.001元 x 0.6节省系数 x 155334次请求 + 0.001元 x 144666次请求 + 0.0009元 x 420000次请求），其中节省计划中的93.2元以及可用额度中的100元将在账单生成后扣减，此时你的可用额度为-421.66元（93.2元节省计划 + 100元可用额度 - 614.86元账单金额）。你可以在10日23:59:59前随时支付421.66元，否则在11日起， 你的服务被中止，并进入欠款状态。

### 支付方式 {#payment-methods}

我们提供多种支付方式。

- **支付宝：**对于中国地区的用户，我们推荐使用支付宝进行支付。支持支付宝中绑定的信用卡、储蓄卡、余额以及花呗。
- **银行转帐：**对于中国地区的企业开发者，我们支持使用银行转账进行支付。请注意，银行转账需要24-72小时的审核时间或以银行到账为准（如遇节假日可能会延后），无法做到实时支付。
- **信用卡：**如果希望使用信用卡支付，请使用上述支付宝中绑定的信用卡进行支付。

### 欠款 {#outstanding}

如果账单未能在付款日完成支付，则进入欠款状态。此时你需要尽快完成欠款账单的支付。

> **警告：** 在“欠款”状态下，和风天气开发服务将被暂停，如“欠款”状态持续30天，你的帐号将被冻结。
{:.bqdanger}

### 退款

标准订阅和高级订阅采用后付费模式，因此你无法对已经使用的服务申请退款。

对于充值到可用额度的费用，请参考[提取可用额度](#withdraw-balance)。

对于其他一次性预付费购买的服务，在符合下列条件时，我们支持无理由退款：

- 还未开始使用
- 没有开具增值税发票
- 购买不超过60天

退款需要支付**5%手续费**，退款金额将退回到原支付渠道。如需要退款，请提交工单。

## 可用额度 {#balance}

可用额度是你帐号中可以使用的金额，用于支付账单费用。

> **注意：** 首次使用标准订阅，可用额度必须大于等于10元。
{:.bqwarning}

对于自动付款的用户，你必须确保可用额度大于或等于0，否则你的服务将被中止。

对于定期付款的用户，你必须在约定的支付日期当天确保可用额度大于或等于0，否则你的服务将被中止。

### 增加可用额度 {#add-balance}

你可以使用[多种支付方式](#payment-methods)增加可用额度。

每次增加可用额度的最小金额为0.01。当你存在待支付/欠款账单时，增加可用额度的最小金额为待支付/欠款金额。

> **例如：**当你有一个待支付账单，金额为123元，你选择增加200元的可用额度，此时将有123元用于支付账单，此时你的可用额度为200元 - 123元 = 77元。

### 提取可用额度 {#withdraw-balance}

你可以随时将可用额度提取出来，但是需要符合下列条件：

- 可用额度大于1元
- 帐号内没有标准订阅或高级订阅的项目
- 没有欠款或待支付帐单
- 帐号未处于冻结状态

提取可用额度需要支付**5%手续费**，提取的金额将退回到原支付渠道。如需要提取可用额度，请提交工单。

## 增值税

对于中国大陆地区用户的购买，账单金额已经包含了增值税。如需要获取增值税发票，参考[增值税发票](/docs/finance/vat-invoice/)。

对于其他国家或地区用户的购买，账单金额不包含所需要征收的任何税种。

## 暂停和冻结

当帐单状态为欠款的时候，你的和风天气服务将被暂停，你需要尽快增加可用额度用于支付欠款帐单。当欠款帐单的状态持续30天后，你的帐号将被冻结并且你仍然需要支付欠款账单，请参考[帐号冻结](/docs/account/suspension/)。