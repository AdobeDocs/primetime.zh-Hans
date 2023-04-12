---
title: 了解Adobe环境
description: 了解Adobe环境
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 了解Adobe环境 {#understanding-the-adobe-environments}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

提供了描述Adobe环境的官方文档 [在Pre-Qual中设置环境和测试](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md):

Adobe环境，概括为以下几个词：

Adobe有两个环境： **资格预审** 和 **版本**.

* 在资格预审环境中，我们正准备发布新的内部版本。

* 当前版本内部版本位于发行环境中。

每个环境都有两个配置文件： **暂存** 和 **生产**.

* 暂存配置文件连接到MVPD暂存服务器
* 生产配置文件连接到MVPD生产配置文件。

拥有这两个用户档案的原因是，在暂存用户档案中，我们正在为新合作伙伴准备上线，他们希望通过即将推出的版本（资格预审）或版本1（更稳定）来测试系统。

如果合作伙伴想要测试新版本，则需要完成几个其他步骤。 看， [在Pre-Qual中设置环境和测试](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

按照上述步骤操作，可以确保即将发布的版本将在资格预审环境中进行测试。
