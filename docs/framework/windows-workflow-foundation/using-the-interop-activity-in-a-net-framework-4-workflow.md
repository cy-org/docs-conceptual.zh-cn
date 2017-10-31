---
title: "在 .NET Framework 4 工作流中使用 Interop 活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9bb747f0-eb33-4f70-84cd-317382372dcd
caps.latest.revision: 20
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 20
---
# 在 .NET Framework 4 工作流中使用 Interop 活动
使用创建的活动 [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] 或 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 可以采用 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 通过使用工作流 <xref:System.Activities.Statements.Interop> 活动。 本主题将概述使用 <xref:System.Activities.Statements.Interop> 活动。  
  
> [!NOTE]
>   <xref:System.Activities.Statements.Interop> 活动不会不会显示在工作流设计器工具箱除非工作流的项目都有其 **目标框架** 设置设为 **.Net Framework 4** 或更高版本。  
  
## <a name="using-the-interop-activity-in-net-framework-45-workflows"></a>在 .NET Framework 4.5 工作流中使用 Interop 活动  
 在本主题中，将要创建一个包含 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 活动的 `DiscountCalculator` 活动库。  `DiscountCalculator` 计算折扣基于购买量，组成 <xref:System.Workflow.Activities.SequenceActivity> ，其中包含 <xref:System.Workflow.Activities.PolicyActivity>。  
  
> [!NOTE]
>   [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 本主题中创建的活动使用 <xref:System.Workflow.Activities.PolicyActivity> 来实现该活动的逻辑。 不需要使用自定义 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 活动或 <xref:System.Activities.Statements.Interop> 若要使用的活动中的规则 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 工作流。 有关示例中使用规则的 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 工作流，而无需使用 <xref:System.Activities.Statements.Interop> 活动，请参阅 [.NET Framework 4.5 中的 Policy 活动](../../../docs/framework/windows-workflow-foundation/samples/policy-activity-in-net-framework-4-5.md) 示例。  
  
#### <a name="to-create-the-net-framework-35-activity-library-project"></a>创建 .NET Framework 3.5 活动库项目  
  
1.  打开 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] ，然后选择 **新建** 然后 **项目...** 从 **文件** 菜单。  
  
2.  展开 **其他项目类型** 中的节点 **已安装的模板** 窗格，然后选择 **Visual Studio 解决方案**。  
  
3.  选择 **空白解决方案** 从 **Visual Studio 解决方案** 列表。 类型 `PolicyInteropDemo` 中 **名称** 框中，单击 **确定**。  
  
4.  用鼠标右键单击 **PolicyInteropDemo** 中 **解决方案资源管理器** ，然后选择 **添加** 然后 **新建项目 …**。  
  
    > [!TIP]
    >  如果 **解决方案资源管理器** 窗口不可见，请选择 **解决方案资源管理器** 从 **视图** 菜单。  
  
5.  在 **已安装的模板** 列表中，选择 **Visual C#** 然后 **工作流**。 选择 **.NET Framework 3.5** 从.NET Framework 版本下拉列表，然后选择 **工作流活动库** 从 **模板** 列表。  
  
6.  类型 `PolicyActivityLibrary` 中 **名称** 框中，单击 **确定**。  
  
7.  用鼠标右键单击 **Activity1.cs** 中 **解决方案资源管理器** ，然后选择 **删除**。 单击 **“确定”** 以确认。  
  
#### <a name="to-create-the-discountcalculator-activity"></a>创建 DiscountCalculator 活动  
  
1.  用鼠标右键单击 **PolicyActivityLibrary** 中 **解决方案资源管理器** ，然后选择 **添加** 然后 **活动 …**。  
  
2.  选择 **Activity （具有单独的代码）** 从 **Visual C# 项** 列表。 类型 `DiscountCalculator` 中 **名称** 框中，单击 **确定**。  
  
3.  用鼠标右键单击 **DiscountCalculator.xoml** 中 **解决方案资源管理器** ，然后选择 **查看代码**。  
  
4.  将以下三个属性添加到 `DiscountCalculator` 类中。  
  
    ```csharp  
    public partial class DiscountCalculator : SequenceActivity  
    {  
        public double Subtotal { get; set; }  
        public double DiscountPercent { get; set; }  
        public double Total { get; set; }  
    }  
    ```  
  
