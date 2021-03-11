---
description: TVSDK支持在VOD流中以编程方式删除和替换广告内容。
title: 删除和替换VOD流中的广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# 广告删除和替换API更改{#ad-deletion-and-replacement-api-changes}

TVSDK支持在VOD流中以编程方式删除和替换广告内容。

删除和替换功能扩展了自定义广告标记功能。 自定义广告标记将主要内容的部分标记为与广告相关的内容句点。 除了标记这些时间范围之外，您还可以删除和替换时间范围。

TVSDK中的以下更改支持删除和替换。

**新API**

* `PTTimeRangeCollection` 是定义预定义范围集和类型的公共类：

   * `property PTTimeRangeCollectionType type` 指示时间范围的类型。
   * `property NSArray* ranges` 用于设置时间范围。

      数组中预期的对象类型是`PTReplacementTimeRange`或`CMTimeRange`。

      >[!TIP]
      >
      >数组中的所有对象都必须是同一类型。

   * `PTTimeRangeCollectionType` 是一个枚举，用于定义在以下位置中定义的范围的行为 `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`:范围的类型是“标 *记”*。这些范围用于将内容中的范围标记为“广告”。

      * `PTTimeRangeCollectionTypeDeleteRanges`:范围的类型为“删除”。在广告插入之前，将从主内容中删除定义的范围。
      * `PTTimeRangeCollectionTypeReplaceRanges`:范围的类型为“替换”。定义的范围从主范围替换为Ads（Ad信令模式设置为`PTAdSignalingModeCustomTimeRanges`）。

* `PTReplacementTimeRange`  — 定义以下单个范围的新公共类 `PTTimeRangeCollection`:

   * `property CMTimeRange range`  — 定义范围的开始和持续时间。
   * `property long replacementDuration`  — 如果类型 `TimeRangeCollection` 为 `PTTimeRangeCollectionTypeReplaceRanges`, `replacementDuration` 则用于创建持续时间为的放置机会（广告插入） `replacementDuration`。如果未设置`replacementDuration`，广告服务器将确定该投放机会的广告持续时间和数量。

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges`  — 添加了新类型 `PTAdSignalingMode`。此模式与类型为`PTTimeRangeCollectionReplace`的`PTTimeRangeCollection`一起使用，以根据替换范围进行广告插入。

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection`  — 用于设置在播放内容中的标记/删除/替换范围中使用的时间范围。

* 警告日志：

   * `UNDEFINED_TIME_RANGES`

      * 类型 — 警告
      * 描述 — 广告信令模式定义为自定义范围，但未定义自定义范围。
   * `INVALID_TIME_RANGES`

      * 类型 — 警告
      * 描述 — 一个或多个时间范围无效，将被忽略或修改。


**已弃用的API**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges`  — 此属性以前用于定义C3范围进行标记。现在已弃用，因为这些范围是通过`PTTimeRangeCollection`设置的。