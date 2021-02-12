---
description: 客户端视频播放器或清单服务器可以与CRS交互以实现JIT重新打包。 二者都使用相同的广告选择逻辑。
seo-description: 客户端视频播放器或清单服务器可以与CRS交互以实现JIT重新打包。 二者都使用相同的广告选择逻辑。
seo-title: JIT重新打包的详细工作流
title: JIT重新打包的详细工作流
uuid: 11b6eb3c-f6aa-4018-9b20-ab6f5910508b
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# JIT重新打包的详细工作流{#detailed-workflows-for-jit-repackaging}

客户端视频播放器或清单服务器可以与CRS交互以实现JIT重新打包。 二者都使用相同的广告选择逻辑。

## 清单服务器{#section_1F1C1B7DD146403890C2B43E24FEF0EB}启动的JIT重新打包

![](assets/ssai_JIT-workflow_web.png)

清单服务器端的JIT重新打包的工作流如下：

1. 清单服务器向广告服务器发出请求。
1. 清单服务器接收不是HLS格式的广告创意。
1. 清单服务器向CDN服务器发送广告创意的先前已转码的HLS版本的请求。

   >[!NOTE]
   >
   >在多CDN设置中，清单服务器使用引导URL中的`ptcdn`参数来标识CDN服务器。

1. 清单服务器检查响应：

   1. 如果请求成功，清单服务器会将之前转码的广告创意HLS版本插入到内容流中。
   1. 如果请求失败，清单服务器生成日志条目并从CRS请求转码版本。

1. CRS转码广告创意并将HLS版本上传到CDN服务器以供将来使用。

对于该创意的所有后续请求，清单服务器从CDN检索HLS版本并将其插入到内容流中。

## 客户端{#section_FBC97D40043F4FDD98247A08BB6195B0}启动的JIT重新打包

<!--<a id="fig_hkn_ndt_3z"></a>-->

![](assets/ssai_JIT-workflow_client_web.png)

基于TVSDK或具有类似功能的客户端可以与CRS交互以实现JIT重新打包，如下所示：

1. 客户端从广告服务器请求广告。
1. 广告服务器将广告返回给客户端。
1. 客户端检查广告服务器中的广告格式：

   1. 如果广告创意采用HLS格式，则客户端会将其插入（拼接）内容，然后完成。
   1. 如果广告创意不是HLS格式，则客户端从CDN服务器请求一个。

      >[!NOTE]
      >
      >在多CDN设置中，清单服务器使用引导URL中的`ptcdn`参数来标识CDN服务器。

1. 客户端检查来自CDN服务器的响应。

   1. 如果CDN提供了HLS版本，则客户端将其插入（拼接）内容，然后完成。
   1. 如果CDN服务器不提供HLS版本，则客户端会要求广告服务器从CRS请求一个版本。 客户端不会将广告插入内容。

1. 广告服务器请求将非HLS广告转码到HLS。
1. CRS创建HLS版本并将其上传到CDN服务器以供将来使用。

## 广告格式优先级和时间线{#section_A74DE37A57BF45D7B6D09E3DE40F8E61}

清单服务器和客户端使用相同的选择逻辑来确定用于播放可用广告的优先级。 HLS格式的广告优先级最高，其次是MP4、FLV和WebM。

CRS通常需要2-4分钟来处理非HLS广告创意，通常不到3分钟。

CRS生成不同的HLS比特率，因此广告可以以适合可用连接速度和带宽的速度播放。 如果有多个可用比特率，CRS将选择可用的最高比特率。 如果CRS收到非HLS广告创意，则它将以可用的最高分辨率生成HLS版本。