---
title: "&lt;transport&gt; для &lt;netNamedPipeBinding&gt;"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d9eff52d-4bde-4586-b56a-b0ec24611f8d
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 84811c70f2f3608c10d8886900169f804a8c9b62
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="lttransportgt-of-ltnetnamedpipebindinggt"></a>&lt;transport&gt; для &lt;netNamedPipeBinding&gt;
Определяет параметры безопасности транспорта для именованного канала.  
  
 \<system.ServiceModel>  
\<привязки >  
\<netNamedPipeBinding>  
\<Привязка >  
\<Безопасность >  
\<Транспорт >  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<netNamedPipeBinding>  
   <binding>  
      <security mode="None/Transport">  
            <transport protectionLevel="None/Sign/EncryptAndSign" />  
      </security>  
   </binding>  
</netNamedPipeBinding>  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|protectionLevel|Определяет уровень защиты именованного канала. Подпись сообщений уменьшает риск подделки сообщения сторонними лицами при его передаче. Шифрование обеспечивает конфиденциальность на уровне данных во время транспортировки. Допустимы следующие значения:<br /><br /> — None: Без защиты.<br />-Sign: Сообщения подписываются.<br />-EncryptAndSign: Сообщения шифруются и подписываются.<br /><br /> Значение по умолчанию - EncryptAndSign.|  
  
### <a name="child-elements"></a>Дочерние элементы  
 Нет  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание:|  
|-------------|-----------------|  
|[\<Безопасность >](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-netnamedpipebinding.md)|Определяет параметры безопасности для привязки.|  
  
## <a name="see-also"></a>См. также  
 <xref:System.ServiceModel.NamedPipeTransportSecurity>  
 <xref:System.ServiceModel.Configuration.NetNamedPipeSecurityElement.Transport%2A>  
 <xref:System.ServiceModel.NetNamedPipeSecurity.Transport%2A>  
 <xref:System.ServiceModel.Configuration.NamedPipeTransportSecurityElement>  
 [Защита служб и клиентов](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)  
 [Привязки](../../../../../docs/framework/wcf/bindings.md)  
 [Настройка привязок, предоставляемых системой](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)  
 [Использование привязок для настройки служб Windows Communication Foundation и клиентов](http://msdn.microsoft.com/library/bd8b277b-932f-472f-a42a-b02bb5257dfb)  
 [\<Привязка >](../../../../../docs/framework/misc/binding.md)
