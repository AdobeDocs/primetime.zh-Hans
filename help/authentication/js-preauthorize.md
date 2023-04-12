---
title: 预授权
description: JavaScript预授权
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---


# 预授权 {#js-preauthorize}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 概述 {#preauth-overview}

预授权API方法将被应用程序用来获取一个或多个资源的预授权决策。 预授权API请求应用于UI提示和/或内容过滤。 必须先发出实际的授权API请求，然后才允许用户访问指定的资源。

如果在Adobe Primetime身份验证服务处理预授权API请求时发生意外错误（例如，网络问题和MVPD授权端点不可用），则作为预授权API响应结果的一部分，将为受影响的资源包含一个或多个单独的错误信息。

### 公共预授权（请求）：PreauthorizeRequest，回调：AccessEnablerCallback&lt;any>):void {#preauth-method}

**描述：** 此方法将被应用程序用于从Adobe Primetime Authentication Service获取经过验证的用户的预授权（信息）决策，以查看特定的受保护资源，以便装饰应用程序的UI（例如，用锁图标和解锁图标指示访问状态）。

**可用性：** v4.4.0+

**参数：**

* `PreauthorizeRequest`:用于定义请求的生成器对象
* `AccessEnablerCallback`:用于返回API响应的回调
* `PreauthorizeResponse`:用于返回API响应内容的对象

### 类PreauthorizeRequestBuilder {#preath-req-builder-class}

#### setResources(resources:字符串[]):PreauthorizeRequestBuilder {#set-res-preath-req-buildr}

* 设置要获取预授权决策的资源列表。
* 必须为使用预授权API对其进行设置。
* 列表中的每个元素都必须是一个字符串，表示必须与MVPD协议的资源ID值或媒体RSS片段。
* 此方法仅在当前上下文中设置信息 `PreauthorizeRequestBuilder` 对象实例，此方法调用的接收器。

* 构建实际 `PreauthorizeRequest` 你可以看看 `PreauthorizeRequestBuilder`s方法：

```JavaScript
  build(): PreauthorizeRequest
```

* `@param {string[]}` 资源。 要获得预授权决策的资源列表。
* `@returns {PreauthorizeRequestBuilder}` 对同一项的引用 `PreauthorizeRequestBuilder` 对象实例，该实例是方法调用的接收器。
* 这样做可允许创建方法链接。

#### disableFeatures(...功能：字符串[]):PreauthorizeRequestBuilder {#disabl-featres-preauth-req-buildr}

* 设置在获取预授权决策时要禁用这些功能的功能。
* 此函数仅在当前上下文中设置信息 `PreauthorizeRequestBuilder` 对象实例，该实例是此函数调用的接收器。
* 构建实际 `PreauthorizeRequest` 你可以看看 `PreauthorizeRequestBuilder`s函数：

```JavaScript
public func build() -> PreauthorizeRequest
```

* `@param {string[]}` 功能。 您希望禁用这些功能的集合。
* `@returns` 对同一项的引用 `PreauthorizeRequestBuilder` 对象实例，该实例是函数调用的接收器。
* 这样做是为了允许创建函数链。

#### build():PreauthorizeRequest {#preauth-req}

