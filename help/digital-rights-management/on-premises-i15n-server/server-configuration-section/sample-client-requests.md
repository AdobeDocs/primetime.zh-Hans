---
seo-title: 客户端请求示例
title: 客户端请求示例
uuid: 330d5e3c-1711-4375-bd11-e7702f0cde31
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 客户端请求示例{#sample-client-requests}

您可以使用Charles Proxy或Wireshark等工具收集示例客户端请求库。 在设置个性化服务器后，您应使用个性化传输凭证来捕获客户端请求。 然后，您可以(通过 *curl* 或其他工具)将这些客户端请求发送到个性化服务器的端点，以验证服务器是否已正常启动和运行。 例如：

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

您可能还希望在任何服务器配置更改或ECI / CRL更新后再次发送这些请求。

您还应当使用成功的个性化事务相应地更新“个性化统计信息”页。
