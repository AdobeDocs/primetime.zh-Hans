---
title: 启动身份验证
description: 启动身份验证
source-git-commit: 0839e9f2eac7eeeadf9bbfafb2bdd76596f4fb06
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 启动身份验证 {#initiate-authentication}

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


## 描述 {#description}

通过通知MVPD选择事件来启动身份验证过程。 在Primetime身份验证数据库上创建记录，当从MVPD收到成功响应时进行协调。 



| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate | AuthN模块 | 1.requestor_id（必填）</br>2.  mso_id（必填）</br>3.  reg_code（必填）</br>4.  domain_name（必填）</br>5.  noflash=true -  </br>    （必需，剩余参数）</br>6.  no_iframe=true（必需，残留参数）</br>7.  额外参数（可选）</br>8.  redirect_url（必填） | GET | 登录Web应用程序将被重定向到MVPD登录页面。 | 302，用于完整重定向实施 |

{style=&quot;table-layout:auto&quot;}


| 输入参数 | 描述 |
| --- | --- |
| requestor_id | 此操作有效的程序员请求者。 |
| mso_id | 此操作有效的MVPD ID。 |
| reg_code | 雷吉公司生成的注册码。 |
| domain_name | 原始域。 |
| redirect_url | 身份验证完成后的登录Web应用程序重定向url。 |

{style=&quot;table-layout:auto&quot;}

</br>

>[!IMPORTANT]
> 
>**重要信息：必需参数 —** 无论客户端实施如何，上述所有参数都是必需的。
>
>
>示例：    
>
>
```
>domain_name=loginwebapp.com
>mso_id=sampleMvpdId
>reg_code=RO0885W
>requestor_id=sampleRequestorId
>noflash=true
>redirect_url=http://loginwebapp.com
>```

>[!IMPORTANT]
> 
>**重要信息：可选参数**
>
>调用还可以包含可启用其他功能(如：
>
> * generic\_data — 允许使用 [促销TempPass](https://tve.helpdocsonline.com/promotional-temp-pass)
>
>```JSON
>Example:
>   generic_data=("email":"email@domain.com")
>```


### **注释** {#notes}

* 的值 `domain_name` 参数必须设置为在Primetime身份验证中注册的域名之一。 有关更多详细信息，请参阅 [注册和初始化](http://tve.helpdocsonline.com/new-programmer-overview$reg_and_init).

* [避免在/authenticate请求中使用&#39;&amp;&#39;reg\_code（技术说明）](https://tve.helpdocsonline.com/clientless:-avoid-using-&#39;&amp;&#39;reg_code-in-/authenticate-request)

* 的 `redirect_url` 参数必须是按顺序排列的最后一个参数

* 的值 `redirect_url` 参数必须为URL编码

[返回到REST API引用](http://tve.helpdocsonline.com/rest-api-reference)
