---
description: 权利管理器是支持Primetime身份验证实施的功能管理器。
title: 授权管理器概述
exl-id: a66e131e-283f-4378-b834-7cfa887b3ec9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# 授权管理器概述 {#entitlement-manager-overview}

权利管理器是支持Primetime身份验证实施的功能管理器。

## 功能概述

与Android Primetime SDK参考实施的Primetime身份验证集成向应用程序添加了一个新的功能管理器。 但是，与许多其他功能管理器不同， *EntitlementManager在整个应用程序中的多个位置中使用*. 下面概述了为支持Primetime身份验证而对Reference Implementation所做的更改和添加：

### EntitlementManager类

此 `EntitlementManager` 类处理与Primetime身份验证SDK的所有通信，并且封装权利工作流所需的应用程序逻辑。 此 `EntitlementManager`的公共API由应用程序用于启动授权工作流，而 `EntitlementMangerListener` 接口为应用程序提供回调机制以处理 `EntitlementManger` 事件。

### EntitlementManger回调

参考实施的主要活动 `CatalogActivity`，创建实例 `EntitlementManagerListener` 并在 `EntitlementManager`. 通过这种方式， `EntitlementManager` 可能会向应用程序的其余部分发出所需的UI更新的信号。 回调包括显示/隐藏加载对话框、显示状态对话框、更新授权和身份验证图标以及在成功授权后开始视频播放。

### 权利对话框

此 `EntitlementDialogFragment` 类根据传递给类构造函数的权利状态生成对话框消息。 此类用于身份验证成功消息以及所有错误消息。 此 `CatalogActivity` 当从以下位置收到特定事件时显示权利文件对话框： `EntitlementManager`. 此外， `CatalogActivity` 实施 `EntitlementDialogListener` 界面，包括回调方法，用于在对话框关闭或用户从Primetime身份验证服务注销时发出信号。

### 内容提供商选择和登录

在使用Primetime身份验证期间，有两个新的活动， `MvpdPickerActivity` 和 `MvpdLoginActivity`，允许用户选择其内容提供商并登录。 这两个活动都是从以下位置开始的： `CatalogActivity` 通过 `EntitlementManager`. 此外， `MvpdPickerActivity` 和 `MvpdLoginActivity` 将结果返回到 `CatalogActivity` 及因此，本公 `CatalogActivity` 必须覆盖 `Activity.onActivityResult` 方法。

### 登录按钮

参考实施的主要活动 `CatalogActivity`，在其操作栏中包含一个新的“登录”按钮。 “登录”按钮允许用户使用Primetime身份验证启动身份验证。 此外，用户可以通过选择用于播放的受保护视频来启动身份验证。 登录按钮的图标和文本会根据用户的身份验证状态以及 `CatalogActivity` 包含用于在页面刷新时更新按钮图标和文本的代码。 要执行此操作，当 `CatalogActivity` 开始，它调用 `EntitlementManager.checkAuthentication()` 更新用户的身份验证状态。

### 内容权利

在 `CatalogView`时，新图标会显示在内容图标的顶部，表示该内容的用户授权状态。 例如，如果用户获得了查看视频的预授权，则内容上方会显示一个绿色圆圈图标。 但是，如果用户未获得查看视频的预授权，则会显示一个键图标。 这些图标的显示在中处理 `ContentTileAdapter`但是，其状态的更新是从以下位置启动的： `CatalogActivity` 当回调位于 `EntitlementManagerListener` 称为。

### 内容播放

现在，视频播放需要由进行授权检查 `EntitlementManager`. 对的调用 `EntitlementManager.getAuthorization()` 发生于 `CatalogView`. 如果视频需要授权并且用户已获得授权，则 `PlayerActivity` 开始于 `CatalogActivity`.
