---
title: "Разрешение перегрузки функций (Entity SQL)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9c648054-3808-4a69-9d3e-98e6a4f9c5ca
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: cafbdd1a06ce506516fa985e9af147f55b4ea3d4
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="function-overload-resolution-entity-sql"></a>Разрешение перегрузки функций (Entity SQL)
В данном разделе описывается, каким образом разрешаются функции [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
 С одним именем можно определить более одной функции при условии, что эти функции имеют уникальные сигнатуры.  
  
 В этом случае для определения, на какие функции ссылается данное выражение, следует применить следующие критерии. Эти критерии применяются последовательно. Первый критерий, применимый только к одной функции, определяет разрешенную функцию.  
  
1.  **Параметр с номером**. Функция имеет то же число параметров, которое указано в выражении.  
  
2.  **Точное совпадение типа**. Тип каждого аргумента функции точно соответствует типу параметра или является литералом NULL.  
  
3.  **Совпадение подтипов**. Тип каждого аргумента функции точно соответствует подтипу типа параметра или аргумент является литералом NULL. В случае, если несколько функций отличаются только числом требуемых преобразований подтипа, разрешаемой является функция с наименьшим числом преобразований подтипа.  
  
4.  **Совпадение подтипов или повышение типа**. Тип каждого аргумента функции точно соответствует, является подтипом или может быть повышен до типа параметра или аргумент является литералом NULL. С другой стороны, в случае, если несколько функций отличаются только числом требуемых преобразований и повышений подтипа, то разрешаемой является функция с наименьшим числом преобразований и повышений подтипа.  
  
 Если ни один из этих критериев не позволяет выбрать единственную функцию, то выражение вызова функции неоднозначно.  
  
 Даже если с помощью этих правил можно извлечь единственную функцию, аргументы могут не соответствовать параметрам. В этом случае возникает ошибка.  
  
 Что касается определяемых пользователем функций, то приоритет имеет определение для встроенной функции запроса, даже если существует функция, определенная в модели, с сигнатурой, которая больше подходит для пользовательской функции.  
  
## <a name="see-also"></a>См. также  
 [Справочник по Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)  
 [Общие сведения об Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)  
 [Функции](../../../../../../docs/framework/data/adonet/ef/language-reference/functions-entity-sql.md)
