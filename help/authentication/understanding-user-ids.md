---
title: 了解用户ID
description: 了解用户ID
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# 了解用户ID {#understanding-user-ids}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

从概念上讲，启动授权流程的每个用户都与单个唯一的用户ID关联。 但是，在授权流程中，一个用户ID可以通过不同的方式显示，具体取决于您从哪个API获取该ID。

的 `sessionGUID` 短媒体令牌是用户ID的安全形式，可通过 `sendTrackingData()` 呼叫。 在所有当前集成中，这是跨时间和设备的用户的永久GUID。 GUID的源以来自MVPD的身份验证响应中的用户ID开头。 但是，某些MVPD将来可能会改变主意，开始发送临时GUID。 如果程序员希望确保AuthN响应中的MVPD源用户ID是永久性的，则他们应在与MVPD的协议中安排该ID。

以下是用户ID在Adobe Primetime身份验证API中的不同显示方式：

| 属性 | 用途 | 哈希 | 数字签名 | 描述 |
| --- | --- | --- | --- | --- |
| sendTrackingData()GUID属性 | 跟踪/分析 | 是 | 否 | - MVPD用户ID，由Adobe经过哈希处理。 用户ID无法追溯到源MVPD。 </br> </br>  — 此形式的ID未进行数字签名，因此无法安全防范欺诈。 但是，它对于Analytics是足够好的。  </br> </br>  — 在Adobe Primetime身份验证在AuthN/AuthZ流中生成的所有事件上，客户端提供了此形式的用户ID。 |
| 短媒体令牌的sessionGUID属性 | 并发使用的欺诈跟踪 | 是 | 是 |  — 此ID与通过sendTrackingData()的用户ID相同，但是，此ID经过数字签名以保护其完整性，并且非常适合用于欺诈跟踪。 </br> </br>  — 在使用我们的验证器库后，将在服务器端处理该数据流，在将视频流发布到客户端之前，可以对其进行欺诈模式分析。  要完成这些任务，都由程序员来决定。 |
| getMetadata()userID属性 | 与MVPD的帐户关联、欺诈调查 | 否 | 否 |  — 此属性允许Adobe向程序员公开实际的源MVPD用户ID。 </br> </br>  — 在Adobe的配置中，可以将其设置为加密或不加密（具体取决于MVPD首选项）。 如果加密了，则将使用程序员证书中提供给Adobe的公钥对其进行加密，以便不会向客户端明确显示该密钥。 </br> </br>  — 这会向程序员提供MVPD中的实际用户ID，因此它可直接用于与MVPD进行帐户关联或欺诈调查。 |


**最后**

* 通常，MVPD会提供永久唯一ID <u>并在成功验证后将其传递到Adobe</u>. 它在所有网络中都是一致的。 Comcast MVPD是例外，它为每个渠道提供不同的用户ID。

* MVPD用户ID不包含PII，也不是帐号。 由于我们已与所有MVPD一起验证没有发送PII的信息，因此无需以加密形式公开该信息。

用户ID的使用方式取决于用例：

* 如果您需要它进行跟踪/分析，最实际的位置是从 `sendTrackingData()`.
* 如果需要在服务器端获取流发布、欺诈或操作数据，可以从媒体令牌验证器获取该数据。
* 如果您需要它来关联帐户和进行更深入的欺诈，请咨询您的Adobe联系人以获取相关信息。

