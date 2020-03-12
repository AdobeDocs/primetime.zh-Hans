---
seo-title: AIR Publisher ID实用程序概述
title: AIR Publisher ID实用程序概述
uuid: 31aecc0e-ad9b-43ad-ba58-77d2c999f4a4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# AIR Publisher ID实用程序概述 {#air-publisher-id-utility-overview}

作为构建AIR文件过程的一部分，AIR开发人员工具(ADT)生成发布者ID。 这是用于构建AIR文件的证书的唯一标识符。 如果对多个AIR应用程序重用同一证书，则它们将具有相同的发布者ID。AIR发布者ID实用程序用于计算AIR应用程序的发布者ID。 1.5.2之后的AIR版本不将生成的发布者ID写入文件，因此，如果您使用的是AIR应用程序白名单，则必须使用此工具确定发布者ID。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>用于AIR白名单实施的发布者ID与应用程序文件中应用程序发布者指定的发布者ID不相 [!DNL application.xml] 同。

