---
title: "使用配置文件配置服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "配置服务 [WCF]"
ms.assetid: c9c8cd32-2c9d-4541-ad0d-16dff6bd2a00
caps.latest.revision: 29
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# 使用配置文件配置服务
通过使用配置文件配置 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务，可提供在部署时而非设计时提供终结点和服务行为数据的灵活性。 本主题概述了当前可用的主要技术。  
  
 可使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 配置技术对 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 服务进行配置。 通常情况下，向承载 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务的 Internet 信息服务 \(IIS\) 网站的 Web.config 文件添加 XML 元素。 通过这些元素，可以逐台计算机更改详细信息，例如终结点地址（用于与服务进行通信的实际地址）。 此外，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 包括几个系统提供的元素，可用于快速选择服务的最基本的功能。 从 [!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)] 开始，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 附带一个新的默认配置模型，该模型简化了 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 配置要求。 如果您没有为特定服务提供任何 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 配置，运行时将自动使用一些标准终结点和默认绑定\/行为配置您的服务。 实际上，编写配置是 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 应用程序编程的主要部分。  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [为服务配置绑定](../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md).[!INCLUDE[crlist](../../../includes/crlist-md.md)]最常使用的元素的列表，请参阅[系统提供的绑定](../../../docs/framework/wcf/system-provided-bindings.md)。[!INCLUDE[crabout](../../../includes/crabout-md.md)]默认终结点、绑定和行为，请参阅[简化配置](../../../docs/framework/wcf/simplified-configuration.md)和 [WCF 服务的简化配置](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)。  
  
> [!IMPORTANT]
>  在部署并行方案（其中部署了服务的两个不同版本）时，必须指定配置文件中引用的程序集的部分名称。 这是因为配置文件将在服务的所有版本间共享，并可在不同版本的 .NET Framework 下运行。  
  
## System.Configuration：Web.config 和 App.config  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 的 System.Configuration 配置系统。  
  
 在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中配置服务时，使用 Web.config 文件或 App.config 文件指定设置。 配置文件名称的选择由为服务选择的宿主环境确定。 如果正在使用 IIS 来承载服务，则使用 Web.config 文件。 如果正在使用任何其他宿主环境，则使用 App.config 文件。  
  
 在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中，名为 App.config 的文件可用于创建最终的配置文件。 实际用于配置的最终名称取决于程序集名称。 例如，名为“Cohowinery.exe”的程序集具有的最终配置文件名称为“Cohowinery.exe.config”。 但是，只需要修改 App.config 文件。 在编译时，对该文件所做的更改会自动应用于最终应用程序配置文件。  
  
 在使用 App.config 文件的过程中，当应用程序启动并应用配置时，文件配置系统会将 App.config 文件与 Machine.config 文件的内容合并。 此机制允许在 Machine.config 文件中定义计算机范围的设置。 可以使用 App.config 文件重写 Machine.config 文件的设置；也可以锁定 Machine.config 文件中的设置以应用它们。 对于 Web.config，配置系统会将应用程序目录之下的所有目录中的 Web.config 文件合并到要应用的配置中。[!INCLUDE[crabout](../../../includes/crabout-md.md)]配置和设置属性的更多信息，请参见 <xref:System.Configuration> 命名空间中的主题。  
  
## 配置文件的主要部分  
 配置文件中的主要部分包括以下元素。  
  
```  
<system.ServiceModel>  
  
   <services>  
   <!—- Define the service endpoints. This section is optional in the new  
    default configuration model in .NET Framework 4. -->  
      <service>  
         <endpoint/>  
      </service>  
   </services>  
  
   <bindings>  
   <!-- Specify one or more of the system-provided binding elements,  
    for example, <basicHttpBinding> -->   
   <!-- Alternatively, <customBinding> elements. -->  
      <binding>  
      <!-- For example, a <BasicHttpBinding> element. -->  
      </binding>  
   </bindings>  
  
   <behaviors>  
   <!-- One or more of the system-provided or custom behavior elements. -->  
      <behavior>  
      <!-- For example, a <throttling> element. -->  
      </behavior>  
   </behaviors>  
  
</system.ServiceModel>  
```  
  
> [!NOTE]
>  绑定部分和行为部分是可选的，只在需要时才包括。  
  
### \<services\> 元素  
 `services` 元素包含应用程序承载的所有服务的规范。 从 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 中的简化配置模型开始，此部分是可选的。  
  
 [\<服务\>](../../../docs/framework/configure-apps/file-schema/wcf/services.md)  
  
