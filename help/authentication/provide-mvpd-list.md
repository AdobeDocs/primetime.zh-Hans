---
title: 提供MVPD列表
description: 提供MVPD列表
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# 提供MVPD列表 {#provide-mvpd-list}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## REST API端点 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生产 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暂存 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生产 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暂存 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## 描述 {#description}

返回请求者已配置的MVPD列表。

| 端点 | 已调用  </br>按 | 输入   </br>参数 | HTTP  </br>方法 | 响应 | HTTP  </br>响应 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/config/{requestorId}</br></br>例如：</br></br>&lt;sp_fqdn>/api/v1/config/sampleRequestorId | Primetime身份验证 | 1.请求者</br>    （路径组件）</br>_2.  deviceType（已弃用）_ | GET | 包含MVPD列表的XML或JSON。 | 200 |

{style="table-layout:auto"}


| 输入参数 | 描述 |
| --------------- | ------------------------------------------------------------- |
| 请求者 | 此操作有效的程序员请求者ID。 |
| *deviceType* | 设备类型。 |

{style="table-layout:auto"}

### 示例响应 {#sample-response}

与对/config servlet的现有MVPD XML响应相同

注意：配置为使用平台SSO的所有MVPD在其相应节点(JSON/XML)中将具有以下额外属性：

* **enablePlatformServices（布尔）：** 指示此MVPD是否通过平台SSO集成的标记
* **toardingStatus（字符串）：** 指示MVPD是否完全支持平台SSO（受支持）或MVPD是否仅显示在平台选取器(PICKER)中的标记
* **displayInPlatformPicker（布尔）：** 此MVPD是否应显示在平台选取器中
* **platformMappingId（字符串）：** 平台所知的此MVPD的标识符
* **requiredMetadataFields（字符串数组）：** 用户元数据字段应在成功登录时可用
