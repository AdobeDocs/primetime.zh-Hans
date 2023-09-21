---
title: 在“选择”对话框中允许MVPD
description: 在“选择”对话框中允许MVPD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 在“选择”对话框中允许MVPD {#allow-mvpds-selection-dialog}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

## 问题 {#issue}

在面向最终用户公开之前，程序员可能需要测试或检查新MVPD集成的用户体验。

## 解决方案 {#solution}

在 `displayProviderDialog()` callback，Adobe Primetime身份验证将返回与选定程序员（请求者ID）集成的所有MVPD。 但是，程序员可以在MVPD的返回数组中应用过滤器，并且只显示同时位于两个列表中的那些。

## 示例 {#example}

此示例演示如何在MVPD选择器对话框中仅显示CableCompany_1和CableCompany_2，而不显示CableCompany_NewIntegration。

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if ( isAllowListed(currentMvpd.ID) ) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isAllowListed(mvpdID) {
    // Implement allowlisting on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
}
```

<!--
**Related Information**
* [Prevent MVPDs from appearing in the Selection Dialog](/help/authentication/prevent-mvpd-selectn-dialog.md)
* **Code Samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->
