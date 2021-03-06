---
title: "Пошаговое руководство. Запросы по связям (Visual Basic)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- vb
ms.assetid: a7da43e3-769f-4e07-bcd6-552b8bde66f4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: fef9880d5f9fa652eab2eb0d17bbf782dc64773d
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="walkthrough-querying-across-relationships-visual-basic"></a>Пошаговое руководство. Запросы по связям (Visual Basic)
В этом пошаговом руководстве демонстрируется использование [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] *ассоциации* для представления связей внешних ключей в базе данных.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Это пошаговое руководство было написано с помощью параметров разработки Visual Basic.  
  
## <a name="prerequisites"></a>Предварительные требования  
 Необходимо выполнить [Пошаговое руководство: простая модель объекта и запрос (Visual Basic)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-simple-object-model-and-query-visual-basic.md). На этом пошаговом руководстве основано руководство, описываемое в данном разделе. В частности на компьютере должен иметься файл northwnd.mdf в папке c:\linqtest.  
  
## <a name="overview"></a>Обзор  
 Данное пошаговое руководство состоит из трех основных задач.  
  
-   Добавление класса сущности, который представляет таблицу "Orders" в базе данных "Northwind".  
  
-   Добавление примечаний к классу `Customer`, чтобы расширить связи между классами `Customer` и `Order`.  
  
-   Создание и выполнение запроса для тестирования процесса получения сведений класса `Order` с помощью класса `Customer`.  
  
## <a name="mapping-relationships-across-tables"></a>Сопоставление связей между таблицами  
 После определения класса `Customer` создайте определение класса сущностей `Order`, включающее следующий код, который указывает, что свойство `Orders.Customer` связано как внешний ключ со свойством `Customers.CustomerID`.  
  
#### <a name="to-add-the-order-entity-class"></a>Добавление класса сущностей "Order"  
  
-   Введите или вставьте следующий код после определения класса `Customer`.  
  
     [!code-vb[DLinqWalk2VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#1)]  
  
## <a name="annotating-the-customer-class"></a>Добавление примечаний к классу "Customer"  
 На этом этапе добавляются примечания к классу `Customer`, чтобы указать его связь с классом `Order`. (Это добавление не является обязательным, поскольку для создания связи достаточно создать определение связи в любом направлении. Однако добавление этого примечания позволит с легкостью переходить по объектам в любом направлении.)  
  
#### <a name="to-annotate-the-customer-class"></a>Добавление примечаний к классу "Customer"  
  
-   Введите или вставьте следующий код в класс `Customer`.  
  
     [!code-vb[DLinqWalk2VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#2)]  
  
## <a name="creating-and-running-a-query-across-the-customer-order-relationship"></a>Создание и выполнение запроса в рамках связи "Customer-Order"  
 Теперь можно получить доступ к объектам `Order` непосредственно из объектов `Customer` или в обратном направлении. Нет необходимости явно *соединения* между клиентами и заказами.  
  
#### <a name="to-access-order-objects-by-using-customer-objects"></a>Получение доступа к объектам "Order" с помощью объектов "Customer"  
  
1.  Измените метод `Sub Main` посредством ввода или вставки в метод следующего кода:  
  
     [!code-vb[DLinqWalk2VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#3)]  
  
2.  Нажмите клавишу F5, чтобы начать отладку приложения.  
  
     В окне сообщения отобразятся два имени, и в окне "Консоль" появится созданный код SQL.  
  
3.  Закройте окно сообщения, чтобы остановить отладку.  
  
## <a name="creating-a-strongly-typed-view-of-your-database"></a>Создание строго типизированного представления базы данных  
 Общая процедура становится гораздо проще, если в начале использовать строго типизированное представление базы данных. Задавая строгую типизацию объекта <xref:System.Data.Linq.DataContext>, можно избежать вызовов метода <xref:System.Data.Linq.DataContext.GetTable%2A>. Строго типизированные таблицы можно использовать в запросах только при использовании строго типизированного объекта <xref:System.Data.Linq.DataContext>.  
  
 В представленных ниже шагах создается объект `Customers` в качестве строго типизированной таблицы, которая сопоставляется с таблицей "Customers" в базе данных.  
  
#### <a name="to-strongly-type-the-datacontext-object"></a>Установка строгой типизации объекта "DataContext"  
  
1.  Добавьте следующий код непосредственно перед объявлением класса `Customer`.  
  
     [!code-vb[DLinqWalk2VB#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#4)]  
  
2.  Измените метод `Sub Main`, чтобы использовать строго типизированный объект <xref:System.Data.Linq.DataContext>, как показано ниже:  
  
     [!code-vb[DLinqWalk2VB#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#5)]  
  
3.  Нажмите клавишу F5, чтобы начать отладку приложения.  
  
     В окне «Консоль"» отобразится следующее.  
  
     `ID=WHITC`  
  
4.  Чтобы закрыть приложение, в окне "Консоль" нажмите клавишу ВВОД.  
  
5.  На **файл** меню, нажмите кнопку **сохранить все** Если вы хотите сохранить это приложение.  
  
## <a name="next-steps"></a>Следующие шаги  
 Следующего пошагового руководства ([Пошаговое руководство: управление данными (Visual Basic)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-manipulating-data-visual-basic.md)) демонстрирует способ обработки данных. Для этого пошагового руководства не требуется сохранять два пошаговых руководства, которые уже выполнены в этой серии.  
  
## <a name="see-also"></a>См. также  
 [Обучение с использованием пошаговых руководств](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)
