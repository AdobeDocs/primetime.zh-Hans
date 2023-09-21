---
title: 示例客户端请求
description: 示例客户端请求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 示例客户端请求{#sample-client-requests}

您可以使用Charles Proxy或Wireshark等工具收集示例客户端请求库。 您应使用个性化传输凭据在设置个性化服务器后捕获客户端请求。 然后，您可以发送这些客户端请求(通过 *curl* 或其他工具)，以验证服务器是否已启动并正常运行。 例如：

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

您还可以在任何服务器配置更改或ECI/CRL更新后再次发送这些请求。

您还应该使用成功的个性化事务相应地更新“个性化统计信息”页面。
