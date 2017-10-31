---
title: "调用活动验证 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 22bef766-c505-4fd4-ac0f-7b363b238969
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 调用活动验证
活动验证提供了一种在执行任何活动配置之前标识和报告此配置中的错误的方法。当在工作流设计器中修改工作流，并且工作流设计器中显示任何验证错误或警告时，将执行验证。此外，当调用工作流时，如果发生任何验证错误，默认验证逻辑将引发 <xref:System.Activities.InvalidWorkflowException>，此时，也将在运行时执行验证。工作流应用程序和工具开发人员可使用 [!INCLUDE[wf](../../../includes/wf-md.md)] 提供的 <xref:System.Activities.Validation.ActivityValidationServices> 类显式验证活动。  本主题说明如何使用 <xref:System.Activities.Validation.ActivityValidationServices> 执行活动验证。  
  
## 使用 ActivityValidationServices  
 <xref:System.Activities.Validation.ActivityValidationServices> 具有两种 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 重载，用于调用活动的验证逻辑。第一种重载采用要验证的根活动，并返回验证错误和警告的集合。下面的示例使用含有两个必需参数的自定义 `Add` 活动。  
  
```csharp  
public sealed class Add : CodeActivity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Operand1 { get; set; }  
  
    [RequiredArgument]  
    public InArgument<int> Operand2 { get; set; }  
  
    protected override int Execute(CodeActivityContext context)  
    {  
        return Operand1.Get(context) + Operand2.Get(context);  
    }  
}  
```  
  
 `Add` 活动在 <xref:System.Activities.Statements.Sequence> 中使用，但未绑定该活动的两个必需参数，如下面的示例所示。  
  
```csharp  
Variable<int> Operand1 = new Variable<int>{ Default = 10 };  
Variable<int> Operand2 = new Variable<int>{ Default = 15 };  
Variable<int> Result = new Variable<int>();  
  
Activity wf = new Sequence  
{  
    Variables = { Operand1, Operand2, Result },  
    Activities =   
    {  
        new Add(),  
        new WriteLine  
        {  
            Text = new InArgument<string>(env => "The result is " + Result.Get(env))  
        }  
    }  
};  
```  
  
 此工作流可以通过调用 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 进行验证。<xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 返回活动及其所有子级包含的所有验证错误或警告的集合，如下面的示例所示。  
  
