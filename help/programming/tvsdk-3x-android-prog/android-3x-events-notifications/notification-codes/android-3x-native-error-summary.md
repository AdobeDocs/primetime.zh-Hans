---
title: NATIVE_ERROR通知的详细信息
description: NATIVE_ERROR通知的详细信息
copied-description: true
exl-id: 08121879-d5a6-4224-b08d-9e66fe4d185a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '6888'
ht-degree: 2%

---

# NATIVE_ERROR通知的详细信息 {#details-for-the-native-error-notification}

当TVSDK处理本机错误时，它将以下部分或全部元数据键值作为字符串返回。

<table id="table_7F713B7A56024D8DA3C84E449D09CC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>元数据键名称</b></th> 
   <th colname="col2" class="entry"><b>元数据值</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR_CODE</span> </td> 
   <td colname="col2"> <p>AVE中的本机错误代码。 </p> <p>这些代码表示以下内容： 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">DRM错误（代码3300至3367）。 这些与等效的Flash Player错误代码相同 </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">视频播放错误（–1到89） </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">加密错误（300到307） </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR</span> </td> 
   <td colname="col2">通知的简短描述(例如， <span class="codeph"> AAXS_InvalidVoucher</span> 或 <span class="codeph"> 解码器失败</span>)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 描述</span> </td> 
   <td colname="col2"> 通知的详细描述（例如，广告解析操作失败）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> 字符串形式的数值（例如，“13”）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> 作为字符串(例如， <span class="codeph"> kECNetworkError</span>)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 警告</span> </td> 
   <td colname="col2"> 警告的说明。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 错误</span> </td> 
   <td colname="col2"> 错误描述。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>DRM</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="col2"> DRM模块出现轻微错误。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_STRING</span> </td> 
   <td colname="col2"> 错误描述。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_SERVER_URL</span> </td> 
   <td colname="col2"> TVSDK尝试与之通话的DRM服务器的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>广告清单加载失败</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> 无法加载的内容的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD类型</span> </td> 
   <td colname="col2">广告类型（来自的常量） <span class="codeph"> MediaResource.Type</span> 枚举)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_DURATION</span> </td> 
   <td colname="col2"> 广告持续时间（毫秒）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_ID</span> </td> 
   <td colname="col2"> 分配给广告的ID。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>文件错误</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="col2"> 媒体文件下载过程中错误的描述。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> URL</span> </td> 
   <td colname="col2"> 正在下载的文件的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MANIFEST_ERROR</span> </td> 
   <td colname="col2"> 清单文件下载过程中出错的描述。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="col2">片段期间的错误描述(例如， <span class="codeph"> ts</span>)下载。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>音轨错误</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_名称</span> </td> 
   <td colname="col2"> 未能加载的音频曲目的名称，在清单中指定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_LANGUAGE</span> </td> 
   <td colname="col2"> 清单中指定的音频轨道语言。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>搜寻错误</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_PERIOD</span> </td> 
   <td colname="col2"> 句点的ID（整数）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_POSITION</span> </td> 
   <td colname="col2"> <p>查找的位置（以毫秒为单位）（双精度）。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>其他</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDITUDE_ERROR_CODE</span> </td> 
   <td colname="col2"> 审核错误代码（数字）。 </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR： DRM值 {#section_D240082B93D34902A18C3923C1C717B3}

Adobe视频引擎的视频编码器界面会在以下位置返回这些DRM通知： `NATIVE_ERROR` 元数据对象。

向Adobe报告DRM错误时，请确保包括 `NATIVE_SUBERROR_CODE` 和 `DRM_ERROR_STRING` 以获取故障排除帮助。

>[!TIP]
>
>此列表提供有关错误的特定于TVSDK的信息。 有关完整说明，请参阅 [Adobe Flash Platform的ActionScript运行时错误ActionScript参考](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300).

<table id="table_CD59A859865F4FFDBAA249C89C74770A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>NATIVE_- ERROR_CODE元数据键的值</b></th> 
   <th colname="col2" class="entry"><b>NATIVE_ERROR_NAME元数据键的值</b></th> 
   <th colname="col3" class="entry"><b>含义</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 3300 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidVoucher</span> </td> 
   <td colname="col3"> 
    <ul id="ul_516E4CB32D624B22892DDB9266CB04CA"> 
     <li id="li_348FC0F38B11417994119B61C9244076">分发商的软件应该做什么： 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">如果您使用的是Google Chrome，并且处于无痕模式，而Flash Player版本低于11.6，则可能会发生此错误。 <p>我们建议播放器检查浏览器的版本号，并建议用户退出无痕模式。 </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">再次请求许可证。 <p>如果请求成功，则无需记录或上报。 如果请求不成功，请记录导致错误的内容。 <span class="codeph"> subErrorId</span> 包含行错误（如果存在）。 </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">分发程序应执行的操作： 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">如果Flash低于版本11.6的Chrome以外的配置上的重试不成功，则打包中可能会发生失败。 </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">检查该问题是否特定于某些内容和重新打包。 </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3301 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthenticationFailed</span> </td> 
   <td colname="col3"> <p>服务器无法对客户端进行身份验证或授权。 </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">分发商的软件应采取任何必要的操作来重新建立用户的凭据，或指导用户获取对内容的访问权限。 </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">分发服务器应确认分发服务器的授权和身份验证机制运行正常。 <p>如果分发商不打算使用身份验证或授权功能，则应检查违规内容的策略是否需要身份验证，并参阅诊断策略/许可证差异。 </p> </li> 
    </ul> <p>有关此错误代码的详细信息，请参阅 <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM错误3301原因和解决方法</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3302 </td> 
   <td colname="col2"><span class="codeph"> AAXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>在Access 4.0及更高版本上，当远程密钥URL不使用HTTPS作为方案时，会在iOS上引发此错误。 需要HTTPS。 </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">如果分发服务器使用的版本低于Access v4，或者版本至少为4，但平台不是iOS，则分发服务器的软件应记录该错误。 <p>仅在iOS上引发错误。 </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">如果分发服务器的软件至少为Adobe访问版本4，并且平台为iOS，则分发服务器必须将它们使用的远程密钥服务器URL更改为HTTPS。 <p>如果分发商仅使用HTTP，则可能必须设置HTTPS服务器。 否则，分销商需要提交记录的信息以Adobe并上报问题。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3303 </td> 
   <td colname="col2"><span class="codeph"> aaxs_ContentExpired</span> </td> 
   <td colname="col3"> <p>根据内容提供商设置的规则，您查看的内容已过期。 subErrorId包含特定于客户端的错误或行错误。 </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">分发服务器的软件应尝试从服务器重新获取许可证一次，以确定是否有新的未过期的许可证可用。 <p>如果没有许可证可用或许可证已过期，则允许用户获取新许可证，或者通知用户内容无法观看。如果内容已打包并带有过期日期/结束日期的策略，则许可证服务器将记录报告 <span class="codeph"> PolicyEvaluationException</span> 并声明策略结束日期已过期（服务器错误代码303）。 检查服务器的日志文件以进行验证。 </p> <p>如果可能，客户应检查他们在打包过程中使用的策略，以查看它是否已过期。 Java命令行工具是： <code> java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol</code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">分销商应确认许可证过期日期是否按预期配置。 </li> 
     </ul> </p> <p>有关此错误代码的详细信息，请参阅 <a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> 使用实时流的AMS/FMS的3303（内容已过期）？</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3304 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthorizationFailed</span> </td> 
   <td colname="col3">有关此错误代码的详细信息，请参阅 <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM错误3301原因和解决方法</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3305 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerConnectionFailed</span> </td> 
   <td colname="col3"> <p>由于网络延迟或客户端脱机，与许可证或域服务器的连接超时。 通常，subErrorId包含HTTP返回代码。 </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">分发服务器的软件应尝试与已知正常的服务器建立网络连接。 <p>如果尝试失败，则提示用户重新连接到网络。 如果尝试成功，请将其记录。 </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">分发服务器应验证任何正在使用的许可证和域服务器是否在线并从客户端网络可见。 </li> 
    </ul> <p>有关此错误代码的详细信息，请参阅 <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed]原因和解决方法</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3306 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClientUpdateRequire</span> </td> 
   <td colname="col3"> 使用更新版本的TVSDK for Android。 <p>当前客户端无法完成请求的操作，但更新的客户端可能能够完成请求。 </p> <p>这可能有几个原因： 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">使用的共享域在此客户端上不可用。 当播放在Chrome上运行时，可能出现这种情况，但是其他任何浏览器都无法正常工作，反之亦然。 <p> <p>提示： Chrome使用的PHDS/PHLS密钥与其他浏览器使用的不同。 有关更多信息，请参阅 <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">在5.0之前的iOS版本上运行时，应用程序尝试添加多个DRMSession。 </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">仅支持版本2时，元数据的版本为3或更高版本。 </li> 
     </ul> </p> 
     <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
      <li id="li_7A83869D4262443DA35FA1DF8D3097DD">分发商的软件应提醒用户并中止操作。 <p>如果软件能够确定升级是否可用，则以适合平台的方式将用户引导至该升级。 </p> </li> 
      <li id="li_AF9C2711FDE54DA196EB9D2864632000">如果问题是由共享域引起的，分发服务器将需要向Adobe确认更新的运行时或库。 <p>对于Flash运行时，分发服务器可以直接在其应用程序中强制升级。 对于库，分发服务器将需要获取更新的库，重建其应用程序并将其部署到其用户。 </p> <p>如果由于多个DRMSessions而出现问题，分发服务器将需要更新其应用程序以在添加多个DRMSessions之前检查iOS版本号。 或者，他们可以限制将其应用程序分发到iOS v5及更高版本。 </p> <p>如果由于元数据版本高于版本2而出现问题，则问题可能是元数据已损坏。 他们可以尝试重建元数据并查看结果。 如果他们仍然看到问题，请记录问题并升级至Adobe。 </p> </li> 
     </ul> <p>有关此错误代码的详细信息，请参阅 <a href="https://forums.adobe.com/thread/1266675" format="https" scope="external"> 如何纠正3306 DRMErrorEvent错误代码</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3307 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InternalFailure</span> </td> 
   <td colname="col3"> <p>这通常表示Adobe访问代码中的错误，除非存在如下已知错误，否则属于意外情况。 subErrorId包含特定于客户端的错误或行错误。 </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">如果Windows上的Flash是Chrome，而浏览器版本是11.6(SWF版本19或更高版本)，则分发服务器的软件应假定用户已按下 <span class="uicontrol"> 拒绝</span> 在信息栏上处理相同的数据，如3368。 </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">如果浏览器不是Chrome或Flash版本不是11.6时出现3307，则分发服务器应升级为Adobe。 </li> 
    </ul> <p>重要提示： <span class="codeph"> 3307：1107296344 (FailedToGetBrokerHandle)</span> Chrome浏览器版本24-28中可能会发生这种情况。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3308 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WrongLicenseKey</span> </td> 
   <td colname="col3"> <p>只要使用的许可证包含解密内容的错误密钥，就会引发此错误。 subErrorId包含特定于客户端的错误或行错误。 </p> <p>产生这种错误似乎只有两种方式： 
    <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
     <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">客户已修改用于生成许可证的标准Adobe工具（例如，许可方服务器Java框架）。 <p>在这种情况下，许可证包含可能未与任何内容对应的错误密钥。 </p> </li> 
     <li id="li_21D04ED1F1FA464785BC297D385766FF">客户已使用相同的许可证ID颁发了多个许可证。 <p>在这种情况下，客户端上存在多个与内容元数据匹配的许可证，并且访问代码选择了错误的许可证来使用。 </p> </li> 
    </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">分发服务器的软件应尝试从服务器重新获取许可证。 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">如果没有许可证可用或许可证已过期，请为用户提供获取新许可证的工作流，或者通知用户内容无法观看并记录问题。 </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">如果这是域绑定的内容(适用于AIR)，则提供用户加入域的方法。 </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">分发服务器应： 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">确认他们尚未自定义访问许可证服务器的许可证颁发部分。 </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">验证他们是否为所有许可证颁发了唯一的许可证ID。 </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">使Adobe问题升级。 </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3309 </td> 
   <td colname="col2"><span class="codeph"> aaxs_CorruptedAdditionalHeader </span> </td> 
   <td colname="col3"> <p>如果标头大于65536字节，则会发生这种情况。 </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">分发服务器的软件应记录导致错误的内容段。 </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">分发服务器应确认错误可随特定内容片段重现。 重新打包损坏的内容。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3310 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppIDMismatch </span> </td> 
   <td colname="col3">Android应用程序与正在使用的应用程序不匹配。 <p>未使用正确的AIR应用程序或FlashSWF。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3311 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppVersionMismatch </span> </td> 
   <td colname="col3"> 未使用。 此问题可能仍由AIR中的1.x版本栈栈生成。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3312 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LicenseIntegrity </span> </td> 
   <td colname="col3"> 要解决此问题，请从服务器重新下载许可证。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3313 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WriteMicrosafeFailed </span> </td> 
   <td colname="col3"> <p>当系统无法写入文件系统时，会出现此问题。 <span class="codeph"> subErrorId</span> 包含特定于客户端的错误或行错误。 </p> <p>在Microsoft Windows上，当加密的内容具有licenseID或policyID太长时，Active X或NPAPI插件flash player可能会引发错误3313。 这是因为Windows中的最大路径长度。 （Pepper插件没有此问题。） </p> <p>参见watson 3549660 </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">分发服务器的软件应提示用户确认其用户目录未锁定，也不在已满或已锁定的卷上。 </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">如果分发服务器使用的是AIR而不是Flash，则问题可能是由路径长度限制引起的。 <p>分销商应将其AIR应用程序的名称缩短为一些合理的名称。 此外，请使用更短的重新发布内容 <span class="codeph"> 许可证ID</span> 和 <span class="codeph"> policyID</span>. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3314 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedDRMetadata </span> </td> 
   <td colname="col3"> <p>此错误通常表示内容与测试PKI证书一起打包，并且播放器使用生产PKI构建，反之亦然。 subErrorId包含特定于客户端的错误或行错误。 </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">分发服务器的软件应记录导致该错误的内容段。 </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">分发服务器应确认该错误可随特定内容片段重现。 <p>您可能需要重新打包损坏的内容。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3315 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PermissionDenied </span> </td> 
   <td colname="col3"> <p>存在已知的错误，在预期出现3305时会引发此错误代码。 有关更多信息，请参阅 <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed]原因和解决方法</a>. </p> <p>AIR加载的远程SWF不允许访问Flash Access功能。 如果在网络访问期间发生安全错误，也可能会引发此错误代码。 例如，目标服务器不是使用crossdomain.xml进行连接的客户端，或者无法访问crossdomain.xml。 </p> <p>有关更多信息，请参阅 <a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> DRM错误3315可能的根本原因和解决方法</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3316 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NOTUSED_MOVED </span> </td> 
   <td colname="col3"> 为 <span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPModule</span>. 已移动到3344，因为与Flash错误代码冲突。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3317 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LoadAdobeCPF失败 </span> </td> 
   <td colname="col3"> <p>重要信息：这是一个罕见的错误，通常不会在生产环境中发生。 </p> <p>如果出现错误，您可以执行以下操作之一： 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">如果您使用的是AIR，请重新安装它。 </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">如果您使用的是Flash Player，请下载 <span class="codeph"> AdobeCP</span> 模块。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3318 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncompatibleAdobeCPVersion </span> </td> 
   <td colname="col3"> 不适用于Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3319 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPGetAPI </span> </td> 
   <td colname="col3"> 不适用于Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3320 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HostAuthenticateFailed </span> </td> 
   <td colname="col3"> 不适用于Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3321 </td> 
   <td colname="col2"><span class="codeph"> AAXS_I15n失败 </span> </td> 
   <td colname="col3"> <p>使用密钥设置客户端的过程失败。 subErrorId包含特定于客户端、特定于服务器或行错误。 </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">分发服务器的软件应至少重试一次该操作。 <p>如果您在Windows上使用Google Chrome，请解释如何允许不在沙盒中的插件访问。 有关详细信息，请参阅 <a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> Google Chrome的非沙盒访问被拒绝</a>. </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">分发服务器应完成以下任务之一： 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">如果错误在各个平台之间保持一致，则应通过Adobe使问题升级。 </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">如果错误仅限于Windows上的Chrome，请引导用户允许无沙盒插件访问。 </li> 
      </ul> <p>分发商应将其SWF更新到版本19或更高版本，并且会引发特定于Chrome的3321错误和3368错误。 错误3368可以由分发服务器的软件更具体地处理。 此更改已在Chrome稳定渠道版本26.0.1410.43中引入。 </p> <p>提示：错误 <span class="codeph"> 3321：1090519056</span> Flash Player版本11.1到11.6时可能会发生。我们建议您升级到最新的Flash Player版本。 </p> </li> 
    </ul> <p>有关更多信息，请参阅 <a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> DRM错误3321原因和解决方法</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>全局存储损坏错误</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3322 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DeviceBindingFailed </span> </td> 
   <td colname="col3"> <p>设备似乎与初始化时存在的配置不匹配。 subErrorId包含特定于客户端的错误或行错误。 </p> <p>分发服务器的软件应完成以下任务之一： 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>如果设备未使用Flash Player，而是使用AIR、iOS等，请调用 <span class="codeph"> DRMManager.resetDRMVouchers()</span>. </p> <p>如果iOS上发生问题且处于开发阶段，请要求开发人员确认在从第三方预发行分发系统（例如HockeyApp）下载的内部版本和从Xcode下载的本地内部版本之间进行切换时，是否发现该问题。 在从HockeyApp分发的版本和从Xcode分发的版本之间切换时，不会完全覆盖以前安装的属性。 这种情况可能会触发3322错误。 </p> <p>要解决此问题，开发人员应先从设备中删除旧内部版本，然后再安装新内部版本。 </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">如果设备正在使用Flash Player，并且在3322或3346错误代码中无法使用，请参阅Adobe中有关如何以编程方式重置您的DRM许可证存储区的说明，网址为 <a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> Chrome中的DRM错误3322/3346/3368（信息栏问题）</a>. </li> 
     </ul> </p> <p>此错误不应频繁发生。 在使用漫游配置文件的公司环境中，如果用户正在查看受DRM保护的内容，则当用户从不同计算机登录时，发生错误3322的可能性会增加。 如有可能，分发服务器应尝试从用户处获取此信息。 </p> <p>如果错误频繁发生，请升级至Adobe。 您必须通知Adobe重置许可证存储是否已解决问题，并告知Adobe哪些浏览器上发生了错误。 </p> <p>有关更多信息，请参阅以下文章： 
     <ul id="ul_C468409D1EA046178CA7F54DCDCB84EA"> 
      <li id="li_20C8CA3853574CE486F21E7A3667DAB9"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> https://forums.adobe.com/message/5520902</a> </li> 
      <li id="li_6E6F1BD6FE7843449B3E2F06F342EFF7"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> https://forums.adobe.com/message/5535911</a> </li> 
      <li id="li_2BE40E513A0C4BAD900C7B69FEF5D690"><a href="https://forums.adobe.com/message/5748618" format="https" scope="external"> https://forums.adobe.com/message/5748618</a> </li> 
      <li id="li_9C2BD122E3874E2893DD43E082A877E0"><a href="https://forums.adobe.com/message/6061165" format="https" scope="external"> https://forums.adobe.com/message/6061165</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3323 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptGlobalStateStore </span> </td> 
   <td colname="col3"> <p>DRM客户端使用的文件已被意外修改。 subErrorId包含特定于客户端的错误或行错误。 </p> 
    <ul id="ul_96EA771046CA4B2B9FAE24D493F43FF2"> 
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">分发服务器的软件应引导用户以与3322相同的方式重置。 </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">如果GlobalStore的故障率高于用户群硬盘的预期故障率，请将问题升级至Adobe。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3324 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MachineTokenInvalid </span> </td> 
   <td colname="col3"> 为此应用程序重置DRM本地存储。 调用DRMManager.resetDRM。 <p>许可证服务器可能无法连接到证书吊销列表(CRL)服务器以刷新其CRL文件，或者客户端计算机正在请求许可证服务器已吊销的许可证/身份验证。 </p> <p>在服务器日志中，错误代码111为MachineTokenInvalid。 然而，在客户端级别，错误代码111被转换为错误代码3324。 </p> <p>DRM许可证服务器管理员应检查客户的许可证服务器是否能够检索AdobeCRL文件。 如果客户使用的是Tomcat，则客户可以检查<span class="filepath"> tomcat/temp/</span> 目录以查看是否有4个CRL文件。 </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
      <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">如果文件位于此目录中，双击Windows资源管理器和CRL查看器应用程序中的文件，确定是否有任何文件已过期。 </li> 
      <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">如果tomcat/temp/中没有文件，则可以假定由于防火墙/路由问题，此许可证服务器从未能够访问AdobeCRL服务器。 有关更多信息，请参阅 <a href="https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf" format="http" scope="external"> 防火墙规则。</a></li>
    </ul> </p> <p>如果CRL文件不可用或已过期，则必须确认是否可以访问许可证服务器。 在客户的许可证服务器上打开网络探查器，重新启动服务器，然后让客户端尝试从服务器请求许可证。 您可以观察网络流量，以查看对以下URL端点的调用是否成功： <p>提示：您还可以在浏览器中输入以下CRL URL，以查看是否可以手动下载每个文件。 </p> 
    <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated FlashAccessRuntime/LatestCRL.crl</li> 
    </ul> </p> <p>如果防火墙规则处于打开状态，并且当前没有任何3324错误，则可能是临时网络问题。 检查客户的服务器日志，这些日志可能位于 <span class="codeph"> /tomcat/logs/</span> 目录，以确定许可证服务器尝试获取证书吊销列表时是否出现错误。 <p>重要信息：在续订CRL文件时，如果大量客户端（或突发）向临时网络问题报告3324错误，则可能会发生错误。 网络问题解决后，3324问题也得以解决。 </p> </p> <p>如果所有4个CRL文件都存在于 <span class="filepath"> tomcat/temp/</span> 目录，客户端仍收到3324错误代码，则可能对CRL文件存在文件访问问题。 要解决此问题，您可能需要查看日志并清除现有CRL文件。 </p> <p>如果没有服务器问题，则提示用户在中重置，如3322中所述。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>服务器存储损坏错误</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3325 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptServerStateStore </span> </td> 
   <td colname="col3"> <p>DRM客户端使用的文件已被意外修改。 <span class="codeph"> subErrorId</span> 包含特定于客户端的错误或行错误。 </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">分发服务器的软件应再次重试该操作，因为AdobeCP已在内部删除了违规服务器存储，重试应会成功。 如果重试失败，请记录问题。 </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">如果重试失败率高于用户群硬盘的预期失败率，则将问题升级至Adobe。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3326 </td> 
   <td colname="col2"><span class="codeph"> AAXS_StoreTamperingDetected </span> </td> 
   <td colname="col3"> 调用 <span class="codeph"> DRMManager.resetDRM</span>. <p>许可证存储已被篡改/损坏，无法再使用。 </p> <p>分发服务器的软件应按照3322中所述的方式引导用户进行重置。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3327 </td> 
   <td colname="col2"><span class="codeph"> 检测到AAXS_ClockTampering </span> </td> 
   <td colname="col3"> 固定时钟或获取 <span class="codeph"> 身份验证/许可证/域</span> 再次获得许可证。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>身份验证/许可证/域服务器错误</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3328 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerErrorTryAgrein </span> </td> 
   <td colname="col3"> <p>这是服务器端错误，服务器无法完成来自客户端的请求。 例如，当服务器繁忙、HTTP/500、服务器没有解密请求所需的密钥等情况时，就会发生此错误。 </p> <p>在客户端，无法确定哪里出错。 客户必须查看Adobe访问服务器日志，通常称为 <span class="codeph"> AdobeFlashAccess.log</span>，以确定哪里出错了。 日志中始终存在描述性栈栈跟踪以指示问题。 <span class="codeph"> subErrorId</span> 包含服务器特定的错误或行错误。 </p> <p>分发服务器应查看服务器日志，以识别哪个服务器正在发送此错误。 对于具有子错误代码101的3328错误，服务器无法解密请求。 客户必须验证许可证服务器上安装的许可证/传输服务器证书是否与打包期间使用的证书匹配和相对应。 </p> <p>此外，如果客户使用参考实施，他们必须确保 <span class="codeph"> flashaccess-refimpl.properties</span> 指定主要证书和其他证书的文件。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3329 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ApplicationSpecificError </span> </td> 
   <td colname="col3"> <p>Flash Access不知道特定于应用程序的子错误代码。 <span class="codeph"> subErrorId</span> 包含来自发布服务器自定义许可证服务器的特定于服务器的错误。 服务器在特定于应用程序的命名空间中返回了错误。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3330 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NeedAuthentication </span> </td> 
   <td colname="col3"> <p>当内容配置为在获取许可证之前要求客户端进行身份验证时，会发生此错误。 </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">分发商的软件应该对用户进行身份验证，然后再次获取许可证。 <p>如果您的服务不打算使用身份验证，请记录导致此错误的内容标识。 </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">此错误不应要求提升，除非不应将内容配置为要求身份验证。 <p>在这种情况下，请使用适当的策略重新打包违规内容。 如果内容已正确打包，请参阅诊断策略/许可证差异。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>上面未介绍的许可证实施错误</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3331 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentNotYetValid </span> </td> 
   <td colname="col3"> <p>获得的许可证尚未生效。 要解决此问题，请检查客户端时钟设置是否正确。 要设置客户端时钟，请重新打包内容或修改许可证服务器配置。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3332 </td> 
   <td colname="col2"><span class="codeph"> aaxs_CachedLicenseExpired </span> </td> 
   <td colname="col3"> 从服务器重新获取许可证。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3333 </td> 
   <td colname="col2"><span class="codeph"> aaxs_PlaybackWindowExpired </span> </td> 
   <td colname="col3"> <p>您必须通知用户，在策略过期之前，他们无法播放此内容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3334 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMPlatform </span> </td> 
   <td colname="col3"> <p>不允许此平台播放内容，例如，因为内容提供商已将Adobe访问配置为拒绝对平台上的Adobe访问进行内容访问，或者共享域绑定的许可证已绑定到专用于其他分区的共享域令牌。 </p> <p>如果未使用适当的（CDM功能选通）打包器认证来打包内容，CDM可能会引发此错误。 </p> <p>如果内容与不正确的PHDS/PHLS证书一起打包，则该内容可能在Chrome中有效，但在其他浏览器中无效（反之亦然）。 <p>提示：这是因为Chrome使用不同的PHDS/PHLS证书。 </p>要确认使用了哪个证书，请转储内容元数据的详细信息并查找 <i>收件人证书</i>. 有关更多信息，请参阅 <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3335 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMVersion </span> </td> 
   <td colname="col3"> 升级到Android版TVSDK的最新版本。 <p>要解决此问题，请完成以下任务之一： 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">升级AIR </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">对于Flash Player，请升级AdobeCP模块并重试播放。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3336 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimePlatform </span> </td> 
   <td colname="col3"> <p>不允许此平台播放内容，例如，因为内容提供商已将Access配置为拒绝对平台上的FP/AIR的内容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3337 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimeVersion </span> </td> 
   <td colname="col3"> 升级到Android版TVSDK的最新版本。 <p>如果内容或服务器配置为拒绝播放特定版本的Flash或AIR运行时，则会发生这种情况。 </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">如果用户使用的是可以升级Flash的操作系统，则分发服务器的软件应提示用户升级Flash并重试。 否则，建议用户使用其他计算机。 </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">如果怀疑错误3337s，请确定特定内容是否出现该错误，然后重新打包该内容。 如果内容正确打包，请参阅诊断策略/许可证差异 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3338 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnknownConnectionType </span> </td> 
   <td colname="col3"> <p>无法检测连接类型，策略要求您打开输出保护。 仅当封装的内容需要数字或模拟输出保护时，才可能出现此问题。 </p> <p>早于版本11.8.800.168的Flash Player版本中存在一个问题，该问题会导致在策略指示内容保护的内容上偶尔出现错误3338 <span class="codeph"> 如果可用，则使用</span>. 此问题已在版本11.8.800.168及更高版本中修复。 </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">分发商的软件选择不需要输出保护的内容的变体（例如HD流的SD变体）。 <p>如果错误3338发生在 <span class="codeph"> USE_IF_AVAILABLE </span> 内容，检查播放器版本号。 如果播放器版本低于11.8.800.168，建议用户升级Flash Player。 如果在11.8.800.168以上的版本中出现错误3338，请记录导致该错误的内容。 </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">分发服务器应检查导致此错误的内容，并验证内容的策略是否正在设置 <span class="codeph"> 无保护</span> 或 <span class="codeph"> USE_IF_AVAILABLE</span> 模拟和数字输出。 <p>如果内容无意中打包了 <span class="codeph"> NO_OUTPUT</span> 或 <span class="codeph"> 必需</span>，请重新打包内容。 如果内容正确打包，请参阅诊断策略/许可证差异。 否则，将升级至Adobe。 </p> </li> 
    </ul> <p>有关更多信息，请参阅 <a href="https://forums.adobe.com/message/5518688" format="https" scope="external"> 当DRM策略设置为USE_IF_AVAILABLE时，是否收到意外的3338错误？</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3339 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogPlaybackAllowed </span> </td> 
   <td colname="col3"> 无法在模拟设备上播放。 要解决此问题，请连接数字设备。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3340 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogProtectionAvail </span> </td> 
   <td colname="col3"> 无法播放内容，因为连接的模拟外部显示设备（显示器/电视）没有正确的功能（例如，该设备没有Macrovision或ACP）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3341 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalPlaybackAllowed </span> </td> 
   <td colname="col3"> 无法在数字设备上播放内容。 <p>重要信息：此问题不应在生产环境中发生，因为内容发布者不应禁止数字播放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3342 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalProtectionAvail </span> </td> 
   <td colname="col3"> 连接的数字外部显示设备（显示器/电视）没有正确的功能。 例如，设备没有HDCP。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3343 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IntegrityVerificationFailed </span> </td> 
   <td colname="col3"> <p>不适用于Android。 </p> <p>目前已知此错误最初发生在发布新版本的Flash之后。 发生此错误的原因是Flash在Flash打开时升级，这会使Flash处于不良状态，直到浏览器重新启动。 </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">分发服务器的软件应完成以下任务： 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">建议用户关闭或退出所有浏览器，然后重新打开。 </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">检查Flash的版本是否为当前版本。 <p>如果版本不是最新的，建议客户升级，关闭其浏览器中的所有选项卡，然后重新打开。 </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">如果在成功重新启动浏览器后似乎出现错误，请升级至Adobe。 <p>发布新版本后，我们建议您联系Adobe支持，以查看后台更新问题是否已修复。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3344 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPModule </span> </td> 
   <td colname="col3"> 不适用于Android。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3345 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DRMNoAccessError </span> </td> 
   <td colname="col3"> <p>不适用于Android。 </p> <p>未正确安装Flash或AIR的一部分时，会发生此错误。 </p> <p>分发服务器的软件应执行以下操作之一： 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">要求用户卸载并重新安装AIR。 </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">对于Flash Player，调用 <span class="codeph"> 系统更新</span>. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3346 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MigrationFailed </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">分发服务器的软件应执行以下操作之一： 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">如果AIR，请调用 <span class="codeph"> DRMManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">如果Flash因错误3322或3346错误代码而不可用，则用户应转到 <a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a> 并按照Adobe文章的说明以编程方式重置其DRM许可证存储区。 </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">如果此错误频繁发生，分发服务器应提供要Adobe的频率播放器版本和浏览器版本的详细信息。 </li> 
    </ul> <p>有关更多信息，请参阅以下论坛文章： 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Chrome中的DRM错误3322/3346/3368（信息栏问题）</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> 硬件更改后出现3322或3346错误</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3347 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnfirmedDeviceCapabilites </span> </td> 
   <td colname="col3"> <p>此错误的主要含义是许可证具有客户端的DRM证书指示它无法满足的约束。 在颁发客户端DRM证书时，将定义以下“硬件功能”： 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>非用户可访问总线</b>. 如果 <b>true</b>，解密的媒体绝不会流经总线或进入主内存（应用程序可访问该主内存）。 <p>如果 <b>false</b>，内容在解密后可供应用程序访问。 </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>信任的硬件根目录</b>. 如果 <b>true</b>，则启动时加载到设备上的所有软件均会根据仅在硬件中可用的密钥或摘要进行验证。 <p>当针对客户端的DRM证书打开许可证时，客户端会检查这两个约束，并且故障会立即发生。 在颁发许可证之前，还可以在服务器端检查这些限制。 </p> </li> 
     </ul> </p> <p>此错误的次要含义是许可证设置了“Jailbreak Enforcement”策略，并在设备上检测到越狱。 此检查定期在客户端完成，无法在服务器端检查。 </p> <p>分发商可以更新策略并删除限制。 对于设备功能策略，发出策略更新命令 <span class="codeph"> -devCapabilitiesV1</span> 标记且无参数。 对于越狱执法，设置 <span class="codeph"> policy.enforceJailbreak=false</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3348 </td> 
   <td colname="col2"><span class="codeph"> aaxs_HardStopIntervalExpired </span> </td> 
   <td colname="col3"> 硬停止间隔已过期。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3349 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooHigh </span> </td> 
   <td colname="col3"> 服务器运行的版本高于客户端支持的最高版本。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3350 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooLow </span> </td> 
   <td colname="col3"> 服务器运行的版本低于客户端支持的最低版本。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3351 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenInvalid </span> </td> 
   <td colname="col3"> 域令牌无效。 要解决此问题，请再次向域注册。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3352 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooOld </span> </td> 
   <td colname="col3"> 域令牌早于许可证所需的令牌。 要解决此问题，请再次向域注册。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3353 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooNew </span> </td> 
   <td colname="col3"> 域令牌比许可证所需的令牌新。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3354 </td> 
   <td colname="col2"><span class="codeph"> aaxs_DomainTokenExpired </span> </td> 
   <td colname="col3"> 域令牌已过期。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3355 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainJoinFailed </span> </td> 
   <td colname="col3"> 域加入失败。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3356 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoActivatedRoot </span> </td> 
   <td colname="col3"> 未找到V3叶许可证的根许可证。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3357 </td> 
   <td colname="col2"><span class="codeph"> aaxs_NoValidEmbeddedLicense </span> </td> 
   <td colname="col3"> 未找到有效的嵌入式许可证。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3358 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoACProtectionAvail </span> </td> 
   <td colname="col3"> 无法回放，因为连接的模拟设备没有ACP保护。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3359 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCGMSAProtectionAvail </span> </td> 
   <td colname="col3"> 无法回放，因为连接的模拟设备没有CGMS-A保护。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3360 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainRegistrationRequired </span> </td> 
   <td colname="col3"> 内容需要域注册。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3361 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NotRegisteredToDomain </span> </td> 
   <td colname="col3"> 计算机未注册到指定元数据的域。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3362 </td> 
   <td colname="col2"><span class="codeph"> AAXS_OperationTimeoutError </span> </td> 
   <td colname="col3"> 异步操作花费的时间超过 <span class="codeph"> maxOperationTimeout</span>. 仅由iOS DRMNative Framework返回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3363 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnsupportedIOSPlaylistError </span> </td> 
   <td colname="col3"> 传入的M3U8播放列表包含不支持的内容。 仅由iOS DRMNative Framework返回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3364 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDeviceId </span> </td> 
   <td colname="col3"> <p>框架请求了设备ID，但返回的值为空。 </p> <p>用户不应选择 <span class="uicontrol"> 允许受保护内容的标识符</span> 复选框。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3365 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncognitoModeNotAllowed </span> </td> 
   <td colname="col3"> <p>此浏览器/平台组合不允许在无痕模式下播放受DRM保护的内容。 </p> <p>分发服务器的软件应建议用户退出无痕模式或使用其他浏览器。 有关更多信息，请参阅 <a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> DRM错误3365原因和解决方法</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3366 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadParameter </span> </td> 
   <td colname="col3"> <p>主机运行时使用错误的参数调用了Access库。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3367 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadSignature </span> </td> 
   <td colname="col3"> m3u8清单签名失败。 仅由iOS DRMNative Framework或AVE返回。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3368 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>用户已取消该操作，或已输入不允许访问系统的设置。 </p> <p>仅当SWF版本为19或更高版本时才会引发此错误。 为了向后兼容，当SWF的版本为18或更低版本时，会引发3321。 </p> <p>分发商的软件应引导用户说明如何允许无沙盒插件访问。 有关更多信息，请参阅 <a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> Google Chrome的非沙盒访问被拒绝</a> 和 <a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Chrome中的DRM错误3322/3346/3368（信息栏问题）</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3369 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>所需的浏览器界面不可用。 此问题仅在Pepper上出现。 Flash插件与浏览器版本之间可能存在不匹配。 </p> <p>分发商的软件应指导用户确保他们安装了最新版本的浏览器。 </p> <p> 如果此错误的发生次数增加，并且与正在发布的浏览器更新相对应，请升级至Adobe。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3370 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>用户已禁用 <span class="uicontrol"> 允许受保护内容的标识符</span> 设置。 </p> <p>提示：此错误出现在Pepper 13.0.0.x或更高版本中。 </p> <p>分发服务器的软件应引导用户启用 <span class="uicontrol"> 允许受保护内容的标识符</span> 设置。 </p> <p>分发服务器的操作团队应指导用户启用 <span class="uicontrol"> 允许受保护内容的标识符</span> 设置。 </p> <p>有关更多信息，请参阅 <a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3371 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoOPConstraintInPixel</span><span class="codeph"> 约束</span> </td> 
   <td colname="col3"> <p>基于许可证中的输出保护约束的解析格式不正确。 </p> <p>分发服务器的软件应显示一条错误消息。 要求用户使用内容标题将问题报告给分发服务器。 </p> <p>分发服务器应使用有效策略重新打包内容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3372 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ResolutionLargerThanMaxResolution</span> </td> 
   <td colname="col3"> <p>内容的分辨率大于输出保护约束中指定的最大分辨率。 </p> <p>如果分发商的操作团队在日志中看到此错误，他们应该检查基于解析度的输出保护策略，并在必要时重新打包内容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3373 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_DisplayResolutionLargerThanConstrain</span> </td> 
   <td colname="col3"> <p>内容分辨率大于当前活动输出保护约束指定的分辨率。 </p> <p>如果分发商的操作团队在日志中看到此错误，他们应该检查基于解析度的输出保护策略，并在必要时重新打包内容。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3374 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>在客户端通信处理（例如，请求生成、响应处理、错误的身份验证令牌等）期间失败。 </p> <p>如果分发服务器的操作团队在日志中看到此错误，他们应该检查基于解析度的输出保护策略，并在必要时重新打包内容。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR：视频播放值 {#section_7079501250C2487499639F92EC774525}

AVE的视频编码器界面在中返回这些视频播放通知 `NATIVE_ERROR` 元数据对象。

<table id="table_5EEB1F60E5854452A8B0BABBE9B32651"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>NATIVE_ERROR_CODE元数据键的值</b></th> 
   <th colname="col2" class="entry"><b>NATIVE_ERROR_NAME元数据键的值</b></th> 
   <th colname="col3" class="entry"><b>描述</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> END_OF_PERIOD</span> </td> 
   <td colname="col3"> 期间结束。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> 成功</span> </td> 
   <td colname="col3"> 操作成功。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> 异步操作。 已发出操作请求。 成功/失败信息将在稍后提供。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> 由于文件结束(EOF)条件，无法执行此操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> 解码器失败</span> </td> 
   <td colname="col3"> 解码器在运行时失败。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> 无法打开硬件解码器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> FILE_NOT_FOUND </span> </td> 
   <td colname="col3"> 无法找到资源。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR </span> </td> 
   <td colname="col3"> 一般错误。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> IRRECOVERABLE_ERROR </span> </td> 
   <td colname="col3"> 视频引擎无法从中恢复的错误情况。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE </span> </td> 
   <td colname="col3"> 网络错误，正在尝试恢复。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE </span> </td> 
   <td colname="col3"> 无法确定资源的大小。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> 未实现 </span> </td> 
   <td colname="col3"> 功能未实现。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> 内存不足 </span> </td> 
   <td colname="col3"> 内存不足。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR </span> </td> 
   <td colname="col3"> 分析媒体文件时出错。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> SIZE_UNKNOWN </span> </td> 
   <td colname="col3"> 资源大小不一，但未知。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> UNDER_FLOW </span> </td> 
   <td colname="col3"> 下溢条件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_CONFIG </span> </td> 
   <td colname="col3"> 不支持配置。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> 不受支持的操作 </span> </td> 
   <td colname="col3"> 不支持此操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT </span> </td> 
   <td colname="col3"> 尚未初始化。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER </span> </td> 
   <td colname="col3"> 参数无效。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19 </td> 
   <td colname="col2"><span class="codeph"> 无效操作</span> </td> 
   <td colname="col3"> 不允许执行该操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> 该操作仅在暂停时允许。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> 无法在仅音频文件上使用操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> 上一步_寻找_进行中</span> </td> 
   <td colname="col3"> 上一个搜寻操作仍在进行中。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED </span> </td> 
   <td colname="col3"> 未指定资源。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> 指定的值超出范围。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEEK_TIME</span> </td> 
   <td colname="col3"> 搜寻时间无效。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> 指定的文件不符合预期的语法。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAIL</span> </td> 
   <td colname="col3"> 无法创建基本组件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> 无法创建DRM上下文。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORT </span> </td> 
   <td colname="col3"> 不支持容器类型。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> 搜寻失败</span> </td> 
   <td colname="col3"> 搜寻失败。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORT</span> </td> 
   <td colname="col3"> 不支持的编解码器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_UNAVAILABLE</span> </td> 
   <td colname="col3"> 网络不可用。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_ERROR</span> </td> 
   <td colname="col3"> 从网络获取数据时出错。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> 溢出</span> </td> 
   <td colname="col3"> 溢出。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORT</span> </td> 
   <td colname="col3"> 不支持的视频配置文件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> 在HOLD时段或尚未加载的时段上尝试了操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> 指定的替换持续时间无效或超出流结尾。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> CALLED_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> 无法从错误的线程中调用API。 通常，适用于只应从主线程中调用的API元素。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> 片段读取错误。 不存在故障转移。 引擎将尝试读取下一个片段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> 已中止</span> </td> 
   <td colname="col3"> 该操作已被显式Abort或销毁调用中止。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> 无法播放此版本的HLS媒体。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> 无法故障转移。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> HTTP下载已超时。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_DOWN </span> </td> 
   <td colname="col3"> 用户的网络连接已断开。 播放可能会随时停止，并将在连接可用时恢复。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> 在流中未找到可用的比特率配置文件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> 清单的签名无效。 它未能通过清单签名测试。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> 无法加载播放列表。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> 插入API中指定的替换无法成功。 这意味着插入成功，但替换失败。 如果要替换的清单已从时间线中移除，则替换可能会失败。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM正在切换到非对称配置文件。 所有用户档案的持续时间应保持一致。 如果不存在，则会引发此警告，并且播放过程中可能会出现跳转。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> 实时窗口应仅向前移动。 否则，将引发此警告，并且不会读取窗口。 因此，播放过程中可能会出现跳转（或停止/长时间暂停）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> 实时窗口移动到当前时段之外。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> HTTP服务器报告的内容长度与实际媒体大小不匹配。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> 媒体读取器无法进一步读取，因为它已达到setHoldAt API设置的时间。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD </span> </td> 
   <td colname="col3">媒体读取器无法加载区段，因为它已到达实时窗口的结尾。 当服务器向实时窗口添加新媒体时，将继续加载区段。 通常达到此状态的情况是： 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">此 <span class="codeph"> bufferTime</span> 过高（等于或大于实时窗口持续时间）。 </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">插入/擦除API的一个或多个组合替换了比添加的多媒体。 </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">下一个时段是具有挂起的媒体替换的实时时段（由于InsertBy API调用） </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING </span> </td> 
   <td colname="col3"> 媒体中的音频和视频交错处理不正确。 这是一个打包错误。 当差值超过两秒时，将调度警告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> 尚未在Flash Player中启用HLS播放。 请参阅AuthorizedFeatures.enableHLSPlayback。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> 解码器接收到无法解码的坏样本。 这通常不是致命错误，但表示音频/视频中可能有故障。 此错误的实例太多，表示编码错误或文件错误。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> 开始播放后，“插入”/“替换”范围不应包含读取头。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> 不允许对实时媒体进行后置式插入。 但是，在服务器将媒体标记为完成之后，才允许设置这些值。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> INTERNAL_ERROR</span> </td> 
   <td colname="col3"> 这是一个非常罕见的问题，绝不应该发生。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> 流不遵循始终将H264 SPS/PPS放入AVCC中的打包建议。 可能会出现搜寻/播放问题。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARTIAL_REPLACEMENT</span> </td> 
   <td colname="col3"> 插入API中指定的替换仅部分完成。 当replaceDuration跨越时间线持续时间时会发生这种情况。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> 加载演绎版播放列表时出错。 这仅适用于AVE，不适用于FlashPlayer。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL操作</span> </td> 
   <td colname="col3"> 操作不执行任何操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILED</span> </td> 
   <td colname="col3"> 无法播放区段，因失败而跳过。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> INCOMPATIBLE_RENDER_MODE</span> </td> 
   <td colname="col3"> 渲染模式不兼容。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORT </span> </td> 
   <td colname="col3"> 不支持URL中使用的Web协议。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> 解析媒体文件时出错。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTED_CHANGED</span> </td> 
   <td colname="col3"> 清单文件以意外的方式更改。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> 无法对时间轴执行拆分操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> 无法对时间轴执行擦除操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_NEXT_GET</span> </td> 
   <td colname="col3"> 没有获得下一个片段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> 内部数据结构中不存在时间轴。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> 在内部数据结构中未找到侦听器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> 无法启动音频。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> 内部数据结构中不存在音频接收器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> 无法打开文件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> 无法写入文件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> 无法从文件读取。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> 解析ID3数据时出错。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> 安全性_错误 </span> </td> 
   <td colname="col3"> 由于安全限制，加载内容失败。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> 时间轴_TOO_SHORT</span> </td> 
   <td colname="col3"> 时间线持续时间太短。 如果这是实时流，则可能会发生频繁缓冲。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> 流已切换为纯音频流。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> 流已从纯音频流切换为带有视频的流。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> KEY_NOT_FOUND </span> </td> 
   <td colname="col3"> 找不到键。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> 密钥无效。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> 密钥服务器未返回密钥。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> 无法处理主清单更新。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> 未报告的_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> 发现未报告的时间(PTS)中断。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNMATCHED_AV_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> 发现不匹配的音频和视频中断。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">在中播放媒体时出现错误 <i>特技游戏</i> 模式。 结束特技播放模式并暂停流。 调用 <span class="codeph"> Play()</span> 以正常模式播放媒体。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_AHEAD</span> </td> 
   <td colname="col3"> 播放器超出实时窗口，必须向前搜寻才能赶上进度。 </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR：加密值 {#section_39365E545CAC49B9A4D4678657BB2155}

Adobe视频引擎的加密模块将这些通知返回到 `NATIVE_ERROR` 元数据对象。

| **NATIVE_ERROR_CODE元数据键的值** | **NATIVE_ERROR_NAME元数据键的值** | **含义** |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | 不支持正在使用的算法。 |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | 数据已损坏。 |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | 缓冲区太小。 |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | 证书无效。 |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | 摘要更新。 |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | 摘要结束。 |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | 参数错误。 |
