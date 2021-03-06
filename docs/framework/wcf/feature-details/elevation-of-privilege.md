---
title: "Повышение привилегий"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- elevation of privilege [WCF]
- security [WCF], elevation of privilege
ms.assetid: 146e1c66-2a76-4ed3-98a5-fd77851a06d9
caps.latest.revision: "16"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 4225460698d36b3b56b9b0b03cde34e4502b13c9
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="elevation-of-privilege"></a>Повышение привилегий
*Несанкционированное получение прав* полученный в результате, когда злоумышленник права по сравнению с были предоставлены изначально. Например, злоумышленник, ранее имевший разрешение «только для чтения», может каким-либо образом расширить его до уровня «чтение и запись».  
  
## <a name="trusted-sts-should-sign-saml-token-claims"></a>Доверенная служба маркеров безопасности должна подписывать утверждения маркеров SAML  
 Маркер языка SAML (Security Assertions Markup Language) - это универсальный маркер XML, являющийся типом по умолчанию для выдаваемых маркеров. Маркер SAML может создаваться при обмене данными службой маркеров безопасности, которой веб-служба доверяет. Маркеры SAML содержат утверждения в операторах. Злоумышленник может скопировать утверждения из действительного маркера, создать новый маркер SAML и подписать его именем другого издателя. Идея состоит в том, чтобы проверить, проверяет ли сервер издателей, и, если сервер этого не делает, создать маркеры SAML, расширяющие права по сравнению с правами, которые выдаются доверенной службой маркеров безопасности.  
  
 Класс <xref:System.IdentityModel.Tokens.SamlAssertion> проверяет цифровые подписи в токене SAML, и класс <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> по умолчанию требует, чтобы токены SAML были подписаны сертификатом X.509, если свойство <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> класса <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> имеет значение <xref:System.ServiceModel.Security.X509CertificateValidationMode.ChainTrust>. Одного использования режима `ChainTrust` недостаточно, чтобы определить, является ли издатель токена SAML доверенным. Службы, которым требуется более детальная модель управления безопасностью, могут использовать политики авторизации и принудительного применения для проверки издателей наборов утверждений, создаваемых при проверке подлинности токенов, или использовать параметры проверки X.509 в <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> для ограничения набора разрешенных сертификатов подписи. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Управление утверждениями и авторизацией с помощью модели удостоверения](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md) и [Федерация и выданные маркеры](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md).  
  
## <a name="switching-identity-without-a-security-context"></a>Смена удостоверения без контекста безопасности  
 Приведенные ниже сведения относятся только к [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)].  
  
 При установке подключения между клиентом и сервером удостоверение клиента не изменяется, если только не имеет место следующая ситуация: после открытия клиента [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], если выполняются все приведенные ниже условия:  
  
-   Процедуры определения контекста безопасности (с помощью безопасности транспорта и сеансы безопасности сообщений) отключены (<xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> свойству `false` в случае безопасности сообщений или транспорта, не поддерживающий создание системы безопасности в случае безопасности транспорта используются сеансы. Пример подобного транспорта - HTTPS.);  
  
-   используется проверка подлинности Windows;  
  
-   учетные данные не задаются явным образом;  
  
