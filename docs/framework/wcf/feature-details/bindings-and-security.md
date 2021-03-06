---
title: "Привязки и безопасность"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bindings [WCF], security
- WCF security
- Windows Communication Foundation, security
- bindings [WCF]
ms.assetid: 4de03dd3-968a-4e65-af43-516e903d7f95
caps.latest.revision: "42"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload: dotnet
ms.openlocfilehash: 9e44db963a696f22f91569eb3d7c2956289a9c76
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="bindings-and-security"></a>Привязки и безопасность
Предоставляемые системой привязки, включенные в [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], обеспечивают быстрый способ программирования приложений [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. За одним исключением, во всех привязках включена схема безопасности по умолчанию. Этот раздел поможет выбрать привязку, соответствующую требованиям к безопасности.  
  
 Общие сведения о [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] безопасности, в разделе [Общие сведения о безопасности](../../../../docs/framework/wcf/feature-details/security-overview.md). [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Программирование [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] с помощью привязки, в разделе [программирование безопасности WCF](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md).  
  
 Если привязка уже выбран, можно найти дополнительные сведения о поведение во время выполнения, связанные с безопасностью в [поведения безопасности](../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md).  
  
 Некоторые функции безопасности невозможно запрограммировать с помощью привязок, предоставляемых системой. Для усиления контроля использования пользовательской привязки, в разделе [возможности безопасности при использовании пользовательских привязок](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md).  
  
## <a name="security-functions-of-bindings"></a>Функции безопасности привязок  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] содержит ряд предоставляемых системой привязок, удовлетворяющих большей части потребностей. Если определенная привязка не удовлетворяет всем необходимым требованиям, можно также создать пользовательскую привязку. Список привязок, предоставляемых системой см. в разделе [привязка, предоставляемая системой](../../../../docs/framework/wcf/system-provided-bindings.md). [!INCLUDE[crabout](../../../../includes/crabout-md.md)]пользовательские привязки в разделе [пользовательские привязки](../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
 Каждая привязка в [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] существует в двух видах: в виде API и в виде элемента XML, используемого в файле конфигурации. Например `WSHttpBinding` (API) имеет аналога в [ \<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).  
  
 В следующем подразделе перечисляются обе формы каждой из привязок и приводится краткое описание возможностей безопасности.  
  
### <a name="basichttp"></a>BasicHttp  
 В коде используйте <xref:System.ServiceModel.BasicHttpBinding> класса; в конфигурации, используйте [ \<basicHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md).  
  
 Эта привязка предназначена для использования с различными существующими технологиями, включая перечисленные ниже.  
  
-   Веб-службы ASP.NET (ASMX), версия 1.  
  
-   Приложения расширений веб-служб (WSE).  
  
-   Профиль Basic, как определено в взаимодействия веб-служб (WS-I) спецификация ([http://go.microsoft.com/fwlink/?LinkId=38955](http://go.microsoft.com/fwlink/?LinkId=38955)).  
  
-   Базовый профиль безопасности, определенный в спецификации WS-I.  
  
 По умолчанию эта привязка не является безопасной. Она предназначена для взаимодействия со службами ASMX. Если безопасность включена, эта привязка обеспечивает беспрепятственное взаимодействие с механизмами безопасности служб IIS, такими как обычная проверка подлинности, дайджест-проверка и встроенная система безопасности Windows. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Общие сведения о безопасности транспорта](../../../../docs/framework/wcf/feature-details/transport-security-overview.md). Эта привязка поддерживает следующие функции:  
  
-   Безопасность транспорта HTTPS.  
  
-   Обычная проверка подлинности HTTP.  
  
-   WS-Security.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.BasicHttpSecurity>, <xref:System.ServiceModel.BasicHttpMessageSecurity>, <xref:System.ServiceModel.BasicHttpMessageCredentialType> и <xref:System.ServiceModel.BasicHttpSecurityMode>.  
  
### <a name="wshttpbinding"></a>WSHttpBinding  
 В коде используйте <xref:System.ServiceModel.WSHttpBinding> класса; в конфигурации, используйте [ \<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).  
  
 По умолчанию эта привязка реализует спецификацию WS-Security и обеспечивает взаимодействие со службами, реализующими спецификации WS-*. Она поддерживает следующие функции:  
  
-   Безопасность транспорта HTTPS.  
  
-   WS-Security.  
  
-   Защита транспорта HTTPS с использованием безопасности учетных данных сообщения SOAP для проверки подлинности вызывающей стороны.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.WSHttpSecurity>, <xref:System.ServiceModel.MessageSecurityOverHttp>, <xref:System.ServiceModel.MessageCredentialType>, <xref:System.ServiceModel.SecurityMode>, <xref:System.ServiceModel.HttpTransportSecurity>, <xref:System.ServiceModel.HttpClientCredentialType> и <xref:System.ServiceModel.HttpProxyCredentialType>.  
  
### <a name="wsdualhttpbinding"></a>WSDualHttpBinding  
 В коде используйте <xref:System.ServiceModel.WSDualHttpBinding> класса; в конфигурации, используйте [ \<wsDualHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md).  
  
 Эта привязка предназначена для обеспечения приложений дуплексных служб. Эта привязка реализует спецификацию WS-Security для обеспечения безопасности передачи на основе сообщений. Безопасность транспорта отсутствует. По умолчанию предусмотрены следующие функции.  
  
-   Для надежности реализован обмен сообщениями WS-Reliable Messaging.  
  
-   Для транспортной безопасности и проверки подлинности реализована спецификация WS-Security.  
  
-   Для доставки сообщений используется протокол HTTP.  
  
-   Используется кодирование текстовых сообщений/сообщений XML.  
  
 Используя WS-Security (безопасность на уровне сообщений), эта привязка позволяет настроить следующие параметры:  
  
-   Набор алгоритмов безопасности для определения алгоритма шифрования.  
  
-   Параметры привязки для:  
  
    -   предоставления учетных данных службы, получаемых клиентом по внештатному каналу;  
  
    -   предоставления учетных данных службы, согласованных со службой в процессе настройки канала.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]<xref:System.ServiceModel.WSDualHttpSecurity> и <xref:System.ServiceModel.WSDualHttpSecurityMode>.  
  
### <a name="nettcpbinding"></a>NetTcpBinding  
 В коде используйте <xref:System.ServiceModel.NetTcpBinding> класса; в конфигурации, используйте [ \<netTcpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md).  
  
 Эта привязка оптимизирована для обмена данными между компьютерами. По умолчанию она имеет следующие характеристики:  
  
-   Реализуется безопасность на транспортном уровне.  
  
-   Для безопасности передачи и проверки подлинности используется безопасность Windows.  
  
-   Для транспорта используется протокол TCP.  
  
-   Реализуется кодирование двоичных сообщений.  
  
-   Реализуется обмен сообщениями WS-Reliable Messaging.  
  
 Дополнительно возможны:  
  
-   Безопасность на уровне сообщений (с использованием WS-Security).  
  
-   Безопасность транспорта с учетными данными сообщений - конфиденциальность и целостность обеспечиваются протоколом TLS через TCP, а учетные данные для проверки подлинности обеспечиваются спецификацией WS-Security.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.NetTcpSecurity>, <xref:System.ServiceModel.TcpTransportSecurity>, <xref:System.ServiceModel.TcpClientCredentialType>, <xref:System.ServiceModel.MessageSecurityOverTcp> и <xref:System.ServiceModel.MessageCredentialType>.  
  
### <a name="netnamedpipebinding"></a>NetNamedPipeBinding  
 В коде используйте <xref:System.ServiceModel.NetNamedPipeBinding> класса; в конфигурации, используйте [ \<netNamedPipeBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/netnamedpipebinding.md).  
  
 Эта привязка оптимизирована для обмена данными между процессами (обычно на одном компьютере). По умолчанию эта привязка имеет следующие характеристики:  
  
-   Для передачи сообщений и проверки подлинности используется безопасность транспорта.  
  
-   Для доставки сообщений используются именованные каналы.  
  
-   Реализуется кодирование двоичных сообщений.  
  
-   Шифрование и подписывание сообщений.  
  
 Дополнительно возможны:  
  
-   Проверка подлинности с использованием безопасности Windows.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.NetNamedPipeSecurity>, <xref:System.ServiceModel.NetNamedPipeSecurityMode> и <xref:System.ServiceModel.NamedPipeTransportSecurity>.  
  
### <a name="msmqintegrationbinding"></a>MsmqIntegrationBinding  
 В коде используйте <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> класса; в конфигурации, используйте [ \<msmqIntegrationBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/msmqintegrationbinding.md).  
  
 Эта привязка оптимизирована для создания клиентов и служб [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], взаимодействующих с конечными точками MSMQ (Microsoft Message Queuing), созданными без использования [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 По умолчанию в этой привязке используется безопасность транспорта и обеспечиваются следующие характеристики безопасности:  
  
-   Система безопасности может быть отключена (None).  
  
-   Безопасность транспорта MSMQ (Transport).  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]<xref:System.ServiceModel.NetMsmqSecurity> и <xref:System.ServiceModel.NetMsmqSecurityMode>.  
  
### <a name="netmsmqbinding"></a>NetMsmqBinding  
 В коде используйте <xref:System.ServiceModel.NetMsmqBinding> класса; в конфигурации, используйте [ \<netMsmqBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md).  
  
 Эта привязка предназначена для использования при создании служб [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], которым требуется поддержка очереди сообщений MSMQ.  
  
 По умолчанию в этой привязке используется безопасность транспорта и обеспечиваются следующие характеристики безопасности:  
  
-   Система безопасности может быть отключена (None).  
  
-   Безопасность транспорта MSMQ (Transport).  
  
-   Безопасность сообщений на основе SOAP (Message).  
  
-   Одновременное использование безопасности транспорта и безопасности сообщений (Both).  
  
-   Поддерживаемые типы учетных данных клиента: None, Windows, UserName, Certificate, IssuedToken.  
  
 Учетные данные типа <xref:System.ServiceModel.MessageCredentialType.Certificate> поддерживаются только в том случае, если задан режим безопасности <xref:System.ServiceModel.NetMsmqSecurityMode.Both> или <xref:System.ServiceModel.NetMsmqSecurityMode.Message>.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]<xref:System.ServiceModel.MessageSecurityOverMsmq> и <xref:System.ServiceModel.MsmqTransportSecurity>.  
  
### <a name="wsfederationhttpbinding"></a>WSFederationHttpBinding  
 В коде используйте <xref:System.ServiceModel.WSFederationHttpBinding> класса; в конфигурации, используйте [ \<wsFederationHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md).  
  
 По умолчанию в этой привязке используется спецификация WS-Security (безопасность на уровне сообщений).  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Федерации](../../../../docs/framework/wcf/feature-details/federation.md), <xref:System.ServiceModel.WSFederationHttpSecurity>, и <xref:System.ServiceModel.WSFederationHttpSecurityMode>.  
  
