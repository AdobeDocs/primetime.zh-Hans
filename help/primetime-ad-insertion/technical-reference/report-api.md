---
title: 报表API
description: Auditude报表API
source-git-commit: 7f958c83a4dd481221feb4a266440b920ac7d195
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---


# 报表API {#report-api}

用户界面为客户和启用(Adobe)团队管理了角色。 客户可以访问门户，然后可以创建和编辑其配置。 用户还可以在用户界面上查看其广告展示次数的报表。

API在后台运行，以便客户和管理员能够与后端基础架构进行通信。

## API端点 {#report-api-endpoint}

### 生产 {#production}

`https://dai-primetime.adobe.io/report`

### 沙盒 {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## 查询参数


| 名称 | 显着性 | 值类型 | 强制性？ | 默认值 | 约束 | 示例/有效示例值 |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | 报表数据的结束日期 | 日期 | Y | 无 | 在UTC-8中不比昨天新 | ###### |
| 过滤器 | 过滤一个或多个列 | 字符串 | N | 无 | ad_config_id , zone_id | ad_config_id=990,900;state=active |
|  |  |  |  |  | 在请求中将metaData设置为“true”时，您还可以按名称进行过滤。 |  |
|  |  |  |  |  |  | 多个滤镜键以分号分隔。 |
|  |  |  |  |  |  | 使用逗号分隔值提供过滤键值列表 |
| groupBy | 按时间分组（年\|月\|日）或ad_config_id。 Adconfig是AdRule的同义词。 | 字符串 | N | 无 | y \| m \| d , ad_config_id | m , ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | 对于groupBy ，按时提供y或m或d之一 |
|  |  |  |  |  |  |  |



## 标题 {#headers}

| 名称 | 值类型 | 必需 | 示例值 | 显着性 |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| 接受 | 字符串 | Y | 适用于CSV的文本/CSV | 应从API响应的类型 |
|  |  |  | application/json或&#39;*/*&#x200B;对于JSON为“ ” |  |
| 授权令牌 | 字符串 | Y | xyz | 授权令牌 |
| x-api-key | 字符串 | Y | xyz | API密钥 |
| x-gw-ims-org-id | 字符串 | Y | xyz12345 | 您帐户的IMS组织ID |

* 您可以按照Adobe.io的JWT身份验证帮助页面中详细描述的步骤，生成授权令牌（也称为访问令牌）。
   >[!NOTE]
   >授权令牌的期限为24小时，因此如果您使用的是使用循环脚本的报表API，请确保在授权令牌到期前或收到有关令牌无效的Oauth错误时生成授权令牌。

* 要在请求标头中设置正确的值并生成授权令牌（使用JWT身份验证），您需要了解您的帐户的以下配置。 请联系Primetime支持团队以获取这些值。
技术帐户ID

   * 组织ID
   * Api_key
   * Client_secret

## 输出 {#output}

默认情况下，报表API查询的结果为JSON格式，它根据所请求维度（groupby参数）的不同值指定展示次数。 示例输出如下：

```JSON
[
    {
        "dates": "07-2020",
        "total_impressions": 213007041
    },
    {
        "dates": "08-2020",
        "total_impressions": 174711626
    },
    {
        "dates": "09-2020",
        "total_impressions": 102863153
    }
]
```

## 错误代码和字符串 {#error-codes-strings}

### 错误响应格式 {#error-response-format}

呈现宏“code”时出错：为参数指定的值无效 `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

下表列出了报表API可返回的错误代码和消息。 有关授权层的错误，请参阅 [错误代码文档](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) Adobe.io.

| 错误代码 | 错误消息 |
|-----------------------|------------------------------------------|
| 4001007 | 用户详细信息无效。 |
| 4001008 | 所有区域都不是来自同一帐户。 |
| 5001010 | 发生内部错误。 |
| 4001011 | 日期不以所需格式发送。 |
| 4001012 | 日期超出范围。 |
| 4001013 | 缺少必需参数。 |
| 4001014 | 帐户的区域列表为空。 |
| 4001015 | 请求中的筛选器键无效。 |
| 4001016 | 请求中的GroupBy选项无效。 |
| 4001017 | 请求中提供的ID无效 |

## 示例调用和预期结果 {#sample-calls-expected-results}

以下是使用访问令牌获取2020-07-01到2021-06-30之间每月展示次数计数的curl命令：

**报表API调用示例**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| 示例调用/用例 | 预期结果 |
|---|---|
| 获取包含开始和结束日期的报表GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2021-01-01 header :接受= application/json。 或 */* | 具有以下参数的JSON，以及属于此帐户total_impressions的所有广告 |
| 获取GroupBy = d \| m \| yGET: [API_ENDPOINT]//report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y header :接受= application/json。 或 */* | 具有以下参数的JSON，其中所有广告都属于此帐户日期（mm-dd-yyyy \|mm-yyyy \| yyy格式）total_impressions |
| 获取GroupBy = ad_config_idGET的报表： [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id头：接受= application/json。 或 */* | 具有以下参数的JSON，其中包含属于此帐户ad_config_id total_idimess的所有广告 |
| 获取GroupBy = d \| m \| y和ad_config_idGET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d，ad_config_id头：接受= application/json。 或 */* | 具有以下参数的JSON，其中所有广告都属于此帐户ad_config_id日期（mm-dd-yyyy \| mm-yyyy \| yyy格式）total_impressions |
| 获取MetaData=true且groupBy=d \| m \| yGET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id头：接受= application/json。 或 */* | 具有以下参数的JSON，其中所有广告都属于此帐户ad_config_id名称total_impressions |
| 获取具有groupBy=d \| m \| y和ad_config_idGET的报表： [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y，ad_config_id头：接受= application/json。 或 */* | 具有以下参数的JSON，其中所有广告都属于此帐户ad_config_id名称total_impressions日期（mm-dd-yyyy \|mm-yyyy \| yyyy格式） |
| 获取报表，以获取给定日期范围（未分页= true）的所有GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 返回的Json数组中的31个条目 |
| 获取包含有效页面查询参数的报表GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 返回数组中的5个条目 |
| 获取报表，其中包含csv格式GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10 header :接受= text/csv | 返回带标题的CSV字符串：总展示次数 |
| 获取Report（采用csv格式），并且groupBy = d \| m \| yGET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y标头：接受= text/csv | 返回带标题的CSV字符串：总展示次数日期（mm-dd-yyyy \|mm-yyyy \| yyyy格式） |
| 获取报表（采用csv格式），元数据= trueGET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true头：接受= text/csv | 返回带标题的CSV字符串：总展示次数 |
| 获取报表，采用csv格式， metadata = true， groupBy = d \| m \| yGET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y标头：接受= text/csv | 返回带标题的CSV字符串：总展示次数日期（mm-dd-yyyy \|mm-yyyy \| yyyy格式） |


## 报表API限制策略 {#report-api-throttling-policy}

* 每个用户在5秒的时间范围内允许有5个API请求。
* 如果用户超过上限，则响应将延迟5秒。
* 如果用户在5秒内发起10次以上的调用，他们将开始收到响应“429请求过多”的拒绝请求。
