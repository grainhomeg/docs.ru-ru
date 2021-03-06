---
title: "&lt;безопасность&gt; для &lt;netHttpBinding | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dc41f6f7-cabc-4a64-9fa0-ceabf861b348
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;безопасность&gt; для &lt;netHttpBinding
Определяет возможности безопасности для элемента [\<basicHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md).  
  
## Синтаксис  
  
```  
  
<security mode="Message/None/Transport/TransportWithCredential">  
   <transport  
      clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"  
      proxyCredentialType="Basic/Digest/None/Ntlm/Windows"  
      realm="string" />  
   <message  
      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
            clientCredentialType="Certificate/IssuedToken/None/UserName/Windows" />  
</security>  
```  
  
## Атрибуты и элементы  
 В следующих разделах описываются атрибуты, дочерние и родительские элементы.  
  
### Атрибуты  
  
|Атрибут|Описание|  
|-------------|--------------|  
|режим|Необязательно.  Задает тип используемого механизма обеспечения безопасности.  Значение по умолчанию — `None`.  Это атрибут типа <xref:System.ServiceModel.NetHttpSecurityMode>.|  
  
## Атрибут mode  
  
|Значение|Описание|  
|--------------|--------------|  
|Нет|-   Во время передачи сообщения не защищены.|  
|Transport|Безопасность обеспечивается с помощью транспорта HTTPS.  Сообщения SOAP защищаются при помощи HTTPS.  Служба проходит проверку подлинности для клиента с использованием сертификата X.509.  Проверка подлинности клиента осуществляется с помощью предоставленного ClientCredentialType.|  
|Сообщение|Безопасность обеспечивается с помощью средств безопасности сообщений SOAP.  По умолчанию текст сообщений шифруется и подписывается.  Для этой привязки система требует, чтобы клиенту был предоставлен сертификат сервера с использованием внештатного канала.  Единственным допустимым значением `ClientCredentialType` для данной привязки является `Certificate`.|  
|TransportWithMessageCredential|Целостность, конфиденциальность и проверка подлинности сервера обеспечиваются с помощью средств безопасности транспорта.  Проверка подлинности клиента осуществляется при помощи механизма безопасности сообщений SOAP.  Данный режим может использоваться, когда проверка подлинности клиента осуществляется с помощью имени пользователя\/пароля и существует развернутый канал HTTP с обеспечением безопасности при передаче сообщений.|  
|TransportCredentialOnly|Данный режим не обеспечивает целостности и конфиденциальности сообщений.  Он предоставляет проверку подлинности клиента на основе http.  Этот режим следует использовать с осторожностью.  Он должен использоваться в тех средах, где безопасность транспорта обеспечивается другими средствами \(например, IPSec\), а инфраструктура [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] обеспечивает только проверку подлинности клиента.|  
  
### Дочерние элементы  
  
|Элемент|Описание|  
|-------------|--------------|  
|[\<транспорт\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-nethttpbinding.md)|Определяет параметры безопасности транспорта для базовой службы HTTP.  Данный элемент соответствует <xref:System.ServiceModel.HttpTransportSecurity>.|  
|[\<сообщение\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-nethttpbinding.md)|Определяет параметры безопасности сообщений для базовой службы HTTP.  Данный элемент соответствует <xref:System.ServiceModel.NetHttpMessageSecurity>.|  
  
### Родительские элементы  
  
|Элемент|Описание|  
|-------------|--------------|  
|привязка|Элемент привязки [\<basicHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md).|  
  
## Заметки  
 По умолчанию сообщение SOAP не защищено и проверка подлинности клиента не выполняется.  Данный элемент позволяет настроить дополнительные параметры безопасности для элемента `netHttpBinding`.  
  
## См. также  
 <xref:System.ServiceModel.NetHttpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.NetHttpBindingElement.Security%2A>   
 <xref:System.ServiceModel.Configuration.NetHttpSecurityElement>   
 <xref:System.ServiceModel.NetHttpSecurity>   
 [Защита служб и клиентов](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Выбор типа учетных данных](../../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)   
 [Привязки](../../../../../docs/framework/wcf/bindings.md)   
 [Настройка привязок, предоставляемых системой](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/ru-ru/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<привязка\>](../../../../../docs/framework/misc/binding.md)