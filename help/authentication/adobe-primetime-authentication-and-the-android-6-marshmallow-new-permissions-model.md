---
title: Adobe Primetime身份验证和Android 6“Marshmallow”新权限模型
description: Adobe Primetime身份验证和Android 6“Marshmallow”新权限模型
exl-id: 3c96769e-b25b-48ab-bb74-40f13d4e5a84
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Adobe Primetime身份验证和Android 6“Marshmallow”新权限模型 {#adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

</br>

新的Android 6棉花糖发行版本引入了权限模型的一些更新，这可能会影响使用现有Adobe Primetime身份验证SDK版本1.8和更早版本的应用程序的行为。 

作为新功能，新的Android操作系统提供 [精细地控制应用程序在安装时和运行时所需的权限](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html).

>[!IMPORTANT]
>
>下面描述的更改将 **仅影响专门为Android 6.0开发的应用程序** (targetSdkVersion=23)。 升级到Android 6.0时，它们不会影响用户设备上已安装的旧版应用程序。 


具体而言，对于在Android Studio中开发的应用程序，使用 [API级别23](http://developer.android.com/sdk/api_diff/23/changes.html) 并且使用Adobe Primetime Authentication SDK的客户，开发人员将需要编写自定义代码（请参阅下面的代码片段） [触发允许/拒绝权限对话框](https://developer.android.com/training/permissions/requesting.html). 

下面是用来请求对设备外部存储的写访问的代码摘录：

```java
// Here, thisActivity is the current activity
if (ContextCompat.checkSelfPermission(thisActivity,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)
        != PackageManager.WRITE_EXTERNAL_STORAGE) {

    // Should we show an explanation?
    if (ActivityCompat.shouldShowRequestPermissionRationale(thisActivity,
            Manifest.permission.WRITE_EXTERNAL_STORAGE)) {

        // Show an expanation to the user *asynchronously* -- don't block
        // this thread waiting for the user's response! After the user
        // sees the explanation, try again to request the permission.

    } else {

        // No explanation needed, we can request the permission.

        ActivityCompat.requestPermissions(thisActivity,
                new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE);

        // MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE is an
        // app-defined int constant. The callback method gets the
        // result of the request.
    }
}
```




**从用户的角度来看**，安装后，用户会看到一个窗口，提示他们确认文件的读/写权限（见下图2）。 这会导致以下两种结果之一：

1. 如果用户 **确认** 权限、常规身份验证流程将保留，令牌将存储在全局存储中。 只要令牌有效，用户就将在使用Adobe Primetime身份验证的应用程序中和跨应用程序保持身份验证。
1. 如果用户 **拒绝** 存储中的权限和写入操作将失败，并且用户只有在退出应用程序后才能进行身份验证。 请注意，某些应用程序在前台和后台之间切换时重新初始化，以便用户在执行此操作时注销。 令牌不会存储，用户每次使用应用程序时都需要进行身份验证。 


>[!TIP]
>
>目前正在为Adobe Primetime Authentication SDK 1.9开发引入存储可复原性的功能。新SDK面向 **在10月最后一周发布**. 每当无法使用常规存储时，应用程序将回退到在应用程序的沙盒存储中写入。 这涵盖了以下情况：对于在API级别23中开发的应用程序，用户不接受全局存储中的读/写权限。 每个应用程序分别存储令牌，这意味着将禁用使用Adobe Primetime身份验证的应用程序之间的单点登录。


![](assets/android-permissions-request.png)

*图：针对API级别23编写的应用程序的权限请求对话框*

>[!IMPORTANT]
>
> Adobe建议 **其合作伙伴将使用API级别22 (targetSdkVersion=22)或更低版本开发应用程序，以确保在身份验证过程中获得最佳用户体验**.
