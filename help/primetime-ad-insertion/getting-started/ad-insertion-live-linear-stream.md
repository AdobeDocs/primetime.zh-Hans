---
title: 在实时/线性流中使用Ad Insertion
description: 在实时/线性流中使用Ad Insertion
exl-id: d56ed723-ec72-4bbd-befc-6858c7c9d800
source-git-commit: 1bc2f6c230c262babf2958c32fee31afcad04c2f
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 在实时/线性流中使用Ad Insertion {#ad-insertion-live-linear-stream}

PrimetimeAd Insertion使发布者能够处理在实时/线性流期间发生的标准和复杂的广告插入情况。

## 支持的提示格式 {#cue-formats-supported}

PrimetimeAd Insertion支持各种标准和非标准提示格式，包括：

* DPI SCTE-35（SCTE-35增强型广告标记）

* [Adobe数字节目插入信令规范](assets/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* 二进制SCTE-35（HLS和DASH）

* 文本SCTE-35（HLS和DASH）

有关其他详细信息或其他支持的提示格式，请联系您的Primetime支持代表。

## 部分广告时间支持 {#partial-ad-break-support}

部分广告时间可用于查看者在广告时间开始后进入实时/线性流的情况。  例如，如果观看者在1:00标记处输入2:00的广告时间，则插入部分广告时间可确保广告在剩余时间内提供。 如果没有插入部分广告时间，则不会在广告时间期间向此查看者提供任何广告。 如果媒体流中存在适当的标记，则默认情况下PrimetimeAd Insertion会启用部分广告时间插入。

## 提前返回（提前广告退出） {#early-return-early-ad-exit}

在某些情况下，可能有必要从实时/线性流中的广告时间提前返回，例如，当体育赛事突然恢复活动时。 每个广告决策格式都包含一个标记，用于“提示输出”（广告）或“提示输入”（内容）。  如果在广告时间结束之前遇到“提示加入”标记，Adobe PrimetimeAd Insertion将遵循该提示加入。  请联系您的内容包管理器以提早返回。
