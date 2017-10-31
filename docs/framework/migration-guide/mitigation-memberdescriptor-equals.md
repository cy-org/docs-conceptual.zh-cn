---
title: "缓解：MemberDescriptor.Equals"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf3735f0-0dd4-4bef-b4b0-575264e10f39
caps.latest.revision: 7
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 4989d3c2611b500063158955f102931902e1ab32
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-memberdescriptorequals"></a>缓解：MemberDescriptor.Equals
自面向 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 的应用起，<xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=fullName> 方法的实现已更改。 由于 `System.ComponentModel.EventDescriptor.Equals` 和 `System.ComponentModel.PropertyDescriptor.Equals` 方法继承基类实现代码，因此这一更改还会影响这些方法。  
  
 在面向低于 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 的 NET Framework 版本的应用中，<xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=fullName> 方法的部分相等性测试误将一个对象的 <xref:System.ComponentModel.MemberDescriptor.Category%2A?displayProperty=fullName> 属性与另一个对象的 <xref:System.ComponentModel.MemberDescriptor.Description%2A?displayProperty=fullName> 属性进行比较。 自面向 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 的应用起，<xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=fullName> 方法比较两个对象的 <xref:System.ComponentModel.MemberDescriptor.Description%2A?displayProperty=fullName> 属性。  
  
## <a name="impact"></a>影响  
 此更改正确实现了 <xref:System.ComponentModel.MemberDescriptor?displayProperty=fullName> 对象的相等性测试，造成的影响应该是最少的。  
  
## <a name="mitigation"></a>缓解操作  
 如果应用面向 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 或更高版本的 .NET Framework，并且依赖于有时在成员描述符相等时返回 `false` 的 <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=fullName> 方法，有两种解决方法可用：  
  
-   可以在 app.config 文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 部分中添加下面的代码行，从而选择禁用此更改，而无需更改源代码：  
  
    ```xml  
    <runtime>  
        <AppContextSwitchOverrides value = "Switch.System.MemberDescriptorEqualsReturnsFalseIfEquivalent=true" />  
     </runtime>  
    ```  
  
-   可通过在调用 <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=fullName> 方法后手动比较 <xref:System.ComponentModel.MemberDescriptor.Category%2A?displayProperty=fullName> 和 <xref:System.ComponentModel.MemberDescriptor.Description%2A?displayProperty=fullName> 属性，将源代码修改为还原旧行为，如以下代码片段所示。  
  
    ```csharp  
    if (memberDescriptor1.Equals(memberDescriptor2) &   
        memberDescriptor1.Description.Equals(memberDescriptor2.Category)) {  
          // Code to execute if true.  
    }  
    else {  
          // Code to execute if false.     
    }  
    ```  
  
    ```  
    If memberDescriptor1.Equals(memberDescriptor2) And   
        memberDescriptor1.Description.Equals(memberDescriptor2.Category)  
          // Code to execute if True.  
    Else  
          // Code to execute if False.     
    End If  
    ```  
  
 对于定位 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 及更低版本的应用程序，可以在 app.config 文件中添加下面的值，从而启用此更改：  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.MemberDescriptorEqualsReturnsFalseIfEquivalent=true />  
</runtime>  
```  
  
## <a name="see-also"></a>另请参阅  
 [重定目标更改](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-2.md)   
 [4.6.2 中的应用程序兼容性](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-2.md)

