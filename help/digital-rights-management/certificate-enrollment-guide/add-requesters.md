---
title: 添加请求者
description: 添加请求者
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 添加请求者{#add-requesters}

一个Adobe Primetime DRM授权厂商最多可以有5个请求者。 但是，Adobe建议您将请求者的数量限制在开发Primetime DRM解决方案的个人。 请求者负责将私钥存储在安全位置。

1. 管理员使用包含许可证持有者域名的有效Adobe ID登录到证书注册网站。
1. 在主页上，单击 **[!UICONTROL Add a Requester]**.
1. 在“用户帐户”选项卡上，执行 *一* 下列各项之一：

   * 添加用户。

     如果员工有Adobe帐户，请输入电子邮件地址。 单击 **[!UICONTROL Add]** 并继续。
   * 邀请用户。

     如果员工没有Adobe帐户，请邀请他们创建帐户。 输入员工的电子邮件地址和姓名，然后单击 **[!UICONTROL Send an invitation]**. 站点向被邀请者发送电子邮件邀请。 电子邮件包含指向adobe.com的链接，受邀者可以在其中创建帐户。 被邀请人必须使用接收邀请的电子邮件地址。

     >[!NOTE]
     >
     >用户创建帐户后，管理员不会收到通知。 查看 **[!UICONTROL User accounts]** 证书注册网站上的选项卡，以查看受邀者是否已创建帐户。

1. 如果添加了用户，则在中显示的角色部分屏幕 **[!UICONTROL User accounts]** 选项卡打开。 执行以下操作：

   1. 确认用户信息是否正确。
   1. 输入公司电话号码和挑战短语。

      用户必须知道此短语才能验证其帐户。
   1. 对于用户类型，选择 **[!UICONTROL Requester]**.
   1. 单击“保存”。

      请求者会收到一封电子邮件，说明其Primetime DRM帐户注册已完成。

1. 如果您邀请了用户，请执行以下操作：

   1. 登录到证书注册网站。
   1. 选择 **[!UICONTROL User accounts]** 选项卡。
   1. 在中查找用户 **[!UICONTROL Invitations Sent]** 部分并单击 **[!UICONTROL Authorize]**.

      >[!NOTE]
      >
      >如果没有 **[!UICONTROL Authorize]** 中的链接 **[!UICONTROL Actions]** 列中，被邀请人尚未创建Adobe帐户。

   1. 确认请求者的信息是否正确。
   1. 输入公司电话号码和挑战短语。

      请求者必须知道此短语才能验证其帐户。
   1. 对于用户类型，选择 **[!UICONTROL Requester]**.
   1. 单击 **[!UICONTROL Save]**.

      用户将收到一封电子邮件，告知其Primetime DRM帐户注册已完成。
