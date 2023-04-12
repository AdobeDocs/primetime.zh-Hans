---
title: Adobe Primetime身份验证和Android 6“棉花糖”新权限模型
description: Adobe Primetime身份验证和Android 6“棉花糖”新权限模型
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---



# Adobe Primetime身份验证和Android 6“棉花糖”新权限模型 {#adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

新的Android 6 Marshmallow版本引入了一些权限模型的更新，这可能会影响使用现有Adobe Primetime身份验证SDK版本1.8及更低版本的应用程序的行为。 

作为一项新功能，Android操作系统提供了 [对应用程序在安装时和运行时所需的权限进行精细控制](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html).

>[!IMPORTANT]
>
>下面描述的更改将 **仅影响专门为Android 6.0开发的应用程序** (targetSdkVersion=23)。 升级到Android 6.0时，它们不会影响用户设备上已安装的旧版应用程序。 


具体而言，适用于在Android Studio中使用 [API级别23](http://developer.android.com/sdk/api_diff/23/changes.html) 如果使用Adobe Primetime Authentication SDK，开发人员将需要编写自定义代码（请参阅下面的代码段） [触发允许/拒绝权限对话框](https://developer.android.com/training/permissions/requesting.html). 

以下是用于请求对设备外部存储的写入访问的代码摘录：

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




**从用户的角度**&#x200B;安装后，用户会看到一个窗口，提示他们确认文件的读/写权限（请参阅下图2）。 这会导致以下两个结果之一：

1. 如果用户 **确认** 权限、常规身份验证流程将保留，令牌将存储在全局存储中。 只要令牌有效，用户就会在应用程序中和使用Adobe Primetime身份验证的应用程序之间保持身份验证。
1. 如果用户 **否认** 存储中的权限和写入操作将失败，用户只有在退出应用程序后才会进行身份验证。 请注意，在前台和后台之间切换时，某些应用程序会重新初始化，这样用户在执行此操作时将被注销。 令牌未存储，用户每次使用应用程序时都需要进行身份验证。 


>[!TIP]
>
>目前正在为Adobe Primetime身份验证SDK 1.9开发一项引入存储可复原性的功能。新的SDK针对 **在10月的最后一周发布**. 当无法使用常规存储时，应用程序将回退到在应用程序的沙盒存储中写入内容。 这包括对于在API级别23中开发的应用程序，用户不接受全局存储中的读/写权限的情况。 令牌是按应用程序单独存储的，这意味着将禁用使用Adobe Primetime身份验证的应用程序之间的单点登录。


![](assets/android-permissions-request.png)

*图：针对定向API级别23的应用程序编写的权限请求对话框*

>[!IMPORTANT]
>
> Adobe建议 **其合作伙伴使用API级别22(targetSdkVersion=22)或更低版本开发应用程序，以保证在身份验证过程中获得最佳的用户体验**. 
