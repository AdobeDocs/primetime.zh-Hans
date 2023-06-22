---
title: 添加请求者
description: 添加请求者
copied-description: true
exl-id: 66d9bc90-8287-4a07-9f60-4263888d5cce
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 添加请求者{#add-requesters}

一个Adobe Primetime DRM授权厂商最多可以有五个请求者。 但是，Adobe建议您限制正在开发Primetime DRM解决方案的个人的请求者数量。 请求者负责将私钥存储到一个安全位置。

1. 管理员使用包含被许可方域名的有效Adobe ID登录到证书注册网站。
1. 在主页上，单击 **[!UICONTROL Add a Requester]**.
1. 在“用户帐户”选项卡上，执行 *一* ，如下所示：

   * 添加用户。

      如果员工拥有Adobe帐户，请输入电子邮件地址。 单击 **[!UICONTROL Add]** 并继续。
   * 邀请用户。

      如果员工没有Adobe帐户，请他们创建一个帐户。 输入员工的电子邮件地址和姓名，然后单击 **[!UICONTROL Send an invitation]**. 站点向被邀请者发送电子邮件邀请。 该电子邮件包含指向adobe.com的链接，被邀请者可以在其中创建帐户。 被邀请人必须使用接收邀请的电子邮件地址。

      >[!NOTE]
      >
      >当用户已创建帐户时，管理员不会收到通知。 查看 **[!UICONTROL User accounts]** 选项卡，以查看受邀者是否已创建帐户。

1. 如果添加了用户，则角色部分屏幕会显示在 **[!UICONTROL User accounts]** 选项卡打开。 执行以下操作：

   1. 确认用户信息正确。
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
      >如果没有 **[!UICONTROL Authorize]** 中的链接 **[!UICONTROL Actions]** 列，则被邀请人尚未创建Adobe帐户。

   1. 确认请求者的信息是否正确。
   1. 输入公司电话号码和挑战短语。

      请求者必须知道此短语才能验证其帐户。
   1. 对于用户类型，选择 **[!UICONTROL Requester]**.
   1. 单击 **[!UICONTROL Save]**.

      用户会收到一封电子邮件，说明其Primetime DRM帐户注册已完成。
