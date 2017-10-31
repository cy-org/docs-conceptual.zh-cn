---
title: "如何：配置 IIS 5.0 和 IIS 6.0 以部署 WPF 应用程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "调整内容过期设置"
  - "应用程序, 部署"
  - "配置 Web 服务器以部署 WPF 应用程序"
  - "内容过期设置, 调整"
  - "部署应用程序"
  - "文件扩展名, 注册"
  - "MIME 类型, 注册"
  - "注册文件扩展名"
  - "注册 MIME 类型"
  - "Web 服务器, 进行配置以部署 WPF 应用程序"
ms.assetid: c6e8c2cb-9ba2-4e75-a0d5-180ec9639433
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：配置 IIS 5.0 和 IIS 6.0 以部署 WPF 应用程序
您可以从大多数 Web 服务器部署 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序，前提是这些服务器配置了适当的[!INCLUDE[TLA#tla_mime](../../../../includes/tlasharptla-mime-md.md)] 类型。  默认情况下，[!INCLUDE[TLA#tla_iis70](../../../../includes/tlasharptla-iis70-md.md)] 配置有这些[!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] 类型，但 [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] 和 [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)] 则不然。  
  
 本主题介绍如何配置 [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] 和 [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)] 来部署 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  
  
   
  
> [!NOTE]
>  您可以检查注册表中的 *UserAgent* 字符串，确定系统是否安装了 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]。  有关检查 *UserAgent* 字符串以确定系统是否安装了 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 的详细信息和脚本，请参见[检测是否安装了 .NET Framework 3.0](../../../../docs/framework/wpf/app-development/how-to-detect-whether-the-net-framework-3-0-is-installed.md)。  
  
