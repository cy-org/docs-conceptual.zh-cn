---
title: "WPF 和 Direct3D9 互操作 | Microsoft Docs"
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
  - "Direct3D9 [WPF 互操作性], 创建 Direct3D9 内容"
  - "WPF, 创建 Direct3D9 内容"
ms.assetid: 1b14b823-69c4-4e8d-99e4-f6dade58f89a
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# WPF 和 Direct3D9 互操作
可以在 Windows Presentation Foundation \(WPF\) 应用程序中包含 Direct3D9 内容。  本主题介绍如何创建 Direct3D9 内容以使其有效地与 WPF 交互操作。  
  
> [!NOTE]
>  当在 WPF 中使用 Direct3D9 内容时，还需要考虑性能问题。  有关如何针对性能进行优化的更多信息，请参见 [Direct3D9 和 WPF 互操作性的性能注意事项](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md)。  
  
## 显示缓冲区  
 <xref:System.Windows.Interop.D3DImage> 类管理两种显示缓冲区，这两种缓冲区分别称为“后台缓冲区”和“前台缓冲区”。  后台缓冲区是 Direct3D9 图面。  当您调用 <xref:System.Windows.Interop.D3DImage.Unlock%2A> 方法时，会将对后台缓冲区所做的更改向前复制到前台缓冲区。  
  
 下面的插图显示后台缓冲区与前台缓冲区之间的关系。  
  
 ![D3DImage 显示缓冲区](../../../../docs/framework/wpf/advanced/media/d3dimage-buffers.png "D3DImage\_buffers")  
  
## Direct3D9 设备创建  
 若要呈现 Direct3D9 内容，必须创建 Direct3D9 设备。  可用于创建设备的 Direct3D9 对象有两个：`IDirect3D9` 和 `IDirect3D9Ex`。  使用这些对象可以分别创建 `IDirect3DDevice9` 和 `IDirect3DDevice9Ex` 设备。  
  
 通过调用下列方法之一来创建设备。  
  
-   `IDirect3D9 * Direct3DCreate9(UINT SDKVersion);`  
  
-   `HRESULT Direct3DCreate9Ex(UINT SDKVersion, IDirect3D9Ex **ppD3D);`  
  
 在Windows vista或更高版本的操作系统上，请使用配置为使用Windows显示驱动程序模型\(WDDM\)显示的 `Direct3DCreate9Ex` 方法。  在任何其他平台上使用 `Direct3DCreate9` 方法。  
  
### Direct3DCreate9Ex 方法的可用性  
 该d3d9.dll具有 `Direct3DCreate9Ex` 只有方法在Windows vista或更高版本的操作系统。  如果在 Windows XP 上直接链接到该函数，将无法加载您的应用程序。  若要确定是否支持 `Direct3DCreate9Ex` 方法，请加载该 DLL，并查找进程地址。  下面的代码演示如何测试 `Direct3DCreate9Ex` 方法。  有关完整的代码示例，请参见[演练：创建在 WPF 中承载的 Direct3D9 内容](../../../../docs/framework/wpf/advanced/walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_EnsureD3DObjects](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_ensured3dobjects)]  
  
### HWND 创建  
 创建设备需要一个 HWND。  通常，可以创建虚拟 HWND 以供 Direct3D9 使用。  下面的代码示例演示如何创建虚拟 HWND。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_EnsureHWND](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_ensurehwnd)]  
  
### 提供参数  
 创建设备还需要一个 `D3DPRESENT_PARAMETERS` 结构，但仅有少数几个参数较为重要。  选择这些参数可以最小化内存空间。  
  
 将 `BackBufferHeight` 和 `BackBufferWidth` 字段都设置为 1。  如果将这两个字段设置为 0，则会使这两个字段设置为 HWND 的尺寸。  
  
 始终设置 `D3DCREATE_MULTITHREADED` 和 `D3DCREATE_FPU_PRESERVE` 标志，以防止 Direct3D9 使用损坏的内存，并防止 Direct3D9 更改 FPU 设置。  
  
 下面的代码演示如何初始化 `D3DPRESENT_PARAMETERS` 结构。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#Renderer_Init](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderer_init)]  
  
