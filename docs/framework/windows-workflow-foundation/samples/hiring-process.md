---
title: "招聘流程 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5fcacbb-c884-4b37-a5d6-02b1b8eec7b4
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# 招聘流程
本示例演示如何使用消息传递活动和作为工作流服务承载的两个工作流来实现业务流程。这些工作流是 Contoso, Inc 虚构公司的 IT 基础结构的一部分。  
  
 `HiringRequest` 工作流程（实现为 <xref:System.Activities.Statements.Flowchart>）需经组织的多名经理授权。为了实现此目标，此工作流使用组织中的其他现有服务（对我们而言，是实现为纯 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务的收件箱服务和组织数据服务）。  
  
 `ResumeRequest` 工作流（实现为 <xref:System.Activities.Statements.Sequence>）在 Contoso 的外部工作机会网站中发布一份招聘启事并管理收到的简历。一份招聘启事可在外部网站中存在一段固定的时间，直到截止日期到期为止，或直到 Contoso 的某名员工决定删除它为止。  
  
 此示例演示 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 的以下功能：  
  
-   用于对业务流程进行建模的 <xref:System.Activities.Statements.Flowchart> 和 <xref:System.Activities.Statements.Sequence> 工作流。  
  
-   工作流服务。  
  
-   消息传递活动。  
  
-   基于内容的相关性。  
  
-   自定义活动（声明性和基于代码）。  
  
-   系统提供的 SQL Server 持久性。  
  
-   自定义的 <xref:System.Activities.Persistence.PersistenceParticipant>。  
  
-   自定义跟踪。  
  
-   Windows 事件跟踪 \(ETW\) 跟踪。  
  
-   活动撰写。  
  
-   <xref:System.Activities.Statements.Parallel> 活动。  
  
-   <xref:System.Activities.Statements.CancellationScope> 活动。  
  
-   持久性计时器（<xref:System.Activities.Statements.Delay> 活动）。  
  
-   事务。  
  
