---
title: 配置文件属性
description: 配置文件属性
copied-description: true
exl-id: 6405126d-4cf2-4ffc-821d-fbfdc00b60ef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# 配置文件属性 {#configuration-file-properties}

配置文件指定以下属性。 对于包含的属性名称 `n`， `n` 表示一个整数，从1开始，对于属性的每个实例都增大。

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 属性/命令行选项 </th> 
   <th colname="2" class="- topic/entry entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> <i class="+ topic/ph hi-d/i ">policyname</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 易于用户识别的策略名称。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">布尔型</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 如果为true，则向iOS交付密钥需要HTTPS密钥服务器。 如果未指定，则默认值为false。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforceJailbreak</span> <i class="+ topic/ph hi-d/i ">布尔型</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 如果为true，则对于支持越狱检测的设备，如果检测到越狱检测，则不允许播放。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -critical</span> <i class="+ topic/ph hi-d/i ">布尔型</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 设置策略重要性。 如果为true，则服务器必须了解策略的所有部分（这是默认行为）。 如果为false，则服务器可能会忽略它不了解的策略属性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">其公钥用于加密的根加密密钥的许可证服务器证书 <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> 增强型许可证链接 </a>
   此属性指定仅包含证书的文件（可以接受PEM或DER格式）。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">根密钥</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 指定增强型许可证链接的根加密密钥。 如果未指定密钥，并且启用了增强型许可证链接，则会生成随机密钥。 密钥长度必须为16个字节，并指定为十六进制值。 十六进制值之间的空格是可选的。 对于更新，不允许使用命令行选项，并忽略属性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainUrl</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 域服务器的URL（如果需要域注册）。 对于更新，不允许使用命令行选项，并忽略属性。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> 指定是否允许匿名域注册。 将属性设置为true或包含此命令行选项以允许匿名访问。 此选项不能与 — domainAuthNS一起使用。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">命名空间</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 用于域注册的身份验证命名空间。 如果指定，则客户端应使用指定授权机构颁发的用户名和密码进行身份验证。 对于更新，不允许使用命令行选项，并忽略属性。 此选项不能与 — domainAnon一起使用。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">模拟选项</i> </p> </td> 
   <td colname="2" class="- topic/entry ">模拟输出保护约束。 支持以下值： 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 无保护</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 必需</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drm黑名单</span> <i class="+ topic/ph hi-d/i ">名称/值对</i> </p> </td> 
   <td colname="2" class="- topic/entry ">DRM客户端访问受保护内容时受到限制。 此选项指定不能使用的DRM模块的版本列表(阻止列表)。 该值由逗号分隔的名称=值对组成，格式如下： <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">其他名称/值对必须以逗号分隔。 例如： <span class="codeph"> os=Win，release=2.0，arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">名称/值对</i> </p> </td> 
   <td colname="2" class="- topic/entry ">应用程序运行时无法访问受保护的内容。 此选项指定不可使用的运行时模块的版本列表(阻止列表)。 该值由逗号分隔的名称=值对组成，格式如下： <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|版本|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">其他名称/值对必须以逗号分隔。 例如， <span class="codeph"> os=Win，application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">名称/值对</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定访问受保护内容所需的设备功能。 该值由逗号分隔的名称=值对组成，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">例如， <span class="codeph"> nonUserAccessibleBus=false，hardwareRootOfTrust=true</span>. 在更新期间，使用 <span class="codeph"> -devCapabilitiesV1</span> 删除设备功能限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">名称/值对</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定客户端向服务器发送同步消息的频率。 如果未设置，客户端在播放使用此策略保护的内容时将不会发送同步消息。 值由逗号分隔组成 <span class="codeph"> name=value</span> 格式对： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> 开始</span> （必需） — 开始间隔指定自上次同步后经过这么几分钟后，客户端应开始与服务器同步。 </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> 强制</span> （可选） — 强制同步概率是客户端在播放期间强制同步消息的概率(0-100)。 </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span> （可选） — 硬停止间隔是指如果无法同步，客户端将在此时间后无法播放的时间（以分钟为单位）。 如果设置，则必须大于开始时间间隔。 </li> 
     </ul>在更新期间，使用 <span class="codeph"> -sync</span> 删除其余参数，以删除同步要求。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">指示此策略是否具有根许可证(请参阅 <i class="+ topic/ph hi-d/i ">增强型许可证链接</i> 在 <i class="+ topic/ph hi-d/i ">使用Adobe访问保护内容</i>)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">内容有效期的截止日期。 使用格式 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> (例如， <span class="codeph"> 2009-01-31</span> 表示1月31日凌晨12:00)或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> (例如， <span class="codeph"> 2009-01-31-14:30:00</span> 代表1月31日下午2:30)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">内容有效之前的日期。 两者 <span class="codeph"> policy.expiration.endDate</span> 不能同时指定和policy.expiration.duration。 使用格式 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> (例如，2009-01-31-14:30:00表示1月31日下午2:30)。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> 策略过期时间</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">内容的有效时间（以分钟为单位），从打包时开始。 两者 <span class="codeph"> policy.expiration.endDate</span> 和 <span class="codeph"> 策略过期时间</span> 不能同时指定。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证在客户端上可以缓存的时间（以分钟为单位）。 将此属性设置为0可不允许许可证缓存。 该值必须为0或更高。 两者 <span class="codeph"> policy.licenseCaching.duration</span> 和 <span class="codeph"> policy.licenseCaching.endDate</span> 不得同时使用。 </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">注释</b>：此策略设置仅适用于磁盘上的许可证缓存。 它不控制内存缓存的许可证持续时间。 即使策略指定的持续时间为零，也可以在内存中缓存许可证。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不能缓存许可证的截止日期。 两者 <span class="codeph"> policy.licenseCaching.duration</span> 和 <span class="codeph"> policy.licenseCaching.endDate</span> 不得同时使用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示是否允许匿名许可证获取。 如果未指定，则默认值为“false”（需要用户名/密码身份验证）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果要求用户名/密码验证，则此属性为用户名指定可选的名称限定符。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在许可证获取期间由服务器使用的自定义名称/值对。 使用以下格式指定属性： <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">值</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定播放窗口（以分钟为单位），该窗口是许可证在首次用于播放受保护内容后有效的持续时间。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">输出保护约束。 值必须是以下值之一： </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION、USE_IF_AVAILABLE、REQUIRED、NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM模块必须具有指定的最低安全级别（或更高）才能访问受保护的内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">应用程序运行时模块必须具有指定的最低安全级别（或更高）才能访问受保护的内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许播放受保护内容的Adobe AIR或iOS应用程序允许列表。 属性必须使用以下格式： <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[：<span class="+ topic/ph pr-d/codeph codeph">appId</span>[：[<span class="+ topic/ph pr-d/codeph codeph">分钟</span>]：[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许播放受保护内容的SWF应用程序允许列表。 使用以下格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">URL</span> 或文件=<span class="+ topic/ph pr-d/codeph codeph">swf文件</span>，时间=<i class="+ topic/ph hi-d/i ">max_time_to_verify</i> <i class="+ topic/ph hi-d/i ">swf文件</i> 是要计算哈希的SWF文件，并且 <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> 是允许下载和验证SWF完成的最长时间（以秒为单位）。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">要包含在颁发给用户的许可证中的自定义名称/值对。 使用以下格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">值</span> </p> <p class="- topic/p ">可以为多个自定义属性多次定义此选项。 </p> </td> 
  </tr> 
 </tbody> 
</table>
