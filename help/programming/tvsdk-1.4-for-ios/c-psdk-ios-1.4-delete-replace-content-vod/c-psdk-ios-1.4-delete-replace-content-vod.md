---
description: TVSDK支持以编程方式删除和替换VOD流中的广告内容。
title: 删除和替换VOD流中的广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# 广告删除和替换API更改 {#ad-deletion-and-replacement-api-changes}

TVSDK支持以编程方式删除和替换VOD流中的广告内容。

删除和替换功能可进一步扩展自定义广告标记功能。 自定义广告标记将主内容的各个部分标记为与广告相关的内容时段。 除了标记这些时间范围之外，您还可以删除和替换时间范围。

TVSDK中的以下更改支持广告删除和替换。

**新API**

* `PTTimeRangeCollection` 是一个公共类，它定义了一组预定义的范围和类型：

   * `property PTTimeRangeCollectionType type` 指示时间范围的类型。
   * `property NSArray* ranges` 用于设置时间范围。

     数组中的预期对象类型为 `PTReplacementTimeRange` 或 `CMTimeRange`.

     >[!TIP]
     >
     >数组的所有对象都必须是同一类型。

   * `PTTimeRangeCollectionType` 是一个枚举，它定义在中定义的范围的行为。 `PTTimeRangeCollection`：

      * `PTTimeRangeCollectionTypeMarkRanges`：范围的类型为 *标记*. 范围用于将内容中的范围标记为广告。

      * `PTTimeRangeCollectionTypeDeleteRanges`：范围的类型为删除。 定义的范围将在广告插入之前从主内容中删除。
      * `PTTimeRangeCollectionTypeReplaceRanges`：范围的类型为替换。 定义的范围从主用Ads替换(Ad信令模式设置为 `PTAdSignalingModeCustomTimeRanges`)。

* `PTReplacementTimeRange`  — 新的公共类，定义 `PTTimeRangeCollection`：

   * `property CMTimeRange range`  — 定义范围的开始时间和持续时间。
   * `property long replacementDuration`  — 如果 `TimeRangeCollection` 是 `PTTimeRangeCollectionTypeReplaceRanges`， `replacementDuration` 用于创建投放机会（广告插入），其持续时间为 `replacementDuration`. 如果 `replacementDuration` 未设置，广告服务器将确定该投放机会的广告持续时间和数量。

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges`  — 添加了一种新类型的 `PTAdSignalingMode`. 此模式与 `PTTimeRangeCollection` 带有类型 `PTTimeRangeCollectionReplace` ，以用于基于替换范围的广告插入。

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection`  — 用于设置播放内容中标记/删除/替换范围所使用的时间范围。

* 警告日志：

   * `UNDEFINED_TIME_RANGES`

      * 类型 — 警告
      * 描述 — 广告信令模式被定义为自定义范围，但自定义范围未定义。

   * `INVALID_TIME_RANGES`

      * 类型 — 警告
      * 描述 — 一个或多个时间范围无效，将被忽略或修改。

**已弃用的API**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges`  — 此属性以前用于定义用于标记的C3范围。 现已弃用，因为这些范围是通过设置的 `PTTimeRangeCollection`.