```csharp  
ValidationResults results = ActivityValidationServices.Validate(wf);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 当对此示例工作流调用 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 时，返回两个验证错误。  
  
 **错误：未提供必要活动参数“Operand2”的值。**   
**错误：未提供必要活动参数“Operand1”的值。**  如果已调用此工作流，将引发 <xref:System.Activities.InvalidWorkflowException>，如下面的示例所示。  
  
```csharp  
try  
{  
    WorkflowInvoker.Invoke(wf);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
 **System.Activities.InvalidWorkflowException：**   
**处理工作流树时遇到以下错误：**   
**“Add”：未提供必要活动参数“Operand2”的值。**   
**“Add”：未提供必要活动参数“Operand1”的值。**  为使此示例工作流有效，必须绑定 `Add` 活动的两个必需参数。在下面的示例中，这两个必需参数绑定到工作流变量和结果值。在此示例中，<xref:System.Activities.Activity%601.Result%2A> 参数与这两个必需参数绑定在一起。不必绑定 <xref:System.Activities.Activity%601.Result%2A> 参数，因为如果未绑定该参数，并不会导致验证错误。如果在工作流中的其他位置使用 <xref:System.Activities.Activity%601.Result%2A> 的值，工作流作者应负责绑定该参数。  
  
```csharp  
new Add  
{  
    Operand1 = Operand1,  
    Operand2 = Operand2,  
    Result = Result  
}  
```  
  
### 验证根活动中的必需参数  
 如果工作流的根活动含有实参，则在调用该工作流并向其传递形参之前，不会绑定这些实参。如果已调用工作流但未传入必需实参，下面的工作流将通过验证，但会引发异常，如下面的示例所示。  
  
```csharp  
Activity wf = new Add();  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
// results has no errors or warnings, but when the workflow  
// is invoked, an InvalidWorkflowException is thrown.  
try  
{  
    WorkflowInvoker.Invoke(wf);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
 **System.ArgumentException：根活动参数的设置不正确。**   
**修复工作流定义或提供要修复这些错误的输入的值：**   
**“Add”：未提供必要活动参数“Operand2”的值。**   
**“Add”：未提供必要活动参数“Operand1”的值。**  传递正确的参数之后，工作流将成功完成，如下面的示例所示。  
  
```csharp  
Add wf = new Add();  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
// results has no errors or warnings, and the workflow completes  
// successfully because the required arguments were passed.  
try  
{  
    Dictionary<string, object> wfparams = new Dictionary<string, object>  
    {  
        { "Operand1", 10 },  
        { "Operand2", 15 }  
    };  
  
    int result = WorkflowInvoker.Invoke(wf, wfparams);  
    Console.WriteLine("Result: {0}", result);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
> [!NOTE]
>  在此示例中，根活动已声明为 `Add`，而不是上述示例中的 `Activity`。这使 `WorkflowInvoker.Invoke` 方法返回一个表示 `Add` 活动的结果的整数，而不是 `out` 参数的字典。也可将 `wf` 变量声明为 `Activity<int>`。  
  
 当验证根参数时，主机应用程序应负责确保在调用工作流时传递所有必需参数。  
  
### 调用基于命令性代码的验证  
 基于命令性代码的验证为活动提供用于自身验证的简单方法，并且该方法可用于从 <xref:System.Activities.CodeActivity>、<xref:System.Activities.AsyncCodeActivity> 和 <xref:System.Activities.NativeActivity> 派生的活动。会向活动中添加确定所有验证错误或警告的验证代码。当在活动上调用验证时，这些警告或错误会包含在对 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 的调用而返回的集合中。在来自 [基本验证](../../../docs/framework/windows-workflow-foundation/samples/basic-validation.md) 示例的以下示例中，定义了一个 `CreateProduct` 活动。如果 `Cost` 大于 `Price`，则会向 <xref:System.Activities.CodeActivity.CacheMetadata%2A> 重写中的元数据添加一个验证错误。  
  
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
  
 在此示例中，使用 `CreateProduct` 活动配置工作流。在此工作流中，`Cost` 大于 `Price`，所需的 `Description` 参数不是集。 当调用验证时，将返回以下错误。  
  
```csharp  
Activity wf = new Sequence  
{  
    Activities =   
    {  
        new CreateProduct  
        {  
            Cost = 75.00,  
            Price = 55.00  
            // Cost > Price and required Description argument not set.  
        },  
        new WriteLine  
        {  
            Text = "Product added."  
        }  
    }  
};  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
  
```  
  
 **错误：成本必须是小于或等于价格。**   
**错误：未提供必要活动参数“Description”的值。**    
> [!NOTE]
>  自定义活动作者可以在活动的 <xref:System.Activities.CodeActivity.CacheMetadata%2A> 重写中提供验证逻辑。由 <xref:System.Activities.CodeActivity.CacheMetadata%2A> 引发的异常不会视为验证错误。这些异常将从对 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 的调用中逃离，因而必须由调用方进行处理。  
  
## 使用 ValidationSettings  
 默认情况下，当 <xref:System.Activities.Validation.ActivityValidationServices> 调用验证时，将计算活动树中的所有活动。<xref:System.Activities.Validation.ValidationSettings> 允许通过配置其三个属性，采用多种不同方法来自定义验证。<xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A> 指定验证程序是应遍历整个活动树，还是仅向提供的活动应用验证逻辑。 此值的默认值是 `false`。<xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> 指定从类型映射到约束列表的其他约束。对于计算的活动树中的每个活动的基类型，将查找 <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>。如果找到匹配的约束列表，则会针对活动计算该列表中的所有约束。<xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> 指定验证程序是应计算所有约束还是仅计算 <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> 中指定的约束。默认值为 `false`。<xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> 和 <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> 有助于工作流主机作者为工作流添加其他验证，例如，适用于 FxCop 等工具的策略约束。有关 [!INCLUDE[crabout](../../../includes/crabout-md.md)] 约束，请参见 [声明性约束](../../../docs/framework/windows-workflow-foundation//declarative-constraints.md)。  
  
 若要使用 <xref:System.Activities.Validation.ValidationSettings>，请配置所需属性，然后在调用 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 时传递这些属性。在此示例中，将验证由包含自定义 `Add` 活动的 <xref:System.Activities.Statements.Sequence> 组成的工作流。`Add` 活动具有两个必需参数。  
  
```csharp  
public sealed class Add : CodeActivity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Operand1 { get; set; }  
  
    [RequiredArgument]  
    public InArgument<int> Operand2 { get; set; }  
  
    protected override int Execute(CodeActivityContext context)  
    {  
        return Operand1.Get(context) + Operand2.Get(context);  
    }  
}  
```  
  
 下面的 `Add` 活动在 <xref:System.Activities.Statements.Sequence> 中使用，但未绑定该活动的两个必需参数。  
  
```csharp  
Variable<int> Operand1 = new Variable<int> { Default = 10 };  
Variable<int> Operand2 = new Variable<int> { Default = 15 };  
Variable<int> Result = new Variable<int>();  
  
Activity wf = new Sequence  
{  
    Variables = { Operand1, Operand2, Result },  
    Activities =   
    {  
        new Add(),  
        new WriteLine  
        {  
            Text = new InArgument<string>(env => "The result is " + Result.Get(env))  
        }  
    }  
};  
```  
  
 在下面的示例中，将执行验证，并将 <xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A> 设置为 `true`，以便仅验证 <xref:System.Activities.Statements.Sequence> 根活动。  
  
```csharp  
ValidationSettings settings = new ValidationSettings  
{  
    SingleLevel = true  
};  
  
ValidationResults results = ActivityValidationServices.Validate(wf, settings);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 此代码显示以下输出内容：  
  
 **没有警告或错误** 尽管未绑定 `Add` 活动的必需参数，但验证仍成功完成，这是因为仅计算了根活动。此验证类型对于只验证活动树中的特定元素非常有用，例如，在设计器中验证单个活动的属性更改。请注意，如果将调用此工作流，将计算在工作流中配置的完全验证，并且将引发 <xref:System.Activities.InvalidWorkflowException>。<xref:System.Activities.Validation.ActivityValidationServices> 和 <xref:System.Activities.Validation.ValidationSettings> 仅配置主机显式调用的验证，而不会配置在调用工作流时所执行的验证。