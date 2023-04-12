---
title: 阻止MVPD在选择对话框中显示
description: 阻止MVPD在选择对话框中显示
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 阻止MVPD在选择对话框中显示

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 问题 {#issue-prevent-mvpd-sel-dialog}

您需要防止（“阻止列表”）特定的MVPD出现在MVPD选择器中。


## 解决方案 {#solution-prevent-mvpd-sel-dialog}

解决方案是在 `displayProviderDialog()` 调用。

例如，如果希望CableCompany_1和CableCompany_2不显示在MVPD选择器内，则需执行类似以下示例中所示的操作。

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if (!isBlocklisted(currentMvpd.ID)) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isBlocklisted(mvpdID) {
    // Implement block-listing on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
} 
```

<!--
**Related Information**

* [Allow MVPDs in the Selection Dialog](/help/authentication/allow-mvpd-selectn-dialog.md)
* **Code samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->