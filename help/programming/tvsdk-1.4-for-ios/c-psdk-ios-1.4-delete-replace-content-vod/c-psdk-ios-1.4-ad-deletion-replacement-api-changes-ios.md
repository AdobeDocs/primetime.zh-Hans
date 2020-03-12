---
description: TVSDK中的以下更改支持删除和替换。
seo-description: TVSDK中的以下更改支持删除和替换。
seo-title: 广告删除和替换API更改
title: 广告删除和替换API更改
uuid: 7cc50e7a-666f-4588-9c16-ad6d7d75cb65
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 广告删除和替换API更改{#ad-deletion-and-replacement-api-changes}

TVSDK中的以下更改支持删除和替换。

**新API**

* `PTTimeRangeCollection` 是一个公共类，它定义了预定义的一组范围和类型：

   * `property PTTimeRangeCollectionType type` 指示时间范围的类型。
   * `property NSArray* ranges` 用于设置时间范围。

      数组中期望的对象类型是 `PTReplacementTimeRange` 或 `CMTimeRange`。

      >[!TIP]
      >
      >数组中的所有对象都必须是同一类型。

   * `PTTimeRangeCollectionType` 是一个枚举，它定义了在以下位置定义的范围的行为 `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`:范围的类型是“标 *记”*。 这些范围用于将内容中的范围标记为“广告”。

      * `PTTimeRangeCollectionTypeDeleteRanges`:范围的类型为“删除”。 在广告插入之前，将从主内容中删除定义的范围。
      * `PTTimeRangeCollectionTypeReplaceRanges`:范围的类型为“替换”。 定义的范围从主范围替换为广告(广告信令模式设置为 `PTAdSignalingModeCustomTimeRanges`)。

* `PTReplacementTimeRange` -新的公共类，它定义了以下单个范围 `PTTimeRangeCollection`:

   * `property CMTimeRange range` -定义范围的开始和持续时间。
   * `property long replacementDuration` -如果类型为， `TimeRangeCollection` 则 `PTTimeRangeCollectionTypeReplaceRanges`使 `replacementDuration` 用它创建持续时间为的放置机会（广告插入） `replacementDuration`。 如果未 `replacementDuration` 设置，广告服务器将确定该投放机会的广告持续时间和数量。

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` -添加了新类型 `PTAdSignalingMode`。 此模式与基于替换范围的 `PTTimeRangeCollection` 广告插 `PTTimeRangeCollectionReplace` 入类型结合使用。

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` -用于设置在回放内容中的标记／删除／替换范围中使用的时间范围。

* 警告日志：

   * `UNDEFINED_TIME_RANGES`

      * 类型——警告
      * 描述——广告信令模式定义为自定义范围，但未定义自定义范围。
   * `INVALID_TIME_RANGES`

      * 类型——警告
      * 说明——一个或多个时间范围无效，将被忽略或修改。


**已弃用的API**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` -此属性以前用于定义C3范围进行标记。 现在已弃用它，因为这些范围是通过设置的 `PTTimeRangeCollection`。

