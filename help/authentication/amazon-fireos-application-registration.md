---
title: Amazon FireOS应用程序注册
description: Amazon FireOS应用程序注册
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Amazon FireOS应用程序注册 {#amazon-fireos-application-registration}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

## 简介 {#intro}

从FireOS AccessEnabler SDK的3.0版开始，我们正在更改Adobe服务器的身份验证机制。 我们引入的软件语句字符串概念不是使用公钥和密钥系统来签署requestorID，而是可用于获取访问令牌，该令牌稍后将用于SDK向我们的服务器发起的所有调用。 除了软件声明之外，您还需要为应用程序创建深层链接。

有关更多信息，请参阅 [动态客户端注册](/help/authentication/dynamic-client-registration.md)

## 什么是软件声明？ {#what}

软件语句是JWT令牌，其中包含有关您的应用程序的信息。 每个应用程序都应具有唯一的“软件声明”，供我们的服务器用来标识Adobe系统中的应用程序。 在初始化AccessEnabler SDK时，需要传递软件语句，该语句将用于注册具有Adobe的应用程序。 注册后，SDK将收到客户端ID和客户端密钥，用于获取访问令牌。 SDK对我们的服务器进行的任何调用都将需要有效的访问令牌。 SDK负责注册应用程序、获取和刷新访问令牌。

**注意：** 软件语句是特定于应用程序的，单个软件语句不能用于多个应用程序。 请注意，这也适用于提供对多个渠道的访问权限的应用程序。

## 如何获取软件声明？ {#how-to}

### 如果您有权访问Adobe的TVE功能板：

- 打开浏览器并导航到 <https://console.auth.adobe.com>
- 导航到 `Channels` ，然后选择您的渠道。
- 导航到 `Registered Applications` 选项卡。
- 单击 `Add new application`.
- 为您的应用程序提供名称和版本，并选择可用该应用程序的平台（例如，在本例中为Android）。
- 通过从已为程序员配置的域列表中进行选择来提供域名。
- 将更改推送到服务器，然后导航回渠道的注册应用程序选项卡。
- 您应会看到包含所有注册应用程序的列表。 单击 `Download` 按钮。 注意：您可能需要等待几分钟，软件声明才能准备好下载。
- 将下载文本文件。 将其内容用作软件声明。

有关更多信息，请参阅 [动态客户端注册管理](/help/authentication/dynamic-client-registration-management.md)

### 如果您无权访问Adobe的TVE功能板：

将票证提交到 <tve-support@adobe.com>. 请提供所有必需的信息，包括渠道、应用程序名称、版本和平台，我们支持团队的人员将为您创建软件声明。

## 如何使用软件声明？ {#use}

获取软件语句后，您需要将其作为Access Enabler构造函数中的参数进行传递。 我们建议在远程位置上托管软件语句。 这样，您就可以轻松撤消和更改软件声明，而无需发布新版本的应用程序。

## 如何使用软件声明 {#use-both}

在应用程序的资源文件中 `strings.xml` 添加以下代码：

```XML
<string name="software_statement">softwarestatement value</string>
```
