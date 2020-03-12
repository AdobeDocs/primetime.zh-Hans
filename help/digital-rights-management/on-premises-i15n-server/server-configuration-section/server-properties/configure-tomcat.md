---
seo-title: 配置Tomcat
title: 配置Tomcat
uuid: 5f23aa33-29d7-4b41-87a4-59dc5b433de4
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 配置Tomcat{#configure-tomcat}

在个性化服务器上，修改Tomcat的文 [!DNL conf/server.xml] 件，以在访问日志中包含其他信息。 您可以将此信息用于报告用途。

1. 找到中的配置 `AccessLogValve` 并 [!DNL server.xml] 修改模式，如下所示：

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` 将记录标题的 `x-forwarded-for` 值。 如果使用Apache反向代理将请求转发到Tomcat服务器，则此头将包含原始客户端的IP地址，而 `%h` 记录Apache服务器的IP地址。 `%{request-id}r` 将记录请求标识符，该标识符与个性化应用程序日志中包含的请求ID相对应。

1. 编 [!DNL conf/server.xml] 辑并将属 `unpackwars` 性设置为false。

   对于个性化和密钥生成服务器，最好编辑属性 [!DNL conf/server.xml] 并将其设 `unpackwars` 置为 `false`。 否则，在更新WAR时，您可能也必须清除未打包的WAR文件夹。

>[!NOTE]
>
>将来的DRM客户端将要求您启用和配置可用于Tomcat的CORS（跨源资源共享）过滤器。 目前，没有DRM客户端具有此要求。

