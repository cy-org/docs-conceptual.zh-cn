---
title: "创建和使用组件 (Visual Basic)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- components [Visual Basic]
ms.assetid: ee6a4156-73f7-4e9b-8e01-c74c4798b65c
caps.latest.revision: 9
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 03929dd0dbb81a9efee5b69ede78ff0b4ab4d380
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="creating-and-using-components-in-visual-basic"></a>创建和使用组件 (Visual Basic)
组件是一个类，该类实现 <xref:System.ComponentModel.IComponent?displayProperty=fullName> 接口或直接/间接派生自实现 <xref:System.ComponentModel.IComponent> 的类。 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 组件是可重复使用的对象，可以和其他对象进行交互，并提供对外部资源和设计时支持的控制。  
  
 组件的一个重要特性在于它们是可设计的，这意味着可以在 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] 集成开发环境中使用作为组件的类。 可以将组件添加到“工具箱”、拖放到窗体以及在设计图面上操作。 请注意，对组件的基本设计时支持已内置于 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 中；组件开发人员不必执行任何附加工作便可利用基本设计时功能。  
  
 控件与组件类似，二者都是可设计的。 不过，控件提供用户界面，而组件不提供。 控件必须派生自基控件类之一：<xref:System.Windows.Forms.Control> 或 <xref:System.Web.UI.Control>。  
  
## <a name="when-to-create-a-component"></a>创建组件的时间  
 如果类将在设计图面（如 Windows 窗体设计器或 Web 窗体设计器）上使用，但没有用户界面，此类应该是一个组件并实现 <xref:System.ComponentModel.IComponent>，或者是从直接或间接实现 <xref:System.ComponentModel.IComponent> 的类派生的。  
  
 <xref:System.ComponentModel.Component> 和 <xref:System.ComponentModel.MarshalByValueComponent> 类是 <xref:System.ComponentModel.IComponent> 接口的基实现。 这些类之间的主要区别在于 <xref:System.ComponentModel.Component> 类由引用封送，而 <xref:System.ComponentModel.IComponent> 由值封送。 以下列表为实施者提供了全面的指南。  
  
-   如果组件需要由引用封送，请从 <xref:System.ComponentModel.Component> 派生。  
  
-   如果组件需要由值封送，请从 <xref:System.ComponentModel.MarshalByValueComponent> 派生。  
  
-   如果因单一继承导致无法从其中一个基实现派生组件，则请实现 <xref:System.ComponentModel.IComponent>。  
  
 有关设计时支持的详细信息，请参阅[组件的设计时特性](http://msdn.microsoft.com/library/12050fe3-9327-4509-9e21-4ee2494b95c3)和[扩展设计时支持](http://msdn.microsoft.com/library/d6ac8a6a-42fd-4bc8-bf33-b212811297e2)。  
  
## <a name="component-classes"></a>组件类  
 <xref:System.ComponentModel> 命名空间提供用于实现组件和控件的运行时和设计时行为的类。 此命名空间包括用于特性和类型转换器的实现、数据源绑定和组件授权的基类和接口。  
  
 核心组件类包括：  
  
-   <xref:System.ComponentModel.Component>。 <xref:System.ComponentModel.IComponent> 接口的基实现。 此类可以实现在应用程序之间共享对象。  
  
-   <xref:System.ComponentModel.MarshalByValueComponent>。 <xref:System.ComponentModel.IComponent> 接口的基实现。  
  
-   <xref:System.ComponentModel.Container>。 <xref:System.ComponentModel.IContainer> 接口的基实现。 此类封装零个或多个组件。  
  
 部分用于组件授权的类包括：  
  
-   <xref:System.ComponentModel.License>。 所有许可证的抽象基类。 对组件的特定实例授予许可证。  
  
-   <xref:System.ComponentModel.LicenseManager>。 提供属性和方法，用以将许可证添加到组件和管理 <xref:System.ComponentModel.LicenseProvider>。  
  
-   <xref:System.ComponentModel.LicenseProvider>。 实现许可证提供程序的抽象基类。  
  
-   <xref:System.ComponentModel.LicenseProviderAttribute>。 指定要与某个类一起使用的 <xref:System.ComponentModel.LicenseProvider> 类。  
  
 常用于描述和保存组件的类。  
  
-   <xref:System.ComponentModel.TypeDescriptor>。 提供有关组件特征的信息，如组件的特性、属性和事件。  
  
-   <xref:System.ComponentModel.EventDescriptor>。 提供有关事件的信息。  
  
-   <xref:System.ComponentModel.PropertyDescriptor>。 提供有关属性的信息。  
  
## <a name="related-sections"></a>相关章节  
 [类、组件和控件](http://msdn.microsoft.com/library/db8b842e-44d9-40cc-a0f8-70fd189632c3)  
 定义组件和控件，并讨论二者与类之间的区别。  
  
 [组件创作](http://msdn.microsoft.com/library/4a5a5e49-0378-4a31-83bc-24da0f1a727d)  
 组件入门路线图。  
  
 [组件创作演练](http://msdn.microsoft.com/library/c414cca9-2489-4208-8b38-954586d91c13)  
 链接到提供组件编程的分步说明的主题。  
  
 [组件类](http://msdn.microsoft.com/library/ce2e5647-e673-4c2b-8125-ffebbd9d71bc)  
 描述什么使类成为组件、公开组件功能的方法、控制对组件的访问以及控制如何创建组件实例。  
  
 [控件和组件创作疑难解答](../../framework/winforms/controls/troubleshooting-control-and-component-authoring.md)  
 解释如何解决常见问题。  
  
## <a name="see-also"></a>另请参阅  
 [如何：在 Windows 窗体中访问设计时支持](http://msdn.microsoft.com/library/a84f8579-1f47-41b9-ba37-69030b0aff09)   
 [如何：在设计模式下扩展控件的外观和行为](http://msdn.microsoft.com/library/68f85054-2253-47f5-a4f2-3f1ac8c9f27b)   
 [如何：在设计模式下执行控件的自定义初始化](http://msdn.microsoft.com/library/914eaa03-092f-4556-9160-b8a2a40641d9)

