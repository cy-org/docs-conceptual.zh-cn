---
title: "基于命令性代码的验证 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae12537c-455e-42b1-82f4-cea4c46c023e
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 基于命令性代码的验证
基于代码的命令性验证为活动提供简单方式，以提供关于其自身的验证，并可用于派生自 <xref:System.Activities.CodeActivity>、<xref:System.Activities.AsyncCodeActivity> 和 <xref:System.Activities.NativeActivity> 的活动。会向活动中添加确定所有验证错误或警告的验证代码。  
  
## 使用基于代码的验证  
 基于代码的验证受派生自 <xref:System.Activities.CodeActivity>、<xref:System.Activities.AsyncCodeActivity> 和 <xref:System.Activities.NativeActivity> 的活动的支持。可以将验证代码放置在 <xref:System.Activities.CodeActivity.CacheMetadata%2A> 重写中，并且可以将验证错误或警告添加到元数据参数。在以下从 [基本验证](../../../docs/framework/windows-workflow-foundation/samples/basic-validation.md) 示例中采用的示例中，如果 `Cost` 大于 `Price`，则会向元数据添加验证错误。  
  
> [!NOTE]
>  请注意，`Cost` 和 `Price` 不是对活动的参数，而是在设计时间设置的属性。这就是为什么他们的价值观可以在 <xref:System.Activities.CodeActivity.CacheMetadata%2A> 重写中得到验证的原因。流经参数的数据值不能在设计时间验证，因为数据在运行时间前，不会流动，但可以验证活动参数，以确保使用 `RequiredArgument` 属性和重载的群体对其进行绑定。此示例代码查看 `Description` 参数的 `RequiredArgument` 特性，如果未绑定，则会生成验证错误。  所需的参数包含在 [必需参数和重载组](../../../docs/framework/windows-workflow-foundation//required-arguments-and-overload-groups.md) 中。  
  
```csharp  
public sealed class CreateProduct : CodeActivity  
{  
    public double Price { get; set; }  
    public double Cost { get; set; }  
  
    // [RequiredArgument] attribute will generate a validation error   
    // if the Description argument is not set.  
    [RequiredArgument]  
    public InArgument<string> Description { get; set; }  
  
    protected override void CacheMetadata(CodeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        // Determine when the activity has been configured in an invalid way.  
        if (this.Cost > this.Price)  
        {  
            // Add a validation error with a custom message.  
            metadata.AddValidationError("The Cost must be less than or equal to the Price.");  
        }  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // Not needed for the sample.  
    }  
}  
  
```  
  
 默认情况下，调用 <xref:System.Activities.CodeActivityMetadata.AddValidationError%2A> 时会向元数据中添加一个验证错误。若要添加验证警告，请使用接受 <xref:System.Activities.Validation.ValidationError> 的 <xref:System.Activities.CodeActivityMetadata.AddValidationError%2A> 重载，并通过设置 <xref:System.Activities.Validation.ValidationError.IsWarning%2A> 属性来指定 <xref:System.Activities.Validation.ValidationError> 表示一个警告。  
  
 当在工作流设计器中修改工作流，并且工作流设计器中显示任何验证错误或警告时，将执行验证。此外，当调用工作流时，如果发生任何验证错误，默认验证逻辑将引发 <xref:System.Activities.InvalidWorkflowException>，此时，也将在运行时执行验证。有关调用验证和访问任意验证警告或错误的 [!INCLUDE[crabout](../../../includes/crabout-md.md)] 信息，请参见 [调用活动验证](../../../docs/framework/windows-workflow-foundation//invoking-activity-validation.md)。  
  
 由 <xref:System.Activities.CodeActivity.CacheMetadata%2A> 引发的任何异常不会视为验证错误。这些异常将从对 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 的调用中逃离，因而必须由调用方进行处理。  
  
 基于代码的验证对于验证包含代码的活动非常有用，但它看不到工作流中的其他活动。声明性约束验证能够验证某个活动与工作流中其他活动之间的关系，在[声明性约束](../../../docs/framework/windows-workflow-foundation//declarative-constraints.md)主题中对此进行了介绍。