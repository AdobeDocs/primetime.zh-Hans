---
title: 在iOS上重置Temp Pass
description: 在iOS上重置Temp Pass
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# 在iOS上重置Temp Pass {#reset-temp-pass-on-ios}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

iOS演示应用程序包括用于重置临时传递TTL的专用屏幕。 重置操作需要以下信息：

- **环境：** 指定将接收重置Temp Pass网络调用的AdobePay-TVpass服务器端点。 可能值： **普雷夸尔** (*mgmt-prequal.auth-staging.adobe.com*)、 **版本** (*mgmt.auth.adobe.com*)或 **自定义** (保留用于Adobe内部测试)。
- **OAuth2载体令牌：** 授权程序员进行Adobe付费电视身份验证时，需要使用OAuth2令牌。 此类令牌可以从专用付费电视身份验证OAuth2端点(例如， *curl -u &quot;\&lt;consumer _key=&quot;&quot;>:\&lt;consumer _secret=&quot;&quot; _key=&quot;&quot;>*&quot; *&quot;https://mgmt.auth.adobe.com/oauth2/permanent\_accesstoken?grant\_type=client\_credentials&quot;*)。
- **请求者ID:** 当前程序员的唯一ID。 此值从演示应用程序的主屏幕（请求者字段）中读取。
- **临时传递ID:** 临时传递MVPD的唯一ID。
- **设备ID:** 由演示应用程序计算的经过哈希处理的设备ID。
- **一般密钥：** 某些Temp Pass MVPD（即下一个可扩展的Temp Pass功能）支持用于重置Temp Pass的通用密钥（与设备ID一起）。

所有上述参数( *通用键*)是必填项。 以下是将由演示应用程序执行的参数和关联的网络调用示例（示例以*curl *command的形式）：

- **环境：** 版本(*mgmt.auth.adobe.com*)
- **OAuth2载体令牌：** H4j7cF3GtJX81BrsgDa10GwSizVz
- **程序员ID:** 参考
- **临时传递ID:** TempPassREF
- **设备ID:** f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991 
- **一般密钥：** null（未提供值）

```curl
curl -X DELETE -H "Authorization:Bearer* *H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991&requestor_id=REF&mvpd_id=TempPassREF"
```

DELETEHTTP请求将发送给 **/reset** 端点，传递 *OAuth2载体令牌* 和 *设备ID*, *请求者ID* 和 *临时传递ID(MVPD ID)* 作为参数。

如果程序员为 *通用键*，将执行另一个HTTP调用(此时 **/reset/generic** 端点)，传递 *通用键* 内部 *key* 请求参数。

例如，将 *通用键* 对于临时传递MVPD（支持此类功能）的电子邮件地址哈希，将产生以下HTTP调用(电子邮件为 `user@domain.com` 其SHA-256哈希为 `f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7`):

```curl
curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz"
"https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=TempPassREF"
```

必须强调的是，在演示应用程序中重置Temp Pass可能对同一设备上的程序员应用程序没有相同的效果。 这是因为设备ID（由演示应用程序和AccessEnabler计算）可能与设备上所有应用程序的ID不同：

- iOS 6及以下版本：设备ID是使用MAC地址计算的（对于所有应用程序而言，该地址都是唯一的），因此在演示应用程序中重置Temp Pass将在设备上的所有其他程序员应用程序中重置它。

- iOS 7及更高版本：设备ID是基于IDFV（供应商的ID）值计算的，对于具有相同捆绑ID前缀（即除最后一个组件外的所有组件）的所有应用程序而言，IDFV（供应商的ID）值是唯一的。 由于演示应用程序和程序员应用程序具有不同的捆绑ID，因此在演示应用程序中重置临时传递对程序员应用程序没有影响。

最后一个用例(iOS 7及更高版本)最常见，因此，让我们看看程序员在这种情况下如何为其应用程序重置Temp Pass。 有以下几个选项：

1. 将代码从演示应用程序端口到程序员应用程序。 的 *TempPassResetViewController* 和 *DeviceIdDemoApp* 类包含用于重置Temp Pass的核心逻辑，并且可以轻松地修改这些逻辑并将其包含在程序员应用程序中。

1. 执行HTTP请求以通过重置Temp Pass *卷曲*. 可以通过计算程序员应用程序的IDFV并对其应用SHA-256哈希( *DeviceIdDemoApp* 类)。

1. 只需通过将程序员应用程序的哈希IDFV指定为 *通用键*. 这将产生两个网络调用：一个用于为演示应用程序重置Temp Pass（与程序员无关），另一个用于为程序员应用程序重置Temp Pass。

以上所有选项都是相似的，需由程序员根据实施的方便程度来选择。 

