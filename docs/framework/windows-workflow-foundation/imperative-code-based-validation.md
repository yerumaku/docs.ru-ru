---
title: "Принудительная проверка на уровне кода | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae12537c-455e-42b1-82f4-cea4c46c023e
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Принудительная проверка на уровне кода
Проверка на основе императивного кода доступна для действий, производных от <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity> и <xref:System.Activities.NativeActivity>, и служит простым способом автономной проверки действия.Код проверки, который определяет все ошибки и предупреждения проверки, добавляется к действию.  
  
## Использование проверки на основе кода  
 Проверка на основе кода поддерживается действиями, которые являются производными от <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity> и <xref:System.Activities.NativeActivity>.Код проверки можно поместить в переопределение метода <xref:System.Activities.CodeActivity.CacheMetadata%2A>, при этом ошибки проверки или предупреждения могут быть добавлены к аргументу метаданных.В следующем примере, взятом из образца [Базовая проверка](../../../docs/framework/windows-workflow-foundation/samples/basic-validation.md), если значение `Cost` больше `Price`, к метаданным добавляется ошибка проверки.  
  
> [!NOTE]
>  Обратите внимание, что `Cost` и `Price` являются не аргументами для действия, а свойствами, задаваемыми во время разработки.Поэтому их значения можно проверить в переопределенном методе действия <xref:System.Activities.CodeActivity.CacheMetadata%2A>.Значение потока данных, проходящее через аргумент, не может быть проверено во время разработки, поскольку данные не будут поступать до времени выполнения, но аргументы действия можно проверить, чтобы убедиться, что они связаны, с помощью атрибута `RequiredArgument` и групп перегруженных вариантов.В этом примере код видит атрибут `RequiredArgument` для аргумента `Description` и, если он не связан, формируется ошибка проверки.Обязательные аргументы представлены в [Обязательные аргументы и группы перегруженных аргументов](../../../docs/framework/windows-workflow-foundation//required-arguments-and-overload-groups.md).  
  
```csharp  
public sealed class CreateProduct : CodeActivity  
{  
    public double Price { get; set; }  
    public double Cost { get; set; }  
  
    // [RequiredArgument] attribute will generate a validation error   
    // if the Description argument is not set.  
    [RequiredArgument]  
    public InArgument<string> Description { get; set; }  
  
    protected override void CacheMetadata(CodeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        // Determine when the activity has been configured in an invalid way.  
        if (this.Cost > this.Price)  
        {  
            // Add a validation error with a custom message.  
            metadata.AddValidationError("The Cost must be less than or equal to the Price.");  
        }  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // Not needed for the sample.  
    }  
}  
  
```  
  
 По умолчанию ошибка проверки добавляется к метаданным при вызове <xref:System.Activities.CodeActivityMetadata.AddValidationError%2A>.Чтобы добавить предупреждение проверки, используйте перегрузку <xref:System.Activities.CodeActivityMetadata.AddValidationError%2A>, принимающую <xref:System.Activities.Validation.ValidationError>, и укажите, что <xref:System.Activities.Validation.ValidationError> представляет предупреждение, задав свойство <xref:System.Activities.Validation.ValidationError.IsWarning%2A>.  
  
 Когда рабочий процесс модифицируется в конструкторе, выполняется проверка и любые ошибки или предупреждения, выявленные в ее ходе, отображаются в конструкторе рабочих процессов.Также проверка происходит во время выполнения, когда вызывается рабочий процесс, и при появлении каких\-либо ошибок проверки логикой проверки по умолчанию выдается исключение <xref:System.Activities.InvalidWorkflowException>.[!INCLUDE[crabout](../../../includes/crabout-md.md)] вызове проверки доступа и всех ошибок проверки и предупреждений см. в разделе [Вызов проверки действия](../../../docs/framework/windows-workflow-foundation//invoking-activity-validation.md).  
  
 Исключения, вызванные в методе <xref:System.Activities.CodeActivity.CacheMetadata%2A>, не считаются ошибками проверки.Эти исключения перейдут из метода <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> к вызывающему объекту, который должен их обработать.  
  
 Проверка на основе кода используется для проверки действий, которые содержат код, но для нее недоступны другие действия в рабочем процессе.Проверка декларативных ограничений обеспечивает возможность проверки связи действия и других действий рабочего процесса. Эта проверка описывается в разделе [Декларативные ограничения](../../../docs/framework/windows-workflow-foundation//declarative-constraints.md).