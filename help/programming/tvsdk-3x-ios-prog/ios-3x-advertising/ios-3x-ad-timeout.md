---
description: 您可以使用Adobe Primetime广告决策界面在VOD和实时／线性内容中插入广告。
seo-description: 您可以使用Adobe Primetime广告决策界面在VOD和实时／线性内容中插入广告。
seo-title: 广告要求
title: 广告要求
uuid: 0287f1e4-746f-42e5-b811-409064dd9b13
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 广告超时 {#ad-timeout}

## AV基础要求 {#av-foundation-requirements}

对于VOD内容，播放列表拼接（包括主内容清单加载、广告分辨率和广告清单加载）应在35秒内完成。

如果是“Live”内容，则每次更新播放列表时，播放列表拼接应在20秒内完成

**与AdResolution超时相关的API**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

在设置广告元数据时，可以通过设置PTAdMetadata::adResolutionTimeout来设置adResolutionTimeout。

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

之后，请按照以下部分操作：Primetime广告 [服务器元数据](../..//tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md)。

**与AdManifest超时相关的API**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

在设置广告元数据时，可以通过设置PTAdMetadata::adManifestTimeout来设置adManifestTimeout。


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

之后，请按照以下部分操作：Primetime广告 [服务器元数据](../..//tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md)。
