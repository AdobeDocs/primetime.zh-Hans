---
seo-title: NATIVE_ERROR通知的详细信息
title: NATIVE_ERROR通知的详细信息
uuid: 59f6077f-8162-4755-afd8-ce95fd5d57b2
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# NATIVE_ERROR通知的详细信息 {#details-for-the-native-error-notification}

当TVSDK处理本机错误时，它会设置以下部分或全部元数据键值。

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 元数据键名 </th> 
   <th colname="col2" class="entry"> 元数据值 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RUNTIME_CODE </span> </td> 
   <td colname="col2"> 
    <ph>
      Flash Player的本机错误代码。 
    </ph> 这些代码表示： 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">DRM错误（代码3300到3367）。 这些错误代码与等效的Flash Player错误代码相同。 </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">视频播放错误（-1到89）。 </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">密码错误（300到307）。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RUNTIME_CODE_MESSAGE </span> </td> 
   <td colname="col2"> 包含错误名称的字符串；例如， <span class="codeph"> AAXS_InvalidVoucher </span> 或 <span class="codeph"> DECODER_FAILED </span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RUNTIME_SUBERROR_CODE </span> </td> 
   <td colname="col2"> 对于DRM错误，还会返回子错误代码。 这些代码与Flash Player <span class="codeph"> 返回 </span> 的DRMErrorEvents子错误代码相对应。 向Adobe报告错误时，请包含此数值以获得疑难解答帮助。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING </span> </td> 
   <td colname="col2"> 对于DRM，这是您在DRM服务器部署中的自定义错误字符串（如果您定义了任何）。 在向Adobe报告错误时，也应包含此内容。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 说明 </span> </td> 
   <td colname="col2"> 错误的字符串描述。 通常是媒体的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RESOURCE_URL </span> </td> 
   <td colname="col2"> 媒体的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RESOURCE_TYPE </span> </td> 
   <td colname="col2"> 媒体类型(HLS)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RESOURCE_ID </span> </td> 
   <td colname="col2"> 媒体ID。 </td> 
  </tr> 
 </tbody> 
</table>

TVSDK从视频引擎接收这些错误代码和字符串。

>[!IMPORTANT]
>
>有关Adobe Primetime DRM客户端错误代码的完整列表，请参阅 [DRM客户端错误消息参考](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf)。