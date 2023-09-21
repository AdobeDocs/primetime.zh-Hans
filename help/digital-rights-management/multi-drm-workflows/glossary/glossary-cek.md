---
title: 术语表
description: 需要特殊定义的常用术语。
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# 术语表 {#glossary}

需要特殊定义的常用术语。

## 内容加密密钥 {#content-encryption-key}

由实用程序生成的内容加密密钥(CEK)随后由内容打包器用于准备必须受保护的内容。
该实用程序生成长度为16字节的十六进制密钥。
本指南在注释和错误消息、文件和命令示例中显示CEK的参数名称和值名称的以下变体：

* 内容键
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

CEK的文件名如下所示：

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

CEK本身可以存储在密钥管理系统中，也可以进行加密。 本指南将存储索引称为CEK Storage ID CEKSID。 密钥加密密钥(Key Encryption Key， KEK)一词指的是第二级加密密钥，而术语 `ek` 是指该加密的值。
某些调用同时使用CEK和CEK存储ID CEKSID，并且从存储中检索的CEK必须与调用中提供的CEK匹配。
对于FairPlay的HLS Offline，还有 `persistentContentKey` 可设置为过期的。

## 内容加密密钥存储Id {#content-encryption-key-storage-id}

内容加密密钥存储ID (CEKSID)是用于从密钥管理系统中检索内容加密密钥的ID。

CEKSID也称为
* 密钥ID
* 内容Id
* `&kid`

## 客户验证者 {#customer-authenticator}

在对Expressplay API的请求中进行身份验证的密钥。 请求可以包含令牌请求。
