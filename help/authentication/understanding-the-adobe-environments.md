---
title: 了解Adobe环境
description: 了解Adobe环境
exl-id: bb6cf37f-48cd-47bb-b3c2-f7a96e49b12d
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 了解Adobe环境 {#understanding-the-adobe-environments}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

提供了描述Adobe环境的官方文档 [设置您的环境并测试预修课程](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md)：

Adobe环境，可以用几个词概括：

Adobe有两个环境： **资格预审** 和 **版本**.

* 在资格预审环境中，我们正在准备要发布的新内部版本。

* 当前版本内部版本位于版本环境中。

每个环境都有两个配置文件： **暂存** 和 **生产**.

* 暂存配置文件连接到MVPD暂存服务器
* 生产配置文件连接到MVPD生产配置文件。

具有这两个配置文件的原因是，在暂存配置文件中，我们在为新合作伙伴准备上线，他们希望通过即将发布的版本（资格预审）或版本版本（更稳定）来测试系统。

如果合作伙伴希望测试新版本，则需要执行一些其他步骤。 参见， [设置您的环境并测试预修课程](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

通过执行上述步骤，可以确保即将发布的版本将在预认证环境中进行测试。
