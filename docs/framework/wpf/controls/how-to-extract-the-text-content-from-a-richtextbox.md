---
title: "Практическое руководство. Извлечение текстового содержимого из элемента управления RichTextBox"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text content [WPF], extracting
- RichTextBox control [WPF], extracting text content
- content [WPF], extracting
- extracting text content [WPF]
ms.assetid: f13c093f-1a05-45b3-ac8f-c9ea5e4a11c5
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 36a34e8f5a96f8b45a6c830ec3c1edeea816bd3b
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-extract-the-text-content-from-a-richtextbox"></a>Практическое руководство. Извлечение текстового содержимого из элемента управления RichTextBox
В этом примере показано, как извлечь содержимое <xref:System.Windows.Controls.RichTextBox> как обычный текст.  
  
## <a name="example"></a>Пример  
 Следующие [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] код описывает именованного <xref:System.Windows.Controls.RichTextBox> управления с простым содержимым.  
  
 [!code-xaml[RichTextBoxSnippets#_RTB_XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxSnippets/CSharp/Window1.xaml#_rtb_xaml)]  
  
## <a name="example"></a>Пример  
 Следующий код реализует метод, который принимает <xref:System.Windows.Controls.RichTextBox> как аргумент и возвращает строку, представляющую текстовое содержимое <xref:System.Windows.Controls.RichTextBox>.  
  
 Метод создает новый <xref:System.Windows.Documents.TextRange> из содержимого <xref:System.Windows.Controls.RichTextBox>, с использованием <xref:System.Windows.Documents.FlowDocument.ContentStart%2A> и <xref:System.Windows.Documents.FlowDocument.ContentEnd%2A> для указания диапазона для извлечения содержимого.  <xref:System.Windows.Documents.FlowDocument.ContentStart%2A>и <xref:System.Windows.Documents.FlowDocument.ContentEnd%2A> свойства каждого возвращают <xref:System.Windows.Documents.TextPointer>и доступно в основном FlowDocument, представляющий содержимое <xref:System.Windows.Controls.RichTextBox>.  <xref:System.Windows.Documents.TextRange>предоставляет свойство Text, которое возвращает часть обычного текста <xref:System.Windows.Documents.TextRange> как строка.  
  
 [!code-csharp[RichTextBoxSnippets#_RTB_StringFrom](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxSnippets/CSharp/Window1.xaml.cs#_rtb_stringfrom)]
 [!code-vb[RichTextBoxSnippets#_RTB_StringFrom](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxSnippets/visualbasic/window1.xaml.vb#_rtb_stringfrom)]  
  
## <a name="see-also"></a>См. также  
 [Общие сведения о RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)  
 [Общие сведения о TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)
