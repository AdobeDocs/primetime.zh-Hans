---
title: 在Primetime身份验证中使用Experience CloudID
description: 在Primetime身份验证中使用Experience CloudID
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# 在Primetime身份验证中使用Experience CloudID

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 什么是Experience CloudID以及如何获取它？ {#what-exp-cloud-id-obtain}

Experience CloudID（简称ECID）是Adobe Experience Cloud为您的应用程序/网站中的每个用户生成的唯一ID。 ECID在所有Experience Cloud报表中大量使用，这些报表用于将多个应用程序/网站中特定用户的信息链接在一起。

如果您已经有一个提供访客ID的系统，则应在本文档的范围中使用相同的ID。

获取ECID的一种方法是使用Experience CloudID服务。 您可以基于TDM、JS库、服务器端、直接集成或适用于移动平台的本机库，来使用首选实施类型。 有关可用服务、库、SDK和实施指南的全面视图，请参阅：https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-implementation-guides.html





## 在Primetime身份验证中使用Experience CloudID有何好处？ {#benefit-ex-cloud-id}

如果您将我们的SDK和无客户端REST API配置为使用您的ECID，您稍后将能够将Primetime身份验证收集的数据关联到您现有的Experience Cloud解决方案。 这样，您就可以更好地了解Adobe提供的所有解决方案的客户历程和体验。

## 如何在Primetime身份验证中使用Experience CloudID? {#how-to-ex-cloud-id-authn}

获取ECID（如上所述）后，您需要将此信息传递到我们的SDK和我们的无客户端REST API。 此信息稍后将在SDK进行的每次网络调用中传递到我们的服务器。 每个SDK的配置过程都不同，如下所示：

### JS SDK {#js-sdk}

对于JavaScript，您需要在映射中将ECID作为第三个参数传递给setRequestor调用。

**用法示例：**

```JavaScript
accessEnabler.setRequestor("REQUESTOR_ID", ["ENDPOINT_URL"],
    {
        "visitorID": "THE_ECID_VALUE"
    }
);
```

### iOS/tvOS SDK {#ios-sdk}

对于iOS/tvOS SDK，有一个名为setOptions的专用方法。

**用法示例：**

```JavaScript
accessEnabler.setOptions(
    [
        "visitorID": "THE_ECID_VALUE"
    ]
);
```

### Android/fireTV SDK {#android-sdk}

对于Android/fireTV SDK，机制类似于iOS。 只是参数名称不同。 此处介绍了API。

**用法示例：**

```JavaScript
String visitor_id = "THE_ECID_VALUE";

HashMap<String, String> options = new HashMap();
options.put("ap_vi",visitor_id);

accessEnabler.setOptions(options);
```

### 无客户端API {#clientless-api}

通过REST API使用Adobe Primetime时， **ECID** 值应发送 **在所有API上** 作为名为 **&#39;ap_vi&#39;**.

**用法示例：**

`GET: https://api.auth.adobe.com/api/v1/authorize?...&ap_vi=THE_ECID_VALUE`