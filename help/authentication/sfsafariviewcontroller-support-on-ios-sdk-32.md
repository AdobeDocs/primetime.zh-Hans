---
title: iOS SDK 3.2+上的SFSafariViewController支持
description: iOS SDK 3.2+上的SFSafariViewController支持
exl-id: 6691550f-c36f-4fae-aa77-082ca7d8a60a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# iOS SDK 3.2+上的SFSafariViewController支持 {#sfsafariviewcontroller-support-on-ios-sdk-3.2}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

</br>


**由于安全要求，某些MVPD的登录页必须以SFSafariViewController而不是Web视图显示。**

有些MVPD要求它们的登录页以安全的浏览器控件（如SFSafariViewController）显示。 它们会主动阻止Web视图，因此为了能够使用它们进行身份验证，我们必须使用SVC。 

## 兼容性 {#compatiblity}

从iOS SDK版本3.1开始，AccessEnabler SDK根据服务器配置自动显示SFSafariViewController中特定MVPD的登录页面。

SDK版本3.1自动从应用程序的根视图控制器中显示SFSafariViewController。 虽然这简化了实施者的登录页面管理，但在某些情况下，由于应用程序的特定实施（如已可见的模式控制器），无法从根视图控制器中显示SFSafariViewController。

对于这种情况，3.2版本引入了程序员手动管理SVC的功能。

## 手动SVC管理 {#manual-svc-management}

要手动管理SVC，实施人员必须执行以下步骤：
 

1. 调用 **setOptions([&quot;handleSVC&quot;：true])** AccessEnabler初始化之后（确保在身份验证开始之前执行此调用）。 这将启用“手动”SVC管理，SDK不会自动呈现SVC，而是在需要时调用 **navigate(toUrl：*{url}* useSVC：true)**.  

1. 实施可选回调 **navigateToUrl:useSVC:** 在实施中，您必须使用提供的URL通过SFSafariViewController实例创建svc实例，并将其显示在屏幕上：

   ```obj-c
   func navigate(toUrl url: String!, useSVC: Bool) {
       svc =  SFSafariViewController(url: URL(string: url)!)
       svc.delegate = self
       myController.present(svc, animated: true)
       }
   ```

   ***注释：***

   - *您可以根据需要任何方式自定义SFSafariViewController。 例如，在iOS 11+上，您可以将“完成”标签更改为“取消”。*
   - *为了能够关闭svc，您需要引用它，请不要在范围内创建它 **navigateToUrl：useSVC***
   - *将您自己的视图控制器用于“myController”*\
       

1. 在您的应用程序委托实现中 **application（\_app： UIApplication，打开URL： URL，选项： \[UIApplicationOpenURLOptionsKey： Any\]） -\> Bool**，添加代码以关闭svc。 您应该已经有一些代码可调用 **accessEnabler.handleExternalURL()**. 在下方添加：

   ```obj-c
   if(svc != nil) {
       svc.dismiss(animated: true)
   }
   ```

   同样，svc是对您在步骤2中创建的SFSafariViewController的引用。\
    

1. 实施 **safariViewControllerDidFinish（\_控制器：SFSafariViewController）** 起始日期 **SFSafariViewControllerDelegate** 以便捕获用户何时使用“Done”按钮取消了svc。 在此函数中，要通知SDK身份验证已取消，您需要调用：

   ```obj-c
   accessEnabler.setSelectedProvider(nil)
   ```
