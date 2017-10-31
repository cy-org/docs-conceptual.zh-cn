---
title: "Direct3D9 和 WPF 互操作性的性能注意事项 | Microsoft Docs"
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
  - "Direct3D9 [WPF 互操作性], 性能"
  - "WPF, Direct3D9 互操作性能"
ms.assetid: ea8baf91-12fe-4b44-ac4d-477110ab14dd
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Direct3D9 和 WPF 互操作性的性能注意事项
可以使用 <xref:System.Windows.Interop.D3DImage> 类来承载 Direct3D9 内容。  承载 Direct3D9 内容可能会影响应用程序的性能。  本主题介绍在 Windows Presentation Foundation \(WPF\) 应用程序中承载 Direct3D9 内容时,优化性能的最佳做法。  这些最佳做法包括如何使用 <xref:System.Windows.Interop.D3DImage>，以及使用 Windows Vista、Windows XP 和多显示器显示时的最佳做法。  
  
> [!NOTE]
>  有关演示这些最佳做法的代码示例，请参见[WPF 和 Direct3D9 互操作](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md)。  
  
## 慎重使用 D3DImage  
 <xref:System.Windows.Interop.D3DImage> 实例中承载的 Direct3D9 内容在呈现时，速度不像在纯 Direct3D 应用程序中那样快。  复制图面和刷新命令缓冲区操作可能需要不少开销。  随着 <xref:System.Windows.Interop.D3DImage> 实例数的增加，刷新次数变多，性能随之下降。  因此，应慎重使用 <xref:System.Windows.Interop.D3DImage>。  
  
## Windows Vista 中的最佳做法  
 要使配置为使用 Windows 显示驱动程序模型 \(WDDM\) 的显示器在 Windows Vista 中具有最佳性能，应在 `IDirect3DDevice9Ex` 设备上创建 Direct3D9 图面。  这样可以启用图面共享。  视频卡必须支持 Windows Vista 中的 `D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES` 和 `D3DCAPS2_CANSHARERESOURCE` 驱动程序功能。  其他任何设置都会导致通过软件复制图面，这将显著降低性能。  
  
> [!NOTE]
>  如果 Windows Vista 中的显示器配置为使用 Windows XP 显示驱动程序模型 \(XDDM\)，则无论设置如何，都始终通过软件复制图面。  借助适当的设置和视频卡，使用 WDDM 时，在 Windows Vista 上可以观察到更好的性能，因为此时图面复制是在硬件中执行的。  
  
## Windows XP 中的最佳做法  
 要在使用 Windows XP 显示驱动程序模型 \(XDDM\) 的 Windows XP 上获得最佳性能，应创建能在调用 `IDirect3DSurface9::GetDC` 方法时正常工作的可锁定图面。  在内部，`BitBlt` 方法在硬件的各个设备之间传输图面。  `GetDC` 方法始终适用于 XRGB 图面。  但是，如果客户端计算机运行的是 Windows XP SP3 或 SP2，并且如果客户端还具有分层窗口功能的修补程序，则此方法仅适用于 ARGB 图面。  视频卡必须支持 `D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES` 驱动程序功能。  
  
 16 位桌面显示深度会显著降低性能。  建议使用 32 位桌面。  
  
 如果您针对 Windows Vista 和 Windows XP 进行开发，请在 Windows XP 上测试性能。  在 Windows XP 上，视频内存不足是一个需要关注的问题。  此外，与 Windows Vista WDDM 相比，Windows XP 上的 <xref:System.Windows.Interop.D3DImage> 会使用更多的视频内存和带宽，因为需要额外的视频内存复制。  因此，对同一视频硬件而言，可以预料其在 Windows XP 上的性能不如在 Windows Vista 上的性能。  
  
> [!NOTE]
>  XDDM 在 Windows XP 和 Windows Vista 上都可用；但 WDDM 仅在 Windows Vista 上可用。  
  
## 通行最佳做法  
 创建设备时，使用 `D3DCREATE_MULTITHREADED` 创建标记。  这会降低性能，但 WPF 呈现系统会在此设备上从另一线程调用方法。  请确保正确遵守锁定协议，防止两个线程同时访问设备。  
  
 如果呈现是在 WPF 托管线程上执行的，强烈建议您使用 `D3DCREATE_FPU_PRESERVE` 创建标记来创建设备。  若无此设置，D3D 呈现将降低 WPF 双精度操作的精确度，且引入呈现问题。  
  
 除非在没有硬件支持的情况下平铺非 pow2 图面，或者平铺包含 <xref:System.Windows.Interop.D3DImage> 的 <xref:System.Windows.Media.DrawingBrush> 或 <xref:System.Windows.Media.VisualBrush>，否则 <xref:System.Windows.Interop.D3DImage> 的平铺速度会很快。  
  
## 多显示器显示的最佳做法  
 如果您使用的计算机安装了多个显示器，则应该遵循前面介绍的最佳做法。  对于多显示器配置，还有其他一些性能注意事项。  
  
 创建后台缓冲区时，它是在特定的设备和适配器上创建的，但 WPF 可能是在任何适配器上显示前台缓冲区。  若选择通过在适配器间进行复制来更新前台缓冲区，开销将非常大。  在配置为使用 WDDM（具有多个视频卡和一个 `IDirect3DDevice9Ex` 设备）的 Windows Vista 上，如果前台缓冲区位于其他适配器上，但视频卡仍相同，对性能将没有影响。  但是，在 Windows XP 和具有多个视频卡的 XDDM 上，当前台缓冲区显示在异于后台缓冲区的适配器上时，对性能将有很大影响。  有关更多信息，请参见[WPF 和 Direct3D9 互操作](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md)。  
  
## 性能摘要  
 下表显示了前台缓冲区更新的性能对操作系统、像素格式和图面可锁定性的函数。  其中假设前、后台缓冲区位于同一适配器上。  硬件更新通常比软件更新速度快得多，具体程度取决于适配器配置。  
  
|图面像素格式|Windows Vista、WDDM 和 9Ex|其他 Windows Vista 配置|Windows XP SP3 或带修补程序的 SP2|Windows XP SP2|  
|------------|------------------------------|-------------------------|--------------------------------|--------------------|  
|D3DFMT\_X8R8G8B8（不可锁定）|**硬件更新**|软件更新|软件更新|软件更新|  
|D3DFMT\_X8R8G8B8（可锁定）|**硬件更新**|软件更新|**硬件更新**|**硬件更新**|  
|D3DFMT\_A8R8G8B8（不可锁定）|**硬件更新**|软件更新|软件更新|软件更新|  
|D3DFMT\_A8R8G8B8（可锁定）|**硬件更新**|软件更新|**硬件更新**|软件更新|  
  
## 请参阅  
 <xref:System.Windows.Interop.D3DImage>   
 [WPF 和 Direct3D9 互操作](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md)   
 [演练：创建在 WPF 中承载的 Direct3D9 内容](../../../../docs/framework/wpf/advanced/walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)   
 [演练：在 WPF 中承载 Direct3D9 内容](../../../../docs/framework/wpf/advanced/walkthrough-hosting-direct3d9-content-in-wpf.md)