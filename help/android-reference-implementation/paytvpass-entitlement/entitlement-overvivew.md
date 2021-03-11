---
description: 授权管理器是支持Primetime身份验证实施的功能管理器。
title: Entitlement Manager概述
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# Entitlement Manager概述{#entitlement-manager-overview}

授权管理器是支持Primetime身份验证实施的功能管理器。

## 功能概述

Primetime身份验证与Android Primetime SDK参考实施的集成为应用程序添加了一个新功能管理器。 但是，与许多其他功能管理器不同，*EntitlementManager用于应用程序中的多个位置*。 以下概述了为支持Primetime身份验证而对参考实施所做的更改和添加：

### EntitlementManager类

`EntitlementManager`类处理与Primetime身份验证SDK的所有通信，并封装授权工作流所需的应用程序逻辑。 应用程序使用`EntitlementManager`的公共API启动授权工作流，而`EntitlementMangerListener`接口为应用程序提供了处理`EntitlementManger`事件的回调机制。

### EntitlementManger回调

引用实现的主活动`CatalogActivity`创建了`EntitlementManagerListener`的实例，并将其注册到`EntitlementManager`。 这样，`EntitlementManager`可以向应用程序的其余部分发出所需UI更新的信号。 回调包括显示/隐藏加载对话框、显示状态对话框、更新授权和身份验证图标以及在成功授权时启动视频回放。

### 授权对话框

`EntitlementDialogFragment`类根据传递给类构造函数的授权状态生成对话框消息。 此类用于身份验证成功消息和所有错误消息。 当`CatalogActivity`从`EntitlementManager`收到特定事件时，将显示授权对话框。 此外，`CatalogActivity`实现`EntitlementDialogListener`接口，该接口包括在关闭对话框或用户从Primetime身份验证服务注销时发出信号的回调方法。

### 内容提供商选择和登录

在使用Primetime身份验证进行身份验证期间，两个新活动`MvpdPickerActivity`和`MvpdLoginActivity`允许用户选择其内容提供商并登录。 这两个活动都通过`EntitlementManager`从`CatalogActivity`启动。 此外，`MvpdPickerActivity`和`MvpdLoginActivity`都将结果返回至`CatalogActivity`，因此`CatalogActivity`必须覆盖`Activity.onActivityResult`方法。

### “登录”按钮

参考实施的主活动`CatalogActivity`在其操作栏中包含一个新的“登录”按钮。 “登录”按钮允许用户使用Primetime身份验证启动身份验证。 此外，用户可以通过选择用于回放的受保护视频来启动身份验证。 “登录”按钮的图标和文本会根据用户的身份验证状态而更改，并且`CatalogActivity`包含用于在页面刷新时更新按钮图标和文本的代码。 为此，当`CatalogActivity`开始时，它将调用`EntitlementManager.checkAuthentication()`以更新用户的身份验证状态。

### 内容授权

在`CatalogView`中，新图标显示在内容图标的上方，以指示用户对该内容的授权状态。 例如，如果用户已获得视图视频的预授权，则内容上方会显示一个绿色圆圈图标。 但是，如果用户未获得视图视频的预授权，则会显示一个键图标。 这些图标的显示在`ContentTileAdapter`中处理，但当调用`EntitlementManagerListener`中的回调时，会从`CatalogActivity`启动其状态的更新。

### 内容播放

现在，视频播放需要`EntitlementManager`的授权检查。 对`EntitlementManager.getAuthorization()`的调用发生在`CatalogView`中。 如果视频需要授权，且用户已获得授权，则从`CatalogActivity`启动`PlayerActivity`。

