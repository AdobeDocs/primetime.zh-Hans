---
seo-title: 使用Java API更新策略
title: 使用Java API更新策略
uuid: 23c50f05-799e-4f5a-869b-4b5e29a36ce1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用Java API更新策略 {#updating-a-policy-using-the-java-api}

要使用Java API更新策略，请执行以下步骤：

1. 设置开发环境，并将“设置开发环境”中提 [及的所有JAR文件包含在项目中](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 。
1. 创建一 `Policy` 个实例，并从文件或数据库读取策略。

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 通过设 `Policy` 置对象的属性（如其名称和使用规则）来更新对象。

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

1. 对更新的对 `Policy` 象进行序列化，并将其存储在文件或数据库中。

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

有关此示例代码的完整源代码，请参 `com.adobe.flashaccess.samples.policy.UpdatePolicy` 阅参考实现命令行工具“samples”目录。
