---
seo-title: 命令行使用
title: 命令行使用
uuid: 54b1e867-c6cc-4355-b8e6-a7ec910bd33d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 命令行使用 {#command-line-usage}

要运行该工具，请使用以下语法：

```
java -jar AdobePublisherIDUtility.jar 
<i class="+ topic ph hi-d="" i "="">
 <i class="+ topic ph hi-d="" i "="">
  signaturefile 
  java -jar AdobePublisherIDUtility.jar -s 
  <i class="+ topic ph hi-d="" i "="">
    signingcert
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* 
   * `signaturefile`*指定AIR应用程序的signatures.xml文件的路径，该文件位于应用程序目 [!DNL META-INF] 录中

* `signingcert` 指定用于对AIR应用程序进行签名的证书

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>要确定iOS应用程序的发布者ID，请使用该 `-s` 选项并指定用于对iOS应用程序进行签名的证书。 ***需要Adobe Primetime构建可播放受访问保护的内容的iOS应用程序***。

