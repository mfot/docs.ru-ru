---
title: "Практическое руководство. Доступ к связанным объектам в строках DataGridView в Windows Forms"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- object binding [Windows Forms], accessing bound objects
- data grids [Windows Forms], accessing bound objects
- DataGridView control [Windows Forms], accessing objects bound to rows
ms.assetid: 0e05748f-4403-4eb8-8b2f-b098108181b5
caps.latest.revision: "21"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 66db5f6ff7b964162f77317f17a9e3a8d3ed22b2
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-access-objects-bound-to-windows-forms-datagridview-rows"></a>Практическое руководство. Доступ к связанным объектам в строках DataGridView в Windows Forms
Иногда полезно отображать таблицу данных, которые хранятся в коллекции бизнес-объектов. При привязке элемента управления <xref:System.Windows.Forms.DataGridView> к такого рода коллекции каждое открытое свойство отображается в собственном столбце, если только оно не помечено как недоступное для просмотра с помощью <xref:System.ComponentModel.BrowsableAttribute>. Например, коллекция объектов `Customer` будет содержать такие столбцы, как **Имя** и **Адрес**.  
  
 Если такие объекты содержат дополнительную информацию и код, к которым требуется доступ, можно использовать объекты строк. В примере кода ниже пользователи могут выбрать несколько строк и отправить счета каждому из соответствующих клиентов путем нажатия на кнопку.  
  
### <a name="to-access-row-bound-objects"></a>Получение доступа к объектам, связанным со строками  
  
-   Используйте свойство <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=nameWithType>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#10)]  
  
## <a name="example"></a>Пример  
 Полный пример кода включает в себя простую реализацию `Customer` и связывает <xref:System.Windows.Forms.DataGridView> со списком <xref:System.Collections.ArrayList>, содержащим несколько объектов `Customer`. Доступ обработчика событий <xref:System.Windows.Forms.Control.Click> элемента <xref:System.Windows.Forms.Button?displayProperty=nameWithType> к объектам `Customer` должен осуществляться через строки, так как коллекция клиентов недоступна вне обработчика событий <xref:System.Windows.Forms.Form.Load?displayProperty=nameWithType>.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#00)]  
  
## <a name="compiling-the-code"></a>Компиляция кода  
 Для этого примера требуются:  
  
-   ссылки на сборки System и System.Windows.Forms;  
  
 Информацию о выполнении сборки этого примера из командной строки для [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] или [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] можно найти в разделе [Построение из командной строки](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md) или [Построение из командной строки с помощью файла csc.exe](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md). Чтобы выполнить сборку этого примера в [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)], можно также вставить код в новый проект.  См. также [Практическое руководство. Компиляция и выполнение откомпилированного примера кода формы Windows Forms с помощью Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Forms.DataGridView>  
 <xref:System.Windows.Forms.DataGridViewRow>  
 <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=nameWithType>  
 [Отображение данных с помощью элемента управления DataGridView в Windows Forms](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)  
 [Практическое руководство. Связывание объектов с элементами управления DataGridView в Windows Forms](../../../../docs/framework/winforms/controls/how-to-bind-objects-to-windows-forms-datagridview-controls.md)
