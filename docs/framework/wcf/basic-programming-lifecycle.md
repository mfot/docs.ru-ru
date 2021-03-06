---
title: "Базовый жизненный цикл программирования"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- service creation [WCF]
ms.assetid: 7cf21bfe-23bd-46aa-8033-609f851dbf76
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 4f5c45cad0b1e4ae1aa6b1963e9acdab47cd9203
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="basic-programming-lifecycle"></a>Базовый жизненный цикл программирования
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] позволяет приложениям обмениваться информацией не только в пределах одного компьютера, но и через Интернет, даже если они выполняются на различных платформах. В этом разделе приводятся задачи, которые необходимо выполнить при создании приложения [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Рабочий пример приложения см. в разделе [учебник по началу работы](../../../docs/framework/wcf/getting-started-tutorial.md).  
  
## <a name="the-basic-tasks"></a>Основные задачи  
 Необходимо выполнить следующие основные задачи в указанном порядке:  
  
1.  Определите контракт службы. В контракте службы указывается ее сигнатура, отправляемые и получаемые ей данные и прочие данные, требуемые контрактом. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Проектирование контрактов службы](../../../docs/framework/wcf/designing-service-contracts.md).  
  
2.  Реализуйте контракт. Для реализации контракта службы создайте класс, который реализует этот контракт, и укажите пользовательские режимы работы, которые должна иметь среда выполнения. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Реализация контрактов службы](../../../docs/framework/wcf/implementing-service-contracts.md).  
  
3.  Настройте службу, указав конечные точки и определив прочие сведения о режимах работы. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Настройка служб](../../../docs/framework/wcf/configuring-services.md).  
  
4.  Разместите службу. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Услуг](../../../docs/framework/wcf/hosting-services.md).  
  
5.  Создайте клиентское приложение. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Создание клиентов](../../../docs/framework/wcf/building-clients.md).  
  
 Несмотря на то что подразделы этого раздела приведены именно в таком порядке, некоторые сценарии не начинаются с самого начала. Например, если требуется создать клиент для существующей службы, следует начать с шага 5. При создании службы, которая будет использоваться другими службами, можно пропустить шаг 5.  
  
 После ознакомления с Разработка контрактов службы, также может считывать [введение в расширяемость](../../../docs/framework/wcf/introduction-to-extensibility.md). Если возникают проблемы со службой, проверьте [примеры устранения неполадок WCF](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md) для просмотра, имеют ли другие такие же или аналогичные проблемы.  
  
## <a name="see-also"></a>См. также  
 [Реализация контрактов служб](../../../docs/framework/wcf/implementing-service-contracts.md)
