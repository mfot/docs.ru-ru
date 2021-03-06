---
title: "Контракты"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WCF [WCF], contracts
- contracts [WCF]
- Windows Communication Foundation [WCF], contracts
ms.assetid: c8364183-4ac1-480b-804a-c5e6c59a5d7d
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 9a45fc606ac962b4dc7aac8b49ed9a3c6c421ccd
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="contracts"></a>Контракты
В настоящем разделе описывается, как определить и реализовать контракты [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]. Контракт службы указывает, какую информацию конечная точка передает во внешний мир. На более конкретном уровне, это выписка о наборе специальных сообщений, объединенных в такие базовые шаблоны обмена сообщениями (MEP), как запрос/ответ, односторонний обмен и дуплексный обмен. Если контракт службы является логически связанным набором обмена сообщениями, операция службы - это обмен одним сообщением. Например, операция `Hello` явно должна явно принять одно сообщение (к примеру, вызывающая сторона может объявить приветствие) и может вернуть или не вернуть сообщение (в зависимости от характера операции).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]контракты и другие основные [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] см. основные понятия, [основные понятия Windows Communication Foundation](../../../../docs/framework/wcf/fundamental-concepts.md). В данном разделе рассматриваются контракты служб. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]контракты способ построения клиентов, использующих службу для подключения к службам см. в разделе [Общие сведения о клиенте WCF](../../../../docs/framework/wcf/wcf-client-overview.md). [!INCLUDE[crabout](../../../../includes/crabout-md.md)]клиентские каналы, архитектуры клиента и других проблем клиента. в разделе [клиентов](../../../../docs/framework/wcf/feature-details/clients.md).  
  
