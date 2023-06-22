---
title: iOS/tvOS应用程序注册
description: iOS/tvOS应用程序注册
exl-id: 89ee6b5a-29fa-4396-bfc8-7651aa3d6826
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# iOS/tvOS应用程序注册 {#iostvos-application-registration}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 介绍 {#Intro}

从iOS/tvOS AccessEnabler SDK版本3.0开始，我们正在更改Adobe服务器的身份验证机制。 我们引入了Software语句字符串的概念，而不是使用公钥和密码系统对requestorID进行签名，该字符串可用于获取访问令牌，该令牌稍后将用于SDK对我们的服务器进行的所有调用。 除了软件声明之外，您还需要为应用程序使用自定义URL方案。

有关更多信息，请参阅 [动态客户端注册](/help/authentication/dynamic-client-registration.md)

## 什么是软件声明？ {#Soft_state}

软件语句是一个JWT令牌，其中包含有关应用程序的信息。 每个应用程序应有一个软件语句，供我们的服务器用来识别Adobe系统中的应用程序。 在初始化AccessEnabler SDK时需要传递软件语句，并将使用它向Adobe注册应用程序。 注册后，SDK将接收客户端ID和用于获取访问令牌的客户端密钥。 SDK对我们的服务器进行的任何调用都需要有效的访问令牌。 SDK负责注册应用程序、获取和刷新访问令牌。

**注意：** 软件语句是特定于应用程序的，同一软件语句不能用于多个应用程序。 请注意，程序员级别的软件语句也遵循相同的规则，即它们只能用于单个应用程序 — 无论是单渠道还是多渠道。 此限制也适用于自定义方案。

## 如何获取软件声明？ {#obtain}

### 如果您有权访问Adobe的TVE仪表板：

- 打开浏览器并导航到 <https://console.auth.adobe.com>
- 导航到 `Channels` 部分，然后选择您的渠道。
- 导航到 `Registered Applications` 选项卡。
- 单击 `Add new application`.
- 为您的应用程序提供名称和版本，并选择其可用的平台。 在我们的例子中，为iOS/tvOS。
- 将更改推送到服务器，然后导航回渠道的已注册应用程序选项卡。
- 您应该会看到一个包含所有已注册应用程序的列表。 单击   `Download` 您刚刚创建的应用程序上的按钮。 您可能需要等待几分钟，软件语句才可供下载。
- 将下载文本文件。 将其内容用作软件声明。

有关详细信息，请参阅， [动态客户端注册管理](/help/authentication/dynamic-client-registration-management.md).

### 如果您无权访问Adobe的TVE功能板：

将票证提交到 <tve-support@adobe.com>. 请包括所有必需的信息，如渠道、应用程序名称、版本和平台，我们的支持团队中的某人将为您创建一份软件声明。

## 如何使用软件声明？ {#use}

在获取软件语句后，您需要将其作为参数在Access Enabler构造函数中传递。 我们建议将软件声明托管在远程位置。 这样，您就可以轻松地撤销和更改软件语句，而无需发布应用程序的新版本。

## 为应用程序生成自定义URL方案 {#generating}

### 如果您有权访问Adobe的TVE仪表板：

- 打开浏览器并导航到 <https://console.auth.adobe.com>
- 导航到 `Channels` 部分，然后选择您的渠道。
- 导航到 `Custom Schemes` 选项卡。
- 单击 `Generate a new custom scheme`.
- 将为您的应用程序生成新的自定义方案。 例如： `adbe.1JqxQsYhQOCIrwPjaooY8w://`
- 将更改推送到服务器。

### 如果您无权访问Adobe的TVE功能板：

将票证提交到 <tve-support@adobe.com>. 请包含渠道ID，我们的支持团队中的某人将为您创建一个自定义方案。

## 如何使用自定义方案 {#use_custom}

在您的应用程序的 `info.plist` 文件添加以下代码：

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>adbe.u-XFXJeTSDuJiIQs0HVRAg</string> // replace this with your custom scheme
            </array>
        </dict>
    </array>
```
