---
title: "如何：创建开发期间使用的临时证书 | Microsoft Docs"
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
  - "证书 [WCF], 创建临时证书"
  - "临时证书 [WCF]"
ms.assetid: bc5f6637-5513-4d27-99bb-51aad7741e4a
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 如何：创建开发期间使用的临时证书
当使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 开发安全服务或客户程序时，经常需要提供 X.509 证书以用作凭据。 该证书通常是证书链的一部分，在计算机的受信任的根证书颁发机构存储区中可找到根证书颁发机构。 拥有一个证书链，使您可以限定一组证书，其中根证书颁发机构通常来自于您的组织或业务单元。 若要在开发时模拟此情况，请创建两个证书以满足安全要求。 第一个证书是自签名证书，放置在受信任的根证书颁发机构存储区中；第二个证书是从第一个证书创建的，放置在本地计算机位置的个人存储区中或当前用户位置的个人存储区中。 本主题指导你逐步完成使用[证书创建工具 \(MakeCert.exe\)](http://go.microsoft.com/fwlink/?LinkId=248185) 创建这两个证书的步骤，该工具由 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] SDK 提供。  
  
> [!IMPORTANT]
>  证书创建工具生成的证书仅供测试使用。 部署服务或客户程序时，请确保使用证书颁发机构提供的适当证书。 这可能是来自于组织或第三方的 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 证书服务器。  
>   
>  默认情况下，[Makecert.exe（证书创建工具）](../Topic/Makecert.exe%20\(Certificate%20Creation%20Tool\).md) 创建根证书颁发机构称为**根证书代理**的证书。由于“根证书代理”不是受信任的根证书颁发机构存储区，这会使这些证书不安全。 创建一个放置在受信任的根证书颁发机构存储区的自签名证书，您可以创建一个与您的部署环境极其类似的开发环境。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]创建和使用证书，请参阅[使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用证书作为凭据，请参阅[保护服务和客户端的安全](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)。 有关使用 Microsoft Authenticode 技术的教程，请参阅 [Authenticode Overviews and Tutorials](http://go.microsoft.com/fwlink/?LinkId=88919)（Authenticode 概述和教程）。  
  
### 创建一个自签名根证书颁发机构证书并导出私钥  
  
1.  使用 MakeCert.exe 工具和以下开关：  
  
    1.  `-n` `subjectName`. 指定主题名称。 约定是为主题名的“公用名”添加前缀“CN \= ”。  
  
    2.  `-r`。 指定证书将自签名。  
  
    3.  `-sv` `privateKeyFile`. 指定包含私钥容器的文件。  
  
     例如，下面的命令创建一个主题名称为“CN\=TempCA”的自签名证书。  
  
    ```  
    makecert -n "CN=TempCA" -r -sv TempCA.pvk TempCA.cer  
    ```  
  
     系统将提示您提供一个密码以保护私钥。 在创建由此根证书签名的证书时需要此密码。  
  
### 创建一个由根证书颁发机构证书签名的新证书  
  
1.  使用 MakeCert.exe 工具和以下开关：  
  
    1.  `-sk` `subjectKey`. 保存私钥的主题密钥容器的位置。 如果密钥容器不存在，则将创建一个。 如果既没有使用 \-sk 选项，也没有使用 \-sv 选项，则默认创建名为 JoeSoft 的密钥容器。  
  
    2.  `-n` `subjectName`. 指定主题名称。 约定是为主题名的“公用名”添加前缀“CN \= ”。  
  
    3.  `-iv` `issuerKeyFile`. 指定颁发者的私钥文件。  
  
    4.  `-ic` `issuerCertFile`. 指定颁发者的证书位置。  
  
     例如，下面的命令使用颁发者的私钥创建一个由 `TempCA` 根证书颁发机构证书签名的证书，其主题名称为 `"CN=SignedByCA"`。  
  
    ```  
    makecert -sk SignedByCA -iv TempCA.pvk -n "CN=SignedByCA" -ic TempCA.cer SignedByCA.cer -sr currentuser -ss My  
    ```  
  
## 在受信任的根证书颁发机构存储区中安装证书  
 创建自签名证书后，您可以将它安装到受信任的根证书颁发机构存储区中。 任何使用该证书签名的证书在此处都受计算机的信任。 为此，当您不再需要该证书时可立即将它从存储区中删除。 当您删除此根证书颁发机构证书时，则由它签名的所有其他证书将成为未经授权的。 根证书颁发机构证书只是一种机制，必要时可限定一组证书。 例如，在对等应用程序中，通常不需要根证书颁发机构，因为您只信任由对方提供的证书的个体标识。  
  
#### 在受信任的根证书颁发机构中安装自签名证书  
  
1.  打开证书管理单元。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [如何：使用 MMC 管理单元查看证书](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).  
  
2.  打开要存储证书的文件夹，**“本地计算机”**或**“当前用户”**。  
  
3.  打开**“受信任的根证书颁发机构”**文件夹。  
  
4.  右击**“证书”**文件夹，再单击**“所有任务”**，然后单击**“导入”**。  
  
5.  按照屏幕向导说明，将 TempCa.cer 导入到存储区中。  
  
## 在 WCF 中使用证书  
 一旦安装了临时证书，就可以使用这些证书开发指定证书作为客户端凭据类型的 WCF 解决方案。 例如，下面的 XML 配置指定消息安全模式，并指定证书作为客户端凭据类型。  
  
#### 指定证书作为客户端凭据类型  
  
-   在服务的配置文件中，使用下面的 XML 将安全模式设置为消息，并将客户端凭据类型设置为证书。  
  
    ```xml  
    <bindings>       
      <wsHttpBinding>  
        <binding name="CertificateForClient">  
          <security>  
            <message clientCredentialType="Certificate" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
  
    ```  
  
 在客户端的配置文件中，使用下面的 XML 指定证书存在于用户存储区中，可以通过在 SubjectName 字段中搜索“CohoWinery”值找到该证书。  
  
```xml  
  
<behaviors>  
  <endpointBehaviors>  
    <behavior name="CertForClient">  
      <clientCredentials>  
        <clientCertificate findValue="CohoWinery" x509FindType="FindBySubjectName" />  
       </clientCredentials>  
     </behavior>  
   </endpointBehaviors>  
</behaviors>  
```  
  
 有关在 WCF 中使用证书的详细信息，请参阅[使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)。  
  
## .NET Framework 安全性  
 请确保通过右击证书，再单击**“删除”**，从**“受信任的根证书颁发机构”**和**“个人”**文件夹中删除所有临时根证书颁发机构证书。  
  
## 请参阅  
 [使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [如何：使用 MMC 管理单元查看证书](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md)   
 [保护服务和客户端的安全](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)