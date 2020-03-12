---
seo-title: 策略工作流详细信息
title: 策略工作流详细信息
uuid: b355fcf6-3416-440f-9b30-a155e20f9f74
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# 蜜蜂工作流 {#bees-workflow}

**摘要：**

* **策略** -创建DRM BEES感知策略，该策略指示使用此策略打包的所有内容都需要BEES。
* **打包** -使用BEES-aware DRM策略打包内容。
* **身份验证** -验证您的客户端设备，并使用Primetime DRM API或Primetime API，将此令牌与Primetime Cloud DRM关联。 这样做将导致客户端设备将此身份验证令牌连同所有许可证请求一起发送到Primetime Cloud DRM。 Primetime Cloud DRM将不处理Thistoken，而是将其作为不透明斑点传递给您的BEES端点进行处理。
* **许可** -请求受保护内容的许可。 客户端设备将自动在调用后附加您先前设置的身份验证令牌。
* **权利** - Primetime Cloud DRM将确定内容已与需要BEES的策略打包。 Primetime Cloud DRM将构建JSON请求，以发送到BEES端点。 BEES响应者将指导Primetime Cloud DRM是否颁发许可证以及（可选）使用哪项DRM策略。

## 策略工作流详细信息 {#policy-workflow-details}

当Primetime Cloud DRM处理许可证请求时，它会分析请求中的DRM策略，以确定在显示内容之前是否需要调用后端授权服务。 如果需要BEES *调用* ,Primetime Cloud DRM将创建BEES请求，然后解析DRM策略以获取BEES请求的指定BEES URL端点。

应用指示BEES要求的DRM策略，在策略中指定以下两个自定义属性：

    * &#39;policy.customProp.1=bees.required=&lt;true| false>`
    * &#39;policy.customProp.2=bees.url=&lt;url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

例如，使用Primetime DRM策略管理器( [!DNL AdobePolicyManager.jar])，您可以在配置文件中指定以下两个自定义 [!DNL flashaccesstools.properties] 属性：

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>如果您已经在使用或 `policy.customProp.1` 用于其 `policy.customProp.2` 他属性，只需为较新的属性使用唯一的数字。

## 包工作流详细信息 {#package-workflow-details}

在打包受Adobe Access保护的内容时，您必须对内容应用BEES感知型DRM策略之一。

## 身份验证工作流详细信息 {#authentication-workflow-details}

为了使您的BEES端点做出授权决策，客户端设备必须提供身份验证信息。 您可以使用自己的客户特定身份验证令牌来完成此操作。

Primetime Cloud DRM不必了解此令牌——它只是将此令牌传递到您的BEES端点。 客户端设备负责创建或获取此令牌，并使用 `DRMManager.setAuthenticationToken()` API设置它。

执行以下操作，将此令牌与Primetime Cloud DRM关联，以便与许可证请求一起发送：

使用为 `DRMManager` Primetime Cloud DRM打包的内容的DRM元数据实例化对象。

该方 `setAuthenticationToken()` 法的工作方式是将给定字节数组与用于实例化的DRM元数据中提供的许可证服务器URL相关联 `DRMManager`。

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

通过调用null作为参数来清除令牌，随所有许可证请求一起发送 `.setAuthenticationToken` 该令牌。

## 许可证工作流程详细信息{#license-workflow-details}

致电从Primetime Cloud DRM请求许可证 `mgr.loadVoucher()`。

## 授权请求和响应详细信息{#entitlement-request-and-response-details}

当Primetime Cloud DRM确定内容已与BEES感知型DRM策略一起打包时，它将构造以下JSON请求以发送到DRM策略中指定的BEES端点：

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

BEES端点应该有以下响应：

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

Primetime Cloud DRM使用响应来确定是否应向请求设备发放许可证，以及是否应将新的DRM策略替换到许可证生成过程中。 如果 `isAllowed` 是 `true` 且响应中未提供策略，则在内容打包期间使用的原始DRM策略将用于生成许可证。