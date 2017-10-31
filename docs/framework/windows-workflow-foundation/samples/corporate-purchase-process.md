---
title: "企业采购过程 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a5e57336-4290-41ea-936d-435593d97055
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 企业采购过程
此示例演示如何使用自动最佳建议书选择来创建基于购买过程的非常基本的征求建议书 \(RFP\)。  它将 <xref:System.Activities.Statements.Parallel>、<xref:System.Activities.Statements.ParallelForEach%601>、<xref:System.Activities.Statements.ForEach%601> 和一个自定义活动组合在一起来创建一个表示该过程的工作流。  
  
 此示例包含一个 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 客户端应用程序，此应用程序允许以不同的参与者身份（如原始请求方或特定的供应商）与该过程进行交互。  
  
## 要求  
  
-   [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]。  
  
-   [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]。  
  
## 演示  
  
-   自定义活动。  
  
-   活动的构成。  
  
-   书签。  
  
-   持久性。  
  
-   程式化的持久性。  
  
-   追踪。  
  
-   跟踪。  
  
-   在不同的客户端（[!INCLUDE[wf1](../../../../includes/wf1-md.md)] Web 应用程序和 WinForms 应用程序）中承载 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Application\PurchaseProcess`  
  
## 流程说明  
 此示例演示如何实现 [!INCLUDE[wf](../../../../includes/wf-md.md)] 程序以便为一般公司收集由供应商提交的建议书。  
  
1.  公司 X 的一名员工创建了一份征求建议书 \(RFP\)。  
  
    1.  该员工键入 RFP 标题和说明。  
  
    2.  该员工选择要请求其提交建议书的供应商。  
  
2.  该员工提交建议书。  
  
    1.  创建一个工作流实例。  
  
    2.  工作流正在等待所有供应商提交其建议书。  
  
3.  在收到所有建议书后，工作流将循环访问所有收到的建议书并选择最佳建议书。  
  
    1.  每个供应商都具有一个信誉（此示例将信誉列表存储在 VendorRepository.cs 中）。  
  
    2.  将（供应商键入的值）\*（记录的供应商信誉）\/100 来计算出建议书的总值。  
  
4.  原始请求方可以查看所有提交的建议书。  最佳建议书将在报告的某个特殊部分中显示。  
  
## 过程定义  
 示例的核心逻辑使用一个 <xref:System.Activities.Statements.ParallelForEach%601> 活动，该活动等待每个供应商的报价（使用创建书签的自定义活动）并将供应商的建议书注册为 RFP（使用 <xref:System.Activities.Statements.InvokeMethod> 活动）。  
  
 然后，此示例循环访问存储在 `RfpRepository` 中的所有收到的建议书，计算调整后的值（使用 <xref:System.Activities.Statements.Assign> 活动和 <xref:System.Activities.Expressions> 活动）；如果调整后的值比先前的最佳报价更可取，则将该新值指定为最佳报价（使用 <xref:System.Activities.Statements.If> 和 <xref:System.Activities.Statements.Assign> 活动）。  
  
## 此示例中的项目  
 此示例包含以下项目。  
  
|Project|描述|  
|-------------|--------|  
|公共|过程中使用的实体对象（征求建议书、供应商和供应商建议书）。|  
|WfDefinition|客户端应用程序用来创建和使用购买过程工作流实例的过程（作为 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 程序）和主机 \(`PurchaseProcessHost`\) 的定义。|  
|WebClient|一个 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 客户端应用程序，它允许用户创建和参与购买过程的实例。  此应用程序使用自定义创建的主机与工作流引擎进行交互。|  
|WinFormsClient|一个 Windows 窗体客户端应用程序，它允许用户创建和参与购买过程的实例。  此应用程序使用自定义创建的主机与工作流引擎进行交互。|  
  
### WfDefinition  
 下表包含对 WfDefinition 项目中最重要文件的说明。  
  
|文件|描述|  
|--------|--------|  
|IPurchaseProcessHost.cs|工作流主机的接口。|  
|PurchaseProcessHost.cs|工作流主机的实现。  该主机提取工作流运行时的详细信息，并在所有客户端应用程序中用于加载和运行 `PurchaseProcess` 工作流实例并与其进行交互。|  
|PurchaseProcessWorkflow.cs|一个包含购买过程工作流定义的活动（派生自 <xref:System.Activities.Activity>）。<br /><br /> 派生自 <xref:System.Activities.Activity> 的活动通过组合现有自定义活动和来自 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 活动库的活动来组合功能。  组合这些活动是创建自定义功能的最基本方法。|  
|WaitForVendorProposal.cs|此自定义活动派生自 <xref:System.Activities.NativeActivity>，并将在提交建议书时创建一个稍后必须由供应商恢复的命名书签。<br /><br /> 从 <xref:System.Activities.NativeActivity> 派生的活动，与从 <xref:System.Activities.CodeActivity> 派生的活动一样，可通过重写 <xref:System.Activities.NativeActivity.Execute%2A> 来创建命令性功能，除此之外还可以通过传递给 <xref:System.Activities.ActivityContext> 方法的 `Execute` 访问工作流运行时的所有功能。  此上下文支持安排和取消子活动、设置非持久性区域（执行阻塞期间，运行时没有保存工作流的数据，如在原子事务内），以及 <xref:System.Activities.Bookmark> 对象（用于继续已暂停工作流的句柄）。|  
|TrackingParticipant.cs|一个 <xref:System.Activities.Tracking.TrackingParticipant>，它接收所有跟踪事件并将这些事件保存到一个文本文件中。<br /><br /> 跟踪参与者将作为扩展添加到工作流实例中。|  
|XmlWorkflowInstanceStore.cs|一个自定义 <xref:System.Runtime.DurableInstancing.InstanceStore>，它将工作流应用程序保存到 XML 文件中。|  
|XmlPersistenceParticipant.cs|一个自定义 <xref:System.Activities.Persistence.PersistenceParticipant>，它将征求建议书实例保存到 XML 文件中。|  
|AsyncResult.cs \/ CompletedAsyncResult.cs|用于在持久性组件中实现异步模式的帮助器类。|  
  
### 公共  
 下表包含对 Common 项目中最重要的类的说明。  
  
|类|描述|  
|-------|--------|  
|Vendor|在征求建议书中提交建议书的供应商。|  
|RequestForProposal|征求建议书 \(RFP\) 是一份邀请，旨在请求供应商提交有关特定商品或服务的建议书。|  
|VendorProposal|供应商针对具体的 RFP 提交的建议书。|  
|VendorRepository|供应商的储存库。  此实现包含一个内存中的集合，其中包括供应商实例和用于公开这些实例的方法。|  
|RfpRepository|征求建议书的储存库。  此实现将使用 Linq to XML 来查询由程式化的持久性所生成的征求建议书的 XML 文件。  此类实现 <xref:System.Runtime.Persistence.IDataViewMapper>。|  
|IOHelper|此类处理所有与 I\/O 有关的问题（文件夹、路径等。）|  
  
### Web 客户端  
 下表包含对 Web Client 项目中最重要网页的说明。  
  
|||  
|-|-|  
|文件|描述|  
|CreateRfp.aspx|创建和提交新的征求建议书。|  
|Default.aspx|显示所有活动的和已完成的征求建议书。|  
|GetVendorProposal.aspx|从具体的征求建议书中获取来自供应商的建议。  此页仅由供应商使用。|  
|ShowRfp.aspx|显示有关征求建议书的所有信息（收到的建议书、日期、值和其他信息）。  此页仅供征求建议书的创建者使用。|  
  
### WinForms Client  
 下表包含对 Win Forms 项目中最重要的窗体的说明。  
  
|||  
|-|-|  
|窗体|描述|  
|NewRfp|创建和提交新的征求建议书。|  
|ShowProposals|显示所有活动的和已完成的征求建议书。 **Note:**  在创建或修改征求建议书后，您可能需要单击 UI 中的**“刷新”**按钮来查看屏幕中的更改。|  
|SubmitProposal|从具体的征求建议书中获取来自供应商的建议。  此窗口仅由供应商使用。|  
|ViewRfp|显示有关征求建议书的所有信息（收到的建议书、日期、值和其他信息）。  此窗口仅供征求建议书的创建者使用。|  
  
### 持久性文件  
 下表显示由永久性提供程序 \(`XmlPersistenceProvider`\) 生成的文件，这些文件位于当前系统的临时文件夹下的路径（使用 <xref:System.IO.Path.GetTempPath%2A>）中。  在当前执行路径中创建跟踪文件。  
  
||||  
|-|-|-|  
|文件名|描述|路径|  
|rfps.xml|具有所有活动的和已完成的征求建议书的 XML 文件。|<xref:System.IO.Path.GetTempPath%2A>|  
|\[instanceid\]|此文件包含有关工作流实例的所有信息。<br /><br /> 此文件由程式化的持久性实现生成（XmlPersistenceProvider 中的 PersistenceParticipant）。|<xref:System.IO.Path.GetTempPath%2A>|  
|\[instanceId\].tracking|一个包含具体实例中发生的所有事件的文本文件。<br /><br /> 此文件由 TrackingParticipant 生成。|<xref:System.IO.Path.GetTempPath%2A>|  
|PurchaseProcess.Tracing.TraceLog.txt|由基于 App.config 文件或 Web.config 文件中的配置参数的工作流生成的跟踪文件。|当前执行路径|  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 PurchaseProcess.sln 解决方案文件。  
  
2.  若要执行 Web Client 项目，请打开**“解决方案资源管理器”**，并右击**“Web Client”**项目。  选择**“设为启动项目”**。  
  
3.  若要执行 WinForms Client 项目，请打开**“解决方案资源管理器”**，并右击**“WinForms Client”**项目。  选择**“设为启动项目”**。  
  
4.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
5.  若要运行解决方案，请按 Ctrl\+F5。  
  
### Web Client 选项  
  
-   **Create a new RFP（创建新的 RFP）**：创建新的征求建议书 \(RFP\) 并启动购买过程工作流。  
  
-   **Refresh（刷新）**：在主窗口中刷新活动的 RFP 和已完成的 RFP 的列表。  
  
-   **View（查看）**：显示现有 RFP 的内容。  供应商可提交其建议书（如果受到邀请或 RFP 尚未完成）。  
  
-   View As（查看者身份）：用户可通过在活动的 RFP 网格的**“View as”**（查看者身份）组合框中选择所需的参与者，使用不同的标识访问 RFP。  
  
### WinForms Client 选项  
  
-   **Create RFP（创建 RFP）**：创建新的征求建议书 \(RFP\) 并启动购买过程工作流。  
  
-   **Refresh（刷新）**：在主窗口中刷新活动的 RFP 和已完成的 RFP 的列表。  
  
-   **View RFP（查看 RFP）**：显示现有 RFP 的内容。  供应商可提交其建议书（如果受到邀请或 RFP 尚未完成）。  
  
-   **Connect As（连接者身份）**：用户可通过在活动的 RFP 网格的**“View as”（查看者身份）**组合框中选择所需的参与者，使用不同的标识访问 RFP。  
  
## 请参阅