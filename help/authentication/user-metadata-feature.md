---
title: 用户元数据功能
description: 用户元数据功能
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 0%

---



# 用户元数据 {#user-metadata}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>
</br>

## 简介 {#intro}

用户元数据功能使程序员能够访问由MVPD维护的不同类型的用户特定数据。  用户元数据类型包括邮政编码、家长评级、用户ID等。  *用户* 元数据是以前可用的扩展 *静态* 元数据（身份验证令牌TTL、授权令牌TTL和设备ID）。


用户元数据关键点：

- 在验证和授权流程期间传递到程序员的应用程序
- 值保存在令牌中
- 如果不同的MVPD以不同的格式提供数据，则值可以进行标准化
- 某些参数可以使用程序员的密钥（例如邮政编码）进行加密
- 特定值由Adobe通过配置更改提供

## 获取用户元数据 {#obtaining}

程序员可通过AccessEnabler获取用户元数据 `getMetadata()` 函数和通过 `/usermetadata` 端点。  有关使用的详细信息，请参阅平台API文档 `getMetadata()` 及其相应的回调 `setMetadataStatus()` （或用于无客户端API中使用的端点和参数）。

程序员通过为要获取的元数据类型提供键来获取元数据： `getMetadata(key)`.  

返回元数据的方式如下： `setMetadataStatus(key, encrypted, data)`:

