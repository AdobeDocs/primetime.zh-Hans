---
description: 您可以使用不同的广告信令模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 信令模式和元数据的不同组合导致不同的行为。
title: 对广告信令模式和广告元数据组合中的广告插入和删除的影响
exl-id: f42a2db5-642f-4944-87f6-2d7d902a2837
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# 对广告信令模式和广告元数据组合中的广告插入和删除的影响 {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

您可以使用不同的广告信令模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 信令模式和元数据的不同组合导致不同的行为。

>[!TIP]
>
>当时间范围与广告信令模式存在冲突时，TVSDK给出时间范围的优先级。

下表提供有关信令模式和元数据组合行为的详细信息：

**服务器映射**

| **广告元数据** | **已创建解析程序** | **`PlacementInformations`已创建** | **结果行为** |
|--- |--- |--- |--- |
|  | 删除 | 删除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已删除范围 |
| 删除，审核 | 删除，审核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 已删除范围，插入广告 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 广告已插入 |
| 替换，审计 | 删除，审核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 已替换范围 |
| 标记 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记的范围 |
| Mark， Auditude | CustomAd， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 已标记范围，未插入广告 |

**清单提示**

| 广告元数据 | 已创建解析程序 | `PlacementInformations` 已创建 | 结果行为 |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 广告已插入 |
| 删除，审核 | 删除，审核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | 已删除范围，插入广告 |
| Mark， Auditude | Mark， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 已标记范围，未插入广告 |
| 删除 | 删除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已删除范围 |
| 标记 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记的范围 |
| 替换，审计 | 删除，审核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 已替换范围 |

**自定义时间范围**

| 广告元数据 | 已创建解析程序 | `PlacementInformations` 已创建 | 结果行为 |
|--- |--- |--- |--- |
| 删除 | 删除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已删除范围 |
| 删除，审核 | 删除，审核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已删除范围，未插入广告 |
| Auditude | Auditude | 无 | 未插入广告 |
| 替换，审计 | 删除，审核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 范围已替换为广告 |
| 标记 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记的范围 |
| Mark， Auditude | 自定义广告、审核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 已标记范围，未插入广告 |

**未设置（默认）**

| 广告元数据 | 已创建解析程序 | `PlacementInformations` 已创建 | 结果行为 |
|--- |--- |--- |--- |
| 删除 | 删除 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | 已删除范围 |
| 删除，审核 | 删除，审核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 已删除范围，插入广告 |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | 广告已插入 |
| 替换，审计 | 删除，审核 | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | 范围已替换为广告 |
| 标记 | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记的范围 |
| Mark， Auditude | CustomAd， Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | 标记的范围 |
