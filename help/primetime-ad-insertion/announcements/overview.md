---
title: Adobe PrimetimeAd Insertion公告
seo-title: Adobe PrimetimeAd Insertion公告
description: 关于Primetime最新功能发布和其他相关新闻的公告Ad Insertion
seo-description: 关于Primetime最新功能发布和其他相关新闻的公告Ad Insertion
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# PrimetimeAd Insertion公告

## 通过广告解决超时减少程序化广告错误

发布日期：2000年12月1日

Adobe专注于帮助PrimetimeAd Insertion客户最大化其广告库存的盈利。 我们特别重视降低满足程序化需求的复杂性，根据eMarketer的数据，程序化需求占美国数字视频广告支出的四分之三以上。 程序化销售使出版商能够最大化对其广告库存的需求，从而提高填写率和收益。 但是，它还增加了广告错误（如格式错误的VAST响应、HTTP错误和其他可能导致收入损失和／或查看器体验不佳的错误）的曝光率。

一个常见问题是程序化合作伙伴的广告响应缓慢。 通常，程序化广告交易以毫秒为单位进行。 但有时，单一需求来源可能需要过长的时间才能响应。 来自单个提供商的延迟可能会影响整个广告实施过程，从而导致查看器、未填充广告插槽或在极端情况下需要重新启动视频流的临时空白屏幕。 不幸的是，识别和绕过缓慢的需求来源是一个重大挑战。

为了解决此问题，Adobe为PrimetimeAd Insertion添加了新工具，使客户能够为广告解决设置时间限制。 设置这些规则会导致慢速需求源自动绕过，从而确保视频播放器及时获得广告响应。 这使出版商能够大大限制需求来源缓慢造成的中断，帮助他们最大限度地提高库存填充率，并提供不间断的、电视质量的观看体验。

要在PrimetimeAd Insertion中启用广告分辨率超时，请修改引导API以包含ptadtimeout参数(持续时间（毫秒）。  在超时持续时间之前未完成的任何广告请求将不会被拼接（将处理任何回退广告）。