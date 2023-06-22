---
title: 策略更新列表
description: 策略更新列表
copied-description: true
exl-id: 78078e95-775e-4c64-ab0f-d8bf644f3aee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 策略更新列表 {#policy-update-list}

您可以使用策略更新列表将策略更改传递给许可证服务器。 如果在使用策略打包内容后修改了策略，则最好让许可证服务器知道策略的最新版本，以便版本可用于颁发许可证。

要首次创建策略更新列表，请单击 **[!UICONTROL Add policies]** 查看服务器上的所有可用策略。 对于自用于打包内容以来更新的任何策略，请选择 **[!UICONTROL update]** 单选按钮。

如果您不再希望使用策略来颁发任何许可证，并且该策略已用于打包内容，则您可能希望撤销该策略。 要执行此操作，请选择 **[!UICONTROL revoke]** 单选按钮。 选择所需的策略后，选择 **[!UICONTROL Create Policy Update List]**. 名为的文件 [!DNL PolicyUpdateList.dat] 将保存在 [!DNL Resources] 目录。

要修改现有的策略更新列表，请单击 **[!UICONTROL Add policies]** 查看服务器上的所有可用策略。 选择要添加或撤销的其他策略。 策略更新列表中的现有条目可以在屏幕的上半部分进行更改。 已标记的策略 **[!UICONTROL updated]** 可以更改为 **[!UICONTROL revoked]**，但是一旦策略能够 **[!UICONTROL revoked]**，无法将其改回 **[!UICONTROL updated]**.

完成所需的更改后，选择 **[!UICONTROL Create Policy Update List]**，以及 [!DNL PolicyUpdateList.dat] 文件已重新生成。 如果某个策略已在策略更新列表中，并且自上次生成该列表以来进行了更新，则再次生成策略更新列表时将使用该策略的最新版本。
