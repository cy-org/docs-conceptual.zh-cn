---
title: "演练：在 WPF 中承载 Direct3D9 内容 | Microsoft Docs"
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
  - "Direct3D9 [WPF 互操作性], 承载 Direct3D9 内容"
  - "WPF, 承载 Direct3D9 内容"
ms.assetid: 60983736-0ab5-42cc-8b16-e9fbde261a43
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 演练：在 WPF 中承载 Direct3D9 内容
本演练演示如何在 Windows Presentation Foundation \(WPF\) 应用程序中承载 Direct3D9 内容。  
  
 在本演练中，您将执行下列任务：  
  
-   创建 WPF 项目以承载 Direct3D9 内容。  
  
-   导入 Direct3D9 内容。  
  
-   使用 <xref:System.Windows.Interop.D3DImage> 类显示 Direct3D9 内容。  
  
 完成后，您将了解如何在 WPF 应用程序中承载 Direct3D9 内容。  
  
## 系统必备  
 您需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
-   DirectX SDK 9 或更高版本。  
  
-   包含 WPF 兼容格式的 Direct3D9 内容的 DLL。  有关更多信息，请参见[WPF 和 Direct3D9 互操作](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md)和[演练：创建在 WPF 中承载的 Direct3D9 内容](../../../../docs/framework/wpf/advanced/walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)。  
  
## 创建 WPF 项目  
 第一步是创建 WPF 应用程序的项目。  
  
#### 创建 WPF 项目  
  
-   使用 Visual C\# 新建一个名为 `D3DHost` 的 WPF 应用程序项目。  有关更多信息，请参见[如何：创建新的 WPF 应用程序项目](http://msdn.microsoft.com/zh-cn/1f6aea7a-33e1-4d3f-8555-1daa42e95d82)。  
  
     MainWindow.xaml 将在 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]中打开。  
  
## 导入 Direct3D9 内容  
 可以使用 `DllImport` 特性从非托管 DLL 中导入 Direct3D9 内容。  
  
#### 导入 Direct3D9 内容  
  
1.  在代码编辑器中打开 MainWindow.xaml.cs。  
  
2.  用下面的代码替换自动生成的代码。  
  
     [!code-csharp[System.Windows.Interop.D3DImage#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml.cs#1)]  
  
## 承载 Direct3D9 内容  
 最后，使用 <xref:System.Windows.Interop.D3DImage> 类承载 Direct3D9 内容。  
  
#### 承载 Direct3D9 内容  
  
1.  在 MainWindow.xaml 中，用以下 XAML 替换自动生成的 XAML。  
  
     [!code-xml[System.Windows.Interop.D3DImage#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml#10)]  
  
2.  生成项目。  
  
3.  将包含 Direct3D9 内容的 DLL 复制到 bin\/Debug 文件夹。  
  
4.  按 F5 运行项目。  
  
     Direct3D9 内容显示在 WPF 应用程序中。  
  
## 请参阅  
 <xref:System.Windows.Interop.D3DImage>   
 [Direct3D9 和 WPF 互操作性的性能注意事项](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md)