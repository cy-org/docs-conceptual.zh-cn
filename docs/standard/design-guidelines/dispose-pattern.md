---
title: "释放模式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Dispose 方法"
  - "类库设计准则 [.NET Framework] Dispose 方法"
  - "类库设计准则 [.NET Framework] Finalize 方法"
  - "自定义 Dispose 方法名称"
  - "Finalize 方法"
ms.assetid: 31a6c13b-d6a2-492b-9a9f-e5238c983bcb
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 22
---
# 释放模式
所有程序都获取其执行过程的一个或多个系统资源，如内存、 系统句柄或数据库连接。 开发人员必须谨慎使用这种系统资源，因为它们必须具有已获得和使用后释放。  
  
 CLR 提供了对自动内存管理的支持。 托管内存 \(使用 C\# 运算符分配的内存 `new`\) 不需要显式释放。 将由垃圾回收器 \(GC\) 自动释放。 这使开发人员不再释放内存的繁琐和困难的任务，并已成为.NET Framework 所提供的前所未有的工作效率的主要原因之一。  
  
 遗憾的是，托管的内存是只是一个许多类型的系统资源。 非托管内存的资源仍需要显式释放和称为非托管资源。 GC 专门初衷并非用于管理此类非托管的资源，这意味着，负责管理非托管的资源存在于中的开发人员的手中。  
  
 CLR 提供了一些在释放非托管的资源的帮助。<xref:System.Object?displayProperty=fullName> 声明虚拟方法 <xref:System.Object.Finalize%2A> （也称为终结器），由 GC 之前调用对象的内存被 GC 将被回收，可以重写以释放非托管的资源。 重写终结器的类型称为可终结的类型。  
  
 尽管在某些方案中清理有效终结器，但它们具有两个明显的缺点︰  
  
-   GC 检测到某个对象符合回收条件时，被调用终结器。 发生这种情况在某个未确定的时间段内后不再需要该资源。 当开发人员可以或想要释放的资源和资源由终结器的实际发布时的时间之间的延迟可能会获得很多稀缺资源 （可以轻松地用完的资源） 的程序中或在该资源是代价高昂，以使保持在使用 （例如，较大的非托管的内存缓冲区） 的情况下，不能接受。  
  
-   当 CLR 需要调用终结器时，它必须推迟集合对象的内存，直至下一次舍入的垃圾回收 （集合之间运行的终结器）。 这意味着，该对象的内存 （和它引用的所有对象） 并不会释放的时间较长时间。  
  
 因此，仅依靠终结器可能不适合在许多情况下很重要，以处理稀缺资源时，尽可能快地回收非托管的资源时或在高性能方案中的终止添加开销的 GC 不适。  
  
 该框架还提供 <xref:System.IDisposable?displayProperty=fullName> 应实现，以提供开发人员不需要它们时，就立即释放非托管的资源的手动方法的接口。 它还提供了 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 方法可以告知 GC 对象手动释放的和不需要完成了，在这种情况下可以前面回收对象的内存。 类型实现 `IDisposable` 接口被称为可释放类型。  
  
 Dispose 模式旨在实现标准化的使用情况和终结器实现与 `IDisposable` 接口。  
  
 该模式的主要目的是减少的实现的复杂程度 <xref:System.Object.Finalize%2A> 和 <xref:System.IDisposable.Dispose%2A> 方法。 复杂性，是因为方法共享 （更高版本在一章中描述了这些差异） 的部分而不是所有代码路径。 此外，还有历史原因的某些元素，以便管理具有确定性的资源的语言支持的不断发展和相关的模式。  
  
 **✓ 执行** 在包含可释放类型的实例类型上实现基本的 Dispose 模式。 请参阅 [基本 Dispose 模式](#basic_pattern) 有关的基本模式的详细信息部分。  
  
 如果类型是负责其他可释放对象的生存期，开发人员需要一种方法中释放它们，太。 使用容器的 `Dispose` 方法是为了实现这一点的方便方法。  
  
 **✓ 执行** 实现基本的释放模式，并提供终结器类型保持资源需要显式释放和没有终结器。  
  
 例如，应在存储非托管的内存缓冲区的类型上实现此模式。[可终结类型](#finalizable_types) 部分讨论了与实现终结器相关的准则。  
  
 **✓ 请考虑** 实现基本的释放模式类本身不包含非托管资源，或者可释放的对象但很可能具有执行的子类型。  
  
 看下面的示例是 <xref:System.IO.Stream?displayProperty=fullName> 类。 虽然很不保留任何资源的抽象基类，但大部分其子类执行操作，正因为如此，它可实现此模式。  
  
<a name="basic_pattern"></a>   
## 基本的释放模式  
 该模式的基本实现涉及到实现 `System.IDisposable` 接口，并声明 `Dispose(bool)` 方法，实现之间共享的所有资源清理逻辑 `Dispose` 方法和可选的终结器。  
  
 下面的示例演示基本模式的简单实现︰  
  
```  
public class DisposableResourceHolder : IDisposable {  
  
    private SafeHandle resource; // handle to a resource  
  
    public DisposableResourceHolder(){  
        this.resource = ... // allocates the resource  
    }  
  
    public void Dispose(){  
        Dispose(true);  
        GC.SuppressFinalize(this);  
    }  
  
    protected virtual void Dispose(bool disposing){  
        if (disposing){  
            if (resource!= null) resource.Dispose();  
        }  
    }  
}  
```  
  
 布尔型参数 `disposing` 指示方法是否从调用 `IDisposable.Dispose` 实现或从终结器。`Dispose(bool)` 实现应检查参数，然后才能访问其他引用的对象 （例如，在前面的示例资源域）。 从调用方法时，只应访问此类对象 `IDisposable.Dispose` 实现 \(当 `disposing` 参数是否等于 true\)。 如果该方法从终结器调用 \(`disposing` 为 false\)，不应访问其他对象。 原因是不可预知的顺序终止对象，因此它们，或任何其依赖关系，可能已经完成。  
  
 此外，本部分适用于具有未实现 Dispose 模式的基本类。 如果您从已实现的模式的类继承的只需重写 `Dispose(bool)` 方法以提供更多资源的清理逻辑。  
  
 **✓ 执行** 声明受保护的虚拟 void `Dispose(bool disposing)` 方法来集中的所有逻辑相关的释放非托管的资源。  
  
 所有资源清理应该都出现在此方法。 从这两个终结器调用该方法与 `IDisposable.Dispose` 方法。 该参数将为 false，如果正在从在终结器内部调用。 它应该用于确保任何在终止期间运行的代码不能访问其他可终结对象。 下一节描述了实现终结器的详细信息。  
  
```  
protected virtual void Dispose(bool disposing){  
    if (disposing){  
        if (resource!= null) resource.Dispose();  
    }  
}  
```  
  
 **✓ 执行** 实现 `IDisposable` 接口只需调用 `Dispose(true)` 跟 `GC.SuppressFinalize(this)`。  
  
 对调用 `SuppressFinalize` 应仅发生如果 `Dispose(true)` 成功执行。  
  
```  
public void Dispose(){  
    Dispose(true);  
    GC.SuppressFinalize(this);  
}  
```  
  
 **X 不** 进行的无参数 `Dispose` 虚拟方法。  
  
 `Dispose(bool)` 方法中，是应由子类中被重写。  
  
```  
// bad design  
public class DisposableResourceHolder : IDisposable {  
    public virtual void Dispose(){ ... }  
    protected virtual void Dispose(bool disposing){ ... }  
}  
  
// good design  
public class DisposableResourceHolder : IDisposable {  
    public void Dispose(){ ... }  
    protected virtual void Dispose(bool disposing){ ... }  
}  
```  
  
 **X 不** 声明的任何重载 `Dispose` 以外的其他方法 `Dispose()` 和 `Dispose(bool)`。  
  
 `Dispose` 应考虑以帮助对这种模式，并避免混淆之间实施者、 用户和编译器的保留的字。 某些语言中可以选择自动在某些类型上实现此模式。  
  
 **✓ 执行** 允许 `Dispose(bool)` 不止一次调用方法。 该方法可以选择在第一次调用后不执行任何操作。  
  
```  
public class DisposableResourceHolder : IDisposable {  
  
    bool disposed = false;  
  
    protected virtual void Dispose(bool disposing){  
        if(disposed) return;  
        // cleanup  
        ...  
        disposed = true;  
    }  
}  
```  
  
 **X 避免** 从引发异常 `Dispose(bool)` 在严重情况下，其中包含进程已被损坏除外 （泄漏了，不一致的共享的状态，等等。）。  
  
 用户期望调用 `Dispose` 将不会引发异常。  
  
 如果 `Dispose` 无法引发了异常，将不执行进一步的 finally 块清理逻辑。 若要解决此问题，用户需要将包装对每个调用 `Dispose` \(在 finally 块 ！\) 在 try 块中，从而产生非常复杂的清理处理程序。 如果执行 `Dispose(bool disposing)` 方法中，永远不会引发了异常，如果释放为 false。 如果终结器上下文中执行，则执行此操作将终止该进程。  
  
 **✓ 执行** 引发 <xref:System.ObjectDisposedException> 从该对象已释放的之后不能使用的任何成员。  
  
```  
public class DisposableResourceHolder : IDisposable {  
    bool disposed = false;  
    SafeHandle resource; // handle to a resource  
  
    public void DoSomething(){  
           if(disposed) throw new ObjectDisposedException(...);  
        // now call some native methods using the resource   
            ...  
    }  
    protected virtual void Dispose(bool disposing){  
        if(disposed) return;  
        // cleanup  
        ...  
        disposed = true;  
    }  
}  
```  
  
 **✓ 请考虑** 提供方法 `Close()`, ，除了 `Dispose()`, ，如果关闭是在区域中的标准术语。  
  
 在时这样做，务必使 `Close` 实现相同 `Dispose` 并考虑实现 `IDisposable.Dispose` 方法显式。  
  
```  
public class Stream : IDisposable {  
    IDisposable.Dispose(){  
        Close();  
    }  
    public void Close(){  
        Dispose(true);  
        GC.SuppressFinalize(this);  
    }  
}  
```  
  
<a name="finalizable_types"></a>   
## 可终结的类型  
 可终结的类型都是通过重写终结器，并提供终结代码方式中的扩展了基本的释放模式的类型 `Dispose(bool)` 方法。  
  
 终结器都是系统的正确，实现还是相当困难的主要是系统的因为您不能假设 （通常情况下有效） 有关的状态在其执行过程。 应仔细考虑采取以下准则。  
  
 请注意，某些准则应用不只是为 `Finalize` 方法，但对任何代码从一个终结器调用。 对于基本释放先前所定义的模式，这意味着内执行的逻辑 `Dispose(bool disposing)` 时 `disposing` 参数为 false。  
  
 如果已类的基类是可终止，并实现基本的释放模式，不应重写 `Finalize` 再次。 相反，应只覆盖 `Dispose(bool)` 方法以提供更多资源的清理逻辑。  
  
 下面的代码演示可终结的类的一个示例︰  
  
```  
public class ComplexResourceHolder : IDisposable {  
  
    private IntPtr buffer; // unmanaged memory buffer  
    private SafeHandle resource; // disposable handle to a resource  
  
    public ComplexResourceHolder(){  
        this.buffer = ... // allocates memory  
        this.resource = ... // allocates the resource  
    }  
  
    protected virtual void Dispose(bool disposing){  
            ReleaseBuffer(buffer); // release unmanaged memory  
        if (disposing){ // release other disposable objects  
            if (resource!= null) resource.Dispose();  
        }  
    }  
  
    ~ ComplexResourceHolder(){  
        Dispose(false);  
    }  
  
    public void Dispose(){  
        Dispose(true);  
        GC.SuppressFinalize(this);  
    }  
}  
```  
  
 **X 避免** 进行类型可终止。  
  
 请仔细考虑在其中您认为终结器所需的任何用例。 还有一片方式有终结器，从性能和代码复杂性角度来看的实例相关联的成本。 更喜欢使用资源的包装，如 <xref:System.Runtime.InteropServices.SafeHandle> 封装非托管的资源，如果可能，在这种情况下终结器由于不必要的包装是否负责其自己的资源清理。  
  
 **X 不** 使成为可终结的值类型。  
  
 只有引用类型实际获取最终确定下来由 CLR，并因此将忽略任何尝试将一个终结器放在值类型。 C\# 和 c \+ \+ 编译器执行此规则。  
  
 **✓ 执行** 使类型成为可终结，如果类型为负责释放不具有其自己的终结器非托管的资源。  
  
 在实现终结器时，只需调用 `Dispose(false)` 内的所有资源清理逻辑，随时随地 `Dispose(bool disposing)` 方法。  
  
```  
public class ComplexResourceHolder : IDisposable {  
  
    ~ ComplexResourceHolder(){  
        Dispose(false);  
    }  
  
    protected virtual void Dispose(bool disposing){  
        ...  
    }  
}  
```  
  
 **✓ 执行** 在每个可终结的类型上实现基本的 Dispose 模式。  
  
 这使类型的用户可以明确地执行终结器所负责的这些相同的资源的确定性清理。  
  
 **X 不** 访问在终结器代码路径中，任何可终结对象，因为高安全风险，它们将已被终结。  
  
 例如，具有对另一个可终结对象 B 的引用可终结对象 A 不能可靠地使用 B 中 A 的终结器中，反之亦然。 （缺少关键终止了弱排序保证） 随机顺序调用终结器。  
  
 另外，请注意，在静态变量中存储的对象将就会收集在特定时间点在应用程序域卸载期间或在退出进程。 访问指的是一个可终结的对象 （或调用静态方法可能会使用存储在静态变量的值） 的静态变量可能不安全的 if <xref:System.Environment.HasShutdownStarted%2A?displayProperty=fullName> ，则返回 true。  
  
 **✓ 执行** 使您 `Finalize` 受保护的方法。  
  
 C\#、 c \+ \+ 和 VB.NET 开发人员不需要担心这一点，因为编译器强制执行这一准则可帮助。  
  
 **X 不** 让的异常转义和终结器逻辑，除了严重系统故障。  
  
 如果从一个终结器引发异常，CLR 将关闭 （截止到.NET Framework 2.0 版\)，整个过程防止执行和控制的方式被释放的资源的其他终结器。  
  
 **✓ 请考虑** 创建和使用关键可终结对象 \(具有包含对类型层次结构的类型 <xref:System.Runtime.ConstrainedExecution.CriticalFinalizerObject>\) 的情况下在其中一个终结器绝对必须执行即使在遇到时强制应用程序域卸载并将线程终止。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName>   
 <xref:System.Object.Finalize%2A?displayProperty=fullName>   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [常见设计模式](../../../docs/standard/design-guidelines/common-design-patterns.md)   
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)