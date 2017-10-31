---
title: "下载 JSON Web 标记处理程序包"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d12b3f5b-f1f1-4a9d-a159-0c13e5976c90
caps.latest.revision: 3
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d3821ff1da945df7c6e07e5baf69730173eacc87
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="downloading-the-json-web-token-handler-package"></a>下载 JSON Web 标记处理程序包
本主题讨论了如何在项目中下载和使用 JSON Web 令牌处理程序。  
  
## <a name="downloading-the-json-web-token-handler"></a>下载 JSON Web 标记处理程序  
 JSON Web 令牌处理程序扩展可用作 NuGet 程序包，可将必要程序集和引用添加到项目。 如果尚未安装 NuGet，请转到 [nuget.org](http://nuget.org) 进行安装。 访问 NuGet 上的扩展页面，查看扩展的版本历史记录：[NuGet 上的 JSON Web 令牌处理程序](http://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/)  
  
#### <a name="downloading-the-json-web-token-handler-by-using-the-package-manager-gui"></a>使用程序包管理器 GUI 下载 JSON Web 令牌处理程序  
  
1.  在 Visual Studio 中，在解决方案资源管理器中右键单击项目，然后选择“管理 NuGet 包”。  
  
2.  在“管理 NuGet 包”窗口中，单击搜索框并输入 `JWT Token Handler`，然后按 Enter。  
  
3.  单击结果窗格中第一个结果的“安装”按钮。  
  
4.  将开始下载包。 将包添加到项目前，会出现“许可证接受”对话框。 如果同意许可条款，请单击“我接受”。  
  
5.  将下载最新的 JSON Web 令牌处理程序程序集并添加到项目。  
  
#### <a name="downloading-the-json-web-token-handler-by-using-the-package-manager-console"></a>使用包管理器控制台下载 JSON Web 令牌处理程序  
  
1.  在 Visual Studio 中，依次单击“工具”、“库包管理器”和“包管理器控制台”。  
  
2.  随即出现“包管理器控制台”。 输入以下文本并按 Enter：  
  
    ```powershell  
    Install-Package System.IdentityModel.Tokens.Jwt  
    ```  
  
3.  将下载最新的 JSON Web 令牌处理程序程序集并添加到项目。

