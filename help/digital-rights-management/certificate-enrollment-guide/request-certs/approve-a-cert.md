---
description: 'null'
seo-description: 'null'
seo-title: 批准证书（帐户或辅助管理员）
title: 批准证书（帐户或辅助管理员）
uuid: 5b95e2e8-abe9-4aef-bcb4-9b98ba6604d1
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# 批准证书（帐户或辅助管理员）{#approve-a-certificate-account-or-secondary-administrator}

1. 登录证书注册站点。
1. 选择&#x200B;**[!UICONTROL Certificates]**&#x200B;选项卡。
1. 检查请求以验证请求是否有效。
1. 如果请求有效，请单击&#x200B;**[!UICONTROL Approve]**。

   您还可以添加评论。 将向请求者发送一封电子邮件，声明请求已经由公司管理员之一批准。 此电子邮件的副本将发送给公司和Adobe管理员。

1. 如果请求无效，请单击&#x200B;**[!UICONTROL Reject]**&#x200B;并在确认对话框中输入注释。

   向请求者发送一封电子邮件，说明请求已被公司管理员之一拒绝。 此电子邮件的副本将发送给公司管理员。

当管理员批准证书请求时，Adobe会验证请求者的身份。 Adobe通过其用户档案中列出的电话号码与请求者联系。

Adobe管理员尝试在三天的时间内与请求者联系两次。 如果Adobe管理员无法联系请求者，他们会留出一条消息请求回叫，或者提供他们再次呼叫的时间。 如果Adobe管理员无法联系到请求者，则向管理员发送电子邮件。

>[!NOTE]
>
>只有帐户和辅助管理员才能更改申请人的公司电话号码和质询短语。

如果验证了请求者的身份，则请求者接收一封包含PKCS#7文件([!DNL p7b])的电子邮件。

请求者可以从电子邮件正文复制PKCS#7内容并将其保存到文件中，或使用附加到电子邮件中的文件。 Adobe建议在保存PKSC#7文件时，使用生成私钥和CSR文件所用的基名。

>[!NOTE]
>
>发送给请求者的文件只包含证书。 文件不包含私钥信息。

