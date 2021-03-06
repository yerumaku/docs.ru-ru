---
title: "Не удается обратиться к члену экземпляра класса из совместно используемого метода или совместно используемого инициализатора без явного указания экземпляра этого класса"
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30369
- bc30369
helpviewer_keywords:
- Shared
- BC30369
ms.assetid: 39d9466b-c1f3-4406-91a5-3d6c52d23a3d
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 6a15d36c0b3a4d6b1657d583de0dc61621da960d
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="cannot-refer-to-an-instance-member-of-a-class-from-within-a-shared-method-or-shared-member-initializer-without-an-explicit-instance-of-the-class"></a>Не удается обратиться к члену экземпляра класса из совместно используемого метода или совместно используемого инициализатора без явного указания экземпляра этого класса
Вы попытались ссылается на член, не являющийся общим класса из общей процедуры. Ниже приведен пример такой ситуации.  
  
```  
Class sample  
    Public x as Integer  
    Public Shared Sub setX()  
        x = 10  
    End Sub  
End Class  
```  
  
 В предыдущем примере оператор присваивания `x = 10` это сообщение об ошибке. Это так, как общая процедура пытается получить доступ к переменной экземпляра.  
  
 Переменная `x` является членом экземпляра, так как он не объявлен как [Shared](../../../visual-basic/language-reference/modifiers/shared.md). Каждый экземпляр класса `sample` содержит собственные переменные `x`. Когда один экземпляр задает или изменяет значение `x`, не влияет на значение `x` в других экземплярах.  
  
 Однако процедура `setX` — `Shared` среди всех экземпляров класса `sample`. Это означает, что он не связан с какой-либо экземпляр класса, но вместо этого работает независимо от отдельных экземпляров. Так как она не связана с конкретным экземпляром `setX` не может получить доступ к переменной экземпляра. Она должна работать только с `Shared` переменных. Когда `setX` задает или изменяет значение общей переменной, это новое значение становится доступным всем экземплярам класса.  
  
 **Идентификатор ошибки:** BC30369  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
1.  Решите, будет ли элемент общим для всех экземпляров класса, то сохраняются отдельно для каждого экземпляра.  
  
2.  Если требуется одна копия элемента для всех экземпляров, добавьте `Shared` ключевое слово в объявлении члена. Сохранить `Shared` ключевое слово в объявлении процедуры.  
  
3.  Если требуется, чтобы каждый экземпляр для отдельных копия элемента, не указывайте `Shared` для объявления члена. Удалить `Shared` ключевое слово из объявления процедуры.  
  
## <a name="see-also"></a>См. также  
 [Общие](../../../visual-basic/language-reference/modifiers/shared.md)
