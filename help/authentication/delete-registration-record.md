---
title: 删除注册记录
description: 删除注册资源
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 删除注册记录 {#delete-registration-record}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## REST API端点 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生产 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暂存 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生产 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暂存 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## 描述 {#delete-record}

删除注册代码记录并释放注册代码以供重复使用。 

| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>例如：</br></br>&lt;reggie_fqdn>/reggie/v1/regcode/ER45RTY | 流应用程序</br></br>或</br></br>程序员服务 | 1.请求者ID  </br>    （路径组件）</br>2.  注册代码  </br>    （路径组件） | DELETE | 无 | 204 |

{style="table-layout:auto"}

</br>

| 输入参数 | 描述 |
| --- | --- |
| 请求者 | 此操作有效的程序员请求者ID。 |
| 注册码 | 将在流设备上显示的注册代码值（要输入到验证流程中）。 |

{style="table-layout:auto"}

</br>

### [返回到REST API引用](/help/authentication/rest-api-reference.md)
