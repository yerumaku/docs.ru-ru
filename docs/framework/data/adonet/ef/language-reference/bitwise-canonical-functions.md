---
title: "Битовые канонические функции"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 993868ca-16e3-47b6-9915-c29cd63b0a21
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 1d703b2467d508324f3eb39b822c239484ac1c6e
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="bitwise-canonical-functions"></a>Битовые канонические функции
Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] включает битовые канонические функции.  
  
## <a name="remarks"></a>Примечания  
 В следующей таблице приведены другие битовые функции [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. Эти функции возвращают `Null` Если `Null` ввода данных пользователем. Тип возвращаемого значения функций совпадает с типами аргументов. Аргументы должны относиться к одному и тому же типу, если функция принимает более одного аргумента. Для выполнения битовых операций с различными типами необходимо выполнить явное приведение к одному и тому же типу.  
  
|Функция|Описание:|  
|--------------|-----------------|  
|`BitWiseAnd (` `value1` `,`  `value2` `)`|Возвращает результат битового логического умножения `value1` и `value2` того же типа, что имеют `value1` и `value2`.<br /><br /> **Аргументы**<br /><br /> Объект `Byte`, `Int16`, `Int32`, и `Int64`.<br /><br /> **Пример**<br /><br /> `-- The following example returns 1.`<br /><br /> `BitWiseAnd(1,3)`|  
|`BitWiseNot (` `value` `)`|Возвращает результат битового отрицания `value`.<br /><br /> **Аргументы**<br /><br /> Объект `Byte`, `Int16`, `Int32`, и `Int64`.<br /><br /> **Пример**<br /><br /> `-- The following example returns -4.`<br /><br /> `BitWiseNot(3)`|  
|`BitWiseOr (` `value1` `,`  `value2` `)`|Возвращает результат битового логического сложения `value1` и `value2` того же типа, что имеют `value1` и `value2`.<br /><br /> **Аргументы**<br /><br /> Объект `Byte`, `Int16`, `Int32` и `Int64`.<br /><br /> **Пример**<br /><br /> `-- The following example returns 3.`<br /><br /> `BitWiseOr(1,3)`|  
|`BitWiseXor (` `value1` `,`  `value2` `)`|Возвращает результат битового исключающего логического сложения `value1` и `value2` того же типа, что имеют `value1` и `value2`.<br /><br /> **Аргументы**<br /><br /> Объект `Byte`, `Int16`, `Int32` и `Int64`.<br /><br /> **Пример**<br /><br /> `-- The following example returns 2.`<br /><br /> `BitWiseXor (1,3)`|  
  
## <a name="see-also"></a>См. также  
 [Канонические функции](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)
