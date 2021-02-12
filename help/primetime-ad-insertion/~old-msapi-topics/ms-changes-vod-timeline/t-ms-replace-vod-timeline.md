---
description: 通过向清单服务器发送新的广告插入请求以适当设置的pttimeline查询参数来替换VOD时间线。
seo-description: 通过向清单服务器发送新的广告插入请求以适当设置的pttimeline查询参数来替换VOD时间线。
seo-title: 替换VOD时间轴
title: 替换VOD时间轴
uuid: 17a6daa3-5ee5-48fb-8981-0d183aed0fe4
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# 替换VOD时间轴{#replace-a-vod-timeline}

通过向清单服务器发送新的广告插入请求以适当设置的pttimeline查询参数来替换VOD时间线。

1. 按常规方式准备广告插入请求。
1. 将`ptcueformat`查询参数设置为DPIScte35。
1. 根据需要将`enableC3`查询参数设置为true或false。
1. 使用VOD时间轴格式创建`pttimeline`参数：
   1. 使用`duration = 0`和`number_of_lots = 1`指定每个内容块（章节）。
   1. 按常规方式指定每个广告块，但设置`lots = 0`以删除中断。 设置`duration = 0`以使用广告中断的持续时间（从M3U8文件）。

## 示例：替换VOD时间轴

此示例假定VOD内容位于时间轴为`C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`的`Original.m3u8`中

以下清单服务器请求用30秒的预卷替换`Original.m3u8`中的中断，后跟两个持续时间的中断，每分钟两分钟。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

以下清单服务器请求删除`Original.m3u8`中的中断，并添加30秒前滚动和30秒后滚动。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
