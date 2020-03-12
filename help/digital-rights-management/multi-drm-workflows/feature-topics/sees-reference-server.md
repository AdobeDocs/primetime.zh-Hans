---
description: 协调许可和策略实施的一种方法是在授权服务器中构建这些功能。 Adobe提供SEES参考授权服务器，您可以使用它来构建自己的服务器。
seo-description: 协调许可和策略实施的一种方法是在授权服务器中构建这些功能。 Adobe提供SEES参考授权服务器，您可以使用它来构建自己的服务器。
seo-title: 参考服务器示例ExpressPlay授权服务器(SEES)
title: 参考服务器示例ExpressPlay授权服务器(SEES)
uuid: 99e42f76-7730-42fc-a9a9-f6396ac12c02
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 参考服务器：示例ExpressPlay授权服务器(SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

协调许可和策略实施的一种方法是在授权服务器中构建这些功能。 Adobe提供SEES参考授权服务器，您可以使用它来构建自己的服务器。

参考服务器SEES演示了ExpressPlay授权服务，其中显示了两个服务：基于基本时间的授权和设备绑定授权。

SEES构建于两个ExpressPlay Fairplay服务之上：

1. Expressplay令牌请求服务
1. Expressplay Retrieving Service

ExpressPlay令牌请求的URL格式采用两种形式，一种用于生产，一种用于测试环境：

**生产**:<span></span>https://fp-gen。{prod_domain}/hms/fp/token

**测试**:<span></span>https://fp-gen.test.expressplay.com/hms/fp/token

ExpressPlay记录检索的URL格式采用两种形式，一种用于生产，一种用于测试环境：

**生产**:<span></span>https://api。{prod_domain}/cmiapi/getrecord/

**测试**:<span></span>https://api.test.expressplay.com/cmiapi/getrecord/
