---
title: "演练：创建在 WPF 中承载的 Direct3D9 内容 | Microsoft Docs"
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
  - "Direct3D9 [WPF 互操作性], 创建 Direct3D9 内容"
  - "WPF, 创建 Direct3D9 内容"
ms.assetid: 286e98bc-1eaa-4b5e-923d-3490a9cca5fc
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 演练：创建在 WPF 中承载的 Direct3D9 内容
本演练演示如何创建适合在 Windows Presentation Foundation \(WPF\) 应用程序中承载的 Direct3D9 内容。  有关在 WPF 应用程序中承载 Direct3D9 内容的更多信息，请参见[WPF 和 Direct3D9 互操作](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md)。  
  
 在本演练中，您将执行下列任务：  
  
-   创建 Direct3D9 项目。  
  
-   配置在 WPF 应用程序中承载的 Direct3D9 项目。  
  
 完成后，您将获得一个 DLL，其中包含要在 WPF 应用程序中使用的 Direct3D9 内容。  
  
## 系统必备  
 您需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
-   DirectX SDK 9 或更高版本。  
  
## 创建 Direct3D9 项目  
 第一步是创建和配置 Direct3D9 项目。  
  
#### 创建 Direct3D9 项目  
  
1.  使用 C\+\+ 创建一个名为 `D3DContent` 的新 Win32 项目。  
  
     Win32 应用程序向导打开并显示欢迎屏幕。  
  
2.  单击**“下一步”**。  
  
     将显示“应用程序设置”屏幕。  
  
3.  在**“应用程序类型:”**部分，选择**“DLL”**选项。  
  
4.  单击**“完成”**。  
  
     生成 D3DContent 项目。  
  
5.  在解决方案资源管理器中，右击 D3DContent 项目，然后选择**“属性”**。  
  
     **“D3DContent 属性页”**对话框即打开。  
  
6.  选择**“C\/C\+\+”**节点。  
  
7.  在**“附加包含目录”**字段中，指定 DirectX 包含文件夹的位置。  此文件夹的默认位置为 %ProgramFiles%\\Microsoft DirectX SDK \(*版本*\)\\Include。  
  
8.  双击**“链接器”**节点将它展开。  
  
9. 在**“附加库目录”**字段中，指定 DirectX 库文件夹的位置。  此文件夹的默认位置为 %ProgramFiles%\\Microsoft DirectX SDK \(*版本*\)\\Lib\\x86。  
  
10. 选择**“输入”**节点。  
  
11. 在**“附加依赖项”**字段中，添加 `d3d9.lib` 和 `d3dx9.lib` 文件。  
  
12. 在解决方案资源管理器中，将名为 `D3DContent.def` 的新模块定义文件 \(.def\) 添加到项目中。  
  
## 创建 Direct3D9 内容  
 若要达到最佳性能，Direct3D9 内容必须使用特定的设置。  下面的代码演示如何创建具有最佳性能特征的 Direct3D9 图面。  有关更多信息，请参见 [Direct3D9 和 WPF 互操作性的性能注意事项](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md)。  
  
#### 创建 Direct3D9 内容  
  
1.  使用解决方案资源管理器，将三个 C\+\+ 类添加到以下名称的项目中。  
  
     `CRenderer`（具有虚析构函数）  
  
     `CRendererManager`  
  
     `CTriangleRenderer`  
  
2.  在代码编辑器中打开 Renderer.h，用下面的代码替换自动生成的代码。  
  
     [!code-cpp[System.Windows.Interop.D3DImage#RendererH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.h#rendererh)]  
  
3.  在代码编辑器中打开 Renderer.cpp，用下面的代码替换自动生成的代码。  
  
     [!code-cpp[System.Windows.Interop.D3DImage#RendererCPP](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderercpp)]  
  
4.  在代码编辑器中打开 RendererManager.h，用下面的代码替换自动生成的代码。  
  
     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.h#renderermanagerh)]  
  
5.  在代码编辑器中打开 RendererManager.cpp，用下面的代码替换自动生成的代码。  
  
     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerCPP](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanagercpp)]  
  
6.  在代码编辑器中打开 TriangleRenderer.h，用下面的代码替换自动生成的代码。  
  
     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.h#trianglerendererh)]  
  
7.  在代码编辑器中打开 TriangleRenderer.cpp，用下面的代码替换自动生成的代码。  
  
     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererCPP](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.cpp#trianglerenderercpp)]  
  
8.  在代码编辑器中打开 stdafx.h，用下面的代码替换自动生成的代码。  
  
     [!code-cpp[System.Windows.Interop.D3DImage#StdafxH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/stdafx.h#stdafxh)]  
  
9. 在代码编辑器中打开 dllmain.cpp，用下面的代码替换自动生成的代码。  
  
     [!code-cpp[System.Windows.Interop.D3DImage#DllMain](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/dllmain.cpp#dllmain)]  
  
10. 在代码编辑器中打开 D3DContent.def。  
  
11. 用下面的代码替换自动生成的代码。  
  
    ```  
  
    LIBRARY "D3DContent"  
  
    EXPORTS  
  
    SetSize  
    SetAlpha  
    SetNumDesiredSamples  
    SetAdapter  
  
    GetBackBufferNoRef  
    Render  
    Destroy  
  
    ```  
  
12. 生成项目。  
  
## 后续步骤  
  
-   在 WPF 应用程序中承载 Direct3D9 内容。  有关更多信息，请参见[演练：在 WPF 中承载 Direct3D9 内容](../../../../docs/framework/wpf/advanced/walkthrough-hosting-direct3d9-content-in-wpf.md)。  
  
## 请参阅  
 <xref:System.Windows.Interop.D3DImage>   
 [Direct3D9 和 WPF 互操作性的性能注意事项](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md)   
 [演练：在 WPF 中承载 Direct3D9 内容](../../../../docs/framework/wpf/advanced/walkthrough-hosting-direct3d9-content-in-wpf.md)