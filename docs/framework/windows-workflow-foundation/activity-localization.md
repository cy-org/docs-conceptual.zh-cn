---
title: "活动本地化 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ee7bc16-e609-469a-a3e8-8062952e2676
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 活动本地化
当工作流应用程序和组件可能要根据其他区域文化和语言进行本地化时，应使用资源字符串，以便无需重新编译即可对它们进行本地化。  
  
## 活动本地化  
 与必须本地化（针对不同的语言和区域文化发布不同的版本）的所有应用程序一样，向用户显示的任何字符串不应直接放在代码中，而应存储在某个资源文件中。然后可以通过 <xref:System.Environment.GetResourceString> 访问这些字符串。如果您开发的某个组件以多种语言分发，则还需要对活动验证消息、用户定义的跟踪数据、跟踪消息以及错误消息使用资源字符串。  
  
 下面的练习演示如何使用资源文件。  
  
#### 对本地化的字符串使用资源文件  
  
1.  在 [!INCLUDE[vs2010](../../../includes/vs2010-md.md)] 中，在**“解决方案资源管理器”**中右击项目，然后选择**“添加…”**，再选择**“新建项…”**。  
  
2.  选择**“资源文件”**，并将该文件命名为 ErrorResources.resx。单击**“添加”**。  
  
3.  打开该资源文件。添加一个新项，该项的**“名称”**为 ErrorString 且**“值”**为“该活动无效。”  
  
4.  向类中添加以下 `using` 声明。  
  
    ```  
    using System.Reflection;  
    using System.Resources;  
  
    ```  
  
5.  在项目中创建一个资源管理器。  
  
    ```  
    ResourceManager ErrorManager;  
    ...  
    ErrorManager = new ResourceManager("MyNamespace.ErrorResources", Assembly.GetExecutingAssembly());  
  
    ```  
  
6.  从资源管理器中获取字符串，该字符串在资源管理器中是必需的。  
  
    ```  
    String errorMessage = ErrorManager.GetString("ErrorString");  
  
    ```  
  
 以下代码示例演示了如何在 <xref:System.Activities.Activity.CacheMetadata%2A> 方法中使用本地化的字符串。  
  
```  
       protected override void CacheMetadata(CodeActivityMetadata metadata)  
        {  
           .....  
          // rest of the code elided for brevity  
           .....  
            if (this.Value != null && this.To != null)  
            {  
                if (!TypeHelper.AreTypesCompatible(this.Value.ArgumentType, this.To.ArgumentType))  
                {  
//---------------------------------------------  
// ** SR.TypeMismatchForAssign will fetch the string from the resource manager **  
//---------------------------------------------  
                    metadata.AddValidationError(SR.TypeMismatchForAssign(  
                                this.Value.ArgumentType,  
                                this.To.ArgumentType,  
                                this.DisplayName));  
                }  
            }  
        }  
```