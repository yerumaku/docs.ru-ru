---
title: "Функциональное сборка (LINQ to XML) (Visual Basic)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: feac4273-39ab-43ae-bab7-4059c807a785
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: d5c68fb71fd59d08574cee9eec933cee25e504d9
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="functional-construction-linq-to-xml-visual-basic"></a>Функциональное сборка (LINQ to XML) (Visual Basic)
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] предоставляет эффективный способ создания XML-элементов, который называется *функциональным построением*. Функциональное построение — это возможность создать XML-дерево одной инструкцией.  
  
 Существует несколько основных функций интерфейса программирования [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], обеспечивающих функциональное построение.  
  
-   Конструктор <xref:System.Xml.Linq.XElement> принимает различные типы аргументов для содержимого. Например, можно передать еще один объект <xref:System.Xml.Linq.XElement>, который станет дочерним элементом. Можно передать объект <xref:System.Xml.Linq.XAttribute>, который станет атрибутом элемента. Можно также передать любой другой тип объекта, который будет преобразован в строку и станет текстовым содержимым элемента.  
  
-   Конструктор <xref:System.Xml.Linq.XElement> принимает массив `params` типа <xref:System.Object>, так что этому конструктору можно передать любое количество объектов. Это позволяет создавать элементы со сложным содержимым.  
  
-   Если объект реализует интерфейс <xref:System.Collections.Generic.IEnumerable%601>, коллекция в этом объекте перечисляется и добавляются все элементы коллекции. Если коллекция содержит объекты <xref:System.Xml.Linq.XElement> или <xref:System.Xml.Linq.XAttribute>, каждый ее элемент добавляется отдельно. Это важно, так как позволяет передавать результаты запроса [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] конструктору.  
  
 Ниже представлен пример такого кода.  
  
 Эти функции позволяют создавать код с помощью литералов XML для создания XML-дерева, а также написать код, использующий результаты [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] запросов при создании XML-дерева:  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element>1</Element>  
        <Element>2</Element>  
        <Element>3</Element>  
        <Element>4</Element>  
        <Element>5</Element>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child>1</Child>  
        <Child>2</Child>  
        <%= From el In srcTree.Elements() _  
            Where CInt(el) > 2 _  
            Select el %>  
    </Root>  
Console.WriteLine(xmlTree)  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Element>3</Element>  
  <Element>4</Element>  
  <Element>5</Element>  
</Root>  
```  
  
## <a name="see-also"></a>См. также  
 [Создание деревьев XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
