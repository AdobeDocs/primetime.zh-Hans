---
description: 协调许可和策略实施的一种方法是在授权服务器中构建这些功能。 Adobe提供SEES引用授权服务器，您可以使用它构建自己的服务器。
title: 参考服务器示例ExpressPlay授权服务器(SEES)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# 参考服务器：示例ExpressPlay授权服务器(SEES){#reference-server-sample-expressplay-entitlement-server-sees}

协调许可和策略实施的一种方法是在授权服务器中构建这些功能。 Adobe提供SEES引用授权服务器，您可以使用它构建自己的服务器。

参考服务器SEES演示了ExpressPlay授权服务，显示了两个服务：基于基本时间的授权和设备绑定授权。

SEES构建在两个ExpressPlay Fairplay Services之上：

1. Expressplay令牌请求服务
1. Expressplay记录检索服务

ExpressPlay令牌请求的URL格式有两种形式，一种用于生产，一种用于测试环境:

**生产**:<span></span>https://fp-gen。{prod_domain}/hms/fp/token

**测试**:<span></span>https://fp-gen.test.expressplay.com/hms/fp/token

ExpressPlay Record检索的URL格式有两种形式，一种用于生产，一种用于测试环境:

**生产**:<span></span>https://api。{prod_domain}/cmiapi/getrecord/

**测试**:<span></span>https://api.test.expressplay.com/cmiapi/getrecord/
