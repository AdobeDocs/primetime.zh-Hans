---
description: 您可以使用不同的广告信号模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 不同的信令模式和元数据组合会导致不同的行为。
seo-description: 您可以使用不同的广告信号模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 不同的信令模式和元数据组合会导致不同的行为。
seo-title: 广告信号模式和广告元数据组合对广告插入和删除的影响
title: 广告信号模式和广告元数据组合对广告插入和删除的影响
uuid: 49abab49-4e52-477d-b7ed-688ee63e7473
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# 广告信号模式和广告元数据组合对广告插入和删除的影响{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

您可以使用不同的广告信号模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 不同的信令模式和元数据组合会导致不同的行为。

>[!TIP]
>
>当时间范围与广告信令模式之间存在冲突时，TVSDK会优先选择时间范围。

下表提供了有关信令模式和元数据组合行为的详细信息：

**服务器映射**

| **广告元数据** | **已创建解析器** | **`PlacementInformations`已创建** | **结果行为** |
|--- |--- |--- |--- |
|  | 删除 | 删除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已删除范围 |
| 删除，Auditude | 删除，Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 删除范围、插入广告 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 插入的广告 |
| 替换， Auditude | 删除，Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 已替换范围 |
| 标记 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记的范围 |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记范围，未插入广告 |

**清单提示**

| 广告元数据 | 已创建解析器 | `PlacementInformations` 已创建 | 结果行为 |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 插入的广告 |
| 删除，Auditude | 删除，Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 删除范围，插入广告 |
| Mark, Auditude | Mark, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记范围，未插入广告 |
| 删除 | 删除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已删除范围 |
| 标记 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记的范围 |
| 替换， Auditude | 删除，Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 已替换范围 |

**自定义时间范围**

| 广告元数据 | 已创建解析器 | `PlacementInformations` 已创建 | 结果行为 |
|--- |--- |--- |--- |
| 删除 | 删除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已删除范围 |
| 删除，Auditude | 删除，Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 范围已删除，未插入任何广告 |
| Auditude | Auditude | 无 | 未插入广告 |
| 替换， Auditude | 删除，Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 用广告替换范围 |
| 标记 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记的范围 |
| Mark, Auditude | 自定义广告， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记范围，未插入广告 |

**未设置（默认）**

| 广告元数据 | 已创建解析器 | `PlacementInformations` 已创建 | 结果行为 |
|--- |--- |--- |--- |
| 删除 | 删除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已删除范围 |
| 删除，Auditude | 删除，Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 删除范围，插入广告 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 插入的广告 |
| 替换， Auditude | 删除，Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 用广告替换范围 |
| 标记 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记的范围 |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记的范围 |