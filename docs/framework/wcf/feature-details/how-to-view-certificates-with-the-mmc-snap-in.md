---
title: "如何：使用 MMC 管理单元查看证书 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "证书 [WCF], 使用 MMC 管理单元查看"
ms.assetid: 2b8782aa-ebb4-4ee7-974b-90299e356dc5
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 如何：使用 MMC 管理单元查看证书
凭据的一种常见类型是 X.509 证书。在创建安全服务或客户端时，可以通过使用如 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> 这样的方法来指定使用证书作为客户端或服务凭据。该方法需要多个参数，如存储证书的存储位置和搜索证书时使用的值。下面的过程演示如何检查计算机上的存储以查找相应的证书。有关查找证书指纹的示例，请参见[如何：检索证书的指纹](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)。  
  
### 在 MMC 管理单元中查看证书  
  
1.  打开一个命令提示符窗口。  
  
2.  键入 `mmc` 然后按 Enter 键。请注意，若要查看本地计算机存储中的证书，您必须具有管理员角色。  
  
3.  在**“文件”**菜单上，单击**“添加\/删除管理单元”**。  
  
4.  单击**“添加”**。  
  
5.  在**“添加独立管理单元”**对话框中，选择**“证书”**。  
  
6.  单击**“添加”**。  
  
7.  在**“证书”管理单元**对话框中，选择**“计算机帐户”**，然后单击 **“下一步”**。也可以选择**“我的用户帐户”**或**“服务帐户”**。如果您不是计算机的管理员，则您只能管理您的用户帐户的证书。  
  
8.  在**“选择计算机”**对话框中，单击**“完成”**。  
  
9. 在**“添加独立管理单元”**对话框中，单击**“关闭”**。  
  
10. 在**“添加\/删除管理单元”**对话框中，单击**“确定”**。  
  
11. 在**“控制台根节点”**窗口中，单击**“证书\(本地计算机\)”**查看计算机的证书存储。  
  
12. 可选。若要查看您的帐户证书，请重复步骤 3 到步骤 6。在步骤 7 中，单击**“我的用户帐户”**而不选择**“计算机帐户”**，然后重复步骤 8 到步骤 10。  
  
13. 可选。在**“文件”**菜单上单击**“保存”**或**“另存为”**。保存控制台文件供以后重复使用。  
  
## 使用 Internet Explorer 查看证书  
 您也可以通过使用 Internet Explorer 来查看、导出、导入和删除证书。  
  
#### 使用 Internet Explorer 查看证书  
  
1.  在 Internet Explorer 中，单击**“工具”**，然后单击**“Internet 选项”**以显示**“Internet 选项”**对话框。  
  
2.  单击**“内容”**选项卡。  
  
3.  在**“证书”**下，单击**“证书”**。  
  
4.  若要查看任何证书的详细信息，请选择该证书，然后单击**“查看”**。  
  
## 请参阅  
 [使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [如何：创建开发期间使用的临时证书](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md)   
 [如何：检索证书的指纹](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)