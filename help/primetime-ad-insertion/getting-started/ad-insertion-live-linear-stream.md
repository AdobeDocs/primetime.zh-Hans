---
title: 在实时/线性流中使用Ad Insertion
description: 在实时/线性流中使用Ad Insertion
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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

有关其他详细信息或其他支持的提示格式，请与Primetime支持代表联系。

## 部分广告时间支持 {#partial-ad-break-support}

部分广告插播可用于查看者在广告插播开始后进入实时/线性流的情况。  例如，如果查看者在1:00标记处输入2:00的广告时间，则插入部分广告时间可确保在其余时间提供广告。 如果没有插入部分广告时间，则不会在广告时间期间向此查看者提供任何广告。 如果媒体流中存在适当的标记，则PrimetimeAd Insertion默认情况下会启用部分广告时间插入。

## 提前返回（提前广告退出） {#early-return-early-ad-exit}

在某些情况下，可能有必要从实时/线性流中的广告时间提前返回，例如，当体育活动突然恢复活动时。 每个广告决策格式都包含一个“cue-out”（广告）或“cue-in”（内容）标记。  如果在广告时间结束之前遇到“提示加入”标记，Adobe PrimetimeAd Insertion将遵循该提示加入。  请联系您的内容包管理器以启用提前返回。
