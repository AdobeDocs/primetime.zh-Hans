---
uuid: 2d927ae8-4c4b-4b64-88b8-9c86430e226c
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# 术语表{#glossary}

需要特殊定义的常用术语。

## 内容加密密钥{#content-encryption-key}

内容加密密钥(CEK)由实用程序生成，随后由内容打包程序在准备必须受保护的内容时使用。
该实用程序以十六进制形式生成长度为16字节的密钥。
本指南在注释和错误消息、文件和命令示例中显示CEK的参数名称和值名称的以下变体：

* 内容密钥
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

CEK的文件名显示为：

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

CEK本身可以存储在密钥管理系统中并加密。 本指南将存储索引称为CEK存储ID CEKSID。 “密钥加密密钥(KEK)”一词指二级加密密钥，“`ek`”一词指该加密的值。
一些调用同时使用CEK和CEK存储ID CEKSID，从存储检索的CEK必须与调用中提供的CEK匹配。
对于使用FairPlay的HLS脱机，还有一个`persistentContentKey`，它可设置为过期。

## 内容加密密钥存储ID {#content-encryption-key-storage-id}

内容加密密钥存储ID(CEKSID)是用于从密钥管理系统检索内容加密密钥的ID。

CEKSID也称为
* 密钥ID
* 内容ID
* `&kid`

## 客户身份验证器{#customer-authenticator}

请求到Expressplay的API时用于验证的密钥。 请求可以包括令牌请求。