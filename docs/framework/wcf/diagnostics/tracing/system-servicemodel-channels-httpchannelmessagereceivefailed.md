---
title: System.ServiceModel.Channels.HttpChannelMessageReceiveFailed
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9eb311da-fdcc-4dd3-9d85-05b3280dfdda
caps.latest.revision: "6"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 46bc39237f0a6f0b9b25b9616782ec3e97fa22ca
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="systemservicemodelchannelshttpchannelmessagereceivefailed"></a>System.ServiceModel.Channels.HttpChannelMessageReceiveFailed
Сбой получения сообщения по каналу HTTP.  
  
## <a name="description"></a>Описание:  
 Данная трассировка может выдаваться в качестве предупреждения или ошибки. В обоих случаях трассировка выдается, если при входящем HTTP-запросе не найден совместимый прослушиватель и HTTP-запрос получил отказ. Это может произойти по той причине, что HTTP-команда запроса не была распознана прослушивателем HTTP, либо потому что прослушиватель ожидал передачи данных по адресу, на который был направлен запрос. Данная трассировка выдается как предупреждение при независимом размещении и как ошибка при размещении службы в IIS.  
  
## <a name="see-also"></a>См. также  
 [Трассировка](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)  
 [Использование трассировки для устранения неполадок приложения](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)  
 [Администрирование и диагностика](../../../../../docs/framework/wcf/diagnostics/index.md)
