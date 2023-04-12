---
title: 确定受保护的资源
description: 确定受保护的资源
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# 确定受保护的资源 {#identifying-protected-resources}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 概述 {#overview}

每个授权请求（或检查授权的请求）必须包含用户请求访问的受保护资源的唯一标识符。 受保护的资源可以是任何级别的授权内容，这是MVPD与参与的程序员之间达成的协议。 潜在的受保护资源必须适合这种越来越具体的粒度的树结构：

- 网络
   - 渠道
      - 显示
         - 剧集
            - 资产\
                

</br>

## 媒体RSS格式 {#media_rss}

资源可以通过简单字符串（渠道的唯一标识符）进行标识，或者可以按照Adobe(或Adobe Primetime身份验证授权合作伙伴)与参与的MVPD和程序员之间的协议，以Media RSS格式(MRSS)表示。 用作资源说明符的RSS字符串可以包含其他信息，如评级和家长控制元数据。\
 

如果您使用简单的资源标识符（如“TNT”），则假定它表示一个渠道，并被转换为以下RSS资源说明符：

```RSS
    <rss version="2.0"> 
        <channel>
            <title>TNT</title>
        </channel>
    </rss>
```
 

比如，更复杂的说明符可能包括其他评级信息。 您可以将整个RSS字符串传递到需要资源ID的Access Enabler函数，例如 [`getAuthorization()`](/help/authentication/rest-api-reference.md):

```rss
    var resource = 
        '<rss version="2.0" xmlns:media="http://search.yahoo.com/mrss/"> 
             <channel>
                 <title>TNT</title>
                 <media:rating scheme="urn:mpaa">pg</media:rating>
             </channel>
         </rss>'; 
    getAuthorization(resource);
```

资源说明符对Adobe Primetime身份验证不透明；它们只是被传递到MVPD。 如果MVPD无法识别或无法解析您的资源说明符，则会向Adobe Primetime身份验证返回错误，该错误会将错误传递回您的 `tokenRequestFailed()` 回调。

<!--
## Related Information {#related}

-  User Metadata
-  Preflight Authorization
-->