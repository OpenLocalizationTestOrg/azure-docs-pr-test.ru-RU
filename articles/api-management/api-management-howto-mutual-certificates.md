---
title: "aaaSecure серверными службами с помощью проверки подлинности сертификата клиента - службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toosecure серверными службами с помощью клиента сертификат проверки подлинности в службе управления API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a>Как toosecure серверными службами с помощью клиента сертификат проверки подлинности в службе управления API Azure
API управления предоставляет hello возможность toosecure доступа toohello серверную службу API-интерфейса с помощью сертификатов клиента. В этом руководстве показано как toomanage сертификаты в портал издателя hello API и как toouse tooconfigure API tooaccess сертификата его внутренней службы.

Сведения об управлении сертификатами с помощью hello API REST управления API см. в разделе [сущность сертификата API REST управления API Azure][Azure API Management REST API Certificate entity].

## <a name="prerequisites"> </a>Предварительные требования
В этом руководстве показано, как tooconfigure ваш API управления службы экземпляра toouse клиентского сертификата проверки подлинности tooaccess hello внутренней службы для API. Перед hello следующие шаги в этом разделе, необходимо установить вашей внутренней службы, настроенного для проверки подлинности сертификата клиента ([tooconfigure сертификат проверки подлинности в веб-сайтов Azure см. в статье toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), и иметь toohello сертификат и hello пароль для доступа к hello сертификат для передачи в портал издателя управления API hello.

## <a name="step1"> </a>Отправка сертификата клиента
tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для службы управления API. Откроется портал издателя управления API toohello.

![Портал издателя API][api-management-management-console]

> Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.
> 
> 

Нажмите кнопку **безопасности** из hello **API управления** меню hello слева, а затем нажмите **клиентские сертификаты**.

![Client certificates][api-management-security-client-certificates]

tooupload новый сертификат, нажмите кнопку **отправить сертификат**.

![Передача сертификата][api-management-upload-certificate]

Обзор tooyour сертификат, а затем введите пароль hello для hello сертификата.

> Hello сертификат должен находиться в **.pfx** формат. Разрешено использовать самозаверяющие сертификаты.
> 
> 

![Передача сертификата][api-management-upload-certificate-form]

Нажмите кнопку **отправить** tooupload hello сертификата.

> в настоящее время проверяется пароль сертификата Hello. Если он неправильный, появится сообщение об ошибке.
> 
> 

![Сертификат добавлен][api-management-certificate-uploaded]

После передачи сертификата hello, оно появляется на hello **клиентские сертификаты** вкладки. Если у вас есть несколько сертификатов, запишите hello субъекта или hello четыре последних символа отпечаток hello, являющиеся используется tooselect hello сертификат при настройке API toouse сертификаты, как описано в следующих hello [Настройка API toouse сертификат клиента для проверки подлинности шлюза] [ Configure an API toouse a client certificate for gateway authentication] раздела.

> tooturn отключить проверку цепочки сертификатов при использовании, например, самостоятельно подписанный сертификат, выполните hello действия, описанные в данном документе [элемент](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).
> 
> 

## <a name="step1a"> </a>Удаление сертификата клиента
toodelete сертификат, нажмите кнопку **удалить** рядом с hello необходимый сертификат.

![Удаление сертификата][api-management-certificate-delete]

Нажмите кнопку **Да, удалите его** tooconfirm.

![Подтверждение удаления][api-management-confirm-delete]

Если сертификат hello используется API-Интерфейс, появится окно с предупреждением. toodelete hello сертификата, необходимо сначала удалить hello сертификат от интерфейсы API, которые настроенное toouse его.

![Подтверждение удаления][api-management-confirm-delete-policy]

## <a name="step2"></a>Настройка API toouse сертификат клиента для проверки подлинности шлюза
Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, щелкните имя требуемого hello API hello и щелкните hello **безопасности** вкладки.

![Безопасность API][api-management-api-security]

Выберите **клиентских сертификатов** из hello **с учетными данными** раскрывающегося списка.

![Client certificates][api-management-mutual-certificates]

Здравствуйте, выберите необходимый сертификат из hello **сертификат клиента** раскрывающегося списка. При наличии нескольких сертификатов можно рассмотреть hello субъекта или hello четыре последних символа отпечаток hello, как указано в hello предыдущий раздел toodetermine hello правильный сертификат.

![Выбор сертификата][api-management-select-certificate]

Нажмите кнопку **Сохранить** toosave hello конфигурации изменение toohello API.

> Это изменение вступает в силу немедленно, а вызовы toooperations из API, который будет использоваться hello tooauthenticate сертификат на внутреннем сервере hello.
> 
> 

![Сохранение изменений в API][api-management-save-api]

> Когда сертификат для проверки подлинности шлюза для внутренней службы hello API-интерфейса, становится частью hello политики для этого API-интерфейса и можно просмотреть в редакторе политики hello.
> 
> 

![Политика сертификата][api-management-certificate-policy]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о других способах toosecure безопасности внутренней службы, такие как основные или общий секретный проверки подлинности HTTP, см. следующие видео hello.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps



