---
title: 策略工作流详细信息
description: 策略工作流详细信息
copied-description: true
exl-id: e3daf7a9-def0-48a9-8190-adb25eec7b59
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# BEES工作流 {#bees-workflow}

**摘要：**

* **策略**  — 创建DRM BEES感知策略，该策略指示使用此策略打包的所有内容需要BEES。
* **包装**  — 使用蜜蜂感知的DRM策略打包内容。
* **身份验证**  — 对您的客户端设备进行身份验证，并使用Primetime DRM API或Primetime API将此令牌与Primetime云DRM关联。 这样做将导致客户端设备将此身份验证令牌连同所有许可证请求一起发送到Primetime Cloud DRM。 Primetime Cloud DRM不会处理此标记，而是会将其作为不透明blob传递到BEES端点以进行处理。
* **许可**  — 为您的受保护内容请求许可证。 客户端设备会自动将您之前设置的身份验证令牌附加到调用。
* **权利** - Primetime Cloud DRM将确定内容是否与需要BEES的策略一起打包。 Primetime Cloud DRM将构造要发送到BEES端点的JSON请求。 BEES响应将指示Primetime Cloud DRM是否颁发许可证，并可以选择使用哪个DRM策略。

## 策略工作流详细信息 {#policy-workflow-details}

当Primetime Cloud DRM处理许可证请求时，它会解析请求中的DRM策略，以确定是否需要在显示内容之前调用后端授权服务。 如果蜜蜂呼叫 *是* 如果需要，Primetime Cloud DRM将创建BEES请求，然后解析DRM策略以获取BEES请求的指定BEES URL端点。

应用指示BEES要求的DRM策略，在策略中指定以下两个自定义属性：

* `policy.customProp.1=bees.required=<true | false>`
* `policy.customProp.2=bees.url=<url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

例如，使用Primetime DRM策略管理器( [!DNL AdobePolicyManager.jar])，则可在 [!DNL flashaccesstools.properties] 配置文件：

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>如果您已在使用 `policy.customProp.1` 或 `policy.customProp.2` 对于其他资产，只需为较新的资产使用唯一数字即可。

## 包工作流详细信息 {#package-workflow-details}

在打包受Adobe访问保护的内容时，您必须对内容应用一个BEES感知DRM策略。

## 身份验证工作流详细信息 {#authentication-workflow-details}

为了使您的BEES端点做出授权决策，客户端设备必须提供身份验证信息。 您可以使用自己的特定于客户的身份验证令牌来完成此操作。

Primetime Cloud DRM无需了解此令牌，它只需将此令牌传递到BEES端点。 客户端设备负责创建或获取此令牌，并使用 `DRMManager.setAuthenticationToken()` API。

执行以下操作可将此令牌与Primetime Cloud DRM关联，以便随许可证请求一起发送：

实例化 `DRMManager` 对象包含为Primetime云DRM打包的内容的DRM元数据。

此 `setAuthenticationToken()` 方法通过将给定的字节数组与用于实例化的DRM元数据中提供的许可证服务器URL关联来工作 `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

令牌将随所有许可证请求一起发送，直到通过调用清除令牌 `.setAuthenticationToken` 将null作为参数。

## 许可证工作流详细信息{#license-workflow-details}

通过调用，从Primetime Cloud DRM请求许可证 `mgr.loadVoucher()`.

## 权利请求和响应详细信息{#entitlement-request-and-response-details}

当Primetime Cloud DRM确定内容已与BEES感知DRM策略打包时，它会构建以下JSON请求，以发送到DRM策略中指定的BEES端点：

```
{
    "title":"Entitlement Request",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"Unique ID for this message. Used to confirm that the
                           returned response is for this particular message."
        },
        "version": {
            "type":"string",
            "description":"BEES Request Version. Currently 1."
        },
        "contentID": {
            "type":"string",
            "description":"Content ID (GUID)"
        },
        "customerSpecificAuthToken": {
            "type":"string",
            "description":"Base64-encoded authentication token. Must be set
                           explicitly by client before making the license request."
        }
    },
    "required": [
        "messageID",
        "version",
        "contentID"
    ]
}
```

BEES端点应出现以下响应：

```
{
    "title":"Entitlement Response",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"ID of the Entitlement Request that this Response is
                           handling. Must exactly match the ID of the request
                           or this response will be rejected."
        },
        "version": {
            "type":"string",
            "description":"BEES Response Version. Currently 1."
        },
        "isAllowed": {
            "type":"boolean",
            "description":"Grant the license or not."
        },
        "policy": {
            "type":"string",
            "description":"Base64-encoded policy to enforce  If no policy is
                           provided, the policy that was packaged with the content
                           during packaging time will be used to generate the license."
        },
        "error": {
            "type":"integer",
            "description":"An error number produced by the entitlement server.
                           Will be passed to the client as the 'code' field of
                           the server error response."
        },
        "errorText": {
            "type":"string",
            "description":"Additional error information produced by the
                           entitlement server. Will be passed to the client as
                           the 'text' field of the server error response."
        }
    },
    "required": [
        "messageID",
        "version",
        "isAllowed"
    ]
}
```

Primetime Cloud DRM使用该响应来确定它是否应该向请求设备颁发许可证，以及它是否应该将新的DRM策略替换为许可证生成过程。 如果 `isAllowed` 是 `true` 并且响应中没有提供策略，那么在内容打包期间使用的原始DRM策略将用于生成许可证。
