---
title: "Сравнение строк без учета языка и региональных параметров | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "языковый и региональный параметр"
  - "операции со строками без учета языка и региональных параметров, сравнения"
  - "сравнение строк [платформа .NET Framework], независимо от языка и региональных параметров"
  - "String.Compare - метод"
  - "String.CompareTo - метод"
  - "строки [платформа .NET Framework], сравнение"
ms.assetid: abae50ef-32f7-4a50-a540-fd256fd1aed0
caps.latest.revision: 23
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 23
---
# Сравнение строк без учета языка и региональных параметров
По умолчанию метод <xref:System.String.Compare%2A?displayProperty=fullName> выполняет сравнение с учетом языка и региона и регистра символов.  Этот метод также содержит несколько перегрузок, которые предоставляют параметр `culture`, позволяющий задать используемый язык и региональные параметры, и параметр `comparisonType`, позволяющий указать используемые правила сравнения.  При вызове этих методов вместо перегрузки по умолчанию удаляется любая неопределенность в отношении правил, используемых при вызове конкретного метода, и четко определяется, учитываются ли при конкретном сравнении язык и региональные параметры.  
  
> [!NOTE]
>  Обе перегрузки метода <xref:System.String.CompareTo%2A?displayProperty=fullName> выполняют сравнение с учетом языка и региональных параметров и с учетом регистра; для сравнения без учета языка и региональных параметров этот метод использовать нельзя.  Для получения более понятного кода рекомендуется вместо этого метода использовать метод <xref:System.String.Compare%2A?displayProperty=fullName>.  
  
 Для операций с учетом языка и региональных параметров в качестве параметра `comparisonType` следует указать значение перечисления <xref:System.StringComparison?displayProperty=fullName> или <xref:System.StringComparison?displayProperty=fullName>.  Если требуется выполнить сравнение с учетом языка и региональных параметров, используя назначенный \(отличный от текущего\) язык и региональные параметры, в качестве параметра `culture`  следует указать объект <xref:System.Globalization.CultureInfo>, представляющий этот язык и региональные параметры.  
  
 Поддерживаемые методом <xref:System.String.Compare%2A?displayProperty=fullName> операции сравнения строк без учета языка и региональных параметров могут быть лингвистическими \(выполняемыми на основе правил сортировки инвариантного языка и региональных параметров\) или нелингвистическими \(выполняемыми на основе порядковых номерах символов в строке\).  Большинство операций сравнения строк без учета языка и региональных параметров являются нелингвистическими.  Для таких операций сравнения в качестве параметра `comparisonType` следует указать значение перечисления <xref:System.StringComparison?displayProperty=fullName> или <xref:System.StringComparison?displayProperty=fullName>.  Например, если решение, влияющее на безопасность \(к примеру, сравнение имени пользователя или пароля\), принимается на основе результата сравнения строк, операция должна быть нелингвистической и выполняться без учета языка и региональных параметров, чтобы на результат не повлияли правила конкретного языка и региональных параметров.  
  
 Если требуется согласованная лингвистическая обработка соответствующих строк из нескольких языков и региональных параметров, следует использовать лингвистическое сравнение строк без учета языка и региональных параметров.  Например, если приложение отображает в списке слова, в которых используется несколько кодировок, может потребоваться отображать слова в одном и том же порядке независимо от текущего языка и региональных параметров.  Для операций лингвистического сравнения без учета языка и региональных параметров платформа .NET Framework определяет инвариантный язык и региональные параметры на основе операций лингвистического сравнения для английского языка.  Для выполнения лингвистического сравнения без учета языка и региональных параметров в качестве параметра `comparisonType` следует указать <xref:System.StringComparison?displayProperty=fullName> или <xref:System.StringComparison?displayProperty=fullName>.  
  
 В следующем примере выполняется два нелингвистических сравнения строк без учета языка и региональных параметров.  В первом сравнении учитывается регистр, а во втором — нет.  
  
 [!code-csharp[Conceptual.Strings.CultureInsensitiveComparison#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.cultureinsensitivecomparison/cs/cultureinsensitive1.cs#1)]
 [!code-vb[Conceptual.Strings.CultureInsensitiveComparison#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.cultureinsensitivecomparison/vb/cultureinsensitive1.vb#1)]  
  
## См. также  
 <xref:System.String.Compare%2A?displayProperty=fullName>   
 <xref:System.String.CompareTo%2A?displayProperty=fullName>   
 [Выполнение строковых операций, не зависящих от языка и региональных параметров](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)   
 [Рекомендации по использованию строк](../../../docs/standard/base-types/best-practices-strings.md)