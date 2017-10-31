---
title: "协定优先工具 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a880690-f460-4475-a5f4-9f91ce08fcc6
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 协定优先工具
服务合同往往需要从现有的服务创建。在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]，使用协定优先工具从现有的服务可以自动创建数据合同类。要使用协定优先工具，必须下载本地XML架构定义 \(XSD\) 文件；该工具无法通过 HTTP 的合同导入远程数据。  
  
 协定优先工具集成到[!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)]作为生成任务。版本任务生成的代码文件创建每时间生成项目时，以使项目可以轻松地通过基础服务合同中的更改。  
  
 协定优先工具可以导入的架构类型包括如下：  
  
```  
<xsd:complexType>  
<xsd:simpleType>  
```  
  
 如果他们是基元值，例如，将不会生成简单类型`Int16` 或  `String`；如果它们的类型将不会生成复杂类型 `Collection`。类型也不会生成如果它们的另一部分 `xsd:complexType`.在所有这些情况下，将转而向现有项目中的类型引用类型。  
  
## 向项目中添加数据协定  
 使用协定优先工具之前，服务合同 \(XSD\) 必须添加到项目中。出于本概述的需要，以下的合同将用于说明合同协定优先函数。此服务的定义是 Bing 的搜索API所使用的服务合同的小子集。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="ServiceSchema"  
    targetNamespace="http://tempuri.org/ServiceSchema.xsd"  
    elementFormDefault="qualified"  
    xmlns="http://tempuri.org/ServiceSchema.xsd"  
    xmlns:mstns="http://tempuri.org/ServiceSchema.xsd"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema"  
>  
  <xs:complexType name="SearchRequest">  
    <xs:sequence>  
      <xs:element minOccurs="0" maxOccurs="1" name="Version" type="xs:string" default="2.2" />  
      <xs:element minOccurs="0" maxOccurs="1" name="Market" type="xs:string" />  
      <xs:element minOccurs="0" maxOccurs="1" name="UILanguage" type="xs:string" />  
      <xs:element minOccurs="1" maxOccurs="1" name="Query" type="xs:string" />  
      <xs:element minOccurs="1" maxOccurs="1" name="AppId" type="xs:string" />  
      <xs:element minOccurs="0" maxOccurs="1" name="Latitude" type="xs:double" />  
      <xs:element minOccurs="0" maxOccurs="1" name="Longitude" type="xs:double" />  
      <xs:element minOccurs="0" maxOccurs="1" name="Radius" type="xs:double" />  
    </xs:sequence>  
  </xs:complexType>  
  <xs:simpleType name="WebSearchOption">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="DisableHostCollapsing" />  
      <xs:enumeration value="DisableQueryAlterations" />  
    </xs:restriction>  
  </xs:simpleType>  
</xs:schema>  
  