## 创建后台缓冲区呈现目标  
 若要在 <xref:System.Windows.Interop.D3DImage> 中显示 Direct3D9 内容，需创建一个 Direct3D9 图面，并通过调用 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 方法为其赋值。  
  
### 验证适配器支持  
 在创建图面之前，请验证所有适配器是否都支持您所需的图面属性。  即使只将图面呈现到一个适配器，WPF 窗口也可能显示在系统的任何一个适配器上。  应始终编写处理多适配器配置的 Direct3D9 代码，并检查所有适配器的支持情况，因为 WPF 可能需要在可用的适配器间移动图面。  
  
 下面的代码示例演示如何检查系统上所有适配器对 Direct3D9 的支持情况。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_TestSurfaceSettings](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_testsurfacesettings)]  
  
### 创建图面  
 在创建图面之前，应验证设备功能在目标操作系统上是否支持良好的性能。  有关更多信息，请参见 [Direct3D9 和 WPF 互操作性的性能注意事项](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md)。  
  
 验证了设备功能之后，即可以创建图面。  下面的代码示例演示如何创建呈现目标。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#Renderer_CreateSurface](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderer_createsurface)]  
  
### WDDM  
 在Windows vista和更高版本的操作系统上，配置为使用WDDM，可以创建呈现目标纹理，并将0级图面到 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 方法。  建议不要在 Windows XP 上使用此方法，因为无法创建可锁定的呈现目标纹理，因而会降低性能。  
  
## 处理设备状态  
 <xref:System.Windows.Interop.D3DImage> 类管理两种显示缓冲区，这两种缓冲区分别称为“后台缓冲区”和“前台缓冲区”。  后台缓冲区是 Direct3D 图面。  对后台缓冲区的更改向前复制到前台缓冲区，当您调用 <xref:System.Windows.Interop.D3DImage.Unlock%2A> 方法时，它为硬件上显示。  有时，前台缓冲区变得不可用。  这种不可用情况可能是由屏幕锁定、全屏独占 Direct3D 应用程序、用户切换或其他系统活动导致的。  发生这种情况时，您的WPF应用程序都通过处理 <xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged> 事件通知。  您的应用程序如何响应变为之前的缓冲区可用取决于WPF是否启用回退到软件呈现。  <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 方法具有参数指定的重载WPF是否会退回到软件呈现。  
  
 当您调用 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%29> 重载调用或时使用 `enableSoftwareFallback` 参数的 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%2CSystem.Boolean%29> 重载设置为 `false`时，该呈现系统将释放它对后台缓冲区，当前台缓冲区变得不可用，而未显示。  当前台缓冲区再次时可用，则呈现系统将引发 <xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged> 事件通知您的WPF应用程序。  可以创建 <xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged> 事件的事件处理程序可以重新激活再次呈现一个有效的呈现图面。  若要重新启动呈现，必须调用 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A>。  
  
 当您调用了 `enableSoftwareFallback` 参数的 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%2CSystem.Boolean%29> 重载设置为 `true`时，该呈现系统保留其对后台缓冲区，当前台缓冲区变得不可用时，因此不需要调用 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> ，当前台缓冲区再次时可用。  
  
 当软件呈现启用时，可能有用户的计算机变得不可用的情况，但是，该呈现系统将保持对呈现图面。  若要检查Direct3D9设备是否可用，请调用 `TestCooperativeLevel` 方法。  ，因为 `TestCooperativeLevel` 方法已弃用并始终返回成功，若要检查Direct3D9Ex设备调用 `CheckDeviceState` 方法。  如果用户计算机变得不可用，请调用 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 释放WPF对后台缓冲区。  如果需要重置设备，调用与 `backBuffer` 参数的 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 设置为 `null`，然后调用 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 和 `backBuffer` 设置为有效的Direct3D面再次  
  
 仅在实现了多适配器支持时才调用 `Reset` 方法以从无效设备中恢复。  否则，将需要释放所有 Direct3D9 接口，然后再重新创建这些接口。  如果适配器布局发生了更改，则不会更新更改前创建的 Direct3D9 对象。  
  
