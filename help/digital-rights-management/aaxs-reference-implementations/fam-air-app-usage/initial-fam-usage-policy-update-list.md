---
seo-title: 策略更新列表
title: 策略更新列表
uuid: ecc74b66-5b53-4ec3-9641-8b78929e2932
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 策略更新列表 {#policy-update-list}

您可以使用策略更新列表将策略更改传达到许可证服务器。 如果在将策略用于打包内容后对其进行了修改，则希望许可证服务器了解策略的最新版本，以便使用该版本发布许可证。

要首次创建策略更新列表，请单击以查 **[!UICONTROL Add policies]** 看服务器上所有可用的策略。 对于自使用策略打包内容以来已更新的任何策略，请选择单选 **[!UICONTROL update]** 按钮。

如果您不再希望使用策略来发行任何许可证，并且该策略已用于打包内容，您可能希望撤销该策略。 要执行此操作，请选择单 **[!UICONTROL revoke]** 选按钮。 选择所需的策略后，选择 **[!UICONTROL Create Policy Update List]**。 名为的文 [!DNL PolicyUpdateList.dat] 件将保存在目录 [!DNL Resources] 中。

要修改现有的策略更新列表，请单 **[!UICONTROL Add policies]** 击以查看服务器上的所有可用策略。 选择要添加或撤销的其他策略。 可以在屏幕的上半部分更改“策略更新列表”中的现有条目。 标记的策略可 **[!UICONTROL updated]** 能会更改为 **[!UICONTROL revoked]**，但一旦策略被更改 **[!UICONTROL revoked]**，则不能将其更改回 **[!UICONTROL updated]**。

完成所需的更改后，选择并 **[!UICONTROL Create Policy Update List]**&#x200B;重新生成 [!DNL PolicyUpdateList.dat] 文件。 如果策略已在策略更新列表中且自上次生成列表以来已更新，则在再次生成策略更新列表时将使用策略的最新版本。
