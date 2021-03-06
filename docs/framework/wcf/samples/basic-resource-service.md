---
title: "Основная служба ресурсов"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4360063e-cc8c-4648-846e-c05a5af51a7a
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 8bfcd632846510f8f62280bfb1620ba1f8c35ce3
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="basic-resource-service"></a>Основная служба ресурсов
В этом образце демонстрируется реализация службы HTTP с использованием модели программирования REST [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], при использовании которой представляется доступ к коллекции клиентов, поддерживающей операции поиска, добавления, удаления и замены. Данный образец состоит из двух компонентов: резидентной службы HTTP [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] (Service.cs) и консольного приложения (program.cs), создающего службу и выполняющего вызовы в этой службе.  
  
## <a name="sample-details"></a>Подробные сведения об образце  
 Служба [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] предоставляет доступ к коллекции клиентов в стиле REST (относительно ресурсов). Кратко говоря, это связано с тем, что каждая запись в коллекции имеет уникальный универсальный код ресурса (URI) для коллекции клиентов и всех клиентов в коллекции. Служба поддерживает отправку HTTP `GET` в универсальном коде ресурса (URI) коллекции для получения всей коллекции и HTTP `POST` в URI коллекции для добавления к коллекции нового клиента. Также для универсального кода ресурса (URI) для отдельного клиента поддерживается отправка HTTP `GET` для получения сведений о клиентах, отправка HTTP `PUT` для замены сведений о клиентах и отправка HTTP `DELETE` для удаления клиента из коллекции. При добавлении к коллекции нового клиента служба назначает ему уникальный URI и сохраняет URI как часть сведений о клиенте. Также назначенный URI передается клиенту с использованием заголовка ответа Location HTTP.  
  
 Файл App.config настраивает для службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] конечную точку по умолчанию <xref:System.ServiceModel.Description.WebHttpEndpoint>, для свойства которой <xref:System.ServiceModel.Description.WebHttpEndpoint.HelpEnabled%2A> задано значение `true`. В результате этого [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] создает автоматическую страницу справки в формате HTML по адресу `http://localhost:8000/Customers/help`, которая предоставляет сведения о том, как строить запросы HTTP службе и как получать доступ к ответу службы в формате HTTP, например образец того, как данные клиента представлены в форматах XML и JSON.  
  
 Предоставление таким способом доступа к коллекции клиентов (и в целом к любому ресурсу) позволяет клиенту взаимодействовать со службой единым образом с помощью URI и команд HTTP `GET`, `PUT`, `DELETE` и `POST`. В файле Program.cs показывается, как можно разработать клиент с помощью <xref:System.Net.HttpWebRequest>. Заметьте, что это лишь один из способов доступа к службе REST [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Также возможен доступ к службе с помощью других классов .NET Framework, например <xref:System.ServiceModel.ChannelFactory> и <xref:System.Net.WebClient>. Другие примеры в пакете SDK (такие как [базовой службы HTTP](../../../../docs/framework/wcf/samples/basic-http-service.md) образца и [автоматический выбор формата](../../../../docs/framework/wcf/samples/automatic-format-selection.md) образец) показано, как использовать эти классы для взаимодействия с [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] службы.  
  
 Образец состоит из резидентной службы и клиента, которые работают в консольном приложении. Во время выполнения консольного приложения клиент совершает запросы к службе и выводит в окно консоли нужные сведения из ответов.  
  
#### <a name="to-use-this-sample"></a>Использование этого образца  
  
1.  Откройте решение в образце базовой службы ресурсов. Для успешного выполнения образца среду [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] необходимо запускать от имени администратора. Для этого щелкните правой кнопкой мыши [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] значок и выбрав **Запуск от имени администратора** в контекстном меню.  
  
2.  Нажмите сочетание клавиш CTRL+SHIFT+B, чтобы построить решение, а затем сочетание клавиш CTRL+F5, чтобы запустить консольное приложение. Открывается окно консоли с URI запущенной службы и URI HTML-страницы справки для запущенной службы. HTML-страницу справки можно просмотреть в любой момент времени, введя URI этой страницы в браузере. Во время работы образца клиент записывает состояние текущего действия.  
  
3.  Чтобы завершить образец, нажмите любую клавишу.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Примеры Windows Communication Foundation (WCF) и Windows Workflow Foundation (WF) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) , чтобы скачать все примеры [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\BasicResourceService`  
  
## <a name="see-also"></a>См. также  
 [Базовая служба HTTP](../../../../docs/framework/wcf/samples/basic-http-service.md)  
 [Автоматический выбор формата](../../../../docs/framework/wcf/samples/automatic-format-selection.md)
