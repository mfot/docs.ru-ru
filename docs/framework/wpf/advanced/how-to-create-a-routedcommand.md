---
title: "Практическое руководство. Создание маршрутизируемой команды RoutedCommand"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- RoutedCommand class [WPF], creating
ms.assetid: aaf6979f-69ab-406f-979f-5766daa85fa0
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 449b55d07aa0119ff23c8642ca83b0989f5b1d4b
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-create-a-routedcommand"></a>Практическое руководство. Создание маршрутизируемой команды RoutedCommand
В этом примере показано, как создать настраиваемый <xref:System.Windows.Input.RoutedCommand> и способ реализации пользовательской команды путем создания <xref:System.Windows.Input.ExecutedRoutedEventHandler> и <xref:System.Windows.Input.CanExecuteRoutedEventHandler> и присоединения их <xref:System.Windows.Input.CommandBinding>.  Дополнительные сведения о командах см. в разделе [Общие сведения о работе с командами](../../../../docs/framework/wpf/advanced/commanding-overview.md).  
  
## <a name="example"></a>Пример  
 Первым шагом при создании <xref:System.Windows.Input.RoutedCommand> является определение команды и создания его экземпляра.  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCommandDefinition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcommanddefinition)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCommandDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcommanddefinition)]  
  
 Чтобы использовать команду в приложении, необходимо создать обработчики событий, которые определяют, что делает команда  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewExecuted](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewexecuted)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewExecuted](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewexecuted)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCanExecute](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcanexecute)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCanExecute](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcanexecute)]  
  
 Далее, <xref:System.Windows.Input.CommandBinding> с обработчиками событий, который связывает команду. <xref:System.Windows.Input.CommandBinding> Создан для определенного объекта.  Этот объект определяет область <xref:System.Windows.Input.CommandBinding> в дереве элементов  
  
 [!code-xaml[CommandingOverviewSnippets#CommandingOverviewWindowCommandBindingXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewwindowcommandbindingxaml)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCustomCommandBindingCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcustomcommandbindingcodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCustomCommandBindingCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcustomcommandbindingcodebehind)]  
  
 Последним шагом является вызов команды.  Один из способов вызова команды является связывание ее с <xref:System.Windows.Input.ICommandSource>, такие как <xref:System.Windows.Controls.Button>.  
  
 [!code-xaml[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewcustomcommandsourcexaml)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcustomcommandsourcecodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcustomcommandsourcecodebehind)]  
  
 При нажатии кнопки <xref:System.Windows.Input.RoutedCommand.Execute%2A> метод в пользовательской <xref:System.Windows.Input.RoutedCommand> вызывается.  <xref:System.Windows.Input.RoutedCommand> Вызывает <xref:System.Windows.Input.CommandManager.PreviewExecuted> и <xref:System.Windows.Input.CommandManager.Executed> перенаправленные события.  Эти события проходят по дереву элементов, поиск <xref:System.Windows.Input.CommandBinding> для этой конкретной команды.  Если <xref:System.Windows.Input.CommandBinding> найден, <xref:System.Windows.Input.ExecutedRoutedEventHandler> связанных с <xref:System.Windows.Input.CommandBinding> вызывается.  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Input.RoutedCommand>  
 [Общие сведения о системе команд](../../../../docs/framework/wpf/advanced/commanding-overview.md)
