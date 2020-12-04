---
seo-title: 使用Java API更新DRM策略
title: 使用Java API更新DRM策略
uuid: ec21351c-900e-48f5-845a-c0b430c210d7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# 使用Java API {#updating-a-drm-policy-with-the-java-api}更新DRM策略

要使用Java API更新DRM策略，请执行以下操作：

1. 设置开发环境，并将[设置开发环境](../../protecting-content/setting-up-the-sdk/setup-dev-env.md)中列出的所有JAR文件包含在项目中。
1. 创建DRM `Policy`实例，并从文件或数据库读取DRM策略。

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 通过设置DRM `Policy`对象的属性（如其名称和使用规则）来更新该对象。

   ```java
   // Change the DRM policy name.  
   policy.setName("UpdatedDemoPolicy");  
   
   // Add DRM module restrictions to the play right  
   for (Right r: policy.getRights()) {  
       if (r instanceof PlayRight) {  
           PlayRight pr = (PlayRight) r;  
           // Disallow Linux versions up to and including 1.9.  Allow  
           // all other OSes and Linux versions above 1.9  
           VersionInfo toExclude = new VersionInfo();  
           toExclude.setOS("Linux");  
           toExclude.setReleaseVersion("1.9");  
           Collection<VersionInfo> exclusions = new ArrayList<VersionInfo>();  
           exclusions.add(toExclude);  
           ModuleRequirements drmRestrictions = new ModuleRequirements();  
           drmRestrictions.setExcludedVersions(exclusions);  
           pr.setDRMModuleRequirements(drmRestrictions);  
           break;  
       }  
   }
   ```

1. 对更新的DRM `Policy`对象进行序列化，并将其存储在文件或数据库中。

   ```java
   // Serialize the DRM policy.  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("New DRM policy revision number: "  
       +  policy.getRevision());      
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
   out.write(policyBytes);  
   out.close();
   ```

有关此示例代码的源，请参见Reference Implementation Command Line Tools [!DNL samples]目录中的`com.adobe.flashaccess.samples.policy.UpdatePolicy`。
