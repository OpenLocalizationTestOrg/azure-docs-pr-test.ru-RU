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
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="c639b-103">Как toosecure серверными службами с помощью клиента сертификат проверки подлинности в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="c639b-103">How toosecure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="c639b-104">API управления предоставляет hello возможность toosecure доступа toohello серверную службу API-интерфейса с помощью сертификатов клиента.</span><span class="sxs-lookup"><span data-stu-id="c639b-104">API Management provides hello capability toosecure access toohello back-end service of an API using client certificates.</span></span> <span data-ttu-id="c639b-105">В этом руководстве показано как toomanage сертификаты в портал издателя hello API и как toouse tooconfigure API tooaccess сертификата его внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="c639b-105">This guide shows how toomanage certificates in hello API publisher portal, and how tooconfigure an API toouse a certificate tooaccess its back-end service.</span></span>

<span data-ttu-id="c639b-106">Сведения об управлении сертификатами с помощью hello API REST управления API см. в разделе [сущность сертификата API REST управления API Azure][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="c639b-106">For information about managing certificates using hello API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="c639b-107"><a name="prerequisites"> </a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c639b-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="c639b-108">В этом руководстве показано, как tooconfigure ваш API управления службы экземпляра toouse клиентского сертификата проверки подлинности tooaccess hello внутренней службы для API.</span><span class="sxs-lookup"><span data-stu-id="c639b-108">This guide shows you how tooconfigure your API Management service instance toouse client certificate authentication tooaccess hello back-end service for an API.</span></span> <span data-ttu-id="c639b-109">Перед hello следующие шаги в этом разделе, необходимо установить вашей внутренней службы, настроенного для проверки подлинности сертификата клиента ([tooconfigure сертификат проверки подлинности в веб-сайтов Azure см. в статье toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), и иметь toohello сертификат и hello пароль для доступа к hello сертификат для передачи в портал издателя управления API hello.</span><span class="sxs-lookup"><span data-stu-id="c639b-109">Before following hello steps in this topic, you should have your back-end service configured for client certificate authentication ([tooconfigure certificate authentication in Azure WebSites refer toothis article][tooconfigure certificate authentication in Azure WebSites refer toothis article]), and have access toohello certificate and hello password for hello certificate for uploading in hello API Management publisher portal.</span></span>

## <span data-ttu-id="c639b-110"><a name="step1"> </a>Отправка сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="c639b-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="c639b-111">tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="c639b-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="c639b-112">Откроется портал издателя управления API toohello.</span><span class="sxs-lookup"><span data-stu-id="c639b-112">This takes you toohello API Management publisher portal.</span></span>

![Портал издателя API][api-management-management-console]

> <span data-ttu-id="c639b-114">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="c639b-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="c639b-115">Нажмите кнопку **безопасности** из hello **API управления** меню hello слева, а затем нажмите **клиентские сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="c639b-115">Click **Security** from hello **API Management** menu on hello left, and click **Client certificates**.</span></span>

![Client certificates][api-management-security-client-certificates]

<span data-ttu-id="c639b-117">tooupload новый сертификат, нажмите кнопку **отправить сертификат**.</span><span class="sxs-lookup"><span data-stu-id="c639b-117">tooupload a new certificate, click **Upload certificate**.</span></span>

![Передача сертификата][api-management-upload-certificate]

<span data-ttu-id="c639b-119">Обзор tooyour сертификат, а затем введите пароль hello для hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="c639b-119">Browse tooyour certificate, and then enter hello password for hello certificate.</span></span>

> <span data-ttu-id="c639b-120">Hello сертификат должен находиться в **.pfx** формат.</span><span class="sxs-lookup"><span data-stu-id="c639b-120">hello certificate must be in **.pfx** format.</span></span> <span data-ttu-id="c639b-121">Разрешено использовать самозаверяющие сертификаты.</span><span class="sxs-lookup"><span data-stu-id="c639b-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Передача сертификата][api-management-upload-certificate-form]

<span data-ttu-id="c639b-123">Нажмите кнопку **отправить** tooupload hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="c639b-123">Click **Upload** tooupload hello certificate.</span></span>

> <span data-ttu-id="c639b-124">в настоящее время проверяется пароль сертификата Hello.</span><span class="sxs-lookup"><span data-stu-id="c639b-124">hello certificate password is validated at this time.</span></span> <span data-ttu-id="c639b-125">Если он неправильный, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="c639b-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Сертификат добавлен][api-management-certificate-uploaded]

<span data-ttu-id="c639b-127">После передачи сертификата hello, оно появляется на hello **клиентские сертификаты** вкладки. Если у вас есть несколько сертификатов, запишите hello субъекта или hello четыре последних символа отпечаток hello, являющиеся используется tooselect hello сертификат при настройке API toouse сертификаты, как описано в следующих hello [Настройка API toouse сертификат клиента для проверки подлинности шлюза] [ Configure an API toouse a client certificate for gateway authentication] раздела.</span><span class="sxs-lookup"><span data-stu-id="c639b-127">Once hello certificate is uploaded, it appears on hello **Client certificates** tab. If you have multiple certificates, make a note of hello subject, or hello last four characters of hello thumbprint, which are used tooselect hello certificate when configuring an API toouse certificates, as covered in hello following [Configure an API toouse a client certificate for gateway authentication][Configure an API toouse a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="c639b-128">tooturn отключить проверку цепочки сертификатов при использовании, например, самостоятельно подписанный сертификат, выполните hello действия, описанные в данном документе [элемент](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="c639b-128">tooturn off certificate chain validation when using, for example, a self-signed certificate, follow hello steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="c639b-129"><a name="step1a"> </a>Удаление сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="c639b-129"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="c639b-130">toodelete сертификат, нажмите кнопку **удалить** рядом с hello необходимый сертификат.</span><span class="sxs-lookup"><span data-stu-id="c639b-130">toodelete a certificate, click **Delete** beside hello desired certificate.</span></span>

![Удаление сертификата][api-management-certificate-delete]

<span data-ttu-id="c639b-132">Нажмите кнопку **Да, удалите его** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="c639b-132">Click **Yes, delete it** tooconfirm.</span></span>

![Подтверждение удаления][api-management-confirm-delete]

<span data-ttu-id="c639b-134">Если сертификат hello используется API-Интерфейс, появится окно с предупреждением.</span><span class="sxs-lookup"><span data-stu-id="c639b-134">If hello certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="c639b-135">toodelete hello сертификата, необходимо сначала удалить hello сертификат от интерфейсы API, которые настроенное toouse его.</span><span class="sxs-lookup"><span data-stu-id="c639b-135">toodelete hello certificate you must first remove hello certificate from any APIs that are configured toouse it.</span></span>

![Подтверждение удаления][api-management-confirm-delete-policy]

## <span data-ttu-id="c639b-137"><a name="step2"></a>Настройка API toouse сертификат клиента для проверки подлинности шлюза</span><span class="sxs-lookup"><span data-stu-id="c639b-137"><a name="step2"> </a>Configure an API toouse a client certificate for gateway authentication</span></span>
<span data-ttu-id="c639b-138">Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, щелкните имя требуемого hello API hello и щелкните hello **безопасности** вкладки.</span><span class="sxs-lookup"><span data-stu-id="c639b-138">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, and click hello **Security** tab.</span></span>

![Безопасность API][api-management-api-security]

<span data-ttu-id="c639b-140">Выберите **клиентских сертификатов** из hello **с учетными данными** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="c639b-140">Select **Client certificates** from hello **With credentials** drop-down list.</span></span>

![Client certificates][api-management-mutual-certificates]

<span data-ttu-id="c639b-142">Здравствуйте, выберите необходимый сертификат из hello **сертификат клиента** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="c639b-142">Select hello desired certificate from hello **Client certificate** drop-down list.</span></span> <span data-ttu-id="c639b-143">При наличии нескольких сертификатов можно рассмотреть hello субъекта или hello четыре последних символа отпечаток hello, как указано в hello предыдущий раздел toodetermine hello правильный сертификат.</span><span class="sxs-lookup"><span data-stu-id="c639b-143">If there are multiple certificates you can look at hello subject or hello last four characters of hello thumbprint as noted in hello previous section toodetermine hello correct certificate.</span></span>

![Выбор сертификата][api-management-select-certificate]

<span data-ttu-id="c639b-145">Нажмите кнопку **Сохранить** toosave hello конфигурации изменение toohello API.</span><span class="sxs-lookup"><span data-stu-id="c639b-145">Click **Save** toosave hello configuration change toohello API.</span></span>

> <span data-ttu-id="c639b-146">Это изменение вступает в силу немедленно, а вызовы toooperations из API, который будет использоваться hello tooauthenticate сертификат на внутреннем сервере hello.</span><span class="sxs-lookup"><span data-stu-id="c639b-146">This change is effective immediately, and calls toooperations of that API will use hello certificate tooauthenticate on hello back-end server.</span></span>
> 
> 

![Сохранение изменений в API][api-management-save-api]

> <span data-ttu-id="c639b-148">Когда сертификат для проверки подлинности шлюза для внутренней службы hello API-интерфейса, становится частью hello политики для этого API-интерфейса и можно просмотреть в редакторе политики hello.</span><span class="sxs-lookup"><span data-stu-id="c639b-148">When a certificate is specified for gateway authentication for hello back-end service of an API, it becomes part of hello policy for that API, and can be viewed in hello policy editor.</span></span>
> 
> 

![Политика сертификата][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="c639b-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c639b-150">Next steps</span></span>
<span data-ttu-id="c639b-151">Дополнительные сведения о других способах toosecure безопасности внутренней службы, такие как основные или общий секретный проверки подлинности HTTP, см. следующие видео hello.</span><span class="sxs-lookup"><span data-stu-id="c639b-151">For more information on other ways toosecure your backend service, such as HTTP basic or shared secret authentication, see hello following video.</span></span>

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