## <a name="overview"></a>Обзор  
 В настоящем разделе дается высокоуровневое введение в принципы разработки и реализации служб [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. В подразделах приводятся более подробные сведения об особенностях разработки и реализации. Перед разработкой и реализацией приложения [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] рекомендуется:  
  
-   понять, что представляет собой контракт службы, как он работает и как его создать;  
  
-   понять, что контракты устанавливают минимальные требования, которые конфигурация среды выполнения или среда размещения могут не поддерживать.  
  
## <a name="service-contracts"></a>Контракты служб  
 Контракт службы - это заявление, в котором принимаются обязательства в отношении:  
  
-   группирования операций в службу;  
  
-   сигнатуры операций, связанной с обменом сообщениями;  
  
-   типов данных этих сообщений;  
  
-   расположения операций;  
  
-   специальных протоколов и форматов сериализации, используемых для поддержки успешной связи со службой.  
  
 Например, контракт, связанный с заказом на поставку, может содержать операцию `CreateOrder`, которая принимает входные данные о типах информации заказа и возвращает информацию об успешности или сбое, включая идентификатор заказа. Он также может содержать операцию `GetOrderStatus`, которая принимает идентификатор заказа и возвращает информацию о состоянии заказа. Контракт службы этого типа указывает:  
  
-   что контракт, связанный с заказом на поставку, состоит из операций `CreateOrder` и `GetOrderStatus`;  
  
-   что операции имеют заданные входные и выходные сообщения;  
  
-   данные, которые могут передаваться в этих сообщениях;  
  
-   категорические заявления об инфраструктуре связи, необходимые для успешной обработки сообщений. Например, эти сведения включают данные о том, требуются ли какие-либо формы безопасности для установления успешной связи, и какие конкретно формы безопасности.  
  
 Для передачи, подобные сведения для приложений на других платформах (включая платформы не Майкрософт), контрактов службы XML публично выражаются в стандартных форматах XML, таких как [языка описания веб-служб (WSDL)](http://go.microsoft.com/fwlink/?LinkId=87004) и [схемы XML (XSD)](http://go.microsoft.com/fwlink/?LinkId=87005), среди прочего. Разработчики многих платформ могут использовать эти открытые данные контрактов для создания приложений, которые могут взаимодействовать со службой, поскольку они понимают язык спецификации, и эти языки позволяют обеспечить возможность взаимодействия, описывая открытые формы, форматы и протоколы, поддерживаемые службой. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]как [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] обрабатывает этот тип данных, в разделе [метаданные](../../../../docs/framework/wcf/feature-details/metadata.md).  
  
 Контракты могут выражаться различными способами. Хотя языки WSDL и XSD отлично подходят для описания служб доступным способом, их трудно использовать непосредственно, и они представляют просто описания службы, а не реализации контракта службы. Поэтому приложения [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] используют управляемые атрибуты, интерфейсы и классы как для определения структуры службы, так и для ее реализации.  
  
 Получающийся контракт, определенный в управляемых типах, которые можно преобразовать (также называется *экспортировать*) как метаданные — WSDL и XSD — Если требуется клиентам или другим ответственным за реализацию службы, особенно на других платформах. Результат — простая модель программирования, которая может быть описана с использованием открытых метаданных для любого клиентского приложения. Подробности базовых сообщений SOAP, такие как информация о транспорте и безопасности, могут быть предоставлены [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], который автоматически выполняет необходимые преобразования в систему типа контракта службы и из системы типа контракта службы в систему типа XML.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Проектирование контрактов, в разделе [проектирование контрактов службы](../../../../docs/framework/wcf/designing-service-contracts.md). [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Реализация контрактов, в разделе [реализация контрактов службы](../../../../docs/framework/wcf/implementing-service-contracts.md).  
  
 Кроме того, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] дает возможность разрабатывать контракты службы целиком на уровне сообщения. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Разработка контрактов службы на уровне сообщений. в разделе [использование контрактов сообщений](../../../../docs/framework/wcf/feature-details/using-message-contracts.md). [!INCLUDE[crabout](../../../../includes/crabout-md.md)]разработке службы в не - SOAP XML, см. [взаимодействие с приложениями POX](../../../../docs/framework/wcf/feature-details/interoperability-with-pox-applications.md).  
  
### <a name="understanding-the-hierarchy-of-requirements"></a>Понимание иерархии требований  
 В контракте службы группируются операции, задаются шаблон обмена сообщениями, типы сообщений и типы данных, передаваемых в этих сообщениях, а также указываются категории поведения во время выполнения, которые должны быть предусмотрены в реализации для поддержки контракта (например, может требоваться, чтобы сообщения шифровались и подписывались). В самом контракте службы, однако, точно не указывается, как удовлетворяются эти требования, а указывается только то, что они должны быть удовлетворены. Выбор типа шифрования или способа, с помощью которого подписывается сообщение, определяются реализацией и конфигурацией совместимой службы.  
  
 Обратите внимание на то, каким способом контракт предъявляет определенные требования к реализации контракта службы и конфигурации среды выполнения для добавления поведения. Набор требований, которые должны быть удовлетворены для передачи службы в использование, основывается на предыдущем наборе требований. Если контракт предъявляет некоторые требования к реализации, реализация может предъявлять дополнительные требования к конфигурации и привязкам, которые позволяют запустить службу. Наконец, ведущее приложение должно также поддерживать любые требования, добавляемые конфигурацией и привязками службы.  
  
 Этот аддитивный процесс предъявления требований важно иметь в виду при разработке, реализации, настройке и размещении приложения службы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]. Например, в контракте может указываться, что ему требуется для поддержки сеанса. В этом случае необходимо настроить привязку для поддержки этого требования контракта, иначе реализация службы работать не будет. Если же служба требует встроенной проверки подлинности Windows и размещается в службах IIS, в веб-приложении, где находится служба, то должна быть включена встроенная проверка подлинности Windows и отключена поддержка анонимных обращений. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]возможности и влияние типов узла приложения другую службу, в разделе [размещения](../../../../docs/framework/wcf/feature-details/hosting.md).  
  
## <a name="see-also"></a>См. также  
 [Конечные точки: адреса, привязки и контракты](../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)  
 [Разработка контрактов службы](../../../../docs/framework/wcf/designing-service-contracts.md)  
 [Реализация контрактов служб](../../../../docs/framework/wcf/implementing-service-contracts.md)
