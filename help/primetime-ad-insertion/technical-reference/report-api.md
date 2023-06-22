---
title: 报表API
description: 审核报表API
exl-id: 50eb4869-3765-4591-8c41-794b29d50044
source-git-commit: 628544e38616715e83e0274ba26cf93302ce0e61
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 1%

---

# 报表API {#report-api}

用户界面管理着客户和支持(Adobe)团队的角色。 客户可以访问该门户，然后可以创建和编辑其配置。 用户还可以在用户界面上查看其广告展示次数报表。

API在后台工作，以帮助客户和管理员与后端基础架构通信。

要探索 [!DNL Primetime Ad Insertion] API请参阅 [在Swaggred用户界面中Ad InsertionAPI端点](https://adconfigservice-va6.cloud.adobe.io/swagger-ui/index.html#/).

## API端点 {#report-api-endpoint}

### 生产 {#production}

`https://dai-primetime.adobe.io/report`

### 沙盒 {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## 查询参数


| 名称 | 重要性 | 值类型 | 必需？ | 默认值 | 约束 | 示例/有效示例值 |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | 报表数据的结束日期 | 日期 | Y | 无 | UTC-8中的时间不比昨天晚 | ######## |
| 过滤器 | 在一列或多列上筛选 | 字符串 | N | 无 | ad_config_id ， zone_id | ad_config_id=990,900；state=active |
|  |  |  |  |  | 当请求中的metaData设置为“true”时，您还可以按名称筛选。 |  |
|  |  |  |  |  |  | 多个筛选键以分号分隔。 |
|  |  |  |  |  |  | 使用逗号分隔值提供筛选器键的值列表 |
| groupBy | 按时间（年\|月\|日）或ad_config_id分组。 Adconfig是AdRule的同义词。 | 字符串 | N | 无 | y \| m \| d ， ad_config_id | m ， ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | 对于groupBy on time，提供y或m或d之一 |
|  |  |  |  |  |  |  |



## 标头 {#headers}

| 名称 | 值类型 | 必需 | 示例值 | 重要性 |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| 接受 | 字符串 | Y | text/csv （对于CSV） | API中所需的响应类型 |
|  |  |  | application/json或&#39;*/*&#39;对于JSON |  |
| 授权令牌 | 字符串 | Y | xyz | 授权令牌 |
| x-api-key | 字符串 | Y | xyz | API密钥 |
| x-gw-ims-org-id | 字符串 | Y | xyz12345 | 您帐户的IMS组织ID |

* 您可以按照Adobe.io的JWT身份验证帮助页中详述的步骤生成授权令牌（也称为访问令牌）。
   >[!NOTE]
   >授权令牌的有效期为24小时，因此，如果您使用定期脚本使用报表API，请确保在令牌到期之前或您收到有关令牌无效的Oauth错误时生成授权令牌。

* 要在请求标头中设置正确的值并生成授权令牌（使用JWT身份验证），您需要知道帐户的以下配置。 请联系Primetime支持团队以获取这些值。
技术帐户ID

   * 组织ID
   * Api_key
   * Client_secret

## 输出 {#output}

默认情况下，报表API查询的结果是JSON格式，该格式指定针对所请求维度（groupby参数）的不同值展示的次数。 示例输出如下所示：

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

渲染宏&#39;code&#39;时出错：为参数指定的值无效 `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

下表列出了Report API可以返回的错误代码和消息。 有关与授权层相关的错误，请参阅 [错误代码文档](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) Adobe.io的

| 错误代码 | 错误消息 |
|-----------------------|------------------------------------------|
| 4001007 | 用户详细信息无效。 |
| 4001008 | 所有区域不是来自同一帐户。 |
| 5001010 | 发生内部错误。 |
| 4001011 | 日期未按要求的格式发送。 |
| 4001012 | 日期超出范围。 |
| 4001013 | 缺少必需的参数。 |
| 4001014 | 帐户的区域列表为空。 |
| 4001015 | 请求中的筛选键无效。 |
| 4001016 | 请求中的GroupBy选项无效。 |
| 4001017 | 请求中提供了无效的ID |

## 示例调用和预期结果 {#sample-calls-expected-results}

以下是使用access令牌获取2020-07-01和2021-06-30之间的每月展示次数计数的curl命令：

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
| 获取具有开始和结束日期GET的报表： [API端点]/report？startDate=2020-01-01&amp;endDate=2021-01-01标头：接受= application/json。 或 */* | 包含以下参数的JSON，以及属于此帐户total_impressions的所有广告 |
| 使用GroupBy = d \| m \| yGET获取报表： [API端点]//report？startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y标头：接受= application/json。 或 */* | 包含以下参数的JSON，以及属于此帐户日期(mm-dd-yyyy \| mm-yyyy \| yyyy format) total_impressions |
| 使用GroupBy = ad_config_idGET获取报表： [API端点]/report？startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id标头：接受= application/json。 或 */* | 包含以下参数的JSON，以及属于此帐户ad_config_id total_impressions的所有广告 |
| 使用GroupBy = d \| m \| y和ad_config_idGET获取报表： [API端点]/report？startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d，ad_config_id标头：接受= application/json。 或 */* | 包含以下参数的JSON，以及属于此帐户ad_config_id日期的所有广告(mm-dd-yyyy \| mm-yyyy \| yyyy format) total_impressions |
| 通过metaData=true和groupBy=d \| m \| yGET获取报表： [API端点]/report？startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id标头：接受= application/json。 或 */* | 包含以下参数的JSON，以及属于此帐户ad_config_id名称total_impressions的所有广告 |
| 使用groupBy=d \| m \| y和ad_config_idGET获取报表： [API端点]/report？startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y，ad_config_id标头：接受= application/json。 或 */* | 包含以下参数的JSON，以及属于此帐户ad_config_id名称total_impressions日期（mm-dd-yyyy \| mm-yyyy \| yyyy格式） |
| 获取报告以获取给定日期范围（未分页= true）GET的所有行： [API端点]/report？startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 返回的Json数组中的31个条目 |
| 使用有效的页面查询参数获取报表GET： [API端点]/report？startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 返回的数组中有5个条目 |
| 以csv格式GET获取报表： [API端点]/report？startDate=2020-01-01&amp;endDate=2020-01-10标头：接受=文本/csv | 返回CSV字符串，标头： total_impressions |
| 以csv格式获取报表，且groupBy = d \| m \| yGET： [API端点]/report？startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y标头：接受=文本/csv | 返回CSV字符串，标头： total_impressions日期（mm-dd-yyyy \| mm-yyyy \| yyyy格式） |
| 以csv格式获取报表，元数据= trueGET： [API端点]/report？startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true标头：接受=文本/csv | 返回CSV字符串，标头： total_impressions |
| 提取报表，CSV格式为，metadata = true，groupBy = d \| m \| yGET： [API端点]/report？startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y标头：接受=文本/csv | 返回CSV字符串，标头： total_impressions日期（mm-dd-yyyy \| mm-yyyy \| yyyy格式） |


## 报表API限制策略 {#report-api-throttling-policy}

* 每个用户可在5秒内收到5个API请求。
* 如果用户超过限制，响应将延迟5秒。
* 如果用户在5秒内进行超过10次调用，则将开始被拒绝，并返回响应“429请求过多”。
