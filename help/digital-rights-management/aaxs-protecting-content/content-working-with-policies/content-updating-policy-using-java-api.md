---
title: 使用Java API更新策略
description: 使用Java API更新策略
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 使用Java API更新策略 {#updating-a-policy-using-the-java-api}

要使用Java API更新策略，请执行以下步骤：

1. 设置开发环境，并包含中提到的所有JAR文件 [设置开发环境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 在您的项目中。
1. 创建 `Policy` 实例并从文件或数据库读取策略。

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 更新 `Policy` 对象的方法是设置其属性，如其名称和使用规则。

   ```java
     // Change the policy name.  
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

1. 序列化更新的 `Policy` 对象并将其存储在文件或数据库中。

   ```java
      // Serialize the policy.  
      byte[] policyBytes = policy.getBytes();  
      System.out.println("New policy revision number: "  
       +  policy.getRevision());      
      // Write the policy to a file.   
      // Alternatively, the policy may be stored in a database.  
      FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
      out.write(policyBytes);  
      out.close(); 
   ```

有关此示例代码的完整源，请参见 `com.adobe.flashaccess.samples.policy.UpdatePolicy` 在参考实施命令行工具“samples”目录中。
