---
title: "Введение в универсальные шаблоны. (Руководство по программированию на C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "универсальные шаблоны [C#], сведения об универсальных шаблонах"
ms.assetid: a1ad761e-42f7-41dd-a62f-452a2de26b9d
caps.latest.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 32
---
# Введение в универсальные шаблоны. (Руководство по программированию на C#)
Способ, которым универсальные классы и методы сочетают возможность многократного использования, строгую типизацию и эффективность, отличается от способа, используемого их нестандартными аналогами.  Чаще всего универсальные шаблоны используются с функционирующими с ними коллекциями и методами.  Библиотека классов в платформе .NET Framework версии 2.0 предоставляет новое пространство имен, <xref:System.Collections.Generic>, содержащее несколько новых универсальных классов коллекций.  Во всех приложениях, предназначенных для выполнения в [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 2.0 и более поздней версии, вместо старых нестандартных аналогов, таких как <xref:System.Collections.ArrayList>, рекомендуется использовать новые универсальные классы коллекции.  Дополнительные сведения см. в разделе [Универсальные шаблоны в библиотеке классов платформы .NET Framework](../../../csharp/programming-guide/generics/generics-in-the-net-framework-class-library.md).  
  
 Разумеется, чтобы получить собственные типобезопасные и эффективные обобщенные решения и шаблоны разработки, можно создать пользовательские универсальные типы и методы.  В следующем примере кода в демонстрационных целях показан простой универсальный класс, реализующий связанный список.  \(В большинстве случаев следует использовать класс <xref:System.Collections.Generic.List%601>, предоставленный библиотекой классов платформы .NET Framework, а не создавать собственный.\) Параметр\-тип `T` используется в нескольких местах, где конкретный тип обычно использовался бы для указания типа элемента, хранящегося в списке.  Его можно использовать следующим образом:  
  
-   в качестве типа параметра метода в методе `AddHead`;  
  
-   в качестве возвращаемого типа свойства `GetNext` и `Data` открытого метода во вложенном классе `Node`;  
  
-   в качестве типа данных закрытого члена во вложенном классе.  
  
 Обратите внимание, что T доступен для вложенного класса `Node`.  Когда будет создан `GenericList<T>` с конкретным типом, например как `GenericList<int>`, каждое вхождение `T` будет заменено `int`.  
  
 [!code-cs[csProgGuideGenerics#2](../../../csharp/programming-guide/generics/codesnippet/csharp/introduction-to-generics_1.cs)]  
  
 Следующий пример кода показывает, как клиентский код использует класс `GenericList<T>` для создания списка целых чисел.  Благодаря простому изменению аргумента\-типа, следующий код можно легко преобразовать для создания списка строк или любого другого пользовательского типа.  
  
 [!code-cs[csProgGuideGenerics#3](../../../csharp/programming-guide/generics/codesnippet/csharp/introduction-to-generics_2.cs)]  
  
## См. также  
 <xref:System.Collections.Generic>   
 [Руководство по программированию на C\#](../../../csharp/programming-guide/index.md)   
 [Универсальные шаблоны](../../../csharp/programming-guide/generics/index.md)