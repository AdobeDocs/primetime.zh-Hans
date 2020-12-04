---
description: Flash运行时TVSDK需要一个签名令牌来验证您是否有权在应用程序所在的域中调用TVSDK API。
seo-description: Flash运行时TVSDK需要一个签名令牌来验证您是否有权在应用程序所在的域中调用TVSDK API。
seo-title: 加载已签名令牌
title: 加载已签名令牌
uuid: 8760eab3-3d6d-47c6-9aa7-f64f6aa5ddcf
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---


# 加载已签名的令牌{#load-your-signed-token}

Flash运行时TVSDK需要一个签名令牌来验证您是否有权在应用程序所在的域中调用TVSDK API。

1. 从Adobe代表处获取每个域的签名令牌（其中每个域可以是特定域或通配符域）。

       要获取令牌，请向Adobe提供存储或加载应用程序的域，或者最好将域作为SHA256哈希提供。作为回报，Adobe为每个域提供一个已签名的令牌。 这些令牌采用以下形式之一：
   
   * 充当单个域或通配符域的令牌的[!DNL .xml]文件。

      >[!NOTE]
      >
      >通配符域的令牌覆盖该域及其所有子域。 例如，域[!DNL mycompany.com]的通配符令牌也将涵盖[!DNL vids.mycompany.com]和[!DNL private.vids.mycompany.com];[!DNL vids.mycompany.com]的通配符令牌也涵盖[!DNL private.vids.mycompany.com]。 *通配符域令牌仅支持某些Flash Player版本。*

   * 一个[!DNL .swf]文件，包含多个域（不包括通配符）的令牌信息（单个或通配符），应用程序可以动态加载该文件。

1. 将令牌文件存储在与应用程序相同的位置或域中。

   默认情况下，TVSDK在此位置查找令牌。 或者，也可以在HTML文件的`flash_vars`中指定令牌的名称和位置。
1. 如果令牌文件是单个XML文件：
   1. 使用`utils.AuthorizedFeaturesHelper.loadFrom`下载存储在指定URL（令牌文件）的数据，并从中提取`authorizedFeatures`信息。

      此步骤可能不同。 例如，您可能希望在启动应用程序之前执行身份验证，或者您可能直接从内容管理系统(CMS)接收令牌。

   1. 如果加载成功，TVSDK将调度`COMPLETED`事件，否则将调度`FAILED`事件。 检测到任一事件时，请采取适当的操作。

      如果应用程序以`MediaPlayerContext`的形式向TVSDK提供所需的`authorizedFeatures`对象，则必须成功。
   此示例说明如何使用单令牌[!DNL .xml]文件。

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

1. 如果令牌是[!DNL .swf]文件：
   1. 定义`Loader`类以动态加载[!DNL .swf]文件。
   1. 设置`LoaderContext`以指定当前应用程序域中的加载，这允许TVSDK在[!DNL .swf]文件中选择正确的令牌。 如果未指定`LoaderContext`，则`Loader.load`的默认操作是在当前域的子域中加载。swf。
   1. 监听COMPLETE事件，如果加载成功，TVSDK将调度它。

      同时侦听ERROR事件并采取适当的操作。
   1. 如果加载成功，请使用`AuthorizedFeaturesHelper`获取包含PCKS-7编码的安全数据的`ByteArray`。

      此数据通过AVE V11 API从Flash运行时播放器获取授权确认。 如果字节数组没有内容，请改用该过程查找单域令牌文件。
   1. 使用`AuthorizedFeatureHelper.loadFeatureFromData`从字节数组获取所需数据。
   1. 卸载[!DNL .swf]文件。

   以下示例显示如何使用多令牌[!DNL .swf]文件。

   **多令牌示例1:**

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

   **多令牌示例2:**

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

