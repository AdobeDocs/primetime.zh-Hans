---
description: 'null'
seo-description: 'null'
seo-title: 批准证书（帐户或辅助管理员）
title: 批准证书（帐户或辅助管理员）
uuid: 5b95e2e8-abe9-4aef-bcb4-9b98ba6604d1
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# 批准证书（帐户或辅助管理员）{#approve-a-certificate-account-or-secondary-administrator}

1. 登录“证书登记”站点。
1. 选择选 **[!UICONTROL Certificates]** 项卡。
1. 查看请求以验证请求是否有效。
1. 如果请求有效，请单击 **[!UICONTROL Approve]**。

   您还可以添加评论。 将向请求者发送一封电子邮件，声明请求已由公司管理员之一批准。 此电子邮件的副本将发送给公司和Adobe管理员。

1. 如果请求无效，请单击并 **[!UICONTROL Reject]** 在确认对话框中输入评论。

   将向请求者发送一封电子邮件，声明请求已被公司管理员之一拒绝。 此电子邮件的副本将发送给公司管理员。

管理员批准证书请求后，Adobe将验证请求者的身份。 Adobe会通过其个人资料中列出的电话号码与申请人联系。

Adobe管理员会尝试在三天内两次联系请求者。 如果Adobe管理员无法联系请求者，他们会留出一条消息请求回叫，或者提供再次呼叫的时间。 如果Adobe管理员无法联系到请求者，则会向管理员发送电子邮件。

>[!NOTE]
>
>只有帐户和辅助管理员才能更改公司电话号码和请求者的质询短语。

如果验证请求者的身份，则请求者接收包含PKCS#7文件( [!DNL p7b])的电子邮件。

请求者可以从电子邮件正文中复制PKCS#7内容并将其保存到文件中或使用附加到电子邮件的文件。 Adobe建议在保存PKSC#7文件时，使用用于生成私钥和CSR文件的基本名称。

>[!NOTE]
>
>发送到请求者的文件仅包含证书。 该文件不包含私钥信息。

