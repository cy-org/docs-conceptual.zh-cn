---
title: "最大程度地提高 WPF 三维性能 | Microsoft Docs"
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
  - "三维图形 [WPF]"
ms.assetid: 4bcf949d-d92f-4d8d-8a9b-1e4c61b25bf6
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 最大程度地提高 WPF 三维性能
在应用程序中使用 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 生成三维控件并包含三维场景时，重要的一点是要考虑性能优化。本主题提供一个影响应用程序性能的三维类和属性的列表，以及使用这些类和属性时优化性能的建议。  
  
 本主题假定您已深入了解 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 三维功能。  本文档中的建议适用于“呈现层 2”\- 大致定义为支持像素着色器 2.0 版和顶点着色器 2.0 版的硬件。  有关更多详细信息，请参见[图形呈现层](../../../../docs/framework/wpf/advanced/graphics-rendering-tiers.md)。  
  
## 性能影响：高  
  
|||  
|-|-|  
|属性|建议|  
|<xref:System.Windows.Media.Brush>|画笔速度（从最快到最慢）：<br /><br /> <xref:System.Windows.Media.SolidColorBrush><br /><br /> <xref:System.Windows.Media.LinearGradientBrush><br /><br /> <xref:System.Windows.Media.ImageBrush><br /><br /> <xref:System.Windows.Media.DrawingBrush>（已缓存）<br /><br /> <xref:System.Windows.Media.VisualBrush>（已缓存）<br /><br /> <xref:System.Windows.Media.RadialGradientBrush><br /><br /> <xref:System.Windows.Media.DrawingBrush>（未缓存）<br /><br /> <xref:System.Windows.Media.VisualBrush>（未缓存）|  
|<xref:System.Windows.UIElement.ClipToBoundsProperty>|在不需要 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 显式将 <xref:System.Windows.Controls.Viewport3D> 的内容剪辑到 Viewport3D 的矩形时，将 `Viewport3D.ClipToBounds` 设置为 false。[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 的抗锯齿剪辑非常慢，并且 `ClipToBounds` 在 <xref:System.Windows.Controls.Viewport3D> 上是默认启用的（较慢）。|  
|<xref:System.Windows.UIElement.IsHitTestVisible%2A>|如果在执行鼠标命中测试时不需要让 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 考虑 <xref:System.Windows.Controls.Viewport3D> 的内容，将 `Viewport3D.IsHitTestVisible` 设置为 false。对三维内容的命中测试是以软件进行的，遇到大型网格时可能非常慢。<xref:System.Windows.UIElement.IsHitTestVisible%2A> 在 <xref:System.Windows.Controls.Viewport3D> 上是默认启用的（较慢）。|  
|<xref:System.Windows.Media.Media3D.GeometryModel3D>|仅当需要不同的 Material 或 Transform 时，才会创建不同的模型。  否则，请尝试将具有相同 Material 和 Transform 的多个 <xref:System.Windows.Media.Media3D.GeometryModel3D> 实例合并到少数几个较大的 <xref:System.Windows.Media.Media3D.GeometryModel3D> 和 <xref:System.Windows.Media.Media3D.MeshGeometry3D> 实例中。|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|网格动画是指按帧更改网格的各个顶点，在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中它并非总是那么高效。在修改每个顶点时，为了尽可能降低更改通知对性能的影响，应在对每个顶点执行修改之前将网格与可视化树分离。修改网格之后，再将网格重新附加到可视化树。此外，应尝试尽量减小以这种方式进行动画处理的网格大小。|  
|3D Antialiasing|若要提高呈现速度，请通过将附加属性 <xref:System.Windows.Media.RenderOptions.EdgeMode%2A> 设置为 `Aliased`，在 <xref:System.Windows.Controls.Viewport3D> 上禁用多级采样。  默认情况下，三维抗锯齿在 [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 中是禁用的，而在 [!INCLUDE[TLA#tla_longhorn](../../../../includes/tlasharptla-longhorn-md.md)] 中是启用的，每个像素具有 4 个样本。|  
|Text|三维场景中的实时文本（由于位于 <xref:System.Windows.Media.DrawingBrush> 或 <xref:System.Windows.Media.VisualBrush> 中，因此是实时文本）非常缓慢。  请尝试改用文本的图像（通过 <xref:System.Windows.Media.Imaging.RenderTargetBitmap>），除非文本会发生更改。|  
|<xref:System.Windows.Media.TileBrush>|如果由于该画笔的内容不是静态的而导致必须在三维场景中使用 <xref:System.Windows.Media.VisualBrush> 或 <xref:System.Windows.Media.DrawingBrush>，请尝试缓存此画笔，方法是将附加属性 <xref:System.Windows.Media.RenderOptions.CachingHint%2A> 设置为 `Cache`。  使用 <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMinimum%2A> 和 <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A> 附加属性设置无效缩放的最小和最大阈值，以便不会过度频繁地重新生成缓存的画笔，同时保持所需的质量。  默认情况下不会缓存 <xref:System.Windows.Media.DrawingBrush> 和 <xref:System.Windows.Media.VisualBrush>，这表示当每次必须重新呈现使用画笔绘制的内容时，必须首先将画笔的整个内容重新呈现到中间图面。|  
|<xref:System.Windows.Media.Effects.BitmapEffect>|<xref:System.Windows.Media.Effects.BitmapEffect> 强制呈现所有受影响的内容，无需硬件加速。  为获取最佳性能，请不要使用 <xref:System.Windows.Media.Effects.BitmapEffect>。|  
  
## 性能影响：中  
  
|||  
|-|-|  
|属性|建议|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|如果通过共享顶点和具有相同的位置、法向量和纹理坐标的顶点以邻接三角形的形式定义网格，只需定义一次每个共享的顶点，然后使用带有 <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A> 的索引来定义三角形。|  
|<xref:System.Windows.Media.ImageBrush>|当您可以显式控制纹理大小时（例如当您正在使用 <xref:System.Windows.Media.Imaging.RenderTargetBitmap> 和\/或 <xref:System.Windows.Media.ImageBrush> 时），请尝试将其大小最小化。  请注意，较低的纹理分辨率会降低显示质量，因此，请在质量和性能之间进行合理选择。|  
|Opacity|呈现半透明的三维内容（如反射）时，请通过 <xref:System.Windows.Media.Brush.Opacity%2A> 或 <xref:System.Windows.Media.Media3D.DiffuseMaterial.Color%2A> 使用画笔或材料上的不透明度属性，而不要通过将 `Viewport3D.Opacity` 设置为小于 1 的值来创建单独的半透明 <xref:System.Windows.Controls.Viewport3D>。|  
|<xref:System.Windows.Controls.Viewport3D>|尽可能减少场景中正在使用的 <xref:System.Windows.Controls.Viewport3D> 对象的数目。  将多个三维模型放置到同一个 Viewport3D 中，而不是为每个模型创建单独的 Viewport3D 实例。|  
|<xref:System.Windows.Freezable>|通常，最好重复使用 <xref:System.Windows.Media.Media3D.MeshGeometry3D>、<xref:System.Windows.Media.Media3D.GeometryModel3D>、Brush 和 Material。  由于它们都是从 `Freezable` 派生的，因此都具有多个父级。|  
|<xref:System.Windows.Freezable>|当 Freezable 的属性在应用程序中保持不变时，请对其调用 <xref:System.Windows.Freezable.Freeze%2A> 方法。  冻结可减少工作集并提高速度。|  
|<xref:System.Windows.Media.Brush>|当画笔的内容不会发生更改时，请使用 <xref:System.Windows.Media.ImageBrush>，而不要使用 <xref:System.Windows.Media.VisualBrush> 或 <xref:System.Windows.Media.DrawingBrush>。  二维内容可以通过 <xref:System.Windows.Media.Imaging.RenderTargetBitmap> 转换为 <xref:System.Windows.Controls.Image>，然后再在 <xref:System.Windows.Media.ImageBrush> 中使用。|  
|<xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A>|请不要使用 <xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A>，除非您确实需要查看 <xref:System.Windows.Media.Media3D.GeometryModel3D> 的背面。|  
|<xref:System.Windows.Media.Media3D.Light>|光源速度（从最快到最慢）：<br /><br /> <xref:System.Windows.Media.Media3D.AmbientLight><br /><br /> <xref:System.Windows.Media.Media3D.DirectionalLight><br /><br /> <xref:System.Windows.Media.Media3D.PointLight><br /><br /> <xref:System.Windows.Media.Media3D.SpotLight>|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|尽量使网格大小小于下列限制：<br /><br /> <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A>：20,001 个 <xref:System.Windows.Media.Media3D.Point3D> 实例<br /><br /> <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A>：60,003 个 <xref:System.Int32> 实例|  
|<xref:System.Windows.Media.Media3D.Material>|Material 速度（从最快到最慢）：<br /><br /> <xref:System.Windows.Media.Media3D.EmissiveMaterial><br /><br /> <xref:System.Windows.Media.Media3D.DiffuseMaterial><br /><br /> <xref:System.Windows.Media.Media3D.SpecularMaterial>|  
|<xref:System.Windows.Media.Brush>|[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 三维不会以一致的方式退出不可见的画笔（黑色环境画笔、透明画笔等）。可以考虑在场景中省略这些画笔。|  
|<xref:System.Windows.Media.Media3D.MaterialGroup>|<xref:System.Windows.Media.Media3D.MaterialGroup> 中的每个 <xref:System.Windows.Media.Media3D.Material> 都会引起其他呈现过程，因此包含多个材料（即使是简单的材料）会大幅度增加 GPU 的填充请求。  请尽量减少 <xref:System.Windows.Media.Media3D.MaterialGroup> 中材料的数目。|  
  
## 性能影响：低  
  
|||  
|-|-|  
|属性|建议|  
|<xref:System.Windows.Media.Media3D.Transform3DGroup>|如果不需要动画或数据绑定，请不要使用包含多个变换的变换组，而应使用单一 <xref:System.Windows.Media.Media3D.MatrixTransform3D>，将其设置为变换组中原本应单独存在的所有变换的积。|  
|<xref:System.Windows.Media.Media3D.Light>|请最大程度地减少场景中的光源数。  场景中光源过多会使 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 动用软件呈现。此限制大致为 110 个 <xref:System.Windows.Media.Media3D.DirectionalLight> 对象、70 个 <xref:System.Windows.Media.Media3D.PointLight> 对象或 40 个 <xref:System.Windows.Media.Media3D.SpotLight> 对象。|  
|<xref:System.Windows.Media.Media3D.ModelVisual3D>|将移动对象与静态对象分隔开来，方法是将移动对象放置到单独的 <xref:System.Windows.Media.Media3D.ModelVisual3D> 实例中。  ModelVisual3D 比 <xref:System.Windows.Media.Media3D.GeometryModel3D> 更“重”，因为它缓存了变换的边界。  GeometryModel3D 适用于模型；ModelVisual3D 适用于场景节点。  请使用 ModelVisual3D 将 GeometryModel3D 的共享实例放置到场景中。|  
|<xref:System.Windows.Media.Media3D.Light>|请最大程度地减少场景中光源数的更改次数。  每次更改光源数都会强制重新生成和重新编译着色器，除非该配置原来已经存在（并因此而缓存其着色器）。|  
|Light|黑色光源是不可见的，但它们会增加呈现时间；请考虑不要使用它们。|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|若要最大程度地减少在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中构建大型集合（如 MeshGeometry3D 的 <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A>、<xref:System.Windows.Media.Media3D.MeshGeometry3D.Normals%2A>、<xref:System.Windows.Media.Media3D.MeshGeometry3D.TextureCoordinates%2A> 和 <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A>）的时间，请在填充值之前预先调整集合大小。  如果可能，请向集合的构造函数传递预填充数据结构（例如数组或列表）。|  
  
## 请参阅  
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)