-   служба вызывается в олицетворенном контексте безопасности.  
  
 Если эти условия выполняются, удостоверение, которое используется для проверки подлинности клиента на стороне службы, может измениться (в данном случае не может использоваться олицетворенное удостоверение, но может использоваться удостоверение процесса) после открытия клиента [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Это происходит потому, что удостоверение Windows, которое используется для проверки подлинности клиента на стороне службы, передается с каждым сообщением, а удостоверение, которое используется для проверки подлинности, получается из удостоверения Windows текущего потока. Если удостоверение Windows текущего потока изменяется (например, путем олицетворения другого вызывающего объекта), удостоверение, которое прикрепляется к сообщению и используется для проверки подлинности клиента на стороне службы, также может измениться.  
  
 Если при использовании проверки подлинности Windows совместно с олицетворением требуется детерминированное поведение, необходимо явным образом задать учетные данные Windows или установить со службой контекст безопасности. Для этого следует использовать сеанс безопасности сообщений или сеанс безопасности транспорта. Например, сеанс безопасности транспорта можно обеспечить с помощью транспорта net.tcp. Кроме того, при вызове службы необходимо использовать только синхронную версию операций клиента. При установки контекста безопасности сообщений необходимо поддерживать подключение к службе открытым дольше, чем длится настроенный период обновления сеанса, поскольку удостоверение также может измениться в процессе обновления сеанса.  
  
### <a name="credentials-capture"></a>Получение учетных данных  
 Приведенные ниже сведения относятся к [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] и последующим версиям.  
  
 Учетные данные, используемые клиентом или службой, основаны на текущем потоке контекста. Получение учетных данных происходит, когда вызывается метод `Open` (или `BeginOpen` для асинхронных вызовов) клиента или службы. Для классов <xref:System.ServiceModel.ServiceHost> и <xref:System.ServiceModel.ClientBase%601> методы `Open` и `BeginOpen` наследуются от методов <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> и <xref:System.ServiceModel.Channels.CommunicationObject.BeginOpen%2A> класса <xref:System.ServiceModel.Channels.CommunicationObject>.  
  
> [!NOTE]
>  При использовании метода `BeginOpen` невозможно гарантировать, что получаемые учетные данные принадлежат процессу, вызвавшему метод.  
  
## <a name="token-caches-allow-replay-using-obsolete-data"></a>Кэширование делает возможным повторное использование маркеров с помощью устаревших данных  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] использует функцию `LogonUser` подсистемы LSA для проверки подлинности пользователей по их имени и паролю. Поскольку при вызове функции входа используется большое количество ресурсов, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] позволяет в целях повышения производительности кэшировать маркеры, представляющие прошедших проверку подлинности пользователей. Механизм кэширования сохраняет результаты предыдущей функции `LogonUser` для использования в будущем. Этот механизм отключен по умолчанию. Чтобы ее включить, задайте <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.CacheLogonTokens%2A> свойства `true`, или используйте `cacheLogonTokens` атрибут [ \<userNameAuthentication >](../../../../docs/framework/configure-apps/file-schema/wcf/usernameauthentication.md).  
  
 Чтобы установить срок жизни кэшированных маркеров, задайте для свойства <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.CachedLogonTokenLifetime%2A> значение <xref:System.TimeSpan> или установите значение атрибута `cachedLogonTokenLifetime` элемента `userNameAuthentication`; значение по умолчанию - 15 минут. Обратите внимание, что пока маркер находится в кэше, любой клиент, который указывает соответствующие имя пользователя и пароль, может использовать маркер, даже если учетная запись была удалена из Windows или если пароль изменился. До истечения срока жизни и удаления маркера из кэша [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] позволяет пользователям (в том числе и потенциально опасным) проходить проверку подлинности.  
  
 Чтобы ограничить связанные с этим угрозы, уменьшите вероятность атаки, задав в качестве значения `cachedLogonTokenLifetime` минимальный промежуток времени, который может потребоваться пользователям.  
  
## <a name="issued-token-authorization-expiration-reset-to-large-value"></a>Авторизация выданных маркеров: сброс времени истечения до больших значений  
 При выполнении некоторых условий для свойства <xref:System.IdentityModel.Policy.AuthorizationContext.ExpirationTime%2A> объекта <xref:System.IdentityModel.Policy.AuthorizationContext> может быть установлено неожиданно большое значение (значение поля <xref:System.DateTime.MaxValue> минус один день или 20 декабря 9999 г.).  
  
 Это происходит при использовании <xref:System.ServiceModel.WSFederationHttpBinding> и любой из предоставляемых системой привязок, которые получили в качестве типа удостоверения клиента выданный маркер.  
  
 Кроме того, это происходит при создании пользовательских привязок с помощью одного из следующих методов.  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenBindingElement%2A>  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement%2A>  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForSslBindingElement%2A>  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenOverTransportBindingElement%2A>  
  
 Чтобы ограничить эту проблему, политика авторизации должна проверять действие и срок действия каждой политики авторизации.  
  
## <a name="the-service-uses-a-different-certificate-than-the-client-intended"></a>Служба использует не тот сертификат, который ожидает клиент  
 При выполнении определенных условий клиент может снабдить сообщение цифровой подписью с сертификатом X.509, но служба извлечет другой сертификат.  
  
 Это может произойти при следующих обстоятельствах.  
  
-   Клиент снабжает сообщение цифровой подписью с сертификатом X.509, но не прикрепляет к сообщению сертификат X.509; вместо этого он только ссылается на сертификат, используя идентификатор ключа субъекта.  
  
-   Компьютер службы содержит один или несколько сертификатов с одним и тем же открытым ключом, но они содержат различную информацию.  
  
-   Служба извлекает сертификат, соответствующий идентификатору ключа субъекта, но оказывается, что это не тот сертификат, использования которого ожидал клиент. Когда среда [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] получает сообщение и проверяет подпись, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] сопоставляет информацию в извлеченном сертификате X.509 с набором утверждений, которые отличаются от ожидаемых клиентом и, возможно, предоставляют расширенные полномочия.  
  
 Чтобы избежать этого, следует ссылаться на сертификат X.509 иначе, например с помощью поля <xref:System.ServiceModel.Security.Tokens.X509KeyIdentifierClauseType.IssuerSerial>.  
  
## <a name="see-also"></a>См. также  
 [Вопросы безопасности](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)  
 [Раскрытие информации](../../../../docs/framework/wcf/feature-details/information-disclosure.md)  
 [Отказ в обслуживании](../../../../docs/framework/wcf/feature-details/denial-of-service.md)  
 [Атаки с повторением](../../../../docs/framework/wcf/feature-details/replay-attacks.md)  
 [Подделка](../../../../docs/framework/wcf/feature-details/tampering.md)  
 [Неподдерживаемые сценарии](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)