<a name="content_expiration"></a>   
## 调整内容过期设置  
 您应当将内容过期设置调整为 1 分钟。  下面的过程简要介绍了如何对 [!INCLUDE[TLA2#tla_iis5](../../../../includes/tla2sharptla-iis5-md.md)] 执行此操作。  
  
1.  单击**“开始”**菜单，指向**“管理工具”**，然后单击**“Internet 信息服务\(IIS\)管理器”**。  您还可以使用“%SystemRoot%\\system32\\inetsrv\\iis.msc”从命令行启动此应用程序。  
  
2.  展开 [!INCLUDE[TLA2#tla_iis5](../../../../includes/tla2sharptla-iis5-md.md)] 树，直到找到**“默认网站”**节点。  
  
3.  右击**“默认网站”**，从上下文菜单中选择**“属性”**。  
  
4.  选择**“HTTP 头”**选项卡，然后单击“启用内容过期”。  
  
5.  将内容设置为 1 分钟后过期。  
  
<a name="register_mime_types"></a>   
## 注册 MIME 类型和文件扩展名  
 必须注册几种 [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] 类型和文件扩展名，客户端系统上的浏览器才能加载正确的处理程序。  需要添加以下类型：  
  
|扩展|MIME 类型|  
|--------|-------------|  
|.manifest|application\/manifest|  
|.xaml|application\/xaml\+xml|  
|.application|application\/x\-ms\-application|  
|.xbap|application\/x\-ms\-xbap|  
|.deploy|application\/octet\-stream|  
|.xps|application\/vnd.ms\-xpsdocument|  
  
> [!NOTE]
>  您不需要在客户端系统上注册 [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] 类型或文件扩展名。  它们是在您安装 [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)]时自动注册的。  
  
 下面的 [!INCLUDE[TLA#tla_visualbscrpt](../../../../includes/tlasharptla-visualbscrpt-md.md)] 示例自动将必要的 [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] 类型添加到 [!INCLUDE[TLA2#tla_iis5](../../../../includes/tla2sharptla-iis5-md.md)]。  若要使用此脚本，请将代码复制到服务器上的 .vbs 文件。  然后，通过从命令行运行此文件或者在 [!INCLUDE[TLA#tla_winexpl](../../../../includes/tlasharptla-winexpl-md.md)]中双击此文件来运行脚本。  
  
```  
' This script adds the necessary Windows Presentation Foundation MIME types   
' to an IIS Server.  
' To use this script, just double-click or execute it from a command line.  
' Running this script multiple times results in multiple entries in the IIS MimeMap.  
  
Dim MimeMapObj, MimeMapArray, MimeTypesToAddArray, WshShell, oExec  
Const ADS_PROPERTY_UPDATE = 2   
  
' Set the MIME types to be added  
MimeTypesToAddArray = Array(".manifest", "application/manifest", ".xaml", _  
    "application/xaml+xml", ".application", "application/x-ms-application", _  
    ".deploy", "application/octet-stream", ".xbap", "application/x-ms-xbap", _  
    ".xps", "application/vnd.ms-xpsdocument")   
  
' Get the mimemap object   
Set MimeMapObj = GetObject("IIS://LocalHost/MimeMap")  
  
' Call AddMimeType for every pair of extension/MIME type  
For counter = 0 to UBound(MimeTypesToAddArray) Step 2  
    AddMimeType MimeTypesToAddArray(counter), MimeTypesToAddArray(counter+1)  
Next  
  
' Create a Shell object  
Set WshShell = CreateObject("WScript.Shell")  
  
' Stop and Start the IIS Service  
Set oExec = WshShell.Exec("net stop w3svc")  
Do While oExec.Status = 0  
    WScript.Sleep 100  
Loop  
  
Set oExec = WshShell.Exec("net start w3svc")  
Do While oExec.Status = 0  
    WScript.Sleep 100  
Loop  
  
Set oExec = Nothing  
  
' Report status to user  
WScript.Echo "Windows Presentation Foundation MIME types have been registered."  
  
' AddMimeType Sub  
Sub AddMimeType (Ext, MType)  
  
    ' Get the mappings from the MimeMap property.   
    MimeMapArray = MimeMapObj.GetEx("MimeMap")   
  
    ' Add a new mapping.   
    i = UBound(MimeMapArray) + 1   
    Redim Preserve MimeMapArray(i)   
    Set MimeMapArray(i) = CreateObject("MimeMap")   
    MimeMapArray(i).Extension = Ext   
    MimeMapArray(i).MimeType = MType   
    MimeMapObj.PutEx ADS_PROPERTY_UPDATE, "MimeMap", MimeMapArray  
    MimeMapObj.SetInfo  
  
End Sub  
```  
  
> [!NOTE]
>  运行此脚本多次会在 [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] 或 [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)] 元数据库中创建多个 [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] 映射项。  
  
 运行此脚本后，您可能不会从 [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] 或 [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)] [!INCLUDE[TLA#tla_mmc](../../../../includes/tlasharptla-mmc-md.md)] 中看到其他 [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] 类型。  但是，这些 [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] 类型已添加到 [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] 或 [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)] 元数据库中。  下面的脚本将显示 [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] 或 [!INCLUDE[TLA#tla_iis60](../../../../includes/tlasharptla-iis60-md.md)] 元数据库中的所有 [!INCLUDE[TLA2#tla_mime](../../../../includes/tla2sharptla-mime-md.md)] 类型。  
  
```  
' This script lists the MIME types for an IIS Server.  
' To use this script, just double-click or execute it from a command line   
' by calling cscript.exe  
  
dim mimeMapEntry, allMimeMaps  
  
' Get the mimemap object.  
Set mimeMapEntry = GetObject("IIS://localhost/MimeMap")  
allMimeMaps = mimeMapEntry.GetEx("MimeMap")  
  
' Display the mappings in the table.  
For Each mimeMap In allMimeMaps  
    WScript.Echo(mimeMap.MimeType & " (" & mimeMap.Extension + ")")  
Next  
```  
  
 将脚本另存为 `.vbs` 文件（例如，`DiscoverIISMimeTypes.vbs`），然后从命令提示窗口使用以下命令运行它：  
  
 `cscript DiscoverIISMimeTypes.vbs`