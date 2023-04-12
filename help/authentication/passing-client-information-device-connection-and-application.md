---
title: 传递客户端信息（设备、连接和应用程序）
description: 传递客户端信息（设备、连接和应用程序）
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---


# 传递客户端信息（设备、连接和应用程序） {#pass-client-info}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。


## 范围 {#pass-client-info-scope}

本文档汇总了用于将客户端信息（设备、连接和应用程序）从程序员应用程序传递到Adobe Primetime Authentication REST API或SDK的详细信息和指南。

提供客户信息的好处包括：

* 在某些可支持HBA的设备类型和MVPD的情况下，能够正确启用家庭基本身份验证(HBA)。
* 在某些设备类型的情况下正确应用TTL的功能（例如，为电视连接设备上的身份验证会话配置更长的TTL）。
* 能够使用授权服务监控(ESM)在不同设备类型的划分报表中正确汇总业务量度。
* 取消阻止正确应用各种业务规则(例如 降级)。

## 概述 {#pass-client-info-overview}

客户端信息包括：

* **设备** 关于设备硬件和软件属性的信息，用户试图从中消费程序员内容。
* **连接** 有关用户从中连接到Adobe Primetime身份验证服务和/或程序员服务（例如服务器到服务器实施）的设备的连接属性的信息。
* **应用程序** 关于用户试图从中使用程序员内容的注册应用程序的信息。

客户端信息是使用下表所示的键构建的JSON对象。

>[!NOTE]
>
>以下 **键** are **强制** 要在客户端信息JSON对象中发送的： **模型**, **osName**.
>
>以下键具有 **受限** 值： `primaryHardwareType`, `osName`, `osFamily`, `browserName`, `browserVendor`, `connectionSecure`.

|  | 键 | 受限 | 描述 | 可能值 |
|---|---|---|---|---|
|  | primaryHardwareType | #是 | 设备的主要硬件类型。 | #值受限制：相机数据收集终端桌面嵌入式网络模块电子阅读器游戏控制台地理位置跟踪器眼镜媒体播放器手机支付终端插件调制解调器机顶盒电视平板电脑无线热点腕表未知 |
| #mandatory | 模型 | 否 | 设备的型号名称。 | 例如iPhone、SM-G930V、AppleTV等。 |
|  | 版本 | 否 | 设备的版本。 | 例如2.0.1等 |
|  | 制造商 | 否 | 设备的制造公司/组织。 | 例如，三星、LG、中兴、华为、摩托罗拉、Apple等。 |
|  | 供应商 | 否 | 设备的销售公司/组织。 | 例如，Apple、Samsung、LG、Google等 |
| #mandatory | osName | #是 | 设备的操作系统(OS)名称。 | #值受限制：Android Chrome OS Linux Mac OS X OpenBSD Roku OS Windows iOS tvOS webOS |
|  | osFamily | 是 | 设备的操作系统(OS)组名称。 | #值受限制：Android BSD Linux PlayStation OS Roku OS Symbian Tizen Windows iOS macOS tvOS webOS |
|  | osVendor | 否 | 设备的操作系统(OS)供应商。 | Amazon Apple Google LG Microsoft Mozilla任天堂Nokia Roku三星索尼Tizen项目 |
|  | osVersion | 否 | 设备的操作系统(OS)版本。 | 例如10.2、9.0.1等 |
|  | browserName | #是 | 浏览器的名称。 | #值受限制：Android浏览器Chrome Edge Firefox Internet Explorer Opera Safari SeaMonkey Symbian浏览器 |
|  | browserVendor | #是 | 浏览器的构建公司/组织。 | #值受限制：Amazon Apple Google Microsoft Motorola Mozilla Netscape任天堂Nokia Samsung Sony Ericsson |
|  | browserVersion | 否 | 设备的浏览器版本。 | 例如60.0.3112 |
|  | userAgent | 否 | 设备的用户代理。 | 例如，Mozilla/5.0(Macintosh;英特尔Mac OS X 10_12_3)AppleWebKit/602.4.8（KHTML，如Gecko）版本/10.0.3 Safari/602.4.8 |
|  | displayWidth | 否 | 设备的物理屏幕宽度。 |  |
|  | displayHeight | 否 | 设备的物理屏幕高度。 |  |
|  | displayPpi | 否 | 设备的物理屏幕像素密度。 | 例如294 |
|  | diagonalScreenSize | 否 | 设备的物理屏幕对角线尺寸（英寸）。 | 例如5.5、10.1 |
|  | connectionIp | 否 | 用于发送HTTP请求的设备的IP。 | 例如8.8.4.4 |
|  | connectionPort | 否 | 用于发送HTTP请求的设备的端口。 | 例如53124 |
|  | connectionType | 否 | 网络连接类型。 | 例如WiFi、LAN、3G、4G、5G |
|  | connectionSecure | #是 | 网络连接安全状态。 | #值受限制：true — 如果是安全网络false — 如果是公共热点，则为true |
|  | applicationId | 否 | 应用程序的唯一标识符。 | 例如，CNN |

