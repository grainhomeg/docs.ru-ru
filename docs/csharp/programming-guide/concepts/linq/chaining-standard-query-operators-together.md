---
title: "Связывание стандартных операторов запросов (C#) | Документы Майкрософт"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 66f2b0a9-2c23-4735-988e-bbc9dfb55c7b
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8e9da047fcc224176d028f8caef8b57bc134dc21
ms.lasthandoff: 03/13/2017


---
# <a name="chaining-standard-query-operators-together-c"></a>Связывание стандартных операторов запросов (C#)
Это последний раздел учебника [Объединение запросов в цепочки (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md).  
  
 Стандартные операторы запросов также можно объединять в цепочки. Например, можно вставить оператор <xref:System.Linq.Enumerable.Where%2A?displayProperty=fullName>, который также будет действовать как отложенный. Этот оператор не материализует промежуточные результаты.  
  
## <a name="example"></a>Пример  
 В этом примере метод <xref:System.Linq.Enumerable.Where%2A> вызывается до вызова метода `ConvertCollectionToUpperCase`. Метод <xref:System.Linq.Enumerable.Where%2A> действует практически так же, как отложенные методы, которые использовались в предыдущих примерах в этом учебнике, `ConvertCollectionToUpperCase` и `AppendString`.  
  
 Отличие заключается в том, что в этом случае метод <xref:System.Linq.Enumerable.Where%2A> просматривает свою исходную коллекцию, определяет, что первый элемент не передает предикат, а затем переходит к следующему элементу, который передает предикат. После этого метод выдает второй элемент.  
  
 Однако базовый принцип остался прежним: промежуточные коллекции материализуются только в случае необходимости.  
  
 При использовании выражений запросов они преобразуются в вызовы стандартных операторов запросов, а затем применяется тот же принцип.  
  
 Во всех примерах, приведенных в этом разделе, в которых запрашиваются документы Office Open XML, используется один и тот же принцип. Отложенное выполнение и отложенное вычисление - это основополагающие принципы, которые необходимо понимать, чтобы эффективно использовать LINQ (и LINQ to XML).  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source >{0}<", str);  
            yield return str.ToUpper();  
        }  
    }  
  
    public static IEnumerable<string>  
      AppendString(this IEnumerable<string> source, string stringToAppend)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("AppendString: source >{0}<", str);  
            yield return str + stringToAppend;  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        IEnumerable<string> q1 =  
            from s in stringArray.ConvertCollectionToUpperCase()  
            where s.CompareTo("D") >= 0  
            select s;  
  
        IEnumerable<string> q2 =  
            from s in q1.AppendString("!!!")  
            select s;  
  
        foreach (string str in q2)  
        {  
            Console.WriteLine("Main: str >{0}<", str);  
            Console.WriteLine();  
        }  
    }  
}  
```  
  
 В этом примере выводятся следующие данные:  
  
```  
ToUpper: source >abc<  
ToUpper: source >def<  
AppendString: source >DEF<  
Main: str >DEF!!!<  
  
ToUpper: source >ghi<  
AppendString: source >GHI<  
Main: str >GHI!!!<  
```  
  
## <a name="see-also"></a>См. также  
 [Учебник. Объединение запросов в цепочки (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md)