---
title: "volatile (Справочник по C#)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- volatile_CSharpKeyword
- volatile
dev_langs:
- CSharp
helpviewer_keywords:
- volatile keyword [C#]
ms.assetid: 78089bc7-7b38-4cfd-9e49-87ac036af009
caps.latest.revision: 29
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c8f9fba15991197be885a973435089098a57db87
ms.contentlocale: ru-ru
ms.lasthandoff: 09/25/2017

---
# <a name="volatile-c-reference"></a>volatile (Справочник по C#)
Ключевое слово `volatile` означает, что поле может изменить несколько потоков, выполняемых одновременно. Поля, объявленные `volatile`, не участвуют в оптимизации компилятора, предполагающей доступ для одного потока. Это гарантирует, что в любой момент времени в поле будет содержаться актуальное значение.  
  
 Обычно модификатор `volatile` используется для поля, к которому обращаются несколько потоков; при этом для сериализации доступа оператор [lock](../../../csharp/language-reference/keywords/lock-statement.md) не применяется.  
  
 Ключевое слово `volatile` может применяться к полям следующих типов:  
  
-   Ссылочные типы.  
  
-   Типы указателей (в небезопасном контексте). Несмотря на то, что сам указатель может быть изменяемым, объект, на который он указывает, должен быть постоянным. Другими словами, объявить указатель на изменяемый объект невозможно.  
  
-   Типы: sbyte, byte, short, ushort, int, uint, char, float и bool.  
  
-   Тип перечисления с одним из следующих базовых типов: byte, sbyte, short, ushort, int или uint.  
  
-   Параметры универсального типа называются ссылочными типами.  
  
-   <xref:System.IntPtr> и <xref:System.UIntPtr>.  
  
 Ключевое слово volatile можно применять только к полям класса или структуры. Локальные переменные не могут объявляться как `volatile`.  
  
## <a name="example"></a>Пример  
 В следующем примере показано, как объявить переменную поля открытого типа `volatile`.  
  
 [!code-cs[csrefKeywordsModifiers#24](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_1.cs)]  
  
## <a name="example"></a>Пример  
 Следующий пример демонстрирует создание вспомогательного или рабочего потока и его применение для выполнения обработки параллельно с обработкой основного потока. Дополнительные сведения о многопоточности см. в разделах [Потоки](../../../standard/threading/index.md) и [Потоки](http://msdn.microsoft.com/library/552f6c68-dbdb-4327-ae36-32cf9063d88c).  
  
 [!code-cs[csProgGuideThreading#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_2.cs)]  
  
## <a name="c-language-specification"></a>Спецификация языка C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Справочник по C#](../../../csharp/language-reference/index.md)   
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)   
 [Ключевые слова в C#](../../../csharp/language-reference/keywords/index.md)   
 [Модификаторы](../../../csharp/language-reference/keywords/modifiers.md)

