---
title: Account IQ术语表
description: 产品术语词汇表。
exl-id: 2ee54442-9538-4c30-b999-265310b3935f
source-git-commit: 4eb5ba53fb3e0a0c314695fcd30cf15c7242b53c
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 0%

---

# 产品概念和术语表 {#glossary}

请参阅以下产品术语及其定义。

## 帐户共享概率 {#account-sharing-probability-def}

带有图表的仪表板面板，可将当前区段共享得分分为“非常低”、“低”、“中”、“高”和“非常高”等共享范围类别。

## 操作 {#action-def}

与关联的直接或间接事件 [操作](#operation-def) ，这会影响相关操作区段（或同类群组）的特性（例如，共享分数或使用中的设备数量）。

## 聚合共享分数 {#sharing-probability-level-def}

带有图表的仪表板面板，可将当前共享得分的区段分为非常低、低、中、高和非常高的共享范围类别，以及每个类别占区段流处理总量的百分比。

## 身份验证N {#authn-def}

身份验证，或身份验证尝试的次数。 身份验证尝试是一个过程，没有当前有效身份验证状态的用户将被重定向到他们选择的MVPD，他们在其中向MVPD标识自己 — 通常使用用户名和密码。

## 身份验证正常 {#authn-ok-def}

成功身份验证的次数。 当用户标识由MVPD确认并导致用户被重定向回程序员应用程序或站点时，就会发生成功的身份验证。

## AuthZ {#authz-def}

授权，或授权请求的数量。 授权请求是程序员通过Adobe从MVPD请求权限以开始流式传输用户请求内容的过程。 MVPD通常根据与用户的MVPD订阅相关联的内容权限来授予请求（例如，与内容相关联的频道是否在用户的订阅中）。 Adobe缓存了一些授权请求响应，这允许Adobe立即响应，而无需将请求传递给MVPD。

## AuthZ正常 {#authz-ok-def}

成功的授权数量。

## 渠道 {#channel-def}

渠道（也称为属性）是视频内容的主题相关来源。 传统上，表示来自MVPD的不同、数字可寻址连续视频馈送。 该渠道直接映射到订阅者通过其机顶盒(STB)可用的内容的可访问渠道。

## 集群 {#cluster-def}

群集是位置和设备的集合。 群集是通过查找设备之间的公共位置创建的。 在公共位置看到的设备将被视为属于同一群集。 两个设备可以位于同一群集中，即使它们没有公共位置，但可以通过其他设备的位置进行连接。

### 移动集群 {#mobile-cluster-def}

没有静态设备的群集。

### 静态群集 {#static-cluster-def}

至少具有一个静态设备的群集。

## 并发 {#consurrency-def}

并发由两个（或多个）同时播放或时间非常接近的流定义，因此它们之间的间隔不能通过以正常速度旅行来调整。
并行使用量是使用2个不同集群之间的最大速度（英里/小时）计算的。 如果用户在124英里以下的距离上速度大于124米/小时，或者如果用户在超过124英里的距离上速度大于400米/小时，则被视为同时使用。 计算来自不同簇的位置之间的距离。 同一群集中允许并发使用。

## 设备 {#device-def}

一种数字视频硬件产品，可播放TV Everywhere内容，并受Adobe Pass支持。 例如，智能手机、笔记本电脑和台式计算机、游戏机和智能电视。

## 地理范围 {#geographical-span-def}

一组位置中最远点之间的距离。

## 粒度 {#granularity-def}

对于时间范围，是指期间的大小；例如一周或一个月。

## 行业平均指数 {#industry-avg-index-def}

在选定的时间范围内为所有程序员和MVPD的每个风险指数（帐户、使用情况、总体）计算的值。

## IP {#ip-def}

Internet服务提供商分配给设备的Internet协议地址。 例如，有线服务提供商和小区服务提供商。

## 隔离模式 {#isolation-mode-def}

一种共享分析类型，其中帐户的评估仅限于在选定区段中直接发生在程序员身上的事件。  通常，会评估所有帐户事件，从而更准确地估计共享情况。  某些MVPD数据的结构方式仅允许隔离模式分析。

## 位置 {#location-def}

地球上独一无二的地方。 此外，它也被称为特定播放请求的地理位置（使用Pass数据检测），精度为1000mx1000m（1平方公里）。

<!-- ### Home location {#home-location-def}

the precision is 0.01 ~ 2000mx2000m (4 square km) - at this moment the home location is detected using an ML algo, based on data provided by two mvpds. The probability is ~ 80%. We are not using the zip code for the majority of the users. Currently, this information is not used in assessing the sharing probability. -->

## 媒体公司 {#media-company-def}

Media Company是一家拥有一组媒体网络的公司。

## 量度 {#metric}

量度是订阅者帐户的一个属性（例如，他们的MVPD、程序员和他们流传输内容的渠道、他们使用的设备数量）。

## 移动设备 {#mobile-device-def}

具有高移动性的设备。 例如，手机和平板电脑。

## MVPD {#mvpd-def}

MVPD也称为分发商，是媒体公司视频内容的汇总、转销商和分发商。

## 操作 {#operation-def}

操作是为跟踪特定操作效果而创建的记录 [操作](#action-def) 在关联的区段上。 例如，可以限制段标识的帐户允许的并发流数量。

## 总体共享得分 {#overall-sharing-score}

一个值，可帮助用户了解在程序员资产上或MVPD订阅者共享密码的程度，并让他们有一种紧迫感，需要采取行动。

<!--**Aggregated Risk Index**
Also known as Risk Index and Sharing Risk Index, it is a value that helps users understand the magnitude of password sharing on Programmer properties or by MVPD subscribers and provides them a sense of urgency to act upon it.-->

<!--**Risk Index - Overall**
A value computed as an average of "Risk Index - Accounts" and the "Risk Index - Usage". Overall Sharing Risk Index-->

## 播放请求 {#play-requests-def}

客户端应用程序或站点发出的请求，用于Adobe请求用于记录和保护流开始的媒体令牌。

## 程序员 {#programmer-def}

Programmer，也称为Network，是拥有和管理一个或多个渠道的大公司（公司）的子公司。

## 请求者ID {#requestorid-def}

媒体公司用于标识自己或MVPD子公司的ID。  根据程序员实施，这可以映射到媒体公司、程序员或渠道。  媒体公司用于标识自己或MVPD子公司的最常见ID。  根据程序员实施，这可以映射到媒体公司、程序员或渠道。  传统上，这会映射到渠道。  通过创建诸如MML（三月疯狂Live）之类的伪渠道以及进行技术性移动以解决MVPD驱动的数据限制，requestorID开始越来越与媒体公司建立关联。

## 资源ID {#resource-id-def}

最终用户请求的内容。  传统上，这已标识与用户请求的内容关联的渠道。  系统增强允许ID表示特定节目（例如具有特定评级），ID继续标识相关联频道。

## 风险指数 — 使用情况 {#risk-index-usage}

也称为“共享帐户的使用情况”，它是一个根据每个帐户发出的播放请求数计算的值，这些播放请求由每个帐户的共享概率加权。 也称为使用共享帐户风险指数。

## 区段 {#segmet-def}

区段是一组符合由所选量度指定的用户定义条件的帐户（例如“已观看频道X、Y或Z的MVPD A、B、C、D或E的用户”）。

## 共享级别 {#sharing-level-def}

风险指数 — 帐户或共享帐户风险指数，该值是根据一组选定MVPD中每个帐户计算的平均共享概率而计算的，该组选定MVPD在选定的时间范围内从其中一个选定的程序员渠道进行流式处理。

## 静态设备 {#static-device-def}

移动性非常低的设备。 例如，游戏机、机顶盒和电视机。

## 期限 {#time-frame-def}

该时段也称为“时段”或“时隙”，它包含用户界面中显示的播放请求活动，以及从开始到结束的表格。

## 区段中的热门MVPD {#top-mvpds-def}

所选区段中的排名最前的（最多10个）MVPD，可按共享级别、共享帐户的使用情况或总体共享分数进行衡量。

## 趋势 {#trend-def}

当前时段和上一时段之间关联量度的百分比差异（例如，总播放请求的百分比）。

## 独特订阅者 {#unique-subscriber-def}

在给定期间内与程序员TV Everywhere应用程序或涉及Adobe Pass的网站交互的给定期间的唯一MVPD帐户数。  该交互包括程序员应用程序或网站上导致调用Adobe Pass服务的任何活动。 例如，检查authN或authZ状态、身份验证和授权。 如果程序员使用AdobeTempPass（即免费预览）是区段的一部分，则独特订阅者的总数还将包括独特设备的数量。

## 使用情况 {#usage-defs}

### 狂热用户 {#avid-user-def}

每月超过37个播放请求。

### 不常见用户 {#infrequent-users-def}

每月少于9个播放请求。

### 普通用户 {#regular-user-def}

每月9到37个播放请求。

## 使用模式 {#usage-patern-def}

应用于帐户的一组有限类别标签之一，最能体现帐户用户在社交群体或行为方面的特征（例如，小家庭、旅行者或通勤者、社交分享等）。

## 邮政编码 {#zip-code-def}

与境内位置关联的美国邮政编码
