---
title: "Безопасность и поля-массивы с общим доступом только для чтения"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [.NET Framework], public read-only array fields
ms.assetid: 3df28dee-2a9f-40ff-9852-bfdbe59c27f3
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: d86d054d3a5a4e10b8efcc3292f3a18ea37f9b87
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="security-and-public-read-only-array-fields"></a>Безопасность и поля-массивы с общим доступом только для чтения
Никогда не используйте поля только для чтения общих массивов из управляемых библиотек для определения поведения границы или безопасности приложений, так как открытые массива только для чтения можно изменять.  
  
## <a name="remarks"></a>Примечания  
 Некоторые классы .NET framework включают только для чтения открытых полей, содержащих параметры границы конкретной платформы.  Например <xref:System.IO.Path.InvalidPathChars> представляет собой массив, описывающий символы, которые не разрешены в строке пути к файлу.  Многие аналогичные поля, присутствуют в .NET Framework.  
  
 Значения открытых полей только для чтения, например <xref:System.IO.Path.InvalidPathChars> может изменяться функцией код или код, который использует ваш код домена приложения.  Не следует использовать только для чтения массив открытые поля следующим образом для определения поведения границы приложений.  В противном случае вредоносный код можно изменить определения границ и использовании кода вами непредвиденным образом.  
  
 В версии 2.0 и более поздней версии платформы .NET Framework следует использовать методы, возвращающие новый массив, вместо того чтобы использовать массивы с общим поля.  Например, вместо использования <xref:System.IO.Path.InvalidPathChars> поля, следует использовать <xref:System.IO.Path.GetInvalidPathChars%2A> метода.  
  
 Обратите внимание, что типы .NET Framework не используют открытые поля для внутреннего определения граничных типов.  Вместо этого в .NET Framework используются отдельные закрытые поля.  Изменение значений полей с общим доступом не влияет на поведение типов .NET Framework.  
  
## <a name="see-also"></a>См. также  
 [Правила написания безопасного кода](../../../docs/standard/security/secure-coding-guidelines.md)
