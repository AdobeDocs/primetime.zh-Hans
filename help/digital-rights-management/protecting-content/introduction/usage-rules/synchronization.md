---
description: 'null'
seo-description: 'null'
seo-title: 同步要求
title: 同步要求
uuid: 594a4bb2-c042-4485-9cae-73b8f9f93d82
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 同步{#requirements-for-synchronization}的要求

同步要求指定客户端与服务器同步其状态的频率。 如果客户端已颁发带外许可证（未联系许可证服务器），则使用规则可指定客户端必须向服务器发送同步消息以同步客户端的安全时间，并向服务器报告客户端状态。

同步行为使用以下参数定义：

* **开始间隔** -指定在上次成功同步后等待多长时间以开始另一个同步请求。
* **硬停止间隔** -（可选）。如果在指定的时间段内未成功同步，则不允许播放。
* **强制同步概率** -（可选）。客户端在下一个开始间隔之前发送同步消息的概率。

>[!NOTE]
>
>Primetime DRM客户端版本3.0或更高版本支持此使用规则。 旧客户端上的行为取决于许可证服务器支持的最低客户端版本。