* 创建并检索新的 `PreauthorizeRequest` 对象实例。
* 此方法可实例化新 `PreauthorizeRequest` 对象。
* 此方法使用在当前上下文中预先设置的值 `PreauthorizeRequestBuilder` 对象实例，此方法调用的接收器。
* 请记住，此方法不会产生任何副作用，
* 因此，它不会更改SDK的状态或 `PreauthorizeRequestBuilder` 对象实例，此方法调用的接收器。
* 这意味着，对同一接收机的此方法的后续调用将创建不同的新 `PreauthorizeRequest` 对象实例，但具有相同的信息(如果值设置为 `PreauthorizeRequestBuilder` ，其中未在调用之间进行修改。
* 如果您不需要更新任何提供的信息（资源和缓存），则可以重复使用PreauthorizeRequest实例以多次使用预授权API。
* `@returns {PreauthorizeRequest}`

### 接口AccessEnablerCallback&lt;t> {#interface-access-enablr-callback}

#### onResponse(结果：T); {#on-response-result}

* 在完成预授权API请求后，SDK调用响应回调。
* 结果是成功的结果或包含状态的错误结果。
* `@param {T} result`

#### onFailure(result:T); {#on-failure-result}

* 当无法提供预授权API请求时，SDK调用失败回调。
* 结果是包含状态的失败结果。
* `@param {T} result`

### 类PreauthorizeResponse {#preauth-response-class}

#### 公共状态：状态； {#public-status}

* 返回：失败时的其他状态（状态）信息。
* 可能会持有 `null` 值。

#### 公共决策：决策[]; {#public-decisions}

* 返回：预授权决定的列表。 每个资源一个决策。
* 失败时，列表可能为空。

### 类状态 {#class-status}

#### 公共状态：数字； {#public-status-numbr}

* RFC 7231中所述的HTTP响应状态代码。
* 可能为0，以防 `Status` 来自SDK，而不是Adobe Primetime身份验证服务。

#### 公共代码：数字； {#public-code-numbr}

* 标准Adobe Primetime身份验证服务错误代码。
* 可能包含空字符串或 `null` 值。

#### 公共消息：字符串； {#public-msg-string}

* 在某些情况下由MVPD授权端点或程序员降级规则提供的详细消息。
* 可能包含空字符串或 `null` 值。

#### 公共详细信息：字符串； {#public-details-strng}

* 保存详细消息，在某些情况下，该消息由MVPD授权端点或程序员降级规则提供。
* 可能包含空字符串或 `null` 值。


#### 公共帮助URL:字符串； {#public-help-url-string}

* 链接到此状态/错误发生原因及可能解决方案的更多信息的URL。
* 可能包含空字符串或 `null` 值。

#### 公共跟踪：字符串； {#public-trace-string}

* 此响应的唯一标识符，在联系支持人员以识别更复杂情景中的特定问题时可使用。
* 可能包含空字符串或 `null` 值。

#### 公共操作：字符串； {#public-action-string}

* 建议的修复情况的操作。
   * **无**:很遗憾，没有预定义操作来修正此问题。 这可能表示公共API调用不当
   * **配置**:需要通过TVE仪表板或联系支持人员来更改配置。
   * **申请注册**:应用程序必须重新注册。
   * **身份验证**:用户必须进行身份验证或重新进行身份验证。
   * **授权**:用户必须获得特定资源的授权。
   * **降解**:应采用某种形式的退化。
   * **重试**:重试该请求可能会解决此问题
   * **重试后**:在指定的时间段后重试请求可能会解决此问题。
* 可能包含空字符串或 `null` 值。

### 类决策 {#class-decision}

#### 公共id:字符串； {#public-id-string}

* 获取决策的资源ID。

#### 公共授权：布尔值； {#public-auth-boolean}

* 指示决策是否成功的标记值。

#### 公共错误：状态； {#public-error-status}

* 发生错误时的其他状态（状态）信息。 可能会持有 `null` 值。

## 客户端实施示例 {#client-imp-example}

```JavaScript
let accessEnablerApi = new window.AccessEnabler.AccessEnabler("software statement");
let accessEnablerModels = window.AccessEnabler.models;



// Build request
let requestBuilder = new accessEnablerModels.PreauthorizeRequest.getBuilder();
let request = requestBuilder
    .setResources(["RES01", "RES02", "RES03"])
    .disableFeatures("LOCAL_CACHE")
    .build();



// Create callback
let callback = {
    onResponse(response) {
        // Handle onResponse
    },
    onFailure(response) {
        // Handle onFailure
    }
};

// Invoke call
accessEnablerApi.preauthorize(request, callback);
```


## 方案示例 {#scenario-examples}

### 场景1:所有请求的资源都获得授权 {#all-req-res-auth}

<table>
<thead>
  <tr>
    <th>增强的错误代码标记</th>
    <th>响应</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>已禁用</td>
    <td>

```JavaScript
        {
    "decisions": [
        {
        "id": "RES01",
        "authorized": true
        },
        {
        "id": "RES02",
        "authorized": true
        },
        {
        "id": "RES03",
        "authorized": true
        }
    ]
    }    
```

</td>
  </tr>
</tbody>


### 场景2:已授权一些请求的资源。 {#sm-req-res-auth}

<table>
<thead>
  <tr>
    <th>增强的错误代码标记</th>
    <th>响应</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>已禁用</td>
    <td>

    &quot;&#39;JavaScript
    
    {
    &quot;决定&quot;:[
    {
    &quot;id&quot;:&quot;RES01&quot;,
    “已授权”：true
    },
    {
    &quot;id&quot;:&quot;RES02&quot;,
    “已授权”：false
    },
    {
    &quot;id&quot;:&quot;RES03&quot;,
    “已授权”：true
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>已启用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;决定&quot;:[
    {
    &quot;id&quot;:&quot;RES01&quot;,
    “已授权”：true
    },
    {
    &quot;id&quot;:&quot;RES02&quot;,
    “已授权”：false，
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;:&quot;MVPD在请求对指定资源进行预授权时返回了\&quot;拒绝\&quot;决定。&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;none&quot;
    }
    },
    {
    &quot;id&quot;:&quot;RES03&quot;,
    “已授权”：true
    },
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### 情景3:请求的资源均未获得授权。 {#none-req-res-auth}

<table>
<thead>
  <tr>
    <th>增强的错误代码标记</th>
    <th>响应</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>已禁用</td>
    <td>

    &quot;&#39;JavaScript
    
    {
    &quot;决定&quot;:[
    {
    &quot;id&quot;:&quot;RES01&quot;,
    “已授权”：false
    },
    {
    &quot;id&quot;:&quot;RES02&quot;,
    “已授权”：false
    },
    {
    &quot;id&quot;:&quot;RES03&quot;,
    “已授权”：false
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>已启用</td>
    <td>

    &quot;&#39;JavaScript
    
    {
    &quot;决定&quot;:[
    {
    &quot;id&quot;:&quot;RES01&quot;,
    “已授权”：false，
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;:&quot;MVPD在请求对指定资源进行预授权时返回了\&quot;拒绝\&quot;决定。&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;none&quot;
    }
    },
    {
    &quot;id&quot;:&quot;RES02&quot;,
    “已授权”：false，
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;:&quot;MVPD在请求对指定资源进行预授权时返回了\&quot;拒绝\&quot;决定。&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;none&quot;
    }
    },
    {
    &quot;id&quot;:&quot;RES03&quot;,
    “已授权”：false，
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;maximum_execution_time_exceeded&quot;,
    &quot;message&quot;:“请求未在允许的最长时间内完成。 重试该请求可能会解决此问题。”，
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;retry&quot;
    }
    }
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### 场景4:客户端请求错误 — 未指定资源。 {#bad-cl-req-no-res-sp}

<table>
<thead>
  <tr>
    <th>增强的错误代码标记</th>
    <th>响应</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已禁用/已启用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;status&quot;:{
    &quot;status&quot;:400,
    &quot;code&quot;:&quot;internal_error&quot;,
    &quot;message&quot;:&quot;由于内部错误，请求失败。&quot;,
    “详细信息”：&quot;必需的String[]参数&#39;resource&#39;不存在&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;none&quot;
    },
    &quot;决定&quot;:[]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### 场景5:客户端请求错误 — 指定了空资源。 {#bad-cl-req-empt-res-sp}

<table>
<thead>
  <tr>
    <th>增强的错误代码标记</th>
    <th>响应</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已禁用/已启用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;status&quot;:{
    &quot;status&quot;:412,
    &quot;code&quot;:&quot;missing_resource&quot;,
    &quot;message&quot;:&quot;缺少资源参数&quot;,
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;none&quot;
    },
    &quot;决定&quot;:[]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### 场景6:网络错误。 {#ntwrk-error}

<table>
<thead>
  <tr>
    <th>增强的错误代码标记</th>
    <th>响应</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已启用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;决定&quot;:[
    {
    &quot;id&quot;:&quot;RES01&quot;,
    “已授权”：false，
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;network_received_error&quot;,
    &quot;message&quot;:“从关联的合作伙伴服务检索响应时出现读取错误。 重试该请求可能会解决此问题。”，
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;retry&quot;
    }
    },
    {
    &quot;id&quot;:&quot;RES02&quot;,
    “已授权”：false，
    &quot;error&quot;:{
    &quot;status&quot;:403,
    &quot;code&quot;:&quot;network_received_error&quot;,
    &quot;message&quot;:“从关联的合作伙伴服务检索响应时出现读取错误。 重试该请求可能会解决此问题。”，
    &quot;helpUrl&quot;:&quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;:&quot;retry&quot;
    }
    }
    ]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### 情景7:在没有有效的AuthN会话的情况下调用了预授权流程。

<table>
<thead>
  <tr>
    <th>增强的错误代码标记</th>
    <th>响应</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已禁用/已启用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;status&quot;:{
    &quot;status&quot;:0,
    &quot;code&quot;:&quot;authentication_session_missing&quot;,
    &quot;message&quot;:&quot;无法检索与此请求关联的身份验证会话。 用户必须使用支持的MVPD进行重新身份验证才能继续。”，
    &quot;action&quot;:&quot;authentication&quot;
    },
    &quot;决定&quot;:[]
    }
    
    &quot;

</td>
  </tr>
</tbody>
</table>



### 情景8:在setRequestor调用完成之前调用了预授权流程

<table>
<thead>
  <tr>
    <th>增强的错误代码标记</th>
    <th>响应</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>已禁用/已启用</td>
    <td>

    &quot;&#39;JavaScript
    {
    &quot;status&quot;:{
    &quot;status&quot;:0,
    &quot;code&quot;:&quot;requestor_not_configured&quot;,
    &quot;message&quot;:“尚未配置请求者，这是使用除setRequestor API之外的任何API的先决条件。”，
    &quot;action&quot;:&quot;retry&quot;
    },
    &quot;决定&quot;:[]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