## 处理大小调整  
 除了本机范围外，如果 <xref:System.Windows.Interop.D3DImage> 显示在解析，它基于当前 <xref:System.Windows.Media.RenderOptions.BitmapScalingMode%2A>缩放，除此之外， <xref:System.Windows.Media.Effects.SamplingMode> 用 <xref:System.Windows.Media.BitmapScalingMode>进行替换。  
  
 如果需要更高的保真度，则在 <xref:System.Windows.Interop.D3DImage> 的容器大小发生变化时，必须创建新的图面。  
  
 用来处理大小调整的方法有三种。  
  
-   参与布局系统，并在大小发生变化时创建新图面。  不要创建过多的图面，否则可能会耗尽视频内存或使其分段。  
  
-   请等待，直到在固定的时段内不会再发生大小调整事件时再创建新图面。  
  
-   创建一个 <xref:System.Windows.Threading.DispatcherTimer>，每秒对容器维度进行多次检查。  
  
## 多监视器优化  
 当呈现系统将 <xref:System.Windows.Interop.D3DImage> 移动到其他监视器时，性能会急剧下降。  
  
 在 WDDM 上，只要监视器在同一视频卡上，并使用 `Direct3DCreate9Ex`，性能就不会下降。  如果监视器在不同的视频卡上，则性能会下降。  在 Windows XP 上，性能始终会下降。  
  
 当 <xref:System.Windows.Interop.D3DImage> 移动到其他监视器时，可以在相应的适配器上创建新图面，以恢复良好的性能。  
  
 若要避免性能降低，可以为多监视器情况专门编写代码。  下面的列表介绍了一种编写多监视器代码的方法。  
  
1.  用 `Visual.ProjectToScreen` 方法查找屏幕空间中 <xref:System.Windows.Interop.D3DImage> 上的一个点。  
  
2.  使用 `MonitorFromPoint` GDI 方法查找显示该点的监视器。  
  
3.  使用 `IDirect3D9::GetAdapterMonitor` 方法查找监视器所在的 Direct3D9 适配器。  
  
4.  如果适配器不同于具有后台缓存区的适配器，则在新监视器上创建一个新的后台缓冲区，并将其分配给 <xref:System.Windows.Interop.D3DImage> 后台缓冲区。  
  
> [!NOTE]
>  如果 <xref:System.Windows.Interop.D3DImage> 跨多台监视器，则会降低性能，WDDM 和 `IDirect3D9Ex` 位于同一适配器上的情况除外。  在这种情况下，无法提高性能。  
  
 下面的代码示例演示如何查找当前监视器。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_SetAdapter](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_setadapter)]  
  
 在 <xref:System.Windows.Interop.D3DImage> 容器的大小或位置发生变化时更新监视器，或通过使用每秒更新多次的 `DispatcherTimer` 来更新监视器。  
  
## WPF 软件呈现  
 在以下情况下，WPF 会同步呈现在软件中的 UI 线程上。  
  
-   打印  
  
-   <xref:System.Windows.Media.Effects.BitmapEffect>  
  
-   <xref:System.Windows.Media.Imaging.RenderTargetBitmap>  
  
 发生其中一种情况时，呈现系统将调用 <xref:System.Windows.Interop.D3DImage.CopyBackBuffer%2A> 方法以将硬件缓冲区复制到软件。  默认实现用您的图面调用 `GetRenderTargetData` 方法。  因为此调用发生在锁定\/取消锁定模式之外，所以调用可能会失败。  在这种情况下，`CopyBackBuffer` 方法返回 `null`，并且不显示任何图像。  
  
 您可以重写 <xref:System.Windows.Interop.D3DImage.CopyBackBuffer%2A> 方法，调用基实现，如果它返回 `null`，您可以返回一个占位符 <xref:System.Windows.Media.Imaging.BitmapSource>。  
  
 您还可以实现自己的软件呈现（而不是调用基实现）。  
  
> [!NOTE]
>  如果 WPF 完全呈现在软件中，则不会显示 <xref:System.Windows.Interop.D3DImage>，因为 WPF 没有前台缓冲区。  
  
## 请参阅  
 <xref:System.Windows.Interop.D3DImage>   
 [Direct3D9 和 WPF 互操作性的性能注意事项](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md)   
 [演练：创建在 WPF 中承载的 Direct3D9 内容](../../../../docs/framework/wpf/advanced/walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)   
 [演练：在 WPF 中承载 Direct3D9 内容](../../../../docs/framework/wpf/advanced/walkthrough-hosting-direct3d9-content-in-wpf.md)