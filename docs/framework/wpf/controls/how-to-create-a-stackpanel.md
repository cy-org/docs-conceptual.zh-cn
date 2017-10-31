---
title: "如何：创建 StackPanel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "StackPanel 控件创建"
ms.assetid: e7ce65cb-720a-4bb6-95b6-286b74488a58
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：创建 StackPanel
此示例演示如何创建<xref:System.Windows.Controls.StackPanel>。  
  
## <a name="example"></a>示例  
 一个<xref:System.Windows.Controls.StackPanel>可以堆叠元素中指定的方向。 通过使用在定义的属性<xref:System.Windows.Controls.StackPanel>，内容可以同时垂直排列，这是默认设置，还是水平排列。  
  
 下面的示例垂直堆栈五个<xref:System.Windows.Controls.TextBlock>控件，每个替换为其他<xref:System.Windows.Controls.Border>和<xref:System.Windows.Controls.Border.Background%2A>，通过使用<xref:System.Windows.Controls.StackPanel>。 没有指定的子元素<xref:System.Windows.FrameworkElement.Width%2A>拉长以填充父窗口; 但是，子元素具有指定<xref:System.Windows.FrameworkElement.Width%2A>，在窗口内居中。  
  
 中的默认堆栈方向<xref:System.Windows.Controls.StackPanel>是垂直的。 向控件中的内容流<xref:System.Windows.Controls.StackPanel>，使用<xref:System.Windows.Controls.StackPanel.Orientation%2A>属性。 你可以通过使用控制水平对齐方式<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>属性。  
  
```xaml  
  
<Page xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" WindowTitle="StackPanel Sample">  
  <StackPanel>  
    <Border Background="SkyBlue" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="12">Stacked Item #1</TextBlock>  
    </Border>  
    <Border Width="400" Background="CadetBlue" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="14">Stacked Item #2</TextBlock>  
    </Border>  
    <Border Background="LightGoldenRodYellow" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="16">Stacked Item #3</TextBlock>  
    </Border>  
    <Border Width="200" Background="PaleGreen" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="18">Stacked Item #4</TextBlock>  
    </Border>  
    <Border Background="White" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="20">Stacked Item #5</TextBlock>  
    </Border>  
  </StackPanel>  
</Page>  
  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Controls.StackPanel>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [操作指南主题](../../../../docs/framework/wpf/controls/stackpanel-how-to-topics.md)