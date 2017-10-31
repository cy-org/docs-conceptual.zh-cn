---
title: "优化性能：利用硬件 | Microsoft Docs"
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
  - "图形呈现层"
  - "图形, 性能"
  - "图形, 呈现层"
  - "硬件呈现管道"
  - "呈现层"
  - "软件呈现管道"
ms.assetid: bfb89bae-7aab-4cac-a26c-a956eda8fce2
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 优化性能：利用硬件
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的内部结构有两个呈现管道，即硬件和软件。  本主题提供有关这些呈现管道的信息，以帮助您在对应用程序进行性能优化时作出正确的决策。  
  
## 硬件呈现管道  
 决定 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 性能的最重要因素之一是它是呈现绑定的，即要呈现的像素越多，性能成本就越高。  但是，能转交给[!INCLUDE[TLA#tla_gpu](../../../../includes/tlasharptla-gpu-md.md)] 来处理的呈现任务越多，能获得的性能改进就越多。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序硬件呈现管道充分利用支持 [!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)] 7.0 版最小功能的硬件上的 [!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)] 功能。  通过支持 [!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)] 7.0 版和 PixelShader 2.0\+ 功能的硬件，可实现进一步的优化。  
  
## 软件呈现管道  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 软件呈现管道是完全绑定 CPU 的。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 利用 CPU 中的 SSE 和 SSE2 指令集来实现优化的、功能全面的软件光栅器。  只要无法使用硬件呈现管道呈现应用程序功能，都可以非常顺利地转而使用软件。  
  
 在以软件模式呈现时，遇到的最大的性能问题与填充率有关，该值定义为呈现的像素数目。  如果您关注采用软件呈现模式时的性能，请尝试将重绘像素的次数降至最少。  例如，如果您有一个具有蓝色背景的应用程序，随后要在该背景上呈现略微透明的图像，则要呈现两次应用程序中的所有像素。  因此，呈现具有该图像的应用程序所需的时间是呈现只有蓝色背景的应用程序的两倍。  
  
### 图形呈现层  
 预测应用程序将运行于的硬件配置可能很难。  但是，您可能会考虑一种设计，它使应用程序在不同的硬件上运行时可以顺利地切换功能，从而充分利用各个不同的硬件配置。  
  
 为了实现此目的，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一个功能，它可以在运行时确定系统的图形功能。  通过将视频卡归类为三个呈现功能层之一来确定图形功能。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 公开一个 [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)]，该 API 使应用程序可以查询呈现功能层。  然后应用程序就可以在运行时根据硬件支持的呈现层采用不同的代码路径。  
  
 对呈现层级别影响最大的图形硬件功能包括：  
  
-   **视频 RAM** 图形硬件中的视频内存量决定了可用于合成图形的缓冲区的大小和数量。  
  
-   **像素着色器** 像素着色器是按像素计算效果的图形处理功能。  每个显示帧可能有数百万像素需要处理，具体取决于所显示的图形的分辨率。  
  
-   **顶点着色器** 顶点着色器是对对象的顶点数据执行数学运算的图形处理功能。  
  
-   **多纹理支持** 多纹理支持是指在对三维图形对象执行混合操作期间应用两个或更多个不同纹理的功能。  多纹理支持的程度由图形硬件中的多纹理单元数决定。  
  
 像素着色器、顶点着色器和多纹理功能用于定义特定的 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 版本级别，而版本级别又用于定义 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的不同呈现层。  
  
 图形硬件的功能决定了 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序的呈现功能。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 系统定义了三个呈现层：  
  
-   **呈现层 0** 无图形硬件加速。  [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 版本级别低于 7.0。  
  
-   **呈现层 1** 部分图形硬件加速。  [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 版本级别高于或等于 7.0 且**低于** 9.0。  
  
-   **呈现层 2** 大多数图形功能都使用图形硬件加速。  [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 版本级别高于或等于 9.0。  
  
 有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 呈现层的更多信息，请参见[图形呈现层](../../../../docs/framework/wpf/advanced/graphics-rendering-tiers.md)。  
  
## 请参阅  
 [优化 WPF 应用程序性能](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [规划应用程序性能](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [布局和设计](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [对象行为](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [应用程序资源](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [其他性能建议](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)