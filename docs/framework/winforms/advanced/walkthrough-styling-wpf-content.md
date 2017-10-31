---
title: "演练：设置 WPF 内容的样式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "互操作性 [WDF]"
  - "样式, WPF 内容"
  - "WPF 设计器, 设置 WPF 内容的样式"
ms.assetid: e574aac7-7ea4-4cdb-8034-bab541f000df
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 演练：设置 WPF 内容的样式
本演练显示了如何将样式应用到 Windows 窗体上承载的 Windows Presentation Foundation \(WPF\) 控件中。  
  
 在本演练中，你将要执行以下任务：  
  
-   创建项目。  
  
-   创建 WPF 控件类型。  
  
-   将样式应用到 WPF 控件。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关详细信息，请参阅 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 系统必备  
 你需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_dev11_long](../../../../includes/vs-dev11-long-md.md)]。  
  
## 创建项目  
 第一步是创建 Windows 窗体项目。  
  
> [!NOTE]
>  承载 WPF 内容时，仅支持 C\# 和 Visual Basic 项目。  
  
#### 创建项目  
  
-   在 Visual Basic 或 Visual C\# 中创建名为 `SelectingWpfContent` 的新 Windows 窗体应用程序项目。  
  
## 创建 WPF 控件类型  
 将 WPF 控件类型添加到项目后，就可在 <xref:System.Windows.Forms.Integration.ElementHost> 控件中托管它。  
  
#### 创建 WPF 控件类型  
  
1.  将新的 WPF <xref:System.Windows.Controls.UserControl> 项目添加到解决方案。  使用控件类型的默认名称，`UserControl1.xaml`。  有关详细信息，请参阅[演练：设计时在 Windows 窗体上创建新的 WPF 内容](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)。  
  
2.  在设计视图中，请确保已选中 `UserControl1`。  有关详细信息，请参阅[如何：在设计图面上选择和移动元素](http://msdn.microsoft.com/zh-cn/54cb70b6-b35b-46e4-a0cc-65189399c474)。  
  
3.  在“属性”窗口中，将 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性的值设置为 `200`。  
  
4.  将 <xref:System.Windows.Controls.Button?displayProperty=fullName> 控件添加到 <xref:System.Windows.Controls.UserControl>，并将 <xref:System.Windows.Controls.ContentControl.Content%2A> 属性的值设置为“Cancel”。  
  
5.  将第二个 <xref:System.Windows.Controls.Button?displayProperty=fullName> 控件添加到 <xref:System.Windows.Controls.UserControl>，并将 <xref:System.Windows.Controls.ContentControl.Content%2A> 属性的值设置为“OK”。  
  
6.  生成项目。  
  
## 将样式应用到 WPF 控件  
 可对 WPF 控件应用不同样式以更改它的外观和行为。  
  
#### 将样式应用到 WPF 控件  
  
1.  在 Windows 窗体设计器中打开 `Form1`。  
  
2.  在“工具箱”中，双击 `UserControl1` 在窗体上创建 `UserControl1` 的实例。  
  
     `UserControl1` 的实例托管在名为 `elementHost1` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。  
  
3.  在 `elementHost1` 的智能标记面板中，单击下拉列表中的“编辑所承载的内容”。  
  
     `UserControl1` 将在 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)] 中打开。  
  
4.  在 XAML 视图中，将以下 XAML 插到 `<UserControl>` 开始标记后面。  
  
     此 XAML 创建具有对比渐变边框的渐变。  单击此控件后，将更改渐变以生成按下按钮的外观。  有关详细信息，请参阅[样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。  
  
```xaml  
<UserControl.Resources>  
    <LinearGradientBrush x:Key="NormalBrush" EndPoint="0,1" StartPoint="0,0">  
        <GradientStop Color="#FFF" Offset="0.0"/>  
        <GradientStop Color="#CCC" Offset="1.0"/>  
    </LinearGradientBrush>  
    <LinearGradientBrush x:Key="PressedBrush" EndPoint="0,1" StartPoint="0,0">  
        <GradientStop Color="#BBB" Offset="0.0"/>  
        <GradientStop Color="#EEE" Offset="0.1"/>  
        <GradientStop Color="#EEE" Offset="0.9"/>  
        <GradientStop Color="#FFF" Offset="1.0"/>  
    </LinearGradientBrush>  
    <LinearGradientBrush x:Key="NormalBorderBrush" EndPoint="0,1" StartPoint="0,0">  
        <GradientStop Color="#CCC" Offset="0.0"/>  
        <GradientStop Color="#444" Offset="1.0"/>  
    </LinearGradientBrush>  
    <LinearGradientBrush x:Key="BorderBrush" EndPoint="0,1" StartPoint="0,0">  
        <GradientStop Color="#CCC" Offset="0.0"/>  
        <GradientStop Color="#444" Offset="1.0"/>  
    </LinearGradientBrush>  
    <LinearGradientBrush x:Key="PressedBorderBrush" EndPoint="0,1" StartPoint="0,0">  
        <GradientStop Color="#444" Offset="0.0"/>  
        <GradientStop Color="#888" Offset="1.0"/>  
    </LinearGradientBrush>  
  
    <Style x:Key="SimpleButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">  
        <Setter Property="Background" Value="{StaticResource NormalBrush}"/>  
        <Setter Property="BorderBrush" Value="{StaticResource NormalBorderBrush}"/>  
        <Setter Property="Template">  
            <Setter.Value>  
                <ControlTemplate TargetType="{x:Type Button}">  
                    <Grid x:Name="Grid">  
                        <Border x:Name="Border" Background="{TemplateBinding Background}" BorderBrush="{TemplateBinding BorderBrush}" BorderThickness="{TemplateBinding BorderThickness}" Padding="{TemplateBinding Padding}"/>  
                        <ContentPresenter HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}" Margin="{TemplateBinding Padding}" VerticalAlignment="{TemplateBinding VerticalContentAlignment}" RecognizesAccessKey="True"/>  
                    </Grid>  
                    <ControlTemplate.Triggers>  
                        <Trigger Property="IsPressed" Value="true">  
                            <Setter Property="Background" Value="{StaticResource PressedBrush}" TargetName="Border"/>  
                            <Setter Property="BorderBrush" Value="{StaticResource PressedBorderBrush}" TargetName="Border"/>  
                        </Trigger>  
                    </ControlTemplate.Triggers>  
                </ControlTemplate>  
            </Setter.Value>  
        </Setter>  
    </Style>  
</UserControl.Resources>  
```  
  
1.  通过插入“取消”按钮的 `<Button>` 标记中的以下 XAML，将上一步中定义的 `SimpleButton` 样式应用到“取消”按钮。  
  
    ```  
    Style="{StaticResource SimpleButton}  
    ```  
  
     按钮声明将类似于以下 XAML。  
  
```xaml  
<Button Height="23" Margin="41,52,98,0" Name="button1" VerticalAlignment="Top"  
                Style="{StaticResource SimpleButton}">Cancel</Button>  
```  
  
1.  生成项目。  
  
2.  在 Windows 窗体设计器中打开 `Form1`。  
  
3.  将新样式应用到按钮控件中。  
  
4.  在“调试”菜单中，选择“启动调试”以运行应用程序。  
  
5.  单击“确定”和“取消”按钮并查看差异。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [迁移和互操作性](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [使用 WPF 控件](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)