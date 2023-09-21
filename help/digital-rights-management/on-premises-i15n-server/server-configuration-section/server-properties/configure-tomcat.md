---
title: 配置Tomcat
description: 配置Tomcat
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 配置Tomcat{#configure-tomcat}

在Individualization Server上，修改Tomcat的 [!DNL conf/server.xml] 文件，以在访问日志中包含其他信息。 您可以将此信息用于报告目的。

1. 查找的配置 `AccessLogValve` 在 [!DNL server.xml] 并修改该模式，如下所示：

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` 将记录 `x-forwarded-for` 标题。 如果您使用Apache反向代理将请求转发到Tomcat服务器，则此标头将包含原始客户端的IP地址，而 `%h` 记录Apache服务器的IP地址。 `%{request-id}r` 将记录请求标识符，该标识符与个性化应用程序日志中包含的请求ID相对应。

1. 编辑 [!DNL conf/server.xml] 并设置 `unpackwars` 属性设置为false。

   对于“个性化”和“密钥生成”服务器，最好编辑一下 [!DNL conf/server.xml] 并设置 `unpackwars` 属性至 `false`. 否则，当您更新WAR时，可能还必须清除解压缩的WAR文件夹。

>[!NOTE]
>
>将来的DRM客户端将要求您启用并配置可用于Tomcat的CORS（跨源资源共享）过滤器。 目前，没有任何DRM客户端具有此要求。
