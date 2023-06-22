---
title: Android应用程序注册
description: Android应用程序注册
exl-id: 6238bd87-ac97-4a5c-9d92-3631f7b2d46a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---

# Android应用程序注册 {#android-application-registration}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 介绍 {#intro}

从Android AccessEnabler SDK版本3.0开始，我们正在更改Adobe服务器的身份验证机制。 我们引入了Software语句字符串的概念，而不是使用公钥和密码系统对requestorID进行签名，该字符串可用于获取访问令牌，该令牌稍后将用于SDK对我们的服务器进行的所有调用。 除了软件声明之外，您还需要为应用程序创建深层链接。

有关更多信息，请参阅 [动态客户端注册](/help/authentication/dynamic-client-registration.md)

## 什么是软件声明？ {#what}

软件语句是一个JWT令牌，其中包含有关应用程序的信息。 每个应用程序应有一个软件语句，供我们的服务器用来识别Adobe系统中的应用程序。 在初始化AccessEnabler SDK时需要传递软件语句，并将使用它向Adobe注册应用程序。 注册后，SDK将接收客户端ID和用于获取访问令牌的客户端密钥。 SDK对我们的服务器进行的任何调用都需要有效的访问令牌。 SDK负责注册应用程序、获取和刷新访问令牌。

>[!NOTE]
>
>软件语句特定于应用程序，单个软件语句不能用于多个应用程序。 请注意，程序员级别的软件语句具有相同的限制，它们只能用于单个应用程序，无论是单渠道还是多渠道。

## 如何获取软件声明？ {#how-to-get-ss}

### 如果您有权访问Adobe的TVE仪表板：

* 打开浏览器并导航到 [Adobe Primetime TVE功能板](https://console.auth.adobe.com).
* 导航到 `Channels` 部分，然后选择您的渠道。
* 导航到 `Registered Applications` 选项卡。
* 单击 `Add new application`.
* 为您的应用程序提供名称和版本，并选择其可用的平台。 Android。
* 从已为程序员配置的域列表中进行选择，以提供域名。
* 将更改推送到服务器，然后导航回渠道的已注册应用程序选项卡。
* 您应该会看到一个包含所有已注册应用程序的列表。 选择 **下载** 您刚刚创建的应用程序上的按钮。 您可能需要等待几分钟，软件语句才可供下载。
* 将下载文本文件。 将其内容用作软件声明。

有关更多信息，请参阅 [动态客户端注册管理](/help/authentication/dynamic-client-registration-management.md)

### 如果您无权访问Adobe的TVE功能板：

将票证提交到 `tve-support@adobe.com`. 请包括所有必需的信息，如渠道、应用程序名称、版本和平台，我们的支持团队中的某人将为您创建一份软件声明。

## 如何使用软件声明？ {#how-to-use-ss}

在获取软件语句后，您需要将其作为参数在Access Enabler构造函数中传递。 我们建议将软件声明托管在远程位置。 这样，您就可以轻松地撤销和更改软件语句，而无需发布应用程序的新版本。

## 为您的应用程序创建并使用深层链接 {#create}

在Android上，使用与创建软件语句时选择的域名相反的深层链接值

创建的深层链接在Android设备上应具有唯一值。 当多个应用程序使用相同的深层链接值时，身份验证和注销流将干预。

## 如何使用软件声明和深层链接 {#use-both}

在应用程序的资源文件中 `strings.xml` 添加以下代码：

```JAVA
    <string name="software_statement">softwarestatement value</string>
    <string name="redirect_uri">com.domain_name</string>
```
