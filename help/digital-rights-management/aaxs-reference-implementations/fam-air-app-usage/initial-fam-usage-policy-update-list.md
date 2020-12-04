---
seo-title: 策略更新列表
title: 策略更新列表
uuid: ecc74b66-5b53-4ec3-9641-8b78929e2932
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# 策略更新列表{#policy-update-list}

您可以使用策略更新列表将策略更改传达到许可证服务器。 如果在将策略用于打包内容后对其进行了修改，则希望让许可证服务器了解策略的最新版本，以便该版本可用于发布许可证。

要首次创建策略更新列表，请单击&#x200B;**[!UICONTROL Add policies]**&#x200B;以视图服务器上所有可用的策略。 对于自使用策略打包内容以来已更新的任何策略，请选择&#x200B;**[!UICONTROL update]**&#x200B;单选按钮。

如果您不再希望使用策略颁发任何许可证并且该策略已用于打包内容，则可能希望撤销该策略。 为此，请选择&#x200B;**[!UICONTROL revoke]**&#x200B;单选按钮。 选择所需的策略后，选择&#x200B;**[!UICONTROL Create Policy Update List]**。 名为[!DNL PolicyUpdateList.dat]的文件将保存在[!DNL Resources]目录中。

要修改现有的策略更新列表，请单击&#x200B;**[!UICONTROL Add policies]**&#x200B;以视图服务器上的所有可用策略。 选择要添加或撤销的其他策略。 “策略更新”列表中的现有条目可以在屏幕的上半部分进行更改。 标记为&#x200B;**[!UICONTROL updated]**&#x200B;的策略可以更改为&#x200B;**[!UICONTROL revoked]**，但一旦策略为&#x200B;**[!UICONTROL revoked]**，则不能将其更改回&#x200B;**[!UICONTROL updated]**。

完成所需的更改后，选择&#x200B;**[!UICONTROL Create Policy Update List]**，并重新生成[!DNL PolicyUpdateList.dat]文件。 如果策略已在策略更新列表中，且自上次生成列表后已更新策略，则在再次生成策略更新列表时将使用策略的最新版本。