## API参考 {#api-ref}

本节介绍在使用Adobe Primetime身份验证REST API或SDK时负责处理客户端信息的API。

### REST API {#rest-api}

Adobe Primetime身份验证服务支持通过以下方式接收客户端信息：

* As a **标题：&quot;X-Device-Info&quot;**
* As a **查询参数：&quot;device_info&quot;**
* As a **帖子参数：&quot;device_info&quot;**

>[!IMPORTANT]
>
>在所有三种情况下，标头或参数的有效负荷必须为 **Base64编码和URL编码**.

**SDK**

#### JavaScript SDK {#js-sdk}

默认情况下，AccessEnabler JavaScript SDK会生成一个客户端信息JSON对象，该对象将传递到Adobe Primetime身份验证服务，除非被覆盖。

AccessEnabler JavaScript SDK支持 **仅限** 客户端信息JSON对象中的“applicationId”键(通过 [setRequestor](/help/authentication/javascript-sdk-api-reference.md#setrequestor(inRequestorID,endpoints,options))&#39;s *applicationId* 选项参数。

>[!CAUTION]
>
>的 `applicationId` 参数值必须是纯文本字符串值。
>如果程序员应用程序决定传递applicationId，则其余的客户端信息键仍由AccessEnabler JavaScript SDK计算。

#### iOS/tvOS SDK {#ios-tvos-sdk}

默认情况下， AccessEnabler iOS/tvOS SDK会生成一个客户端信息JSON对象，该对象将传递到Adobe Primetime身份验证服务，除非被覆盖。

AccessEnabler iOS/tvOS SDK支持 **凌驾于整个** 客户端信息JSON对象(通过 [setOptions](/help/authentication/iostvos-sdk-api-reference.md#setoptions)&#39;s device_info参数。

>[!CAUTION]
>
>的 *device_info* 参数值必须 **Base64编码** *NSString* 值。
>
>如果程序员应用程序决定通过 *device_info*，则由AccessEnabler iOS/tvOS SDK计算的所有客户端信息键都将被覆盖。 因此，计算并传递尽可能多的键值非常重要。 有关实施的更多详细信息，请参阅 [概述](#pass-client-info-overview) 表格和 [iOS/tvOS指南](#ios-tvos).

#### Android/FireOS SDK {#and-fire-os-sdk}

的 `AccessEnabler` Android/FireOS SDK默认会生成一个客户端信息JSON对象，该对象将传递到Adobe Primetime身份验证服务，除非被覆盖。

的 `AccessEnabler` Android/FireOS SDK支持 **凌驾于整个** 客户端信息JSON对象(通过 [setOptions](/help/authentication/android-sdk-api-reference.md#setOptions)&#39;s/[setOptions](/help/authentication/amazon-fireos-native-client-api-reference.md#fire_setOption)&#39;s `device_info` 参数。

>[!NOTE]
>
>的 `device_info` 参数值必须 **Base64编码** 字符串值。

>[!IMPORTANT]
>
>如果程序员应用程序决定通过 `device_info`，然后是 `AccessEnabler` Android/FireOS SDK将被覆盖。 因此，计算并传递尽可能多的键值非常重要。 有关实施的更多详细信息，请参阅 [概述](#pass-client-info-overview) 表格和 [Android](#android) 和 [FireOS](#fire-tv) 指南。

## 指南 {#cookbooks}

本节介绍一本指南，用于在不同设备类型情况下构建客户端信息JSON对象。

>[!IMPORTANT]
>
>标有的键  **!** 必须发送。

### Android {#android}

设备信息可以通过以下方式构建：

|  | 键 | 来源 | 值（示例） |
|---|---------------|-----------------------------|---------------|
| ! | 模型 | Build.MODEL | GT-I9505 |
|  | 供应商 | Build.BRAND | 三星 |
|  | 制造商 | Build.MANUFACTURER | 三星 |
| ! | 版本 | Build.DEVICE | jflte |
|  | displayWidth | DisplayMetrics.widthPixels | 600 |
|  | displayHeight | DisplayMetrics.heightPixels | 800 |
| ! | osName | 硬编码 | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.0.1 |

连接信息可以通过以下方式构建：

|  | 键 | 来源 | 值（示例） |
|---|---|---|---|
| ! | connectionType | `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` `getSystemService(Context.CONNECTIVITY_SERVICE).getActiveNetworkInfo().getType()` | `"WIFI","BLUETOOTH","MOBILE","ETHERNET","VPN","DUMMY","MOBILE_DUN","WIMAX","notAccessible"` |
|  | connectionSecure |  |  |

应用信息可以通过以下方式构建：

|  | 键 | 来源 | 值（示例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬编码 | CNN |

>[!IMPORTANT]
设备、连接和应用程序信息必须添加到同一JSON对象中。 之后，生成的对象必须为 **Base64编码**. 此外，对于Adobe Primetime身份验证REST API，值必须为 **URL编码**.

**示例代码**

```JAVA
private JSONObject computeClientInformation() {
     String LOGGING_TAG = "DefineClass.class";
  
     JSONObject clientInformation = new JSONObject();

     String connectionType;

     try {
          ConnectivityManager cm = (ConnectivityManager) getContext().getSystemService(CONNECTIVITY_SERVICE);
          NetworkInfo activeNetwork = cm.getActiveNetworkInfo();

          if (activeNetwork != null && activeNetwork.isConnectedOrConnecting()) {
              switch (activeNetwork.getType()) {
                    case ConnectivityManager.TYPE_WIFI: {
                        connectionType = "WIFI";
                        break;
                    }
                    case ConnectivityManager.TYPE_BLUETOOTH: {
                        connectionType = "BLUETOOTH";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE: {
                        connectionType = "MOBILE";
                        break;
                    }
                    case ConnectivityManager.TYPE_ETHERNET: {
                        connectionType = "ETHERNET";
                        break;
                    }
                    case ConnectivityManager.TYPE_VPN: {
                        connectionType = "VPN";
                        break;
                    }
                    case ConnectivityManager.TYPE_DUMMY: {
                        connectionType = "DUMMY";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE_DUN: {
                        connectionType = "MOBILE_DUN";
                        break;
                    }
                    case ConnectivityManager.TYPE_WIMAX: {
                        connectionType = "WIMAX";
                        break;
                    }
                    default:
                       connectionType = ConnectivityManager.EXTRA_OTHER_NETWORK_INFO;
              }
          } else {
                connectionType = ConnectivityManager.EXTRA_NO_CONNECTIVITY;
          }
     } catch (Exception e) {
          connectionType = "notAccessible";
     }

     try {
          clientInformation.put("model",Build.MODEL);
          clientInformation.put("vendor", Build.BRAND);
          clientInformation.put("manufacturer",Build.MANUFACTURER);
          clientInformation.put("version",Build.DEVICE);
          clientInformation.put("osName","Android");
          clientInformation.put("osVersion",Build.VERSION.RELEASE);
          clientInformation.put("connectionType",connectionType);
          clientInformation.put("applicationId","CNN");
     } catch (JSONException e) {
          Log.e(LOGGING_TAG, e.getMessage());
     }

     return Base64.encodeToString(clientInformation.toString().getBytes(), Base64.NO_WRAP);
}
```

>[!NOTE]
**资源：**
* 公共类 [构建](https://developer.android.com/reference/android/os/Build.html){target=_blank} （位于Java开发人员文档中）。


### FireTV {#fire-tv}

设备信息可以通过以下方式构建：

|  | 键 | 来源 | 值(例如 |
|---|---------------|-----------------------------|--------------|
| ! | 模型 | Build.MODEL | AFTM |
|  | 供应商 | Build.BRAND | Amazon |
|  | 制造商 | Build.MANUFACTURER | Amazon |
| ! | 版本 | Build.DEVICE | 蒙托亚 |
|  | displayWidth | DisplayMetrics.widthPixels |  |
|  | displayHeight | DisplayMetrics.heightPixels |  |
| ! | osName | 硬编码 | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.1.1 |

连接信息可以通过以下方式构建：

|  | 键 | 来源 | 值（示例） |
|---|------------------|--------|---------------|
| ! | connectionType |  |  |
|  | connectionSecure |  |  |

应用信息可以通过以下方式构建：

|  | 键 | 来源 | 值（示例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬编码 | CNN |

>[!IMPORTANT]
设备、连接和应用程序信息必须添加到同一JSON对象中。 之后，生成的对象必须为 **Base64编码**. 此外，对于Adobe Primetime身份验证REST API，值必须为 **URL编码**.

>[!NOTE]
**资源：**
* 公共类 [生成](https://developer.android.com/reference/android/os/Build.html){target=_blank} ，位于Android开发人员文档中。
* [识别FireTV设备](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html){target=_blank}


### iOS/tvOS {#ios-tvos}

设备信息可以通过以下方式构建：

|  | 键 | 来源 | 值（示例） |
|---|---------------|------------------------|--------------|
| ! | 模型 | uname.machine | iPhone |
|  | 供应商 | 硬编码 | Apple |
|  | 制造商 | 硬编码 | Apple |
| ! | 版本 | uname.machine | 8,1 |
|  | displayWidth | UIScreen.mainScreen | 320 |
|  | displayHeight | UIScreen.mainScreen | 568 |
| ! | osName | UIDevice.systemName | iOS |
| ! | osVersion | UIDevice.systemVersion | 10.2 |

连接信息可以通过以下方式构建：

|  | 键 | 来源 | 值（示例） |
|---|------------------|-------------------------------------------|--------------|
| ! | connectionType | [可达性currentReachabilityStatus] |  |
|  | connectionSecure |  |  |


应用信息可以通过以下方式构建：

|  | 键 | 来源 | 值（示例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬编码 | CNN |

>[!IMPORTANT]
设备、连接和应用程序信息必须添加到同一JSON对象中。 之后，生成的对象必须进行Base64编码。 此外，对于Adobe Primetime身份验证REST API，值必须进行URL编码。

**示例代码**

```C
+ (NSString *)computeClientInformation {        
        struct utsname u;
        uname(&u);

        NSString *hardware = [NSString stringWithCString:u.machine encoding:NSUTF8StringEncoding];

        UIDevice *device = [UIDevice currentDevice];

        NSString *deviceType;

        switch (UI_USER_INTERFACE_IDIOM()) {
            case UIUserInterfaceIdiomPhone:
                deviceType = @"MobilePhone";
                break;
            case UIUserInterfaceIdiomPad:
                deviceType = @"Tablet";
                break;
            case UIUserInterfaceIdiomTV:
                deviceType = @"TV";
                break;
            default:
                deviceType = @"Unknown";
        }

        CGRect screenRect = [[UIScreen mainScreen] bounds];
        NSNumber *screenWidth = @((float) screenRect.size.width);
        NSNumber *screenHeight = @((float) screenRect.size.height);

        Reachability *reachability = [Reachability reachabilityForInternetConnection];
        [reachability startNotifier];

        NetworkStatus status = [reachability currentReachabilityStatus];

        NSString *connectionType;

        if (status == NotReachable) {
            connectionType = @"notConnected";
        } else if (status == ReachableViaWiFi) {
            connectionType = @"WiFi";
        } else if (status == ReachableViaWWAN) {
            connectionType = @"cellular";
        }

        NSMutableDictionary *clientInformation = [@{
                @"type": deviceType,
                @"model": device.model,
                @"vendor": @"Apple",
                @"manufacturer": @"Apple",
                @"version": [hardware stringByReplacingOccurrencesOfString:device.model withString:@""],
                @"osName": device.systemName,
                @"osVersion": device.systemVersion,
                @"displayWidth": screenWidth,
                @"displayHeight": screenHeight,
                @"connectionType": connectionType,
                @"applicationId": @"CNN" 
        } mutableCopy];

        NSError *error;
        NSData *jsonData = [NSJSONSerialization dataWithJSONObject:clientInformation options:NSJSONWritingPrettyPrinted error:&error];
        NSString *base64Encoded = [jsonData base64EncodedStringWithOptions:0];

        return base64Encoded;
}
```

>[!NOTE]
**资源：**
* [UIDevice](https://developer.apple.com/documentation/uikit/uidevice#//apple_ref/occ/cl/UIDevice){target=_blank}
* [uname](https://man7.org/linux/man-pages/man2/uname.2.html){target=_blank}
* [关于可达性](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html){target=_blank}


### Roku {#roku}

设备信息可以通过以下方式构建：

| 键 | 来源 | 值（示例） |  |
|-----|---------------|--------------------------------------------|-----------------|
| ! | 模型 | 硬编码 | &quot;Roku&quot; |
|  | 供应商 | ifDeviceInfo.GetModelDetails().VendorName | “锐利”、“Roku” |
|  | 制造商 | ifDeviceInfo.GetModelDetails().VendorName | “锐利”、“Roku” |
| ! | 版本 | ifDeviceInfo.GetModelDetails().ModelNumber | 《5303X》 |
|  | displayWidth | ifDeviceInfo.GetDisplaySize().w | 1920 |
|  | displayHeight | ifDeviceInfo.GetDisplaySize().h | 1080 |
| ! | osName | 硬编码 | &quot;Roku&quot; |
| ! | osVersion | ifDeviceInfo.getVersion() |  |

连接信息可以通过以下方式构建：

|  | 键 | 来源 | 值（示例） |
|---|---|---|---|
| ! | connectionType | ifDeviceInfo.GetConnectionType() | &quot;WifiConnection&quot;、&quot;WiredConnection&quot; |
|  | connectionSecure | 硬编码 | 如果连接已连接，则为true |

应用信息可以通过以下方式构建：

|  | 键 | 来源 | 值（示例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬编码 | CNN |

>[!IMPORTANT]
设备、连接和应用程序信息必须添加到同一JSON对象中。 之后，生成的对象必须为 **Base64编码**. 此外，对于Adobe Primetime身份验证REST API，值必须进行URL编码。

>[!NOTE]
有关更多信息，请参阅 [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md)

### XBOX 1/360 {#xbox}

设备信息可以通过以下方式构建：

|  | 键 | 来源 | 值（示例） |
|---|---|---|---|
| ! | 模型 | EasClientDeviceInformation.SystemProductName |  |
|  | 供应商 | 硬编码 | Microsoft |
|  | 制造商 | 硬编码 | Microsoft |
| ! | 版本 | EasClientDeviceInformation.SystemHardwareVersion |  |
|  | displayWidth | DisplayInformation.ScreenWidthInRawPixels | 1920 |
|  | displayHeight | DisplayInformation.ScreenHeightInRawPixels | 1080 |
| ! | osName | EasClientDeviceInformation.OperatingSystem |  |
| ! | osVersion | EasClientDeviceInformation.SystemFirmwareVersion |  |

连接信息可以通过以下方式构建：

|  | 键 | 来源 | 示例 |
|---|---|---|---|
| ! | connectionType |  |  |
|  | connectionSecure | NetworkAuthenticationType | “无”、“Wpa”等 |

应用信息可以通过以下方式构建：

| 键 | 来源 | 值（示例） |
|---|---|---|
| applicationId | 硬编码 | CNN |

>[!IMPORTANT]
设备、连接和应用程序信息必须添加到同一JSON对象中。 之后，生成的对象必须为 **Base64编码**. 此外，对于Adobe Primetime身份验证REST API，值必须为 **URL编码**.

**资源**

* [EasClientDeviceInformation类](https://docs.microsoft.com/en-us/uwp/api/windows.security.exchangeactivesyncprovisioning.easclientdeviceinformation?view=winrt-22000)
* [显示信息类](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.display.displayinformation?view=winrt-22000)


