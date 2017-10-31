---
title: "数据流（任务并行库） | Microsoft Docs"
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
  - "任务并行库, 数据流"
  - "TPL 数据流库"
ms.assetid: 643575d0-d26d-4c35-8de7-a9c403e97dd6
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 22
---
# 数据流（任务并行库）
<a name="top"></a>任务并行库 (TPL) 提供数据流组件以帮助提高启用并发的应用程序的健壮性。 这些数据流组件统称为*TPL 数据流库*。 这种数据流模型通过向粗粒度的数据流和管道任务提供进程内消息传递来促进基于角色的编程。 数据流组件基于 TPL 的类型和计划基础结构，并与 C#、[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 和 F# 语言支持集成，从而可以进行异步编程。 当您有必须相互异步沟通的多个操作或者想要在数据可用时对其处理时，这些数据流组件就非常有用。 例如，请考虑一个处理网络摄像机图像数据的应用程序。 通过使用数据流模型，当图像帧可用时，应用程序就可以处理它们。 如果应用程序增强图像帧，例如，通过执行灯光修正或红眼，您可以创建*管道*数据流组件。 管道的每个阶段可以使用更粗粒度的并行功能（例如 TPL 提供的功能）来转换图像。  
  
 本文档对 TPL 数据流库进行了概述。 它介绍编程模型，预定义的数据流块类型，以及如何配置数据流块来满足应用程序的特定要求。  
  
> [!TIP]
>  TPL 数据流库 (<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName>命名空间) 未随分发[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]。 若要安装<xref:System.Threading.Tasks.Dataflow>命名空间中，打开你的项目中[!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]，选择**管理 NuGet 包**从项目菜单上，然后在线搜索`Microsoft.Tpl.Dataflow`程序包。  
  
 本文档包含以下各节：  
  
