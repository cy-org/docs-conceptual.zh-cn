---
title: "PrintForm 组件 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- PrintForm component [Visual Basic]
ms.assetid: 03de98b8-b54c-4764-91d7-83c64e974750
caps.latest.revision: 19
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f0c51ef0131c874ed33af7a19f9145a790d14ade
ms.lasthandoff: 03/13/2017

---
# <a name="printform-component-visual-basic"></a>PrintForm 组件 (Visual Basic)
<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件可以对[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]使你能够在运行时打印 Windows 窗体的图像。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 其行为取代了 Visual Basic 早期版本中的 `PrintForm` 方法。  
  
 Visual Studio 中不再包含 PowerPack 控件，但你可以从 [下载中心](http://www.microsoft.com/en-us/download/details.aspx?id=25169)下载它们。  
  
## <a name="printform-component-overview"></a>PrintForm 组件概述  
 Windows 窗体的一个常见方案是创建格式设置为类似于纸质表单或报表的窗体，然后打印窗体的图像。 虽然您可以使用<xref:System.Drawing.Printing.PrintDocument>组件来执行此操作，它将需要大量的代码。</xref:System.Drawing.Printing.PrintDocument> <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件，您可以打印到打印机、 打印预览窗口或文件的窗体的图像，而无需使用<xref:System.Drawing.Printing.PrintDocument>组件。</xref:System.Drawing.Printing.PrintDocument> </xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件位于**Visual Basic PowerPacks**的选项卡上**工具箱**。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 将其拖动到窗体上时，它将显示在组件栏中，组件栏是窗体下边框之下的小块区域。 选中该组件后，可以在“属性” **** 窗口中设置定义其行为的属性。 所有这些属性也可以在代码中设置。 您还可以创建的实例<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件而无需在设计时添加该组件的代码中。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
 打印窗体时，将打印该窗体工作区中的所有内容。 这包括所有控件和通过图形方法在窗体上绘制的任何文本或图形。 默认情况下，不打印窗体的标题栏、滚动条和边框。 此外，默认情况下，<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件打印窗体中的，只有可见部分。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 例如，如果用户在运行时调整窗体大小，则只打印当前可见的控件和图形。  
  
 通过使用的默认打印机<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件取决于操作系统的控制面板设置。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
 启动打印后，一种标准<xref:System.Drawing.Printing.PrintDocument>打印对话框随即显示。</xref:System.Drawing.Printing.PrintDocument> 用户可通过此对话框取消打印作业。  
  
### <a name="key-methods-properties-and-events"></a>关键方法、属性和事件  
 主要方法<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件是<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>方法，打印到打印机、 打印预览窗口中或文件格式的图像。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A> </xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 有两个版本的<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>方法︰</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>  
  
-   不带参数基本版本︰`Print()`  
  
-   使用指定打印行为的参数的重载的版本︰`Print(printForm As Form, printFormOption As PrintOption)`  
  
     重载的方法的 `PrintOption` 参数将决定用于打印窗体的基础实现；是否打印窗体的标题栏、滚动条和边框；是否打印窗体的可滚动部分。  
  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>属性是键属性的<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> </xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> 此属性确定是将输出发送到打印机、显示在打印预览窗口中还是另存为封装的 PostScript 文件。 如果<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>属性设置为<xref:System.Drawing.Printing.PrintAction>、<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintFileName%2A>属性指定的路径和文件名的名称。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintFileName%2A> </xref:System.Drawing.Printing.PrintAction> </xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>  
  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrinterSettings%2A>属性提供对基础<xref:System.Drawing.Printing.PrintDocument.PrinterSettings%2A>对象，可用于指定要使用的打印机和打印的份数诸如设置</xref:System.Drawing.Printing.PrintDocument.PrinterSettings%2A>的访问</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrinterSettings%2A> 此外还可以查询打印机的功能，如颜色或双工支持。 此属性不显示在“属性” **** 窗口中；只能从代码对其进行访问。  
  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Form%2A>属性用于指定要打印在调用时的窗体<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件以编程方式。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> </xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Form%2A> 如果在设计时向某窗体添加了该组件，则该窗体为默认窗体。  
  
 关键事件<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件包括以下︰</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
-   <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.BeginPrint>事件。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.BeginPrint> 发生时<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>调用方法之前打印文档的第一页。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>  
  
-   <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.EndPrint>事件。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.EndPrint> 在已打印最后一页之后发生。  
  
-   <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.QueryPageSettings>事件。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.QueryPageSettings> 在打印每一页之前立即发生。  
  
### <a name="remarks"></a>备注  
 如果窗体中包含文本或图形绘制<xref:System.Drawing.Graphics>方法时，使用基本<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>(`Print()`) 方法，以打印它。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A> </xref:System.Drawing.Graphics> 在某些操作系统上可能无法呈现图形时重载<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>使用方法。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>  
  
 如果窗体的宽度大于打印机中纸张的宽度，则窗体的右侧可能被截断。 设计要打印的窗体时，请确保窗体可容纳于标准尺寸的纸张之上。  
  
## <a name="example"></a>示例  
 下面的示例演示一种常用的<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
```  
' Visual Basic.  
Dim pf As New PrintForm  
pf.Form = Me  
pf.PrintAction = PrintToPrinter  
pf.Print()  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A></xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>   
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A></xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>   
 [如何︰ 使用 PrintForm 组件打印窗体](../../../visual-basic/developing-apps/printing/how-to-print-a-form-by-using-the-printform-component.md)   
 [如何︰ 打印窗体的工作区](../../../visual-basic/developing-apps/printing/how-to-print-the-client-area-of-a-form.md)   
 [如何︰ 打印客户端和窗体的非工作区](../../../visual-basic/developing-apps/printing/how-to-print-client-and-non-client-areas-of-a-form.md)   
 [如何：打印可滚动的窗体](../../../visual-basic/developing-apps/printing/how-to-print-a-scrollable-form.md)
