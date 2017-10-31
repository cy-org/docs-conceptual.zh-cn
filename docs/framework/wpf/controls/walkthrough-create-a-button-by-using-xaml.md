---
title: "演练：使用 XAML 创建按钮 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "按钮"
ms.assetid: 138c41c4-1759-4bbf-8d77-77031a06a8a0
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 演练：使用 XAML 创建按钮
本演练的目的在于介绍如何创建要在 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 应用程序中使用的动画按钮。  本演练使用样式和模板来创建自定义的按钮资源，通过该按钮资源可以重用代码并将按钮逻辑与按钮声明分开。  本演练完全是用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 编写的。  
  
> [!IMPORTANT]
>  本演练指导您通过在 Microsoft [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 中键入或复制和粘贴[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 来逐步创建应用程序。  如果您想了解如何使用设计工具 \(Microsoft Expression Blend\) 来创建同样的应用程序，请参见[使用 Microsoft Expression Blend 创建按钮](../../../../docs/framework/wpf/controls/walkthrough-create-a-button-by-using-microsoft-expression-blend.md)。  
  
 下图显示的是已完成的按钮。  
  
 ![使用 XAML 创建的自定义按钮](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-5.png "custom\_button\_AnimatedButton\_5")  
  
## 创建基本按钮  
 让我们首先从创建一个新项目并向窗口中添加几个按钮开始。  
  
#### 创建新的 WPF 项目并向窗口中添加按钮  
  
1.  启动 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]。  
  
2.  **创建新的 WPF 项目：**在**“文件”**菜单上，指向**“新建”**，再单击**“项目”**。  找到**“Windows 应用程序\(WPF\)”**模板并将项目命名为“AnimatedButton”。  这将创建应用程序的主干。  
  
3.  **添加基本的默认按钮：**本演练中所需的全部文件均由该模板提供。  通过在解决方案资源管理器中双击 Window1.xaml 文件来打开它。  默认情况下，Window1.xaml 中存在一个 <xref:System.Windows.Controls.Grid> 元素。  移除 <xref:System.Windows.Controls.Grid> 元素，并通过向 Window1.xaml 中键入或复制和粘贴以下突出显示的代码来向[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 页面中添加几个按钮：  
  
    ```  
    <Window x:Class="AnimatedButton.Window1"  
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
      Title="AnimatedButton" Height="300" Width="300"   
      Background="Black">  
  
      <!-- Buttons arranged vertically inside a StackPanel. -->  
      <StackPanel HorizontalAlignment="Left">  
        <Button>Button 1</Button>  
        <Button>Button 2</Button>  
        <Button>Button 3</Button>  
      </StackPanel>  
  
    </Window>  
    ```  
  
     按 F5 运行该应用程序；您应当能够看到类似下图的一组按钮。  
  
     ![三个基本按钮](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-1.png "custom\_button\_AnimatedButton\_1")  
  
     现在您已经创建了基本按钮，这样就完成了在 Window1.xaml 文件中的工作。  本演练其余部分重点介绍如何在 app.xaml 文件中为这些按钮定义样式和模板。  
  
## 设置基本属性  
 接着，我们将会为这些按钮设置一些属性，以便控制按钮外观和布局。  您将使用资源来为整个应用程序定义按钮属性，而不是为这些按钮单独设置属性。  在概念上，应用程序资源与网页的外部[!INCLUDE[TLA#tla_css](../../../../includes/tlasharptla-css-md.md)] 相似；但是，资源远比[!INCLUDE[TLA#tla_css](../../../../includes/tlasharptla-css-md.md)] 强大，在本演练结束时您将明白这一点。  若要进一步了解资源，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
#### 使用样式为按钮设置基本属性  
  
1.  **定义 Application.Resources 块：**打开 app.xaml 并添加下面突出显示的标记（如果尚未添加）：  
  
    ```  
    <Application x:Class="AnimatedButton.App"  
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
      StartupUri="Window1.xaml"  
      >  
      <Application.Resources>  
  
        <!-- Resources for the entire application can be   
             defined here. -->  
  
      </Application.Resources>  
    </Application>  
    ```  
  
     资源范围由资源的定义位置来确定。  如果资源是在 app.xaml 文件的 `Application.Resoureses` 中定义的，则将允许从应用程序中的任何位置使用资源。  若要了解有关定义资源范围的更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
2.  **创建一个样式并用该样式定义基本属性值：**向 `Application.Resources` 块添加下面的标记。  此标记创建一个应用于该应用程序中所有按钮的 <xref:System.Windows.Style>，并将这些按钮的 <xref:System.Windows.FrameworkElement.Width%2A> 设置为 90，将 <xref:System.Windows.FrameworkElement.Margin%2A> 设置为 10：  
  
    ```  
    <Application.Resources>  
  
      <Style TargetType="Button">  
        <Setter Property="Width" Value="90" />  
        <Setter Property="Margin" Value="10" />  
      </Style>  
  
    </Application.Resources>  
    ```  
  
     <xref:System.Windows.Style.TargetType%2A> 属性指定将该样式应用于 <xref:System.Windows.Controls.Button> 类型的所有对象。  每个 <xref:System.Windows.Setter> 都为 <xref:System.Windows.Style> 设置不同的属性值。  因此，此时应用程序中的每个按钮的宽度都为 90，边距都为 10。  如果您按 F5 运行应用程序，则会看到下面的窗口。  
  
     ![宽度为 90、边距为 10 的按钮](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-2.png "custom\_button\_AnimatedButton\_2")  
  
     您还可以对样式进行更多的处理，这包括以各种方式微调对象的目标、指定复杂的属性值，甚至将样式作为其他样式的输入。  有关更多信息，请参见[样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。  
  
3.  **为资源设置样式属性值：**使用资源，可以通过一种简单的方式来重用通常定义的对象和值。  为了使代码更加模块化，使用资源定义复杂值尤其有用。  向 app.xaml 添加下面突出显示的标记。  
  
    ```  
    <Application.Resources>  
  
      <LinearGradientBrush x:Key="GrayBlueGradientBrush"   
        StartPoint="0,0" EndPoint="1,1">  
        <GradientStop Color="DarkGray" Offset="0" />  
        <GradientStop Color="#CCCCFF" Offset="0.5" />  
        <GradientStop Color="DarkGray" Offset="1" />  
      </LinearGradientBrush>  
  
      <Style TargetType="{x:Type Button}">  
        <Setter Property="Background"   
          Value="{StaticResource GrayBlueGradientBrush}" />  
        <Setter Property="Width" Value="80" />  
        <Setter Property="Margin" Value="10" />  
      </Style>  
  
    </Application.Resources>  
    ```  
  
     您已经在 `Application.Resources` 块的正下方创建了一个名为“GrayBlueGradientBrush”的资源。  此资源将定义一个水平渐变。  此资源可以在该应用程序中的任何位置（包括在 <xref:System.Windows.Controls.Control.Background%2A> 属性的按钮样式 setter 内部中）用作属性值。  现在，所有的按钮都具有此渐变的 <xref:System.Windows.Controls.Control.Background%2A> 属性值。  
  
     按 F5 运行该应用程序。  其外观类似于下图：  
  
     ![具有渐变背景的按钮](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-3.png "custom\_button\_AnimatedButton\_3")  
  
## 创建一个定义按钮外观的模板  
 在本节中，将创建一个用来自定义按钮外观（表示）的模板。  按钮表示是由几个赋予按钮独特外观的对象（包括矩形和其他组件）组成的。  
  
 到目前为止，对应用程序中按钮外观的控制已限制为更改按钮的属性。  如果您希望更彻底地改变按钮的外观，该怎么办？  使用模板可以强有力地控制对象的表示。  由于模板可以在样式中使用，因此您可以将模板应用于所有应用了样式的对象（在本演练中为按钮）。  
  
#### 使用模板定义按钮的外观  
  
1.  **设置模板：**由于控件（如 <xref:System.Windows.Controls.Button>）具有 <xref:System.Windows.Controls.Control.Template%2A> 属性，因此您可以像对 <xref:System.Windows.Style> 中所设置的其他属性值那样，使用 <xref:System.Windows.Setter> 来定义模板属性值。  向按钮样式中添加下面突出显示的标记。  
  
    ```  
    <Application.Resources>  
  
      <LinearGradientBrush x:Key="GrayBlueGradientBrush"   
        StartPoint="0,0" EndPoint="1,1">  
        <GradientStop Color="DarkGray" Offset="0" />  
        <GradientStop Color="#CCCCFF" Offset="0.5" />  
        <GradientStop Color="DarkGray" Offset="1" />  
      </LinearGradientBrush>  
  
      <Style TargetType="{x:Type Button}">  
      <Setter Property="Background" Value="{StaticResource GrayBlueGradientBrush}" />  
        <Setter Property="Width" Value="80" />  
        <Setter Property="Margin" Value="10" />  
        <Setter Property="Template">  
          <Setter.Value>  
            <!-- The button template is defined here. -->  
          </Setter.Value>  
        </Setter>  
      </Style>  
  
    </Application.Resources>  
    ```  
  
2.  **更改按钮表示：**此时，您需要定义模板。  添加下面突出显示的标记。  此标记指定了两个后跟 <xref:System.Windows.Controls.DockPanel> 且具有圆角的 <xref:System.Windows.Shapes.Rectangle> 元素。  <xref:System.Windows.Controls.DockPanel> 用于承载按钮的 <xref:System.Windows.Controls.ContentPresenter>。  A <xref:System.Windows.Controls.ContentPresenter> 显示按钮的内容。  本演练中，内容为文本 \("Button 1", "Button 2", "Button 3"\)。  所有模板组件（矩形和 <xref:System.Windows.Controls.DockPanel>）都放置在一个 <xref:System.Windows.Controls.Grid> 内。  
  
    ```  
    <Setter.Value>  
      <ControlTemplate TargetType="Button">  
        <Grid Width="{TemplateBinding Width}"   
         Height="{TemplateBinding Height}" ClipToBounds="True">  
  
          <!-- Outer Rectangle with rounded corners. -->  
          <Rectangle x:Name="outerRectangle"   
            HorizontalAlignment="Stretch"   
            VerticalAlignment="Stretch"   
            Stroke="{TemplateBinding Background}"   
            RadiusX="20" RadiusY="20" StrokeThickness="5"   
            Fill="Transparent" />  
  
          <!-- Inner Rectangle with rounded corners. -->  
          <Rectangle x:Name="innerRectangle"   
            HorizontalAlignment="Stretch"   
            VerticalAlignment="Stretch" Stroke="Transparent"   
            StrokeThickness="20"   
            Fill="{TemplateBinding Background}"   
            RadiusX="20" RadiusY="20"   />  
  
          <!-- Present Content (text) of the button. -->  
          <DockPanel Name="myContentPresenterDockPanel">  
            <ContentPresenter x:Name="myContentPresenter" Margin="20"   
              Content="{TemplateBinding  Content}"   
              TextBlock.Foreground="Black" />  
          </DockPanel>  
        </Grid>  
      </ControlTemplate>  
    </Setter.Value>  
    ```  
  
     按 F5 运行该应用程序。  其外观类似于下图：  
  
     ![](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-4.gif "custom\_button\_AnimatedButton\_4")  
  
3.  **向模板中添加玻璃效果：**接着将添加玻璃效果。  首先创建一些用来生成玻璃渐变效果的资源。  将这些渐变资源添加到 `Application.Resources` 块中的任何位置：  
  
    ```  
    <Application.Resources>  
      <GradientStopCollection x:Key="MyGlassGradientStopsResource">  
        <GradientStop Color="WhiteSmoke" Offset="0.2" />  
        <GradientStop Color="Transparent" Offset="0.4" />  
        <GradientStop Color="WhiteSmoke" Offset="0.5" />  
        <GradientStop Color="Transparent" Offset="0.75" />  
        <GradientStop Color="WhiteSmoke" Offset="0.9" />  
        <GradientStop Color="Transparent" Offset="1" />  
      </GradientStopCollection>  
  
      <LinearGradientBrush x:Key="MyGlassBrushResource"   
       StartPoint="0,0" EndPoint="1,1" Opacity="0.75"   
       GradientStops="{StaticResource MyGlassGradientStopsResource}" />  
    <!-- Styles and other resources below here. -->  
    ```  
  
     这些资源将用作按钮模板的 <xref:System.Windows.Controls.Grid> 中所插入的矩形的 <xref:System.Windows.Shapes.Shape.Fill%2A>。  向模板添加下面突出显示的标记。  
  
    ```  
    <Setter.Value>  
      <ControlTemplate TargetType="{x:Type Button}">  
        <Grid Width="{TemplateBinding Width}" Height="{TemplateBinding Height}"  
    ClipToBounds="True">  
  
        <!-- Outer Rectangle with rounded corners. -->  
        <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"   
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"   
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />  
  
        <!-- Inner Rectangle with rounded corners. -->  
        <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"   
          VerticalAlignment="Stretch" Stroke="Transparent" StrokeThickness="20"   
          Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20" />  
  
        <!-- Glass Rectangle -->  
        <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"  
          VerticalAlignment="Stretch"  
          StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"  
          Fill="{StaticResource MyGlassBrushResource}"  
          RenderTransformOrigin="0.5,0.5">  
          <Rectangle.Stroke>  
            <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">  
              <LinearGradientBrush.GradientStops>  
                <GradientStop Offset="0.0" Color="LightBlue" />  
                <GradientStop Offset="1.0" Color="Gray" />  
              </LinearGradientBrush.GradientStops>  
            </LinearGradientBrush>  
          </Rectangle.Stroke>  
  
          <!-- These transforms have no effect as they are declared here.   
               The reason the transforms are included is to be targets   
               for animation (see later). -->  
          <Rectangle.RenderTransform>  
            <TransformGroup>  
              <ScaleTransform />  
              <RotateTransform />  
            </TransformGroup>  
          </Rectangle.RenderTransform>  
  
          <!-- A BevelBitmapEffect is applied to give the button a   
               "Beveled" look. -->  
          <Rectangle.BitmapEffect>  
            <BevelBitmapEffect />  
          </Rectangle.BitmapEffect>  
        </Rectangle>  
  
        <!-- Present Text of the button. -->  
        <DockPanel Name="myContentPresenterDockPanel">  
          <ContentPresenter x:Name="myContentPresenter" Margin="20"   
            Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />  
        </DockPanel>  
      </Grid>  
    </ControlTemplate>  
    </Setter.Value>  
    ```  
  
     请注意，`x:Name` 属性为“glassCube”的矩形的 <xref:System.Windows.UIElement.Opacity%2A> 为 0，因此，当您运行该示例时，将看到上面并没有覆盖玻璃矩形。  这是由于我们将在以后向该模板中添加用户与该按钮交互时将触发的触发器。  但是，您可以通过将 <xref:System.Windows.UIElement.Opacity%2A> 值更改为 1 并运行该应用程序来查看按钮现在的外观。  请参见下图。  在转至下一步之前，请将 <xref:System.Windows.UIElement.Opacity%2A> 更改回 0。  
  
     ![使用 XAML 创建的自定义按钮](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-5.png "custom\_button\_AnimatedButton\_5")  
  
## 创建按钮交互性  
 在本节中，将创建属性触发器和事件触发器来更改属性值和运行动画，以响应用户操作（如将鼠标指针移到按钮上并单击）。  
  
 添加交互性（鼠标悬停、鼠标离开和单击等）的一个简便方法就是在模板或样式内部定义触发器。  若要创建 <xref:System.Windows.Trigger>，需要定义一个属性“条件”，例如：按钮的 <xref:System.Windows.UIElement.IsMouseOver%2A> 属性值等于 `true`。  随后将定义在触发条件为 true 时所发生的 setter（操作）。  
  
#### 创建按钮交互性  
  
1.  **添加模板触发器：**向模板添加突出显示的标记。  
  
    ```  
    <Setter.Value>  
      <ControlTemplate TargetType="{x:Type Button}">  
        <Grid Width="{TemplateBinding Width}"   
          Height="{TemplateBinding Height}" ClipToBounds="True">  
  
          <!-- Outer Rectangle with rounded corners. -->  
          <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"   
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"   
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />  
  
          <!-- Inner Rectangle with rounded corners. -->  
          <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"   
            VerticalAlignment="Stretch" Stroke="Transparent"   
            StrokeThickness="20"   
            Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20"   
          />  
  
          <!-- Glass Rectangle -->  
          <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"  
            VerticalAlignment="Stretch"  
            StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"  
            Fill="{StaticResource MyGlassBrushResource}"  
            RenderTransformOrigin="0.5,0.5">  
            <Rectangle.Stroke>  
              <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">  
                <LinearGradientBrush.GradientStops>  
                  <GradientStop Offset="0.0" Color="LightBlue" />  
                  <GradientStop Offset="1.0" Color="Gray" />  
                </LinearGradientBrush.GradientStops>  
              </LinearGradientBrush>  
            </Rectangle.Stroke>  
  
            <!-- These transforms have no effect as they   
                 are declared here.   
                 The reason the transforms are included is to be targets   
                 for animation (see later). -->  
            <Rectangle.RenderTransform>  
              <TransformGroup>  
                <ScaleTransform />  
                <RotateTransform />  
              </TransformGroup>  
            </Rectangle.RenderTransform>  
  
              <!-- A BevelBitmapEffect is applied to give the button a   
                   "Beveled" look. -->  
            <Rectangle.BitmapEffect>  
              <BevelBitmapEffect />  
            </Rectangle.BitmapEffect>  
          </Rectangle>  
  
          <!-- Present Text of the button. -->  
          <DockPanel Name="myContentPresenterDockPanel">  
            <ContentPresenter x:Name="myContentPresenter" Margin="20"   
              Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />  
          </DockPanel>  
        </Grid>  
  
        <ControlTemplate.Triggers>  
          <!-- Set action triggers for the buttons and define  
               what the button does in response to those triggers. -->  
        </ControlTemplate.Triggers>  
      </ControlTemplate>  
    </Setter.Value>  
    ```  
  
2.  **添加属性触发器：**向 `ControlTemplate.Triggers` 块添加突出显示的标记：  
  
    ```  
    <ControlTemplate.Triggers>  
  
      <!-- Set properties when mouse pointer is over the button. -->  
      <Trigger Property="IsMouseOver" Value="True">  
  
        <!-- Below are three property settings that occur when the   
             condition is met (user mouses over button).  -->  
        <!-- Change the color of the outer rectangle when user   
             mouses over it. -->  
        <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"  
          Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />  
  
        <!-- Sets the glass opacity to 1, therefore, the   
             glass "appears" when user mouses over it. -->  
        <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />  
  
        <!-- Makes the text slightly blurry as though you   
             were looking at it through blurry glass. -->  
        <Setter Property="ContentPresenter.BitmapEffect"   
          TargetName="myContentPresenter">  
          <Setter.Value>  
            <BlurBitmapEffect Radius="1" />  
          </Setter.Value>  
        </Setter>  
      </Trigger>  
  
    <ControlTemplate.Triggers/>  
    ```  
  
     按 F5 运行应用程序，并查看在将鼠标指针移到按钮上时的效果。  
  
3.  **添加焦点触发器：**接着，将添加一些类似的 setter 来处理当按钮具有焦点时（例如，当用户单击按钮之后）的情况。  
  
    ```  
    <ControlTemplate.Triggers>  
  
      <!-- Set properties when mouse pointer is over the button. -->  
      <Trigger Property="IsMouseOver" Value="True">  
  
        <!-- Below are three property settings that occur when the   
             condition is met (user mouses over button).  -->  
        <!-- Change the color of the outer rectangle when user          mouses over it. -->  
        <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"  
          Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />  
  
        <!-- Sets the glass opacity to 1, therefore, the          glass "appears" when user mouses over it. -->  
        <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />  
  
        <!-- Makes the text slightly blurry as though you were          looking at it through blurry glass. -->  
        <Setter Property="ContentPresenter.BitmapEffect"       TargetName="myContentPresenter">  
          <Setter.Value>  
            <BlurBitmapEffect Radius="1" />  
          </Setter.Value>  
        </Setter>  
      </Trigger>  
      <!-- Set properties when button has focus. -->  
      <Trigger Property="IsFocused" Value="true">  
        <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />  
        <Setter Property="Rectangle.Stroke" TargetName="outerRectangle"  
          Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />  
        <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />  
      </Trigger>  
  
    </ControlTemplate.Triggers>  
    ```  
  
     按 F5 运行应用程序，并单击其中的某个按钮。  请注意，在单击该按钮之后，该按钮仍具有焦点，因此它仍将保持突出显示状态。  如果您单击另一个按钮，则新按钮将获得焦点，而上一个按钮则失去焦点。  
  
4.  **为**  <xref:System.Windows.UIElement.MouseEnter>  **和**  <xref:System.Windows.UIElement.MouseLeave>  **添加动画：**接下来我们将向触发器添加一些动画。  在 `ControlTemplate.Triggers` 块内部的任意位置添加下面的标记。  
  
    ```  
  
                    <!-- Animations that start when mouse enters and leaves button. -->  
    <EventTrigger RoutedEvent="Mouse.MouseEnter">  
      <EventTrigger.Actions>  
        <BeginStoryboard Name="mouseEnterBeginStoryboard">  
          <Storyboard>  
  
          <!-- This animation makes the glass rectangle shrink in the X direction. -->  
            <DoubleAnimation Storyboard.TargetName="glassCube"   
              Storyboard.TargetProperty=  
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleX)"  
              By="-0.1" Duration="0:0:0.5" />  
  
            <!-- This animation makes the glass rectangle shrink in the Y direction. -->  
            <DoubleAnimation  
            Storyboard.TargetName="glassCube"   
              Storyboard.TargetProperty=  
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleY)"   
              By="-0.1" Duration="0:0:0.5" />  
          </Storyboard>  
        </BeginStoryboard>  
      </EventTrigger.Actions>  
    </EventTrigger>  
    <EventTrigger RoutedEvent="Mouse.MouseLeave">  
      <EventTrigger.Actions>  
  
        <!-- Stopping the storyboard sets all animated properties back to default. -->  
        <StopStoryboard BeginStoryboardName="mouseEnterBeginStoryboard" />  
      </EventTrigger.Actions>  
    </EventTrigger>  
    ```  
  
     当鼠标指针移到该按钮上时，玻璃矩形会收缩；当指针离开该按钮时，镜面矩形会返回到其正常大小。  
  
     当指针移到该按钮上（引发 <xref:System.Windows.UIElement.MouseEnter> 事件）时会触发两个动画。  这些动画会使玻璃矩形沿着 X 轴和 Y 轴收缩。  请注意 <xref:System.Windows.Media.Animation.DoubleAnimation> 元素的属性：<xref:System.Windows.Media.Animation.Timeline.Duration%2A> 和 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>。  <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 指定动画持续半秒多，<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 指定玻璃收缩 10%。  
  
     第二个事件触发器 \(<xref:System.Windows.UIElement.MouseLeave>\) 只是停止第一个触发器。  当您停止某个 <xref:System.Windows.Media.Animation.Storyboard> 时，所有的动画属性都恢复到其默认值。  因此，当用户将指针移开按钮时，该按钮将返回到鼠标指针移到其上之前的状态。  有关动画的更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
5.  **添加单击按钮时的动画效果：**最后一步是添加在用户单击按钮时将触发的触发器。  在 `ControlTemplate.Triggers` 块内部的任意位置添加下面的标记：  
  
    ```  
  
                    <!-- Animation fires when button is clicked, causing glass to spin.  -->  
    <EventTrigger RoutedEvent="Button.Click">  
      <EventTrigger.Actions>  
        <BeginStoryboard>  
          <Storyboard>  
            <DoubleAnimation Storyboard.TargetName="glassCube"   
              Storyboard.TargetProperty=  
              "(Rectangle.RenderTransform).(TransformGroup.Children)[1].(RotateTransform.Angle)"   
              By="360" Duration="0:0:0.5" />  
          </Storyboard>  
        </BeginStoryboard>  
      </EventTrigger.Actions>  
    </EventTrigger>  
    ```  
  
     按 F5 运行应用程序，并单击其中的某个按钮。  当您单击某个按钮时，玻璃矩形会旋转。  
  
## 摘要  
 在本演练中，进行了下列练习：  
  
-   使 <xref:System.Windows.Style> 面向对象类型 \(<xref:System.Windows.Controls.Button>\)。  
  
-   使用 <xref:System.Windows.Style> 控制整个应用程序中按钮的基本属性。  
  
-   创建要用于 <xref:System.Windows.Style> setter 的属性值的资源（如渐变）。  
  
-   通过向按钮应用模板来自定义整个应用程序中按钮的外观。  
  
-   自定义按钮的行为（包括动画效果）来响应用户操作（如 <xref:System.Windows.UIElement.MouseEnter>、<xref:System.Windows.UIElement.MouseLeave> 和 <xref:System.Windows.Controls.Primitives.ButtonBase.Click>）。  
  
## 请参阅  
 [使用 Microsoft Expression Blend 创建按钮](../../../../docs/framework/wpf/controls/walkthrough-create-a-button-by-using-microsoft-expression-blend.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [位图效果概述](../../../../docs/framework/wpf/graphics-multimedia/bitmap-effects-overview.md)