-   [编程模型](#model)  
  
-   [预定义的数据流块类型](#predefined_types)  
  
-   [配置数据流块行为](#behavior)  
  
-   [自定义数据流块](#custom)  
  
<a name="model"></a>   
## <a name="programming-model"></a>编程模型  
 TPL 数据流库向具有高吞吐量和低滞后时间的占用大量 CPU 和 I/O 操作的应用程序的并行化和消息传递提供了基础。 它还能显式控制缓存数据的方式以及在系统中移动的方式。 为了更好地了解数据流编程模型，请考虑一个以异步方式从磁盘加载图像并创建复合图像的应用程序。 传统编程模型通常需要使用回调和同步对象（例如锁）来协调任务和访问共享数据。 通过使用数据流编程模型，您可以从磁盘读取时创建处理图像的数据流对象。 在数据流模型下，您可以声明当数据可用时的处理方式，以及数据之间的所有依赖项。 由于运行时管理数据之间的依赖项，因此通常可以避免这种要求来同步访问共享数据。 此外，因为运行时计划基于数据的异步到达，所以数据流可以通过有效管理基础线程提高响应能力和吞吐量。 使用数据流编程模型实现图像处理在 Windows 窗体应用程序中的示例，请参阅[演练︰ 在 Windows 窗体应用程序中使用数据流](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md)。  
  
### <a name="sources-and-targets"></a>源和目标  
 TPL 数据流库包括*数据流块*，这是数据缓冲并处理数据的结构。 TPL 定义了三种类型的数据流块︰*从源块*，*目标块*，和*传播器块*。 源块作为数据源，可以读取。 目标块作为数据接收方，可以写入。 传播器块作为源块和目标块，可以读取和写入。 TPL 定义了<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601?displayProperty=fullName>接口来表示源， <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601?displayProperty=fullName>表示目标和<xref:System.Threading.Tasks.Dataflow.IPropagatorBlock%602?displayProperty=fullName>表示传播器。</TInput, TOutput> <xref:System.Threading.Tasks.Dataflow.IPropagatorBlock%602>同时继承自<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601>，和<xref:System.Threading.Tasks.Dataflow.ITargetBlock%601>。\</TInput, TOutput>  
  
 TPL 数据流库提供了实现的几个预定义的数据流块类型<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601>， <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601>，和<xref:System.Threading.Tasks.Dataflow.IPropagatorBlock%602>接口。\</TInput, TOutput> 此部分中的文档中描述这些数据流块类型[预定义的数据流块类型](#predefined_types)。  
  
### <a name="connecting-blocks"></a>连接块  
 您可以连接数据流块来形成*管道*，这是数据流块的线性序列或*网络*，这是数据流块的图形。 管道是网络的一种形式。 在管道或网络中，当数据可用时源向目标异步传播数据。 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A?displayProperty=fullName>方法将源数据流块链接到目标块。 源可以链接到零个或多个目标；目标可以从零个或多个源进行链接。 您可以同时向管道或网络中添加或从其移除数据流块。 预定义的数据流块类型处理所有的建立或释放链接的线程安全性。  
  
 有关连接数据流块以形成基本管道的示例，请参阅[演练︰ 创建数据流管道](../../../docs/standard/parallel-programming/walkthrough-creating-a-dataflow-pipeline.md)。 有关连接数据流块以形成更复杂的网络的示例，请参阅[演练︰ 在 Windows 窗体应用程序中使用数据流](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md)。 有关源向目标一条消息后取消源的数据目标的链接的示例，请参阅[如何︰ 取消链接数据流块](../../../docs/standard/parallel-programming/how-to-unlink-dataflow-blocks.md)。  
  
#### <a name="filtering"></a>筛选  
 当您调用<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A?displayProperty=fullName>方法将源链接到目标时，您可以提供一个委托来决定目标块是接受还是拒绝该消息的值的消息。 这种筛选机制很有用，它可以保证数据流块只接收特定值。 对于大多数预定义的数据流块类型，如果源块连接到多个目标块，那么当目标块拒绝消息时，源将向下一个目标提供该消息。 源向目标提供消息的顺序是按源定义的，可以根据源类型的不同而不同。 一个目标接受消息后，大多数源块类型会停止提供该消息。 此规则的例外是<xref:System.Threading.Tasks.Dataflow.BroadcastBlock%601>类，该类提供向所有目标，每条消息，即使某些目标拒绝消息。 有关使用筛选来仅处理特定消息的示例，请参阅[演练︰ 在 Windows 窗体应用程序中使用数据流](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md)。  
  
> [!IMPORTANT]
>  由于每个预定义源数据流块类型确保了消息是按照它们接收的顺序来传播的，因此每一条消息都必须在源块可以处理下一条消息之前从源块读取。 因此，当您使用筛选向一个源连接多个目标时，请确保至少一个目标块能够接收每一条消息。 否则，您的应用程序可能发生死锁。  
  
### <a name="message-passing"></a>消息传递  
 数据流编程模型相关的概念*消息传递*、 程序的独立组件通过发送消息来与另一个进行通信的位置。 应用程序组件间传播消息的一种方法是调用<xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A>和<xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A?displayProperty=fullName>方法来向目标数据流块发送消息 (<xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A>同步进行;<xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A>异步) 和<xref:System.Threading.Tasks.Dataflow.DataflowBlock.Receive%2A>， <xref:System.Threading.Tasks.Dataflow.DataflowBlock.ReceiveAsync%2A>，和<xref:System.Threading.Tasks.Dataflow.DataflowBlock.TryReceive%2A>方法来从源块接收消息。 您可以通过向头节点（目标块）发送输入数据，从管道的终端节点或网络的终端节点（一个或多个源块）接收输出数据来使用数据流管道或网络组合使用这些方法。 您还可以使用<xref:System.Threading.Tasks.Dataflow.DataflowBlock.Choose%2A>方法来读取从第一个具有可用数据并对该数据执行操作的提供源。  
  
 源块提供数据的目标块通过调用<xref:System.Threading.Tasks.Dataflow.ITargetBlock%601.OfferMessage%2A?displayProperty=fullName>方法。 目标块通过以下三种方式之一来回应提供的消息：它可以接受消息，拒绝消息或推迟消息。 当目标接受消息时， <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601.OfferMessage%2A>方法将返回<xref:System.Threading.Tasks.Dataflow.DataflowMessageStatus>。 当目标拒绝消息时， <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601.OfferMessage%2A>方法将返回<xref:System.Threading.Tasks.Dataflow.DataflowMessageStatus>。 当目标要求它不再来源，接收任何消息<xref:System.Threading.Tasks.Dataflow.ITargetBlock%601.OfferMessage%2A>返回<xref:System.Threading.Tasks.Dataflow.DataflowMessageStatus>。 预定义的源块类型在这些返回值接收后不会向链接的目标提供消息，并且它们会自动取消这些目标的链接。  
  
 当目标块推迟消息以备日后使用时， <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601.OfferMessage%2A>方法将返回<xref:System.Threading.Tasks.Dataflow.DataflowMessageStatus>。 推迟消息的目标快可以稍后调用<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.ReserveMessage%2A?displayProperty=fullName>方法来尝试保留所提供的消息。 此时，消息仍可用，并且可由该目标块使用，否则表明该消息已由另一个目标接收。 当目标块稍后需要消息或不再需要消息时，它将调用<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.ConsumeMessage%2A?displayProperty=fullName>或<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.ReleaseReservation%2A>方法，分别。 消息保留通常由以非贪婪模式运行的数据流块类型使用。 非贪婪模式将在本文档的后面详细介绍。 除了保留推迟的消息，还可以使用目标块<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.ConsumeMessage%2A?displayProperty=fullName>方法来尝试直接使用推迟的消息。  
  
### <a name="dataflow-block-completion"></a>数据流块完成  
 数据流块也支持这一概念*完成*。 完成状态的数据流块不执行任何进一步的工作。 每个数据流块都有一个关联<xref:System.Threading.Tasks.Task?displayProperty=fullName>对象，称为*完成任务*，表示块的完成状态。 因为您可以等待<xref:System.Threading.Tasks.Task>对象完成后，通过使用完成任务，您可以等待一个或更多终端节点的数据流网络，以完成。 <xref:System.Threading.Tasks.Dataflow.IDataflowBlock>接口定义<xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A>方法，通知它完成的请求的数据流块，请与<xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Completion%2A>属性，它返回数据流块的完成任务。 同时<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601>和<xref:System.Threading.Tasks.Dataflow.ITargetBlock%601>继承<xref:System.Threading.Tasks.Dataflow.IDataflowBlock>接口。  
  
 有两种方法来确定数据流块完成时是否没有出错、遇到一个或多个错误或已取消。 第一种方法是调用<xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=fullName>方法中的完成任务`try` - `catch`块 (`Try` - `Catch`在 Visual Basic 中)。 下面的示例创建<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>对象，它将引发<xref:System.ArgumentOutOfRangeException>如果其输入的值小于零。 <xref:System.AggregateException>此示例调用时，将引发<xref:System.Threading.Tasks.Task.Wait%2A>在完成任务。 <xref:System.ArgumentOutOfRangeException>通过访问<xref:System.AggregateException.InnerExceptions%2A>属性<xref:System.AggregateException>对象。  
  
 [!code-csharp[TPLDataflow_Overview#10](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_overview/cs/program.cs#10)]
 [!code-vb[TPLDataflow_Overview#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_overview/vb/program.vb#10)]  
  
 此示例演示在执行数据流块的委托中异常变成不可处理的情况。 建议您在这样的块主体中处理异常。 然而，你如果没能这么做，块就表现得好像是它被取消了，而且不会处理传入消息。  
  
 当显式取消数据流块<xref:System.AggregateException>对象包含<xref:System.OperationCanceledException>中<xref:System.AggregateException.InnerExceptions%2A>属性。 有关数据流取消的详细信息，请参阅本文档后面的“启用取消”部分。  
  
 第二种确定数据流块的完成状态的方法是使用延续执行完成任务，或者使用 C# 和 Visual Basic 的异步语言功能以异步方式等待完成任务。 向提供的委托<xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=fullName>方法采用<xref:System.Threading.Tasks.Task>对象，表示在前面的任务。 情况下<xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Completion%2A>属性，则延续任务的委托采用完成任务本身。 下面的示例与上一个一个示例相似，但它还使用<xref:System.Threading.Tasks.Task.ContinueWith%2A>方法创建输出整个数据流操作状态的完成任务。  
  
 [!code-csharp[TPLDataflow_Overview#11](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_overview/cs/program.cs#11)]
 [!code-vb[TPLDataflow_Overview#11](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_overview/vb/program.vb#11)]  
  
 您还可以使用属性如<xref:System.Threading.Tasks.Task.IsCanceled%2A>的延续任务来确定数据流块的完成状态有关的其他信息的正文中。 有关延续任务以及它们如何相关取消和错误处理的详细信息，请参阅[使用延续任务来链接任务](../../../docs/standard/parallel-programming/chaining-tasks-by-using-continuation-tasks.md)，[任务取消](../../../docs/standard/parallel-programming/task-cancellation.md)，[异常处理](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)，和[NIB︰ 如何︰ 处理由任务引发的异常](http://msdn.microsoft.com/zh-cn/d6c47ec8-9de9-4880-beb3-ff19ae51565d)。  
  
 [[go to top](#top)]  
  
<a name="predefined_types"></a>   
## <a name="predefined-dataflow-block-types"></a>预定义的数据流块类型  
 TPL 数据流库提供了多个预定义的数据流块类型。 这些类型分为三个类别︰*缓冲块*，*执行块*，和*分组块*。 以下部分描述了组成这些类别的块类型。  
  
### <a name="buffering-blocks"></a>缓冲块  
 缓冲块存放的数据供数据使用者使用。 TPL 数据流库提供三种缓冲块类型︰ <xref:System.Threading.Tasks.Dataflow.BufferBlock%601?displayProperty=fullName>， <xref:System.Threading.Tasks.Dataflow.BroadcastBlock%601?displayProperty=fullName>，和<xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601?displayProperty=fullName>。  
  
#### <a name="bufferblockt"></a>BufferBlock(T)  
 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601>类表示一般用途的异步消息结构。 此类存储先进先出 (FIFO) 消息队列，此消息队列可由多个源写入或从多个目标读取。 在目标收到来自消息<xref:System.Threading.Tasks.Dataflow.BufferBlock%601>对象，从消息队列中移除该消息。 因此，尽管<xref:System.Threading.Tasks.Dataflow.BufferBlock%601>对象可以具有多个目标，只有一个目标将接收每条消息。 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601>类很有用，当你想要将多个消息传递到另一个组件，并且该组件必须接收每条消息。  
  
 下面的基本示例将发布多个<xref:System.Int32>值复制到<xref:System.Threading.Tasks.Dataflow.BufferBlock%601>对象，然后这些值从读回该对象。  
  
 [!code-csharp[TPLDataflow_Overview#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_overview/cs/program.cs#1)]
 [!code-vb[TPLDataflow_Overview#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_overview/vb/program.vb#1)]  
  
 有关完整的示例演示如何从中读取消息并将消息写入到<xref:System.Threading.Tasks.Dataflow.BufferBlock%601>对象，请参阅[如何︰ 将消息写入和从数据流块读取消息](../../../docs/standard/parallel-programming/how-to-write-messages-to-and-read-messages-from-a-dataflow-block.md)。  
  
#### <a name="broadcastblockt"></a>BroadcastBlock(T)  
 <xref:System.Threading.Tasks.Dataflow.BroadcastBlock%601>类很有用，必须将多个消息传递到另一个组件，而该组件只需要最新的值。 需向多个组件广播消息时，此类也很有用。  
  
 有跟帖时的基本示例<xref:System.Double>值赋给<xref:System.Threading.Tasks.Dataflow.BroadcastBlock%601>对象，然后读回该值从该对象多次。 因为值不会从<xref:System.Threading.Tasks.Dataflow.BroadcastBlock%601>对象在被读取后，相同的值将出现每次。  
  
 [!code-csharp[TPLDataflow_Overview#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_overview/cs/program.cs#2)]
 [!code-vb[TPLDataflow_Overview#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_overview/vb/program.vb#2)]  
  
 有关完整的示例演示如何使用<xref:System.Threading.Tasks.Dataflow.BroadcastBlock%601>要广播到多个目标块的消息，请参阅[如何︰ 指定数据流块中的任务计划程序](../../../docs/standard/parallel-programming/how-to-specify-a-task-scheduler-in-a-dataflow-block.md)。  
  
#### <a name="writeonceblockt"></a>WriteOnceBlock(T)  
 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>类类似于<xref:System.Threading.Tasks.Dataflow.BroadcastBlock%601>类，不同之处在于<xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>对象可写入一次。 您可以认为<xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>视为类似于 C# [readonly](../Topic/readonly%20\(C%23%20Reference\).md) ([ReadOnly](../Topic/ReadOnly%20\(Visual%20Basic\).md)中[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) 关键字，不同之处在于<xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>接收值，而不是在构造之后对象将成为不可变。 如<xref:System.Threading.Tasks.Dataflow.BroadcastBlock%601>类，当目标收到来自消息<xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>对象，该消息不会从该对象。 因此，多个目标将接收到该消息的副本。 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>您想要传播多条消息的第一个类很有用。  
  
 下面的基本示例将发布多个<xref:System.String>值复制到<xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>对象，然后读回该对象中的该值。 因为<xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>对象可写入一次后只能<xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>对象收到一条消息，因此它放弃后续消息。  
  
 [!code-csharp[TPLDataflow_Overview#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_overview/cs/program.cs#3)]
 [!code-vb[TPLDataflow_Overview#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_overview/vb/program.vb#3)]  
  
 有关完整的示例演示如何使用<xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>要接收完成的第一个操作的值，请参阅[如何︰ 取消链接数据流块](../../../docs/standard/parallel-programming/how-to-unlink-dataflow-blocks.md)。  
  
### <a name="execution-blocks"></a>执行块  
 执行块为每条接收数据调用用户提供的委托。 TPL 数据流库提供三种执行块类型︰<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>， <xref:System.Threading.Tasks.Dataflow.TransformBlock%602?displayProperty=fullName>，和<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602?displayProperty=fullName>。\</TInput, TOutput> \</TInput, TOutput>  
  
#### <a name="actionblockt"></a>ActionBlock(T)  
 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>类是在收到数据时调用委托的目标块。 思考的<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>对象视为数据可用时以异步方式运行的委托。 向提供的委托<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>对象可以是类型<xref:System.Action>或类型`System.Func\<TInput, Task>`。 当您使用<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>对象<xref:System.Action>，每个输入元素的处理才可以视为已完成在委托返回时。 当您使用<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>对象`System.Func\<TInput, Task>`，每个输入元素的处理才可以视为已完成的时，才返回<xref:System.Threading.Tasks.Task>对象完成。 通过使用这两种机制，您可以使用<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>以进行同步和异步处理的每个输入元素。  
  
 下面的基本示例将发布多个<xref:System.Int32>值复制到<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>对象。 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>对象将输出到控制台这些值。 然后此示例将该块设置为已完成状态，并等待所有数据流任务完成。  
  
 [!code-csharp[TPLDataflow_Overview#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_overview/cs/program.cs#4)]
 [!code-vb[TPLDataflow_Overview#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_overview/vb/program.vb#4)]  
  
 有关完整的示例演示如何使用委托的<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>类，请参阅[如何︰ 执行操作时数据流块收到数据](../../../docs/standard/parallel-programming/how-to-perform-action-when-a-dataflow-block-receives-data.md)。  
  
#### <a name="transformblocktinput-toutput"></a>TransformBlock(TInput, TOutput)  
 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602>类类似于<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>类，只不过它充当这两个源和目标。\</TInput, TOutput> 传递给该委托<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>对象返回类型的值`TOutput`。</TInput, TOutput> 向提供的委托<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>对象可以是类型`System.Func<TInput, TOutput>`或类型`System.Func<TInput, Task>`。\</TInput, TOutput> 当您使用<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>对象`System.Func\<TInput, TOutput>`，每个输入元素的处理才可以视为已完成在委托返回时。</TInput, TOutput> 当您使用<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>与使用对象`System.Func<TInput, Task<TOutput>>`，每个输入元素的处理才可以视为已完成的时，才返回<xref:System.Threading.Tasks.Task>对象完成。\</TInput, TOutput> 与<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>，通过使用这两种机制，您可以使用<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>以进行同步和异步处理的每个输入元素。\</TInput, TOutput>  
  
 下面的基本示例创建<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>对象计算其输入的平方根。</TInput, TOutput> <xref:System.Threading.Tasks.Dataflow.TransformBlock%602>对象采用<xref:System.Int32>值作为输入并生成<xref:System.Double>值作为输出。\</TInput, TOutput>  
  
 [!code-csharp[TPLDataflow_Overview#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_overview/cs/program.cs#5)]
 [!code-vb[TPLDataflow_Overview#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_overview/vb/program.vb#5)]  
  
 有关完整示例，请使用<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>中在 Windows 窗体应用程序中执行图像处理的数据流块网络，请参阅[演练︰ 在 Windows 窗体应用程序中使用数据流](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md)。\</TInput, TOutput>  
  
#### <a name="transformmanyblocktinput-toutput"></a>TransformManyBlock(TInput, TOutput)  
 <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>类类似于<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>类，不同之处在于<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>生成为每个输入值，而不是仅一个输出值为每个输入值生成零个或多个输出值。</TInput, TOutput> </TInput, TOutput> </TInput, TOutput> 向提供的委托<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>对象可以是类型`System.Func<TInput, IEnumerable<TOutput>>`或`type System.Func<TInput, Task<IEnumerable<TOutput>>>`。\</TInput, TOutput> 当您使用<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>对象`System.Func<TInput, IEnumerable<TOutput>>`，每个输入元素的处理才可以视为已完成在委托返回时。</TInput, TOutput> 当您使用<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>对象`System.Func<TInput, Task<IEnumerable<TOutput>>>`，每个输入元素的处理才可以视为完成时，才返回`System.Threading.Tasks.Task<IEnumerable<TOutput>>`对象完成。\</TInput, TOutput>  
  
 下面的基本示例创建<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>将字符串拆分为单个字符序列的对象。</TInput, TOutput> <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>对象采用<xref:System.String>值作为输入并生成<xref:System.Char>值作为输出。\</TInput, TOutput>  
  
 [!code-csharp[TPLDataflow_Overview#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_overview/cs/program.cs#6)]
 [!code-vb[TPLDataflow_Overview#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_overview/vb/program.vb#6)]  
  
 有关完整示例，请使用<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>若要生成多个独立输出的数据流管道中的每个输入，请参阅[演练︰ 创建数据流管道](../../../docs/standard/parallel-programming/walkthrough-creating-a-dataflow-pipeline.md)。\</TInput, TOutput>  
  
#### <a name="degree-of-parallelism"></a>并行度  
 每个<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>， <xref:System.Threading.Tasks.Dataflow.TransformBlock%602>，和<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>对象都缓冲输入消息，直到块准备处理它们。</TInput, TOutput> </TInput, TOutput> 默认情况下，这些类以接收消息的顺序处理消息，一次处理一条消息。 您还可以指定要启用的并行度<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>， <xref:System.Threading.Tasks.Dataflow.TransformBlock%602>和<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>对象同时处理多条消息。\</TInput, TOutput> \</TInput, TOutput> 有关并行执行的详细信息，请参阅本文档后面的“指定并行度”部分。 有关设置的示例，要使执行数据流块能够一次处理多条消息的并行度，请参阅[如何︰ 在数据流块中指定并行度](../../../docs/standard/parallel-programming/how-to-specify-the-degree-of-parallelism-in-a-dataflow-block.md)。  
  
#### <a name="summary-of-delegate-types"></a>委托类型摘要  
 下表总结了可以向提供的委托类型<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>， <xref:System.Threading.Tasks.Dataflow.TransformBlock%602>，和<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>对象。\</TInput, TOutput> \</TInput, TOutput> 此表还指出委托类型是同步执行还是异步执行。  
  
|类型|同步委托类型|异步委托类型|  
|----------|-------------------------------|--------------------------------|  
|<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>|`System.Action`|`System.Func\<TInput, Task>`|  
|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602></TInput, TOutput>|`System.Func\<TInput, TOutput>`2`|`System.Func<TInput, Task<TOutput>>`|  
|<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602></TInput, TOutput>|`System.Func<TInput, IEnumerable<TOutput>>`|`System.Func<TInput, Task<IEnumerable<TOutput>>>`|  
  
 当处理执行块类型时，还可以使用 lambda 表达式。 有关演示如何使用 lambda 表达式处理执行块的示例，请参阅[如何︰ 执行操作时数据流块收到数据](../../../docs/standard/parallel-programming/how-to-perform-action-when-a-dataflow-block-receives-data.md)。  
  
### <a name="grouping-blocks"></a>分组块  
 分组块在各种约束下合并一个或多个源的数据。 TPL 数据流库提供三种联接块类型︰ <xref:System.Threading.Tasks.Dataflow.BatchBlock%601>， <xref:System.Threading.Tasks.Dataflow.JoinBlock%602>，和<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602>。\</T1, T2> \</T1, T2>  
  
#### <a name="batchblockt"></a>BatchBlock(T)  
 <xref:System.Threading.Tasks.Dataflow.BatchBlock%601>类可将合并的输入数据，这称为批，数组中的输出数据集。 在创建时指定的每个批次大小<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>对象。 当<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>对象接收指定的数量的输入元素时，它会异步传播包含这些元素的数组。 如果<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>对象设置为已完成状态，但不包含足够的元素形成批，则会传播包含其余输入的元素的最终数组。  
  
 <xref:System.Threading.Tasks.Dataflow.BatchBlock%601>类中任意一种操作*贪婪*或*非贪婪*模式。 在贪婪模式下，这是默认值， <xref:System.Threading.Tasks.Dataflow.BatchBlock%601>对象接受它提供并收到指定的数量的元素后传播数组每条消息。 在非贪婪模式下， <xref:System.Threading.Tasks.Dataflow.BatchBlock%601>对象推迟所有传入的消息，直到足够的源提供的块的消息来形成批。 贪婪模式处理开销较少，所以通常比非贪婪模式执行得更有效。 但是，当您必须以基本方式协调来自多个源的消耗时，可以使用非贪婪模式。 通过设置来指定非贪婪模式<xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions.Greedy%2A>到`False`中`dataflowBlockOptions`中的参数<xref:System.Threading.Tasks.Dataflow.BatchBlock%601.%23ctor%2A>构造函数。  
  
 下面的基本示例将发布多个<xref:System.Int32>值复制到<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>批中能容纳十个元素的对象。 若要确保所有值都传播外<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>，此示例调用<xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A>方法。 <xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A>方法设置<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>对象传递给完成的状态，因此， <xref:System.Threading.Tasks.Dataflow.BatchBlock%601>对象作为最终批传播剩余的所有元素。  
  
 [!code-csharp[TPLDataflow_Overview#7](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_overview/cs/program.cs#7)]
 [!code-vb[TPLDataflow_Overview#7](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_overview/vb/program.vb#7)]  
  
 有关完整的示例使用<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>若要提高数据库插入操作的效率，请参阅[演练︰ 使用 BatchBlock 和 BatchedJoinBlock 提高效率](../../../docs/standard/parallel-programming/walkthrough-using-batchblock-and-batchedjoinblock-to-improve-efficiency.md)。  
  
#### <a name="joinblockt1-t2-"></a>JoinBlock(T1, T2, ...)  
 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602>和<xref:System.Threading.Tasks.Dataflow.JoinBlock%603>类收集输入的元素并传播<xref:System.Tuple%602?displayProperty=fullName>或<xref:System.Tuple%603?displayProperty=fullName>包含这些元素的对象。\</T1, T2, T3> \</T1, T2> \</T1, T2, T3> \</T1, T2> <xref:System.Threading.Tasks.Dataflow.JoinBlock%602>和<xref:System.Threading.Tasks.Dataflow.JoinBlock%603>类并非继承自<xref:System.Threading.Tasks.Dataflow.ITargetBlock%601>。</T1, T2, T3> </T1, T2> 相反，它们提供属性， <xref:System.Threading.Tasks.Dataflow.JoinBlock%602.Target1%2A>， <xref:System.Threading.Tasks.Dataflow.JoinBlock%602.Target2%2A>，和<xref:System.Threading.Tasks.Dataflow.JoinBlock%603.Target3%2A>，实现<xref:System.Threading.Tasks.Dataflow.ITargetBlock%601>。  
  
 如<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>， <xref:System.Threading.Tasks.Dataflow.JoinBlock%602>和<xref:System.Threading.Tasks.Dataflow.JoinBlock%603>在贪婪或非贪婪模式下操作。</T1, T2, T3> </T1, T2> 在贪婪模式下，这是默认值， <xref:System.Threading.Tasks.Dataflow.JoinBlock%602>或<xref:System.Threading.Tasks.Dataflow.JoinBlock%603>对象接受它提供并传播元组其每个目标接收至少一条消息之后每条消息。</T1, T2, T3> </T1, T2> 在非贪婪模式下， <xref:System.Threading.Tasks.Dataflow.JoinBlock%602>或<xref:System.Threading.Tasks.Dataflow.JoinBlock%603>对象推迟所有传入的消息，直到所有目标向都提供了创建元组所需的数据。\</T1, T2, T3> \</T1, T2> 此时，块参与两阶段提交协议，以原子方式从源中检索所有必需的项。 此延迟使得其他实体可以同时使用数据，这使整个系统取得进展。  
  
 下面的基本示例演示如何在这种情况下<xref:System.Threading.Tasks.Dataflow.JoinBlock%603>对象需要多个数据来计算值。</T1, T2, T3> 此示例将创建<xref:System.Threading.Tasks.Dataflow.JoinBlock%603>对象，它需要两个<xref:System.Int32>值和一个<xref:System.Char>值来执行算术运算。\</T1, T2, T3>  
  
 [!code-csharp[TPLDataflow_Overview#8](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_overview/cs/program.cs#8)]
 [!code-vb[TPLDataflow_Overview#8](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_overview/vb/program.vb#8)]  
  
 有关完整的示例使用<xref:System.Threading.Tasks.Dataflow.JoinBlock%602>对象在非贪婪模式下合作共享资源，请参阅[如何︰ 使用 JoinBlock 数据从多个源读取](../../../docs/standard/parallel-programming/how-to-use-joinblock-to-read-data-from-multiple-sources.md)。\</T1, T2>  
  
#### <a name="batchedjoinblockt1-t2-"></a>BatchedJoinBlock(T1, T2, ...)  
 <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602>和<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%603>类收集各批输入元素并传播`System.Tuple(IList(T1), IList(T2))`或`System.Tuple(IList(T1), IList(T2), IList(T3))`包含这些元素的对象。\</T1, T2, T3> \</T1, T2> 思考的<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602>的组合作为<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>和<xref:System.Threading.Tasks.Dataflow.JoinBlock%602>。</T1, T2> </T1, T2> 在创建时指定的每个批次大小<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602>对象。\</T1, T2> <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602>还提供了属性， <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602.Target1%2A>和<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602.Target2%2A>，实现<xref:System.Threading.Tasks.Dataflow.ITargetBlock%601>。\</T1, T2> 当从所有目标收到指定的数量的输入元素时<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602>对象会异步传播`System.Tuple(IList(T1), IList(T2))`对象，其中包含这些元素。\</T1, T2>  
  
 下面的基本示例创建<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602>对象，它包含结果、 <xref:System.Int32>值以及错误<xref:System.Exception>对象。</T1, T2> 此示例执行多项操作，然后将结果写入<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602.Target1%2A>属性，并将错误记录到<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602.Target2%2A>属性的<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602>对象。\</T1, T2> 由于成功和失败操作的计数事先是未知的因此<xref:System.Collections.Generic.IList%601>对象使每个目标都能收到零个或多个值。  
  
 [!code-csharp[TPLDataflow_Overview#9](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_overview/cs/program.cs#9)]
 [!code-vb[TPLDataflow_Overview#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_overview/vb/program.vb#9)]  
  
 有关完整的示例使用<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602>要捕获的结果和程序从数据库读取数据时出现的任何异常，请参阅[演练︰ 使用 BatchBlock 和 BatchedJoinBlock 提高效率](../../../docs/standard/parallel-programming/walkthrough-using-batchblock-and-batchedjoinblock-to-improve-efficiency.md)。\</T1, T2>  
  
 [[go to top](#top)]  
  
<a name="behavior"></a>   
## <a name="configuring-dataflow--block-behavior"></a>配置数据流块行为  
 您可以通过提供启用其他选项<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions?displayProperty=fullName>对象传递给数据流块类型的构造函数。 这些选项控制这类管理基础任务和并行度的调度程序的行为。 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions>还包含派生类型，用以指定特定于某些数据流块类型的行为。 下表汇总了与每个数据流块类型相关的选项类型。  
  
|数据流块类型|<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions>类型|  
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Threading.Tasks.Dataflow.BufferBlock%601>|<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions>|  
|<xref:System.Threading.Tasks.Dataflow.BroadcastBlock%601>|<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions>|  
|<xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>|<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions>|  
|<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>|<xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions>|  
|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>\</TInput, TOutput>|<xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions>|  
|<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>\</TInput, TOutput>|<xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions>|  
|<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>|<xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions>|  
|<xref:System.Threading.Tasks.Dataflow.JoinBlock%602>\</T1, T2>|<xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions>|  
|<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602>\</T1, T2>|<xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions>|  
  
 以下各节提供其他信息有关重要数据流块选项可通过<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions?displayProperty=fullName>， <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions?displayProperty=fullName>，和<xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions?displayProperty=fullName>类。  
  
### <a name="specifying-the-task-scheduler"></a>指定任务计划程序  
 每个预定义的数据流块在数据可用时使用 TPL 任务计划机制执行一些活动，例如，将数据传播到目标、接收来自源的数据并运行用户定义的委托。 <xref:System.Threading.Tasks.TaskScheduler>是一个抽象类表示的任务计划程序排队成线程的任务。 默认任务计划程序<xref:System.Threading.Tasks.TaskScheduler.Default%2A>，使用<xref:System.Threading.ThreadPool>类进行排队并执行工作。 可以通过设置重写默认任务计划程序<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.TaskScheduler%2A>属性构造数据流块对象时。  
  
 当同一个任务计划程序管理多个数据流块时，它可在它们之间强制实施策略。 例如，如果多个数据流块分别配置为针对相同的独占计划程序<xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair>对象，则会序列化这些块间运行的所有工作。 同样，如果这些块配置为面向相同的并发计划程序<xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair>对象，而该计划配置为具有最大并发级，这些块中的所有工作都都会受到并发操作数的。 有关使用示例， <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair>类，以启用读取的操作中并行发生，但写入操作独立于所有其他操作，请参阅[如何︰ 指定数据流块中的任务计划程序](../../../docs/standard/parallel-programming/how-to-specify-a-task-scheduler-in-a-dataflow-block.md)。 有关 TPL 中的任务计划程序的详细信息，请参阅<xref:System.Threading.Tasks.TaskScheduler>类主题。  
  
### <a name="specifying-the-degree-of-parallelism"></a>指定并行度  
 默认情况下，TPL 数据流库提供的三种执行块类型<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>， <xref:System.Threading.Tasks.Dataflow.TransformBlock%602>，和<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>，一次处理一条消息。\</TInput, TOutput> \</TInput, TOutput> 这些数据流块类型也会按照接收消息的顺序对消息进行处理。 若要使这些数据流块可以同时处理消息，将设置<xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A?displayProperty=fullName>属性构造数据流对象块时。  
  
 默认值为<xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A>为 1，这保证了数据流块一次处理一条消息。 将该属性设置为大于 1 的值将使数据流块可以同时处理多条消息。 此属性设置为<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.Unbounded?displayProperty=fullName>使基础任务计划程序管理最大并发程度。  
  
> [!IMPORTANT]
>  当您指定大于 1 的最大并行度时，会同时处理多条消息，因此，消息可能不会按照接收的顺序进行处理。 将会对从块中输出消息的顺序进行正确排序。  
  
 因为<xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A>属性表示最大并行度，数据流块执行时可能较小的并行度超过您指定。 为了达到功能要求或因为缺少可用的系统资源，数据流块可能使用较小的并行度。 数据流块选择的并行度不会超过您指定的值。  
  
 值<xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A>属性是否专用于每个数据流块对象。 例如，如果四个数据流对象块中的每一个都指定 1 作为最大并行度，则所有四个数据流对象块可以并行运行。  
  
 设置最大并行度导致并行操作较长的示例，请参阅[如何︰ 在数据流块中指定并行度](../../../docs/standard/parallel-programming/how-to-specify-the-degree-of-parallelism-in-a-dataflow-block.md)。  
  
### <a name="specifying-the-number-of-messages-per-task"></a>指定每个任务的消息数  
 预定义的数据流块类型使用任务来处理多个输入元素。 这有助于最大限度地减少需要处理数据的任务对象数，从而使应用程序可以更有效地运行。 但是，当一个数据流块集合中的任务处理数据时，其他数据流块的任务可能需要按照队列消息等待处理时间。 若要启用数据流任务更加公平，设置<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.MaxMessagesPerTask%2A>属性。 当<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.MaxMessagesPerTask%2A>设置为<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.Unbounded?displayProperty=fullName>，这是默认设置，数据流块使用的任务会处理尽可能多的消息。 当<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.MaxMessagesPerTask%2A>设置为一个值除<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.Unbounded>，数据流块最多处理这个数量的每个消息<xref:System.Threading.Tasks.Task>对象。 虽然设置<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.MaxMessagesPerTask%2A>属性可以提高任务间的公平性，但它可能会导致系统创建多个任务不是必需的这可能会降低性能。  
  
### <a name="enabling-cancellation"></a>启用取消  
 TPL 提供了一种机制，能使任务以一种合作的方式协调取消。 若要启用数据流块参与此取消机制，设置<xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A>属性。 当这<xref:System.Threading.CancellationToken>对象设置为已取消状态，所有监视该标记的数据流块都会完成当前项目的执行，但不是会开始处理后续项。 这些数据流块也会清除所有缓冲的消息，释放所有源和目标块的连接，并转换为已取消状态。 通过转换为已取消状态，<xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Completion%2A>属性具有<xref:System.Threading.Tasks.Task.Status%2A>属性设置为<xref:System.Threading.Tasks.TaskStatus>，除非在处理过程中出现异常。 在这种情况下，<xref:System.Threading.Tasks.Task.Status%2A>设置为<xref:System.Threading.Tasks.TaskStatus>。  
  
 有关演示如何在 Windows 窗体应用程序中使用取消的示例，请参阅[如何︰ 取消数据流块](../../../docs/standard/parallel-programming/how-to-cancel-a-dataflow-block.md)。 有关 TPL 中取消的详细信息，请参阅[任务取消](../../../docs/standard/parallel-programming/task-cancellation.md)。  
  
### <a name="specifying-greedy-versus-non-greedy-behavior"></a>指定贪婪与非贪婪行为  
 多个分组数据流块类型可以在任何一个操作*贪婪*或*非贪婪*模式。 默认情况下，预定义的数据流块类型在贪婪模式下运行。  
  
 对于联接块类型如<xref:System.Threading.Tasks.Dataflow.JoinBlock%602>，贪婪模式意味着块立即接受数据，即使相应的数据联接尚不可用。</T1, T2> 非贪婪模式意味着块推迟所有传入的消息，直到在其每个目标上有一个可完成联接。 如果任何推迟的消息不再可用，则联接块会释放所有推迟的消息并重新启动该过程。 有关<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>类，贪婪和非贪婪行为非常相似，不同之处在于在非贪婪模式下， <xref:System.Threading.Tasks.Dataflow.BatchBlock%601>对象推迟所有传入的消息，直到有足够可用不同的源，若要完成一批中。  
  
 若要指定非贪婪模式数据流块，请设置<xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions.Greedy%2A>到`False`。 有关示例，演示如何使用非贪婪模式使多个联接块更有效地共享数据源，请参阅[如何︰ 使用 JoinBlock 数据从多个源读取](../../../docs/standard/parallel-programming/how-to-use-joinblock-to-read-data-from-multiple-sources.md)。  
  
 [[go to top](#top)]  
  
<a name="custom"></a>   
## <a name="custom-dataflow-blocks"></a>自定义数据流块  
 尽管 TPL 数据流库提供了许多预定义块类型，但是您还是可以创建执行自定义行为的其他块类型。 实现<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601>或<xref:System.Threading.Tasks.Dataflow.ITargetBlock%601>直接接口或使用<xref:System.Threading.Tasks.Dataflow.DataflowBlock.Encapsulate%2A>方法生成封装现有块类型行为的复杂块。\</TInput, TOutput> 有关演示如何实现自定义数据流块功能的示例，请参阅[演练︰ 创建自定义的数据流块类型](../../../docs/standard/parallel-programming/walkthrough-creating-a-custom-dataflow-block-type.md)。  
  
 [[go to top](#top)]  
  
## <a name="related-topics"></a>相关主题  
  
|标题|说明|  
|-----------|-----------------|  
|[如何︰ 将消息写入和从数据流块读取消息](../../../docs/standard/parallel-programming/how-to-write-messages-to-and-read-messages-from-a-dataflow-block.md)|演示如何从中读取消息并将消息写入到<xref:System.Threading.Tasks.Dataflow.BufferBlock%601>对象。|  
|[如何︰ 实现制造者-使用者数据流模式](../../../docs/standard/parallel-programming/how-to-implement-a-producer-consumer-dataflow-pattern.md)|描述如何使用数据流模型实现制造者-使用方模式，在这个模型中制造者向数据流块发送消息，而使用方从该块中读取消息。|  
|[如何︰ 在数据流块收到数据时执行操作](../../../docs/standard/parallel-programming/how-to-perform-action-when-a-dataflow-block-receives-data.md)|描述如何向执行数据流块类型，提供委托<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>， <xref:System.Threading.Tasks.Dataflow.TransformBlock%602>，和<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>。\</TInput, TOutput> \</TInput, TOutput>|  
|[演练︰ 创建数据流管道](../../../docs/standard/parallel-programming/walkthrough-creating-a-dataflow-pipeline.md)|描述如何创建从 Web 下载文本并对该文本执行操作的数据流管道。|  
|[如何︰ 取消链接数据流块](../../../docs/standard/parallel-programming/how-to-unlink-dataflow-blocks.md)|演示如何使用<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A>方法源向目标提供消息后取消目标块从其源的链接。|  
|[演练︰ 在 Windows 窗体应用程序中使用数据流](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md)|演示如何创建在 Windows 窗体应用程序中执行图像处理的数据流块网络。|  
|[如何︰ 取消数据流块](../../../docs/standard/parallel-programming/how-to-cancel-a-dataflow-block.md)|演示如何在 Windows 窗体应用程序中使用取消。|  
|[如何︰ 使用 JoinBlock 从多个源读取数据](../../../docs/standard/parallel-programming/how-to-use-joinblock-to-read-data-from-multiple-sources.md)|说明如何使用<xref:System.Threading.Tasks.Dataflow.JoinBlock%602>类在数据从多个源，以及如何使用非贪婪模式使多个联接块更有效地共享数据源可用时执行的操作。\</T1, T2>|  
|[如何︰ 指定数据流块中的并行度](../../../docs/standard/parallel-programming/how-to-specify-the-degree-of-parallelism-in-a-dataflow-block.md)|描述如何设置<xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A>属性使执行数据流块能够一次处理多条消息。|  
|[如何︰ 指定数据流块中的任务计划程序](../../../docs/standard/parallel-programming/how-to-specify-a-task-scheduler-in-a-dataflow-block.md)|演示在应用程序中使用数据流时如何关联特定任务计划程序。|  
|[演练︰ 使用 BatchBlock 和 BatchedJoinBlock 提高效率](../../../docs/standard/parallel-programming/walkthrough-using-batchblock-and-batchedjoinblock-to-improve-efficiency.md)|介绍如何使用<xref:System.Threading.Tasks.Dataflow.BatchBlock%601>类，以提高效率的数据库插入操作，以及如何使用<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602>类获取结果和程序从数据库读取数据时出现的任何异常。\</T1, T2>|  
|[演练︰ 创建自定义数据流块类型](../../../docs/standard/parallel-programming/walkthrough-creating-a-custom-dataflow-block-type.md)|演示创建实现自定义行为的数据流块类型的两种方法。|  
|[任务并行库 (TPL)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)|介绍 TPL，一个可在 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 应用程序里简化并行和并发编程的库。|