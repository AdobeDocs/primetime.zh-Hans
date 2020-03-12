---
description: 授权管理器是支持Primetime身份验证实现的功能管理器。
seo-description: 授权管理器是支持Primetime身份验证实现的功能管理器。
seo-title: Entitlement Manager概述
title: Entitlement Manager概述
uuid: b33dfae3-a132-4215-9992-80cbf4c87a61
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Entitlement Manager概述 {#entitlement-manager-overview}

授权管理器是支持Primetime身份验证实现的功能管理器。

## 功能概述

Primetime身份验证与Android Primetime SDK参考实施的集成为应用程序添加了新功能管理器。 但是，与许多其他功能管理器不同， *EntitlementManager在整个应用程序的多个位置都使用*。 以下概述了为支持Primetime身份验证而对参考实施所做的更改和添加：

### EntitlementManager类

该类 `EntitlementManager` 处理与Primetime身份验证SDK的所有通信，并封装授权工作流程所需的应用程序逻辑。 应用 `EntitlementManager`程序使用公共API来启动授权工作流，而接口为应用程序提供了处理事件的回调机 `EntitlementMangerListener``EntitlementManger` 制。

### EntitlementManger回调

引用实施的主要活动( `CatalogActivity`)创建一个实例，并 `EntitlementManagerListener` 在中注册它 `EntitlementManager`。 这样，可能会向应 `EntitlementManager` 用程序的其余部分发出所需UI更新的信号。 回调包括显示／隐藏加载对话框、显示状态对话框、更新授权和身份验证图标以及在成功授权时启动视频回放。

### 授权对话框

类根 `EntitlementDialogFragment` 据传递给类构造函数的授权状态生成对话框消息。 此类用于验证成功消息和所有错误消息。 当 `CatalogActivity` 从中接收特定事件时，将显示授权对话框 `EntitlementManager`。 此外，该接 `CatalogActivity` 口包括回 `EntitlementDialogListener` 调方法，用于在关闭对话框或用户从Primetime身份验证服务注销时发出信号。

### 内容提供者选择和登录

在使用Primetime身份验证进行身份验证期间，有两 `MvpdPickerActivity` 个新活 `MvpdLoginActivity`动，允许用户选择其内容提供商并登录。 这两个活动都从中 `CatalogActivity` 启动 `EntitlementManager`。 此外，将结 `MvpdPickerActivity` 果和 `MvpdLoginActivity` 返回结果都返回到 `CatalogActivity` ，因此 `CatalogActivity` 必须覆盖 `Activity.onActivityResult` 方法。

### “登录”按钮

“参考实施”的主要活动( `CatalogActivity`)在其操作栏中包含一个新的“登录”按钮。 “登录”按钮允许用户使用Primetime身份验证启动身份验证。 此外，用户可以通过选择用于回放的受保护视频来启动身份验证。 “登录”按钮的图标和文本会根据用户的身份验证状态而更改，其中包含的代码用于在页面刷新时更新按钮的图标和文本。 `CatalogActivity` 为此，启动时， `CatalogActivity` 会调用以更 `EntitlementManager.checkAuthentication()` 新用户的身份验证状态。

### 内容授权

在中， `CatalogView`新图标显示在内容图标的顶部，以指示用户对该内容的授权状态。 例如，如果用户已获得观看视频的预授权，则内容上方会显示一个绿色圆圈图标。 但是，如果用户未获得观看视频的预先授权，则会显示一个键图标。 这些图标的显示在中处理 `ContentTileAdapter`，但是，当调用回调时，会从中启动 `CatalogActivity` 其状态的 `EntitlementManagerListener` 更新。

### 内容播放

现在，视频播放需要经过授权检查 `EntitlementManager`。 在中发 `EntitlementManager.getAuthorization()` 生调用 `CatalogView`。 如果视频需要授权且用户已获得授权，则 `PlayerActivity` 从启动 `CatalogActivity`。

