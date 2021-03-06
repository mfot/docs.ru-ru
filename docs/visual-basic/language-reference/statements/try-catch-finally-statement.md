---
title: "Оператор Try... Catch... Finally (Visual Basic)"
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Try...Catch...Finally
- vb.when
- vb.Finally
- vb.Catch
- vb.Try
helpviewer_keywords:
- Try...Catch...Finally statements
- Try statement [Visual Basic]
- try-catch exception handling, Try...Catch...Finally statements
- error handling, while running code
- Try statement [Visual Basic], Try...Catch...Finally
- Finally keyword [Visual Basic], Try...Catch...Finally
- Catch statement [Visual Basic]
- When keyword [Visual Basic]
- Visual Basic code, handling errors while running
- structured exception handling, Try...Catch...Finally statements
ms.assetid: d6488026-ccb3-42b8-a810-0d97b9d6472b
caps.latest.revision: "69"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: c297a84b37b455a4b30b1848aa9bdd30dc567ec1
ms.sourcegitcommit: 34ec7753acf76f90a0fa845235ef06663dc9e36e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="trycatchfinally-statement-visual-basic"></a>Оператор Try... Catch... Finally (Visual Basic)
Позволяет обрабатывать некоторые или все возможные ошибки, которые могут возникать в конкретном блоке кода, не прерывая выполнение кода.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
Try  
    [ tryStatements ]  
    [ Exit Try ]  
[ Catch [ exception [ As type ] ] [ When expression ]  
    [ catchStatements ]  
    [ Exit Try ] ]  
[ Catch ... ]  
[ Finally  
    [ finallyStatements ] ]  
