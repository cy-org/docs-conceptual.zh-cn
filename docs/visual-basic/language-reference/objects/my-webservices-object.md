---
title: "My.WebServices 对象 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "My.WebServices"
  - "My.MyProject.WebServices"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.WebServices 对象"
ms.assetid: f188dc05-2c75-41b6-bb68-122d1c3110a2
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# My.WebServices 对象
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

提供一些属性，它们用于创建和访问当前项目引用的每个 XML Web services 的单个实例。  
  
## 备注  
 `My.WebServices` 对象提供了当前项目引用的每个 Web 服务的实例。  每个实例根据需要进行实例化。  您可以通过 `My.WebServices` 对象的属性访问这些 Web 服务。  该属性与它所访问的 Web 服务同名。  从 <xref:System.Web.Services.Protocols.SoapHttpClientProtocol> 继承的任何类都是 Web 服务。  有关向项目中添加 Web 服务的信息，请参见 [访问应用程序 Web 服务](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)。  
  
 `My.WebServices` 对象只公开与当前项目相关联的 Web 服务。  它不提供对引用的 DLL 中声明的 Web 服务的访问。  若要访问 DLL 提供的 Web 服务，必须使用 Web 服务的限定名称，格式为 *Dll 名称*.*Web 服务名称*。  有关更多信息，请参见[访问应用程序 Web 服务](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)。  
  
 该对象及其属性对于 Web 应用程序不可用。  
  
## 属性  
 `My.WebServices` 对象的每个属性都提供对当前项目所引用的 Web 服务的实例的访问。  属性的名称与该属性访问的 Web 服务的名称相同，并且属性类型与 Web 服务的类型相同。  
  
> [!NOTE]
>  如果发生名称冲突，则用于访问 Web 服务的属性名称将为*根命名空间*\_*命名空间*\_*服务名称*。  例如，请考虑两个名为 `Service1` 的 Web 服务。  如果其中一个服务位于根命名空间 `WindowsApplication1` 和命名空间 `Namespace1` 中，则可以使用 `My.WebServices.WindowsApplication1_Namespace1_Service1` 访问该服务。  
  
 当首次访问 `My.WebServices` 对象的其中一个属性时，它将创建一个新的 Web 服务实例，并存储该实例。  对该属性的后续访问都将返回 Web 服务的该实例。  
  
 可以通过将 `Nothing` 赋予 Web 服务的属性来释放该 Web 服务。  属性 setter 将 `Nothing` 赋予已存储的值。  如果向属性赋予 `Nothing` 以外的任何值，setter 将引发 <xref:System.ArgumentException> 异常。  
  
 可以使用 `Is` 或 `IsNot` 运算符测试 `My.WebServices` 对象的属性是否存储了 Web 服务的实例，  并可以使用这些运算符来检查此属性的值是否为 `Nothing`。  
  
> [!NOTE]
>  通常，`Is` 或 `IsNot` 运算符必须读取此属性的值以执行比较。  但是，如果属性当前存储了 `Nothing`，则它将创建一个新的 Web 服务实例，然后返回该实例。  不过，Visual Basic 编译器将特殊对待 `My.WebServices` 对象的属性，并且允许 `Is` 或 `IsNot` 运算符检查属性的状态而不改变其值。  
  
## 示例  
 此示例调用 `TemperatureConverter` XML Web services 的 `FahrenheitToCelsius` 方法，然后返回结果。  
  
 [!code-vb[VbVbalrMyWebService#1](../../../visual-basic/language-reference/objects/codesnippet/VisualBasic/my-webservices-object_1.vb)]  
  
 为使此示例运行，项目必须引用一个名为 `Converter` 的 Web 服务，而且该 Web 服务必须公开 `ConvertTemperature` 方法。  有关更多信息，请参见[访问应用程序 Web 服务](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)。  
  
 这段代码在 Web 应用程序项目中无法运行。  
  
## 要求  
  
### 按项目类型列出的可用性  
  
|||  
|-|-|  
|项目类型|是否可用|  
|Windows 应用程序|**是**|  
|类库|**是**|  
|控制台应用程序|**是**|  
|Windows 控件库|**是**|  
|Web 控件库|**是**|  
|Windows 服务|**是**|  
|网站|否|  
  
## 请参阅  
 <xref:System.Web.Services.Protocols.SoapHttpClientProtocol>   
 <xref:System.ArgumentException>   
 [访问应用程序 Web 服务](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)