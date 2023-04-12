---
title: 使用Primetime身份验证访问启用程序时在iOS上使用SSO
description: 使用Primetime身份验证访问启用程序时在iOS上使用SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---


# 使用Primetime身份验证访问启用程序时在iOS上使用SSO {#sso-on-ios-when-using-the-primetime-authentication-access-enabler}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

## 概述

Primetime身份验证支持的应用程序之间的单点登录(SSO)工作方式不同，具体取决于底层操作系统。

本文档的地址 **iOS上的单点登录**，使用Adobe Primetime身份验证时 **Access Enabler**.

**Access Enabler** **1.10** 是Adobe Primetime身份验证iOS本机SDK的最新版本。 Adobe强烈建议您转到此版本，而不是继续使用旧版本。 如果您使用的是旧版Access Enabler，则可以下载最新版本 [此处](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

iOS上的单点登录受以下条件限制：

- 应用程序必须使用相同的 **令牌存储** （以Access Enabler创建的自定义粘贴板的形式）。
- 应用程序必须生成相同的 **设备ID** (Access Enabler根据MAC地址或IDFV计算设备ID，具体取决于操作系统版本)。

## 行为

SSO行为如下：

- **iOS 6及更低版本**:SSO可在由同一团队或不同团队开发的应用程序之间自动工作。 设备ID是根据MAC地址计算的（所有应用程序中都会生成相同的值），并且存储区域对所有应用程序都是通用的(自定义粘贴板可在iOS 6及更低版本的应用程序中共享)。
   - **重要信息：** 请注意，iOS SDK 1.9.4版本已 [将iOS的最低部署目标提高到iOS 7。](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library) 
- **iOS 7及更高版本**:SSO将在以下条件下工作：

1. 使用相同的Apple分发配置文件或属于同一团队的配置文件发布应用程序。 这是应用程序在iOS 7和更高版本上共享自定义粘贴板的唯一方法。 在所有其他情况下，粘贴板会根据应用程序进行沙箱处理。 从 [*https://developer.apple.com/library/IOs/releasenotes/General/RN-iOSSDK-7.0/index.html*](https://developer.apple.com/library/ios/releasenotes/General/RN-iOSSDK-7.0/index.html):\+\[UIPasteboard pasteboardWithName:create:\]和+\[UIPasteboard粘贴板WithUniqueName\]现在具有给定名称的唯一性，只允许同一应用程序组中的这些应用程序访问粘贴板。 如果开发人员尝试创建一个粘贴板，其名称已存在，并且它们不属于同一应用程序包，则他们将获得自己唯一的专用粘贴板。 请注意，这不会影响系统提供的粘贴板、常规和查找。

1. 应用程序具有相同的包ID前缀（除最后一个组件外的所有组件）。 只有共享相同捆绑ID前缀的应用程序才会计算相同的IDFV。 从 [*https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice\_Class/index.html\#//apple\_ref/occ/instp/UIDevice/identifierForVendor*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice_Class/index.html#//apple_ref/occ/instp/UIDevice/identifierForVendor):在IOS 7中，包中除最后一个组件之外的所有组件都用于生成供应商ID。 如果包ID只包含单个组件，则使用整个包ID。

现在，我们来关注 **“iOS 7及更高版本”** 情景中，由于它是实际用户最频繁的事件：

这两个条件（共享来自同一开发团队的用户档案并具有通用捆绑标识符前缀）都是SSO的必备条件。

以下是可能的组合及其产生的结果：

- **来自同一团队和同一包ID前缀的用户档案**:应用程序将共享相同的粘贴板存储，并将具有相同的设备ID(IDFV)。 用户只需进行一次身份验证（在使用的第一个应用程序中），身份验证状态将在所有其他应用程序之间共享。 示例流量：

1. 用户打开应用程序A（具有包ID） *com.x.y.AppA*)且未进行身份验证
1. 用户在应用程序A中执行身份验证
1. 用户打开应用程序B（具有包ID） *com.x.y.AppB*)，并通过从应用程序A共享授权数据自动进行身份验证（步骤2中）
1. 用户打开应用程序A，并且仍经过身份验证（从步骤2开始）

 

- **来自同一团队但包ID前缀不同的配置文件**:应用程序将共享相同的粘贴板存储，但将具有不同的设备ID(IDFV)。 用户需要对每个应用程序进行一次身份验证。 示例流量：

1. 用户打开应用程序A（具有包ID） *com.x.y.AppA*)且未进行身份验证
1. 用户在应用程序A中执行身份验证
1. 用户打开应用程序B（具有包ID） *com.z.AppB*)，并且Access Enabler会检测由第一个应用程序获取的令牌（因为存储是共享的），但由于设备ID不同，它不会尝试通过SSO来使用它
1. 用户在应用程序B中执行身份验证
1. 用户打开应用程序A，并且仍经过身份验证（从步骤2开始）

 

- **来自不同团队的用户档案（在此情景中，包ID无关紧要）**:应用程序将具有不同的粘贴板存储，并且它们之间将禁用SSO。 用户将需要为每个应用程序进行一次身份验证，并且在应用程序之间切换时，身份验证会话将保持永久性。 示例流量：


1. 用户打开应用程序A，并且未进行身份验证
1. 用户在应用程序A中执行身份验证
1. 用户打开应用程序B，并且未进行身份验证
1. 用户在应用程序B中执行身份验证
1. 用户打开应用程序A并进行身份验证（步骤2中）
1. 用户打开应用程序B并进行身份验证（步骤4中）

**注意：** 请注意，上述SSO条件适用于通过 **AppleApp Store**. 如果应用程序是在模拟器上部署的（应用程序签名不适用），与Xcode一起安装或通过临时配置文件分发的，您可能会获得不同的结果。

**重要信息：** 注(**关于AccessEnabler v1.8**):上述第二种情况（来自同一团队但包ID前缀不同的用户档案）将为 **AccessEnabler v1.8** 跨由同一团队（媒体公司）开发的应用程序。 在来自同一媒体公司的应用程序之间进行转换时，用户将被自动注销，因此，应用程序开发人员在决定捆绑ID和分发配置文件时必须小心。 本例中的确切情况如下：

应用程序将共享相同的粘贴板存储，但将具有不同的设备ID(IDFV)。 用户需要对每个应用程序进行一次身份验证， **但是，在应用程序之间切换时，验证会话将被擦除**. 示例流量：

1. 用户打开应用程序A（具有包ID） *com.x.y.AppA*)且未进行身份验证
1. 用户在应用程序A中执行身份验证
1. 用户打开应用程序B（具有包ID） *com.z.AppB*)，应用程序A创建的授权数据将由Access Enabler自动擦除（安全机制可检测应用程序B中当前计算的设备ID与应用程序A创建的授权令牌中存储的设备ID之间是否存在冲突）
1. 用户在应用程序B中执行身份验证
1. 用户打开应用程序A，并且由应用程序B创建的授权数据会由Access Enabler自动擦除（安全机制可检测应用程序A中当前计算的设备ID与由应用程序B创建的授权令牌中存储的设备ID之间是否存在冲突）

