---
description: Flash运行时TVSDK需要一个已签名的令牌来验证您是否有权在应用程序所在的域中调用TVSDK API。
title: 加载您的签名令牌
exl-id: fef6b764-dc65-412e-a990-3f0b1fef94dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 加载您的签名令牌 {#load-your-signed-token}

Flash运行时TVSDK需要一个已签名的令牌来验证您是否有权在应用程序所在的域中调用TVSDK API。

1. 从您的Adobe代表处获取每个域（其中每个域可以是特定域或通配符域）的签名令牌。

       要获取令牌，请为Adobe提供将存储或加载您的应用程序的域，或者最好提供作为SHA256哈希的域。 作为回报，Adobe将为您提供每个域的签名令牌。 这些令牌采用以下形式之一：
   
   * An [!DNL .xml] 用作单个域或通配符域的令牌的文件。

      >[!NOTE]
      >
      >通配符域的令牌涵盖该域及其所有子域。 例如，域的通配符令牌 [!DNL mycompany.com] 还将涵盖 [!DNL vids.mycompany.com] 和 [!DNL private.vids.mycompany.com]；的通配符令牌 [!DNL vids.mycompany.com] 还将涵盖 [!DNL private.vids.mycompany.com]. *仅某些Flash Player版本支持通配符域令牌。*

   * A [!DNL .swf] 包含应用程序可动态加载的多个域（不包括通配符）（单个或通配符）的令牌信息的文件。

1. 将令牌文件存储在与您的应用程序相同的位置或域中。

   默认情况下，TVSDK会在此位置查找令牌。 或者，您也可以指定令牌的名称和位置 `flash_vars` 在您的HTML文件中。
1. 如果您的令牌文件是单个XML文件：
   1. 使用 `utils.AuthorizedFeaturesHelper.loadFrom` 下载存储在指定URL中的数据（令牌文件）并解压缩 `authorizedFeatures` 信息来源。

      此步骤可能有所不同。 例如，您可能需要在启动应用程序之前执行身份验证，或者可以直接从内容管理系统(CMS)接收令牌。

   1. TVSDK调度 `COMPLETED` 事件(如果加载成功或 `FAILED` 事件。 在检测到任一事件时采取适当措施。

      这必须成功，您的应用程序才能提供所需的 `authorizedFeatures` 对象以形式添加到TVSDK `MediaPlayerContext`.
   此示例说明如何使用单个令牌 [!DNL .xml] 文件。

   ```
   private function loadDirectTokenURL():void { 
       var url:String = constructAuthorizedFeatureTokenURL(); 
       _logger.debug("#onApplicationComplete Loading token from [{0}].", url); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE,  
           onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR,  
           onFeatureError); 
        _authorizedFeatureHelper.loadFrom(url); 
    }
   ```

1. 如果您的令牌是 [!DNL .swf] 文件：
   1. 定义 `Loader` 类以动态加载 [!DNL .swf] 文件。
   1. 设置 `LoaderContext` 指定加载位于当前应用程序域中，这允许TVSDK在 [!DNL .swf] 文件。 如果 `LoaderContext` 未指定，默认操作为 `Loader.load` 是在当前域的子域中加载.swf。
   1. 监听COMPLETE事件，如果加载成功，TVSDK将调度该事件。

      同时侦听ERROR事件并采取适当的操作。
   1. 如果加载成功，请使用 `AuthorizedFeaturesHelper` 获取 `ByteArray` ，其中包含PCKS-7编码的安全数据。

      此数据通过AVE V11 API用于从Flash运行时播放器获取授权确认。 如果字节数组没有内容，请改用过程查找单域令牌文件。
   1. 使用 `AuthorizedFeatureHelper.loadFeatureFromData` 以从字节阵列中获取所需数据。
   1. 卸载 [!DNL .swf] 文件。

   以下示例显示如何使用多令牌 [!DNL .swf] 文件。

   **多令牌示例1：**

   ```
   private function onApplicationComplete(event:FlexEvent):void { 
       var url:String = constructAuthorizedFeatureTokenURLFromSwf();   
       _loader = new Loader(); 
       var swfUrl:URLRequest = new URLRequest(url); 
       var loaderContext:LoaderContext =  
           new LoaderContext(false, ApplicationDomain.currentDomain, null); 
       _loader.contentLoaderInfo.addEventListener(Event.COMPLETE,  
           modEventHandler); 
       _loader.contentLoaderInfo.addEventListener(IOErrorEvent.IO_ERROR,  
           errEventHandler); 
       _loader.contentLoaderInfo.addEventListener(ProgressEvent.PROGRESS,  
           onProgressHandler); 
       _loader.uncaughtErrorEvents.addEventListener(UncaughtErrorEvent. 
           UNCAUGHT_ERROR, uncaughtEventHandler); 
       _logger.debug("# Loading token swf with context from [{0}].", url); 
       _loader.load(swfUrl, loaderContext); 
   } 
   
   private function modEventHandler(e:Event):void { 
       _logger.debug("loadSWF with domainID {0}",  
       SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
           loader.contentLoaderInfo.applicationDomain. 
           getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray = myTokens. 
           FetchToken(SecurityDomain.currentDomain.domainID); 
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           _logger.debug("token bytearry size {0}", byteArray.length); 
           _authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   ```

   **多令牌示例2：**

   ```
   private function tokenSwfLoadedHandler(e:Event):void { 
       trace("loadSWF with domainID {0}", SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
         loader.contentLoaderInfo.applicationDomain. 
         getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray =  
           myTokens.FetchToken(SecurityDomain.currentDomain.domainID); 
       var myDomains:Array = ["domain.com"]; 
       if (byteArray == null || byteArray.length == 0) { 
           // check for wildcard tokens 
           if (myTokens.hasOwnProperty("FetchWildCardToken") == true) { 
               // contains wildcard domains 
               for each (var domain:String in myDomains) { 
                   byteArray = myTokens.FetchWildCardToken(domain); 
                   if (byteArray != null && byteArray.length != 0) { 
                       break; 
                   } 
               }; 
           } 
       } 
   
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           trace("token bytearry size {0}", byteArray.length); 
           authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   
   private function loadDirectTokenURL():void { 
       trace("#onApplicationComplete Loading token from [{0}].", tokenUrl); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       authorizedFeatureHelper.loadFrom(tokenUrl); 
   }
   ```