-   同一个解决方案中多个工作流。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Application\HiringProcess`  
  
## 流程说明  
 Contoso, Inc.希望严密控制其每个部门的员工总数。因此，每当有任意员工想要启动新的招聘流程时，在招聘实际发生之前，这些员工都需要经过招聘请求流程的审批。此流程称为招聘流程请求（在 HiringRequestService 项目中定义），它包括以下几个步骤：  
  
1.  员工（请求方）启动招聘流程请求。  
  
2.  请求方的经理必须审批请求：  
  
    1.  经理可以拒绝请求。  
  
    2.  经理可将请求返回给请求方以获取其他信息：  
  
        1.  请求方复查请求并将请求发送回经理。  
  
    3.  经理可以批准请求。  
  
3.  在请求方的经理批准后，部门所有人必须审批请求：  
  
    1.  部门所有人可以拒绝请求。  
  
    2.  部门所有人可以批准请求。  
  
4.  在部门所有人批准后，流程需要经过两名 HR 经理或 CEO 的审批：  
  
    1.  流程可转换为已接受或已拒绝状态。  
  
    2.  如果流程为已接受状态，则启动 `ResumeRequest` 工作流的新实例（通过服务引用将 `ResumeRequest` 链接到 HiringRequest.csproj）。  
  
 一旦经理批准招聘新员工，HR 必须找到合适的人选。此流程由第二个工作流（在 ResumeRequestService.csproj 中定义的 `ResumeRequest`）执行。此工作流定义向 Contoso 的外部工作机会网站提交提供职位空缺的招聘启事的流程，接收申请人的简历并监视招聘启事的状态。职位可存在一段固定的时间，直到时间到期为止，或直到 Contoso 的某员工决定删除它为止。`ResumeRequest` 工作流包含以下几个步骤：  
  
1.  Contoso 的某员工键入有关职位和超时持续时间的信息。在员工键入此类信息之后，相应职位将发布在工作机会网站上。  
  
2.  信息一经发布，感兴趣的人即可提交自己的简历。提交简历时，将简历存储在链接到职位空缺的记录中。  
  
3.  在超时到期之前，或 Contoso HR 部门的某员工通过停止流程明确决定删除此招聘信息之前，申请者均可提交简历。  
  
## 示例中的项目  
 下表显示示例解决方案中的项目。  
  
|项目|说明|  
|--------|--------|  
|ContosoHR|包含数据协定、业务对象和储存库类。|  
|HiringRequestService|包含招聘请求流程工作流的定义。<br /><br /> 此项目实现为控制台应用程序，该应用程序自承载作为服务的工作流（xaml 文件）。|  
|ResumeRequestService|收集申请者的简历（直到超时到期或有人决定必须停止此流程为止）的工作流服务。<br /><br /> 此项目实现为声明性工作流服务 \(xamlx\)。|  
|OrgService|公开组织信息（员工、职位、职位类型和部门）的服务。可将此服务视为企业资源计划 \(ERP\) 的公司组织模块。<br /><br /> 此项目实现为公开 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务的控制台应用程序。|  
|InboxService|包含针对员工的可操作任务的收件箱。<br /><br /> 此项目实现为公开 WCF 服务的控制台应用程序。|  
|InternalClient|与流程交互的 Web 应用程序。用户可启动、参与和查看其 HiringProcess 工作流。通过使用此应用程序，用户还可以启动和监视 ResumeRequest 流程。<br /><br /> 此网站实现为 Contoso 的 Intranet 内部网站。此项目实现为 ASP.NET 网站。|  
|CareersWebSite|公开 Contoso 的空缺职位的外部网站。任意可能的申请者都可导航到此网站并提交简历。|  
  
## 功能概述  
 下表说明每个功能在此示例中的使用方式。  
  
|功能|说明|项目|  
|--------|--------|--------|  
|流程图|业务流程表示为流程图。此流程图说明表示流程的方式与业务在白板中绘制流程的方式相同。|HiringRequestService|  
|工作流服务|包含流程定义的流程图承载于某服务（在此示例中，此服务承载于控制台应用程序中）。|HiringRequestService|  
|消息传递活动|此流程图以两种方式使用消息传递活动：<br /><br /> -   获取用户信息（以接收每个审批步骤中的决定及相关信息）。<br />-   与其他现有服务（可通过服务引用使用的 InboxService 和 OrgDataService）交互。|HiringRequestService|  
|基于内容的相关性|批准消息根据招聘请求的 ID 属性相关：<br /><br /> -   启动流程时，使用请求 ID 初始化相关性句柄。<br />-   传入的批准消息根据其 ID 相关（每个批准消息的第一个参数即为请求的 ID）。|HiringRequestService \/ ResumeRequestService|  
|自定义活动（声明性和基于代码）|此示例中有几个自定义活动：<br /><br /> -   `SaveActionTracking`：此活动发出一个自定义的 <xref:System.Activities.Tracking.TrackingRecord>（使用 <xref:System.Activities.NativeActivityContext.Track%2A>）。此活动已使用命令性代码扩展 <xref:System.Activities.NativeActivity> 进行创作。<br />-   `GetEmployeesByPositionTypes`：此活动接收职位类型 ID 的列表，并返回在 Contoso 中拥有相应职位的人员列表。此活动已通过声明性方式进行创作（使用活动设计器）。<br />-   `SaveHiringRequestInfo`：此活动保存 `HiringRequest` 的信息（使用 `HiringRequestRepository.Save`）。此活动已使用命令性代码扩展 <xref:System.Activities.CodeActivity> 进行创作。|HiringRequestService|  
|系统提供的 SQL Server 持久性|将承载流程图过程定义的 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 实例配置为使用系统提供的 SQL Server 持久性。|HiringRequestService \/ ResumeRequestService|  
|自定义跟踪|此示例包含保存 `HiringRequestProcess` 的历史记录（记录完成的操作、执行者以及执行时间）的自定义跟踪参与者。源代码位于 HiringRequestService 的跟踪文件夹中。|HiringRequestService|  
|ETW 跟踪|在 HiringRequestService 服务的 App.config 文件中配置系统提供的 ETW 跟踪。|HiringRequestService|  
|活动撰写|此过程定义使用 <xref:System.Activities.Activity> 的自由撰写。流程图包含若干个顺序活动和并行活动，而这些活动同时又包含其他活动，等待。|HiringRequestService|  
|并行活动|-   <xref:System.Activities.Statements.ParallelForEach%601> 用于以并行方式在 CEO 和 HR 经理的收件箱中注册（等待两名 HR 经理的审批步骤）。<br />-   <xref:System.Activities.Statements.Parallel> 用于在“已完成”和“已拒绝”步骤中执行一些清理任务。|HiringRequestService|  
|模型取消|此流程图使用 <xref:System.Activities.Statements.CancellationScope> 创建取消行为（在此情况下它执行一些清理操作）。|HiringRequestService|  
|客户持久性参与者|`HiringRequestPersistenceParticipant` 将工作流变量中的数据保存到 Contoso HR 数据库中存储的某个表中。|HiringRequestService|  
|工作流服务|使用工作流服务实现 `ResumeRequestService`。工作流定义和服务信息包含在 ResumeRequestService.xamlx 中。此服务配置为使用持久性和跟踪。|ResumeRequestService|  
|持久性计时器|`ResumeRequestService` 使用持久性计时器定义招聘启事的持续时间（一旦超时到期，将关闭招聘启事）。|ResumeRequestService|  
|事务|<xref:System.Activities.Statements.TransactionScope> 用于确保数据在若干个活动的执行期间（接收新简历时）保持一致。|ResumeRequestService|  
|事务|自定义持久性参与者 \(`HiringRequestPersistenceParticipant`\) 和自定义跟踪参与者 \(`HistoryFileTrackingParticipant`\) 使用相同的事务。|HiringRequestService|  
|在 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序中使用 [!INCLUDE[wf1](../../../../includes/wf1-md.md)]。|从两个 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序访问工作流。|InternalClient \/ CareersWebSite|  
  
## 数据存储  
 数据存储在名为 `ContosoHR` 的 SQL Server 数据库中（创建此数据库的脚本位于 `DbSetup` 文件夹中）。工作流实例存储在名为 `InstanceStore` 的 SQL Server 数据库中（创建实例存储的脚本是 [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] 分布的一部分）。  
  
 通过从 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 命令提示中运行 Setup.cmd 脚本可创建这两个数据库。  
  
## 运行示例  
  
#### 创建数据库  
  
1.  打开 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 命令提示符。  
  
2.  导航到示例文件夹。  
  
3.  运行 Setup.cmd。  
  
4.  验证 `ContosoHR` 和 `InstanceStore` 这两个数据库是否已在 SQL Express 中创建。  
  
#### 设置执行解决方案  
  
1.  以管理员身份运行 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]。打开 HiringRequest.sln。  
  
2.  在**“解决方案资源管理器”**中右键单击此解决方案并选择**“属性”**。  
  
3.  选择**“多启动项目”**选项，然后将**“CareersWebSite”**、**“InternalClient”**、**“HiringRequestService”**和**“ResumeRequestService”**设置为**“启动”**。保留**“ContosoHR”**、**“InboxService”**和**“OrgService”**为“无”。  
  
4.  按 Ctrl\+Shift\+B 生成解决方案。验证此生成是否已成功。  
  
#### 运行解决方案  
  
1.  解决方案生成后，按 Ctrl\+F5 无需调试即可运行。验证所有服务是否已启动。  
  
2.  在解决方案中右键单击**“InternalClient”**，然后选择**“用浏览器查看”**。随即显示 `InternalClient` 的默认页。确保服务正在运行，然后单击链接。  
  
3.  将显示**“HiringRequest”**模块。可遵循此处详细描述的方案。  
  
4.  `HiringRequest` 完成后，可启动 `ResumeRequest`。可遵循此处详细描述的方案。  
  
5.  发布 `ResumeRequest` 时，信息将显示在公共网站（Contoso 工作机会网站）中。若要查看招聘启事和申请职位，请导航到此工作机会网站。  
  
6.  在解决方案中右键单击**“CareersWebSite”**，然后选择**“用浏览器查看”**。  
  
7.  通过在解决方案中右键单击**“InternalClient”**并选择**“用浏览器查看”**，导航回 `InternalClient`。  
  
8.  通过单击收件箱顶部菜单中的**“招聘启事”**链接，转到**“JobPostings”**部分。可遵循此处详细描述的方案。  
  
## 方案  
  
### 招聘请求  
  
1.  Michael Alexander（软件工程师）希望请求一个新职位，以便在工程部门雇佣一名至少具有 3 年 C\# 使用经验的软件开发测试工程师 \(SDET\)。  
  
2.  创建后，此请求将出现在 Michael 的收件箱中（如果您看不到此请求，请单击**“刷新”**），等待 Michael 的经理 Peter Brehm 的审批。  
  
3.  Peter 需要处理 Michael 的请求。他认为此职位需要 5 年的 C\# 工作经验而不是 3 年，因此他发回自己的建议以进行复查。  
  
4.  Michael 查看收件箱中来自他的经理的邮件并需要执行操作。Michael 查看此职位请求的历史记录，并同意 Peter 的建议。Michael 修改说明以要求 5 年的 C\# 工作经验，并接受修改。  
  
5.  Peter 处理 Michael 修改过的请求，并接受它。现在必须由工程总监 Tsvi Reiter 审批此请求。  
  
6.  Tsvi Reiter 希望迅速发出此请求，因此，他加上一条注释，说明此请求非常紧急并接受它。  
  
7.  现在必须由两名 HR 经理或 CEO 审批此请求。CEO Brian Richard Goldstein 看到了 Tsvi 发出的此紧急请求。他接受此请求，从而不再需要两名 HR 经理的审批。  
  
8.  此请求将会从 Michael 的收件箱中删除，招聘 SDET 的过程现已开始。  
  
### 启动简历请求  
  
1.  现在，此招聘启事正等待发布到人们可申请的外部网站（单击**“招聘启事”**链接可进行查看）。目前，此招聘启事由 HR 代表接手，他负责最后确定招聘启事并进行发布。  
  
2.  HR 希望编辑此招聘启事（通过单击**“编辑”**链接）将超时设置为 60 分钟（现实生活中，此值可以是几天或几个星期）。超时允许根据指定的时间从外部网站中删除此招聘启事。  
  
3.  在保存编辑的招聘启事后，它将显示在**“接收简历”**选项卡中（刷新网页可看到此新招聘启事）。  
  
### 收集简历  
  
1.  招聘启事应显示在外部网站上。如果某人对此工作有兴趣，则可申请此职位并提交简历。  
  
2.  如果返回到“招聘启事列表”服务，您可“查看简历”（目前为止已收集到的简历）。  
  
3.  HR 还可停止收集简历（例如，确定了合适的人选）。  
  
## 疑难解答  
  
1.  确保您使用管理员权限运行 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]。  
  
2.  如果生成解决方案失败，请验证以下内容：  
  
    -   `InternalClient` 或 `CareersWebSite` 项目不缺少对 `ContosoHR` 的引用。  
  
3.  如果执行解决方案失败，请验证以下内容：  
  
    1.  所有服务正在运行。  
  
    2.  服务引用已更新。  
  
        1.  打开 App\_WebReferences 文件夹  
  
        2.  右键单击**“Contoso”**，并选择**“更新 Web\/服务引用”**。  
  
        3.  在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 中按 Ctrl\+Shift\+B 重新生成解决方案。  
  
## 卸载  
  
1.  通过运行 Cleanup.bat 删除位于 DbSetup 文件夹的 SQL Server 实例存储。  
  
2.  从硬盘上删除源代码。  
  
## 请参阅