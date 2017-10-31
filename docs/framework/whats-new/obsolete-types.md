---
title: ".NET Framework 中的过时类型"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- .NET Framework 4.5, obsolete types
- types, obsolete in .NET Framework 4.5
- obsolete types [.NET Framework]
ms.assetid: e636d024-0fac-45eb-b721-25a8c0ceca8f
caps.latest.revision: 41
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 15ab48dedaef24ea209c38939ee87a0321da55cf
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="obsolete-types-in-the-net-framework"></a>.NET Framework 中的过时类型
<a name="introduction"></a>本文中的表格列出了 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 和 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 中由程序集组织的过时的类型。 使用以下链接可查看每个程序集中过时的类型和建议的备选项的列表。 由于这些类型已过时，因此其所有成员也已过时。 有关 .NET Framework 类库中其他过时成员的列表，请参阅[过时成员](../../../docs/framework/whats-new/obsolete-members.md)。  
  
-   [系统程序集中的过时类型](#obsolete_types_in_system_assemblies)  
  
    -   [mscorlib.dll](#mscorlib)  
  
    -   [System.Core.dll](#Core)  
  
    -   [System.Data.dll](#data)  
  
    -   [System.Data.OracleClient.dll](#oracleclient)  
  
    -   [System.Design.dll](#design)  
  
    -   [System.dll](#system)  
  
    -   [System.EnterpriseServices.dll](#enterpriseservices)  
  
    -   [System.Net.dll](#net)  
  
    -   [System.ServiceModel.dll](#servicemodel)  
  
    -   [System.Web.dll](#web)  
  
    -   [System.Web.Mobile.dll](#mobile)  
  
    -   [System.Workflow.Activities.dll](#workflow_activities)  
  
    -   [System.Workflow.ComponentModel.dll](#workflow_componentmodel)  
  
    -   [System.Workflow.Runtime.dll](#workflow_runtime)  
  
    -   [System.WorkflowServices.dll](#workflowservices)  
  
    -   [System.Xaml.dll](#xaml)  
  
    -   [System.Xml.dll](#xml)  
  
    -   [WindowsBase.dll](#WindowsBase)  
  
-   [Microsoft 程序集中的过时类型](#obsolete_types_in_microsoft_assemblies)  
  
    -   [IEHost.dll and IEExec.exe](#IEHost)  
  
    -   [Microsoft.Build.Engine.dll](#Engine)  
  
    -   [Microsoft.JScript.dll](#jscript)  
  
    -   [Microsoft.VisualBasic.Compatibility.dll](#VBCompat)  
  
    -   [Microsoft.VisualBasic.Compatibility.Data.dll](#VBCompatData)  
  
    -   [Microsoft.VisualC.dll](#visualc)  
  
<a name="obsolete_types_in_system_assemblies"></a>   
## <a name="obsolete-types-in-system-assemblies"></a>系统程序集中的过时类型  
 以下各表列出了系统程序集中已声明为过时的类型。 这些程序集用于面向 .NET Framework 的通用\-应用程序开发。  
  
<a name="mscorlib"></a>   
### <a name="assembly-mscorlibdll"></a>程序集：mscorlib.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.ExecutionEngineException?displayProperty=fullName>|该类型以前指示运行时中未指定的错误。 由于运行时不再引发此异常，因此该类型已过时。|  
|<xref:System.Collections.CaseInsensitiveHashCodeProvider?displayProperty=fullName>|请改用 <xref:System.StringComparer?displayProperty=fullName>。|  
|<xref:System.Collections.IHashCodeProvider?displayProperty=fullName>|请改用 <xref:System.Collections.IEqualityComparer?displayProperty=fullName>。|  
|<xref:System.Configuration.Assemblies.AssemblyHash?displayProperty=fullName>|<xref:System.Configuration.Assemblies.AssemblyHash> 类已弃用。|  
|<xref:System.Diagnostics.Contracts.Internal.ContractHelper?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。 请改用 System.Runtime.CompilerServices 命名空间中的 <xref:System.Runtime.CompilerServices.ContractHelper?displayProperty=fullName> 类。|  
|<xref:System.Reflection.Emit.UnmanagedMarshal?displayProperty=fullName>|备用 API 可用：改为发出 <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=fullName> 自定义特性。|  
|<xref:System.Runtime.InteropServices.BIND_OPTS?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.BIND_OPTS?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.BINDPTR?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.BINDPTR?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.CALLCONV?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.CALLCONV?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.CONNECTDATA?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.CONNECTDATA?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.DESCKIND?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.DESCKIND?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.DISPPARAMS?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.DISPPARAMS?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.ELEMDESC?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.ELEMDESC?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.EXCEPINFO?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.EXCEPINFO?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.FILETIME?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.FILETIME?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.FUNCDESC?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.FUNCDESC?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.FUNCFLAGS?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.FUNCFLAGS?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.FUNCKIND?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.FUNCKIND?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.IDispatchImplAttribute?displayProperty=fullName>|此特性已弃用，并将从未来版本中移除。|  
|<xref:System.Runtime.InteropServices.IDispatchImplType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.IDispatchImplAttribute?displayProperty=fullName> 已弃用。|  
|<xref:System.Runtime.InteropServices.IDLDESC?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IDLDESC?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.IDLFLAG?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IDLFLAG?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.IMPLTYPEFLAGS?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IMPLTYPEFLAGS?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.INVOKEKIND?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.INVOKEKIND?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.LIBFLAGS?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.LIBFLAGS?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.PARAMDESC?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.PARAMDESC?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.PARAMFLAG?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.PARAMFLAG?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.SetWin32ContextInIDispatchAttribute?displayProperty=fullName>|此特性已弃用。 应用程序域不再考虑 IDispatch 调用中的激活上下文边界。|  
|<xref:System.Runtime.InteropServices.STATSTG?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.STATSTG?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.SYSKIND?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.SYSKIND?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.TYPEATTR?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.TYPEATTR?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.TYPEDESC?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.TYPEDESC?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.TYPEFLAGS?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.TYPEFLAGS?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.TYPEKIND?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.TYPEKIND?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.TYPELIBATTR?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.TYPELIBATTR?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIBindCtx?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IBindCtx?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIConnectionPoint?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIConnectionPointContainer?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIEnumConnectionPoints?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IEnumConnectionPoints?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIEnumConnections?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IEnumConnections?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIEnumMoniker?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IEnumMoniker?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIEnumString?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IEnumString?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIEnumVARIANT?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIMoniker?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IMoniker?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIPersistFile?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IPersistFile?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIRunningObjectTable?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IRunningObjectTable?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMIStream?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.IStream?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMITypeComp?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.ITypeComp?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMITypeInfo?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.UCOMITypeLib?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.ITypeLib?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.VARDESC?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.VARDESC?displayProperty=fullName> 。|  
|<xref:System.Runtime.InteropServices.VARFLAGS?displayProperty=fullName>|请改用 <xref:System.Runtime.InteropServices.ComTypes.VARFLAGS?displayProperty=fullName> 。|  
|<xref:System.Security.SecurityCriticalScope?displayProperty=fullName>|<xref:System.Security.SecurityCriticalScope> 仅用于实现 .NET 2.0 透明度兼容性。|  
|<xref:System.Security.SecurityTreatAsSafeAttribute?displayProperty=fullName>|<xref:System.Security.SecurityTreatAsSafeAttribute> 仅用于实现 .NET 2.0 透明度兼容性。 请改用 <xref:System.Security.SecuritySafeCriticalAttribute?displayProperty=fullName>。|  
|<xref:System.Security.Policy.FirstMatchCodeGroup?displayProperty=fullName>|此类型已过时，并将从 .NET Framework 的未来版本中移除。|  
|<xref:System.Security.Policy.PermissionRequestEvidence?displayProperty=fullName>|程序集级别声明性安全已过时，默认情况下不再由 CLR 强制实施。|  
|<xref:System.Security.Policy.UnionCodeGroup?displayProperty=fullName>|此类型已过时，并将从 .NET Framework 的未来版本中移除。|  
  
 [返回页首](#introduction)  
  
<a name="Core"></a>   
### <a name="assembly-systemcoredll"></a>程序集：System.Core.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.Runtime.CompilerServices.ExecutionScope?displayProperty=fullName>|使用此类型会生成编译器错误。<br /><br /> 不要使用此类型。|  
  
 [返回页首](#introduction)  
  
<a name="data"></a>   
### <a name="assembly-systemdatadll"></a>程序集：System.Data.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.Data.DataSysDescriptionAttribute?displayProperty=fullName>|<xref:System.Data.DataSysDescriptionAttribute> 已弃用。|  
|<xref:System.Data.PropertyAttributes?displayProperty=fullName>|<xref:System.Data.PropertyAttributes> 已弃用。|  
|<xref:System.Data.TypedDataSetGenerator?displayProperty=fullName>|将从未来版本中移除 <xref:System.Data.TypedDataSetGenerator> 类。 请使用 System.Design.dll 中的 <xref:System.Data.Design.TypedDataSetGenerator?displayProperty=fullName>。|  
|<xref:System.Xml.XmlDataDocument?displayProperty=fullName>|将从未来版本中移除 <xref:System.Xml.XmlDataDocument> 类。|  
  
 [返回页首](#introduction)  
  
<a name="oracleclient"></a>   
### <a name="assembly-systemdataoracleclientdll"></a>程序集：System.Data.OracleClient.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.Data.OracleClient.OracleClientFactory?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleClientFactory> 已弃用。|  
|<xref:System.Data.OracleClient.OracleCommand?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleCommand> 已弃用。|  
|<xref:System.Data.OracleClient.OracleCommandBuilder?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleCommandBuilder> 已弃用。|  
|<xref:System.Data.OracleClient.OracleConnection?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleConnection> 已弃用。|  
|<xref:System.Data.OracleClient.OracleConnectionStringBuilder?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleConnectionStringBuilder> 已弃用。|  
|<xref:System.Data.OracleClient.OracleDataAdapter?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleDataAdapter> 已弃用。|  
|<xref:System.Data.OracleClient.OraclePermission?displayProperty=fullName>|<xref:System.Data.OracleClient.OraclePermission> 已弃用。|  
|<xref:System.Data.OracleClient.OraclePermissionAttribute?displayProperty=fullName>|<xref:System.Data.OracleClient.OraclePermissionAttribute?displayProperty=fullName> 已弃用。|  
  
 [返回页首](#introduction)  
  
<a name="design"></a>   
### <a name="assembly-systemdesigndll"></a>程序集：System.Design.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.ComponentModel.Design.LocalizationExtenderProvider?displayProperty=fullName>|此类已弃用。 请改用 <xref:System.ComponentModel.Design.Serialization.CodeDomLocalizationProvider?displayProperty=fullName> 。|  
|<xref:System.Web.UI.Design.DataBindingCollectionConverter?displayProperty=fullName>|建议不要使用此类型，因为 DataBindings 编辑是通过 <xref:System.ComponentModel.Design.DesignerActionList?displayProperty=fullName> 而不是属性网格启动的。|  
|<xref:System.Web.UI.Design.DataBindingCollectionEditor?displayProperty=fullName>|建议不要使用此类型，因为 DataBindings 编辑是通过 <xref:System.ComponentModel.Design.DesignerActionList?displayProperty=fullName> 而不是属性网格启动的。|  
|<xref:System.Web.UI.Design.IControlDesignerBehavior?displayProperty=fullName>|建议的替代项为 <xref:System.Web.UI.Design.IControlDesignerTag?displayProperty=fullName> 和 <xref:System.Web.UI.Design.IControlDesignerView?displayProperty=fullName>。|  
|<xref:System.Web.UI.Design.IHtmlControlDesignerBehavior?displayProperty=fullName>|建议的替代项为 <xref:System.Web.UI.Design.IControlDesignerTag?displayProperty=fullName> 和 <xref:System.Web.UI.Design.IControlDesignerView?displayProperty=fullName>。|  
|<xref:System.Web.UI.Design.ITemplateEditingFrame?displayProperty=fullName>|建议不要使用此类型，因为模板编辑是在 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName> 中处理的。 若要支持模板编辑，请在 <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=fullName> 属性中公开模板数据，并调用 <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=fullName>。|  
|<xref:System.Web.UI.Design.IWebFormReferenceManager?displayProperty=fullName>|建议的替代项为 <xref:System.Web.UI.Design.WebFormsReferenceManager?displayProperty=fullName>。 <xref:System.Web.UI.Design.WebFormsReferenceManager> 包含其他功能并允许更大的扩展性。 若要获取 <xref:System.Web.UI.Design.WebFormsReferenceManager>，请使用 `RootDesigner.ReferenceManager` 中的 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName> 属性。|  
|<xref:System.Web.UI.Design.IWebFormsDocumentService?displayProperty=fullName>|建议的替代项为 <xref:System.Web.UI.Design.WebFormsRootDesigner?displayProperty=fullName>。 <xref:System.Web.UI.Design.WebFormsRootDesigner> 包含其他功能并允许更大的扩展性。 若要获取 <xref:System.Web.UI.Design.WebFormsRootDesigner>，请使用 <xref:System.Web.UI.Design.ControlDesigner.RootDesigner%2A> 中的 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName> 属性。|  
|<xref:System.Web.UI.Design.ITemplateEditingService?displayProperty=fullName>|建议不要使用此类型，因为模板编辑是在 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName> 中处理的。 若要支持模板编辑，请在 <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=fullName> 属性中公开模板数据，并调用 <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=fullName>。|  
|<xref:System.Web.UI.Design.ReadWriteControlDesigner?displayProperty=fullName>|建议的替代项为 <xref:System.Web.UI.Design.ContainerControlDesigner?displayProperty=fullName>，因为它使用 <xref:System.Web.UI.Design.EditableDesignerRegion?displayProperty=fullName> 来编辑内容。 利用设计器区域，可更好地控制正在编辑的内容。|  
|<xref:System.Web.UI.Design.TemplateEditingService?displayProperty=fullName>|建议不要使用此类型，因为模板编辑是在 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName> 中处理的。 若要支持模板编辑，请在 <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=fullName> 属性中公开模板数据，并调用 <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=fullName>。|  
|<xref:System.Web.UI.Design.TemplateEditingVerb?displayProperty=fullName>|建议不要使用此类型，因为模板编辑是在 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName> 中处理的。 若要支持模板编辑，请在 <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=fullName> 属性中公开模板数据，并调用 <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=fullName>。|  
|<xref:System.Web.UI.Design.WebControls.CalendarAutoFormatDialog?displayProperty=fullName>|建议不要使用此类型，因为 AutoFormat 对话框是由设计器宿主启动的。 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName> 属性中的 <xref:System.Web.UI.Design.ControlDesigner.AutoFormats%2A?displayProperty=fullName> 上公开了可用的 AutoFormat 的列表。|  
|<xref:System.Web.UI.Design.WebControls.PanelDesigner?displayProperty=fullName>|建议的替代项为 <xref:System.Web.UI.Design.WebControls.PanelContainerDesigner?displayProperty=fullName>，因为它使用 <xref:System.Web.UI.Design.EditableDesignerRegion?displayProperty=fullName> 来编辑内容。 利用设计器区域，可更好地控制正在编辑的内容。|  
  
 [返回页首](#introduction)  
  
<a name="system"></a>   
### <a name="assembly-systemdll"></a>程序集：System.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.ComponentModel.IComNativeDescriptorHandler?displayProperty=fullName>|此接口已弃用。 改为将 <xref:System.ComponentModel.TypeDescriptionProvider?displayProperty=fullName> 添加到句柄类型 <xref:System.ComponentModel.TypeDescriptor.ComObjectType%2A?displayProperty=fullName>。|  
|<xref:System.ComponentModel.RecommendedAsConfigurableAttribute?displayProperty=fullName>|改用 <xref:System.ComponentModel.SettingsBindableAttribute?displayProperty=fullName> 来处理新的设置模型。|  
|<xref:System.ComponentModel.Design.Serialization.RootDesignerSerializerAttribute?displayProperty=fullName>|此特性已弃用。 请改用 <xref:System.ComponentModel.Design.Serialization.DesignerSerializerAttribute?displayProperty=fullName>。 例如，若要为 CodeDom 指定根设计器，请使用 `DesignerSerializerAttribute\(...,typeof\(TypeCodeDomSerializer\)\)`。|  
|<xref:System.Diagnostics.DiagnosticsConfigurationHandler?displayProperty=fullName>|此类已弃用。|  
|<xref:System.Diagnostics.PerformanceCounterManager?displayProperty=fullName>|此类已弃用。 改为通过 <xref:System.Diagnostics.PerformanceCounter?displayProperty=fullName> 类使用性能计数器。|  
|<xref:System.Net.GlobalProxySelection?displayProperty=fullName>|此类已弃用。 请改用 <xref:System.Net.WebRequest.DefaultWebProxy%2A?displayProperty=fullName> 以访问和设置全局默认代理。 使用“null”而非 <xref:System.Net.GlobalProxySelection.GetEmptyWebProxy%2A?displayProperty=fullName>。|  
|<xref:System.Net.Sockets.SocketClientAccessPolicyProtocol?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 使用此类型会生成编译器错误。<br /><br /> 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
  
 [返回页首](#introduction)  
  
<a name="enterpriseservices"></a>   
### <a name="assembly-systementerpriseservicesdll"></a>程序集：System.EnterpriseServices.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.EnterpriseServices.RegistrationHelperTx?displayProperty=fullName>|<xref:System.EnterpriseServices.RegistrationHelperTx> 类已弃用。|  
  
 [返回页首](#introduction)  
  
<a name="net"></a>   
### <a name="assembly-systemnetdll"></a>程序集：System.Net.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.Net.INetworkProgress?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 使用此类型会生成编译器错误。<br /><br /> 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
|<xref:System.Net.IUnsafeWebRequestCreate?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 使用此类型会生成编译器错误。<br /><br /> 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
|<xref:System.Net.NetworkProgressChangedEventArgs?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 使用此类型会生成编译器错误。<br /><br /> 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
|<xref:System.Net.UiSynchronizationContext?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 使用此类型会生成编译器错误。<br /><br /> 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
|<xref:System.Net.Sockets.HttpPolicyDownloaderProtocol?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 使用此类型会生成编译器错误。<br /><br /> 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
|<xref:System.Net.Sockets.SecurityCriticalAction?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 使用此类型会生成编译器错误。<br /><br /> 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
|<xref:System.Net.Sockets.SocketPolicy?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 使用此类型会生成编译器错误。<br /><br /> 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
|<xref:System.Net.Sockets.UdpAnySourceMulticastClient?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 使用此类型会生成编译器错误。<br /><br /> 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
|<xref:System.Net.Sockets.UdpSingleSourceMulticastClient?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 使用此类型会生成编译器错误。<br /><br /> 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
  
 [返回页首](#introduction)  
  
<a name="servicemodel"></a>   
### <a name="assembly-systemservicemodeldll"></a>程序集：System.ServiceModel.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.ServiceModel.NetPeerTcpBinding?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 对等通道功能已过时，并将在以后删除。|  
|<xref:System.ServiceModel.Channels.HttpCookieContainerBindingElement?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 此类型已过时。 若要启用 Http <xref:System.Net.CookieContainer>，请在 Http 绑定或 `AllowCookies` 上使用 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 属性。|  
|<xref:System.ServiceModel.Channels.PeerCustomResolverBindingElement?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 对等通道功能已过时，并将在以后删除。|  
|<xref:System.ServiceModel.Channels.PeerTransportBindingElement?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 对等通道功能已过时，并将在以后删除。|  
|<xref:System.ServiceModel.Configuration.NetPeerTcpBindingCollectionElement?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 对等通道功能已过时，并将在以后删除。|  
|<xref:System.ServiceModel.Configuration.NetPeerTcpBindingElement?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 对等通道功能已过时，并将在以后删除。|  
|<xref:System.ServiceModel.Configuration.PeerTransportElement?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 对等通道功能已过时，并将在以后删除。|  
|<xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 对等通道功能已过时，并将在以后删除。|  
  
 [返回页首](#introduction)  
  
<a name="web"></a>   
### <a name="assembly-systemwebdll"></a>程序集：System.Web.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.Web.Configuration.PassportAuthentication?displayProperty=fullName>|此类型已过时。 Passport 身份验证产品不再受支持，并且已由 [Microsoft 帐户](http://go.microsoft.com/fwlink/?LinkId=733413)取代。|  
|<xref:System.Web.Mail.MailAttachment?displayProperty=fullName>|建议的替代项为 <xref:System.Net.Mail.Attachment?displayProperty=fullName>。|  
|<xref:System.Web.Mail.MailEncoding?displayProperty=fullName>|建议的替代项为 <xref:System.Net.Mime.TransferEncoding?displayProperty=fullName>。|  
|<xref:System.Web.Mail.MailFormat?displayProperty=fullName>|建议的替代项为 <xref:System.Net.Mail.MailMessage.IsBodyHtml%2A?displayProperty=fullName>。|  
|<xref:System.Web.Mail.MailMessage?displayProperty=fullName>|建议的替代项为 <xref:System.Net.Mail.MailMessage?displayProperty=fullName>。|  
|<xref:System.Web.Mail.MailPriority?displayProperty=fullName>|建议的替代项为 <xref:System.Net.Mail.MailPriority?displayProperty=fullName>。|  
|<xref:System.Web.Mail.SmtpMail?displayProperty=fullName>|建议的替代项为 <xref:System.Net.Mail.SmtpClient?displayProperty=fullName>。|  
|<xref:System.Web.Security.PassportAuthenticationEventArgs?displayProperty=fullName>|此类型已过时。 Passport 身份验证产品不再受支持，并且已由 [Microsoft 帐户](http://go.microsoft.com/fwlink/?LinkId=733413)取代。|  
|<xref:System.Web.Security.PassportAuthenticationEventHandler?displayProperty=fullName>|此类型已过时。 Passport 身份验证产品不再受支持，并且已由 [Microsoft 帐户](http://go.microsoft.com/fwlink/?LinkId=733413)取代。|  
|<xref:System.Web.Security.PassportAuthenticationModule?displayProperty=fullName>|此类型已过时。 Passport 身份验证产品不再受支持，并且已由 [Microsoft 帐户](http://go.microsoft.com/fwlink/?LinkId=733413)取代。|  
|<xref:System.Web.Security.PassportIdentity?displayProperty=fullName>|此类型已过时。 Passport 身份验证产品不再受支持，并且已由 [Microsoft 帐户](http://go.microsoft.com/fwlink/?LinkId=733413)取代。|  
|<xref:System.Web.Security.PassportPrincipal?displayProperty=fullName>|此类型已过时。 Passport 身份验证产品不再受支持，并且已由 [Microsoft 帐户](http://go.microsoft.com/fwlink/?LinkId=733413)取代。|  
|<xref:System.Web.UI.ObjectConverter?displayProperty=fullName>|建议的替代项为 <xref:System.Convert?displayProperty=fullName> 和 <xref:System.String.Format%2A?displayProperty=fullName>。|  
  
 [返回页首](#introduction)  
  
<a name="mobile"></a>   
### <a name="assembly-systemwebmobiledll"></a>程序集：System.Web.Mobile.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.Web.Mobile.CookielessData?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.Mobile.DeviceFilterElement?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.Mobile.DeviceFilterElementCollection?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.Mobile.DeviceFiltersSection?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.Mobile.ErrorHandlerModule?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.Mobile.MobileCapabilities?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.Mobile.MobileDeviceCapabilitiesSectionHandler?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.Mobile.MobileErrorInfo?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.Mobile.MobileFormsAuthentication?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.Design.MobileControls.IMobileDesigner?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.Design.MobileControls.IMobileWebFormServices?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.Design.MobileControls.MobileResource?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.Design.MobileControls.Converters.DataFieldConverter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.Design.MobileControls.Converters.DataMemberConverter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.AdRotator?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Alignment?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ArrayListCollectionBase?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.BaseValidator?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.BooleanOption?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Calendar?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Command?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.CommandFormat?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.CompareValidator?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Constants?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ControlElement?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ControlElementCollection?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ControlPager?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.CustomValidator?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.DesignerAdapterAttribute?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.DeviceElement?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.DeviceElementCollection?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.DeviceOverridableAttribute?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.DeviceSpecific?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoice?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceCollection?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceControlBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceTemplateBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceTemplateContainer?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificControlBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ErrorFormatterPage?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.FontInfo?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.FontSize?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Form?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.FormControlBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.FormMethod?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.IControlAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Image?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.IObjectListFieldCollection?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.IPageAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ItemPager?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ITemplateable?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Label?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Link?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.List?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ListCommandEventArgs?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ListCommandEventHandler?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ListControlBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ListDataBindEventArgs?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ListDataBindEventHandler?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ListDecoration?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ListSelectType?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.LiteralLink?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.LiteralText?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.LiteralTextContainerControlBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.LiteralTextControlBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.LoadItemsEventArgs?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.LoadItemsEventHandler?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.MobileControl?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.MobileControlBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.MobileControlsSection?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.MobileControlsSectionHandler?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.MobileListItem?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.MobileListItemCollection?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.MobileListItemType?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.MobilePage?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.MobileTypeNameConverter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.MobileUserControl?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectList?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListCommand?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListCommandCollection?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListCommandEventArgs?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListCommandEventHandler?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListControlBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListDataBindEventArgs?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListDataBindEventHandler?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListField?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListFieldCollection?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListItem?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListItemCollection?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListSelectEventArgs?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListSelectEventHandler?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListShowCommandsEventArgs?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListShowCommandsEventHandler?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListTitleAttribute?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ObjectListViewMode?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.PagedControl?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.PagerStyle?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Panel?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.PanelControlBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.PersistNameAttribute?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.PhoneCall?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.RangeValidator?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.RegularExpressionValidator?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.RequiredFieldValidator?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.SelectionList?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Style?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.StyleSheet?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.StyleSheetControlBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.TemplateContainer?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.TextBox?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.TextBoxControlBuilder?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.TextControl?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.TextView?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.TextViewElement?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.ValidationSummary?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Wrapping?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlCalendarAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlCommandAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlFormAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlImageAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlLinkAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlMobileTextWriter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlPageAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlPhoneCallAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlSelectionListAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlTextBoxAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.ControlAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlCalendarAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlCommandAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlControlAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlFormAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlImageAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlLabelAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlLinkAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlListAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlLiteralTextAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlMobileTextWriter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlObjectListAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlPageAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlPanelAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlPhoneCallAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlSelectionListAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlTextBoxAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlTextViewAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlValidationSummaryAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlValidatorAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.MobileTextWriter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.MultiPartWriter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.UpWmlMobileTextWriter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.UpWmlPageAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlCalendarAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlCommandAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlControlAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlFormAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlImageAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlLabelAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlLinkAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlListAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlLiteralTextAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlMobileTextWriter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlObjectListAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlPageAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlPanelAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlPhoneCallAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlPostFieldType?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlSelectionListAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlTextBoxAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlTextViewAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlValidationSummaryAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlValidatorAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.Doctype?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.StyleSheetLocation?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlCalendarAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlCommandAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlControlAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlCssHandler?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlFormAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlImageAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlLabelAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlLinkAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlListAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlLiteralTextAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlMobileTextWriter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlObjectListAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlPageAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlPanelAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlPhoneCallAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlSelectionListAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlTextBoxAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlTextViewAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlValidationSummaryAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlValidatorAdapter?displayProperty=fullName>|System.Web.Mobile.dll 程序集已弃用，因此不应再使用。 有关如何开发 ASP.NET 移动应用程序的信息，请参阅[面向移动应用程序的 ASP.NET](http://go.microsoft.com/fwlink/?LinkId=157231)。|  
  
 [返回页首](#introduction)  
  
<a name="workflow_activities"></a>   
### <a name="assembly-systemworkflowactivitiesdll"></a>程序集：System.Workflow.Activities.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.Workflow.Activities?displayProperty=fullName> 命名空间中的所有类型|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.Activities.Configuration.ActiveDirectoryRoleFactoryConfiguration?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.Activities.Rules.RuleActionTrackingEvent?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.Activities.Rules.RuleConditionReference?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.Activities.Rules.RuleSetReference?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
  
 [返回页首](#introduction)  
  
<a name="workflow_componentmodel"></a>   
### <a name="assembly-systemworkflowcomponentmodeldll"></a>程序集：System.Workflow.ComponentModel.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.Workflow.ComponentModel> 命名空间中的所有类型，<xref:System.Workflow.ComponentModel.GetValueOverride?displayProperty=fullName> 和 <xref:System.Workflow.ComponentModel.SetValueOverride?displayProperty=fullName> 除外|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.ComponentModel.Compiler> 命名空间中的所有类型，<xref:System.Workflow.ComponentModel.Compiler.ValidationError?displayProperty=fullName> 和 <xref:System.Workflow.ComponentModel.Compiler.ValidationErrorCollection?displayProperty=fullName> 除外|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.ComponentModel.Design> 命名空间中的所有类型，<xref:System.Workflow.ComponentModel.Design.ConnectorEventHandler> 除外|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.ComponentModel.Serialization.ActivityCodeDomSerializationManager?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.ComponentModel.Serialization.ActivityCodeDomSerializer?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.ComponentModel.Serialization.ActivityMarkupSerializer?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.ComponentModel.Serialization.ActivitySurrogateSelector?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.ComponentModel.Serialization.ActivityTypeCodeDomSerializer?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.ComponentModel.Serialization.CompositeActivityMarkupSerializer?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.ComponentModel.Serialization.DependencyObjectCodeDomSerializer?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
  
 [返回页首](#introduction)  
  
<a name="workflow_runtime"></a>   
### <a name="assembly-systemworkflowruntimedll"></a>程序集：System.Workflow.Runtime.dll  
  
|类型|消息|  
|----------|-------------| 
|<xref:System.Activities.Statements.Interop>|在 .NET Framework 4.5 中首次被废弃。<br /><br />Workflow Foundation 3.0 类型已弃用。 请改用 <xref:System.Activities>.\* 中的 Workflow 4.0 类型。|  
|<xref:System.Activities.Tracking.InteropTrackingRecord>|在 .NET Framework 4.5 中首次被废弃。<br /><br />Workflow Foundation 3.0 类型已弃用。 请改用 <xref:System.Activities>.\* 中的 Workflow 4.0 类型。|   
|<xref:System.Workflow.Runtime> 命名空间中的所有类型|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.Runtime.Configuration> 命名空间中的所有类型|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.Runtime.DebugEngine> 命名空间中的所有类型，<xref:System.Workflow.Runtime.DebugEngine.DebugEngineCallback> 除外|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.Runtime.Hosting> 命名空间中的所有类型，<xref:System.Workflow.Runtime.Hosting.WorkflowCommitWorkBatchService.CommitWorkBatchCallback> 除外|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
|<xref:System.Workflow.Runtime.Tracking> 命名空间中的所有类型|在 .NET Framework 4.5 中首次被废弃。<br /><br /> System.Workflow.\* 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新类型。|  
  
 [返回页首](#introduction)  
  
<a name="workflowservices"></a>   
### <a name="assembly-systemworkflowservicesdll"></a>程序集：System.WorkflowServices.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.ServiceModel.WorkflowServiceHost?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Activation.WorkflowServiceHostFactory?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Activities.Description.WorkflowRuntimeEndpoint?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Configuration.ExtendedWorkflowRuntimeServiceElementCollection?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Configuration.PersistenceProviderElement?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Configuration.WorkflowRuntimeElement?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Description.DurableOperationAttribute?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Description.DurableServiceAttribute?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Description.PersistenceProviderBehavior?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Description.UnknownExceptionAction?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Description.WorkflowRuntimeBehavior?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Dispatcher.DurableOperationContext?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Persistence.InstanceLockException?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Persistence.InstanceNotFoundException?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Persistence.LockingPersistenceProvider?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Persistence.PersistenceException?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Persistence.PersistenceProvider?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Persistence.PersistenceProviderFactory?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.ServiceModel.Persistence.SqlPersistenceProviderFactory?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.Workflow.Activities?displayProperty=fullName> 命名空间中的所有类型|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
|<xref:System.Workflow.Runtime.Hosting.ChannelManagerService?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> WF 3 类型已弃用。 请改用 <xref:System.Activities>.\* 中的新 WF 4 类型。|  
  
 [返回页首](#introduction)  
  
<a name="xaml"></a>   
### <a name="assembly-systemxamldll"></a>程序集：System.Xaml.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.Windows.Markup.AcceptedMarkupExtensionExpressionTypeAttribute?displayProperty=fullName>|XAML 分析器不使用此类型。 请查看 <xref:System.Windows.Markup.XamlSetMarkupExtensionAttribute?displayProperty=fullName>。|  
  
 [返回页首](#introduction)  
  
<a name="xml"></a>   
### <a name="assembly-systemxmldll"></a>程序集：System.Xml.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.Xml.IApplicationResourceStreamResolver?displayProperty=fullName>|在 .NET Framework 4.5 中首次被废弃。<br /><br /> 使用此类型会生成编译器错误。<br /><br /> 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
|<xref:System.Xml.Schema.XmlSchemaCollection?displayProperty=fullName>|请使用 <xref:System.Xml.Schema.XmlSchemaSet?displayProperty=fullName> 进行架构编译和验证。|  
|<xref:System.Xml.XmlValidatingReader?displayProperty=fullName>|改用使用适当的 <xref:System.Xml.XmlReader?displayProperty=fullName> 的 <xref:System.Xml.XmlReader.Create%2A?displayProperty=fullName> 方法创建的 <xref:System.Xml.XmlReaderSettings?displayProperty=fullName>。|  
|<xref:System.Xml.XmlXapResolver?displayProperty=fullName>|使用此类型会生成编译器错误。 此 API 支持 .NET Framework 基础结构，但不应在代码中直接使用。|  
|<xref:System.Xml.Xsl.XslTransform?displayProperty=fullName>|此类已弃用。 请改用 <xref:System.Xml.Xsl.XslCompiledTransform?displayProperty=fullName>。|  
  
 [返回页首](#introduction)  
  
<a name="WindowsBase"></a>   
### <a name="assembly-windowsbasedll"></a>程序集：WindowsBase.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:System.Windows.Markup.IReceiveMarkupExtension?displayProperty=fullName>|<xref:System.Windows.Markup.IReceiveMarkupExtension?displayProperty=fullName> 已弃用。 不再使用此接口。|  
  
 [返回页首](#introduction)  
  
<a name="obsolete_types_in_microsoft_assemblies"></a>   
## <a name="obsolete-types-in-microsoft-assemblies"></a>Microsoft 程序集中的过时类型  
 以下各节列出了 Microsoft 程序集中的过时类型。 这些程序集是具有特殊用途的程序集，如面向单一语言的程序集（如 Microsoft.JScript.dll 或 Microsoft.VisualC.dll）。  
  
<a name="IEHost"></a>   
### <a name="assembly-iehostdll-and-ieexecexe"></a>程序集：IEHost.dll 和 IEExec.exe  
 IEHost.dll 和 IEExec.exe 程序集已从 .NET Framework 中删除。 其所有类型和成员已过时，且从 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 开始已不支持它们。 这些程序集过去用于承载 Windows 窗体控件和在 Internet Explorer 中运行可执行文件。 建议的替代项包括 ClickOnce、XAML 浏览器应用程序 (XBAP) 和 Microsoft Silverlight。  
  
 [返回页首](#introduction)  
  
<a name="Engine"></a>   
### <a name="assembly-microsoftbuildenginedll"></a>程序集：Microsoft.Build.Engine.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:Microsoft.Build.BuildEngine.Engine?displayProperty=fullName>|此类已弃用。 请改用 Microsoft.Build 程序集中的 <xref:Microsoft.Build.Evaluation.ProjectCollection?displayProperty=fullName>。|  
|<xref:Microsoft.Build.BuildEngine.Project?displayProperty=fullName>|此类已弃用。 请改用 Microsoft.Build 程序集中的 <xref:Microsoft.Build.Evaluation.ProjectCollection?displayProperty=fullName>。|  
  
 [返回页首](#introduction)  
  
<a name="jscript"></a>   
### <a name="assembly-microsoftjscriptdll"></a>程序集：Microsoft.JScript.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:Microsoft.JScript.Vsa.BaseVsaEngine?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.BaseVsaSite?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.BaseVsaStartup?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.IJSVsaCodeItem?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.IJSVsaEngine?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.IJSVsaError?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.IJSVsaGlobalItem?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.IJSVsaItem?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.IJSVsaItems?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.IJSVsaPersistSite?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.IJSVsaReferenceItem?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.IJSVsaSite?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.JSVsaError?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.JSVsaException?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.JSVsaItemFlag?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.JSVsaItemType?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.ResInfo?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
|<xref:Microsoft.JScript.Vsa.VsaEngine?displayProperty=fullName>|建议不要使用此类型，因为此类型在 Visual Studio 2005 中已弃用；此功能将没有替代项。 有关其他帮助，请参见 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName> 文档。|  
  
 [返回页首](#introduction)  
  
<a name="VBCompat"></a>   
### <a name="assembly-microsoftvisualbasiccompatibilitydll"></a>程序集：Microsoft.VisualBasic.Compatibility.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BaseControlArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BaseOcxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ButtonArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.CheckBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.CheckedListBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ColorDialogArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ComboBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DirListBox?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DirListBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DriveListBox?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DriveListBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FileListBox?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FileListBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FixedLengthString?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FontDialogArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FormShowConstants?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.GroupBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.HScrollBarArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ImageListArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.LabelArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ListBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ListBoxItem?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ListViewArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.LoadResConstants?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MaskedTextBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MenuItemArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MouseButtonConstants?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.OpenFileDialogArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.PanelArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.PictureBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.PrintDialogArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ProgressBarArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.RadioButtonArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.RichTextBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.SaveFileDialogArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ScaleMode?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ShiftConstants?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.StatusBarArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.StatusStripArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.Support?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TabControlArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TextBoxArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TimerArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ToolBarArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ToolStripArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ToolStripMenuItemArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TreeViewArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.VScrollBarArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebBrowserArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClass?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassContainingClassNotOptional?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassCouldNotFindEvent?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassNextItemCannotBeCurrentWebItem?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassNextItemRespondNotFound?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassUserWebClassNameNotOptional?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassWebClassFileNameNotOptional?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassWebItemNotValid?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItem?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemAssociatedWebClassNotOptional?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemClosingTagNotFound?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemCouldNotLoadEmbeddedResource?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemCouldNotLoadTemplateFile?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemNameNotOptional?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemNoTemplateSpecified?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemTooManyNestedTags?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemUnexpectedErrorReadingTemplateFile?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ZOrderConstants?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
  
 [返回页首](#introduction)  
  
<a name="VBCompatData"></a>   
### <a name="assembly-microsoftvisualbasiccompatibilitydatadll"></a>程序集：Microsoft.VisualBasic.Compatibility.Data.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.BOFActionEnum?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.EndOfRecordsetDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.EOFActionEnum?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.ErrorDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.FetchCompleteDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.FetchProgressDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.FieldChangeCompleteDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.MoveCompleteDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.OrientationEnum?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.RecordChangeCompleteDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.RecordsetChangeCompleteDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillChangeFieldDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillChangeRecordDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillChangeRecordsetDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillMoveDelegate?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODCArray?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BaseDataEnvironment?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BindingCollectionEnumerator?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.CONNECTDATA?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBBINDING?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBCOLUMNINFO?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBID?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBinding?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBindingCollection?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBKINDENUM?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBPROPIDSET?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IAccessor?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IChapteredRowset?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IColumnsInfo?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IConnectionPoint?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IConnectionPointContainer?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IDataFormat?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IDataFormatDisp?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IEnumConnectionPoints?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IEnumConnections?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowPosition?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowPositionChange?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowset?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetChange?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetIdentity?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetInfo?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetNotify?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MBinding?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MBindingCollection?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.SRDescriptionAttribute?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.UGUID?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.UNAME?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.UpdateMode?displayProperty=fullName>|请参阅 [Microsoft.VisualBasic.Compatibility.VB6.\<member> 已过时，仅在 32 位进程中受支持](https://msdn.microsoft.com/library/ee839621.aspx)。|  
  
 [返回页首](#introduction)  
  
<a name="visualc"></a>   
### <a name="assembly-microsoftvisualcdll"></a>程序集：Microsoft.VisualC.dll  
  
|类型|消息|  
|----------|-------------|  
|<xref:Microsoft.VisualC.DebugInfoInPDBAttribute?displayProperty=fullName>|Microsoft.VisualC.dll 是已过时的程序集，仅出于向后兼容目的而存在。|  
|<xref:Microsoft.VisualC.DecoratedNameAttribute?displayProperty=fullName>|Microsoft.VisualC.dll 是已过时的程序集，仅出于向后兼容目的而存在。|  
|<xref:Microsoft.VisualC.IsConstModifier?displayProperty=fullName>|Microsoft.VisualC.dll 是已过时的程序集，仅出于向后兼容目的而存在。|  
|<xref:Microsoft.VisualC.IsCXXReferenceModifier?displayProperty=fullName>|Microsoft.VisualC.dll 是已过时的程序集，仅出于向后兼容目的而存在。|  
|<xref:Microsoft.VisualC.IsLongModifier?displayProperty=fullName>|Microsoft.VisualC.dll 是已过时的程序集，仅出于向后兼容目的而存在。|  
|<xref:Microsoft.VisualC.IsSignedModifier?displayProperty=fullName>|Microsoft.VisualC.dll 是已过时的程序集，仅出于向后兼容目的而存在。|  
|<xref:Microsoft.VisualC.IsVolatileModifier?displayProperty=fullName>|Microsoft.VisualC.dll 是已过时的程序集，仅出于向后兼容目的而存在。|  
|<xref:Microsoft.VisualC.MiscellaneousBitsAttribute?displayProperty=fullName>|Microsoft.VisualC.dll 是已过时的程序集，仅出于向后兼容目的而存在。|  
|<xref:Microsoft.VisualC.NeedsCopyConstructorModifier?displayProperty=fullName>|Microsoft.VisualC.dll 是已过时的程序集，仅出于向后兼容目的而存在。|  
|<xref:Microsoft.VisualC.NoSignSpecifiedModifier?displayProperty=fullName>|Microsoft.VisualC.dll 是已过时的程序集，仅出于向后兼容目的而存在。|  
  
## <a name="see-also"></a>另请参阅  
 [类库中过时的内容](../../../docs/framework/whats-new/whats-obsolete.md)   
 [过时成员](../../../docs/framework/whats-new/obsolete-members.md)

