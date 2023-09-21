---
title: 防止在选择对话框中显示MVPD
description: 防止在选择对话框中显示MVPD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 防止在选择对话框中显示MVPD

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

## 问题 {#issue-prevent-mvpd-sel-dialog}

您需要防止特定于（“阻止列表”）的MVPD出现在MVPD选择器中。


## 解决方案 {#solution-prevent-mvpd-sel-dialog}

解决方法是，在以下情况下执行阻止列表 `displayProviderDialog()` 称为。

例如，如果您希望CableCompany_1和CableCompany_2不显示在MVPD选择器中，则可以执行以下示例中显示的操作。

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
