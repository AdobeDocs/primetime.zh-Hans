---
description: 通过向清单服务器发送新的广告插入请求以使用相应设置的pttimeline查询参数来替换VOD时间轴。
seo-description: 通过向清单服务器发送新的广告插入请求以使用相应设置的pttimeline查询参数来替换VOD时间轴。
seo-title: 替换VOD时间轴
title: 替换VOD时间轴
uuid: 17a6daa3-5ee5-48fb-8981-0d183aed0fe4
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 替换VOD时间轴 {#replace-a-vod-timeline}

通过向清单服务器发送新的广告插入请求以使用相应设置的pttimeline查询参数来替换VOD时间轴。

1. 按常规方式准备广告插入请求。
1. 将查 `ptcueformat` 询参数设置为DPIScte35。
1. 根据需要 `enableC3` 将查询参数设置为true或false。
1. 使用VOD `pttimeline` 时间轴格式创建参数：
   1. 使用和指定每个内容块(章 `duration = 0` 节) `number_of_lots = 1`。
   1. 按常规方式指定每个广告块，但 `lots = 0` 设置为删除分段。 设 `duration = 0` 置为使用广告中断的持续时间（从M3U8文件）。

## 示例：替换VOD时间轴

此示例假定VOD内容与时间 `Original.m3u8` 轴位于 `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

以下清单服务器请求用30秒 `Original.m3u8` 的前滚时间替换中断，后跟两个持续时间间隔，每个分钟两分钟。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

以下清单服务器请求删除了中断 `Original.m3u8` ，并添加了30秒前滚和30秒后滚。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
