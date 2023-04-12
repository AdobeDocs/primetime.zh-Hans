---
title: iOS SDK 3.2+上的SFSafariViewController支持
description: iOS SDK 3.2+上的SFSafariViewController支持
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# iOS SDK 3.2+上的SFSafariViewController支持 {#sfsafariviewcontroller-support-on-ios-sdk-3.2}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>


**由于安全性要求，某些MVPD的登录页面必须显示在SFSafariViewController中，而不是Web视图中。**

某些MVPD要求在诸如SFSafariViewController之类的安全浏览器控件中显示其登录页面。 它们会主动阻止Web视图，因此为了能够使用它们进行身份验证，我们必须使用SVC。 

## 兼容性 {#compatiblity}

从iOS SDK版本3.1开始，AccessEnabler SDK会根据服务器配置，在SFSafariViewController中自动显示特定MVPD的登录页面。

SDK的3.1版本自动显示来自应用程序根视图控制器的SFSafariViewController。 虽然这简化了实施人员的登录页面管理，但在某些情况下，由于应用程序的特定实施（如已显示的模态控制器），无法从根视图控制器显示SFSafariViewController。

对于此类情况，3.2版本引入了程序员手动管理SVC的功能。

## 手动SVC管理 {#manual-svc-management}

为了手动管理SVC，实施者必须执行以下步骤：
 

1. 调用 **setOptions([&quot;handleSVC&quot;:true])** 在AccessEnabler初始化之后（确保在身份验证开始之前执行此调用）。 这将启用“手动”SVC管理， SDK不会自动显示SVC，而是在需要时调用 **navigate(toUrl:*{url}* useSVC:true)**.  

1. 实施可选回调 **navigateToUrl:useSVC:** 在实施中，必须使用提供的url使用SFSafariViewController实例创建svc实例，并将其显示在屏幕上：

   ```obj-c
   func navigate(toUrl url: String!, useSVC: Bool) {
       svc =  SFSafariViewController(url: URL(string: url)!)
       svc.delegate = self
       myController.present(svc, animated: true)
       }
   ```

   ***注意：***

   - *您可以根据需要自定义SFSafariViewController。 例如，在iOS 11+上，您可以将“完成”标签更改为“取消”。*
   - *为了能够取消svc，您需要引用它，请不要在 **navigateToUrl:useSVC***
   - *将您自己的视图控制器用于“myController”*\
       

1. 在应用程序的委托实施中 **application(\_app):UIApplication，打开url:URL，选项：\[UIApplicationOpenURLOptionsKey:Any\])-\>布尔**，添加代码以关闭svc。 您应该已经有一些代码可调用 **accessEnabler.handleExternalURL()**. 在下面添加：

   ```obj-c
   if(svc != nil) {
       svc.dismiss(animated: true)
   }
   ```

   同样，svc是对您在步骤2中创建的SFSafariViewController的引用。\
    

1. 实施 **safariViewControllerDidFinish(\_ controller:SFSafariViewController)** 从 **SFSafariViewControllerDelegate** 以便在用户使用“完成”按钮取消svc时捕获。 在此函数中，为了告知SDK身份验证已取消，您需要调用：

   ```obj-c
   accessEnabler.setSelectedProvider(nil)
   ```

