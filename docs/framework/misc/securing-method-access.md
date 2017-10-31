---
title: "保护方法访问 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "代码安全性, 方法访问"
  - "方法访问安全性"
  - "安全编码, 方法访问"
  - "安全性 [.NET Framework], 方法访问"
ms.assetid: f7c2d6ec-3b18-4e0e-9991-acd97189d818
caps.latest.revision: 16
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# 保护方法访问
某些方法可能不适用于允许任意不受信任的代码进行调用。 此类方法会带来几种风险：方法可能会提供一些受限制的信息；它可能信任传递给它的任何信息；它可能不会对参数执行错误检查；如果使用错误的参数，它还可能出现故障或执行某些有害操作。 应该注意这些情况，并采取措施以帮助保护这类方法。  
  
 在某些情况下，可能需要限制并不打算用于公共用途但仍须为公共方法的方法。 例如，可能有一个需在你自己的 DLL 间调用（从而必须为公共接口）的接口，但你不希望将其以公共方式公开，以防止客户使用它，或防止恶意代码利用入口点进入组件中。 限制不打算用于公共用途（但必须为公共方法）的方法的另一个常见理由是：为了避免不得不记录和支持可能是内部接口的接口。  
  
> [!CAUTION]
>  代码访问安全性和部分受信任的代码  
>   
>  .NET Framework 提供一种机制，对在相同应用程序中运行的不同代码强制实施不同的信任级别，该机制称为代码访问安全性 \(CAS\)。  .NET Framework 中的代码访问安全性不应用作部分受信任的代码（特别是未知来源的代码）的安全边界。 建议在未实施其他安全措施的情况下，不要加载和执行未知来源的代码。  
>   
>  此策略适用于 .NET Framework 的所有版本，但不适用于 Silverlight 中所含的 .NET Framework。  
  
 托管代码提供几种方法来限制方法访问：  
  
-   如果可以信任类、程序集或派生类，则限制它们的可访问性的范围。 这是限制方法访问的最简单的方法。 请注意，派生类的可信度通常可低于其从中派生的类，尽管在某些情况下它们共享父类的标识。 特别注意，不要从关键字 **protected** 而作出推断，因为安全上下文中并不一定使用了它。  
  
-   限制对指定标识的调用方的方法访问：标识实质上就是你选择的任何特定[证据](http://msdn.microsoft.com/zh-cn/64ceb7c8-a0b4-46c4-97dc-6c22da0539da)（强名称、发布者、区域等等）。  
  
-   限制对具有你选择的任何权限的调用方的方法访问。  
  
 同样，声明性安全使你可以控制类的继承。 可以使用 **InheritanceDemand** 来执行以下操作：  
  
-   要求派生类具有指定的标识或权限。  
  
-   要求重写特定方法的派生类具有指定的标识或权限。  
  
 下面的示例演示如何通过要求使用特定强名称对调用方进行签名来帮助保护具有有限访问权限的公共类。 此示例使用带有 **Demand** 强名称的 <xref:System.Security.Permissions.StrongNameIdentityPermissionAttribute>。 有关如何使用强名称对程序集进行签名的基于任务的信息，请参阅[创建和使用具有强名称的程序集](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)。  
  
```vb  
<StrongNameIdentityPermissionAttribute(SecurityAction.Demand, PublicKey := "…hex…", Name := "App1", Version := "0.0.0.0")>  _ Public Class Class1 End Class  
  
```  
  
```csharp  
[StrongNameIdentityPermissionAttribute(SecurityAction.Demand, PublicKey="…hex…", Name="App1", Version="0.0.0.0")] public class Class1 { }   
```  
  
## 防止不受信任的代码使用类和成员  
 使用本节中所示的声明来防止部分受信任的代码使用特定的类、方法以及属性和事件。 将这些声明应用到类，即可对类的所有方法、属性和事件应用保护；但请注意，字段访问不受声明性安全影响。 也请注意，链接要求仅帮助不受直接调用方的攻击，可能仍会受到引诱攻击。  
  
> [!NOTE]
>  [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 中引入了新的透明度模型。[安全透明的代码，级别 2](../../../docs/framework/misc/security-transparent-code-level-2.md) 模型用 <xref:System.Security.SecurityCriticalAttribute> 特性标识安全代码。 安全关键代码需要调用方和继承者均完全受信任。 在早期 .NET Framework 版本中的代码访问安全性规则下运行的程序集可以调用级别 2 程序集。 在这种情况下，安全关键属性将被视为完全信任的链接要求。  
  
 在具有强名称的程序集中，[LinkDemand](../../../docs/framework/misc/link-demands.md) 被应用于其中所有可通过公共方式访问的方法、属性和事件，以将它们限制为仅可由完全受信任的调用方使用。 若要禁用此功能，必须应用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 特性。 因此，仅未签名的程序集或具有此特性的程序集需要显式标记类以排除不受信任调用方；可以使用这些声明来标记其中并不打算用于不受信任的调用方的类型子集。  
  
 下面的示例说明如何防止不受信任的代码使用类和成员。  
  
 对于公共非密封类：  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name := "FullTrust"), _ System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _ Public Class CanDeriveFromMe End Class  
  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")] [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")] public class CanDeriveFromMe { }  
