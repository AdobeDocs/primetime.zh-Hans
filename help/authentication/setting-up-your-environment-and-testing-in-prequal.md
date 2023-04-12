---
title: 在每季度前设置环境和测试
description: 在每季度前设置环境和测试
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# 在每季度前设置环境和测试{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

本技术说明旨在帮助我们的合作伙伴设置其环境，并开始测试在Adobe资格预审环境中部署的新内部版本。

由于存在两种构建风格： ***生产*** 和 ***暂存***，在本文档中，我们将重点介绍生产设置，并提及所有步骤在暂存方面是相同的，只有URL不同。

步骤1和2在其中一台测试机上设置测试环境，步骤3是对基本流程的验证，步骤4和5介绍一些测试准则。

>[!IMPORTANT]
>
> 每当您想要更改测试环境（从暂存配置文件切换到生产配置文件，或者以其他方式切换到）时，执行步骤1和2非常重要
 

## 步骤1. 解析将域传递到IP {#resolving-pass-domain-to-an-ip}

* 要查找可用于欺骗的负载平衡器IP，请运行以下命令：

* **在Windows上**

   ```cmd
   C:\>nslookup sp-prequal.auth.adobe.com
   ...
   Addresses:  52.13.71.11
               54.184.208.150
   ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **在Linux/Mac上**

```sh
    $ dig sp-prequal.auth.adobe.com
    
    ;; ANSWER SECTION:
    ...
    ............ 60 IN A      52.13.71.11
    ............ 60 IN A      54.184.208.150
```

```Choose any IP from **A records (**e.g `52.13.71.11)```

>[!NOTE]
>
>因为域名不相关，可能因用户而异，因此无法回答相关问题。

>[!IMPORTANT]
>
> 这些IP地址在将来可能会发生更改，对于不同地理区域的用户来说，它们可能不相同。


## 步骤2.  诱使资格预审环境成为生产环境 {#spoofing-the-prequalification-environment}

* 编辑 *c:\\windows\\System32\\drivers\\etc\\hosts* 文件（在Windows中）或 */etc/hosts* 文件（在Macintosh/Linux/Android上）并添加以下内容：

* 假脱机生产配置文件
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Android上的欺骗：** 要在Android上假设，您必须使用Android模拟器。

* 实施欺骗后，您只需为生产和暂存用户档案使用常规URL即可：(即 `http://sp.auth-staging.adobe.com` 和 `http://entitlement.auth-staging.adobe.com` 而你会真的 *资格预审环境/生产* *新内部版本的。


## 步骤3.  验证您是否指向正确的环境 {#Verify-you-are-pointing-to-the-right-environment}

**这是一个简单的步骤：**

* 加载 [权利预定环境](https://entitlement-prequal.auth.adobe.com/environment.html) 和 [权利](https://entitlement.auth.adobe.com/environment.html). 他们应返回相同的响应。


## 步骤4.  使用程序员的网站执行简单的验证/授权流程 {#peform-a-simple-auth-flow}

* 此步骤需要程序员的网站地址和一些有效的MVPD凭据（经过身份验证和授权的用户）。

## 步骤5.  使用程序员网站执行情景测试 {#perform-scenario-testing-using-programmer-website}

* 完成环境设置并确保基本的身份验证授权流程正常工作后，您可以继续测试更复杂的方案。


## 步骤6.  使用API测试网站执行测试 {#perform-testing-using-api-testing-site}

* 如果您想要更深入地测试Adobe Primetime身份验证，我们建议您使用 [API测试网站](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

有关API测试网站的更多详细信息，请访问 [如何使用Adobe的API测试网站测试身份验证和授权流程](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

