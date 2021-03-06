---
title: "Оболочки COM"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- wrapper classes
- COM interop, COM wrappers
- COM wrappers
- COM, wrappers
- interoperation with unmanaged code, COM wrappers
- COM callable wrappers
ms.assetid: e56c485b-6b67-4345-8e66-fd21835a6092
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: b899ed162fa626f8c378923907f275cebf9a7db4
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="com-wrappers"></a>Оболочки COM
Модель COM имеет несколько важных отличий от объектной модели .NET Framework:  
  
-   Клиенты COM-объектов должны управлять временем существования этих объектов. В общеязыковой среде выполнения управление временем существования объектов осуществляет сама среда.  
  
-   Клиенты COM-объектов определяют доступность службы, запрашивая интерфейс, который ее предоставляет, в результате чего возвращается или не возвращается указатель на интерфейс. Клиенты объектов .NET могут получать описание функциональных возможностей объекта с помощью отражения.  
  
-   Объекты .NET располагаются в памяти под управлением среды выполнения .NET Framework. Среда выполнения может перемещать объекты в памяти в целях оптимизации производительности и обновлять все ссылки на перемещаемые объекты. Неуправляемые клиенты после получения указателя на объект работают с объектом, находящимся в указанном расположении. У этих клиентов отсутствуют механизмы для работы с объектами, не имеющими фиксированного расположения.  
  
 Чтобы обойти эти различия, среда выполнения предоставляет классы-оболочки, которые моделируют вызов объектов в соответствующих им средах для управляемых и неуправляемых клиентов. Каждый раз, когда управляемый клиент вызывает метод для COM-объекта, среда выполнения создает [вызываемую оболочку времени выполнения](../../../docs/framework/interop/runtime-callable-wrapper.md) (RCW). Помимо прочего, вызываемая оболочка времени выполнения позволяет абстрагировать различия между управляемыми и неуправляемыми механизмами ссылок. Среда выполнения также создает [вызываемую оболочку COM](../../../docs/framework/interop/com-callable-wrapper.md) (CCW) для работы в обратном направлении, когда COM-клиенту требуется вызвать метод для объекта .NET. Как показано на следующем рисунке, класс-оболочка, который создается средой выполнения, зависит от контекста вызывающего кода.  
  
 ![Общие сведения об оболочках COM](../../../docs/framework/interop/media/bidirectional.gif "bidirectional")  
Общие сведения об оболочках COM  
  
 В большинстве случаев стандартная вызываемая оболочка времени выполнения или вызываемая оболочка COM, создаваемая средой выполнения, реализует маршалинг вызовов, которые выполняются между средами COM и .NET Framework. С помощью настраиваемых атрибутов при необходимости можно определить способ представления управляемого и неуправляемого кода в среде выполнения.  
  
## <a name="see-also"></a>См. также  
 [Расширенное COM-взаимодействие](http://msdn.microsoft.com/library/3ada36e5-2390-4d70-b490-6ad8de92f2fb)  
 [Вызываемая оболочка времени выполнения](../../../docs/framework/interop/runtime-callable-wrapper.md)  
 [Вызываемая оболочка COM](../../../docs/framework/interop/com-callable-wrapper.md)  
 [Настройка стандартных оболочек](http://msdn.microsoft.com/library/c40d089b-6a3c-41b5-a20d-d760c215e49d)  
 [Практическое руководство. Настройка вызываемых оболочек времени выполнения](http://msdn.microsoft.com/library/4a4bb3da-4d60-4517-99f2-78d46a681732)