5.  用鼠标右键单击 **DiscountCalculator.xoml** 中 **解决方案资源管理器** ，然后选择 **视图设计器**。  
  
6.  拖动 **策略** 活动从 **Windows Workflow v3.0** 部分 **工具箱** 并将其放 **DiscountCalculator** 活动。  
  
    > [!TIP]
    >  如果 **工具箱** 窗口不可见，请选择 **工具箱** 从 **视图** 菜单。  
  
#### <a name="to-configure-the-rules"></a>配置规则  
  
1.  单击新添加 **策略** 活动以选择它，如果未选中。  
  
2.  单击 **rulesetreference** 中的属性 **属性** 窗口选择它，然后单击属性右侧的省略号按钮。  
  
    > [!TIP]
    >  如果 **属性** 窗口不可见，请选择 **属性窗口** 从 **视图** 菜单。  
  
3.  选择 **单击新建...**。  
  
4.  单击 **添加规则**。  
  
5.  将以下表达式键入 **条件** 框。  
  
    ```  
    this.Subtotal >= 50 && this.Subtotal < 100  
    ```  
  
6.  将以下表达式键入 **Then 操作** 框。  
  
    ```  
    this.DiscountPercent = 0.075  
    ```  
  
7.  单击 **添加规则**。  
  
8.  将以下表达式键入 **条件** 框。  
  
    ```  
    this.Subtotal >= 100  
    ```  
  
9. 将以下表达式键入 **Then 操作** 框。  
  
    ```  
    this.DiscountPercent = 0.15  
    ```  
  
10. 单击 **添加规则**。  
  
11. 将以下表达式键入 **条件** 框。  
  
    ```  
    this.DiscountPercent > 0  
    ```  
  
12. 将以下表达式键入 **Then 操作** 框。  
  
    ```  
    this.Total = this.Subtotal - this.Subtotal * this.DiscountPercent  
    ```  
  
13. 将以下表达式键入 **Else 操作** 框。  
  
    ```  
    this.Total = this.Subtotal  
    ```  
  
14. 单击 **确定** 关闭 **规则集编辑器** 对话框。  
  
15. 确保新创建 <xref:System.Workflow.Activities.Rules.RuleSet> 中选定 **名称** 列表，然后单击 **确定**。  
  
16. 按 Ctrl+Shift+B 生成解决方案。  
  
 在此过程中添加到 `DiscountCalculator` 活动中的规则如下面的代码示例所示。  
  
```  
Rule1: IF this.Subtotal >= 50 && this.Subtotal < 100   
       THEN this.DiscountPercent = 0.075   
  
Rule2: IF this. Subtotal >= 100   
       THEN this.DiscountPercent = 0.15   
  
Rule3: IF this.DiscountPercent > 0   
       THEN this.Total = this.Subtotal - this.Subtotal * this.DiscountPercent   
       ELSE this.Total = this.Subtotal  
```  
  
 当 <xref:System.Workflow.Activities.PolicyActivity> 执行，这三个规则会计算和修改 `Subtotal`, ，`DiscountPercent`, ，和 `Total` 属性值 `DiscountCalculator` 活动来计算所需的折扣。  
  
## <a name="using-the-discountcalculator-activity-with-the-interop-activity"></a>将 DiscountCalculator 活动与 Interop 活动一起使用  
 若要使用 `DiscountCalculator` 内的活动中 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 工作流， <xref:System.Activities.Statements.Interop> 使用活动。 在本节中两个工作流创建，使用代码和使用工作流设计器，它们演示如何使用 <xref:System.Activities.Statements.Interop> 活动 `DiscountCalculator` 活动。 这两个工作流使用同一主机应用程序。  
  
#### <a name="to-create-the-host-application"></a>创建主机应用程序  
  
1.  用鼠标右键单击 **PolicyInteropDemo** 中 **解决方案资源管理器** ，然后选择 **添加**, ，然后 **新建项目 …**。  
  
2.  确保 **.NET Framework 4.5** 在.NET Framework 版本下拉列表中，选择，并且选择  **工作流控制台应用程序** 从 **Visual C# 项** 列表。  
  
3.  类型 `PolicyInteropHost` 到 **名称** 框中，单击 **确定**。  
  
4.  用鼠标右键单击 **PolicyInteropHost** 中 **解决方案资源管理器** ，然后选择 **属性**。  
  
