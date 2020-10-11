---
title: 在实时／线性流中使用Ad Insertion
description: 在实时／线性流中使用Ad Insertion
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 在实时／线性流中使用Ad Insertion {#ad-insertion-live-linear-stream}

PrimetimeAd Insertion使出版商能够处理实时／线性流中出现的标准和复杂的广告插入情况。

## 支持的Cue格式 {#cue-formats-supported}

PrimetimeAd Insertion支持各种标准和非标准提示格式，包括：

* DPI SCTE-35（SCTE-35增强的广告标记）

* [Adobe数字项目插入信令规范](https://www.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* 二进制SCTE-35

有关更多详细信息或其他支持的提示格式，请与Primetime支持代表联系。

## 部分广告中断支持 {#partial-ad-break-support}

在广告中断开始后，查看器进入实时／线性流时，可使用部分广告中断。  例如，如果观众在1:00处输入2:00长的广告中断，则部分广告中断插入可确保广告在剩余时间内投放。 如果不插入部分广告中断，则在中断期间不会向此查看者投放任何广告。 如果媒体流中存在相应的标记，PrimetimeAd Insertion将默认启用部分广告中断插入。

## 提前退货（提前广告退出） {#early-return-early-ad-exit}

在某些情况下，可能需要从实时／线性流中的广告中断中提前返回，例如当体育事件突然恢复行动时。 每种广告决策格式都包含一个“提示”（广告）或“提示”（内容）的标签。 如果在广告结束前遇到“提示”标签，Adobe PrimetimeAd Insertion将遵守提示。 请与内容包装程序联系以启用提前返回。
