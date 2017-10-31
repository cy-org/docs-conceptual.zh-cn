---
title: "带自定义类型的切换活动的用法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 482a48c4-eb83-40c3-a4e2-2f9a8af88b75
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 带自定义类型的切换活动的用法
此示例介绍如何使 <xref:System.Activities.> Statements.Switch`1?qualifyHint=False&autoUpgrade=True 活动能够在运行时计算用户定义的复杂类型。在大多数传统的过程性编程语言中，[switch](http://go.microsoft.com/fwlink/?LinkId=180521) 语句会根据变量的条件评估来选择执行逻辑。传统上，`switch` 语句会操作可静态计算的表达式。例如，在 C\# 中，这表示仅支持基元类型（如 <xref:System.Boolean>、<xref:System.Int32>、<xref:System.String>）和枚举类型。  
  
 若要启用针对自定义类的切换，则必须实现逻辑以在运行时计算自定义复杂类型的值。此示例演示如何启用针对名为 `Person` 的自定义复杂类型的切换。  
  
-   在自定义类 `Person` 中，使用自定义 <xref:System.ComponentModel.TypeConverter> 的名称声明 <xref:System.ComponentModel.TypeConverter> 特性。  
  
    ```  
    [TypeConverter(typeof(PersonConverter))]  
    public class Person  
    {  
       public string Name { get; set; }  
       public int Age { get; set; }  
    ...  
  
    ```  
  
-   在自定义类 `Person` 中，重写 <xref:System.Object.Equals%2A> 和 <xref:System.Object.GetHashCode%2A> 类。  
  
    ```  
    public override bool Equals(object obj)  
    {  
        Person person = obj as Person;  
  
        if (person != null)  
        {  
            return string.Equals(this.Name, person.Name);  
        }  
  
        return false;  
    }  
  
    public override int GetHashCode()  
    {  
        if (this.Name != null)  
        {  
            return this.Name.GetHashCode();  
        }  
  
        return 0;  
    }  
  
    ```  
  
-   实现自定义 <xref:System.ComponentModel.TypeConverter> 类，这将执行自定义类的实例与字符串之间的相互转换。  
  
    ```  
    public class PersonConverter : TypeConverter  
    {  
        public override bool CanConvertFrom(ITypeDescriptorContext context,  
           Type sourceType)  
        {  
            return (sourceType is string);  
        }  
  
        // Overrides the ConvertFrom method of TypeConverter.  
        public override object ConvertFrom(ITypeDescriptorContext context,  
           CultureInfo culture, object value)  
        {  
            if (value == null)  
            {  
                return null;  
            }  
  
            if (value is string)  
            {  
                return new Person  
                {  
                    Name = (string)value  
                };  
            }  
  
            return base.ConvertFrom(context, culture, value);  
        }  
  
        // Overrides the ConvertTo method of TypeConverter.  
        public override object ConvertTo(ITypeDescriptorContext context,  
           CultureInfo culture, object value, Type destinationType)  
        {  
            if (destinationType == typeof(string))  
            {  
                if (value != null)  
                {  
                    return ((Person) value).Name;  
                }  
                else  
                {  
                    return null;  
                }  
            }  
  
            return base.ConvertTo(context, culture, value, destinationType);  
        }  
    }  
    ```  
  
 此示例中包括以下文件：  
  
-   **Person.cs**：定义 `Person` 类。  
  
-   **PersonConverter.cs**：`Person` 类的类型转换器。  
  
-   **Sequence.xaml**：基于 `Person` 类型进行切换的工作流。  
  
-   **Program.cs**：运行工作流的主函数。  
  
#### 使用此示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中加载 Switch.sln。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案。  
  
3.  按 Ctrl\+F5 运行示例。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Built-InActivities\Switch`  
  
## 请参阅  
 [内置活动库](../../../../docs/framework/windows-workflow-foundation//net-framework-4-5-built-in-activity-library.md)