---
description: 通过向清单服务器发送新的广告插入请求来替换VOD时间轴，并使用相应设置的时间轴查询参数。
title: 替换VOD时间轴
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 替换VOD时间轴{#replace-a-vod-timeline}

通过向清单服务器发送新的广告插入请求来替换VOD时间轴，并使用相应设置的时间轴查询参数。

1. 按常规方式准备广告插入请求。
1. 将`ptcueformat`查询参数设置为DPIScte35。
1. 根据需要将`enableC3`查询参数设置为true或false。
1. 使用VOD时间轴格式创建`pttimeline`参数：
   1. 使用`duration = 0`和`number_of_lots = 1`指定每个内容块（章节）。
   1. 按常规方式指定每个广告块，但设置`lots = 0`以删除中断。 设置`duration = 0`以使用广告中断的持续时间（来自M3U8文件）。

## 示例：替换VOD时间轴

此示例假定VOD内容位于时间轴为`C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`的`Original.m3u8`中

以下清单服务器请求用30秒的预卷替换`Original.m3u8`中的分段，然后是两个持续时间的分段，每分钟两分钟。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

以下清单服务器请求删除`Original.m3u8`中的中断，并添加30秒前滚和30秒后滚。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