5.  在 **目标框架** 下拉列表中，将选项从 **.NET Framework 4 Client Profile** 到 **.NET Framework 4.5**。 单击 **是** 以确认。  
  
6.  用鼠标右键单击 **PolicyInteropHost** 中 **解决方案资源管理器** ，然后选择 **添加引用...**。  
  
7.  选择 **PolicyActivityLibrary** 从 **项目** 选项卡上，单击 **确定**。  
  
8.  用鼠标右键单击 **PolicyInteropHost** 中 **解决方案资源管理器** ，然后选择 **添加引用...**。  
  
9. 选择 **System.Workflow.Activities**, ，**System.Workflow.ComponentModel**, ，然后 **System.Workflow.Runtime** 从 **.NET** 选项卡上，单击 **确定**。  
  
10. 用鼠标右键单击 **PolicyInteropHost** 中 **解决方案资源管理器** ，然后选择 **设为启动项目**。  
  
11. 按 Ctrl+Shift+B 生成解决方案。  
  
### <a name="using-the-interop-activity-in-code"></a>在代码中使用 Interop 活动  
 在此示例中，使用包含的代码创建工作流定义 <xref:System.Activities.Statements.Interop> 活动和 `DiscountCalculator` 活动。 使用调用此工作流 <xref:System.Activities.WorkflowInvoker> 并将规则计算的结果将写入到控制台使用 <xref:System.Activities.Statements.WriteLine> 活动。  
  
##### <a name="to-use-the-interop-activity-in-code"></a>在代码中使用 Interop 活动  
  
1.  用鼠标右键单击 **Program.cs** 中 **解决方案资源管理器** ，然后选择 **查看代码**。  
  
2.  将下面的 `using` 语句添加到文件的顶部。  
  
    ```csharp  
    using PolicyActivityLibrary;  
    ```  
  
3.  移除 `Main` 方法的内容并替换为以下代码。  
  
    ```csharp  
    static void Main(string[] args)  
    {  
        CalculateDiscountUsingCodeWorkflow();  
    }  
    ```  
  
4.  在 `Program` 类中创建一个名为 `CalculateDiscountUsingCodeWorkflow` 的新方法，此方法包含以下代码。  
  
    ```csharp  
    static void CalculateDiscountUsingCodeWorkflow()  
    {  
        Variable<double> Subtotal = new Variable<double>  
        {  
            Default = 75.99,  
            Name = "Subtotal"  
        };  
  
        Variable<double> DiscountPercent = new Variable<double>  
        {  
            Name = "DiscountPercent"  
        };  
  
        Variable<double> Total = new Variable<double>  
        {  
            Name = "Total"  
        };  
  
        Activity wf = new Sequence  
        {  
            Variables = { Subtotal, DiscountPercent, Total },  
            Activities =   
            {  
                new Interop  
                {  
                    ActivityType = typeof(DiscountCalculator),  
                    ActivityProperties =   
                    {  
                        { "Subtotal", new InArgument<double>(Subtotal) },  
                        { "DiscountPercentOut", new OutArgument<double>(DiscountPercent) },  
                        { "TotalOut", new OutArgument<double>(Total) }  
                    }  
                },  
                new WriteLine  
                {  
                    Text =  new InArgument<string>(env =>   
                        string.Format("Subtotal: {0:C}, Discount {1}%, Total {2:C}",   
                        Subtotal.Get(env), DiscountPercent.Get(env) * 100, Total.Get(env)))  
                }  
            }  
        };  
  
        WorkflowInvoker.Invoke(wf);  
    }  
    ```  
  
    > [!NOTE]
    >   `Subtotal`, ，`DiscountPercent`, ，和 `Total` 属性 `DiscountCalculator` 活动作为参数的 <xref:System.Activities.Statements.Interop> 活动，并在绑定到本地工作流变量 <xref:System.Activities.Statements.Interop> 活动的 <xref:System.Activities.Statements.Interop.ActivityProperties%2A> 集合。 `Subtotal` 添加为 <xref:System.Activities.ArgumentDirection> 参数因为 `Subtotal` 数据流入 <xref:System.Activities.Statements.Interop> 活动，和 `DiscountPercent` 和 `Total` 添加为 <xref:System.Activities.ArgumentDirection> 参数由于它们的数据流向外 <xref:System.Activities.Statements.Interop> 活动。 请注意，这两个 <xref:System.Activities.ArgumentDirection> 参数添加具有名称 `DiscountPercentOut` 和 `TotalOut` 以指示它们表示 <xref:System.Activities.ArgumentDirection> 参数。  `DiscountCalculator` 类型指定为 <xref:System.Activities.Statements.Interop> 活动的 <xref:System.Activities.Statements.Interop.ActivityType%2A>。  
  
