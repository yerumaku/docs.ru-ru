---
title: "x:Arguments Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "x:Arguments directive [XAML Services]"
  - "Arguments directive in XAML [XAML Services]"
  - "XAML [XAML Services], x:Arguments directive"
ms.assetid: 87cc10b0-b610-4025-b6b0-ab27ca27c92e
caps.latest.revision: 12
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 12
---
# x:Arguments Directive
Упаковывает аргументы создания для объявления объектного элемента в конструкторе, не являющемся конструктором по умолчанию, в XAML или для объявления объекта фабричного метода.  
  
## Использование элемента XAML \(конструктор не по умолчанию\)  
  
```  
<object ...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## Использование элемента XAML \(фабричный метод\)  
  
```  
<object x:FactoryMethod="methodName"...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## Значения XAML  
  
|||  
|-|-|  
|`oneOrMoreObjectElements`|Один или несколько элементов объекта, определяющие аргументы, передаваемые резервным методом фабрики или конструктора, не заданного по умолчанию.<br /><br /> Типичное использование заключается в том, чтобы использовать текст инициализации внутри элементов object для указания фактических значений аргументов.  См. раздел примеров.<br /><br /> Порядок элементов имеет значение.  Порядок XAML\-типов должен соответствовать типам и порядку типов резервного конструктора или перегрузки статичного метода.|  
|`methodName`|Имя фабричного метода, который должен обрабатывать любые аргументы `x:Arguments`.|  
  
## Зависимости  
 `x:FactoryMethod` может изменять область и поведение, где применяется `x:Arguments`.  
  
 Если не указан ни один `x:FactoryMethod`, то `x:Arguments` применяются к альтернативным \(не установленным по умолчанию\) сигнатурам резервных конструкторов.  
  
 Если задан `x:FactoryMethod`, то `x:Arguments` применяется к перегрузке именованного метода.  
  
## Заметки  
 XAML 2006 потенциально поддерживает нестандартную инициализацию с помощью текста инициализации.  Однако практическое применение методики построения текста инициализации ограничено.  Текст инициализации рассматривается как единая текстовая строка. Поэтому это только добавляет возможность инициализации одного параметра, за исключением случая, когда для поведения конструирования определяется преобразователь типов, который может проанализировать элементы пользовательских данных и пользовательские разделители из строки.  Кроме того, логика преобразования текстовой строки в объект потенциально может представлять собой собственный используемый по умолчанию преобразователь типов данного средства синтаксического анализа XAML для обработки примитивов, отличных от настоящей строки.  
  
 Использование элемента XAML `x:Arguments` не является использованием элемента свойства в обычном смысле, так как разметка директивы не ссылается на тип элемента содержащего его объекта.  Это более свойственно для других директив, таких как `x:Code`, где этот элемент разграничивает диапазон, в котором разметку следует интерпретировать как отличную от используемой по умолчанию разметки для дочернего содержимого.  В этом случае тип XAML каждого элемента объекта сообщает сведения о типах аргументов, которые используется средством синтаксического анализа XAML, чтобы определить на какую определенную сигнатуру фабричного метода конструктора пытается сослаться потребление `x:Arguments`.  
  
 `x:Arguments` для создаваемого элемента объекта должен предварять другие элементы свойства и должен предшествовать содержимому, внутреннему тексту или строкам инициализации элемента объекта.  Элементы объекта в `x:Arguments` могут включать атрибуты и строки инициализации в соответствии с тем, что разрешено типом XAML и его резервным конструктором или фабричным методом.  И для объекта, и для аргументов можно указать пользовательские типы XAML или типы XAML, которые иначе находятся за пределами пространства имен XAML по умолчанию, путем ссылки на установленные сопоставления префиксов.  
  
 Процессоры XAML используют следующие руководящие принципы для определения того, как указанные в `x:Arguments` аргументы должны использоваться для создания объекта.  Если `x:FactoryMethod` указан, данные сравниваются с указанным методом `x:FactoryMethod` \(обратите внимание, что значение `x:FactoryMethod` является именем метода, и именованный метод может иметь перегрузки.  Если `x:FactoryMethod` не указан, данные сравниваются с набором всех перегрузок открытого конструктора объекта.  Логика обработки XAML затем сравнивает количество параметров и выбирает перегрузку с соответствующей арностью.  Если имеется более одного совпадения, обработчик XAML должен сравнивать типы параметров на основе типов XAML предоставляемых элементов объекта.  Если по\-прежнему имеется более одного совпадения, поведение процессора XAML не определено.  Если `x:FactoryMethod` определен, но метод невозможно разрешить, обработчик XAML должен выдавать исключение.  
  
 Использование атрибута XAML `<x:Arguments>string</x:Arguments>` технически возможно.  Однако это не обеспечивает дополнительных возможностей по сравнению с тем, что можно сделать через текст инициализации и преобразователи типов, и использование данного синтаксиса не является намеренной реализацией возможностей фабричного метода XAML 2009.  
  
## Примеры  
 В следующем примере показана сигнатуры конструктора не по умолчанию, а затем использование XAML `x:Arguments`, осуществляющего доступ к этой подписи.  
  
```csharp  
public class Food {  
    private string _name;  
    private Int32 _calories;  
    public Food(string name, Int32 calories) {  
        _name=name;  
        _calories=calories;  
    }  
}  
```  
  
```  
<my:Food>  
    <x:Arguments>  
        <x:String>Apple</x:String>  
        <x:Int32>150</x:Int32>  
    </x:Arguments>  
</my:Food>  
```  
  
 В следующем примере показана сигнатура целевого фабричного метод, а затем использование XAML `x:Arguments`, осуществляющего доступ к этой сигнатуре.  
  
```csharp  
public Food TryLookupFood(string name)  
{  
  switch (name) {  
    case "Apple": return new Food("Apple",150);  
    case "Chocolate": return new Food("Chocolate",200);  
    case "Cheese": return new Food("Cheese", 450);  
    default: {return new Food(name,0);  
  }  
}  
```  
  
```  
<my:Food x:FactoryMethod="TryLookupFood">  
    <x:Arguments>  
        <x:String>Apple</x:String>  
    </x:Arguments>  
</my:Food>  
```  
  
## См. также  
 [Defining Custom Types for Use with .NET Framework XAML Services](../../../docs/framework/xaml-services/defining-custom-types-for-use-with-net-framework-xaml-services.md)   
 [Общие сведения о языке XAML \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)