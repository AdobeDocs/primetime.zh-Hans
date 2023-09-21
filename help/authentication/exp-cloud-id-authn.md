---
title: 在Primetime身份验证中使用Experience CloudID
description: 在Primetime身份验证中使用Experience CloudID
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# 在Primetime身份验证中使用Experience CloudID

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

## 什么是Experience CloudID以及如何获取它？ {#what-exp-cloud-id-obtain}

Experience CloudID（简称ECID）是Adobe Experience Cloud为您应用程序/网站中的每个用户生成的唯一ID。 ECID在用于链接多个应用程序/网站中特定Experience Cloud信息的所有用户报表中大量使用。

如果您已具有提供访客ID的系统，则应该对此文档的范围使用同一ID。

获取ECID的一种方法是使用Experience CloudID服务。 您可以使用基于TDM、JS库、服务器端、直接集成或移动设备平台本机库的首选实施类型。 有关可用服务、库、SDK和实施指南的完整视图，请参阅： <https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html>

## 在Primetime身份验证中使用Experience CloudID有何好处？ {#benefit-ex-cloud-id}

如果您将我们的SDK和无客户端REST API配置为使用您的ECID，则以后可以将Primetime身份验证收集的数据链接到您现有的Experience Cloud解决方案中。 这样，您就可以更好地了解客户在Adobe提供的所有解决方案中的历程和体验。

## 如何在Primetime身份验证中使用Experience CloudID？ {#how-to-ex-cloud-id-authn}

在获得ECID（如上所述）后，您需要将这些信息传递到我们的SDK和无客户端REST API。 此信息稍后将在SDK进行的每次网络调用中传递到我们的服务器。 每个SDK的配置过程各不相同，如下所示：

### JS SDK {#js-sdk}

对于JavaScript，您需要将ECID作为第三个参数传递到setRequestor调用。

**使用示例：**

```JavaScript
accessEnabler.setRequestor("REQUESTOR_ID", ["ENDPOINT_URL"],
    {
        "visitorID": "THE_ECID_VALUE"
    }
);
```

### iOS/tvOS SDK {#ios-sdk}

对于iOS/tvOS SDK，有一个名为setOptions的专用方法。

**使用示例：**

```JavaScript
accessEnabler.setOptions(
    [
        "visitorID": "THE_ECID_VALUE"
    ]
);
```

### Android/fireTV SDK {#android-sdk}

对于Android/fireTV SDK，该机制类似于iOS。 只是参数名称不同。 此处记录了API。

**使用示例：**

```JavaScript
String visitor_id = "THE_ECID_VALUE";

HashMap<String, String> options = new HashMap();
options.put("ap_vi",visitor_id);

accessEnabler.setOptions(options);
```

### 无客户端API {#clientless-api}

通过它的REST API使用Adobe Primetime时， **ECID** 应发送值 **在所有API上** 作为参数，名为 **&#39;ap_vi&#39;**.

**使用示例：**

`GET: https://api.auth.adobe.com/api/v1/authorize?...&ap_vi=THE_ECID_VALUE`
