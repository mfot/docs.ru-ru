---
title: /link (Visual Basic)
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- l compiler option [Visual Basic]
- EmbedInteropTypes
- embed interop types [COM Interop]
- -link compiler option [Visual Basic]
- /link compiler option [Visual Basic]
- link compiler option [Visual Basic]
- -l compiler option [Visual Basic]
- /l compiler option [Visual Basic]
ms.assetid: 1885f24a-86f5-486c-a064-9fb7e455ccec
caps.latest.revision: "27"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: effaeae48bdeb1dfd0f8cda31fedf2436e7deaca
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="link-visual-basic"></a>/link (Visual Basic)
Дает компилятору указание сделать всю информацию о типах COM из указанных сборок доступной компилируемому проекту.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
/link:fileList  
' -or-  
/l:fileList  
```  
  
## <a name="arguments"></a>Аргументы  
  
|Термин|Определение|  
|---|---|  
|`fileList`|Обязательный. Список всех имен файлов сборки, разделенных запятыми. Если имя файла содержит пробел, заключите его в кавычки.|  
  
## <a name="remarks"></a>Примечания  
 Параметр `/link` позволяет развернуть приложение, содержащее внедренные сведения о типе. После этого приложение может использовать типы из сборки среды выполнения, реализующей информацию о внедренных типах, без ссылки на эту сборку. Если опубликовано несколько версий сборки среды выполнения, приложение, содержащее сведения о внедренных типах, может работать с различными версиями без перекомпиляции. Пример см. в разделе [Пошаговое руководство. Внедрение данных о типах из управляемых сборок](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21).  
  
 Параметр `/link` особенно полезен при работе с COM-взаимодействием. COM-типы внедряются для того, чтобы приложению не требовалась основная сборка взаимодействия (PIA) на целевом компьютере. Параметр `/link` предписывает компилятору внедрить сведения о COM-типах из указанной сборки взаимодействия в полученный скомпилированный код. COM-тип определяется значением CLSID (GUID). Это позволяет запускать приложение на целевом компьютере, где установлены те же COM-типы с такими же значениями CLSID. В качестве примера можно привести приложения, автоматизирующие Microsoft Office. Поскольку в приложениях типа Office значение CLSID обычно не зависит от версии, ваше приложение сможет использовать COM-типы по ссылке до тех пора, пока на целевом компьютере установлена платформа .NET Framework 4 или более поздней версии, а приложение работает с методами, свойствами или событиями, включенными в эти COM-типы.  
  
 Параметр `/link` внедряет только интерфейсы, структуры и делегаты. Внедрение COM-классов не поддерживается.  
  
> [!NOTE]
>  Если в коде создается экземпляр внедренного COM-типа, его следует создавать, используя соответствующий интерфейс. При попытке создать экземпляр внедренного COM-типа с помощью компонентного класса возникнет ошибка.  
  
 Чтобы задать параметр `/link` в [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)], добавьте ссылку на сборку и задайте для свойства `Embed Interop Types` значение **true**. По умолчанию для свойства `Embed Interop Types` задается значение **false**.  
  
 Ссылаясь на COM-сборку (сборку A), которая, в свою очередь, ссылается на другую COM-сборку (сборку Б), необходимо также добавить ссылку на сборку Б, если выполняется любое из следующих условий:  
  
-   Тип из сборки A наследуется из типа или реализует интерфейс сборки Б.  
  
-   Вызывается поле, свойство, событие или метод, имеющий тип возвращаемого значения или тип параметра из сборки Б.  
  
 Используйте [/LIBPATH](../../../visual-basic/reference/command-line-compiler/libpath.md) для указания каталога, в котором находится один или несколько ссылок на сборки.  
  
 Как [/reference](../../../visual-basic/reference/command-line-compiler/reference.md) параметр компилятора `/link` компилятора использует файл ответов Vbc.rsp, который ссылается на часто используемые [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] сборки. Используйте [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md) параметр компилятора, если не хотите, чтобы компилятор использовал файл Vbc.rsp.  
  
 Краткой формой `/link` является `/l`.  
  
## <a name="generics-and-embedded-types"></a>Универсальные и внедренные типы  
 В следующих разделах описаны ограничения на использование универсальных типов в приложениях с внедренными типами взаимодействия.  
  
### <a name="generic-interfaces"></a>Универсальные интерфейсы  
 Использовать универсальные интерфейсы, внедренные из сборки взаимодействия, нельзя. Эти действия показаны в следующем примере.  
  
 [!code-vb[VbLinkCompiler#1](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_1.vb)]  
  
### <a name="types-that-have-generic-parameters"></a>Типы с универсальными параметрами  
 Типы с универсальным параметром, тип которого внедрен из сборки взаимодействия, нельзя использовать, если он относится к внешней сборке. Это ограничение не относится к интерфейсам. Например, рассмотрим интерфейс <xref:Microsoft.Office.Interop.Excel.Range>, который определен в сборке <xref:Microsoft.Office.Interop.Excel>. Если библиотека содержит внедренные типы взаимодействия из сборки <xref:Microsoft.Office.Interop.Excel> и предоставляет метод, возвращающий универсальный тип с параметром, типом которого является интерфейс <xref:Microsoft.Office.Interop.Excel.Range>, этот метод должен возвращать универсальный интерфейс, как показано в следующем примере кода.  
  
 [!code-vb[VbLinkCompiler#2](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_2.vb)]  
[!code-vb[VbLinkCompiler#3](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_3.vb)]  
[!code-vb[VbLinkCompiler#4](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_4.vb)]  
  
 В следующем примере клиентский код может вызывать метод, возвращающий универсальный интерфейс <xref:System.Collections.IList> без ошибок.  
  
 [!code-vb[VbLinkCompiler#5](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_5.vb)]  
  
## <a name="example"></a>Пример  
 Следующий код компилирует исходный файл `OfficeApp.vb` и ссылочные сборки из `COMData1.dll` и `COMData2.dll` и создает, таким образом, файл `OfficeApp.exe`.  
  
```vb  
vbc /link:COMData1.dll,COMData2.dll /out:OfficeApp.exe OfficeApp.vb  
```  
  
## <a name="see-also"></a>См. также  
 [Компилятор Visual Basic с интерфейсом командной строки](../../../visual-basic/reference/command-line-compiler/index.md)  
 [Пошаговое руководство. Внедрение данных о типах из управляемых сборок](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)  
 [/ Reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)  
 [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)  
 [/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md)  
 [Примеры командных строк компиляции](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [Знакомство с COM-взаимодействием](../../../visual-basic/programming-guide/com-interop/introduction-to-com-interop.md)
