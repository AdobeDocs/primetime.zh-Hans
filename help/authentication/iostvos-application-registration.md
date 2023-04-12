---
title: iOS/tvOS应用程序注册
description: iOS/tvOS应用程序注册
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# iOS/tvOS应用程序注册 {#iostvos-application-registration}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#Intro}

从版本3.0的iOS/tvOS AccessEnabler SDK开始，我们正在更改Adobe服务器的身份验证机制。 我们引入的Software语句字符串概念不是使用公钥和密钥系统来签署requestorID，而是可用于获取访问令牌，该令牌稍后将用于SDK向我们的服务器发起的所有调用。 除了软件语句外，您还需要为应用程序提供自定义URL方案。

有关更多信息，请参阅 [动态客户端注册](/help/authentication/dynamic-client-registration.md)

## 什么是软件声明？ {#Soft_state}

软件语句是JWT令牌，其中包含有关您的应用程序的信息。 每个应用程序都应具有一个唯一的软件语句，供我们的服务器用来标识Adobe系统中的应用程序。 在初始化AccessEnabler SDK时，需要传递软件语句，该语句将用于注册具有Adobe的应用程序。 注册后，SDK将收到客户端ID和客户端密钥，用于获取访问令牌。 SDK对我们的服务器进行的任何调用都将需要有效的访问令牌。 SDK负责注册应用程序、获取和刷新访问令牌。

**注意：** 软件语句是特定于应用程序的，并且同一软件语句不能在多个应用程序上使用。 请注意，程序员级别的软件语句也遵循相同的内容，即它们只能用于单个应用程序 — 无论是单个渠道还是多渠道。 此限制也适用于自定义方案。

## 如何获取软件声明？ {#obtain}

### 如果您有权访问Adobe的TVE功能板：

- 打开浏览器并导航到 <https://console.auth.adobe.com>
- 导航到 `Channels` ，然后选择您的渠道。
- 导航到 `Registered Applications` 选项卡。
- 单击 `Add new application`.
- 为您的应用程序提供名称和版本，并选择可用该应用程序的平台。 iOS/tvOS。
- 将更改推送到服务器，然后导航回渠道的注册应用程序选项卡。
- 您应会看到一个包含所有注册应用程序的列表。 单击   `Download` 按钮。 您可能需要等待几分钟，软件声明才可供下载。
- 将下载文本文件。 将其内容用作软件声明。

有关详细信息，请参阅 [动态客户端注册管理](/help/authentication/dynamic-client-registration-management.md).

### 如果您无权访问Adobe的TVE功能板：

将票证提交到 <tve-support@adobe.com>. 请包含所有必需的信息，如渠道、应用程序名称、版本和平台，我们支持团队的人员将为您创建软件声明。

## 如何使用软件声明？ {#use}

获取软件语句后，您需要将其作为Access Enabler构造函数中的参数进行传递。 我们建议在远程位置上托管软件语句。 这样，您就可以轻松撤消和更改软件声明，而无需发布新版本的应用程序。

## 为应用程序生成自定义URL方案 {#generating}

### 如果您有权访问Adobe的TVE功能板：

- 打开浏览器并导航到 <https://console.auth.adobe.com>
- 导航到 `Channels` ，然后选择您的渠道。
- 导航到 `Custom Schemes` 选项卡。
- 单击 `Generate a new custom scheme`.
- 将为您的应用程序生成新的自定义方案。 例如： `adbe.1JqxQsYhQOCIrwPjaooY8w://`
- 将更改推送到服务器。

### 如果您无权访问Adobe的TVE功能板：

将票证提交到 <tve-support@adobe.com>. 请包含渠道id，我们支持团队的人员将为您创建自定义方案。

## 如何使用自定义方案 {#use_custom}

在您应用程序的 `info.plist` 文件添加以下代码：

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