### \<service\> 元素  
 每个服务都具有以下属性：  
  
-   `name`。 指定提供服务协定的实现的类型。 这是完全限定名称，其中包含命名空间、句点和类型名称。 例如，`"MyNameSpace.myServiceType"`。  
  
-   `behaviorConfiguration`。 指定一个在 `behavior` 元素中找到的 `behaviors` 元素的名称。 指定的行为控制操作，例如服务是否允许模拟。 如果它的值是空的，或者未提供任何 `behaviorConfiguration`，则向服务中添加默认服务行为集。  
  
-   [\<service\>](../../../docs/framework/configure-apps/file-schema/wcf/service.md)  
  
### \<endpoint\> 元素  
 每个终结点都需要以下属性表示的地址、绑定和协定：  
  
-   `address`。 指定服务的统一资源标识符 \(URI\)，它可以是一个绝对地址，或是一个相对于服务基址给定的地址。 如果设置为空字符串，则指示在创建服务的 <xref:System.ServiceModel.ServiceHost> 时，终结点在指定的基址上可用。  
  
-   `binding`。 通常，指定一个类似 <xref:System.ServiceModel.WsHttpBinding> 的系统提供的绑定，但也可以指定一个用户定义的绑定。 指定的绑定确定传输协议类型、安全和使用的编码，以及是否支持或启用可靠会话、事务或流。  
  
-   `bindingConfiguration`。 如果必须修改绑定的默认值，则可通过在 `binding` 元素中配置相应的 `bindings` 元素来执行此操作。 此属性应赋予与用于更改默认值的 `name` 元素的 `binding` 属性相同的值。 如果未提供任何名称，或者在绑定中未指定任何 `bindingConfiguration`，则在终结点中使用绑定类型的默认绑定。  
  
-   `contract`。 指定定义协定的接口。 这是在由 `name` 元素的 `service` 属性指定的公共语言运行库 \(CLR\) 类型中实现的接口。  
  
