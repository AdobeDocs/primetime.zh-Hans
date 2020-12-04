---
description: 在某些情况下，您可能希望限制最终用户在购买或租用内容时在多个设备上播放内容。 如果客户使用Expressplay，则可以使用Expressplay API将用户的Expressplay令牌绑定到用户的机器上。
seo-description: 在某些情况下，您可能希望限制最终用户在购买或租用内容时在多个设备上播放内容。 如果客户使用Expressplay，则可以使用Expressplay API将用户的Expressplay令牌绑定到用户的机器上。
seo-title: 设备绑定
title: 设备绑定
uuid: 351fa33c-4226-4ed5-829c-56b563166fec
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# 设备绑定{#device-binding}

在某些情况下，您可能希望限制最终用户在购买或租用内容时在多个设备上播放内容。 如果客户使用Expressplay，则可以使用Expressplay API将用户的Expressplay令牌绑定到用户的机器上。

您可以通过以下方式使用API。

1. 生成Cookie。
1. 发送虚拟令牌生成请求，生成的cookie作为查询字符串(cookie=`<cookie>`)或头附加。
1. 让用户的计算机使用上述令牌向Expressplay许可证服务器发送许可证请求，例如播放虚拟内容。

   如果此虚拟许可证请求成功，则将用户的device_id（由用户设备上的DRM实现计算或生成）与Expressplay后端中的cookie关联。 然后，此Cookie的使用方式如下：

   * 在内容购买／租用时，代码通过发送关联的cookie([https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))将Expressplay后端查询为用户的device_id
   * 发送包含所购买内容的密钥(CEK)、keyID(CEKSID)、策略和其他信息的令牌生成请求，将上述cookie和device_id分别附加为`cookie`相关参数和`deviceid`令牌限制参数。

   * 为用户提供此令牌。

      此进程为绑定到用户的device_id的内容生成一个令牌。 当用户的计算机发出包含此令牌的许可证请求时，Expressplay后端将使用许可证请求的device_id交叉检查令牌的device_id。

      示例Expressplay授权服务器实现此工作流。
