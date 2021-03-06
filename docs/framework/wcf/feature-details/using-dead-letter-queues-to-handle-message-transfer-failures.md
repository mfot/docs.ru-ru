---
title: "Использование очередей недоставленных сообщений для обработки сбоев при передаче сообщений"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 9e891c6a-d960-45ea-904f-1a00e202d61a
caps.latest.revision: "19"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 9f10b3895fcdea0c3ab80617acd9874953b7665e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="using-dead-letter-queues-to-handle-message-transfer-failures"></a>Использование очередей недоставленных сообщений для обработки сбоев при передаче сообщений
Сообщения в очереди могут вызвать сбой доставки. Сообщения, во время доставки которых произошел сбой, записываются в очередь недоставленных сообщений. Сбой доставки может быть вызван такими причинами, как сбои сети, удаленная очередь, заполнение очереди, сбой проверки подлинности или сбой доставки по времени.  
  
 Сообщения могут длительное время оставаться в очереди, если принимающее приложение не считывает их из очереди за отведенное время. Такое поведение может не быть свойственно чувствительным к времени сообщениям. Критичные к времени сообщения имеют свойство срок жизни (TTL), заданное в привязке с очередью, которое указывает, насколько долго сообщения могут находиться в очереди до истечения срока действия. Просроченные сообщения отправляются в специальную очередь, называемую очередью недоставленных сообщений. Сообщения могут быть помещены в очередь недоставленных сообщений и по другим причинам, таким как превышение квоты очереди или сбой проверки подлинности.  
  
 Обычно для прочтения сообщений из очереди недоставленных сообщений и причин сбоя приложения записывают компенсирующую логику. Компенсирующая логика зависит от причины сбоя. Например, в случае сбоя проверки подлинности можно исправить сертификат, прикрепленный к сообщению, и отправить сообщение повторно. Если сбой доставки произошел по причине достижения квоты целевой очереди, можно повторить попытку отправки в надежде, что проблема с квотой была устранена.  
  
 Большинство систем организации очереди имеют общесистемную очередь недоставленных сообщений, в которой хранятся все сообщения данной системы, во время доставки которых произошел сбой. Очередь сообщений (MSMQ) имеет две общесистемные очереди недоставленных сообщений: общесистемная очередь недоставленных транзакционных сообщений, в которой хранятся сообщения, по причине сбоя не доставленные в транзакционную очередь, и общесистемная очередь недоставленных нетранзакционных сообщений, в которой хранятся сообщения, по причине сбоя не доставленные в нетранзакционную очередь. Если два клиента отправляют сообщения в две разные службы, то есть разные очереди в [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] одновременно используют одну службу MSMQ для отправки, в системной очереди недоставленных сообщений возможна смесь сообщений. Это не всегда оптимально. В некоторых случаях (по соображениям безопасности, например), может быть нежелательно, чтобы один клиент прочел сообщения другого клиента из очереди недоставленных сообщений. При использовании общей очереди недоставленных сообщений клиенты также вынуждены просматривать всю очередь, чтобы найти отправленное ими сообщение, что, в зависимости от количества сообщений в очереди недоставленных сообщений, может оказаться чрезмерно дорого. Таким образом, в [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] `NetMsmqBinding`, `MsmqIntegrationBinding,` и MSMQ на [!INCLUDE[wv](../../../../includes/wv-md.md)] предоставляют пользовательской очереди недоставленных сообщений (иногда называют очереди недоставленных сообщений конкретного приложения).  
  
 Пользовательская очередь недоставленных сообщений обеспечивает изоляцию между клиентами, использующими для отправки сообщений одну службу MSMQ.  
  
 В [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] и [!INCLUDE[wxp](../../../../includes/wxp-md.md)], [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] предоставляет общесистемную очередь недоставленных сообщений для всех клиентских приложений в очереди. В [!INCLUDE[wv](../../../../includes/wv-md.md)], [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] предоставляет очередь недоставленных сообщений каждому клиентскому приложению в очереди.  
  
## <a name="specifying-use-of-the-dead-letter-queue"></a>Указание использования очереди недоставленных сообщений  
 Очередь недоставленных сообщений находится в диспетчере очереди отправляющего приложения. В диспетчере очереди хранятся сообщения с истекшим сроком или сообщения, во время передачи или доставки которых произошел сбой.  
  
 Привязка имеет следующие свойства очереди недоставленных писем.  
  
-   <xref:System.ServiceModel.MsmqBindingBase.DeadLetterQueue%2A>  
  
-   <xref:System.ServiceModel.MsmqBindingBase.CustomDeadLetterQueue%2A>  
  
