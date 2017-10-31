---
title: virtualCERCall MDA
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MDAs (managed debugging assistants), CER calls
- virtualCERCall MDA
- virtual CER calls
- constrained execution regions
- CER calls
- managed debugging assistants (MDAs), CER calls
ms.assetid: 1eb18c7a-f5e0-443f-80fb-67bfbb047da2
caps.latest.revision: 13
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 334900cbcc04cb1883b93a6bac17309add9ec159
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="virtualcercall-mda"></a>virtualCERCall MDA
`virtualCERCall` 托管调试助手 (MDA) 作为警告被激活，指示某个受约束的执行区域 (CER) 调用关系图中的调用站点引用了虚拟目标，即对非最终虚拟方法的虚拟调用或使用接口的调用。 公共语言运行时 (CLR) 无法只凭中间语言和元数据分析预测这些调用的目标方法。 因此无法将调用树准备为 CER 关系图的一部分，且无法阻止该子树中的线程中止。 此 MDA 警告以下情况：一旦计算调用目标所需的附加信息在运行时已知，则可能需要使用对 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A> 方法的显式调用来扩展 CER。  
  
## <a name="symptoms"></a>症状  
 线程中止或应用程序域卸载时 CER 不运行。  
  
## <a name="cause"></a>原因  
 CER 包含对无法自动准备的虚拟方法的调用。  
  
## <a name="resolution"></a>解决方法  
 为该虚拟方法调用 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>。  
  
## <a name="effect-on-the-runtime"></a>对运行时的影响  
 此 MDA 对 CLR 无任何影响。  
  
## <a name="output"></a>输出  
  
```  
Method 'MethodWithCer', while executing within a constrained execution region, makes a call  
at IL offset 0x0024 to 'VirtualMethod', which is virtual and cannot be prepared automatically  
at compile time. The caller must ensure this method is prepared explicitly at  
runtime before entering the constrained execution region.  
method name="VirtualMethod"  
declaringType name="VirtualCERCall+MyClass"  
  declaringModule name="mda"  
    callsite name="MethodWithCer" offset="0x0024"  
```  
  
## <a name="configuration"></a>配置  
  
```xml  
<mdaConfig>  
  <assistants>  
    < VirtualCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>示例  
  
```  
class MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    virtual void VirtualMethod()  
    {  
        ...  
    }  
}  
  
class MyDerivedClass : MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    override void VirtualMethod()  
    {  
        ...  
    }  
}  
  
void MethodWithCer(MyClass object)  
{  
    RuntimeHelpers.PrepareConstrainedRegions();  
    try  
    {  
        ...  
    }  
    finally  
    {  
        // Start of the CER.  
  
        // Cannot tell at analysis time whether object is a MyClass  
        // or a MyDerivedClass, so we do not know which version of   
        // VirtualMethod we are going to call.  
        object.VirtualMethod();  
    }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [使用托管调试助手诊断错误](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [互操作封送处理](../../../docs/framework/interop/interop-marshaling.md)

