---
title: "Условные выражения. if... then...else (F#)"
description: "Дополнительные сведения о записи условные выражения на языке F # для выполнения различных ветвей кода."
keywords: "visual f#, f#, функциональное программирование"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 16e1871c-4d4d-4691-9ab2-bd2c6f65589a
ms.openlocfilehash: 3531a112eb53657d5e9102d5e5f3be988360b76e
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="conditional-expressions-ifthenelse"></a>Условные выражения.`if...then...else`

`if...then...else` Выражение выполняет различные ветви кода и имеет разные значения в зависимости от заданного логического выражения.


## <a name="syntax"></a>Синтаксис

```fsharp
if boolean-expression then expression1 [ else expression2 ]
```

## <a name="remarks"></a>Примечания
В предыдущем синтаксисе *expression1* выполняется, когда логическое выражение, результатом которого является `true`; в противном случае *expression2* запускает.

В отличие от других языков, `if...then...else` конструктор является выражением, а не оператором. Это означает, что она создает значение, которое является значением последнего выражения в ветвь, для которой выполняется. Типы значений, получаемых в каждой ветви должны совпадать. При наличии без явного указания `else` ветви, но его тип — `unit`. Таким образом Если тип `then` ветвь — любой тип, отличный от `unit`, должно быть `else` с тем же типом возврата ветви. При объединении `if...then...else` выражений, можно использовать ключевое слово `elif` вместо `else if`; они равны.

## <a name="example"></a>Пример
Следующий пример показывает, как использовать `if...then...else` выражение.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4501.fs)]

```
John
910 is less than 20
You are only 9 years old and already learning F#? Wow!
```

## <a name="see-also"></a>См. также
[Справочник по языку F#](index.md)

