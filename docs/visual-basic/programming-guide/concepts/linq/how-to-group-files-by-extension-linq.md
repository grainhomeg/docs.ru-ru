---
title: "Практическое руководство: группировка файлов по расширению (LINQ) (Visual Basic) | Документы Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 904dc6d7-7162-4655-a7f4-5785d669bc5a
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f78785b4da3ae3b362603eea34d81207ed48a657
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-group-files-by-extension-linq-visual-basic"></a>Практическое руководство: группировка файлов по расширению (LINQ) (Visual Basic)
В этом примере показано, как можно использовать LINQ для выполнения расширенной группировки и сортировки списков файлов или папок. Также показано, как на страницы выходные данные в окне консоли с помощью <xref:System.Linq.Enumerable.Skip%2A>и <xref:System.Linq.Enumerable.Take%2A>методы.</xref:System.Linq.Enumerable.Take%2A> </xref:System.Linq.Enumerable.Skip%2A>  
  
## <a name="example"></a>Пример  
 Следующий запрос демонстрирует Группировка содержимого указанном дереве каталогов по расширению имени файла.  
  
```vb  
Module GroupByExtension  
    Public Sub Main()  
  
        ' Root folder to query, along with all subfolders.  
        Dim startFolder As String = "C:\program files\Microsoft Visual Studio 9.0\VB\"  
  
        ' Used in WriteLine() to skip over startfolder in output lines.  
        Dim rootLength As Integer = startFolder.Length  
  
        'Take a snapshot of the folder contents  
        Dim dir As New System.IO.DirectoryInfo(startFolder)  
        Dim fileList = dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories)  
  
        ' Create the query.  
        Dim queryGroupByExt = From file In fileList _  
                          Group By file.Extension.ToLower() Into fileGroup = Group _  
                          Order By ToLower _  
                          Select fileGroup  
  
        ' Execute the query. By storing the result we can  
        ' page the display with good performance.  
        Dim groupByExtList = queryGroupByExt.ToList()  
  
        ' Display one group at a time. If the number of   
        ' entries is greater than the number of lines  
        ' in the console window, then page the output.  
        Dim trimLength = startFolder.Length  
        PageOutput(groupByExtList, trimLength)  
  
    End Sub  
  
    ' Pages console diplay for large query results. No more than one group per page.  
    ' This sub specifically works with group queries of FileInfo objects  
    ' but can be modified for any type.  
    Sub PageOutput(ByVal groupQuery, ByVal charsToSkip)  
  
        ' "3" = 1 line for extension key + 1 for "Press any key" + 1 for input cursor.  
        Dim numLines As Integer = Console.WindowHeight - 3  
        ' Flag to indicate whether there are more results to diplay  
        Dim goAgain As Boolean = True  
  
        For Each fg As IEnumerable(Of System.IO.FileInfo) In groupQuery  
            ' Start a new extension at the top of a page.  
            Dim currentLine As Integer = 0  
  
            Do While (currentLine < fg.Count())  
                Console.Clear()  
                Console.WriteLine(fg(0).Extension)  
  
                ' Get the next page of results  
                ' No more than one filename per page  
                Dim resultPage = From file In fg _  
                                Skip currentLine Take numLines  
  
                ' Execute the query. Trim the display output.  
                For Each line In resultPage  
                    Console.WriteLine(vbTab & line.FullName.Substring(charsToSkip))  
                Next  
  
                ' Advance the current position  
                currentLine = numLines + currentLine  
  
                ' Give the user a chance to break out of the loop  
                Console.WriteLine("Press any key for next page or the 'End' key to exit.")  
                Dim key As ConsoleKey = Console.ReadKey().Key  
                If key = ConsoleKey.End Then  
                    goAgain = False  
                    Exit For  
                End If  
            Loop  
        Next  
    End Sub  
End Module  
```  
  
 Выходные данные этой программы могут быть длинными в зависимости от сведений о локальной файловой системы и что `startFolder` имеет значение. Для просмотра всех результатов, в этом примере показано, как просматривать результаты постранично. Те же методы могут применяться для Windows и веб-приложений. Обратите внимание, что поскольку код страницы элементов в группе, требуется вложенный `For Each` цикла является обязательным. Также существует некоторая дополнительная логика для вычисления текущей позиции в списке и предоставления пользователю возможности остановить разбиение по страницам и выйти из программы. В данном конкретном случае запрос разбиения на страницы выполняется к кэшированным результатам из исходного запроса. В других контекстах, например LINQ to SQL подобное кэширование не требуется.  
  
## <a name="compiling-the-code"></a>Компиляция кода  
 Создайте проект, в платформе .NET Framework версии 3.5 или более поздней версии с ссылку на библиотеку System.Core.dll и `Imports` оператор для пространства имен System.Linq.  
  
## <a name="see-also"></a>См. также  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)   
 [LINQ и каталоги файлов (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)
