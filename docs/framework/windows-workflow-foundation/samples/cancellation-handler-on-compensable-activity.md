---
title: "可补偿活动上的取消处理程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: afd98bee-eccf-47e9-99c9-27cea84ce5ce
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 可补偿活动上的取消处理程序
此示例演示如何对 <xref:System.Activities.Statements.CompensableActivity> 使用取消处理程序。  
  
 此示例包含两个演示如何使用 <xref:System.Activities.Statements.CompensableActivity> 取消的方案。第一个方案包含一个根可补偿活动，而根可补偿活动又包含三个子可补偿活动。两个子活动成功地运行完它们的活动主体。当运行第三个子活动主体时，它会遇到一个异常，该异常可通过取消第三个活动进程来处理，此后，将会触发根活动的取消。此示例中根活动的逻辑是补偿较早完成的另外两个子活动。  
  
```  
Try  
{  
    CA   
    {  
        CA1   
        {  
        }  
        CA2  
        {  
        }  
        CA3  
        {  
            //Exception here  
            // Then this will get cancelled  
        }  
  
       // Cancellation for the root activity automatically gets called, which, in turn, adds some logic to revert what was done (Or can decide to actually confirm CA1 & CA2 if the user so desires).  
    }  
}  
Catches {  
// Can do more stuff...  
}  
  
```  
  
 第二个方案演示如何与 <xref:System.Activities.Statements.Delay> 一起并行执行 <xref:System.Activities.Statements.TryCatch>，此操作在 <xref:System.Activities.Statements.TryCatch> 分支之前完成。在完成第一个分支之后，完成条件将设置为 `true`，从而导致取消另一个分支。  
  
```  
Parallel   
{  
    Branch1   
    {  
        // Small Delay that times out (timeout1) before branch2.  
    }  
    Branch2   
    {  
        CA   
        {  
            CA1   
            {  
            }  
            CA2   
            {  
            }  
            CA3   
            {  
            }  
            If (timeout1)    
            {  
                call Cancel CA  
            }  
        }  
    }  
}  
  
```  
  
### 设置、生成和运行示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 CompensationCancellation.sln。  
  
2.  请按 CTRL\+SHIFT\+B 或从生成菜单中选择“生成解决方案”来生成示例。  
  
3.  按 F5 或从“调试”菜单中选择“开始调试”来运行示例。或者，可以按 Ctrl\+F5 或从“调试”菜单中选择“开始执行\(不调试\)”。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Compensation\CompensationCancellation`  
  
## 请参阅