---
title: "Создание первой службы WCF на основе утверждений"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0e6d091-9a97-4888-8f2c-cbcee42d90ee
caps.latest.revision: 7
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 3155295489e1188640dae5aa5bf9fdceb7480ed6
ms.openlocfilehash: a27420609a6bcb6e30a351e4b84a899da9583d5e
ms.contentlocale: ru-ru
ms.lasthandoff: 08/21/2017

---
# <a name="building-my-first-claims-aware-wcf-service"></a>Создание первой службы WCF на основе утверждений
## <a name="applies-to"></a>Применение  
  
-   Windows Identity Foundation (WIF)  
  
-   Windows Communication Foundation (WCF)  
  
## <a name="overview"></a>Обзор  
 В этом разделе представлен сценарий создания служб WCF, поддерживающих утверждения, при помощи WIF. Обычно существует три участника сценария для веб-службы, поддерживающей утверждения: сама веб-служба, пользователь и служба маркеров безопасности (STS). Данный сценарий представлен на иллюстрации ниже:  
  
 ![Базовая служба WCF с поддержкой утверждений на основе WIF](../../../docs/framework/security/media/wifbasicclaimsawarewcfservice.gif "WIFBasicClaimsAwareWCFService")  
  
1.  Клиент службы WCF (который иногда называют агентом) использует WIF для отправки учетных данных в службу STS. После успешной аутентификации служба STS создает токен для данного агента.  
  
2.  Агент отправляет токен, созданный STS, в службу WCF.  
  
3.  Служба WCF, поддерживающая утверждения, настроена на доверие к службе STS и ее токенам. Служба WCF, поддерживающая утверждения, использует WIF для проверки и анализа токена. Разработчики используют соответствующий API-интерфейс WIF и типы, например **ClaimsPrincipal**, для удовлетворения потребностей приложения (например, внедрения авторизации).  
  
 WIF входит в пакет .NET Framework, начиная с версии .NET 4.5. Прямая доступность классов WIF на этой платформе обеспечивает гораздо более глубокую интеграцию удостоверения на базе утверждений с платформой .NET, благодаря которой использовать утверждения становится проще. Если используется WIF 4.5, то для того, чтобы приступить к разработке веб-приложений, поддерживающих утверждения, не требуется устанавливать никакие дополнительные компоненты. Классы WIF теперь распространяются на различные сборки, например System.Security.Claims, System.IdentityModel и System.IdentityModel.Services.  
  
 STS — это служба, использующая токены после успешной аутентификации. Microsoft предлагает две службы STS, соответствующие отраслевым стандартам:  
  
-   [Службы федерации Active Directory (AD FS) 2.0](http://go.microsoft.com/fwlink/?LinkID=247516) (http://go.microsoft.com/fwlink/?LinkID=247516)  
  
-   [Служба управления доступом Windows Azure (ACS)](http://go.microsoft.com/fwlink/?LinkID=247517) (http://go.microsoft.com/fwlink/?LinkID=247517).  
  
 AD FS 2.0 является компонентом решения Windows Server R2 и может использоваться в качестве службы STS для локальных сценариев. Контроль доступа Azure Active Directory (также называемый службой контроля доступа или ACS) — это облачная служба, входящая в состав Microsoft Azure. Для тестирования или обучения можно также использовать другие службы STS, создавая с их помощью приложения, поддерживающие утверждения. Например, можно использовать службу STS локальной разработки, входящую в средство [Identity and Access Tool для Visual Studio](http://go.microsoft.com/fwlink/?LinkID=245849) (http://go.microsoft.com/fwlink/?LinkID=245849), которое можно бесплатно загрузить из Интернета.  
  
 Инструкции по сборке первой службы WCF, поддерживающей утверждения с помощью WIF, см. в разделе [Практическое руководство. Сборка службы WCF, поддерживающей утверждения с помощью WIF](http://msdn.microsoft.com/en-us/431e6415-62ed-4a9f-af03-f14d2b4dfe6d).  
  
## <a name="see-also"></a>См. также  
 [Приступая к работе с WIF](../../../docs/framework/security/getting-started-with-wif.md)

