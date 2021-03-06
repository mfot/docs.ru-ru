---
title: "Значимые трассировки"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 40a1770e-3b09-4142-b0dd-f9ef73642074
caps.latest.revision: "4"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 6641fe633585caf6cbf068a804430f9171e5ece0
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="significant-traces"></a>Значимые трассировки
В этом разделе перечислены некоторые основные трассировки, создаваемые инфраструктурой [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  
  
## <a name="significant-traces"></a>Значимые трассировки  
  
|Трассировка|Описание:|  
|-----------|-----------------|  
|Трассировка журнала сообщений|Трассировка создается, когда сообщение [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] записывается в журнал с помощью функции ведения журнала при включении источника трассировки `System.ServiceModel.MessageLogging`. При щелчке трассировки отображается сообщение. Существует четыре настраиваемые точки ведения журнала для сообщения: `ServiceLevelSendRequest`, `TransportSend`, `TransportReceive`, `ServiceLevelReceiveRequest`, также указанные атрибутом источника сообщений в трассировке журнала сообщений.|  
|Трассировка получения сообщений|Эта трассировка выдается при получении сообщения [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], если источник трассировки `System.ServiceModel` включен на уровне "Данные" или "Подробно". Эта трассировка позволяет просматривать путь корреляции сообщений в представлении графика действий.|  
|Трассировка отправки сообщений|Эта трассировка создается при отправке сообщения [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], если источник трассировки `System.ServiceModel` включен на уровне "Данные" или "Подробно". Эта трассировка позволяет просматривать путь корреляции сообщений в представлении графика действий.|  
|Возвращение ChannelEndpointElement|Эта трассировка создается фабрикой каналов конструктора на уровне "Данные". В ней описывается конечная точка, с которой взаимодействует клиент (удаленный адрес, привязка, имя контракта).|  
|Возвращение ServiceElement|Эта трассировка создается узлом службы конструктора на уровне "Данные". В ней описывается контракт службы и привязка.|  
|Создание SocketConnection|Эта трассировка создается в первом действии процесса, выполненном клиентом, и при получении данных службой. В ней указываются локальный и удаленный IP-адреса. Она выдается на уровне "Данные".|