-   [\<endpoint\> element reference](http://msdn.microsoft.com/zh-cn/13aa23b7-2f08-4add-8dbf-a99f8127c017)  
  
### \<bindings\> 元素  
 `bindings` 元素包含可由任何服务中定义的任何终结点使用的所有绑定的规范。  
  
 [\<绑定\>](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)  
  
### \<binding\> 元素  
 `bindings` 元素中包含的 `binding` 元素可以是系统提供的绑定之一（请参阅[系统提供的绑定](../../../docs/framework/wcf/system-provided-bindings.md)），也可以是自定义绑定（请参阅[自定义绑定](../../../docs/framework/wcf/extending/custom-bindings.md)）。`binding` 元素具有 `name` 属性，此属性将绑定与 `bindingConfiguration` 元素的 `endpoint` 属性中指定的终结点相关联。 如果未指定任何名称，则该绑定对应于该绑定类型的默认值。  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)]配置服务和客户端，请参阅[Configuring Windows Communication Foundation Applications](http://msdn.microsoft.com/zh-cn/13cb368e-88d4-4c61-8eed-2af0361c6d7a)。  
  
 [\<绑定\>](../../../docs/framework/misc/binding.md)  
  
### \<behaviors\> 元素  
 这是定义服务行为的 `behavior` 元素的容器元素。  
  
 [\<行为\>](../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)  
  
### \<behavior\> 元素  
 每个 `behavior` 元素均由 `name` 属性进行标识，并提供系统提供的行为（例如 \<`throttling`\>）或自定义行为。 如果未提供任何名称，则该行为元素对应于默认服务或终结点行为。  
  
 [\<行为\>](../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md)  
  
## 如何使用绑定和行为配置  
 在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 中，通过在配置中使用引用系统，可以很方便地在终结点之间共享配置。 与绑定相关的配置值在 `bindingConfiguration` 部分的 `<binding>` 元素中进行分组，而不是直接将配置值分配到终结点。 绑定配置是一组命名的绑定设置。 然后，终结点可以通过名称来引用 `bindingConfiguration`。  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
 <system.serviceModel>  
  <bindings>  
    <basicHttpBinding>  
     <binding name="myBindingConfiguration1" closeTimeout="00:01:00" />  
     <binding name="myBindingConfiguration2" closeTimeout="00:02:00" />  
     <binding closeTimeout="00:03:00" />  <!—- Default binding for basicHttpBinding -->  
    </basicHttpBinding>  
     </bindings>  
     <services>  
      <service name="MyNamespace.myServiceType">  
       <endpoint   
          address="myAddress" binding="basicHttpBinding"   
          bindingConfiguration="myBindingConfiguration1"  
          contract="MyContract"  />  
       <endpoint   
          address="myAddress2" binding="basicHttpBinding"   
          bindingConfiguration="myBindingConfiguration2"  
          contract="MyContract" />  
       <endpoint   
          address="myAddress3" binding="basicHttpBinding"   
          contract="MyContract" />  
       </service>  
      </services>  
    </system.serviceModel>  
</configuration>  
```  
  
 在 `name` 元素中设置 `bindingConfiguration` 的 `<binding>`。`name` 必须是绑定类型（在本例中为 [\<basicHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)）范围中的唯一字符串，或者是引用默认绑定的空值。 通过将 `bindingConfiguration` 属性设置为此字符串，终结点链接到该配置。  
  
 以相同方式实现 `behaviorConfiguration`，如以下示例中所示。  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="myBehavior">  
           <callbackDebug includeExceptionDetailInFaults="true" />  
         </behavior>  
      </endpointBehaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="true" />  
        </behavior>  
      </serviceBehaviors>  
  
    </behaviors>  
    <services>  
     <service name="NewServiceType">  
       <endpoint   
          address="myAddress3" behaviorConfiguration="myBehavior"  
          binding="basicHttpBinding"  
          contract=”MyContract” />  
      </service>  
    </services>  
   </system.serviceModel>  
</configuration>  
```  
  
 请注意，向服务中添加了默认服务行为集。 此系统允许终结点共享公共配置而不用重新定义设置。 如果需要计算机范围，则在 Machine.config 中创建绑定或行为配置。 配置设置在所有 App.config 文件中可用。 通过[配置编辑器工具 \(SvcConfigEditor.exe\)](../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md) 可以很方便地创建配置。  
  
## 行为合并  
 当您需要统一使用一组公共行为时，利用行为合并功能，可更加轻松地管理行为。 此功能允许您在配置层次结构的各个层上指定行为，并使服务能够从配置层次结构的多个层继承行为。 为了演示此功能的工作方式，假定您的 IIS 中包含以下虚拟目录布局：  
  
 ~\\Web.config~\\Service.svc~\\Child\\Web.config~\\Child\\Service.svc  
  
 ~\\Web.config 文件包含以下内容：  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceDebug includeExceptionDetailInFaults="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 具有一个位于 ~\\Child\\Web.config 并包含以下内容的子 Web.config：  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 位于 ~\\Child\\Service.svc 的服务的行为如同该服务具有 serviceDebug 和 serviceMetadata 行为一样。 位于 ~\\Service.svc 的服务只具有 serviceDebug 行为。 发生的情况是，名称相同的两个行为集合（此情况下为空字符串）将合并。  
  
 也可使用 \<clear\> 标记来清除行为集合，使用 \<remove\> 标记从集合中移除各个行为。 例如，子服务中的以下两个配置结果只具有 serviceMetadata 行为：  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <remove name="serviceDebug"/>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <clear/>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 对无名称行为集合执行行为合并（如上所示），并对命名行为集合执行行为合并。  
  
 行为合并在 IIS 宿主环境中进行，在该环境中，Web.config 文件将以分层方式与根 Web.config 文件和 machine.config 合并。 但行为合并也可在应用程序环境中进行，在该环境中，machine.config 可与 App.config 文件合并。  
  
 行为合并适用于配置中的终结点行为和服务行为。  
  
 如果子行为集合包含一个已显示在父行为集合中的行为，则子行为将重写父行为。 因此，如果父行为集合具有 `<serviceMetadata httpGetEnabled="False" />`，而子行为集合具有 `<serviceMetadata httpGetEnabled="True" />`，则子行为将重写行为集合中的父行为并且 httpGetEnabled 将为“true”。  
  
## 请参阅  
 [简化配置](../../../docs/framework/wcf/simplified-configuration.md)   
 [Configuring Windows Communication Foundation Applications](http://msdn.microsoft.com/zh-cn/13cb368e-88d4-4c61-8eed-2af0361c6d7a)   
 [\<service\>](../../../docs/framework/configure-apps/file-schema/wcf/service.md)   
 [\<绑定\>](../../../docs/framework/misc/binding.md)