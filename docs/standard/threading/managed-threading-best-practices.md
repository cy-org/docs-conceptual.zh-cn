---
title: "Managed Threading Best Practices | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "threading [.NET Framework], design guidelines"
  - "threading [.NET Framework], best practices"
  - "managed threading"
ms.assetid: e51988e7-7f4b-4646-a06d-1416cee8d557
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Managed Threading Best Practices
多线程编程需要在编程时倍加注意。  对于多数任务，通过将执行请求以线程池线程的方式排队，可以降低复杂性。  本主题将探讨更复杂的情形，比如协调多个线程的工作或处理造成阻止的线程。  
  
> [!NOTE]
>  在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]中，任务并行库和 PLINQ 提供了 API，可降低多线程编程的复杂性和风险。  有关详细信息，请参阅[Parallel Programming](../../../docs/standard/parallel-programming/index.md)。  
  
## 死锁和争用条件  
 多线程编程解决了吞吐量和响应性问题，但引入此功能会带来新的问题：死锁和争用条件。  
  
### 死锁  
 当两个线程中的每一个线程都在尝试锁定另外一个线程已锁定的资源时，就会发生死锁。  其中任何一个线程都不能继续执行。  
  
 托管线程处理类的许多方法都提供了超时设定，可帮您检测到死锁。  例如，下面的代码尝试获取对当前实例的锁定。  如果在 300 毫秒内未能锁定，<xref:System.Threading.Monitor.TryEnter%2A?displayProperty=fullName> 将返回 **false**。  
  
```vb  
If Monitor.TryEnter(lockObject, 300) Then  
    Try  
        ' Place code protected by the Monitor here.  
    Finally  
        Monitor.Exit(Me)  
    End Try  
Else  
    ' Code to execute if the attempt times out.  
End If  
```  
  
```csharp  
if (Monitor.TryEnter(lockObject, 300)) {  
    try {  
        // Place code protected by the Monitor here.  
    }  
    finally {  
        Monitor.Exit(this);  
    }  
}  
else {  
    // Code to execute if the attempt times out.  
}  
```  
  