5.  按 Ctrl+F5 生成并运行应用程序。 将 `Subtotal` 值替换为不同值以测试由 `DiscountCalculator` 活动提供的不同折扣级别。  
  
    ```csharp  
    Variable<double> Subtotal = new Variable<double>  
    {  
        Default = 75.99, // Change this value.  
        Name = "Subtotal"  
    };  
    ```  
  
### <a name="using-the-interop-activity-in-the-workflow-designer"></a>在工作流设计器中使用 Interop 活动  
 在本示例中，工作流是使用工作流设计器创建的。 此工作流具有相同的功能与前面的示例中，除比而不是使用 <xref:System.Activities.Statements.WriteLine> 活动来显示折扣，宿主应用程序检索并在工作流完成时，显示折扣信息。 此外，调用该工作流时，自变量在工作流设计器中创建并且从宿主传入值，而不是使用局部工作流变量来包含数据。  
  
##### <a name="to-host-the-policyactivity-using-a-workflow-designer-created-workflow"></a>使用工作流设计器创建的工作流承载 PolicyActivity  
  
1.  用鼠标右键单击 **Workflow1.xaml** 中 **解决方案资源管理器** ，然后选择 **删除**。 单击 **“确定”** 以确认。  
  
2.  用鼠标右键单击 **PolicyInteropHost** 中 **解决方案资源管理器** ，然后选择 **添加**, ，**新项 …**。  
  
3.  展开 **Visual C# 项** 节点，然后选择 **工作流**。 选择 **活动** 从 **Visual C# 项** 列表。  
  
4.  类型 `DiscountWorkflow` 到 **名称** 框中，单击 **添加**。  
  
5.  单击 **参数** 按钮上显示工作流设计器左下方 **参数** 窗格。  
  
6.  单击 **创建参数**。  
  
7.  类型 `Subtotal` 到 **名称** 框中，选择 **中** 从 **方向** 下拉列表中，选择 **Double** 从 **参数类型** 下拉列表中，然后按 enter 键保存该参数。  
  
    > [!NOTE]
    >  如果 **Double** 未处于 **参数类型** 下拉列表中，选择 **浏览类型 …**, ，类型 `System.Double` 中 **类型名称** 框，然后单击 **确定**。  
  
8.  单击 **创建参数**。  
  
9. 类型 `DiscountPercent` 到 **名称** 框中，选择 **出** 从 **方向** 下拉列表中，选择 **Double** 从 **参数类型** 下拉列表中，然后按 enter 键保存该参数。  
  
10. 单击 **创建参数**。  
  
11. 类型 `Total` 到 **名称** 框中，选择 **出** 从 **方向** 下拉列表中，选择 **Double** 从 **参数类型** 下拉列表中，然后按 enter 键保存该参数。  
  
12. 单击 **参数** 按钮以关闭工作流设计器左下方 **参数** 窗格。  
  
13. 拖动 **序列** 活动从 **控制流** 部分 **工具箱** 并将其放到工作流设计器图面上。  
  
14. 拖动 **互操作** 活动从 **迁移** 部分 **工具箱** 并将其放 **序列** 活动。  
  
15. 单击 **互操作** 上的活动 **单击此项可浏览...** 标签中，键入 **DiscountCalculator** 中 **类型名称** 框，然后单击 **确定**。  
  
    > [!NOTE]
    >  当 <xref:System.Activities.Statements.Interop> 活动添加到工作流和 `DiscountCalculator` 类型指定为其 <xref:System.Activities.Statements.Interop.ActivityType%2A>, 、 <xref:System.Activities.Statements.Interop> 活动会公开三个 <xref:System.Activities.ArgumentDirection> 参数和三个 <xref:System.Activities.ArgumentDirection> 参数，它们表示的三个公共属性 `DiscountCalculator` 活动。  <xref:System.Activities.ArgumentDirection> 参数具有相同的名称作为三个公共属性，而三个 <xref:System.Activities.ArgumentDirection> 参数具有相同的名称与 **出** 追加到属性名称。 在下面的步骤中，在上一步骤中创建的工作流参数绑定到 <xref:System.Activities.Statements.Interop> 活动的参数。  
  
