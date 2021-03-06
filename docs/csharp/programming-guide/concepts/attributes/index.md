---
title: "Атрибуты (C#)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-csharp
ms.topic: article
ms.assetid: f148f13f-a0d5-4f22-9c87-4b73d5dde270
caps.latest.revision: "3"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: f9fc23cf7afbd28f0c9ae438cbce298cbf362fbd
ms.sourcegitcommit: 685143b62385500f59bc36274b8adb191f573a16
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2017
---
# <a name="attributes-c"></a>Атрибуты (C#)
Атрибуты предоставляют мощное средство для связывания метаданных или декларативной информации с кодом (сборки, типы, методы, свойства и т. д.). Связав атрибут связан с сущностью программы, вы можете проверять этот атрибут во время выполнения, используя технику *отражения*. Подробнее см. в разделе [Отражение (C#)](../../../../csharp/programming-guide/concepts/reflection.md).  
  
 Атрибуты имеют следующие свойства.  
  
-   Атрибуты добавляют в программу метаданные. *Метаданные* — это сведения о типах, определенных в программе. Все сборки .NET содержат некоторый набор метаданных, описывающих типы и члены типов, определенные в этой сборке. Вы можете добавить пользовательские атрибуты, чтобы указать любую дополнительную информацию. Подробнее см. в разделе [Создание настраиваемых атрибутов (C#)](../../../../csharp/programming-guide/concepts/attributes/creating-custom-attributes.md).  
  
-   Вы можете применить один или несколько атрибутов ко всей сборке, к модулю или к более мелким элементам программы, например к классам и свойствам.  
  
-   Атрибуты могут принимать аргументы, так же как методы и свойства.  
  
-   Программа может проверить собственные метаданные или метаданные в других программах, используя отражение. Дополнительные сведения см. в разделе [Обращение к атрибутам с помощью отражения (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md).  
  
## <a name="using-attributes"></a>Использование атрибутов  
 Атрибуты можно использовать почти в любых объявлениях, но для каждого атрибута можно ограничить типы объявлений, в которых он является допустимым. Чтобы указать атрибут на C#, поместите имя атрибута в квадратных скобках ([]) над объявлением сущности, к которой он применяется.  
  
 В этом примере атрибут <xref:System.SerializableAttribute> используется для применения определенной характеристики к классу:  
  
```csharp  
[System.Serializable]  
public class SampleClass  
{  
    // Objects of this type can be serialized.  
}  
```  
  
 Метод с атрибутом <xref:System.Runtime.InteropServices.DllImportAttribute> объявляется следующим образом:  
  
```csharp  
using System.Runtime.InteropServices;  
```  
  
```csharp  
[System.Runtime.InteropServices.DllImport("user32.dll")]  
extern static void SampleMethod();  
```  
  
 В объявлении можно разместить несколько атрибутов:  
  
```csharp  
using System.Runtime.InteropServices;  
```  
  
```csharp  
void MethodA([In][Out] ref double x) { }  
void MethodB([Out][In] ref double x) { }  
void MethodC([In, Out] ref double x) { }  
```  
  
 Некоторые атрибуты можно указать для одной сущности более одного раза. Пример такого многократно используемого атрибута — <xref:System.Diagnostics.ConditionalAttribute>:  
  
```csharp  
[Conditional("DEBUG"), Conditional("TEST1")]  
void TraceMethod()  
{  
    // ...  
}  
```  
  
> [!NOTE]
>  По соглашению все имена атрибутов заканчиваются словом "Attribute", чтобы отличать их от других элементов платформы .NET Framework. Но при использовании атрибута в коде этот суффикс можно не указывать. Например, обращение `[DllImport]` эквивалентно `[DllImportAttribute]`, хотя в .NET Framework этот атрибут имеет имя `DllImportAttribute`.  
  
### <a name="attribute-parameters"></a>Параметры атрибутов  
 Многие атрибуты имеют параметры, которые могут быть позиционными, неименованными или именованными. Позиционные параметры необходимо указывать в строгом порядке и их нельзя опускать. Именованные параметры являются необязательными и их можно указывать в любом порядке. Сначала указываются позиционные параметры. Например, эти три атрибута являются эквивалентными:  
  
```csharp  
[DllImport("user32.dll")]  
[DllImport("user32.dll", SetLastError=false, ExactSpelling=false)]  
[DllImport("user32.dll", ExactSpelling=false, SetLastError=false)]  
```  
  
 Первый параметр (имя библиотеки DLL) является позиционным и всегда располагается первым, остальные параметры являются именованными. В этом примере оба именованных параметра имеют значение по умолчанию (false), и мы можем их опустить. Сведения о значениях параметров по умолчанию указываются в документации по каждому отдельному атрибуту.  
  
### <a name="attribute-targets"></a>Целевые объекты атрибутов  
 *Целевой объект* атрибута — это сущность, к которой применяется атрибут. Например, атрибут можно применить к классу, отдельному методу или ко всей сборке. По умолчанию атрибут применяется к тому элементу, перед которым он указан. Но у вас есть возможность явным образом указать, например, что атрибут применяется к методу, параметру или возвращаемому значению.  
  
 Чтобы явным образом определить целевой объект атрибута, используйте следующий синтаксис:  
  
```csharp  
[target : attribute-list]  
```  
  
 Возможные значения `target` перечислены в следующей таблице.  
  
|Целевое значение|Применение|  
|------------------|----------------|  
|`assembly`|Вся сборка|  
|`module`|Модуль текущей сборки|  
|`field`|Поле в классе или структуре|  
|`event`|Событие|  
|`method`|Метод либо методы доступа к свойствам `get` и `set`|  
|`param`|Параметры метода или параметры метода доступа `set`|  
|`property`|Свойство|  
|`return`|Возвращаемое значение метода, индексатора свойства или метода доступа к свойствам `get`|  
|`type`|Структура, класс, интерфейс, перечисление или делегат|  
  
 Следующий пример демонстрирует, как применить атрибуты к сборкам и модулям. Дополнительные сведения см. в разделе [Общие атрибуты (C#)](../../../../csharp/programming-guide/concepts/attributes/common-attributes.md).  
  
```csharp  
using System;  
using System.Reflection;  
[assembly: AssemblyTitleAttribute("Production assembly 4")]  
[module: CLSCompliant(true)]  
```  
  
 В следующем примере показано, как применять атрибуты к методам, параметрам и возвращаемым значениям методов в C#.  
  
```csharp  
// default: applies to method  
[SomeAttr]  
int Method1() { return 0; }  
  
// applies to method  
[method: SomeAttr]  
int Method2() { return 0; }  
  
// applies to return value  
[return: SomeAttr]  
int Method3() { return 0; }  
```  
  
> [!NOTE]
>  Вне зависимости от целевых объектов, для которых действует атрибут `SomeAttr`, необходимо задать целевой объект для `return`, даже если атрибут `SomeAttr` назначен только возвращаемым значениям. Другими словами, компилятор не будет использовать сведения `AttributeUsage` для разрешения конфликтов между неоднозначными целевыми объектами атрибута. Подробнее см. в разделе [AttributeUsage (C#)](../../../../csharp/programming-guide/concepts/attributes/attributeusage.md).  
  
## <a name="common-uses-for-attributes"></a>Популярные методы применения атрибутов  
 В следующем списке перечислены несколько распространенных применений для атрибутов.  
  
-   Указание для методов в веб-службах атрибута `WebMethod`, который обозначает, что метод должен вызываться по протоколу SOAP. Для получения дополнительной информации см. <xref:System.Web.Services.WebMethodAttribute>.  
  
-   Описание способов упаковки параметров методов при взаимодействии с машинным кодом. Для получения дополнительной информации см. <xref:System.Runtime.InteropServices.MarshalAsAttribute>.  
  
-   Описание свойств COM для классов, методов и интерфейсов.  
  
-   Вызов неуправляемого кода с помощью класса <xref:System.Runtime.InteropServices.DllImportAttribute>.  
  
-   Указание для сборки таких параметров, как заголовок, версия, описание или товарный знак.  
  
-   Указание членов класса, которые будут сериализованы при сохранении класса.  
  
-   Описание правил сопоставления членов класса с XML-узлами при XML-сериализации.  
  
-   Описание требований безопасности для методов.  
  
-   Указание характеристик, используемых для обеспечения безопасности.  
  
-   Управление оптимизацией для JIT-компилятора, сохраняя при этом простоту отладки кода.  
  
-   Получение сведений об объекте, вызывающем метод.  
  
## <a name="related-sections"></a>Связанные разделы  
 Дополнительные сведения:  
  
-   [Создание настраиваемых атрибутов (C#)](../../../../csharp/programming-guide/concepts/attributes/creating-custom-attributes.md)  
  
-   [Обращение к атрибутам с помощью отражения (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)  
  
-   [Практическое руководство. Создание объединения C/C++ с помощью атрибутов (C#)](../../../../csharp/programming-guide/concepts/attributes/how-to-create-a-c-cpp-union-by-using-attributes.md)  
  
-   [Общие атрибуты (C#)](../../../../csharp/programming-guide/concepts/attributes/common-attributes.md)  
  
-   [Caller Information (C#)](../../../../csharp/programming-guide/concepts/caller-information.md) (Сведения о вызывающем объекте (C#))  
  
## <a name="see-also"></a>См. также  
 [Руководство по программированию на C#](../../../../csharp/programming-guide/index.md)  
 [Reflection (C#)](../../../../csharp/programming-guide/concepts/reflection.md) (Отражение (C#))  
 [Атрибуты](../../../../../docs/standard/attributes/index.md)
