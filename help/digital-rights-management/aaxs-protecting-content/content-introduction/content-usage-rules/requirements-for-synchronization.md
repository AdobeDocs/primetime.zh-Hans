---
seo-title: 同步要求
title: 同步要求
uuid: 976a0ae1-bece-437e-b95b-6cd222525d13
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 同步要求{#requirements-for-synchronization}

指定客户端将其状态与服务器同步的频率。 如果客户端已经发出带外许可证（未联系许可证服务器），则使用规则可指定客户端必须向服务器发送同步消息以同步客户端的安全时间并向服务器报告客户端状态。

同步行为是使用以下参数定义的：

* 开始间隔— 指定上次成功同步后等待多长时间以启动另一个同步请求。
* 硬停止间隔— （可选）。 如果在指定的时间段内未成功同步，则不允许播放。
* 强制同步概率— （可选）。 客户端在下一个开始间隔之前发送同步消息的概率。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Adobe Access客户端版本3.0及更高版本支持此使用规则。 旧客户端上的行为取决于许可证服务器支持的最低客户端版本。 请参阅， [最低客户端版本](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md)。

