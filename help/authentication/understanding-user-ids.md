---
title: 了解用户ID
description: 了解用户ID
exl-id: 813a8501-db72-4850-a387-c8db6120db80
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# 了解用户ID {#understanding-user-ids}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

从概念上讲，启动权利流的每个用户都与一个唯一的用户ID相关联。 但是，在权利流的过程中，可以根据您从哪个API获取用户ID，以不同的方式呈现该用户ID。

此 `sessionGUID` 短媒体令牌是用户ID的安全形式，可通过 `sendTrackingData()` 呼叫。 在所有当前的集成中，这是用户在不同时间和不同设备上的永久GUID。 GUID的源以来自MVPD的身份验证响应中的用户ID开头。 但是，一些MVPD可能会在未来改变主意，并开始发送临时GUID。 如果程序员希望确保AuthN响应中的MVPD源用户ID是永久性的，他们应在与MVPD签订的协议中对此进行安排。

以下是在Adobe Primetime身份验证API中表示用户ID的不同方式：

| 属性 | 用途 | 经过哈希处理 | 数字签名 | 描述 |
| --- | --- | --- | --- | --- |
| sendTrackingData() GUID属性 | 跟踪/分析 | 是 | 否 | - MVPD用户ID，按Adobe进行哈希处理。 用户ID无法回溯到MVPD的源位置。 </br> </br>  — 此形式的ID未经数字签名，因此对于防欺诈而言并不安全。 但是，它对于分析来说足够好。  </br> </br>  — 此形式的用户ID在Adobe Primetime身份验证在AuthN/AuthZ流中生成的所有事件的客户端提供。 |
| 短媒体令牌的sessionGUID属性 | 对并发使用情况的欺诈跟踪 | 是 | 是 |  — 这与通过sendTrackingData()的用户ID相同，但是，此ID经过数字签名以保护其完整性，并且足以用于欺诈跟踪。 </br> </br>  — 此视频流将在使用我们的验证器库后在服务器端进行处理，并可在向客户端释放视频流之前对欺诈模式进行分析。  这些任务中的任何一个都由程序员来完成。 |
| getMetadata() userID属性 | 帐户关联、与MVPD的欺诈调查 | 否 | 否 |  — 此属性允许Adobe向程序员公开实际的源MVPD用户ID。 </br> </br>  — 在Adobe的配置中，可以将其设置为加密或不加密（取决于MVPD首选项）。 如果已加密，则使用提供给Adobe的程序员证书中的公钥进行加密，因此客户端不会清楚地看到该密钥。 </br> </br>  — 这将为程序员提供MVPD中的实际用户ID，因此它可用于直接与MVPD进行帐户关联或欺诈调查。 |


**总结**

* 通常，MVPD会提供一个永久的唯一ID <u>并在成功进行身份验证后将其传递给Adobe</u>. 它通常在所有网络中都是一致的。 Comcast MVPD例外，它为每个渠道提供不同的用户ID。

* MVPD用户ID不包含PII，它不是帐号。 它不需要以加密形式公开，因为我们已通过所有MVPD验证未发送任何PII。

用户ID的使用方式取决于用例：

* 如果您需要它来进行跟踪/分析，最实用的方法就是从获取 `sendTrackingData()`.
* 如果在服务器端需要流发布、欺诈或操作数据的数据，则可以从媒体令牌验证器中获取该数据。
* 如果您需要它来关联帐户和进行更深入的欺诈，请与您的Adobe联系人联系以获取可用性。
