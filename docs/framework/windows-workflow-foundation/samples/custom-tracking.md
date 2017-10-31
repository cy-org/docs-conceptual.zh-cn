---
title: "自定义跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d191c9f-62f4-4c63-92dd-cda917fcf254
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# 自定义跟踪
此示例演示如何创建自定义跟踪参与者并将跟踪数据的内容写入控制台。另外，此示例还演示如何发出使用用户定义的数据填充的 <xref:System.Activities.Tracking.CustomTrackingRecord> 对象。基于控制台的跟踪参与者将使用代码中创建的跟踪配置文件对象来筛选由工作流发出的 <xref:System.Activities.Tracking.TrackingRecord> 对象。  
  
## 示例详细信息  
 [!INCLUDE[wf](../../../../includes/wf-md.md)] 提供一个跟踪基础结构，用于跟踪工作流实例的执行。跟踪运行时实现一个工作流实例，以便发出与工作流生命周期有关的事件、来自工作流活动的事件和自定义跟踪事件。下表详细介绍了跟踪基础结构的主要组件。  
  
|组件|说明|  
|--------|--------|  
|跟踪运行时|提供基础结构以发出跟踪记录。|  
|跟踪参与者|消耗跟踪记录。[!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)] 附带一个跟踪参与者，该参与者作为 Windows 事件跟踪 \(ETW\) 事件写入跟踪记录。|  
|跟踪配置文件|筛选机制，允许跟踪参与者订阅从工作流实例发出的跟踪记录的子集。|  
  
 下表详细介绍工作流运行时发出的跟踪记录。  
  
|跟踪记录|说明|  
|----------|--------|  
|工作流实例跟踪记录。|描述工作流实例的生命周期。例如，当工作流启动或完成时发出一个实例记录。|  
|活动状态跟踪记录。|详细说明活动执行情况。这些记录指示工作流活动的状态，例如，当安排活动时、活动完成时或引发错误时。|  
|书签恢复记录。|当恢复工作流实例中的书签时发出。|  
|自定义跟踪记录。|工作流作者可以在自定义活动中创建并发出自定义跟踪记录。|  
  
 跟踪参与者使用跟踪配置文件来订阅已发出 <xref:System.Activities.Tracking.TrackingRecord> 对象的子集。一个跟踪配置文件包含允许订阅特定跟踪记录类型的查询。可以在代码或配置中指定跟踪配置文件。  
  
### 自定义跟踪参与者  
 跟踪参与者 API 允许以用户提供的跟踪参与者扩展跟踪运行时，该用户提供的跟踪参与者可包括用于对工作流运行时发出的 <xref:System.Activities.Tracking.TrackingRecord> 对象进行处理的自定义逻辑。  
  
 若要编写跟踪参与者，用户必须实现 <xref:System.Activities.Tracking.TrackingParticipant>。具体而言，<xref:System.Activities.Tracking.TrackingParticipant.Track%2A> 方法必须由自定义参与者实现。此方法在工作流运行时发出 <xref:System.Activities.Tracking.TrackingRecord> 时调用。  
  
```csharp  
public abstract class TrackingParticipant  
{  
    protected TrackingParticipant();  
  
    public virtual TrackingProfile TrackingProfile { get; set; }  
    public abstract void Track(TrackingRecord record, TimeSpan timeout);  
}  
  
```  
  
 完整的跟踪参与者是在 ConsoleTrackingParticipant.cs 文件中实现的。下面的代码示例是用于自定义跟踪参与者的 <xref:System.Activities.Tracking.TrackingParticipant.Track%2A> 方法。  
  
```csharp  
protected override void Track(TrackingRecord record, TimeSpan timeout)  
{  
    ...             
    WorkflowInstanceRecord workflowInstanceRecord = record as WorkflowInstanceRecord;  
    if (workflowInstanceRecord != null)  
    {  
        Console.WriteLine(String.Format(CultureInfo.InvariantCulture,  
            " Workflow InstanceID: {0} Workflow instance state: {1}",  
            record.InstanceId, workflowInstanceRecord.State));  
    }  
  
    ActivityStateRecord activityStateRecord = record as ActivityStateRecord;  
    if (activityStateRecord != null)  
    {  
        IDictionary<String, object> variables = activityStateRecord.Variables;  
        StringBuilder vars = new StringBuilder();  
  
        if (variables.Count > 0)  
        {  
            vars.AppendLine("\n\tVariables:");  
            foreach (KeyValuePair<string, object> variable in variables)  
            {     
                vars.AppendLine(String.Format(  
                    "\t\tName: {0} Value: {1}", variable.Key, variable.Value));  
            }  
        }  
        Console.WriteLine(String.Format(CultureInfo.InvariantCulture,  
            " :Activity DisplayName: {0} :ActivityInstanceState: {1} {2}",  
                activityStateRecord.Activity.Name, activityStateRecord.State,  
            ((variables.Count > 0) ? vars.ToString() : String.Empty)));  
    }  
  
    CustomTrackingRecord customTrackingRecord = record as CustomTrackingRecord;  
  
    if ((customTrackingRecord != null) && (customTrackingRecord.Data.Count > 0))  
    {  
        ...  
    }  
    Console.WriteLine();  
  
}  
  
```  
  
 下面的代码示例将向工作流调用程序添加控制台参与者。  
  
```csharp  
ConsoleTrackingParticipant customTrackingParticipant = new ConsoleTrackingParticipant()  
{  
    ...  
    // The tracking profile is set here, refer to Program.CS  
...  
}  
  
WorkflowInvoker invoker = new WorkflowInvoker(BuildSampleWorkflow());  
invoker.Extensions.Add(customTrackingParticipant);  
  
```  
  
### 发出自定义跟踪记录  
 此示例还演示从自定义工作流活动发出 <xref:System.Activities.Tracking.CustomTrackingRecord> 对象的功能：  
  
-   创建 <xref:System.Activities.Tracking.CustomTrackingRecord> 对象，并使用用户定义的数据（此数据必须与记录一起发出）对其进行填充。  
  
-   通过调用 <xref:System.Activities.ActivityContext> 的跟踪方法发出 <xref:System.Activities.Tracking.CustomTrackingRecord>。  
  
 下面的示例演示如何发出自定义活动内的 <xref:System.Activities.Tracking.CustomTrackingRecord> 对象。  
  
```csharp  
// Create the Custom Tracking Record  
CustomTrackingRecord customRecord = new CustomTrackingRecord("OrderIn")  
{  
    Data =   
    {  
        {"OrderId", 200},  
        {"OrderDate", "20 Aug 2001"}  
    }  
};  
  
// Emit custom tracking record  
context.Track(customRecord);  
  
```  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 CustomTrackingSample.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Tracking\CustomTracking`  
  
## 请参阅  
 [AppFabric 监视示例](http://go.microsoft.com/fwlink/?LinkId=193959)