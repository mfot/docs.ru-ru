---
title: "Практическое руководство. Написание простого цикла Parallel.ForEach"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- foreach, parallel version
- parallel programming, foreach
ms.assetid: cb5fab92-1c19-499e-ae91-8b7525dd875f
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: bb628c0de1f0e4452ae13b5f5ee392084118bea5
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="how-to-write-a-simple-parallelforeach-loop"></a>Практическое руководство. Написание простого цикла Parallel.ForEach
В этом примере показано, как использовать цикл <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> для включения параллелизма данных в любом источнике данных <xref:System.Collections.IEnumerable?displayProperty=nameWithType> или <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>.  
  
> [!NOTE]
>  В этой документации для определения делегатов в PLINQ используются лямбда-выражения. Если вы не знакомы с лямбда-выражениями в C# или Visual Basic, см. раздел [Лямбда-выражения в PLINQ и TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md).  
  
## <a name="example"></a>Пример  
 [!code-csharp[TPL_Parallel#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/simpleforeach.cs#03)]
 [!code-vb[TPL_Parallel#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/simpleforeach.vb#03)]  
  
 Цикл <xref:System.Threading.Tasks.Parallel.ForEach%2A> действует как цикл <xref:System.Threading.Tasks.Parallel.For%2A>. Исходная коллекция разделяется на секции, и задачи распределяются по нескольким потокам с учетом доступной среды системы. Чем больше в системе процессоров, тем быстрее выполняются параллельные методы. Для некоторых исходных коллекций, в зависимости от размера источника и типа выполняемых работ, последовательный цикл может оказаться быстрее. Дополнительные сведения о производительности см. в статье [Потенциальные ошибки, связанные с параллелизмом данных и задач](../../../docs/standard/parallel-programming/potential-pitfalls-in-data-and-task-parallelism.md).  
  
 Дополнительные сведения о параллельных циклах см. в статье [Практическое руководство. Написание простого цикла Parallel.For](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-for-loop.md).  
  
 Чтобы применить <xref:System.Threading.Tasks.Parallel.ForEach%2A> для неуниверсальной коллекции, вы можете преобразовать ее в универсальную коллекцию с помощью метода расширения <xref:System.Linq.Enumerable.Cast%2A>, как показано в следующем примере.  
  
 [!code-csharp[TPL_Parallel#07](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/nongeneric.cs#07)]
 [!code-vb[TPL_Parallel#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/nongeneric.vb#07)]  
  
 Также вы можете использовать Parallel LINQ (PLINQ) для параллельной обработки источников данных <xref:System.Collections.Generic.IEnumerable%601>. PLINQ позволяет применять декларативный синтаксис запроса для описания поведения цикла. Дополнительные сведения см. в разделе [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md).  
  
## <a name="compiling-the-code"></a>Компиляция кода  
  
-   Скопируйте и вставьте этот код в проект консольного приложения [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 2010.  
  
-   Добавьте ссылку на файл System.Drawing.dll.  
  
-   Нажмите клавишу F5.  
  
## <a name="see-also"></a>См. также  
 [Параллелизм данных](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)  
 [Параллельное программирование](../../../docs/standard/parallel-programming/index.md)  
 [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
