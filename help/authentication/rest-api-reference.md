---
title: REST API引用
description: Rest api引用
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 3%

---


# REST API引用 {#rest-api-reference}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 响应格式 {#response-formats}


>[!NOTE]
>
> 这些服务中提供的API可以以XML或JSON格式返回响应（对于返回响应的API）。 在请求中指定响应格式的方法有3种：
>* 将HTTP接受标头设置为“application/xml”</code>”或“application/json”</code>&quot;
>* 在请求有效负载中，指定参数“format=xml”</code>&quot;或&quot;format=json</code>&quot;</li>
>* 使用扩展名.xml调用Web服务端点</code> 或.json</code>. 例如，“/regcode.xml</code>&quot;或&quot;/regcode.json&quot;</code>&quot;
>
>您可以指定上述任一方法。 指定格式冲突的多种方法可能会导致错误或不期望的输出。

## REST API端点 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生产 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暂存 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生产 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暂存 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## Web服务摘要 {#web_srvs_summary}

下表列出了适用于无客户端方法的可用Web服务。 单击Web服务端点以了解更多信息（示例请求和响应、输入参数、HTTP方法等）


| Sr | Web服务端点 | 描述 | [迪亚格。  </br>参考](http://tve.helpdocsonline.com/api-reference-v2-test#illustration). | 托管位置 | 调用者 |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode](http://tve.helpdocsonline.com/registration-code-request) | 返回随机生成的注册代码和登录页面URI | 2 | Adobe  </br>注册代码服务 | 智能设备 |
| 2. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/return-registration-record) | 返回包含注册代码UUID、注册代码和经过哈希处理的设备ID的注册代码记录 | 8 | Adobe  </br>注册代码服务 | Primetime身份验证 |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestorId}](http://tve.helpdocsonline.com/provide-mvpd-list) | 返回请求者已配置的MVPD列表 | 5 | Adobe  </br>Primetime  </br>身份验证  </br>服务 | 登录  </br>Web  </br>应用程序 |
| 4. | [&lt;sp_fqdn>/api/v1/authenticate](http://tve.helpdocsonline.com/initiate-authentication) | 通过通知MVPD选择事件启动AuthN进程。 在验证数据库上创建记录，当从MVPD收到成功响应时，该记录将进行协调（步骤13） | 7 | Adobe  </br>Primetime  </br>身份验证  </br>服务 | 登录  </br>Web  </br>应用程序 |
| 5. | SAML断言使用者 | Primetime身份验证和MVPD之间的现有SAML工作流 | 13 | Primetime  </br>身份验证  </br>服务 | Primetime身份验证 |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](http://tve.helpdocsonline.com/check-authentication-flow-by-second-screen-web-app) | 登录Web应用程序可以检查尝试的登录流程是否成功 |  | Primetime  </br>身份验证   </br>服务 | 登录   </br>Web   </br>应用程序 |
| 7. | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | 获取与AuthN令牌相关的元数据 | 15 | Primetime  </br>身份验证  </br>服务 | 智能设备 |
| 8. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/delete-registration-record) | 删除注册代码记录并释放注册代码以供重复使用 | 16 | Adobe  </br>注册代码服务 | Primetime身份验证 |
| 9. | [&lt;sp_fqdn>/api/v1/authorize](http://tve.helpdocsonline.com/initiate-authorization) | 获取授权响应。 | 17 | Primetime  </br>身份验证  </br>服务 | 智能设备 |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](http://tve.helpdocsonline.com/check-authentication-token) | 指示设备是否具有未过期的AuthN令牌。 |  | Primetime  </br>身份验证  </br>服务 | 智能设备 |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | 返回AuthN令牌（如果找到）。 |  | Primetime  </br>身份验证  </br>服务 | 智能设备 |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](http://tve.helpdocsonline.com/retrieve-authorization-token) | 返回AuthZ令牌（如果找到）。 |  | Primetime  </br>身份验证  </br>服务 | 智能设备 |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](http://tve.helpdocsonline.com/obtain-short-media-token) | 返回短媒体令牌（如果找到） — 与/api/v1/mediatoken相同 |  | Primetime  </br>身份验证  </br>服务 | 智能设备 |
| 14. | [&lt;sp_fqdn>/api/v1/mediatoken](http://tve.helpdocsonline.com/obtain-short-media-token) | 获取短媒体令牌 |  | Primetime  </br>身份验证  </br>服务 | 智能设备 |
| 15. | [&lt;sp_fqdn>/api/v1/preauthorize](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources) | 检索预授权资源的列表 |  | Primetime  </br>身份验证  </br>服务 | 智能设备 |
| 16. | [&lt;sp_fqdn>/api/v1/preauthorize/{code}](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources-by-way-of-web-app) | 检索预授权资源的列表 |  | Primetime  </br>身份验证  </br>服务 | 登录Web应用程序 |
| 17. | [&lt;sp_fqdn>/api/v1/logout](http://tve.helpdocsonline.com/logout) | 从存储中删除AuthN和AuthZ令牌 |  | Primetime  </br>身份验证   </br>服务 | 智能设备 |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](http://tve.helpdocsonline.com/user-metadata-call) | 在身份验证流程完成后获取用户元数据 | 不适用 | 不适用 | 智能设备 |
| 19. | [&lt;sp_fqdn>/api/v1/authenticate/freepreview](http://tve.helpdocsonline.com/free-preview-for-temp-pass-and-promotional-temp-pass) | 为临时通行证或促销临时通行证创建身份验证令牌 | 不适用 | Primetime  </br>身份验证  </br>服务 | 智能设备 |

{style=&quot;table-layout:auto&quot;}

## REST API安全 {#security}

必须使用HTTPS协议调用所有Primetime身份验证无客户端API，以便进行安全通信。 此外，调用的大多数API都应包含由提供的访问令牌 [动态客户端注册](http://tve.helpdocsonline.com/dynamic-client-registration).


## 相关信息 {#related}

* [REST API概述](http://tve.helpdocsonline.com/reset-api-overview)
* [服务器到服务器指南](http://tve.helpdocsonline.com/server-to-server-cookbook)
* [客户端到服务器指南](http://tve.helpdocsonline.com/client-to-server)
* [避免在/authenticate请求中使用&#39;&amp;&#39;reg\_code（技术说明）](https://tve.zendesk.com/entries/23648011-Clientless-Avoid-using-reg-code-in-authenticate-request)
