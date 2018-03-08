---
title: "int (справочник по C#)"
ms.date: 03/14/2017
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- int_CSharpKeyword
- int
helpviewer_keywords:
- int keyword [C#]
ms.assetid: 212447b4-5d2a-41aa-88ab-84fe710bdb52
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: e7acb8bb482ebf8f5c2b508e7cfd45b5b64aae3b
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="int-c-reference"></a>int (справочник по C#)

`int` обозначает целочисленный тип данных, в котором хранятся значения, размер и диапазон которых приведен в следующей таблице.  
  
|Тип|Диапазон|Размер|Тип платформы .NET Framework|Значение по умолчанию|  
|----------|-----------|----------|-------------------------|-------------------|  
|`int`|От -2 147 483 648 до 2 147 483 647|32-разрядное целое число со знаком|<xref:System.Int32?displayProperty=nameWithType>|0|  
  
## <a name="literals"></a>Литералы  
 
Переменную `int` можно объявить и инициализировать, назначив ей десятичный, шестнадцатеричный или (начиная с C# 7) двоичный литерал.  Если целочисленный литерал выходит за пределы диапазона `int` (то есть если он меньше <xref:System.Int32.MinValue?displayProperty=nameWithType> или больше <xref:System.Int32.MaxValue?displayProperty=nameWithType>), возникает ошибка компиляции. 

В следующем примере целые числа, равные 90 946 и представленные в виде десятичного, шестнадцатеричного и двоичного литерала, назначаются значениям `int`.  
  
[!code-csharp[int](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#Int)]  

> [!NOTE] 
> Для обозначения шестнадцатеричного литерала используйте префикс `0x` или `0X`, а для обозначения двоичного литерала — префикс `0b` или `0B`. У десятичных литералов префиксов нет. 

Начиная с C# 7, ваши возможности были добавлены для повышения удобства чтения. 
 - C# 7.0 допускает использование символа подчеркивания, `_`, в качестве разделителя цифр.
 - C# 7.2 допускает использовать символ подчеркивания, `_`, в качестве разделителя цифр для двоичных или шестнадцатеричных литералов, после префикса. Десятичный литерал не может начинаться с символа подчеркивания.

Ниже приведены некоторые примеры.

[!code-csharp[int](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#IntS)]  
 
 Целочисленные литералы могут содержать суффикс, обозначающий тип, несмотря на то, что для обозначения типа `int` суффикс не предусмотрен. Если целочисленный литерал не имеет суффикса, его типом будет первый из следующих типов, в котором может быть представлено его значение: 

1. `int`
2. [uint](../../../csharp/language-reference/keywords/uint.md)
3. [long](../../../csharp/language-reference/keywords/long.md)
4. [ulong](../../../csharp/language-reference/keywords/ulong.md) 
 
В этих примерах литерал 90946 имеет тип `int`.
  
## <a name="conversions"></a>Преобразования  
 Существует предопределенное неявное преобразование типа `int` в тип [long](../../../csharp/language-reference/keywords/long.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) или [decimal](../../../csharp/language-reference/keywords/decimal.md). Пример:  
  
```csharp  
// '123' is an int, so an implicit conversion takes place here:  
float f = 123;  
```  
  
 Существует предопределенное неявное преобразование типа [sbyte](../../../csharp/language-reference/keywords/sbyte.md), [byte](../../../csharp/language-reference/keywords/byte.md), [short](../../../csharp/language-reference/keywords/short.md), [ushort](../../../csharp/language-reference/keywords/ushort.md) или [char](../../../csharp/language-reference/keywords/char.md) в `int`. Например, следующий оператор назначения вызывает ошибку компиляции без приведения:  
  
```csharp  
long aLong = 22;  
int i1 = aLong;       // Error: no implicit conversion from long.  
int i2 = (int)aLong;  // OK: explicit conversion.  
```  
  
 Обратите внимание, что неявного преобразования типов с плавающей запятой в тип `int` не существует. Например, следующая инструкция приводит к ошибке компилятора, если не выполнить явное приведение типов:  
  
```csharp  
int x = 3.0;         // Error: no implicit conversion from double.  
int y = (int)3.0;    // OK: explicit conversion.  
```  
  
 Дополнительные сведения об арифметических выражениях, в которых одновременно используются переменные типов с плавающей запятой и целочисленных типов, см. в разделах [float](../../../csharp/language-reference/keywords/float.md) и [double](../../../csharp/language-reference/keywords/double.md).  
  
## <a name="c-language-specification"></a>Спецификация языка C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>См. также  
 <xref:System.Int32>  
 [Справочник по C#](../../../csharp/language-reference/index.md)  
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
 [Ключевые слова в C#](../../../csharp/language-reference/keywords/index.md)  
 [Таблица целых типов](../../../csharp/language-reference/keywords/integral-types-table.md)  
 [Таблица встроенных типов](../../../csharp/language-reference/keywords/built-in-types-table.md)  
 [Таблица неявных числовых преобразований](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)  
 [Таблица явных числовых преобразований](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
