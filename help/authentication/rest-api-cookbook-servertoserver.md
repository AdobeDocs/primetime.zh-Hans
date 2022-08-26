---
title: REST API指南（服务器到服务器）
description: 将REST API指南服务器发送到服务器。
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 0%

---


# REST API指南（服务器到服务器） {#rest-api-cookbook-server-to-server}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。


## 概述 {#overview}

本指南文档旨在详细介绍使用服务器到服务器体系结构实施Adobe Primetime身份验证的最佳实践。  它提供了基本要求、分步流实施以及生产环境和操作的一般注意事项。

 

## 组件 {#components}

在工作的服务器到服务器解决方案中，涉及以下组件：

 
|类型 |组件 |描述 | | — | — | — | |流设备 |流应用程序 |驻留在用户流设备上并播放经过验证的视频的程序员应用程序。 | | | \[可选\] AuthN模块 |如果流设备具有用户代理（即Web浏览器），则AuthN模块负责在MVPD IdP上对用户进行身份验证。 | | \[可选\] AuthN设备 | AuthN应用程序 |如果流设备没有用户代理（即Web浏览器），则AuthN应用程序是使用Web浏览器从单独用户设备访问的程序员Web应用程序。 | |程序员基础架构 |程序员服务 |将流设备与Adobe Pass服务链接以获取身份验证和授权决策的服务。 | |Adobe基础架构 | Adobe Pass服务 |与MVPD IdP和AuthZ服务集成并提供身份验证和授权决策的服务。 | | MVPD基础架构 | MVPD IdP |提供基于凭据的身份验证服务以验证其用户身份的MVPD端点。 | | | MVPD AuthZ服务 | MVPD端点，根据用户的订阅、家长控制等提供授权决策。 |