```  
  
 要向项目添加上述服务合同，右键单击项目，然后选择**“添加新航程”**.从 WCF 窗格的模板对话框中，选择架构定义和命名新文件 SampleContract.xsd。复制和并粘贴上面的代码到代码视图新文件。  
  
## 配置协定优先选项  
 协定优先选项可以在属性菜单的[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]项目中配置。要启用协定优先开发，选择**“启用 XSD 作为类型语言定义”**复选框的 WCF 页中的项目属性窗口。  
  
 ![显示协定优先的 WCF 项目选项](../../../docs/framework/wcf/media/contractfirstoptions.png "ContractFirstOptions")  
  
 要配置高级的属性，请单击高级按钮。  
  
 ![高级协定优先属性](../../../docs/framework/wcf/media/contractfirstadvanced.png "ContractFirstAdvanced")  
  
 下列高级设置可以从协定配置用于代码生成。设置只可为项目中的所有文件的配置设置；此时不能为所有为单独的文件配置设置。  
  
-   **“序列化程序模式”**：此设置确定哪些序列化程序用于读取服务协定文件。当选定 **“XML序列化程序”**，**“集合类型”** 和 **“重用类型”**选项将被禁用。这些选项仅适用于**“数据合同的序列化程序”**。  
  
-   **“重用类型”**：此设置指定哪些库用于类型重用。此设置只适用于**“序列化程序模式”** 设置为 **“数据协定序列化程序”**。  
  
-   **“集合类型”**：此设置指定完全限定或程序集限定使用数据类型的集合的类型。此设置只适用于**“序列化程序模式”** 设置为 **“数据协定序列化程序”**。  
  
-   **“字典类型”**：此设置指定完全限定或程序集限定使用数据类型的字典的类型。  
  
-   **EnableDataBinding**：此设置用于指定是否执行 <xref:System.ComponentModel.INotifyPropertyChanged>上所有数据类型执行数据绑定接口。  
  
-   **ExcludedTypes**：此设置指定完全限定的列表或程序集限定要排除从引用的程序集的类型。此设置只适用于**“序列化程序模式”** 设置为 **“数据协定序列化程序”**。  
  
-   **GenerateInternalTypes**：此设置用于指定是否生成标记为内部的类。此设置只适用于**“序列化程序模式”** 设置为 **“数据协定序列化程序”**。  
  
-   **GenerateSerializableTypes**：此设置指定是否生成具有类 <xref:System.SerializableAttribute> 属性。此设置只适用于**“序列化程序模式”** 设置为 **“数据协定序列化程序”**。  
  
-   **ImportXMLTypes**：此设置指定是否配置数据协定序列化程序应用 <xref:System.SerializableAttribute> 属性应用到无类 <xref:System.Runtime.Serialization.DataContractAttribute>属性。此设置只适用于**“序列化程序模式”** 设置为 **“数据协定序列化程序”**。  
  
-   **SupportFx35TypedDataSets**：此设置指定是否为 Net Framework 3.5 创建类型化数据集提供附加功能。当**“序列化程序模式”** 设置为 **“XML序列化程序”**、<xref:System.Data.Design.TypedDataSetSchemaImporterExtensionFx35> 此值集设置为 True 时将添加到 XML 架构导入程序扩展名。当**“序列化程序模式”** 设置为 **“数据协定序列化程序”**，类型 <xref:System.DateTimeOffset>时，该值集设置为 False，将从引用排除，使 [DateTimeOffset](assetId:///DateTimeOffset?qualifyHint=False&amp;autoUpgrade=True) 总是为旧框架版本生成。  
  
-   **InputXsdFiles**：此设置指定的输入文件的列表。每个文件都必须包含有效的 XML 架构。  
  
-   **“语言”**：此设置指定生成的协定代码的语言。该设置必须为 <xref:System.CodeDom.Compiler.CodeDomProvider> 所识别。  
  
-   **NamespaceMappings**：此设置指定 CLR 命名空间的从 XSD 目标命名空间的映射。每个映射应使用以下格式：  
  
    ```xml  
    “<Schema Namespace>, <CLR Namespace>”  
    ```  
  
     XML 序列化程序只接受以下列格式一个映射：  
  
    ```xml  
    “*, <CLR Namespace>”  
    ```  
  
-   **“输出目录”**：此设置指定将生成的代码文件的目录。  
  
 这些设置将用于生成项目时，可从服务协定文件生成服务协定类型。  
  
## 使用协定优先开发  
 向项目中添加的服务协定后和确认生成设置，按 **“F6”** 生成项目。服务协定中定义的类型，然后将可在项目中使用。  
  
 若要使用服务协定中定义的类型，添加的引用 `ContractTypes` 根据当前命名空间：  
  
```csharp  
using MyProjectNamespace.ContractTypes;  
```  
  
 服务协定中定义的类型，然后将可在项目中可解析，如下所示。  
  
 ![使用从服务协定派生的类型](../../../docs/framework/wcf/media/contractfirsttypes.png "ContractFirstTypes")  
  
 在 GeneratedXSDTypes.cs 文件中创建工具生成的类型。目录默认情况下，在创建文件的 \<项目目录\>\/obj\/\< 版本配置 \>\/XSDGeneratedCode\/。在本主题开头的示例架构转换，如下所示：  
  
```scr  
//------------------------------------------------------------------------------  
// <auto-generated>  
//     This code was generated by a tool.  
//     Runtime Version:4.0.30319.17330  
//  
//     Changes to this file may cause incorrect behavior and will be lost if  
//     the code is regenerated.  
// </auto-generated>  
//------------------------------------------------------------------------------  
  
namespace TestXSD3.ContractTypes  
{  
    using System.Xml.Serialization;  
  
