---
title: "My.Forms 对象 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "My.Forms"
  - "My.MyProject.Forms"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Forms 对象"
ms.assetid: f6bff4e6-6769-4294-956b-037aa6106d2a
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# My.Forms 对象
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

提供属性，用于访问在当前项目中声明的每个 Windows 窗体的实例。  
  
## 备注  
 `My.Forms` 对象提供了当前项目中每个窗体的实例。  属性与它所访问的窗体同名。  有关向项目添加窗体的信息，请参见 [How to: Add Windows Forms to a Project](http://msdn.microsoft.com/zh-cn/3d7bb25f-fd90-47cf-9378-fa0d764686c1)。  
  
 您可以通过使用窗体名称（无需限定）访问由 `My.Forms` 对象提供的窗体。  由于属性名称与窗体的类型名称相同，这将允许您如同窗体具有默认实例那样来访问窗体。  例如，`My.Forms.Form1.Show` 等效于 `Form1.Show`。  
  
 `My.Forms` 对象仅公开与当前项目关联的窗体。  它不会提供对在引用 DLL 中声明的窗体的访问。  若要访问 DLL 提供的窗体，必须使用窗体的限定名，书写格式为 *Dll 名称*.*窗体名称*。  
  
 可以使用 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A> 属性获取所有应用程序的打开窗体的集合。  
  
 此对象及其属性仅可用于 Windows 应用程序。  
  
## 属性  
 `My.Forms` 对象的每个属性提供了对当前项目中某个窗体实例的访问。  属性与此属性所访问的窗体同名，且属性类型与窗体类型相同。  
  
> [!NOTE]
>  如果发生名称冲突，则用于访问窗体的属性名称将为*根命名空间*\_*命名空间*\_*窗体名称*。  例如，假设有两个名为 `Form1.` 的窗体。如果其中一个窗体在根命名空间 `WindowsApplication1` 和命名空间 `Namespace1` 中，则您可以通过 `My.Forms.WindowsApplication1_Namespace1_Form1` 访问该窗体。  
  
 `My.Forms` 对象提供了对在启动时创建的应用程序主窗体实例的访问。  对于所有其他窗体，`My.Forms` 对象创建一个新的窗体实例（在它被访问时），并存储该实例。  访问该属性的后续尝试将返回此窗体实例。  
  
 您可以通过将 `Nothing` 赋予该窗体的属性来释放窗体。  属性 setter 调用窗体的 <xref:System.Windows.Forms.Form.Close%2A> 方法，然后将 `Nothing` 赋予存储的值。  如果向属性赋予 `Nothing` 以外的任何值，setter 将引发 <xref:System.ArgumentException> 异常。  
  
 您可以通过使用 `Is` 或 `IsNot` 运算符来测试 `My.Forms` 对象的属性是否存储了窗体的实例，  并可以使用这些运算符来检查此属性的值是否为 `Nothing`。  
  
> [!NOTE]
>  通常，`Is` 或 `IsNot` 运算符必须读取此属性的值以执行比较。  但是，如果属性当前存储的值为 `Nothing`，该属性将创建窗体的一个新实例，然后返回该实例。  不过，Visual Basic 编译器将特殊对待 `My.Forms` 对象的属性，并且允许 `Is` 或 `IsNot` 运算符检查属性的状态而不改变其值。  
  
## 示例  
 此示例更改默认 `SidebarMenu` 窗体的标题。  
  
 [!code-vb[VbVbalrMyForms#2](../../../visual-basic/language-reference/objects/codesnippet/VisualBasic/my-forms-object_1.vb)]  
  
 若要使此示例正常工作，项目必须具有名为 `SidebarMenu` 的窗体。  有关更多信息，请参见 [How to: Add Windows Forms to a Project](http://msdn.microsoft.com/zh-cn/3d7bb25f-fd90-47cf-9378-fa0d764686c1)。  
  
 这些代码将只能在 Windows 应用程序项目中正常运行。  
  
## 要求  
  
### 按项目类型列出的可用性  
  
|||  
|-|-|  
|项目类型|是否可用|  
|Windows 应用程序|**是**|  
|类库|否|  
|控制台应用程序|否|  
|Windows 控件库|否|  
|Web 控件库|否|  
|Windows 服务|否|  
|网站|否|  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A>   
 <xref:System.Windows.Forms.Form>   
 <xref:System.Windows.Forms.Form.Close%2A>   
 [对象](../../../visual-basic/language-reference/objects/index.md)   
 [How to: Add Windows Forms to a Project](http://msdn.microsoft.com/zh-cn/3d7bb25f-fd90-47cf-9378-fa0d764686c1)   
 [Is 运算符](../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot 运算符](../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [访问应用程序窗体](../../../visual-basic/developing-apps/programming/accessing-application-forms.md)