| 参数 | 类型 | 描述 |
| ----------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key` | 字符串 | 指定请求的元数据类型 |
| `encrypted` | 布尔值 | 表示是否加密了“value”的布尔标记。 如果为“true”，则“value”实际上将是实际值的JSON Web加密表示形式。 |
| `data` | 对象 | 包含元数据表示形式的JSON对象 |

 

数据参数的结构、值因类型而异：

| 键 | 值类型 | 示例 | 描述 |
| --- | --- | --- | --- |
| `zip` | JSON数组 | \[&quot;77754&quot;, &quot;12345&quot;\] | 邮政编码 |
| `householdID` | JSON字符串 | “1o7241p” | 家庭标识。 如果MVPD不支持子帐户，则与 `userID` |
| `maxRating` | JSON对象 | 美国电影协会：&quot;NR&quot;, <br>  VCHIP:&quot;X&quot;,  <br>  URL:&quot;http://manage.my/parental&quot; } | 用户的家长评分上限 |
| `userID` | JSON字符串 | “1o7241p” | 用户标识符。 如果MVPD支持子帐户，而用户不是主帐户， `userID` 将不同于 `householdID`. |
| `channelID` | JSON数组 | \[&quot;channel-1&quot;, &quot;channel-2&quot; \] | 用户有权查看的渠道列表 |
| `is_hoh` | JSON字符串 | &quot;1&quot; | 标识用户是否是户主的标记 |
| `encryptedZip` | JSON字符串 | &quot;&quot; | Comcast会公开加密的邮政编码 |
| `typeID` | JSON字符串 | 主要 | 标识用户帐户是主帐户还是辅助帐户的标记 |
| `primaryOID` | JSON字符串 | &quot;uuid1e19ec9-012c-124f-b520-acaf118d16a0&quot; | 家庭标识。 如果 `typeID` 为主，将包含 `userID` |
| hba_status | 布尔值 | &quot;true&quot; &quot;false&quot; | 一个布尔标记，用于指示是否为特定集成启用基于主页的身份验证 |
| allowMirroring | 布尔值 | &quot;true&quot; &quot;false&quot; | 指示此设备是否允许进行屏幕镜像 |

>[!NOTE]
>
> **注意：** 如果数据参数已加密，则 **zip密钥**，则元数据键的表示形式将是JSON字符串，而不是数组或对象。


**重要信息：** 程序员可用的实际用户元数据取决于MVPD提供的内容。  必须先与MVPD签署法律协议，然后才能在生产环境中提供敏感用户元数据（例如zipcode）。

</br>


| 名称 | 详细信息 | 需要加密 | 评论 |
| --- | --- | --- | --- |
| 用户ID | 由MVPD提供 | 否 | 该值随后由Adobe进行哈希处理，并在媒体令牌和sendTrackingData()回调中公开。<br><br>本案的哈希处理是出于历史原因<br><br>此ID可以是家庭ID或子帐户ID。 通常不会指定，它只是与当时使用的登录关联的ID（可以是主帐户或子帐户） |
| 上游用户ID | 由MVPD提供，仅用于并发监控流 | 否 | 在MVPD和程序员网站和应用程序中实施并发限制时，会使用此值。 <br><br>ID还可以包含并发监控策略<br><br>对于大多数MVPD，此值等于用户ID |
| 家庭用户ID | 由MVPD提供，主要用于家长控制流 | 否 | 允许程序员了解家庭帐户与子帐户使用情况的ID。<br><br>如果没有提供真正的评级，则有时会将其用作家长控制的替代内容（如果用户使用他们可以观看的家庭帐户登录，则不会显示评级内容）<br><br>在MVPD中，这种表示方式存在很多差异，包括家庭用户ID、户主ID、户旗负责人等。 |
| 户主 | 标志：经常账户是否为户主 | 否 | 请参阅上文 |
| 类型ID /主ID | 家庭帐户标识符 | 否 | AT&amp;T的户主特定指标。<br><br>类型ID =标识用户帐户是否为主/次帐户的标记<br><br>主OID =家庭标识符。 如果TypeID为主，则将包含userID的值 |
| 最大评分 | 当前帐户允许的最大评级 | 否 | 允许程序员过滤掉不适合帐户的内容。<br><br>具有美国电影协会或VCHIP评级 |
| Channel Line Up | 用户包中可用的渠道列表 | 否 | 用于快速允许/删除聚合多个网络的入口中的各种通道</br></br> *请注意，预检授权通常允许此用例具有更大的灵活性，应改用* <br><br>OLCA规范允许在AuthN响应中将此作为AttributeStatement |
| HBA状态 | 指示是否已通过HBA进行了身份验证 | 否 |  |
| 邮政编码 | 用户的账单邮政编码 | 是 | 用于广播或体育活动<br><br>还可以提供AuthZ响应以进行快速更新<br><br>敏感数据，需要MVPD法律协议 |
| 加密的邮政编码 | 用户的账单邮政编码(Comcast) | 是 | 如上所示，但由Comcast加密 |
| 语言 | 用户语言设置 | 否 | 用于根据用户的偏好显示消息 |
| 允许镜像 | 指示此设备是否允许进行屏幕镜像 | 否 |  |



## 可用元数据 {#available_metadata}

下表列出了Adobe Primetime身份验证生态系统中用户元数据的当前状态：


|  | **法律&#x200B;**<br><br>**协议&#x200B;**<br><br>**已签名（仅限zip）** | **用户ID **<br><br>**在AuthN上** | **Zipcode **<br><br>**在AuthN/Z上** | **评级&#x200B;**<br><br>**在AuthN/Z上** | **家庭&#x200B;**<br><br>**AuthN/Z上的ID** | **AuthN上的渠道ID** | **AuthN家庭主管** | **AuthN上的类型ID** | **AuthN上的主OID** | 语言 | 上游用户ID **在AuthN上** | HBA状态 | OnNet | inHome | 允许在AuthZ上镜像 | **注释** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **正式名称** | n/a | `userID` | `zip` | `maxRating` | `householdID` | `channelID` | is_hoh | typeID | primaryOID | 语言 | upstreamUserID | hba_status | onNet | inHome | allowMirroring | 1.对于AuthN — 必须更改OiasmlMetadataParser，以便所有解析器都启用此新属性 <br>2.  对于AuthZ — 没有通用方法，因为授权实施特定于MVPD |
| **需要加密** | n/a | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** |  |
| **敏感** | n/a | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** |  |  |
| **AdobeIdP** | **是** | **是** | **是（仅限AuthN）** | **是（仅限AuthN）** | **是（仅限AuthN）** | **是** | **是** | **是** | **是** | **否** | **是** | **否** | **否** | **否** | **否** | 无需法律协议，即可启用。 |
| **同步** | **是** | **是** | **是（仅限AuthN）** | **是（仅限AuthN）** | **是（仅限AuthN）** | **是** | **是** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **法律协议不涵盖所有代理的MVPD。**   <br>这是对Synacor的一般支持 — 可能未汇总到其所有MVPD。 |
| 碟 | **否** | **是** | **是（仅限AuthN）** | **是（仅限AuthN）** | **是（仅限AuthN）** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 与所有同步MVPD以及upshreamUserID共享相同的列表。 |
| 康卡斯特 | **否** | **是** | **否** | **是（仅限AuthZ）** | **是（仅限AuthZ）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** |  |
| **AT&amp;T** | **是** | **是** | **是（仅限AuthN）** | **否** | **是（仅限AuthN）** | **否** | **否** | **是** | **是** | **否** | **是** | **否** | **否** | **否** | **否** | 已签署法律协议。 |
| **卡布莱维申** | **是** | **是** | **是（仅限AuthN）** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 已签署法律协议。 |
| **HTC** | **否** | **是** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| **马西隆代理** | **是** | **是** | **是（仅限AuthN）** | **否** | **是（仅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 已签署法律协议。 |
| **代理Clearleap** | **是** | **是** | **是（仅限AuthN）** | **是（仅限AuthZ）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** | **否** | 已签署法律协议。 |
| 罗杰斯 | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| RCN | **是** | **是** | **是（仅限AuthN）** | **是（仅限AuthN）** | **是（仅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 宪章 | **是** | **是** | **是（仅限AuthN）** | **是（仅限AuthN）** | **是（仅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| Verizon | **否** | **是** | **是（仅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **否** |  |
| 东联 | **否** | **是** | **是（仅限AuthN）** | **是（仅限AuthN）** | **是（仅限AuthN）** | **是** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 代理GLDS | **否** | **是** | **是（仅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| DTV | **是** | **是** | **是（仅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| COX | **否** | **是** | **是（仅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| 科热科 | **否** | **是** | **是（仅限AuthN）** | **否** | **是（仅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** |  |
| Videotron | **否** | **是** | **是（仅限AuthN）** | **否** | **是*** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | 显示与userID具有相同值的houselID |
| 光谱 | **是** | **是** | **是（仅限AuthN）** | **是（仅限AuthN）** | **是（仅限AuthN）** | **否** | **否** | **否** | **否** | **否** | **是** | **是** | **否** | **否** | **是** |  |
| **所有其他&#x200B;**<br><br>**MVPD** | **否** | **是** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **否** | **是** | **否** | **否** | **否** | **否** | **尚未达成法律协议，敏感元数据不适用于生产环境。**  <br>对于所有MVPD，都可以使用用户ID，而无需额外工作。 |


随着有新类型可用并添加到Adobe Primetime身份验证系统中，用户元数据类型列表将会展开。

## 代码示例 {#code_samples}

- [代码示例1](#code_sample1)
- [代码示例2(Mock getMetadata)](#code_sample2)


### 代码示例1 {#code_sample1}

```
    // Assuming a reference to the AccessEnabler has been previously obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if(status ==1) {
        // User is authenticated, request metadata
        ae.getMetadata("zip");
        ae.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if(encrypted) {
        // The metadata value is encrypted
        // Needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 

### 代码示例2(Mock getMetadata) {#code_sample2}

```
    // Assuming a reference to the AccessEnabler has been
    //   previously obtained and stored in the "ae" variable
     
    // Mock the getMetadata() method
    var aeMock = {
        getMetadata: function(key) {
          var data = null;
          // Set mock data based on the received key,
          // according to the format in the spec
          switch(key) {
            case 'zip': 
              data = [ "1235", "23456" ];
              break;
            case 'maxRating': 
              data = { "MPAA": "PG-13", "VCHIP": "TV-14" };
              break;
            default:
              break;
          }
          // Call the metadata status just like AccessEnabler does
          setMetadataStatus(key, false, data);
        }
     }
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if (status == 1) {
        // User is authenticated, request metadata using mock object
        aeMock.getMetadata("zip");
        aeMock.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the  setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if (encrypted) {
        // The metadata value is encrypted, so it
        //   needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 

有关您特定平台的详细信息，或要在MVPD端如何处理用户元数据方面获得一些洞察，请参阅下面“相关信息”中的相应链接。  

<!---

## Related Information {#related}

- ActionScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- JavaScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- iOS - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaStatus)
- Android - [getMetadata()](#getMetadata), [setMetadataStatus()](#setMetadaStatus)
- Clientless - [AuthN Metadata](#authn_metadata)
- [MVPD Integration Guide: User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
-->
