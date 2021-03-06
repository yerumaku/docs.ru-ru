---
title: "Атаки с повторением"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7a17e040-93cd-4432-81b9-9f62fec78c8f
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: df2a7a78e876ec3228491569c918ad9add2e080d
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="replay-attacks"></a>Атаки с повторением
Объект *атака воспроизведения* возникает, когда злоумышленник копирует поток сообщений между двумя сторонами и воспроизводит его для одного или нескольких сторон. Если не приняты ответные меры, атакованные компьютеры обрабатывают этот поток как допустимые сообщения, что приводит к ряду негативных последствий, таких как повторные заказы одного элемента.  
  
## <a name="bindings-may-be-subject-to-reflection-attacks"></a>Привязки могут подвергаться атакам отражения  
 *Атаки отражения* представляют собой воспроизведение сообщений обратно отправителю, как будто они поступают от получателя в качестве ответа. Стандартные *обнаружения воспроизведения* в [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] механизм не автоматически обрабатывать такие ошибки.  
  
 Атаки отражения предотвращаются по умолчанию, поскольку модель службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] добавляет в сообщения запроса подписанный идентификатор сообщения и ожидает получить в сообщениях ответов подписанный заголовок `relates-to`. В результате сообщение запроса не может быть воспроизведено в качестве ответа. В сценариях защищенного надежного обмена сообщениями (RM) для предотвращения атак отражения принимаются следующие меры.  
  
-   Схемы сообщения о создании последовательности и ответного сообщения о создании последовательности должны быть различными.  
  
-   В симплексных последовательностях сообщения о последовательности, отправляемые клиентом, не могут быть воспроизведены обратно клиенту, поскольку клиент не распознает такие сообщения.  
  
-   В дуплексных последовательностях два идентификатора последовательности должны быть уникальными. Таким образом, исходящее сообщение последовательности не может быть воспроизведено в качестве входящего сообщения последовательности (все заголовки последовательности и тела сообщений также являются подписанными).  
  
 Единственным типом привязок, чувствительных к атакам отражения, являются специальные привязки, в которых отключен протокол WS-Addressing и в которых используется защита на основе симметричного ключа. В привязке <xref:System.ServiceModel.BasicHttpBinding> по умолчанию не используется протокол WS-Addressing, однако защита на основе симметричных ключей используется таким образом, что привязка не является уязвимой для атаки такого типа.  
  
 Для устранения рисков специальных привязок следует не устанавливать контекст безопасности или требовать использования заголовков WS-Addressing.  
  
## <a name="web-farm-attacker-replays-request-to-multiple-nodes"></a>Веб-ферма: злоумышленник воспроизводит запрос на нескольких узлах  
 Клиент использует службу, которая реализована на веб-ферме. Злоумышленник воспроизводит запрос, отправленный на один узел фермы, на другом узле фермы. Кроме того, в случае перезапуска службы кэш воспроизведения очищается, что позволяет злоумышленнику воспроизвести запрос. (В кэше содержатся использованные ранее значения подписи сообщения. Кэш не позволяет воспроизводить их, так что такие подписи могут использоваться только один раз. Кэш воспроизведения не является общим в масштабах веб-фермы.)  
  
 Возможные способы борьбы с этими угрозами  
  
-   Использование безопасности режима сообщений с маркерами контекста безопасности с отслеживанием состояния (как с включенным, так и с отключенным безопасным диалогом). [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Как: создать контекст безопасности для безопасного сеанса маркера](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).  
  
-   Настройка службы для использования безопасности уровня транспорта.  
  
## <a name="see-also"></a>См. также  
 [Вопросы безопасности](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)  
 [Раскрытие информации](../../../../docs/framework/wcf/feature-details/information-disclosure.md)  
 [Повышение привилегий](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)  
 [Отказ в обслуживании](../../../../docs/framework/wcf/feature-details/denial-of-service.md)  
 [Подделка](../../../../docs/framework/wcf/feature-details/tampering.md)  
 [Неподдерживаемые сценарии](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)