```  
  
 对于公共密封类：  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _ NotInheritable Public Class CannotDeriveFromMe End Class  
  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")] public sealed class CannotDeriveFromMe { }  
```  
  
 对于公共抽象类：  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name := "FullTrust"), _ System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _ MustInherit Public Class CannotCreateInstanceOfMe_CanCastToMe End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")] [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")] public abstract class CannotCreateInstanceOfMe_CanCastToMe{}  
```  
  
 对于公共虚拟函数：  
  
```vb  
Class Base1 <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _ Public Overridable Sub CanOverrideOrCallMe() End Sub 'CanOverrideOrCallMe End Class 'Base1  
```  
  
```csharp  
class Base1 { [System.Security.Permissions.PermissionSetAttribute( System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")] [System.Security.Permissions.PermissionSetAttribute( System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")] public virtual void CanOverrideOrCallMe() {} }  
```  
  
 对于公共抽象函数：  
  
```vb  
MustInherit Class Base2 <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _ Public Sub MustOverrideMe() End Sub End Class 'Base2  
```  
  
```csharp  
abstract class Base2{ [System.Security.Permissions.PermissionSetAttribute( System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")] [System.Security.Permissions.PermissionSetAttribute( System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")] public abstract void MustOverrideMe(); }  
```  
  
 对于基类不要求完全信任的公共重写函数：  
  
```vb  
Class Derived Inherits Base1 <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.Demand, Name:="FullTrust")> _ Public Overrides Sub CanOverrideOrCallMe() MyBase.CanOverrideOrCallMe() End Sub 'CanOverrideOrCallMe End Class 'Derived  
```  
  
```csharp  
class Derived : Base1 { [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.Demand, Name="FullTrust")] public override void CanOverrideOrCallMe() { base.CanOverrideOrCallMe(); } }  
```  
  
 对于基类要求完全信任的公共重写函数：  
  
```vb  
Class Derived Inherits Base1 <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _ Public Overrides Sub CanOverrideOrCallMe() MyBase.CanOverrideOrCallMe() End Sub 'CanOverrideOrCallMe End Class 'Derived  
```  
  
```csharp  
class Derived : Base1 { [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")] public override void CanOverrideOrCallMe() { base.CanOverrideOrCallMe(); } }  
```  
  
 对于公共接口：  
  
```vb  
Public Interface ICanCastToMe <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust")> _ Sub CanImplementMe() End Interface 'ICanCastToMe <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust")> _ Class Implemented Implements ICanCastToMe Public Sub CanImplementMe() End Sub 'CanImplementMe  
```  
  
```csharp  
public interface ICanCastToMe { [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")] [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")] void CanImplementMe(); } [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")] [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")] class Implemented : ICanCastToMe { public void CanImplementMe() { } }  
```  
  
## Virtual Internal 重写或 Overloads Overridable Friend  
  
> [!NOTE]
>  本节警告将方法同时声明为 `virtual` 和 `internal` （Visual Basic 中为 `Overloads``Overridable``Friend`）时可能出现的安全问题。 此警告仅适用于 .NET framework 1.0 和 1.1 版，不适用于 2.0 版。  
  
 在 .NET framework 1.0 和 1.1 版中，确认你的代码对其他程序集不可用时，必须注意类型系统可访问性的细微差别。 声明为 **virtual** 和 **internal**（Visual Basic 中为 **Overloads Overridable Friend**）的方法可以重写父类的 vtable 条目，并且仅可从相同程序集内使用，因为该方法为内部方法。 但是，重写的可访问性由 **virtual** 关键字决定，并且只要代码有权访问类本身，就可以从另一个程序集进行重写。 如果重写的可能性存在问题，请使用声明性安全来解决该问题，或删除 **virtual** 关键字（如果它不是绝对必需的）。  
  
 请注意，即使语言编译器通过编译错误防止这些重写，使用其他编译器编写的代码也可能发生重写。  
  
## 请参阅  
 [代码安全维护指南](../../../docs/standard/security/secure-coding-guidelines.md)