    /// <remarks/>  
    [System.CodeDom.Compiler.GeneratedCodeAttribute("System.Xml", "4.0.30319.17330")]  
    [System.SerializableAttribute()]  
    [System.Diagnostics.DebuggerStepThroughAttribute()]  
    [System.ComponentModel.DesignerCategoryAttribute("code")]  
    [System.Xml.Serialization.XmlTypeAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd")]  
    [System.Xml.Serialization.XmlRootAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd", IsNullable=true)]  
    public partial class SearchRequest  
    {  
  
        private string versionField;  
  
        private string marketField;  
  
        private string uILanguageField;  
  
        private string queryField;  
  
        private string appIdField;  
  
        private double latitudeField;  
  
        private bool latitudeFieldSpecified;  
  
        private double longitudeField;  
  
        private bool longitudeFieldSpecified;  
  
        private double radiusField;  
  
        private bool radiusFieldSpecified;  
  
        public SearchRequest()  
        {  
            this.versionField = "2.2";  
        }  
  
        /// <remarks/>  
        [System.ComponentModel.DefaultValueAttribute("2.2")]  
        public string Version  
        {  
            get  
            {  
                return this.versionField;  
            }  
            set  
            {  
                this.versionField = value;  
            }  
        }  
  
        /// <remarks/>  
        public string Market  
        {  
            get  
            {  
                return this.marketField;  
            }  
            set  
            {  
                this.marketField = value;  
            }  
        }  
  
        /// <remarks/>  
        public string UILanguage  
        {  
            get  
            {  
                return this.uILanguageField;  
            }  
            set  
            {  
                this.uILanguageField = value;  
            }  
        }  
  
        /// <remarks/>  
        public string Query  
        {  
            get  
            {  
                return this.queryField;  
            }  
            set  
            {  
                this.queryField = value;  
            }  
        }  
  
        /// <remarks/>  
        public string AppId  
        {  
            get  
            {  
                return this.appIdField;  
            }  
            set  
            {  
                this.appIdField = value;  
            }  
        }  
  
        /// <remarks/>  
        public double Latitude  
        {  
            get  
            {  
                return this.latitudeField;  
            }  
            set  
            {  
                this.latitudeField = value;  
            }  
        }  
  
        /// <remarks/>  
        [System.Xml.Serialization.XmlIgnoreAttribute()]  
        public bool LatitudeSpecified  
        {  
            get  
            {  
                return this.latitudeFieldSpecified;  
            }  
            set  
            {  
                this.latitudeFieldSpecified = value;  
            }  
        }  
  
        /// <remarks/>  
        public double Longitude  
        {  
            get  
            {  
                return this.longitudeField;  
            }  
            set  
            {  
                this.longitudeField = value;  
            }  
        }  
  
        /// <remarks/>  
        [System.Xml.Serialization.XmlIgnoreAttribute()]  
        public bool LongitudeSpecified  
        {  
            get  
            {  
                return this.longitudeFieldSpecified;  
            }  
            set  
            {  
                this.longitudeFieldSpecified = value;  
            }  
        }  
  
        /// <remarks/>  
        public double Radius  
        {  
            get  
            {  
                return this.radiusField;  
            }  
            set  
            {  
                this.radiusField = value;  
            }  
        }  
  
        /// <remarks/>  
        [System.Xml.Serialization.XmlIgnoreAttribute()]  
        public bool RadiusSpecified  
        {  
            get  
            {  
                return this.radiusFieldSpecified;  
            }  
            set  
            {  
                this.radiusFieldSpecified = value;  
            }  
        }  
    }  
  
    /// <remarks/>  
    [System.CodeDom.Compiler.GeneratedCodeAttribute("System.Xml", "4.0.30319.17330")]  
    [System.SerializableAttribute()]  
    [System.Xml.Serialization.XmlTypeAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd")]  
    [System.Xml.Serialization.XmlRootAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd", IsNullable=false)]  
    public enum WebSearchOption  
    {  
  
        /// <remarks/>  
        DisableHostCollapsing,  
  
        /// <remarks/>  
        DisableQueryAlterations,  
    }  
}  
  
```  
  
## 错误和警告  
 错误和警告时遇到分析 XSD 架构中将显示为生成的错误和警告。  
  
## 接口继承  
 使用接口继承在协定优先的开发下是不可能的；这和接口在其它操作中行为方式一致。为了使用接口继承基接口,使用两个单独的终结点。第一个终结点使用继承协定，第二个终结点实现基接口。