## <a name="reading-messages-from-the-dead-letter-queue"></a>Чтение сообщений из очереди недоставленных сообщений  
 Приложение, считывающее сообщения из очереди недоставленных сообщений, похоже на службу [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], считывающую сообщения из очереди приложения, кроме следующих незначительных отличий.  
  
-   Для чтения сообщений из системной очереди недоставленных транзакционных сообщений универсальный код ресурса (URI) должен иметь вид net.msmq://localhost/system$;DeadXact.  
  
-   Для чтения сообщений из системной очереди недоставленных нетранзакционных сообщений код URI должен иметь вид net.msmq://localhost/system$;DeadLetter.  
  
-   Для чтения сообщений из пользовательской очереди недоставленных сообщений, код URI должен иметь форму: net.msmq://localhost/private/\<*имя пользовательского-очередь dlq*> где *имя пользовательского-очередь dlq* имя пользовательской очередь недоставленных сообщений.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]адрес очереди см. в разделе [конечные точки служб и адресация очереди](../../../../docs/framework/wcf/feature-details/service-endpoints-and-queue-addressing.md).  
  
 Стек приемника [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] сопоставляет адреса, по которым служба ожидает данные, адресу в сообщении. Если адреса совпадают, сообщение отправляется, если нет - не отправляется. Это может создать проблемы при чтении сообщений из очереди недоставленных сообщений, поскольку сообщения в очереди недоставленных сообщений обычно адресованы не службе и не службе очереди отправленных сообщений. Поэтому для чтения службой сообщений из очереди недоставленных сообщений необходима установка фильтра по адресу `ServiceBehavior`, которая дает команду стеку считать совпадающими все сообщения в очереди независимо от адресата. В частности, нужно добавить `ServiceBehavior` при помощи параметра <xref:System.ServiceModel.AddressFilterMode.Any>в службу, считывающую сообщения из очереди недоставленных сообщений.  
  
## <a name="poison-message-handling-from-the-dead-letter-queue"></a>Обработка подозрительных сообщений из очереди недоставленных сообщений  
 При некоторых условиях в очередях недоставленных сообщений возможна обработка подозрительных сообщений. Поскольку создать вложенные очереди из системных очередей нельзя, `ReceiveErrorHandling` при прочтении из системной очереди недоставленных сообщений не может быть установлен в значение `Move`. Обратите внимание, что при чтении сообщений из пользовательской очереди недоставленных сообщений могут использоваться вложенные очереди, и, таким образом, `Move` является подходящим средством удаления подозрительного сообщения.  
  
 Если `ReceiveErrorHandling` установлен в значение `Reject`, подозрительные сообщения при чтении из пользовательской очереди недоставленных сообщений помещаются в системную очередь недоставленных сообщений. При чтении из системной очереди недоставленных сообщений сообщение отбрасывается (удаляется). При возврате из системной очереди недоставленных сообщений в MSMQ сообщение отбрасывается (удаляется).  
  
## <a name="example"></a>Пример  
 В приведенном ниже примере показано, как создавать очередь недоставленных сообщений и как использовать ее для обработки просроченных сообщений. Пример основан на примере в [как: Exchange в очередь сообщения с конечными точками WCF](../../../../docs/framework/wcf/feature-details/how-to-exchange-queued-messages-with-wcf-endpoints.md). В приведенном ниже примере показано, как писать клиентский код для службы обработки заказов, в которой используется очередь недоставленных сообщений для каждого приложения. В примере также показано, как обрабатывать сообщения из очереди недоставленных сообщений.  
  
 В следующем примере показан код для клиента, задающего очередь недоставленных сообщений для каждого приложения.  
  
 [!code-csharp[S_DeadLetter#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_deadletter/cs/client.cs#1)]
 [!code-vb[S_DeadLetter#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_deadletter/vb/client.vb#1)]  
  
 В следующем примере показан код для файла конфигурации клиента.  
  
  
  
 В следующем примере показан код для службы обработки сообщений из очереди недоставленных сообщений.  
  
 [!code-csharp[S_DeadLetter#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_deadletter/cs/dlservice.cs#3)]
 [!code-vb[S_DeadLetter#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_deadletter/vb/dlservice.vb#3)]  
  
 В следующем примере показан код для файла конфигурации службы очереди недоставленных сообщений.  
  
  
  
## <a name="see-also"></a>См. также  
 [Общие сведения об очередях](../../../../docs/framework/wcf/feature-details/queues-overview.md)  
 [Практическое руководство. Обмен сообщениями в очереди с конечными точками WCF](../../../../docs/framework/wcf/feature-details/how-to-exchange-queued-messages-with-wcf-endpoints.md)  
 [Обработка подозрительных сообщений](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)
