---
title: "Практическое руководство. Использование моникера службы с контрактами обмена метаданными"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c41a07e5-cb9d-45d6-9ea4-34511e227faf
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 7d2b5b6d4a671a3eb281f49dd60fd3c00ee76f8a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-use-a-service-moniker-with-metadata-exchange-contracts"></a>Практическое руководство. Использование моникера службы с контрактами обмена метаданными
Разработав несколько новых служб [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], вы, возможно, решите предусмотреть возможность вызова данных служб из скрипта или приложения на Visual Basic 6.0. Один способ - это создание клиентской сборки [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], регистрация сборки с помощью COM, установка сборки в глобальном кэше сборок, а затем ссылка на COM-типы из кода на Visual Basic. При распространении приложения также потребуется распространять клиентскую сборку [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Затем пользователь должен будет зарегистрировать клиентскую сборку WCF с помощью COM и разместить ее в глобальном кэше сборок. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] COM Interop также позволяет выполнять вызовы той же службы без клиентской сборки [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Моникер [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] позволяет вызывать любую службу [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] из любого COM-совместимого языка (Visual Basic, VBScript, Visual Basic for Applications (VBA) и т. п.) путем указания универсального кода ресурса (URI) конечной точки обмена метаданными (Mex), используемого моникером для извлечения типовой информации о службе. В настоящем разделе описывается, как вызывать пример начала работы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] с помощью моникера [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], указывающего конечную точку обмена метаданными (Mex).  
  
> [!NOTE]
>  Типы, определенные клиентской сборкой [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], фактически не используются для создания экземпляра. Сборка используется только для метаданных.  
  
### <a name="using-the-service-moniker-with-a-mex-address"></a>Использование моникера службы с адресом обмена метаданными (Mex)  
  
1.  Создайте пример начала работы и с помощью Internet Explorer перейдите по его URL-адресу (http://localhost/ServiceModelSamples/Service.svc), чтобы удостовериться в работоспособности службы.  
  
2.  Создайте скрипт Visual Basic или приложение Visual Basic, содержащее следующий код:  
  
    ```  
    monString = "service:mexaddress=http://localhost/ServiceModelSamples/Service.svc/MEX"  
    monString = monString + ", address=http://localhost/ServiceModelSamples/Service.svc"  
    monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", binding=WSHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
  
    Set calc = GetObject(monString)  
    MsgBox calc.Add(3, 4)  
    ```  
  
3.  Запустите приложение или скрипт Visual Basic.  
  
    > [!NOTE]
    >  Вызываемая служба должна экспонировать конечную точку обмена метаданными (Mex) в моникер, чтобы прочитать метаданные из службы. Дополнительные сведения см. в разделе [как: публикация метаданных для службы с помощью файла конфигурации](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md).  
  
    > [!NOTE]
    >  Если моникер сформирован неправильно или служба недоступна, при вызове `GetObject` будет возвращена ошибка "Синтаксическая ошибка".  При получении этой ошибки убедитесь, что используется правильный моникер, а служба доступна.  
  
## <a name="see-also"></a>См. также  
 [Практическое руководство. Использование моникера службы Windows Communication Foundation без регистрации](../../../../docs/framework/wcf/feature-details/use-the-wcf-service-moniker-without-registration.md)  
 [Практическое руководство. Использование моникера службы с контрактами WSDL](../../../../docs/framework/wcf/feature-details/how-to-use-a-service-moniker-with-wsdl-contracts.md)
