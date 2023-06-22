---
description: 在某些情况下，您可能希望限制最终用户在购买或租赁内容时在多个设备上播放内容。 如果客户正在使用Expressplay，可以通过使用Expressplay API将用户的Expressplay令牌绑定到用户的计算机来完成此操作。
title: 设备绑定
exl-id: 96ead794-e3eb-4059-91d3-a2c351a17ea3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 设备绑定{#device-binding}

在某些情况下，您可能希望限制最终用户在购买或租赁内容时在多个设备上播放内容。 如果客户正在使用Expressplay，可以通过使用Expressplay API将用户的Expressplay令牌绑定到用户的计算机来完成此操作。

您可以通过以下方式使用API。

1. 生成Cookie。
1. 发送一个虚拟令牌生成请求，并将生成的Cookie作为查询字符串(Cookie=`<cookie>`)或作为标头。
1. 让用户的机器使用上述令牌（例如，通过播放虚拟内容）向Expressplay许可证服务器发送许可证请求。

   此虚拟许可证请求在成功后将用户的device_id（由用户设备上的DRM实施计算或生成）与Expressplay后端中的Cookie相关联。 然后按以下方式使用此Cookie：

   * 在内容购买/租赁时，代码通过发送关联的Cookie ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * 使用购买内容的密钥(CEK)、keyID (CEKSID)、策略和其他信息发送令牌生成请求，并将上述Cookie和device_id分别作为 `cookie` 相关参数和 `deviceid` 令牌限制参数。

   * 将此令牌提供给用户。

      此过程为绑定到用户的device_id的内容生成一个令牌。 当用户的计算机使用此令牌发送许可证请求时，Expressplay后端将交叉检查令牌的device_id和许可证请求的device_id。

      一个Expressplay授权服务器示例实现了此工作流。
