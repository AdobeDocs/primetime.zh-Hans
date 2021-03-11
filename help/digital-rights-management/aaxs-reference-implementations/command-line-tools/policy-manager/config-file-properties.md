---
title: 配置文件属性
description: 配置文件属性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---


# 配置文件属性{#configuration-file-properties}

配置文件指定以下属性。 对于包含`n`的属性名称，`n`表示从1开始的整数，并且对于属性的每个实例都递增。

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 属性/命令行选项 </th> 
   <th colname="2" class="- topic/entry entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">npolicyname</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 用户可读的策略名称。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">keyServerboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 如果为true，则需要HTTPS密钥服务器才能将密钥投放到iOS。 如果未指定，则默认值为false。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">enforceJailbreakboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 如果为true，则对于支持越狱检测的设备，如果检测到越狱，则不允许播放。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">criticalboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 设置策略关键性。 如果为true，则服务器必须了解策略的所有部分（这是默认行为）。 如果为false，则服务器可能会忽略它不理解的策略属性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.ansymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">许可证服务器证书，其公钥用于加密<a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local">增强许可证链</a>的根加密密钥
   此属性指定仅包含证书的文件（PEM或DER格式可接受）。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">rootKeyroot-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 为“增强许可证链”指定根加密密钥。 如果未指定密钥，并且已启用“增强许可证链”，则将生成随机密钥。 键长必须为16个字节，并指定为十六进制值。 十六进制值之间的空格是可选的。 对于更新，不允许使用命令行选项，并忽略该属性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">domainURLurl</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 域服务器的URL（如果需要域注册）。 对于更新，不允许使用命令行选项，并忽略该属性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> 指定是否允许匿名域注册。 将属性设置为true或包含此命令行选项以允许匿名访问。 此选项不能与 — domainAuthNS一起使用。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">domainAuthNSnamespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 域注册的身份验证命名空间。 如果指定，客户端应使用由指定颁发机构颁发的用户名和密码进行身份验证。 对于更新，不允许使用命令行选项，并忽略该属性。 此选项不能与 — domainAnon一起使用。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">opAnalogAnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">模拟输出保护限制。 支持以下值： 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 必需</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 必需_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">drmBlacklistname/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry ">DRM客户端无法访问受保护的内容。 此选项指定不能使用的DRM模块版本的列表(阻止列表)。 值由逗号分隔的name=value对组成，其格式如下： <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名称/值对必须以逗号分隔。 例如：<span class="codeph"> os=Win，release=2.0,arch=32</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">runtimeBlacklsitname/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry ">应用程序运行时限制访问受保护的内容。 此选项指定不能使用的运行时模块的列表(阻止列表)。 值由逗号分隔的name=value对组成，其格式如下： <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名称/值对必须以逗号分隔。 例如，<span class="codeph"> os=Win，application=AIR</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">名称/值对</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定访问受保护内容所需的设备功能。 值由逗号分隔的name=value对组成，其格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">例如，<span class="codeph"> nonUserAccessibleBus=false，hardwareRootOfTrust=true</span>。 在更新过程中，使用<span class="codeph"> -devCapabilitiesV1</span>（不含其余参数）来删除设备功能限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">syncname/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定客户端向服务器发送同步消息的频率。 如果未设置，则客户端在播放使用此策略保护的内容时不会发送同步消息。 值由逗号分隔的<span class="codeph"> name=value</span>对组成，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 开始|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> 开始</span> （必需） — 开始间隔指定客户端应在上次同步后的这几分钟内与服务器进行开始同步。 </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> force</span> （可选） — 强制同步概率是客户端在播放期间强制同步消息的概率(0-100)。 </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span> （可选） — 硬停止时间间隔是在几分钟之后，如果无法同步，客户端将无法播放。如果设置，则必须大于开始间隔。 </li> 
     </ul>在更新过程中，使用<span class="codeph"> -sync</span>（不含其余参数）来删除同步要求。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">指示此策略是否具有根许可证(请参阅<i class="+ topic/ph hi-d/i ">使用Adobe访问保护内容</i>中的<i class="+ topic/ph hi-d/i ">增强许可证链</i>)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">内容的有效日期。 使用格式<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span>(例如，<span class="codeph"> 2009-01-31</span>表示上午12:00的1月31日)或<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span>(例如，<span class="codeph"> 2009-01-31-14:30:0&lt;a/&gt;代表1月31日下午2:30)。</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">内容的有效日期。 不能同时指定<span class="codeph"> policy.expiration.endDate</span>和policy.expiration.duration。 使用格式<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span>或<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span>(例如，2009-01-31-14:30:00表示1月31日下午2:30)。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">内容的有效时间（以分钟为单位），从打包时开始。 不能同时指定<span class="codeph"> policy.expiration.endDate</span>和<span class="codeph"> policy.expiration.duration</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证在客户端上缓存的时间（以分钟为单位）。 将此属性设置为0可禁止许可证缓存。 值必须为0或更高。 <span class="codeph"> policy.licenseCaching.duration</span>和<span class="codeph"> policy.licenseCaching.endDate</span>不能同时使用。 </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">注意</b>:此策略设置仅应用于磁盘上的许可证缓存。它不控制内存缓存的许可证持续时间。 即使策略指定的持续时间为零，也可以在内存中缓存许可证。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证无法缓存的日期。 <span class="codeph"> policy.licenseCaching.duration</span>和<span class="codeph"> policy.licenseCaching.endDate</span>不能同时使用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示是否允许匿名许可获取。 如果未指定，则默认值为“false”（需要用户名/密码身份验证）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果需要用户名/密码身份验证，则此属性为用户名指定可选的名称限定符。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">要在获取许可证期间由服务器使用的自定义名称/值对。 使用以下格式指定属性：<span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定播放窗口（以分钟为单位），该窗口是许可证在首次用于播放受保护内容时有效的持续时间。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">输出保护限制。 值必须为以下值之一： </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION、USE_IF_AVAILABLE、REQUIRED、NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM模块必须具有指定的最低安全级别或更高级别才能访问受保护的内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">应用程序运行时模块必须具有指定的最低安全级别或更高级别才能访问受保护的内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许播放受保护内容的Adobe AIR或iOS应用程序允许列表。 该属性必须使用以下格式：<span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许播放受保护内容的SWF应用程序允许列表。 使用以下格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">URL</span> 或file<span class="+ topic/ph pr-d/codeph codeph">=swf</span>file<i class="+ topic/ph hi-d/i ">,time=</i> <i class="+ topic/ph hi-d/i ">maxtimeto</i> verifyswf <i class="+ topic/ph hi-d/i ">file是SWF文件，它计算哈希和</i> maxtimetoverify是允许下载和验证SWF完成的最大时间（以秒为单位）。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">要包含在发给用户的许可证中的自定义名称/值对。 使用以下格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> <p class="- topic/p ">可以多次为多个自定义属性定义此选项。 </p> </td> 
  </tr> 
 </tbody> 
</table>

