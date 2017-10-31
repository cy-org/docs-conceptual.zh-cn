---
title: "C# 表达式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 29110be7-f4e3-407e-8dbe-78102eb21115
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# C# 表达式
自 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 起，[!INCLUDE[wf](../../../includes/wf-md.md)] 开始支持 C\# 表达式。在 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 中面向 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 新建的 C\# 工作流项目使用 C\# 表达式，而 Visual Basic 工作流项目则使用 Visual Basic 表达式。现有使用 Visual Basic 表达式的 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 工作流项目可以不受项目语言限制而迁移到 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]，并得到支持。本主题概述了 [!INCLUDE[wf1](../../../includes/wf1-md.md)] 中的 C\# 表达式。  
  
## 在工作流中使用 C\# 表达式  
  
-   [在工作流设计器中使用 C# 表达式](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#WFDesigner)  
  
    -   [向后兼容性](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#BackwardCompat)  
  
-   [在代码工作流中使用 C# 表达式](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#CodeWorkflows)  
  
-   [在 XAML 工作流中使用 C# 表达式](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#XamlWorkflows)  
  
    -   [编译型 Xaml](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#CompiledXaml)  
  
    -   [宽松型 Xaml](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#LooseXaml)  
  
-   [在 XAMLX 工作流服务中使用 C# 表达式](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#WFServices)  
  
###  <a name="WFDesigner"></a> 在工作流设计器中使用 C\# 表达式  
 自 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 起，[!INCLUDE[wf](../../../includes/wf-md.md)] 开始支持 C\# 表达式。在 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 中面向 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 创建的 C\# 工作流项目使用 C\# 表达式，而 Visual Basic 工作流项目则使用 Visual Basic 表达式。要指定所需的 C\# 表达式，可将其键入标有**“输入 C\# 表达式”**标签的框中。该标签显示在属性窗口中（当在设计器中选中活动时），或显示在工作流设计器的活动上。下例中，在 `NoPersistScope` 范围内，一个 `Sequence` 中包含了两个 `WriteLine` 活动。  
  
 ![自动创建的序列活动](../../../docs/framework/windows-workflow-foundation//media/autosurround2.png "AutoSurround2")  
  
> [!NOTE]
>  C\# 表达式仅在 [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] 中得到支持，在重新承载的工作流设计器中不予支持。[!INCLUDE[crabout](../../../includes/crabout-md.md)]在重新承载的设计器中支持的新 WF45 功能的更多信息，请参见[重新承载的工作流设计器中新 Workflow Foundation 4.5 功能的支持](../../../docs/framework/windows-workflow-foundation//wf-features-in-the-rehosted-workflow-designer.md)。  
  
####  <a name="BackwardCompat"></a> 向后兼容性  
 在现有已迁移到 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 的 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] C\# 工作流项目中使用的 Visual Basic 表达式是得到支持的。当在工作流设计器中查看 Visual Basic 表达式时，如果 Visual Basic 表达不符合 C\# 语法，则现有 Visual Basic 文本将被替换成**“在 XAML 中设置了值”**。如果 Visual Basic 表达式符合 C\# 语法则予以显示。若要将 Visual Basic 表达式更新为 C\#，可在工作流设计器中编辑这些表达式，指定等效的 C\# 表达式。将 Visual Basic 表达式更新为 C\# 不是必须的，但一旦在工作流设计器中进行更新，这些表达式即转换成 C\# 并不可重新转换为 Visual Basic。  
  
###  <a name="CodeWorkflows"></a> 在代码工作流中使用 C\# 表达式  
 基于 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 代码的工作流支持 C\# 表达式，但 C\# 表达式须用 <xref:System.Activities.XamlIntegration.TextExpressionCompiler.Compile%2A?displayProperty=fullName> 进行编译，然后才能调用工作流。工作流作者可以用 `CSharpValue` 表示表达式的右值，用 `CSharpReference` 表示表达式的左值。在下例中，用一个 `Assign` 活动以及 `Sequence` 活动中所包含的 `WriteLine` 活动创建了一个工作流。为 `Assign` 的 `To` 参数指定了一个 `CSharpReference`，用来表示表达式的左值。为 `Assign` 的 `Value` 参数和 `WriteLine` 的 `Text` 参数指定了一个 `CSharpValue`，用于表示这两个表达式的右值。  
  
```csharp  
Variable<int> n = new Variable<int>  
{  
    Name = "n"  
};  
  
Activity wf = new Sequence  
{  
    Variables = { n },  
    Activities =  
    {  
        new Assign<int>  
        {  
            To = new CSharpReference<int>("n"),  
            Value = new CSharpValue<int>("new Random().Next(1, 101)")  
        },  
        new WriteLine  
        {  
            Text = new CSharpValue<string>("\"The number is \" + n")  
        }  
    }  
};  
  
CompileExpressions(wf);  
  
WorkflowInvoker.Invoke(wf);  
```  
  
 工作流构造完毕后，通过调用 `CompileExpressions` 帮助器方法编译了 C\# 表达式，随后调用工作流。下面的示例为 `CompileExpressions` 方法。  
  
```csharp  
static void CompileExpressions(Activity activity)  
{  
    // activityName is the Namespace.Type of the activity that contains the  
    // C# expressions.  
    string activityName = activity.GetType().ToString();  
  
    // Split activityName into Namespace and Type.Append _CompiledExpressionRoot to the type name  
    // to represent the new type that represents the compiled expressions.  
    // Take everything after the last . for the type name.  
    string activityType = activityName.Split('.').Last() + "_CompiledExpressionRoot";  
    // Take everything before the last . for the namespace.  
    string activityNamespace = string.Join(".", activityName.Split('.').Reverse().Skip(1).Reverse());  
  
    // Create a TextExpressionCompilerSettings.  
    TextExpressionCompilerSettings settings = new TextExpressionCompilerSettings  
    {  
        Activity = activity,  
        Language = "C#",  
        ActivityName = activityType,  
        ActivityNamespace = activityNamespace,  
        RootNamespace = null,  
        GenerateAsPartialClass = false,  
        AlwaysGenerateSource = true,  
        ForImplementation = false  
    };  
  
    // Compile the C# expression.  
    TextExpressionCompilerResults results =  
        new TextExpressionCompiler(settings).Compile();  
  
    // Any compilation errors are contained in the CompilerMessages.  
    if (results.HasErrors)  
    {  
        throw new Exception("Compilation failed.");  
    }  
  
    // Create an instance of the new compiled expression type.  
    ICompiledExpressionRoot compiledExpressionRoot =  
        Activator.CreateInstance(results.ResultType,  
            new object[] { activity }) as ICompiledExpressionRoot;  
  
    // Attach it to the activity.  
    CompiledExpressionInvoker.SetCompiledExpressionRoot(  
        activity, compiledExpressionRoot);  
}  
```  
  
> [!NOTE]
>  如果 C\# 表达式未编译，则调用工作流时将引发 <xref:System.NotSupportedException>，并显示如下类似消息：`Expression Activity type 'CSharpValue`1' requires compilation in order to run.  Please ensure that the workflow has been compiled.`。  
  
 如果基于自定义代码的工作流使用 `DynamicActivity`，则需要对 `CompileExpressions` 方法作一些修改，如下列代码示例所示。  
  
```csharp  
static void CompileExpressions(DynamicActivity dynamicActivity)  
{  
    // activityName is the Namespace.Type of the activity that contains the  
    // C# expressions. For Dynamic Activities this can be retrieved using the  
    // name property , which must be in the form Namespace.Type.  
    string activityName = dynamicActivity.Name;  
  
    // Split activityName into Namespace and Type.Append _CompiledExpressionRoot to the type name  
    // to represent the new type that represents the compiled expressions.  
    // Take everything after the last . for the type name.  
    string activityType = activityName.Split('.').Last() + "_CompiledExpressionRoot";  
    // Take everything before the last . for the namespace.  
    string activityNamespace = string.Join(".", activityName.Split('.').Reverse().Skip(1).Reverse());  
  
    // Create a TextExpressionCompilerSettings.  
    TextExpressionCompilerSettings settings = new TextExpressionCompilerSettings  
    {  
        Activity = dynamicActivity,  
        Language = "C#",  
        ActivityName = activityType,  
        ActivityNamespace = activityNamespace,  
        RootNamespace = null,  
        GenerateAsPartialClass = false,  
        AlwaysGenerateSource = true,  
        ForImplementation = true  
    };  
  
    // Compile the C# expression.  
    TextExpressionCompilerResults results =  
        new TextExpressionCompiler(settings).Compile();  
  
    // Any compilation errors are contained in the CompilerMessages.  
    if (results.HasErrors)  
    {  
        throw new Exception("Compilation failed.");  
    }  
  
    // Create an instance of the new compiled expression type.  
    ICompiledExpressionRoot compiledExpressionRoot =  
        Activator.CreateInstance(results.ResultType,  
            new object[] { dynamicActivity }) as ICompiledExpressionRoot;  
  
    // Attach it to the activity.  
    CompiledExpressionInvoker.SetCompiledExpressionRootForImplementation(  
        dynamicActivity, compiledExpressionRoot);  
}  
```  
  
 在动态活动中编译 C\# 表达式的 `CompileExpressions` 重载中有几处不同。  
  
-   `CompileExpressions` 的参数是一个 `DynamicActivity`。  
  
-   通过使用 `DynamicActivity.Name` 属性检索类型名称和命名空间。  
  
-   将 `TextExpressionCompilerSettings.ForImplementation` 设置为 `true`。  
  
-   调用 `CompiledExpressionInvoker.SetCompiledExpressionRoot` 而非 `CompiledExpressionInvoker.SetCompiledExpressionRootForImplementation`。  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)]在代码中使用表达式的更多信息，请参见[使用命令性代码创作工作流、活动和表达式](../../../docs/framework/windows-workflow-foundation//authoring-workflows-activities-and-expressions-using-imperative-code.md)。  
  
###  <a name="XamlWorkflows"></a> 在 XAML 工作流中使用 C\# 表达式  
 XAML 工作流支持 C\# 表达式。编译型 XAML 工作流被编译到类型中，而宽松型 XAML 工作流由运行时加载，并在工作流执行时编译到活动树中。  
  
-   [编译型 Xaml](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#CompiledXaml)  
  
-   [宽松型 Xaml](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#LooseXaml)  
  
####  <a name="CompiledXaml"></a> 编译型 Xaml  
 编译型 XAML 工作流支持 C\# 表达式，此种工作流编译成类型，作为面向 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 的 C\# 工作流项目的组成部分。编译型 XAML 是以 [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] 编写的默认工作流类型，而在[!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] 中面向 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 创建的 C\# 工作流项目使用 C\# 表达式。  
  
####  <a name="LooseXaml"></a> 宽松型 Xaml  
 宽松型 XAML 工作流支持 C\# 表达式。加载并调用宽松型 XAML 工作流的工作流宿主程序必须面向 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]，而<xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> 必须设为 `true`（默认值为 `false`）。要将 <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> 设置为 `true`，请创建一个 <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings> 实例，创建时将其 <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> 属性设为 `true`，并作为参数传递给 <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A?displayProperty=fullName>。如果 `CompileExpressions` 未设为 `true`，则将引发 <xref:System.NotSupportedException>，并显示如下类似消息：`Expression Activity type 'CSharpValue`1' requires compilation in order to run.  Please ensure that the workflow has been compiled.`。  
  
```csharp  
ActivityXamlServicesSettings settings = new ActivityXamlServicesSettings  
{  
    CompileExpressions = true  
};  
  
DynamicActivity<int> wf = ActivityXamlServices.Load(new StringReader(serializedAB), settings) as DynamicActivity<int>;  
```  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)]使用 XAML 工作流的更多信息，请参见[将工作流和活动序列化为 XAML 和从 XAML 序列化工作流和活动](../../../docs/framework/windows-workflow-foundation//serializing-workflows-and-activities-to-and-from-xaml.md)。  
  
###  <a name="WFServices"></a> 在 XAMLX 工作流服务中使用 C\# 表达式  
 XAMLX 工作流服务支持 C\# 表达式。当工作流服务承载于 IIS 或 WAS 中时，无须执行任何额外步骤，但如果 XAML 工作流服务是自承载的，则 C\# 表达式必须经过编译。要在自承载的 XAMLX 工作流服务中编译 C\# 表达式，应先将 XAMLX 文件加载到 `WorkflowService` 中，然后将 `WorkflowService` 的 `Body` 传递给前面[在代码工作流中使用 C# 表达式](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#CodeWorkflows)中所描述的 `CompileExpressions` 方法。下例加载一个 XAMLX 工作流服务，编译 C\# 表达式，随后打开该工作流服务并等待请求。  
  
```csharp  
// Load the XAMLX workflow service.  
WorkflowService workflow1 =  
    (WorkflowService)XamlServices.Load(xamlxPath);  
  
// Compile the C# expressions in the workflow by passing the Body to CompileExpressions.  
CompileExpressions(workflow1.Body);  
  
// Initialize the WorkflowServiceHost.  
var host = new WorkflowServiceHost(workflow1, new Uri("http://localhost:8293/Service1.xamlx"));  
  
// Enable Metadata publishing/  
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();  
smb.HttpGetEnabled = true;  
smb.MetadataExporter.PolicyVersion = PolicyVersion.Policy15;  
host.Description.Behaviors.Add(smb);  
  
// Open the WorkflowServiceHost and wait for requests.  
host.Open();  
Console.WriteLine("Press enter to quit");  
Console.ReadLine();  
```  
  
 如果 C\# 表达式未编译，那么，虽然 `Open` 操作会成功执行，但工作流在调用时将失败。以下 `CompileExpressions` 方法与上一节[在代码工作流中使用 C# 表达式](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#CodeWorkflows)中的方法相同。  
  
```csharp  
static void CompileExpressions(Activity activity)  
{  
    // activityName is the Namespace.Type of the activity that contains the  
    // C# expressions.  
    string activityName = activity.GetType().ToString();  
  
    // Split activityName into Namespace and Type.Append _CompiledExpressionRoot to the type name  
    // to represent the new type that represents the compiled expressions.  
    // Take everything after the last . for the type name.  
    string activityType = activityName.Split('.').Last() + "_CompiledExpressionRoot";  
    // Take everything before the last . for the namespace.  
    string activityNamespace = string.Join(".", activityName.Split('.').Reverse().Skip(1).Reverse());  
  
    // Create a TextExpressionCompilerSettings.  
    TextExpressionCompilerSettings settings = new TextExpressionCompilerSettings  
    {  
        Activity = activity,  
        Language = "C#",  
        ActivityName = activityType,  
        ActivityNamespace = activityNamespace,  
        RootNamespace = null,  
        GenerateAsPartialClass = false,  
        AlwaysGenerateSource = true,  
        ForImplementation = false  
    };  
  
    // Compile the C# expression.  
    TextExpressionCompilerResults results =  
        new TextExpressionCompiler(settings).Compile();  
  
    // Any compilation errors are contained in the CompilerMessages.  
    if (results.HasErrors)  
    {  
        throw new Exception("Compilation failed.");  
    }  
  
    // Create an instance of the new compiled expression type.  
    ICompiledExpressionRoot compiledExpressionRoot =  
        Activator.CreateInstance(results.ResultType,  
            new object[] { activity }) as ICompiledExpressionRoot;  
  
    // Attach it to the activity.  
    CompiledExpressionInvoker.SetCompiledExpressionRoot(  
        activity, compiledExpressionRoot);  
}  
```