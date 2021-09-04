---
title: PTAI 21.8.1发行说明
description: PTAI发行说明介绍了PrimetimeAd Insertion2021年的新增功能或更改功能、已解决和已知问题。
exl-id: 39a05f6d-431a-4416-81b1-21d82c0dbd69
source-git-commit: 97a192ed1d0ddc034f72a836a70293acfcca9881
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# PrimetimeAd Insertion21.8.1发行说明

PrimetimeAd Insertion21.x.x发行说明介绍了PrimetimeAd Insertion2021年的新增功能或更改功能、已解决的问题和已知问题

<!---
Primetime Ad Insertion 21.9.1
When: Tuesday, September 7, 2021 from 02:30 AM to 05:30 AM EASTERN









What:  Primetime Ad Insertion 21.9.1

When:  Tuesday, September 7, 2021 from 02:30 AM to 05:30 AM Eastern Time

Changes:

* Updates to infrastructure components behind PTAI’s mediation and reporting components (Primetime Ads GUI)
-->

## PTAI 21.8.1的新增功能

时间：2021年8月24日，星期二，东部时间凌晨2点至5点

* 添加了对短划线实时/线性流的支持（已支持VOD）。

## 以前版本中的增强功能和修复

### 版本21.5.1

时间： 2021年5月26日，星期三东部时间凌晨3点30分至6点30分

**更改**

* 为基于SCTE的提示格式添加了对已弃用分段类型0x01(UPID)的支持。

* 为即将进行的功能板更改添加了新的遥测数据。

### 版本21.4.1

**时间：** 2021年4月22日，星期四，东部时间凌晨2点至5点

**更改**

* 将启用会话请求限制以防止潜在的DDOS攻击。 会话数将限制为每秒10个请求，最多为100个已排队的请求。 我们预计不会对按照HLS/DASH规范行事的播放器产生任何影响。

* 其他维护和安全增强功能

### 版本21.2.2

**时间：** 2021年2月23日星期二东部时间凌晨1点至4点

**更改**

* 添加了对HLS流中EXT-X-IMAGE-STREAM-INF流插入/同步的支持。 该功能通过服务器端配置启用。 请联系您的技术客户代表以启用此功能。

### 版本21.2.1

**时间：** 2021年2月3日，星期三，东部时间凌晨1点至4点

**更改**

* 添加了对DASH输出优化的支持：基于时间的节点整合。

### 版本21.1.2

**时间：** 2021年1月19日星期二东部时间半夜12点30分至08点30分

**更改**

* 维护更新：升级PrimetimeAd Insertion后端成员缓存群集。

### 版本21.1.1

**时间：** 2021年1月13日，星期三，东部时间上午1点至4点

**更改**

* 添加了对联属网站提供的对基于SCTE35的提示格式的支持。
