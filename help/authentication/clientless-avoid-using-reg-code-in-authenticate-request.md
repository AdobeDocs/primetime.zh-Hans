---
title: 避免在/authenticate请求中使用'&'reg_code
description: 避免在/authenticate请求中使用'&'reg_code
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 避免在/authenticate请求中使用&#39;&amp;&#39;reg_code {#clientless-avoid-using-reg_code-in-authenticate-request}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>



## 问题

IE 9浏览器将“\®”解释为特殊命令，并将其转换为®。 

## 说明

如果 `/authenticate` 请求的组成如下所示……

 

```
    <FQDN>authenticate? requestor_id=someRequestor&reg_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

...它将由IE浏览器（如下所示）进行解释，并将以以下格式发送到Adobe:

 

```
    <FQDN>authenticate?requestor_id=someRequestor&reg;_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

请求者\_id将被解释为univision®\_code=EKAFMFI，因为不存在“&amp;”，并且Adobe将找不到 `regCode` 参数将令牌与关联。  可能根本无法创建AuthN令牌，在这种情况下 `/checkauthn` 调用将无法找到任何令牌。



## 解决方案

以下选项之一应该可以解决此问题：

1. 避免使用 `&reg_code` 参数之间的其他查询字符串参数。  请改为将其移动到请求URL中的第一个查询字符串参数，从而使请求URL如下所示：\
    

       &lt;fqdn>authenticate?reg_code =EKAFMFI&amp;requestor_id=someRequestor&amp;domain_name=someRequestor.com&amp;noflash=true&amp;mso_id=someMvpd&amp;redirect_url=someRequestor.redirect.url.html
   

   这样， `&reg` 参数将不会被错误解释。

1. 标准化 `&reg_code` 使用 `&amp;reg_code`.

1. 如果AuthN令牌创建失败，Adobe可能会引入新功能，以响应身份验证调用将错误代码发送回第2个屏幕。