End Try  
```  
  
## <a name="parts"></a>Части  
  
|Термин|Определение|  
|---|---|  
|`tryStatements`|Необязательный. Операторы, в которых может возникнуть ошибка. Может быть составным оператором.|  
|`Catch`|Необязательный. Несколько `Catch` допускается блоков. Если исключение возникает при обработке `Try` блокировать друг `Catch` инструкция является проверяются в порядке следования, чтобы определить, является ли он обрабатывает исключение, с `exception` представляет исключение, которое создано.|  
|`exception`|Необязательный. Любое имя переменной. Начальное значение `exception` — это значение возникшей ошибки. При использовании `Catch` ошибок перехвачено. Если не указано, `Catch` инструкции перехватывает все исключения.|  
|`type`|Необязательный. Указывает тип класса фильтра. Если значение `exception` имеет тип, заданный параметром `type` или производного типа, данный идентификатор становится привязкой к объекту исключения.|  
|`When`|Необязательный. Объект `Catch` инструкции с `When` перехватывают исключения только если `expression` равен `True`. Объект `When` предложение применяется только после проверки типа исключения, и `expression` может ссылаться на идентификатор, представляющий исключение.|  
|`expression`|Необязательный. Должно быть неявно преобразуемым в `Boolean`. Любое выражение, которое описывает универсальный фильтр. Обычно используется для фильтрации по номеру ошибки. При использовании `When` ключевое слово для определения условий, при которых была перехвачена данная ошибка.|  
|`catchStatements`|Необязательный. Операторы обработки ошибок, возникающих в соответствующем `Try` блока. Может быть составным оператором.|  
|`Exit Try`|Необязательный. Ключевое слово, которое нарушает из `Try...Catch...Finally` структуры. Выполнение возобновляется с кода, непосредственно следующего `End Try` инструкции. `Finally` Инструкция будет выполняться. Не допускается в `Finally` блоков.|  
|`Finally`|Необязательный. Объект `Finally` блок выполняется всегда, когда выполнение перемещается из любой части `Try...Catch` инструкции.|  
|`finallyStatements`|Необязательный. Операторы, выполняемые после всех других действий по обработке ошибки.|  
|`End Try`|Завершает `Try...Catch...Finally` структуры.|  
  
## <a name="remarks"></a>Примечания  
 Если предполагается, что конкретное исключение может произойти во время соответствующего раздела кода, необходимо поместить код `Try` блокировку и использовать `Catch` блок для сохранения управления и обработки исключения, если это происходит.  
  
 Объект `Try…Catch` оператор состоит из `Try` блока, а затем по одному или нескольким `Catch` предложений, задающих обработчики для различных исключений. Если создается исключение `Try` блока [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] ищет `Catch` оператор, который обрабатывает исключение. Если соответствующий `Catch` оператор не найден, [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] проверяет метод, который вызвал текущий метод, и так далее вверх по стеку вызовов. Если не `Catch` блокировка найдена, [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] отображает пользователю сообщение о необработанном исключении и останавливает выполнение программы.  
  
 Можно использовать более одного `Catch` инструкции в `Try…Catch` инструкции. При этом порядок `Catch` предложений важно, поскольку они проверяются в порядке. Перехватывайте более конкретные исключения перед менее конкретными.  
  
 Следующие `Catch` бы определенные инструкции условия и будет перехватывать все исключения, производные от <xref:System.Exception> класса. Обычно следует использовать один из этих вариантов на последнем `Catch` блока в `Try...Catch...Finally` структуры после перехвата определенных исключений, предполагается, что. Поток управления никогда не может достичь `Catch` блока, который соответствует любой из этих вариантов.  
  
-   `type` — `Exception`, Например:`Catch ex As Exception`  
  
-   Оператор не имеет `exception` переменной, например:`Catch`  
  
 При `Try…Catch…Finally` инструкции вложен в другой `Try` блока [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] сначала проверяет каждый `Catch` инструкции в внутренний `Try` блока. Если совпадений `Catch` оператор найден, поиск продолжается `Catch` операторы внешнего `Try…Catch…Finally` блока.  
  
 Локальные переменные из `Try` блок не доступны в `Catch` заблокирован, поскольку это отдельные блоки. Если вы хотите использовать переменную в нескольких блоках, объявите переменную за пределами `Try...Catch...Finally` структуры.  
  
> [!TIP]
>  `Try…Catch…Finally` Оператор доступен в виде фрагмента кода IntelliSense. В диспетчере фрагментов кода разверните **шаблоны кода: If, For Each, Try Catch, свойство, и т. д**, а затем **обработка ошибок (исключения)**. Дополнительные сведения см. в статье [Фрагменты кода](/visualstudio/ide/code-snippets).  
  
## <a name="finally-block"></a>Блок finally  
 Если у вас есть один или несколько операторов, которые необходимо выполнить перед выходом из `Try` структуру, используйте `Finally` блока. Управление передается `Finally` блокировать только перед передачей из `Try…Catch` структуры. Это верно, даже если исключение возникает внутри `Try` структуры.  
  
 Объект `Finally` блок полезен для выполнить код, который необходимо выполнить, даже если существует одно исключение. Управление передается `Finally` блока независимо от того, как `Try...Catch` блокировать завершает работу.  
  
 Код в `Finally` блок даже при обнаружении в коде `Return` инструкции в `Try` или `Catch` блока. Элемент управления не передает из `Try` или `Catch` в соответствующий блок `Finally` блока в следующих случаях:  
  
-   [Оператор End](../../../visual-basic/language-reference/statements/end-statement.md) встречается в `Try` или `Catch` блока.  
  
-   Объект <xref:System.StackOverflowException> вызывается в `Try` или `Catch` блока.  
  
 Не допускается Явная передача выполнения в `Finally` блока. Передача выполнения из `Finally` недопустимый блок, за исключением случая возникновения исключения.  
  
 Если `Try` инструкция не содержит хотя бы один `Catch` блок, он должен содержать `Finally` блока.  
  
> [!TIP]
>  Если не нужно перехватывать определенные исключения `Using` похожа на инструкцию `Try…Finally` блока и гарантирует освобождение ресурсов, независимо от способа выхода из блока. Это верно даже при возникновении необработанного исключения. Дополнительные сведения см. в разделе [Оператор using](../../../visual-basic/language-reference/statements/using-statement.md).  
  
## <a name="exception-argument"></a>Исключение аргумента  
 `Catch` Блок `exception` аргумент является экземпляром класса <xref:System.Exception> класс или класс, производный от `Exception` класса. `Exception` Ошибки, возникшей в соответствующий экземпляр класса `Try` блока.  
  
 Свойства `Exception` объекта определить причину и место возникновения исключения. Например <xref:System.Exception.StackTrace%2A> списки свойств вызванных методов, которые приводят к исключению, помогая обнаружить, где произошла ошибка в коде. <xref:System.Exception.Message%2A>Возвращает сообщение, описывающее исключение. <xref:System.Exception.HelpLink%2A>Возвращает ссылку на связанный файл справки. <xref:System.Exception.InnerException%2A>Возвращает `Exception` возвращает объект, который вызвал текущее исключение, или его `Nothing` при наличии не оригинал `Exception`.  
  
## <a name="considerations-when-using-a-trycatch-statement"></a>Рекомендации по использованию оператора Try... Оператор catch  
 Используйте `Try…Catch` инструкции только для сигнализации вхождения программы необычных или непредвиденных событий. Для этого существуют следующие причины:  
  
-   Перехват исключений во время выполнения создает дополнительную нагрузку и может работать медленнее, чем предварительно проверки, чтобы избежать исключений.  
  
-   Если `Catch` блок не обрабатывается правильно, исключение может быть некорректно отображается для пользователей.  
  
-   Обработка исключений более осложняет программы.  
  
 Вы не всегда требуется `Try…Catch` инструкции для проверки условия, которое случается. В следующем примере проверяется, существует ли файл, прежде чем пытаться открыть его. Это снижает потребность в перехват исключения, созданного <xref:System.IO.File.OpenText%2A> метод.  
  
 [!code-vb[VbVbalrStatements#94](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_1.vb)]  
  
 Убедитесь, что код в `Catch` блоки должным образом сообщить исключения для пользователей, через поточно ориентированного ведения журнала или соответствующие сообщения. В противном случае может оставаться неизвестные исключения.  
  
## <a name="async-methods"></a>Асинхронные методы  
 Если пометить метод [Async](../../../visual-basic/language-reference/modifiers/async.md) модификатор, можно использовать [Await](../../../visual-basic/language-reference/operators/await-operator.md) в этом методе. Инструкция с `Await` оператор приостанавливает выполнение метода до завершения выполнения ожидающей задачи. Задача представляет выполняющуюся работу. Если задачи, связанные с `Await` оператор завершает выполнение возобновляется в том же методе. Дополнительные сведения см. в разделе [поток управления в асинхронных программах](../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md).  
  
 Задачи, возвращаемой функцией асинхронный метод может оказаться в состоянии faulted, указывающее на то, что она завершена из-за необработанного исключения. Задача также может завершиться в отмененном состоянии, что приводит к `OperationCanceledException` возникшего исключения за пределы выражения await. Для перехвата любого типа исключения, поместите `Await` выражения, связанный с задачей в `Try` блокировку и перехватывайте это исключение в `Catch` блока. Пример приведен далее в этом разделе.  
  
 Задача может быть в состоянии сбоя, так как несколько исключений несут ответственность за его сброса. Например, задача может быть результатом вызова метода <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>. Если вы ожидаете такую задачу, порожденное исключение имеет только одно из исключений и невозможно предсказать, какое исключение будет перехвачено. Пример приведен далее в этом разделе.  
  
 `Await` Выражение не может быть внутри `Catch` блока или `Finally` блока.  
  
## <a name="iterators"></a>Итераторы  
 Функции итератора или `Get` доступа выполняет настраиваемую итерацию по коллекции. Итератор использует [Yield](../../../visual-basic/language-reference/statements/yield-statement.md) инструкции для возврата всех элементов коллекции по одному за раз. Вызов функции итератора с помощью [For Each... Следующий оператор](../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
 Объект `Yield` инструкции могут находиться внутри `Try` блока. Объект `Try` блока, содержащего `Yield` инструкция может иметь `Catch` блокируется и может иметь `Finally` блока. В разделе «Попробуйте блоков в Visual Basic» [итераторы](../../programming-guide/concepts/iterators.md) в качестве примера.  
  
 Объект `Yield` оператор не может находиться внутри `Catch` блока или `Finally` блока.  
  
 Если `For Each` текст (за пределами функции итератора) вызывает исключение, `Catch` блок в функции итератора не выполняется, но `Finally` выполняется блок в функции итератора. Объект `Catch` блоке внутри функции итератора перехватывает только исключения, которые возникают внутри функции итератора.  
  
## <a name="partial-trust-situations"></a>Ситуациях частичного доверия  
 В ситуациях с частичным доверием, например приложения, размещенного в общей сетевой папке `Try...Catch...Finally` не перехватывает исключения безопасности, происходящие до вызова метода, который содержит вызов. Приведенный ниже, когда вы устанавливаете на общую папку сервера и выполнения оттуда, создающий ошибку «System.Security.SecurityException: не удалось запросить.» Дополнительные сведения об исключениях системы безопасности см. в разделе <xref:System.Security.SecurityException> класса.  
  
 [!code-vb[VbVbalrStatements#85](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_2.vb)]  
  
 В такой ситуации частичного доверия необходимо поместить `Process.Start` инструкции в отдельном `Sub`. Первый вызов `Sub` завершится ошибкой. Это позволяет `Try...Catch` перехватить перед `Sub` , содержащий `Process.Start` запускается и создается исключение безопасности.  
  
## <a name="example"></a>Пример  
 Следующий пример иллюстрирует структуру `Try...Catch...Finally` инструкции.  
  
 [!code-vb[VbVbalrStatements#86](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_3.vb)]  
  
## <a name="example"></a>Пример  
 В следующем примере `CreateException` вызывает исключение `NullReferenceException`. Код, который создает исключение, не находится в `Try` блока. Таким образом `CreateException` метод не обрабатывает исключение. `RunSample` Метод обработки исключения, так как вызов `CreateException` метод находится в `Try` блока.  
  
 В примере содержит `Catch` инструкции для различных типов исключений, начиная от наиболее конкретных к наиболее общим.  
  
 [!code-vb[VbVbalrStatements#91](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_4.vb)]  
  
## <a name="example"></a>Пример  
 В следующем примере показано, как использовать `Catch When` инструкции для фильтрации по условному выражению. Если условное выражение, результатом которого является `True`, код в `Catch` блок.  
  
 [!code-vb[VbVbalrStatements#92](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_5.vb)]  
  
## <a name="example"></a>Пример  
 В следующем примере есть `Try…Catch` инструкции, содержащейся в `Try` блока. Внутренний `Catch` блок вызывает исключение, имеющее его `InnerException` свойством, имеющим значение исходное исключение. Внешний `Catch` блок сообщает собственное исключение и внутреннее исключение.  
  
 [!code-vb[VbVbalrStatements#93](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_6.vb)]  
  
## <a name="example"></a>Пример  
 В следующем примере демонстрируется обработка исключений для асинхронных методов. Для перехвата исключения, который применяется для асинхронной задачи, `Await` выражение находится в `Try` блок вызывающего объекта, а исключение перехватывается в `Catch` блока.  
  
 Раскомментируйте строку `Throw New Exception` в этом примере для демонстрации обработки исключений. Исключение перехватывается в `Catch` блокировать задачи `IsFaulted` свойству `True`и эта задача `Exception.InnerException` свойству исключения.  
  
 Раскомментируйте строку `Throw New OperationCancelledException`, чтобы показать, что происходит при отмене асинхронного процесса. Исключение перехватывается в `Catch` блока и эта задача `IsCanceled` свойству `True`. Однако в некоторых условиях, которые неприменимы в данном примере `IsFaulted` равно `True` и `IsCanceled` имеет значение `False`.  
  
 [!code-vb[csAsyncExceptions#1](../../../csharp/language-reference/keywords/codesnippet/VisualBasic/try-catch-finally-statement_7.vb)]  
  
## <a name="example"></a>Пример  
 В следующем примере демонстрируется обработка исключений, когда несколько задач могут привести к нескольким исключениям. `Try` Блок содержит `Await` выражение для задачи, <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> возвращается. Задача завершается после завершения трех задач, к которому <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> применяется являются полными.  
  
 Каждая из трех задач вызывает исключение. `Catch` Блок итерацию по исключениям, которые находятся в `Exception.InnerExceptions` свойство задачи, `Task.WhenAll` возвращается.  
  
 [!code-vb[csAsyncExceptions#3](../../../csharp/language-reference/keywords/codesnippet/VisualBasic/try-catch-finally-statement_8.vb)]  
  
## <a name="see-also"></a>См. также  
 <xref:Microsoft.VisualBasic.Information.Err%2A>  
 <xref:System.Exception>  
 [Оператор Exit](../../../visual-basic/language-reference/statements/exit-statement.md)  
 [Оператор On Error](../../../visual-basic/language-reference/statements/on-error-statement.md)  
 [Рекомендации по использованию фрагментов кода](/visualstudio/ide/best-practices-for-using-code-snippets)  
 [Обработка исключений](../../../standard/parallel-programming/exception-handling-task-parallel-library.md)  
 [Оператор Throw](../../../visual-basic/language-reference/statements/throw-statement.md)