## <a name="custom-bindings"></a>Пользовательские привязки  
 Если ни одна из предоставляемых системой привязок не удовлетворяет вашим требованиям, можно создать пользовательскую привязку с пользовательским элементом привязки безопасности. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Возможности безопасности при использовании пользовательских привязок](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md).  
  
## <a name="binding-choices"></a>Функции привязок  
 В следующей таблице перечислены функции, обеспечиваемые настройкой режима безопасности; другими словами, перечислены доступные функции, если для режима безопасности задано значение `Transport`, `Message` или `TransportWithMessageCredential`. Эта таблица поможет найти функции безопасности, необходимые для вашего приложения.  
  
|Параметр|Функции|  
|-------------|--------------|  
|Transport|Проверка подлинности сервера<br /><br /> Проверка подлинности клиента<br /><br /> Безопасность типа "точка-точка"<br /><br /> Взаимодействие<br /><br /> Аппаратное ускорение<br /><br /> Высокая пропускная способность<br /><br /> Безопасный брандмауэр<br /><br /> Приложения с большой задержкой<br /><br /> Повторное шифрование по нескольким участкам ретрансляции|  
|Сообщение|Проверка подлинности сервера<br /><br /> Проверка подлинности клиента<br /><br /> Сквозная безопасность<br /><br /> Взаимодействие<br /><br /> Утверждения с широкими функциональными возможностями<br /><br /> Федерация<br /><br /> Многофакторная проверка подлинности<br /><br /> Пользовательские маркеры<br /><br /> Служба удостоверения/метки времени<br /><br /> Приложения с большой задержкой<br /><br /> Сохраняемость сигнатур сообщений|  
|TransportWithMessageCredential|Проверка подлинности сервера<br /><br /> Проверка подлинности клиента<br /><br /> Безопасность типа "точка-точка"<br /><br /> Взаимодействие<br /><br /> Аппаратное ускорение<br /><br /> Высокая пропускная способность<br /><br /> Утверждения клиентов с широкими функциональными возможностями<br /><br /> Федерация<br /><br /> Многофакторная проверка подлинности<br /><br /> Пользовательские маркеры<br /><br /> Безопасный брандмауэр<br /><br /> Приложения с большой задержкой<br /><br /> Повторное шифрование по нескольким участкам ретрансляции|  
  
 В следующей таблице перечислены привязки, поддерживающие различные параметры режима. Выберите в таблице привязку для использования при создании конечной точки своей службы.  
  
