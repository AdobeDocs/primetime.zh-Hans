---
title: 客户端请求示例
description: 客户端请求示例
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# 客户端请求示例{#sample-client-requests}

您可以使用Charles Proxy或Wireshark等工具收集示例客户端请求库。 在设置个性化服务器后，您应使用个性化传输凭据来捕获客户端请求。 然后，您可以将这些客户端请求（通过&#x200B;*curl*&#x200B;或其他工具）发送到个性化服务器的端点，以验证服务器是否已启动并正常运行。 例如：

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

您还可能希望在任何服务器配置更改或ECI / CRL更新后再次发送这些请求。

您还应使用成功的个性化事务处理相应地更新“个性化统计信息”页。
