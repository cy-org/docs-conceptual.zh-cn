---
title: "如何：在重新承载的设计器中显示验证错误 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5aa8fb53-8f75-433b-bc06-7c7d33583d5d
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 如何：在重新承载的设计器中显示验证错误
本主题说明如何在重新承载的 [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] 中检索和发布验证错误。这为我们提供了一个用于确认重新承载的设计器中的工作流是否有效的过程。  
  
 此任务包含两个部分。第一部分提供一个实现 <xref:System.Activities.Presentation.Validation.IValidationErrorService>。在此接口上要实现一个关键方法 <xref:System.Activities.Presentation.Validation.IValidationErrorService.ShowValidationErrors%2A>，该方法将一个包含有关错误的信息的 <xref:System.Activities.Presentation.Validation.ValidationErrorInfo> 对象的列表传递给调试日志。实现此接口之后，可通过将该实现的实例发布到编辑上下文来检索错误信息。  
  
### 实现 IValidationErrorService 接口  
  
1.  下面是一个将验证错误写入调试日志的简单实现的代码示例。  
  
    ```  
  
    using System.Activities.Presentation.Validation;  
    using System.Collections.Generic;  
    using System.Diagnostics;  
    using System.Linq;  
  
    namespace VariableFinderShell  
    {  
        class DebugValidationErrorService : IValidationErrorService  
        {  
            public void ShowValidationErrors(IList<ValidationErrorInfo> errors)  
            {  
                errors.ToList().ForEach(vei => Debug.WriteLine(string.Format("Error: {0} ", vei.Message)));  
            }  
        }  
    }  
    ```  
  
### 发布到编辑上下文  
  
1.  下面是将此内容发布到编辑上下文的代码。  
  
    ```  
  
    wd.Context.Services.Publish<IValidationErrorService>(new DebugValidationErrorService());  
    ```