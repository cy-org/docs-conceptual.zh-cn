---
title: "WIF 和 Web 场"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fc3cd7fa-2b45-4614-a44f-8fa9b9d15284
caps.latest.revision: 9
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0bb682c6eaebf7e1a0c2c2de5b584c28e4c192c5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="wif-and-web-farms"></a>WIF 和 Web 场
使用 Windows Identity Foundation (WIF) 保护 Web 场中部署的信赖方 (RP) 应用程序的资源时，必须采取特定的步骤确保 WIF 能处理场中不同计算机上运行的信赖方应用程序实例的令牌。 处理过程包括验证会话令牌签名、加密和解密会话令牌、缓存会话令牌以及检测重播的安全令牌。  
  
 通常情况下，使用 WIF 保护信赖方应用程序的资源时 – 无论 RP 是在单一计算机上运行还是在 Web 场中运行 – 都会基于从安全令牌服务 (STS) 获取的安全令牌与客户端创建一个会话。 这是为了避免强制客户端在 STS 对每个使用 WIF 保护的应用程序资源进行身份验证。 有关 WIF 如何处理会话的详细信息，请参阅 [WIF 会话管理](../../../docs/framework/security/wif-session-management.md)。  
  
 使用默认设置时，WIF 会执行以下操作：  
  
-   它使用 <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> 类的实例读取和写入会话令牌（<xref:System.IdentityModel.Tokens.SessionSecurityToken> 类的实例），此会话令牌传送声明、其他用于身份验证的安全令牌的相关信息和关于会话自身的信息。 会话令牌打包并存储在会话 cookie 中。 默认情况下，<xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> 使用 <xref:System.IdentityModel.ProtectedDataCookieTransform> 类，使用数据保护 API (DPAPI) 保护会话令牌。 DPAPI 使用用户或计算机凭据提供保护并将关键数据存储在用户配置文件中。  
  
-   它使用 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> 类的默认内存中实现来存储和处理会话令牌。  
  
 这些默认设置在信赖方应用程序部署于单台计算机上的方案中工作，但部署在 Web 场中时 ，每个 HTTP 请求都可能发送到不同计算机上运行的信赖方应用程序的不同实例并由这些实例处理。 在此方案中，以上所示的默认 WIF 设置将不会工作，因为令牌保护和令牌都依赖于特定的计算机。  
  
 若要在 Web 场中部署信赖方应用程序，必须确保会话令牌（以及重播令牌）的处理不依赖于特定计算机上运行的应用程序。 一种方法是实现信赖方应用程序，以便它使用 ASP.NET `<machineKey>` 配置元素提供的功能并提供分布式缓存处理会话令牌和重播令牌。 通过 `<machineKey>` 元素可以在配置文件中指定需要验证、加密和解密令牌的密钥，可在 Web 场中的不同计算机上指定相同的密钥。 WIF 提供专用的会话令牌处理程序 <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>该处理程序使用 `<machineKey>` 元素中指定的密钥保护令牌。 若要实现此策略，请遵循这些指导：  
  
-   使用配置中的 ASP.NET `<machineKey>` 元素显式指定可以在场中不同计算机上使用的签名和加密密钥。 以下 XML 显示配置文件中 `<system.web>` 元素下的 `<machineKey>` 元素的规范。  
  
    ```xml  
    <machineKey compatibilityMode="Framework45" decryptionKey="CC510D … 8925E6" validationKey="BEAC8 … 6A4B1DE" />  
    ```  
  
-   配置应用程序使用 <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>，方法是将它添加到令牌处理程序集合。 如果此类处理程序存在，必须先从令牌处理程序集合中删除 <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>（或者任何派生自 <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> 类的处理程序）。 <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler> 使用 <xref:System.IdentityModel.Services.MachineKeyTransform> 类，通过使用 `<machineKey>` 元素中指定的加密材料保护会话 cookie 数据。 以下 XML 显示如何添加 <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler> 到令牌处理程序集合。  
  
    ```xml  
    <securityTokenHandlers>  
      <remove type="System.IdentityModel.Tokens.SessionSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
      <add type="System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    </securityTokenHandlers>  
    ```  
  
