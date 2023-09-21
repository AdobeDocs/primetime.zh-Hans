---
description: 您可以使用Adobe Primetime广告决策界面在VOD和实时/线性内容中插入广告。
title: 广告要求
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 广告超时 {#ad-timeout}

## AV基础要求 {#av-foundation-requirements}

对于VOD内容，应在35秒内完成播放列表拼接，其中涉及主内容清单加载、广告解析和广告清单加载。

对于实时内容，每次更新播放列表时，播放列表拼接应在20秒内完成

**与AdResolution超时相关的API**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

可以通过在设置广告元数据时设置PTAdMetadata：：adResolutionTimeout来设置adResolutionTimeout。

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

此后，请遵循以下章节： [Primetime广告服务器元数据](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

**与AdManifest超时相关的API**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

可以通过在设置广告元数据时设置PTAdMetadata：：adManifestTimeout来设置adManifestTimeout。


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

此后，请遵循以下章节： [Primetime广告服务器元数据](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
