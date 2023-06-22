---
description: 通过用正确设置的时间线查询参数向清单服务器发送新的广告插入请求来替换VOD时间线。
title: 替换VOD时间线
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 替换VOD时间线 {#replace-a-vod-timeline}

通过用正确设置的时间线查询参数向清单服务器发送新的广告插入请求来替换VOD时间线。

1. 按常规方式准备广告插入请求。
1. 设置 `ptcueformat` 查询参数到DPIScte35。
1. 设置 `enableC3` 将查询参数设置为true或false（根据需要）。
1. 创建 `pttimeline` 参数使用VOD时间线格式：
   1. 使用以下方式指定每个内容块（章节） `duration = 0` 和 `number_of_lots = 1`.
   1. 照常指定每个广告块，但设置 `lots = 0` 以删除中断。 设置 `duration = 0` 以使用广告时间的持续时间（来自M3U8文件）。

## 示例：替换VOD时间线

此示例假定VOD内容位于 `Original.m3u8` 时间线为 `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

以下清单服务器请求替换中的断点 `Original.m3u8` 前置时间为30秒，随后是两次持续时间中断，每次中断两分钟。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

以下清单服务器请求删除中的断点 `Original.m3u8` 并添加一个30秒的前置滚动和1个30秒的后置滚动。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
