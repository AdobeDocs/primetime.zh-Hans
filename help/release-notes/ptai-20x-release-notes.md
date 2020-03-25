---
title: PTAI 20.3.3发行说明
description: PTAI 20.3.3发行说明描述了2020年Primetime动态广告插入中的新增功能或变更功能、已解决和已知问题。
translation-type: tm+mt
source-git-commit: ededb36a0b460fff4644a3716b36971ff9454c37

---


# Primetime动态广告插入20.3.3发行说明

动态广告插入20.3.3发行说明描述了2020年Primetime动态广告插入中的新增功能或变更功能、已解决的问题和已知问题。

## PTAI 20.3.3的新增功能

**时间：** 2020年3月26日星期四东部时间凌晨3时至4时

* SSAI 4XX和5XX响应现在可以正确提供与CORS相关的标题，从而允许跨域javascript/webview客户端成功读取错误响应。

* 修复了X-Forwarded-For头的一个问题，该问题导致IPv6地址在传递到广告服务器时未正确进行URL编码。

* 修复了CMAF/已消除混音音频流的一个问题，该问题在某些情况下，EXT-X-MEDIA-SEQUENCE编号增量不正确

## 先前版本中的更改

### 版本

**时间：**

### 版本

**时间：**

## 已解决的问题

如果解决方案与报告的问题相关联，则显示Zendesk引用。 例如ZD#xxxxx。

**PTAI 20.3.3**

* X-Forwarded-For头的问题，当IPv6地址传递到广告服务器时，URL编码不正确。

* CMAF/已消除混音音频流的问题，在某些情况下，EXT-X-MEDIA-SEQUENCE编号在某些情况下增加不正确

## 已知问题和限制

**PTAI 20.3.3**

未添加新限制。
