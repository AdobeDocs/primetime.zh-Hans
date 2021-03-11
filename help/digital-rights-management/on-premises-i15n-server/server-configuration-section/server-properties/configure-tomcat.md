---
title: 配置Tomcat
description: 配置Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# 配置Tomcat{#configure-tomcat}

在个性化服务器上，修改Tomcat的[!DNL conf/server.xml]文件，以在访问日志中包含其他信息。 您可以将此信息用于报告。

1. 在[!DNL server.xml]中找到`AccessLogValve`的配置，并修改以下模式：

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` 将记录标题的 `x-forwarded-for` 值。如果使用Apache反向代理将请求转发到Tomcat服务器，则此标头将包含原始客户端的IP地址，而`%h`将记录Apache服务器的IP地址。 `%{request-id}r` 将记录请求标识符，该标识符与“个性化”应用程序日志中包含的请求ID相对应。

1. 编辑[!DNL conf/server.xml]并将`unpackwars`属性设置为false。

   对于个性化服务器和密钥生成服务器，最好编辑[!DNL conf/server.xml]并将`unpackwars`属性设置为`false`。 否则，在更新WAR时，您可能也必须清除未打包的WAR文件夹。

>[!NOTE]
>
>将来的DRM客户端将要求您启用和配置可用于Tomcat的CORS(跨来源资源共享)筛选器。 目前，没有DRM客户端具有此要求。

