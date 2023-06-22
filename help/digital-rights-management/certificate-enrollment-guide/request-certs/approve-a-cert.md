---
title: 批准证书（帐户或二级管理员）
description: 批准证书（帐户或二级管理员）
copied-description: true
exl-id: 71e647a8-e325-4095-a0ac-775fb5898e9e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 批准证书（帐户或二级管理员）{#approve-a-certificate-account-or-secondary-administrator}

1. 登录到证书注册网站。
1. 选择 **[!UICONTROL Certificates]** 选项卡。
1. 查看请求以验证请求是否有效。
1. 如果请求有效，请单击 **[!UICONTROL Approve]**.

   您还可以添加评论。 会向请求者发送一封电子邮件，声明该请求已获得公司管理员之一的批准。 该电子邮件的副本将发送给公司和Adobe管理员。

1. 如果请求无效，请单击 **[!UICONTROL Reject]** 并在确认对话框中输入注释。

   将向请求者发送电子邮件，说明该请求已被公司管理员之一拒绝。 该电子邮件的副本将发送给公司管理员。

当管理员批准证书请求时，Adobe会验证请求者的身份。 Adobe通过列在其用户档案中的电话号码与请求者联系。

Adobe管理员在三天时间内尝试联系请求者两次。 如果Adobe管理员无法联系请求者，他们会留下请求回叫的消息，或者他们会提供重新回叫的时间。 如果Adobe管理员无法联系到请求者，则会向管理员发送电子邮件。

>[!NOTE]
>
>只有帐户管理员和二级管理员可以更改请求者的公司电话号码和挑战短语。

如果验证请求者的身份，请求者将收到包含PKCS#7文件的电子邮件( [!DNL p7b])。

请求者可以从电子邮件正文中复制PKCS#7内容并将其保存到文件，或者使用附加到电子邮件的文件。 Adobe建议在保存PKSC#7文件时，使用用于生成私钥和CSR文件的基本名称。

>[!NOTE]
>
>发送给请求者的文件仅包含证书。 该文件不包含私钥信息。
