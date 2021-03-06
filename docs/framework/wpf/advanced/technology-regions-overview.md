---
title: "Общие сведения об областях применения технологий"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- window regions [WPF]
- Win32 code [WPF], WPF interoperation
- Win32 code [WPF], airspace
- airspace [WPF]
- interoperability [WPF], airspace
- Win32 code [WPF], window regions
ms.assetid: b7cc350f-b9e2-48b1-be14-60f3d853222e
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 142973793fd002925bbe2b4b09ce8e6d34553031
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="technology-regions-overview"></a>Общие сведения об областях применения технологий
Если в приложении используются несколько технологий представления, такие как WPF, Win32 или DirectX, то они должны совместно использовать области отрисовки в общем окне верхнего уровня. В этом разделе описываются проблемы, которые могут повлиять на представление и выходные данные приложения взаимодействия с WPF.  
  
## <a name="regions"></a>Области  
 В окне верхнего уровня можно представить, что каждый HWND, который представляет собой одну из технологий приложения взаимодействия, имеет собственную область (также называемую "свободное пространство"). Каждый пиксель в окне принадлежит только одному дескриптору HWND, который определяет область этого HWND. (Строго говоря, существует более одной области [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], если имеется более одного HWND [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], но для целей этого обсуждения можно предположить, что есть только один). Область подразумевает, что все слои или другие окна, которые пытаются отобразиться поверх этого пикселя во время существования приложения, должны быть частью одной и той же технологии уровня отрисовки. Попытка отобразить пиксели [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] поверх [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] приводит к нежелательным результатам и в максимально возможной степени запрещается через взаимодействие [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)].  
  
### <a name="region-examples"></a>Примеры областей  
 На следующем рисунке показано приложение, в котором одновременно используются [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] и [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Каждая технология использует отдельный, неперекрывающийся набор пикселей, и проблемы с областями отсутствуют.  
  
 ![Окно, которое не имеет проблем со свободным пространством](../../../../docs/framework/wpf/advanced/media/migrationinteroparchitectarticle01.png "MigrationInteropArchitectArticle01")  
  
 Предположим, что это приложение использует положение указателя мыши для создания анимации, которая пытается выполнить отрисовку поверх любой из этих трех областей. Независимо от того, какая технология отвечает за анимацию, эта технология нарушила бы область двух других. На рисунке показана попытка отрисовать круг WPF поверх области Win32.  
  
 ![Схема взаимодействия](../../../../docs/framework/wpf/advanced/media/migrationinteroparchitectarticle02.png "MigrationInteropArchitectArticle02")  
  
 Другое нарушение — это попытка использовать прозрачность/альфа-смешение между различными технологиями.  На следующей иллюстрации окно [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] нарушает области [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] и [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)]. Так как пиксели в этом окне [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] являются полупрозрачными, они должны принадлежать и [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)], и [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], что невозможно.  Так что это еще одно нарушение, и его нельзя построить.  
  
 ![Схема взаимодействия](../../../../docs/framework/wpf/advanced/media/migrationinteroparchitectarticle03.png "MigrationInteropArchitectArticle03")  
  
 В предыдущих трех примерах использовались прямоугольные области, но возможны разные формы.  Например, в области может быть отверстие. На следующем рисунке показана область [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] с прямоугольным отверстием. Это размер областей [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] и [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] вместе.  
  
 ![Схема взаимодействия](../../../../docs/framework/wpf/advanced/media/migrationinteroparchitectarticle04.png "MigrationInteropArchitectArticle04")  
  
 Области также могут быть полностью непрямоугольными или иметь любую форму, описываемую [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] HRGN (область).  
  
 ![Схема взаимодействия](../../../../docs/framework/wpf/advanced/media/migrationinteroparchitectarticle05.png "MigrationInteropArchitectArticle05")  
  
## <a name="transparency-and-top-level-windows"></a>Прозрачность и окна верхнего уровня  
 Диспетчер окон Windows в действительности обрабатывает только HWND [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]. Таким образом каждый [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Window> является HWND. <xref:System.Windows.Window> HWND должен подчиняться правилам общие для любого HWND. Внутри этого HWND код [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] может выполнять любую поддержку [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]. Но для взаимодействия с другими HWND на рабочем столе [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] должен соответствовать правилам обработки и отрисовки [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] поддерживает непрямоугольные окна с помощью [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] — HRGN для непрямоугольных окон, и многослойные окна для альфа-смешения на уровне отдельных пикселей.  
  
 Постоянные альфа- и цветовые ключи не поддерживаются.  Возможности многослойных окон [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] зависят от платформы.  
  
 Многослойные окна позволяют сделать все окно прозрачным (полупрозрачным), указав альфа-значение, которое применяется к каждому пикселю в окне.  ([!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] фактически поддерживает альфа-смешение на уровне отдельных пикселей, но это очень сложно использовать в практических программах, потому что в этом режиме нужно рисовать все дочерние HWND самостоятельно, включая диалоговые окна и выпадающие списки).  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] поддерживает HRGN. Тем не менее для этой функциональности нет управляемых [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]. Можно воспользоваться платформой вызова неуправляемого кода и <xref:System.Windows.Interop.HwndSource> для вызова соответствующего [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]. Дополнительную информацию см. в разделе [Вызов встроенных функций из управляемого кода](/cpp/dotnet/calling-native-functions-from-managed-code).  
  
 Многослойные окна [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] имеют разные функциональные возможности в различных операционных системах. Это связано с тем, что [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] использует [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] для отрисовки, а многослойные окна были в первую очередь предназначены для отрисовки [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)], а не [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)].  
  
-   [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] поддерживает аппаратное ускорение многослойных окон в [!INCLUDE[TLA#tla_longhorn](../../../../includes/tlasharptla-longhorn-md.md)] и более поздних версиях. Для многослойных окон с аппаратным ускорением в [!INCLUDE[TLA2#tla_winxp](../../../../includes/tla2sharptla-winxp-md.md)] требуется поддержка [!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)], поэтому их возможности будут зависеть от версии [!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)] на данном компьютере.  
  
-   [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] не поддерживает цветовые ключи прозрачности, так как [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] не может гарантировать отрисовку необходимого цвета, особенно при использовании аппаратного ускорения.  
  
-   Если приложение работает в [!INCLUDE[TLA2#tla_winxp](../../../../includes/tla2sharptla-winxp-md.md)], многослойные окна поверх поверхностей [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] мерцают при отрисовке приложения [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)].  (Фактическая последовательность отрисовки заключается в том, что [!INCLUDE[TLA#tla_gdi](../../../../includes/tlasharptla-gdi-md.md)] скрывает многослойное окно, выполняется рисование [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)], а затем возвращает [!INCLUDE[TLA#tla_gdi](../../../../includes/tlasharptla-gdi-md.md)] многослойное окно).  Это ограничение накладывается и на многослойные окна вне [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
## <a name="see-also"></a>См. также  
 [Взаимодействие WPF и Win32](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)  
 [Пошаговое руководство. Размещение часов WPF в Win32](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-clock-in-win32.md)  
 [Размещение содержимого Win32 в WPF](../../../../docs/framework/wpf/advanced/hosting-win32-content-in-wpf.md)
