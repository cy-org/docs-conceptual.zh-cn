---
title: "任务 2：承载工作流设计器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a29b138-270d-4846-b78e-2b875e34e501
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# 任务 2：承载工作流设计器
本主题描述在 [!INCLUDE[avalon1](../../../includes/avalon1-md.md)] 应用程序中承载 [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] 的实例的过程。  
  
 在此过程中将执行以下操作：配置包含设计器的 **Grid** 控件，以编程方式创建包含默认 <xref:System.Activities.Statements.Sequence> 活动的 <xref:System.Activities.Presentation.WorkflowDesigner>，注册设计器元数据以提供针对所有内置活动的设计器支持，以及在 [!INCLUDE[avalon2](../../../includes/avalon2-md.md)] 应用程序中承载 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)]。  
  
### 承载工作流设计器  
  
1.  打开在[任务 1：创建一个新的 Windows Presentation Foundation 应用程序](../../../docs/framework/windows-workflow-foundation//task-1-create-a-new-wpf-app.md)中创建的 HostingApplication 项目。  
  
2.  调整窗口的大小，以便更轻松地使用 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)]。为此，请在设计器中选择**“MainWindow”**，按 F4 以显示**“属性”**窗口，然后在**“布局”**部分中，将**“宽度”**设置为值 600，并将**“高度”**设置为值 350。  
  
3.  通过以下方式设置网格名称：在设计器中选择 **Grid** 面板（单击**“MainWindow”**中的框），并将**“属性”**窗口顶部的 **Name** 属性设置为“grid1”。  
  
4.  在**“属性”**窗口中，单击 `ColumnDefinitions` 属性旁边的省略号（**“…”**），打开**“集合编辑器”**对话框。  
  
5.  在**“集合编辑器”**对话框中，单击**“添加”**按钮三次以在布局中插入三个列。第一列中包含**“工具箱”**，第二列将承载 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)]，第三列则供属性检查器使用。  
  
6.  将中间列的 `Width` 属性值设置为“4\*”。  
  
7.  单击**“确定”**保存更改。以下 XAML 将添加到 MainWindow.xaml 文件中：  
  
    ```  
  
    <Grid Name="grid1">  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition />  
            <ColumnDefinition Width="4*" />  
            <ColumnDefinition />  
        </Grid.ColumnDefinitions>  
    </Grid>  
  
    ```  
  
8.  在**“解决方案资源管理器”**中，右击 MainWindow.xaml 并选择**“查看代码”**。按照以下这些步骤修改代码：  
  
    1.  添加下列命名空间：  
  
        ```csharp  
  
        using System.Activities;  
        using System.Activities.Core.Presentation;  
        using System.Activities.Presentation;  
        using System.Activities.Presentation.Metadata;  
        using System.Activities.Presentation.Toolbox;  
        using System.Activities.Statements;  
        using System.ComponentModel;  
  
        ```  
  
    2.  若要声明某个私有成员字段包含 <xref:System.Activities.Presentation.WorkflowDesigner> 的实例，请将下面的代码添加到 `MainWindow` 类。  
  
        ```csharp  
  
        public partial class MainWindow : Window  
        {  
            private WorkflowDesigner wd;  
  
            public MainWindow()  
            {  
                InitializeComponent();  
            }  
        }  
  
        ```  
  
    3.  将下面的 `AddDesigner` 方法添加到 `MainWindow` 类。在实现中，将创建 <xref:System.Activities.Presentation.WorkflowDesigner> 的实例，将 <xref:System.Activities.Statements.Sequence> 活动添加到其中，并将该实例置于 grid1**“网格”**的中间列中。  
  
        ```csharp  
  
        private void AddDesigner()  
        {  
            //Create an instance of WorkflowDesigner class.  
            this.wd = new WorkflowDesigner();  
  
            //Place the designer canvas in the middle column of the grid.  
            Grid.SetColumn(this.wd.View, 1);  
  
            //Load a new Sequence as default.  
            this.wd.Load(new Sequence());  
  
            //Add the designer canvas to the grid.  
            grid1.Children.Add(this.wd.View);  
        }  
  
        ```  
  
    4.  注册设计器元数据，为所有内置活动添加设计器支持。通过此方法可以将活动从工具箱拖放到 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] 中的原始 <xref:System.Activities.Statements.Sequence> 活动上。为此，请将 `RegisterMetadata` 方法添加到 `MainWindow` 类中。  
  
        ```csharp  
  
        private void RegisterMetadata()  
        {               
            DesignerMetadata dm = new DesignerMetadata();  
            dm.Register();  
        }  
  
        ```  
  
         [!INCLUDE[crabout](../../../includes/crabout-md.md)]注册活动设计器的更多信息，请参见[如何：创建自定义活动设计器](../../../docs/framework/windows-workflow-foundation//how-to-create-a-custom-activity-designer.md)。  
  
    5.  在 `MainWindow` 类构造函数中，添加对上文声明的方法的调用，以便注册设计器支持元数据，并创建 <xref:System.Activities.Presentation.WorkflowDesigner>。  
  
        ```csharp  
        public MainWindow()  
        {  
            InitializeComponent();  
  
            // Register the metadata  
            RegisterMetadata();  
  
            // Add the WFF Designer  
            AddDesigner();  
        }  
  
        ```  
  
        > [!NOTE]
        >  `RegisterMetadata` 方法注册包含 <xref:System.Activities.Statements.Sequence> 活动的内置活动的设计器元数据。由于 `AddDesigner` 方法使用 <xref:System.Activities.Statements.Sequence> 活动，因此必须先调用 `RegisterMetadata` 方法。  
  
9. 按 F5 生成并运行解决方案。  
  
10. 若要了解如何向重新承载的工作流设计器添加**“工具箱”**和**“PropertyGrid”**支持，请参见[任务 3：创建工具箱窗格和属性网格窗格](../../../docs/framework/windows-workflow-foundation//task-3-create-the-toolbox-and-propertygrid-panes.md)。  
  
## 请参阅  
 [重新承载工作流设计器](../../../docs/framework/windows-workflow-foundation//rehosting-the-workflow-designer.md)   
 [任务 1：创建一个新的 Windows Presentation Foundation 应用程序](../../../docs/framework/windows-workflow-foundation//task-1-create-a-new-wpf-app.md)   
 [任务 3：创建工具箱窗格和属性网格窗格](../../../docs/framework/windows-workflow-foundation//task-3-create-the-toolbox-and-propertygrid-panes.md)