### 争用条件  
 争用条件是当程序的结果取决于两个或更多个线程中的哪一个先到达某一特定代码块时出现的一种 Bug。  多次运行程序将产生不同的结果，而且给定的任何一次运行的结果都不可预知。  
  
 争用条件的一个简单例子是递增一个字段。  假定某个类有一个私有 **static** 字段（在 Visual Basic 中为 **Shared**），每创建该类的一个实例时它都递增一次，使用的代码是 `objCt++;` \(C\#\) 或 `objCt += 1` \(Visual Basic\)。  此操作要求将 `objCt` 中的值加载到一个寄存器中，使该值递增，然后将其存储到 `objCt` 中。  
  
 在多线程应用程序中，一个已加载并递增该值的线程可能会被另一个线程抢先，抢先的线程执行全部的三个步骤；当第一个线程继续执行并存储其值时，它覆盖 `objCt`，但不考虑该值在它暂停执行期间已更改这一事实。  
  
 这种特殊的争用条件通过使用 <xref:System.Threading.Interlocked> 类的方法（如 <xref:System.Threading.Interlocked.Increment%2A?displayProperty=fullName>）即可轻松避免。  若要了解在多个线程间同步数据的其他技巧，请参见[为多线程处理同步数据](../../../docs/standard/threading/synchronizing-data-for-multithreading.md)。  
  
 争用条件也可能会在同步多个线程的活动时发生。  编写每一行代码，都必须考虑出现以下特殊情况时会发生什么情况，这里的特殊情况是指：一个线程在执行该行代码（或构成该行的任何机器指令）前，其他线程抢先执行了该代码。  
  
## 处理器数目  
 如今，大多数计算机，甚至平板电脑和手机等小型设备，都具有多个处理器（也称为核心）。  如果您知道您正在开发的软件也将在单处理器计算机上运行，您应了解多线程可解决单处理器计算机和多处理器计算机的诸多问题。  
  
### 多处理器计算机  
 多线程编程提供了更大的吞吐量。  十个处理器可以完成一个处理器的十倍的工作量，不过，只有将任务分开并让十个处理器同时工作才行；线程为划分任务并利用额外的处理能力提供了一种方便的办法。  如果在多处理器计算机上使用多线程编程，那么：  
  
-   可以并发执行的线程的数目取决于处理器的数目。  
  
-   后台线程只有在正在执行的前台线程的数目小于处理器的数目时才执行。  
  
-   对一个线程调用 <xref:System.Threading.Thread.Start%2A?displayProperty=fullName> 方法时，该线程可能会，也可能不会立即执行，具体取决于处理器的数目以及当前等待执行的线程的数目。  
  
-   争用条件不仅可能因为线程被意外抢占而发生，还可能因为在不同的处理器上执行的两个线程在抢用同一代码块而发生。  
  
### 单处理器计算机  
 多线程编程为计算机用户提供了更好的响应能力，并且使用空闲时间处理后台任务。  如果在单处理器计算机上使用多线程编程，那么：  
  
-   在任何时刻都只有一个线程在运行。  
  
-   后台线程仅在主用户线程空闲时才执行。  连续运行的前台线程将使后台线程得不到处理器时间。  
  
-   对一个线程调用 <xref:System.Threading.Thread.Start%2A?displayProperty=fullName> 方法时，该线程只有等到当前线程结束或被操作系统抢占后才会执行。  
  
-   出现争用条件的原因通常是，程序员未预见到一个线程可能会在一个难以控制的时刻被抢占这一事实，有时就会出现另一线程抢先使用代码块这种情况。  
  
## 静态成员和静态构造函数  
 在类的类构造函数（C\# 中的 `static` 构造函数、Visual Basic 中的 `Shared Sub New`）完成运行之前，该类不会初始化。  为防止对未初始化的类型执行代码，在类构造函数完成运行之前，公共语言运行时会禁止从其他线程到类的 `static` 成员（Visual Basic 中的 `Shared` 成员）的所有调用。  
  
 例如，如果某个类构造函数启动了一个新线程，并且该线程过程调用了该类的 `static` 成员，则在该类构造函数完成之前，会一直禁止新线程。  
  
 以上情况适用于可拥有 `static` 构造函数的任意类型。  
  
## 一般性建议  
 使用多线程时要考虑以下准则：  
  
-   不要使用 <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> 终止其他线程。  对另一个线程调用 **Abort** 无异于引发该线程的异常，也不知道该线程已处理到哪个位置。  
  
-   不要使用 <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> 和 <xref:System.Threading.Thread.Resume%2A?displayProperty=fullName> 同步多个线程的活动。  请使用 <xref:System.Threading.Mutex>、<xref:System.Threading.ManualResetEvent>、<xref:System.Threading.AutoResetEvent> 和 <xref:System.Threading.Monitor>。  
  
-   不要从主程序中控制辅助线程的执行（如使用事件），  而应在设计程序时让辅助线程负责等待任务，执行任务，并在完成时通知程序的其他部分。  如果不阻止辅助线程，请考虑使用线程池线程。  如果阻止辅助线程，<xref:System.Threading.Monitor.PulseAll%2A?displayProperty=fullName> 会很有帮助。  
  
-   不要将类型用作锁定对象。  例如，避免在 C\# 中使用 `lock(typeof(X))` 代码，或在 Visual Basic 中使用 `SyncLock(GetType(X))` 代码，或将 <xref:System.Threading.Monitor.Enter%2A?displayProperty=fullName> 和 <xref:System.Type> 对象一起使用。  对于给定类型，每个应用程序域只有一个 <xref:System.Type?displayProperty=fullName> 实例。  如果您锁定的对象的类型是 public，您的代码之外的代码也可锁定它，但会导致死锁。  有关其他信息，请参见[可靠性最佳做法](../../../docs/framework/performance/reliability-best-practices.md)。  
  
-   锁定实例时要谨慎，例如，C\# 中的 `lock(this)` 或 Visual Basic 中的 `SyncLock(Me)`。  如果您的应用程序中不属于该类型的其他代码锁定了该对象，则会发生死锁。  
  
-   一定要确保已进入监视器的线程始终离开该监视器，即使当线程在监视器中时发生异常也是如此。  C\# 的 [lock](../Topic/lock%20Statement%20\(C%23%20Reference\).md) 语句和 Visual Basic 的 [SyncLock](../../../ocs/visual-basic/language-reference/statements/synclock-statement.md) 语句可自动提供此行为，它们用一个 **finally** 块来确保调用 <xref:System.Threading.Monitor.Exit%2A?displayProperty=fullName>。  如果无法确保调用 **Exit**，请考虑将您的设计更改为使用 **Mutex**。  Mutex 在当前拥有它的线程终止后会自动释放。  
  
-   一定要针对那些需要不同资源的任务使用多线程，避免向单个资源指定多个线程。  例如，任何涉及 I\/O 的任务都会从其拥有其自己的线程这一点得到好处，因为此线程在 I\/O 操作期间将阻止，从而允许其他线程执行。  用户输入是另一种可从专用线程获益的资源。  在单处理器计算机上，涉及大量计算的任务可与用户输入和涉及 I\/O 的任务并存，但多个计算量大的任务将相互竞争。  
  
-   对于简单的状态更改，请考虑使用 <xref:System.Threading.Interlocked> 类的方法，而不是 `lock` 语句（在 Visual Basic 中为 `SyncLock`）。  `lock` 语句是一个优秀的通用工具，但是 <xref:System.Threading.Interlocked> 类为必须是原子性的更新提供了更好的性能。  如果没有争夺，它会在内部执行一个锁定前缀。  在查看代码时，请注意类似于以下示例所示的代码。  在第一个示例中，状态变量是递增的：  
  
    ```vb  
    SyncLock lockObject  
        myField += 1  
    End SyncLock  
    ```  
  
    ```csharp  
    lock(lockObject)   
    {  
        myField++;  
    }  
    ```  
  
     可以使用 <xref:System.Threading.Interlocked.Increment%2A> 方法代替 `lock` 语句，从而提高性能，如下所示：  
  
    ```vb  
    System.Threading.Interlocked.Increment(myField)  
    ```  
  
    ```csharp  
    System.Threading.Interlocked.Increment(myField);  
    ```  
  
    > [!NOTE]
    >  在 .NET Framework 2.0 版中，<xref:System.Threading.Interlocked.Add%2A> 方法提供增量大于 1 的原子更新。  
  
     在第二个示例中，仅当引用类型变量为 null 引用（在 Visual Basic 中为 `Nothing`）时，它才会被更新。  
  
    ```vb  
    If x Is Nothing Then  
        SyncLock lockObject  
            If x Is Nothing Then  
                x = y  
            End If  
        End SyncLock  
    End If  
    ```  
  
    ```csharp  
    if (x == null)  
    {  
        lock (lockObject)  
        {  
            if (x == null)  
            {  
                x = y;  
            }  
        }  
    }  
    ```  
  
     改用 <xref:System.Threading.Interlocked.CompareExchange%2A> 方法可以提高性能，如下所示：  
  
    ```vb  
    System.Threading.Interlocked.CompareExchange(x, y, Nothing)  
    ```  
  
    ```csharp  
    System.Threading.Interlocked.CompareExchange(ref x, y, null);  
    ```  
  
    > [!NOTE]
    >  在 .NET Framework 2.0 版中，<xref:System.Threading.Interlocked.CompareExchange%2A> 方法具有一个泛型重载，可用于对任何引用类型进行类型安全的替换。  
  
## 类库的建议  
 在为多线程编程设计类库时，请考虑以下准则：  
  
-   如果可能，请避免同步需求。  对于大量使用的代码更应如此。  例如，可以将一个算法调整为容忍争用情况，而不是完全消除争用情况。  不必要的同步会降低性能，并且可能导致出现死锁和争用情况。  
  
-   默认情况下使静态数据（在 Visual Basic 中为 `Shared`）是线程安全的。  
  
-   默认情况下不要使实例数据是线程安全的。  通过添加锁来创建线程安全的代码的做法会降低性能、加剧锁争夺，并且可能导致出现死锁。  在常见的应用程序模型中，某一时刻只有一个线程执行用户代码，这样可以使对线程安全的需求变为最小。  出于此原因，.NET Framework 类库默认情况下不是线程安全的。  
  
-   避免提供可更改静态状态的静态方法。  在常见的服务器方案中，静态状态在各个请求之间是共享的，这意味着多个线程可在同一时刻执行该代码。  这样就有可能出现线程错误。  请考虑使用一种设计模式，将数据封装到在各请求之间不共享的实例中。  此外，如果同步静态数据，更改状态的静态方法间的调用可导致死锁或冗余同步，从而降低性能。  
  
## 请参阅  
 [Threading](../../../docs/standard/threading/index.md)   
 [Threads and Threading](../../../docs/standard/threading/threads-and-threading.md)