流程中使用的其他术语在
[术语表](http://tve.helpdocsonline.com/adobe-pass-glossary).

## 流量 {#flows}

### 动态客户端注册(DCR)


Adobe Pass使用DCR保护程序员应用程序或服务器与Adobe Pass服务之间的客户端通信。 DCR流是独立的、从属的和先决条件的流，可在此处找到：http://tve.helpdocsonline.com/dynamic-client-registration


### 身份验证(authN)

验证流程用于允许用户在其MVPD中标识自己，以确定用户是否具有有效帐户。 

1. 用户启动流设备应用程序，并尝试登录或查看受保护的内容。
2. 流设备应用程序向程序员服务发出请求，以确定设备是否已经过验证。
3. 程序员服务使用DCR注册应用程序。
4. 程序员服务通过调用Adobe Pass服务来检查流设备authN状态 **checkauthn** API。
5. 对于 **checkauthn** 调用会返回用户设备已验证的状态，然后应用程序可以继续进入授权流程。
6. 对于 **checkauthn** 调用会返回用户设备未通过身份验证的状态，然后应用程序应等待用户请求登录。
7. 当用户请求直接登录（例如选择登录按钮）或间接登录（例如，当未经验证时选择受保护的内容）时，流设备应用程序向程序员服务发出请求以启动用户验证。 程序员服务通过调用Adobe Pass服务请求并接收唯一注册代码(regcode) **regcode** API。
8. 程序员服务还通过调用Adobe Pass服务来检索当前MVPD和属性的列表 **配置** API。 注意：此API也可以在流程中提前调用并缓存。
9. 程序员服务将重编码返回到流设备应用程序，以及步骤\#7中请求的已处理MVPD列表。 注意：已处理的MVPD列表格式由程序员指定，并可进行筛选以明确允许或阻止特定的MVPD（即允许或阻止列表）。
10. 如果与AuthN设备不同(例如，“第二屏幕”)，则流设备应显示重编码和URI，供用户访问AuthN应用程序。 用户在AuthN设备上的用户代理中键入URI以启动AuthN应用程序，然后将重编码键入该应用程序。 如果流设备与AuthN设备相同，则可以通过编程方式将重编码传递到AuthN模块。
11. AuthN模块通过显示MVPD选取器，通过MVPD启动用户身份验证。 用户选择MVPD后，将调用AuthN模块 **身份验证** ，用于将用户代理重定向到MVPD IdP。 当用户通过MVPD成功进行身份验证时，用户代理将通过Adobe Pass服务重定向回，在该服务中，成功的身份验证会通过regcode进行记录，然后被重定向回AuthN模块。
12. 如果流设备与AuthN设备不同，则AuthN设备应向用户显示成功的身份验证消息以及要继续的步骤(例如，“成功\! 您现在可以返回游戏控制台以继续\[...\]”)。 如果流设备与AuthN设备相同，则流设备可以采用编程方式检测身份验证完成情况。

 

下图说明了身份验证流程：

### ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/image\(13\)。png)

### 授权(authZ)

授权流程用于确定用户是否有权访问所请求的内容。

1. 每次用户尝试在流设备应用程序上查看受保护的内容时，流设备应用程序都会调用程序员服务来识别内容，并请求启动流所需的权限和信息。
2. 程序员服务称为Adobe Pass **授权** 传递资源ID的API以及其他必需参数。 Adobe服务会使用资源ID调用MVPD AuthZ服务，并接收和授权决定，然后将该决定传递回程序员服务。 此授权决策将由Adobe Pass服务缓存一段可配置的时间。 在后续 **授权** 从程序员服务调用Adobe Pass服务时，只要缓存的值有效，就会返回该缓存值。
3. 如果授权被授予，程序员服务应调用Adobe Pass /**令牌/媒体** API，将返回已签名的媒体令牌。 程序员服务应使用媒体令牌验证器库(JAR)验证媒体令牌。 如果有效，程序员服务应返回在步骤\#1中请求的启动流（例如流URL）所需的权限和权限。
4. 如果拒绝授权，则 **授权** 调用将向程序员服务返回错误代码和说明。 程序员服务应将错误代码和描述（或程序员修改消息）返回到步骤\#1中的请求。

 

下图说明了授权流程：

### ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/image\(14\)。png)

### 注销

注销流程允许用户删除当前与应用程序关联的身份。

1. 当用户请求注销（即从设备中删除与应用程序关联的当前MVPD帐户）时，流设备应用程序会调用程序员服务来通知它注销设备。
2. 程序员服务应将Adobe Pass **注销** API。

下图说明了注销流程：

 

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/image\(15\)。png)

 

### \[可选\]预授权（也称为飞行前）

预授权可用于从一组资源快速确定用户可能拥有的资源。  此调用的结果通常用于为单个用户自定义UI。

1. 一旦用户被认证，流式装置可调用程序员服务以请求用户有权流到的内容。
2. 程序员服务应将Adobe Pass **预授权** 包含资源ID列表的API，资源ID是一个简单的字符串，通常表示用户有权流式传输的渠道。 *注意：目前，* ***预授权*** *调用配置为将列表限制为五(5)个资源ID。 当需要5个以上的资源时，多个* ***预授权*** *可以进行调用，或者可以将调用配置为接受来自MVPD的协议超过五个资源。 实施者应牢记* ***预授权*** *调用MVPD资源以及向程序员响应的时间，并审慎地构建其调用的使用结构。*
3. 的 **预授权** 调用将使用JSON对象对程序员服务做出响应，该对象在请求中包含每个资源ID的TRUE或FALSE值，以指示用户是否有权访问关联的渠道。 *注意：如果MVPD未为给定的资源ID提供答案（例如，由于网络错误或超时），则该值将默认为FALSE。*
4. 程序员服务应使用 **预授权** 调用响应以创建程序员定义的对流设备的自定义响应，通常根据用户的授权将演示个性化给用户。

下图说明了预授权流程：

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/image\(16\)。png)

 

### \[可选\]元数据

元数据可用于检索MVPD共享的用户信息。
 例如，用户ID、邮政编码等。

1. 用户经过身份验证后，程序员服务可以调用Adobe Pass **用户元数据** 用于请求有关已验证用户的信息的API。
2. 响应将包含给定用户可用的所有元数据。 为每个程序员/MVPD集成分别配置特定字段。

下图说明了预授权流程：

 

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/image\(17\)。png)

 

## 环境和功能要求{#environments}

 

程序员应至少创建两个环境：一个用于生产，一个或多个用于暂存。


### 生产

生产环境应当具有高可用性，并且可以针对较大或意外的尖峰（例如，实时体育、突发新闻）进行适当缩放。

 

Adobe Pass服务在地理上分散在美国各地的多个数据中心上运行。  为了从Adobe Pass服务中获得最佳响应时间（即最短的延迟），程序员还应创建一个地理上分散的类似服务基础结构。 


程序员服务应将DNS缓存限制为最多30秒，以防Adobe需要重新路由流量。 如果数据中心变得不可用，则可能会发生这种情况。\
 

程序员应提供生产环境的公共IP范围。 这些IP将输入到Adobe Pass基础架构中的允许列表中，以便进行访问，并由Adobe的公平API使用策略进行管理。

### 暂存

暂存环境可以是最小的，但应包括所有系统组件和业务逻辑。 它的功能应与生产类似，并允许在生产环境之外测试版本。 理想情况下，暂存环境可以连接到Adobe Pass测试环境，以供程序员使用，并在需要时通过Adobe进行连接，以便我们能够协助测试和疑难解答。

### 功能要求

程序员服务必须传递他们正在执行流的设备的准确设备标识信息。 此外，程序员服务必须传递其正在执行流的设备的IP（在x-forwarded-for头中）以及连接源端口（在设备信息字段中）：

    **X-Forwarded-For :\&lt;client _ip=&quot;&quot;>** 
    
    where \&lt;client _ip=&quot;&quot;> 是客户端公共IP地址
    
     
    
    需要在**regcode**和**授权**调用中添加标头
    
    示例：
    
    POST/reggie/v1/{req\_id}/regcode HTTP/1.1
    
    X-Forwarded-For:203.45.101.20
    
     
    
    GET/api/v1/授权HTTP/1.1
    
    X-Forwarded-For:203.45.101.20

 

程序员服务应发送单个MVPD或集成应用程序(例如设备IP、源端口、设备信息、MRSS、可选数据（例如ECID）所需的数据和格式。 请参阅相关文档 [传递设备和连接信息指南](http://tve.helpdocsonline.com/passing-device-information-cookbook).


当收到通知时，程序员服务必须遵循authN和authZ TTL，才能缓存和使authN或authZ会话失效。

程序员必须维护与Adobe共享的证书。

</br>

## 相关信息 {#related}

* [REST API引用](http://tve.helpdocsonline.com/registration-code-request)
* [术语表](http://tve.helpdocsonline.com/adobe-pass-glossary)