|Привязка|Поддержка режима Transport|Поддержка режима Message|Поддержка режима TransportWithMessageCredential|  
|-------------|----------------------------|--------------------------|--------------------------------------------|  
|`BasicHttpBinding`|Да|Да|Да|  
|`WSHttpBinding`|Да|Да|Да|  
|`WSDualHttpBinding`|Нет|Да|Нет|  
|`NetTcpBinding`|Да|Да|Да|  
|`NetNamedPipeBinding`|Да|Нет|Нет|  
|`NetMsmqBinding`|Да|Да|Нет|  
|`MsmqIntegrationBinding`|Да|Нет|Нет|  
|`wsFederationHttpBinding`|Нет|Да|Да|  
  
## <a name="transport-credentials-in-bindings"></a>Учетные данные транспорта в привязках  
 В приведенной ниже таблице перечислены типы учетных данных клиента, доступные при использовании привязки `BasicHttpBinding` или `WSHttpBinding` в режиме безопасности транспорта.  
  
|Тип|Описание:|  
|----------|-----------------|  
|Нет|Указывает, что клиенту не требуется предоставлять учетные данные. Это означает, что клиент является анонимным.|  
|Basic|Обычная проверка подлинности. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]Документе RFC 2617, проверка подлинности HTTP: Basic и дайджест-проверки подлинности, доступных [http://go.microsoft.com/fwlink/?LinkId=84023](http://go.microsoft.com/fwlink/?LinkId=84023).|  
|Digest|Дайджест-проверка подлинности. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]Документе RFC 2617, проверка подлинности HTTP: Basic и дайджест-проверки подлинности, доступных [http://go.microsoft.com/fwlink/?LinkId=84023](http://go.microsoft.com/fwlink/?LinkId=84023).|  
|NTLM|Проверка подлинности NTLM (NT LAN Manager).|  
|Windows|Проверка подлинности Windows.|  
|Сертификат|Проверка подлинности производится с использованием сертификата.|  
|IssuedToken|Позволяет службе потребовать, чтобы проверка подлинности клиента производилась с помощью маркера, выданного службой маркеров безопасности или [!INCLUDE[infocard](../../../../includes/infocard-md.md)]. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Федерация и выданные маркеры](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md).|  
  
