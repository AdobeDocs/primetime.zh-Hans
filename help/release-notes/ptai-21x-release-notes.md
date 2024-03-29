---
title: PTAI 21.11.1发行说明
description: PTAI发行说明介绍了2021年PrimetimeAd Insertion中的新增或更改内容、已解决问题和已知问题。
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# PrimetimeAd Insertion21.11.1发行说明

PrimetimeAd Insertion21.xx.x发行说明介绍了2021年PrimetimeAd Insertion中的新增或更改内容、已解决问题和已知问题。

## PTAI 21.11.1的新增功能

时间：东部时间2021年11月9日星期二半夜1点30分至4点30分

* [!UICONTROL EXT-X-IMAGE-STREAM-INF] 现在可以按区域进行配置。

* 完全支持Roku Trick Play。

## 以前版本中的增强功能和修复

### 版本21.10.1

时间：东部时间2021年10月12日星期二早上7:45至下午1:45

* 整合了服务器，删除了非生产和无用的服务器。

### PrimetimeAd Insertion维护版本

时间：东部时间2021年9月28日星期二凌晨5点至6点

* 从AWS的Elastic Load Balancer到AWS的Application Load Balancer的负载平衡器栈栈更新，以增强功能和可扩展性。 这些负载平衡器用于将广告请求流量从Ad Insertion层(SSAI/CSAI)路由到Auditude后端。

### 版本21.9.1

时间：东部时间2021年9月7日星期二凌晨02点30分至05点30分

* 更新了PrimetimeAd Insertion的中介和报告组件后面的基础架构组件(Primetime Ads GUI)。

### 版本21.8.1

时间：东部时间2021年8月24日星期二凌晨2点至5点

* 添加了对DASH实时/线性流的支持（已支持VOD）。

### 版本21.5.1

时间：东部时间2021年5月26日星期三凌晨3时30分至6时30分

**更改**

* 为基于SCTE的提示格式添加了对已弃用分段类型0x01 (UPID)的支持。

* 为即将进行的仪表板更改添加了新遥测。

### 版本21.4.1

**时间：** 2021年4月22日，星期四东部时间凌晨2点至5点

**更改**

* 将启用会话请求限制，以防止潜在的DDOS攻击。 会议限制为每秒10个请求，排队的请求上限为100个。 我们预计不会对按照HLS/DASH规范运行的播放器产生任何影响。

* 其他维护和安全增强功能

### 版本21.2.2

**时间：** 2021年2月23日，星期二东部时间半夜1点至4点

**更改**

* 添加了对HLS流中EXT-X-IMAGE-STREAM-INF流插入/同步的支持。 该功能通过服务器端配置启用。 请联系您的技术客户代表以启用该功能。

### 版本21.2.1

**时间：** 2021年2月3日，星期三东部时间半夜1点至4点

**更改**

* 添加了对DASH输出优化（基于时间的节点合并）的支持。

### 版本21.1.2

**时间：** 2021年1月19日，星期二东部时间半夜12点30分至8点30分

**更改**

* 维护更新：升级PrimetimeAd Insertion后端memcache群集。

### 版本21.1.1

**时间：** 2021年1月13日，星期三，东部时间半夜1点至4点

**更改**

* 为基于SCTE35的提示格式添加了对附属机构提供的支持。
