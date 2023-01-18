---
title: 帐户IQ术语表
description: 产品术语表。
exl-id: 2ee54442-9538-4c30-b999-265310b3935f
source-git-commit: 4eb5ba53fb3e0a0c314695fcd30cf15c7242b53c
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 0%

---

# 产品概念和术语表 {#glossary}

请参阅以下产品术语及其定义。

## 帐户共享概率 {#account-sharing-probability-def}

功能板面板，其中包含图表，用于将共享分数的当前区段划分为“非常低”、“低”、“中”、“高”和“非常高”的共享范围类别。

## 操作 {#action-def}

与 [操作](#operation-def) 会影响相关操作区段（或同类群组）的特性（例如，共享分数或正在使用的设备数量）。

## 汇总共享分数 {#sharing-probability-level-def}

一个功能板面板，其中包含图表，用于将共享分数的当前区段划分为“非常低”、“低”、“适度”、“高”和“非常高”的共享范围类别，以及区段流总量的各个类别百分比。

## AuthN {#authn-def}

身份验证或身份验证尝试次数。 身份验证尝试是一种过程，在该过程中，没有当前有效身份验证状态的用户被重定向到其选择的MVPD，在该MVPD中，他们将自己标识到MVPD（通常使用用户名和密码）。

## AuthN OK {#authn-ok-def}

成功身份验证的次数。 当MVPD确认用户的标识并导致用户被重定向回程序员应用程序或网站时，会发生成功的验证。

## AuthZ {#authz-def}

授权或授权请求的数量。 授权请求是程序员通过Adobe从MVPD请求许可以开始流式传输用户请求的内容的过程。 MVPD通常根据与用户的MVPD订阅相关的内容权限（例如，与内容关联的渠道是否在用户的订阅中）来授予请求。 某些授权请求响应由Adobe缓存，这允许Adobe立即做出响应，而无需将请求传递到MVPD。

## AuthZ OK {#authz-ok-def}

成功授权的数量。

## 渠道 {#channel-def}

渠道也称为属性，是与主题相关的视频内容源。 传统上表示来自MVPD的可寻址的不同连续视频馈送。 该频道直接映射到用户通过其机顶盒(STB)可获得的内容的无障碍频道。

## 群集 {#cluster-def}

群集是位置和设备的集合。 通过查找设备之间的公共位置来创建群集。 在公共位置看到的设备将被视为属于同一群集中。 两个设备可以位于同一群集中，即使它们没有共同的位置，但可以通过其他设备的位置进行连接。

### 移动设备群集 {#mobile-cluster-def}

没有静态设备的群集。

### 静态群集 {#static-cluster-def}

具有至少一个静态设备的群集。

## 并发 {#consurrency-def}

并发由两个（或多个）同时播放或时间非常接近的流定义，因此它们之间的间隔不能通过以正常速度行驶来证明。
并行使用率是使用2个不同群集之间的最大速度（英里/小时）计算的。 如果用户的速度在小于124英里的距离上大于124米/小时，或者其速度在大于124英里的距离上大于400米/小时，则用户被视为具有并发使用。 从不同簇的位置之间计算距离。 同一群集中允许并发使用。

## 设备 {#device-def}

一种数字视频硬件产品，可以播放随时随地的电视内容，受Adobe Pass支持。 例如，智能手机、笔记本电脑和台式计算机、游戏机和智能电视。

## 地理范围 {#geographical-span-def}

一组位置中最远点之间的距离。

## 粒度 {#granularity-def}

参照时间范围，周期的大小；例如一周或一个月。

## 行业平均指数 {#industry-avg-index-def}

在选定的时间范围内，针对所有程序员和MVPD的每个风险索引（帐户、使用情况、整体）计算的值。

## IP {#ip-def}

由互联网服务提供商分配给设备的互联网协议地址。 例如，电缆服务提供商和蜂窝服务提供商。

## 隔离模式 {#isolation-mode-def}

一种共享分析类型，其中帐户评估仅限于所选区段中程序员直接发生的事件。  通常，会评估所有帐户事件，从而提供更准确的共享估计。  某些MVPD数据的结构方式仅允许进行隔离模式分析。

## 位置 {#location-def}

地球上独一无二的地方。 此外，它也称为使用Pass数据检测的特定播放请求的地理位置，其精度为1000mx1000m（1平方公里）。

<!-- ### Home location {#home-location-def}

the precision is 0.01 ~ 2000mx2000m (4 square km) - at this moment the home location is detected using an ML algo, based on data provided by two mvpds. The probability is ~ 80%. We are not using the zip code for the majority of the users. Currently, this information is not used in assessing the sharing probability. -->

## 媒体公司 {#media-company-def}

媒体公司是拥有一组媒体网络的公司。

## 量度 {#metric}

量度是订阅者帐户的属性（例如，其MVPD、其流内容的程序员和渠道、使用的设备数量）。

## 移动设备 {#mobile-device-def}

一种高移动性的设备。 例如，手机和平板电脑。

## MVPD {#mvpd-def}

MVPD（也称为“分发者”）是媒体公司视频内容的聚合商、转销商和分发商。

## 操作 {#operation-def}

操作是为跟踪特定 [操作](#action-def) 在关联的区段上。 例如，对区段标识的帐户所允许的并发流数量施加限制。

## 总体共享分数 {#overall-sharing-score}

此值可帮助用户了解程序员属性或MVPD订阅者共享密码的程度，并为用户提供采取行动的紧迫感。

<!--**Aggregated Risk Index**
Also known as Risk Index and Sharing Risk Index, it is a value that helps users understand the magnitude of password sharing on Programmer properties or by MVPD subscribers and provides them a sense of urgency to act upon it.-->

<!--**Risk Index - Overall**
A value computed as an average of "Risk Index - Accounts" and the "Risk Index - Usage". Overall Sharing Risk Index-->

## 播放请求 {#play-requests-def}

客户端应用程序或网站向Adobe发出的请求，请求媒体令牌记录和保护流启动。

## 程序员 {#programmer-def}

程序员，又称Network，是一家大型公司（公司）的子公司，拥有并管理一个或多个渠道。

## requestorID {#requestorid-def}

媒体公司用于标识自己或MVPD子公司的ID。  根据程序员的实施情况，这可以映射到媒体公司、程序员或渠道。  媒体公司用来标识自己或MVPD的子公司的最常见ID。  根据程序员的实施情况，这可以映射到媒体公司、程序员或渠道。  传统上，它会映射到渠道。  随着诸如MML（3月疯狂直播）之类的伪渠道的创建以及技术驱动的旨在解决MVPD驱动数据限制的移动，requestorID开始与媒体公司更加相关联。

## resourceID {#resource-id-def}

最终用户请求的内容。  传统上，这会识别与用户请求的内容关联的渠道。  系统增强功能允许该ID表示特定节目（例如，具有特定评级），该ID继续标识关联的渠道。

## 风险指数 — 使用情况 {#risk-index-usage}

此值也称为“来自共享帐户的使用情况”，它是根据每个帐户发出的播放请求数计算的值，该请求数由每个帐户的共享概率加权。 它也称为“按共享帐户使用风险指数”。

## 区段 {#segmet-def}

区段是一组满足所选量度（例如“MVPD A、B、C、D或E的用户已观看渠道X、Y或Z）所指定用户定义条件的帐户。

## 共享级别 {#sharing-level-def}

它也称为风险指数 — 帐户或共享帐户风险指数，它是根据在选定时间范围内从选定程序员渠道之一流传输的选定MVPD集合中每个帐户的共享概率平均值计算的值。

## 静态装置 {#static-device-def}

一种移动性极低的设备。 例如，游戏机、机顶盒和电视机。

## 时间范围 {#time-frame-def}

它也称为时段或时段，它是包含在用户界面和表中从头到尾显示的播放请求活动的时间窗口。

## 区段中的热门MVPD {#top-mvpds-def}

选定区段中排名最前（最多10个）的MVPD，可通过共享级别、共享帐户的使用情况或整体共享得分来衡量。

## 趋势 {#trend-def}

当前时段与上一时段之间关联量度的百分比差异（例如，总播放请求的百分比）。

## 独特订阅者 {#unique-subscriber-def}

在指定时间段内与程序员TV Everywhere应用程序或涉及Adobe Pass的网站交互的唯一MVPD帐户数。  该交互包括在程序员应用程序或网站上导致调用Adobe Pass服务的任何活动。 例如，检查authN或authZ状态、身份验证和授权。 如果程序员使用AdobeTempPass（免费预览）是区段的一部分，则独特订阅者总数还将包括独特设备数。

## 使用情况 {#usage-defs}

### Avid用户 {#avid-user-def}

每月播放请求超过37次。

### 不频繁用户 {#infrequent-users-def}

每月播放请求少于9个。

### 常规用户 {#regular-user-def}

每月9到37次播放请求。

## 使用模式 {#usage-patern-def}

适用于帐户的有限类别标签集之一，该类别标签在社会群体或行为（例如，小家庭、旅行者或通勤者、社交共享等）方面最能体现帐户用户的特征。

## 邮政编码 {#zip-code-def}

与美国境内的位置关联的美国邮政编码