### <a name="message-client-credentials-in-bindings"></a>Учетные данные клиента в привязках в режиме Message  
 В приведенной ниже таблице перечислены типы учетных данных клиента, доступные при использовании привязки в режиме безопасности Message.  
  
|Тип|Описание:|  
|----------|-----------------|  
|Нет|Позволяет службе взаимодействовать с анонимными клиентами.|  
|Windows|Позволяет проводить обмен сообщениями SOAP, если выполнена проверка подлинности с помощью учетных данных Windows.|  
|UserName|Позволяет службе запрашивать проверку подлинности клиента на основе учетных данных типа "имя пользователя". Обратите внимание, что если задан режим безопасности `TransportWithMessageCredential`, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] не поддерживает отправку дайджеста пароля или создание ключей с помощью пароля и использование таких ключей для режима безопасности Message. Таким образом, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] принудительно задает безопасность транспорта при использовании учетных данных типа "имя пользователя".|  
|Сертификат|Позволяет службе требовать проверки подлинности клиента с помощью сертификата.|  
|IssuedToken|Позволяет службе использовать службу маркеров безопасности для создания пользовательского маркера.|  
  
## <a name="see-also"></a>См. также  
 [Общие сведения о безопасности](../../../../docs/framework/wcf/feature-details/security-overview.md)  
 [Защита служб и клиентов](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)  
 [Выбор типа учетных данных](../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)  
 [Возможности безопасности при использовании пользовательских привязок](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)  
 [Поведения безопасности](../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)  
 [Модель безопасности для Windows Server App Fabric](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
