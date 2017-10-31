---
title: "Attached and Detached Child Tasks | Microsoft Docs"
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
  - "tasks, child tasks"
ms.assetid: c95788bf-90a6-4e96-b7bc-58e36a228cc5
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Attached and Detached Child Tasks
*子任务*（或 *嵌套的任务*）是在被称为*父任务*的另一个任务的用户委托中创建的 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 实例。  可以分离或附加子任务。  *分的离子任务*是不依赖于其父级而执行的任务。  *附加子任务*是使用 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> 选项创建的嵌套任务，该选项的父级不显式或默认禁止其被附加。  一个任务可以创建任意数量的附加和分离子任务，这仅受系统资源限制。  
  
 下表列出了两种子任务之间的基本差异。  
  
|类别|分离子任务|附加子任务|  
|--------|-----------|-----------|  
|父级将等待子任务完成。|No|是|  
|父级将传播由子任务引发的异常。|No|是|  
|父级的状态取决于子级的状态。|No|是|  
  
 在大多数情况下，我们建议你使用分离子任务，因为它们与其他任务之间的关系不太复杂。  这就是父任务内创建的任务会默认分离的原因，并且必须显式指定 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> 选项来创建附加子任务。  
  
## 分离子任务  
 尽管子任务是由父任务创建的，但在默认情况下，它独立于父任务。  在以下示例中，父任务创建了一个简单的子任务。  如果多次运行该示例的代码，你可能会注意到该示例的输出与所演示的输出不同，并且该输出可能在每次运行代码时，会发生更改。  发生这种情况的原因是父任务和子任务彼此独立执行；子任务是一个分离任务。  该示例仅等待父任务完成，并且子任务在控制台应用终止之前，可能无法执行或完成。  
  
 [!code-csharp[TPL_ChildTasks#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/nested1.cs#1)]
 [!code-vb[TPL_ChildTasks#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/nested1.vb#1)]  
  
 如果该子任务由 <xref:System.Threading.Tasks.Task%601> 对象，而不是 <xref:System.Threading.Tasks.Task> 对象表示，则你可以通过访问子任务的 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=fullName> 属性，确保父任务将等待子任务完成，即使该子任务是一个分离子任务。  <xref:System.Threading.Tasks.Task%601.Result%2A> 属性在其任务完成前会进行阻止，如以下示例所示。  
  
 [!code-csharp[TPL_ChildTasks#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/childtasks.cs#4)]
 [!code-vb[TPL_ChildTasks#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/tpl_childtasks.vb#4)]  
  
## 附加子任务  
 不同于分离子任务，附加子任务与父任务紧密同步。  可以通过使用任务创建语句中的 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> 选项，将之前示例中的分离子任务更改为附加子任务，如以下示例中所示。  在此代码中，附加子任务会在父任务之前完成。  因此，每次运行代码时，该示例的输出都是相同的。  
  
 [!code-csharp[TPL_ChildTasks#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/child1.cs#2)]
 [!code-vb[TPL_ChildTasks#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/child1.vb#2)]  
  
 可以使用附加子任务，创建异步操作的紧密同步关系图。  
  
 但是，子任务仅在其父任务不会阻止附加子任务时，才可以附加到其父任务。  通过在父任务类构造函数中指定 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName>选项或 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=fullName> 方法，父任务可以显式阻止子任务附加到其中。  如果父任务是通过调用 <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=fullName> 方法而创建的，则可以隐式阻止子任务附加到其中。  下面的示例阐释了这一点。  这与上述示例相同，除了该父任务是通过调用 <xref:System.Threading.Tasks.Task.Run%28System.Action%29?displayProperty=fullName> 方法，而不是 <xref:System.Threading.Tasks.TaskFactory.StartNew%28System.Action%29?displayProperty=fullName> 方法创建的。  因为子任务不能附加到其父任务，则该示例的输出是不可预知的。  因为 <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=fullName> 重载的默认任务创建选项包括 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName>，所以本示例在功能上等效于“分离子任务”部分中的第一个示例。  
  
 [!code-csharp[TPL_ChildTasks#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/child1a.cs#3)]
 [!code-vb[TPL_ChildTasks#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/child1a.vb#3)]  
  
## 子任务中的异常  
 如果分离子任务引发了异常，则该异常必须直接在父任务中进行观察和处理，正如任何非嵌套任务一样。  如果附加子任务引发了异常，则该异常会自动传播到父任务，并返回到等待或尝试访问任务的 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=fullName> 属性的线程。  因此，通过使用附加子任务，可以一次性处理调用线程上对 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=fullName> 的调用中的所有异常。  有关详细信息，请参阅[异常处理](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)。  
  
## 取消和子任务  
 任务取消需要彼此协作。  也就是说，若要取消任务，则每个附加或分离的子任务必须监视取消标记的状态。  如果想要通过使用一个取消请求来取消父任务及其所有子任务，则需要将作为参数的相同令牌传递到所有的任务，并在每个任务中提供逻辑，以对每个任务中的请求作出响应。  有关详细信息，请参阅[Task Cancellation](../../../docs/standard/parallel-programming/task-cancellation.md)和[How to: Cancel a Task and Its Children](../../../docs/standard/parallel-programming/how-to-cancel-a-task-and-its-children.md)。  
  
### 当父任务取消时  
 如果父任务在其子任务开始前取消了自身，则子任务将永远不会开始。  如果父任务在其子任务已开始后取消了自身，则子任务将完成运行，除非它自己具有取消逻辑。  有关详细信息，请参阅[Task Cancellation](../../../docs/standard/parallel-programming/task-cancellation.md)。  
  
### 当分离子任务取消时  
 如果分离子任务使用传递到父任务的相同标记取消自身，且父任务不会等待子任务，则不会传播异常，因为该异常将被视为良性协作取消。  此行为与任何顶级任务的行为相同。  
  
### 当附加子任务取消时  
 当附加子任务使用传递到其父任务的相同标记取消自身时，<xref:System.Threading.Tasks.TaskCanceledException> 将传播到 <xref:System.AggregateException> 中的联接线程。  必须等待父任务，以便你除了所有通过附加子任务的图形传播的错误异常之外，还可以处理所有良性异常。  
  
 有关详细信息，请参阅[异常处理](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)。  
  
## 阻止子任务附加到其父任务  
 由子任务引发的未经处理的异常将传播到父任务中。  可以使用此行为，从一个根任务而无需遍历任务树来观察所有子任务异常。  但是，当父任务不需要其他代码的附件时，异常传播可能会产生问题。  例如，设想下从 <xref:System.Threading.Tasks.Task> 对象调用第三方库组件的应用。  如果第三方库组件也创建一个 <xref:System.Threading.Tasks.Task> 对象，并指定 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> 以将其附加到父任务中，则子任务中出现的任何未经处理的异常将会传播到父任务。  这可能会导致主应用中出现意外行为。  
  
 若要防止子任务附加到其父任务，请在创建父任务 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601> 对象时，指定 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> 选项。  当某项任务尝试附加到其父任务，且其父任务指定了 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> 选项时，则子任务将不能附加到父任务，并且将像未指定 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> 选项一样进行执行。  
  
 可能还想要防止子任务在没有及时完成时附加到其父任务。  因为父任务只有在所有子任务完成后才会完成，所以长时间运行的子任务会使整个应用执行得非常缓慢。  有关演示如何通过防止子任务附加到其父任务来提高应用性能的示例，请参阅[How to: Prevent a Child Task from Attaching to its Parent](../../../docs/standard/parallel-programming/how-to-prevent-a-child-task-from-attaching-to-its-parent.md)。  
  
## 请参阅  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)   
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)