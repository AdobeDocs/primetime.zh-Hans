---
description: 协调许可和策略实施的一种方法是将这些功能构建到授权服务器中。 Adobe提供了可用于构建您自己的服务器的SEE参考权利文件服务器。
title: 参考服务器示例ExpressPlay授权服务器(SEES)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 参考服务器：示例ExpressPlay授权服务器(SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

协调许可和策略实施的一种方法是将这些功能构建到授权服务器中。 Adobe提供了可用于构建您自己的服务器的SEE参考权利文件服务器。

参考服务器SEE演示了ExpressPlay授权服务，显示两种服务：基本基于时间的授权和设备绑定授权。

SEE基于两种ExpressPlay Fairplay服务构建：

1. Expressplay令牌请求服务
1. Expressplay记录检索服务

ExpressPlay令牌请求的URL格式采用两种形式，一种用于生产，另一种用于测试环境：

**生产**：ht<span></span>tps://fp-gen.{prod_domain}/hms/fp/token

**测试**：ht<span></span>tps://fp-gen.test.expressplay.com/hms/fp/token

用于检索ExpressPlay记录的URL格式采用两种形式，一种用于生产，另一种用于测试环境：

**生产**：ht<span></span>tps://api.{prod_domain}/cmiapi/getrecord/

**测试**：ht<span></span>tps://api.test.expressplay.com/cmiapi/getrecord/
