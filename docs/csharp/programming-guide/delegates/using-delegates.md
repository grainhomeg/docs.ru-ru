---
title: "Использование делегатов (Руководство по программированию на C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "делегаты [C#], использование"
ms.assetid: 99a2fc27-a32e-4a34-921c-e65497520eec
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# Использование делегатов (Руководство по программированию на C#)
[Делегат](../../../csharp/language-reference/keywords/delegate.md) — это тип, который безопасно инкапсулирует метод, схожий с указателем функции в C и C\+\+.  В отличие от указателей функций в C делегаты объектно\-ориентированы, типобезопасны и безопасны.  Тип делегата задается его именем.  В следующем примере объявляется делегат с именем `Del`, который может инкапсулировать метод, использующий в качестве аргумента значение [string](../../../csharp/language-reference/keywords/string.md) и возвращающий значение [void](../../../csharp/language-reference/keywords/void.md).  
  
 [!code-cs[csProgGuideDelegates#21](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#21)]  
  
 Объект делегата обычно создается указанием имени метода, для которого делегат будет служить оболочкой, или с помощью [анонимного метода](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md).  После создания экземпляра делегата вызов метода, выполненный в делегате передается делегатом в этот метод.  Параметры, передаваемые делегату вызывающим объектом, передаются в метод, а возвращаемое методом значение \(при его наличии\) возвращается делегатом в вызывающий объект.  Эта процедура называется вызовом делегата.  Делегат, для которого создан экземпляр, можно вызвать, как если бы это был метод, для которого создается оболочка.  Например:  
  
 [!code-cs[csProgGuideDelegates#22](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#22)]  
  
 [!code-cs[csProgGuideDelegates#23](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#23)]  
  
 Типы делегатов являются производными от класса <xref:System.Delegate> в платформа.NET Framework.  Типы делегатов являются [запечатанными](../../../csharp/language-reference/keywords/sealed.md) — от них нельзя наследовать, а от <xref:System.Delegate> нельзя создавать производные пользовательские классы.  Поскольку созданный экземпляр делегата является объектом, его можно передавать как параметр или назначать свойству.  Это позволяет методу принимать делегат в качестве параметра и вызывать делегат в дальнейшем.  Эта процедура называется асинхронным обратным вызовом и обычно используется для уведомления вызывающего объекта о завершении длительной операции.  Когда делегат используется таким образом, коду, использующему делегат, не требуются сведения о реализации используемого метода.  Данные функциональные возможности аналогичны возможностям, предоставляемым интерфейсами инкапсуляции.  
  
 Обратный вызов также часто используется для задания настраиваемого метода сравнения и передачи этого делегата в метод сортировки.  Это позволяет сделать коду вызывающего объекта частью алгоритма сортировки.  В следующем примере метод использует тип `Del` тип в качестве параметра.  
  
 [!code-cs[csProgGuideDelegates#24](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#24)]  
  
 Затем в данный метод можно передать созданный ранее делегат:  
  
 [!code-cs[csProgGuideDelegates#25](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#25)]  
  
 и получить следующие выходные данные в окне консоли:  
  
 `The number is: 3`  
  
 При использовании делегата в качестве абстракции методу `MethodWithCallback` не нужно выполнять непосредственный вызов консоли, то есть его можно создавать без учета консоли.  Метод `MethodWithCallback` просто подготавливает строку и передает ее в другой метод.  Это очень удобно, так как делегируемый метод может использовать любое количество параметров.  
  
 Если делегат создан в качестве оболочки для метода экземпляра, этот делегат ссылается и на экземпляр, и на метод.  Делегат не имеет сведений о типе экземпляра, кроме полученных из метода, для которого он является оболочкой, поэтому делегат может ссылаться на любой тип объекта, если для этого объекта есть метод, соответствующий сигнатуре делегата.  Если делегат создан в качестве оболочки для статического метода, он ссылается только на метод.  Рассмотрим следующее объявление:  
  
 [!code-cs[csProgGuideDelegates#26](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#26)]  
  
 Вместе с рассмотренным ранее статическим методом `DelegateMethod` есть три метода, для которых можно создать оболочку с помощью экземпляра `Del`.  
  
 При вызове делегат может вызывать сразу несколько методов.  Это называется многоадресностью.  Чтобы добавить в список методов делегата \(список вызова\) дополнительный метод, необходимо просто добавить два делегата с помощью оператора сложения или назначения сложения \("\+" или "\+\="\).  Например:  
  
 [!code-cs[csProgGuideDelegates#27](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#27)]  
  
 На данном этапе список вызова делегата `allMethodsDelegate` содержит три метода — `Method1`, `Method2` и `DelegateMethod`.  Три исходных делегата `d1`, `d2` и `d3` остаются без изменений.  При вызове `allMethodsDelegate` все три метода вызываются по порядку.  Если делегат использует параметры, передаваемые по ссылке, эта ссылка передается после каждого из трех методов, а все изменения одного из методов становятся видны в следующем методе.  Если любой из методов вызывает неперехваченное исключение, это исключение передается в вызывающий делегат объект, а последующие методы в списке вызова не вызываются.  Если делегат имеет возвращаемое значение и \(или\) выходные параметры, он возвращает возвращаемое значение и параметры последнего вызванного метода.  Чтобы удалить метод из списка вызова, используйте оператор decrement или назначения decrement \("\-" или «\-\=»\).  Например:  
  
 [!code-cs[csProgGuideDelegates#28](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#28)]  
  
 Поскольку типы делегата являются производными от `System.Delegate`, в делегате можно вызывать методы и свойства, определенные этим классом.  Например, чтобы определить число методов в списке вызова делегата, можно использовать код:  
  
 [!code-cs[csProgGuideDelegates#29](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#29)]  
  
 Делегаты, в списке вызова которых находятся несколько методов, является производным от <xref:System.MulticastDelegate>, являющегося подклассом класса `System.Delegate`.  Приведенный выше код работает в любом из случаев, так как оба класса поддерживают `GetInvocationList`.  
  
 Групповые делегаты часто используются при обработке событий.  Объекты источников событий отправляют уведомления объектам получателей, зарегистрированным для получения данного события.  Чтобы зарегистрироваться для получения события, объект получателя создает метод, предназначенный для обработки этого события, затем создает делегат для этого метода и передает его в источник события.  Когда происходит событие, источник вызывает делегат.  После этого делегат вызывает в объекте получателя обработки события, предоставив ему данные события.  Тип делегата для данного события задается источником события.  Дополнительные сведения см. в разделе [События](../../../csharp/programming-guide/events/index.md).  
  
 Назначение сравнения делегатов двух различных типов во время компиляции вызовет ошибку компиляции.  Если экземпляры делегата статически относятся к типу `System.Delegate`, сравнение допустимо, но во время выполнения будет возвращено значение false.  Например:  
  
 [!code-cs[csProgGuideDelegates#30](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#30)]  
  
## См. также  
 [Руководство по программированию на C\#](../../../csharp/programming-guide/index.md)   
 [Делегаты](../../../csharp/programming-guide/delegates/index.md)   
 [Использование вариативности в делегатах](../Topic/Using%20Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)   
 [Вариативность в делегатах](../Topic/Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)   
 [Использование вариативности в универсальных методах\-делегатах Func и Action](../Topic/Using%20Variance%20for%20Func%20and%20Action%20Generic%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)   
 [События](../../../csharp/programming-guide/events/index.md)