-   派生自 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> 并实现分布式缓存，即可从运行 RP 的场中所有计算机访问的缓存。 通过指定配置文件中的 [\<sessionSecurityTokenCache>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/sessionsecuritytokencache.md) 元素配置 RP 使用分布式缓存。 可以替代派生类中的 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache.LoadCustomConfiguration%2A?displayProperty=fullName> 方法以按需实现 `<sessionSecurityTokenCache>` 元素的子元素。  
  
    ```xml  
    <caches>  
      <sessionSecurityTokenCache type="MyCacheLibrary.MySharedSessionSecurityTokenCache, MyCacheLibrary">  
        <!—optional child configuration elements, if implemented by the derived class -->  
      </sessionSecurityTokenCache>  
    </caches>  
    ```  
  
     实现分布式缓存的方法之一是为自定义缓存提供 WCF 前端。 有关实现 WCF 缓存服务的详细信息，请参阅 [WCF 缓存服务](#BKMK_TheWCFCachingService)。 有关实现信赖方应用程序可用于调用缓存服务的 WCF 客户端的详细信息，请参阅 [WCF 缓存客户端](#BKMK_TheWCFClient)。  
  
-   如果应用程序检测到重播令牌，则必须为令牌重播缓存采用相似的分布式缓存策略，方法是从 <xref:System.IdentityModel.Tokens.TokenReplayCache> 派生并在 [\<tokenReplayCache>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/tokenreplaycache.md) 配置元素中指向令牌重播缓存服务。  
  
> [!IMPORTANT]
>  本主题中的所有 XML 和代码示例摘自 [ClaimsAwareWebFarm](http://go.microsoft.com/fwlink/?LinkID=248408) (http://go.microsoft.com/fwlink/?LinkID=248408) 示例。  
  
> [!IMPORTANT]
>  本主题中的示例按原样提供，不建议在生产代码中不经修改直接使用。  
  
<a name="BKMK_TheWCFCachingService"></a>   
## <a name="the-wcf-caching-service"></a>WCF 缓存服务  
 以下接口定义 WCF 缓存服务和信赖方应用程序用来通信的 WCF 客户端之间的协定。 它实质上公开作为服务操作的 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> 类的方法。  
  
```  
[ServiceContract()]  
public interface ISessionSecurityTokenCacheService  
{  
    [OperationContract]  
    void AddOrUpdate(string endpointId, string contextId, string keyGeneration, SessionSecurityToken value, DateTime expiryTime);  
  
    [OperationContract]  
    IEnumerable<SessionSecurityToken> GetAll(string endpointId, string contextId);  
  
    [OperationContract]  
    SessionSecurityToken Get(string endpointId, string contextId, string keyGeneration);  
  
    [OperationContract(Name = "RemoveAll")]  
    void RemoveAll(string endpointId, string contextId);  
  
    [OperationContract(Name = "RemoveAllByEndpointId")]  
    void RemoveAll(string endpointId);  
  
    [OperationContract]  
    void Remove(string endpointId, string contextId, string keyGeneration);  
}  
```  
  
 下面的代码演示 WCF 缓存服务的实现。 此示例中使用由 WIF 实现的默认的内存中会话令牌缓存。 此外，可以实现数据库提供支持的持久缓存。 `ISessionSecurityTokenCacheService` 定义上述接口。 此示例中，为简洁起见，未演示实现接口所需的所有方法。  
  
```  
using System;  
using System.Collections.Generic;  
using System.IdentityModel.Configuration;  
using System.IdentityModel.Tokens;  
using System.ServiceModel;  
using System.Xml;  
  
namespace WcfSessionSecurityTokenCacheService  
{  
    [ServiceBehavior(InstanceContextMode = InstanceContextMode.Single)]  
    public class SessionSecurityTokenCacheService : ISessionSecurityTokenCacheService  
    {  
        SessionSecurityTokenCache internalCache;  
  
        // sets the internal cache used by the service to the default WIF in-memory cache.  
        public SessionSecurityTokenCacheService()  
        {  
            internalCache = new IdentityModelCaches().SessionSecurityTokenCache;  
        }  
  
        ...  
  
        public SessionSecurityToken Get(string endpointId, string contextId, string keyGeneration)  
        {  
            // Delegates to the default, in-memory MruSessionSecurityTokenCache used by WIF  
            SessionSecurityToken token = internalCache.Get(new SessionSecurityTokenCacheKey(endpointId, GetContextId(contextId), GetKeyGeneration(keyGeneration)));  
            return token;  
        }  
  
        ...  
  
        private static UniqueId GetContextId(string contextIdString)  
        {  
            return contextIdString == null ? null : new UniqueId(contextIdString);  
        }  
  
        private static UniqueId GetKeyGeneration(string keyGenerationString)  
        {  
            return keyGenerationString == null ? null : new UniqueId(keyGenerationString);  
        }  
    }  
}  
```  
  
<a name="BKMK_TheWCFClient"></a>   
## <a name="the-wcf-caching-client"></a>WCF 缓存客户端  
 此部分演示派生自 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> 并委托调用缓存服务的类的实现。 通过 [\<sessionSecurityTokenCache>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/sessionsecuritytokencache.md) 元素配置信赖方应用程序以使用此类，如下 XML 所示  
  
```xml  
<caches>  
  <sessionSecurityTokenCache type="CacheLibrary.SharedSessionSecurityTokenCache, CacheLibrary">  
    <!--cacheServiceAddress points to the centralized session security token cache service running in the web farm.-->  
    <cacheServiceAddress url="http://localhost:4161/SessionSecurityTokenCacheService.svc" />  
  </sessionSecurityTokenCache>  
</caches>  
```  
  
 此类替代 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache.LoadCustomConfiguration%2A> 方法以从 `<sessionSecurityTokenCache>` 元素的自定义 `<cacheServiceAddress>` 子元素中获取服务终结点。 它使用此终结点初始化用来与服务通信的 `ISessionSecurityTokenCacheService` 通道。  此示例中，为简洁起见，未演示实现 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> 类所需的所有方法。  
  
```  
using System;  
using System.Configuration;  
using System.IdentityModel.Configuration;  
using System.IdentityModel.Tokens;  
using System.ServiceModel;  
using System.Xml;  
  
namespace CacheLibrary  
{  
    /// <summary>  
    /// This class acts as a proxy to the WcfSessionSecurityTokenCacheService.  
    /// </summary>  
    public class SharedSessionSecurityTokenCache : SessionSecurityTokenCache, ICustomIdentityConfiguration  
    {  
        private ISessionSecurityTokenCacheService WcfSessionSecurityTokenCacheServiceClient;  
  
        internal SharedSessionSecurityTokenCache()  
        {  
        }  
  
        /// <summary>  
        /// Creates a client channel to call the service host.  
        /// </summary>  
        protected void Initialize(string cacheServiceAddress)  
        {  
            if (this.WcfSessionSecurityTokenCacheServiceClient != null)  
            {  
                return;  
            }  
  
            ChannelFactory<ISessionSecurityTokenCacheService> cf = new ChannelFactory<ISessionSecurityTokenCacheService>(  
                new WS2007HttpBinding(SecurityMode.None),  
                new EndpointAddress(cacheServiceAddress));  
            this.WcfSessionSecurityTokenCacheServiceClient = cf.CreateChannel();  
        }  
  
        #region SessionSecurityTokenCache Members  
        // Delegates the following operations to the centralized session security token cache service in the web farm.  
  
        ...  
  
        public override SessionSecurityToken Get(SessionSecurityTokenCacheKey key)  
        {  
            return this.WcfSessionSecurityTokenCacheServiceClient.Get(key.EndpointId, GetContextIdString(key), GetKeyGenerationString(key));  
        }  
  
        ...  
  
        #endregion  
  
        #region ICustomIdentityConfiguration Members  
        // Called from configuration infrastructure to load custom elements  
        public void LoadCustomConfiguration(XmlNodeList nodeList)  
        {  
            // Retrieve the endpoint address of the centralized session security token cache service running in the web farm  
            if (nodeList.Count == 0)  
            {  
                throw new ConfigurationException("No child config element found under <sessionSecurityTokenCache>.");  
            }  
  
            XmlElement cacheServiceAddressElement = nodeList.Item(0) as XmlElement;  
            if (cacheServiceAddressElement.LocalName != "cacheServiceAddress")  
            {  
                throw new ConfigurationException("First child config element under <sessionSecurityTokenCache> is expected to be <cacheServiceAddress>.");  
            }  
  
            string cacheServiceAddress = null;  
            if (cacheServiceAddressElement.Attributes["url"] != null)  
            {  
                cacheServiceAddress = cacheServiceAddressElement.Attributes["url"].Value;  
            }  
            else  
            {  
                throw new ConfigurationException("<cacheServiceAddress> is expected to contain a 'url' attribute.");  
            }  
  
            // Initialize the proxy to the WebFarmSessionSecurityTokenCacheService  
            this.Initialize(cacheServiceAddress);  
        }  
        #endregion  
  
        private static string GetKeyGenerationString(SessionSecurityTokenCacheKey key)  
        {  
            return key.KeyGeneration == null ? null : key.KeyGeneration.ToString();  
        }  
  
        private static string GetContextIdString(SessionSecurityTokenCacheKey key)  
        {  
            return GetContextIdString(key.ContextId);  
        }  
  
        private static string GetContextIdString(UniqueId contextId)  
        {  
            return contextId == null ? null : contextId.ToString();  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache>   
 <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>   
 <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>   
 [WIF 会话管理](../../../docs/framework/security/wif-session-management.md)

