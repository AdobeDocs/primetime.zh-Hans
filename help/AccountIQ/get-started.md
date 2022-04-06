---
title: 帐户IQ开始使用帐户IQ、先决条件和入门
description: '如何载入、先决条件以及帐户IQ快速入门。 '
source-git-commit: 258ce10297aa15086a3ed1c1a825af2a30d34d24
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# 如何开始使用帐户IQ {#onboarding}

请阅读并了解使用帐户IQ的先决条件，以及贵公司如何开始查看共享订阅者分数的帐户。

## 先决条件 {#prerequisites}

* 组织必须在中注册 [!DNL Adobe Marketing Cloud] 组织。

* 组织中的用户应被分配到TVE功能板读写或TVE功能板只读。

### 浏览器先决条件 {#browser-prerequisites}

帐户IQ是托管的Web服务。 它与以下浏览器的最新版本兼容：

* Google Chrome
* Mozilla Firefox
* Safari版本

### 如何通过帐户IQ载入组织？ {#steps-to-onboard}


这就是我们现在的情况。 计划删除dma_primetime检查，并为AIQ提供专用配置文件。 需要具有控制台访问权限的用户将需要该用户配置文件。 但目前尚未实施。

1. 将他们的组织载入Adobe Marketing Cloud@Eric或@Peter，您可以接受这个。  我想它现在叫“Experience Cloud”，但那是次要的。  这里有更多细节吗？ 这是否由其他组管理？ 如果是，我们是否提供链接、联系人等？ 此外，还应当包含有关检查其组织是否已包含在Experience Cloud中的注意事项。

2. 将“TVE功能板读写”或“TVE功能板只读”用户档案分配到http://adminconsole.adobe.com/中。
@Eric，你知道怎么做吗？  有子步骤吗？  我们能否向客户解释他们为什么选择“读写”与“只读”？
@Cristina，能否提供一个简短的说明，说明这是一种临时方法，以及它在下一个版本中的工作方式？

3. 在AIQ端将其组织ID列入白名单@Cristina后，是否可以实施一个流程来管理此问题？  例如，使用组织的组织ID向“DL-AdobePass-Eng AdobePass-Eng@adobe.com”发送电子邮件，等等。

<!-- these user groups set dma_primetime product context for the user accounts. In AIQ code we’re checking for this product context when providing access. Internally, in the code we have an additional condition: the org id should be whitelisted in order for the users to get access to their data. -->

访问AdobeEnterprise Dashboard时，您将在Adobe Marketing Cloud组织中看到两个新创建的用户组：

TVE功能板读写 — 该组成员在功能板的所有可编辑部分具有完全权限TVE功能板只读 — 该组成员仅在整个功能板中具有查看权限。请将您的帐户添加到TVE功能板读写用户组、AdobeEnterprise功能板中，然后登录Adobe Primetime TVE功能板。  之后，您将能够在Enterprise Dashboard中通过添加和删除上述两个用户群组中的用户来管理Adobe的用户权限。

...........

在您提供的文档中，有一个名为“Primetime TVE功能板用户配置快速入门”的部分，该部分适用于Adobe Pass控制台，但AIQ也应类似。
http://tve.helpdocsonline.com/primetime-tve-dashboard-user-guide对AIQ感兴趣的组织应是在Adobe Marketing Cloud组织注册的组织。 组织中的用户应被分配到TVE功能板读写或TVE功能板只读。
仅供您了解，这些用户组会为用户帐户设置dma_primetime产品上下文。 在AIQ代码中，我们在提供访问权限时检查此产品上下文。 在内部，在代码中我们还有一个附加条件：组织id应列入白名单，以便用户访问其数据。
这就是我们现在的情况。 计划删除dma_primetime检查，并为AIQ提供专用配置文件。 需要具有控制台访问权限的用户将需要该用户配置文件。 但目前尚未实施。

..........................

1. 在Adobe Marketing Cloud载入组织
2. 将“TVE功能板读写”或“TVE功能板只读”用户档案分配到http://adminconsole.adobe.com/中。
3. 将其组织ID列入AIQ端白名单