16. 类型 `DiscountPercent` 到 **输入 VB 表达式** 右侧的框中 **DiscountPercentOut** 属性然后按 tab 键。  
  
17. 类型 `Subtotal` 到 **输入 VB 表达式** 右侧的框中 **Subtotal** 属性然后按 tab 键。  
  
18. 类型 `Total` 到 **输入 VB 表达式** 右侧的框中 **TotalOut** 属性然后按 tab 键。  
  
19. 用鼠标右键单击 **Program.cs** 中 **解决方案资源管理器** ，然后选择 **查看代码**。  
  
20. 将下面的 `using` 语句添加到文件的顶部。  
  
    ```csharp  
    using System.Collections.Generic;  
    ```  
  
21. 注释掉 `CalculateDiscountInCode` 方法中对 `Main` 方法的调用，然后添加以下代码。  
  
    > [!NOTE]
    >  如果您没有按照前面的过程操作且存在默认 `Main` 代码，请将 `Main` 的内容替换为以下代码。  
  
    ```csharp  
    static void Main(string[] args)  
    {  
        CalculateDiscountUsingDesignerWorkflow();  
        //CalculateDiscountUsingCodeWorkflow();  
    }  
    ```  
  
22. 在 `Program` 类中创建一个名为 `CalculateDiscountUsingDesignerWorkflow` 的新方法，此方法包含以下代码。  
  
    ```csharp  
    static void CalculateDiscountUsingDesignerWorkflow()  
    {  
        double SubtotalValue = 125.99;  
        Dictionary<string, object> wfargs = new Dictionary<string, object>  
        {  
            {"Subtotal", SubtotalValue}  
        };  
  
        Activity wf = new DiscountWorkflow();  
  
        IDictionary<string, object> outputs =  
            WorkflowInvoker.Invoke(wf, wfargs);  
  
        Console.WriteLine("Subtotal: {0:C}, Discount {1}%, Total {2:C}",  
            SubtotalValue, (double)outputs["DiscountPercent"] * 100,  
            outputs["Total"]);  
    }  
    ```  
  
23. 按 Ctrl+F5 生成并运行应用程序。 若要指定其他 `Subtotal` 量，请在以下代码中更改 `SubtotalValue` 的值。  
  
    ```csharp  
    double SubtotalValue = 125.99; // Change this value.  
    ```  
  
## <a name="rules-features-overview"></a>规则功能概述  
 [!INCLUDE[wf1](../../../includes/wf1-md.md)] 规则引擎为以基于优先级别的方式处理规则提供支持，并且支持正向链接。 可为单个项或集合中的多个项计算规则。 有关规则的概述以及特定规则功能的信息，请参考下表。  
  
|规则功能|文档|  
|-------------------|-------------------|  
|规则概述|[Windows Workflow Foundation 规则引擎简介](http://go.microsoft.com/fwlink/?LinkID=152836)|  
|RuleSet|[在工作流中使用 Ruleset](http://go.microsoft.com/fwlink/?LinkId=178516) 和 <xref:System.Workflow.Activities.Rules.RuleSet>|  
|规则计算|[Ruleset 中的规则计算](http://go.microsoft.com/fwlink/?LinkId=178517)|  
|规则链接|[正向链接控制](http://go.microsoft.com/fwlink/?LinkId=178518) 和 [规则的正向链接](http://go.microsoft.com/fwlink/?LinkId=178519)|  
|处理规则中的集合|[处理规则中的集合](http://go.microsoft.com/fwlink/?LinkId=178520)|  
|使用 PolicyActivity|[使用 PolicyActivity 活动](http://go.microsoft.com/fwlink/?LinkId=178521) 和 <xref:System.Workflow.Activities.PolicyActivity>|  
  
 创建工作流 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 并使用提供的规则功能的所有 [!INCLUDE[wf1](../../../includes/wf1-md.md)], ，例如声明性活动条件和条件的活动，如 <xref:System.Workflow.Activities.ConditionedActivityGroup> 和 <xref:System.Workflow.Activities.ReplicatorActivity>。 如果需要，此功能可用于使用 [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] 和 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 创建的工作流。 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][迁移指南](../../../docs/framework/windows-workflow-foundation//migration-guidance.md)。