---
title: "Защита внутренних служб с помощью проверки подлинности на основе сертификата клиента в службе управления API Azure | Документация Майкрософт"
description: "Узнайте, как защитить фоновые службы посредством проверки подлинности с помощью сертификата клиента в службе Azure API Management"
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
ms.openlocfilehash: 2ebe71c96fd9076a48f689041634dbd23d3d8414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="7f241-103">Защита фоновых служб посредством проверки подлинности с помощью сертификата клиента в службе Azure API Management</span><span class="sxs-lookup"><span data-stu-id="7f241-103">How to secure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="7f241-104">Служба API Management дает возможность защищать доступ к фоновым службам API с помощью сертификатов клиента.</span><span class="sxs-lookup"><span data-stu-id="7f241-104">API Management provides the capability to secure access to the back-end service of an API using client certificates.</span></span> <span data-ttu-id="7f241-105">В этом руководстве описывается, как управлять сертификатами на портале издателя API и как настроить использование сертификата в  API для доступа к фоновой службе.</span><span class="sxs-lookup"><span data-stu-id="7f241-105">This guide shows how to manage certificates in the API publisher portal, and how to configure an API to use a certificate to access its back-end service.</span></span>

<span data-ttu-id="7f241-106">Дополнительные сведения об управлении сертификатами с помощью REST API управления API см. в разделе, посвященном [объекту сертификата REST API управления API Azure][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="7f241-106">For information about managing certificates using the API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="7f241-107"><a name="prerequisites"> </a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7f241-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="7f241-108">В этом руководстве описано, как настроить для экземпляра службы API Management проверку подлинности с помощью сертификата клиента при доступе из API к фоновой службе.</span><span class="sxs-lookup"><span data-stu-id="7f241-108">This guide shows you how to configure your API Management service instance to use client certificate authentication to access the back-end service for an API.</span></span> <span data-ttu-id="7f241-109">Перед выполнением инструкций, приведенных в этой статье, во внутренней службе необходимо настроить аутентификацию на основе сертификата клиента. [Сведения о том, как настроить аутентификацию на основе сертификата на веб-сайтах Azure, см. в этой статье][to configure certificate authentication in Azure WebSites refer to this article]. Кроме того, нужен доступ к сертификату, который следует отправить на портал издателя управления API, и его паролю.</span><span class="sxs-lookup"><span data-stu-id="7f241-109">Before following the steps in this topic, you should have your back-end service configured for client certificate authentication ([to configure certificate authentication in Azure WebSites refer to this article][to configure certificate authentication in Azure WebSites refer to this article]), and have access to the certificate and the password for the certificate for uploading in the API Management publisher portal.</span></span>

## <span data-ttu-id="7f241-110"><a name="step1"> </a>Отправка сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="7f241-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="7f241-111">Чтобы начать работу, щелкните **Publisher portal** (Портал издателя) на портале Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="7f241-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="7f241-112">Будет открыт портал издателя службы управления API.</span><span class="sxs-lookup"><span data-stu-id="7f241-112">This takes you to the API Management publisher portal.</span></span>

![Портал издателя API][api-management-management-console]

> <span data-ttu-id="7f241-114">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="7f241-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="7f241-115">В левой части экрана в меню **Управление API** выберите пункт **Безопасность**, а затем перейдите на вкладку **Сертификаты клиента**.</span><span class="sxs-lookup"><span data-stu-id="7f241-115">Click **Security** from the **API Management** menu on the left, and click **Client certificates**.</span></span>

![Client certificates][api-management-security-client-certificates]

<span data-ttu-id="7f241-117">Чтобы добавить новый сертификат, щелкните ссылку **Upload certificate**(Загрузить сертификат).</span><span class="sxs-lookup"><span data-stu-id="7f241-117">To upload a new certificate, click **Upload certificate**.</span></span>

![Upload certificate][api-management-upload-certificate]

<span data-ttu-id="7f241-119">Выберите сертификат и введите пароль к нему.</span><span class="sxs-lookup"><span data-stu-id="7f241-119">Browse to your certificate, and then enter the password for the certificate.</span></span>

> <span data-ttu-id="7f241-120">Сертификат должен быть в формате **PFX** .</span><span class="sxs-lookup"><span data-stu-id="7f241-120">The certificate must be in **.pfx** format.</span></span> <span data-ttu-id="7f241-121">Разрешено использовать самозаверяющие сертификаты.</span><span class="sxs-lookup"><span data-stu-id="7f241-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Upload certificate][api-management-upload-certificate-form]

<span data-ttu-id="7f241-123">Нажмите кнопку **Upload** (Загрузить).</span><span class="sxs-lookup"><span data-stu-id="7f241-123">Click **Upload** to upload the certificate.</span></span>

> <span data-ttu-id="7f241-124">После этого будет проверен пароль к сертификату.</span><span class="sxs-lookup"><span data-stu-id="7f241-124">The certificate password is validated at this time.</span></span> <span data-ttu-id="7f241-125">Если он неправильный, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="7f241-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Сертификат добавлен][api-management-certificate-uploaded]

<span data-ttu-id="7f241-127">После добавления сертификат появляется на вкладке **Сертификаты клиента**.</span><span class="sxs-lookup"><span data-stu-id="7f241-127">Once the certificate is uploaded, it appears on the **Client certificates** tab.</span></span> <span data-ttu-id="7f241-128">Если у вас несколько сертификатов, запишите субъект или последние четыре знака отпечатка. Эти данные используются для выбора сертификата при настройке API для использования сертификатов, как описано в разделе [Настройка API для проверки подлинности шлюза с помощью сертификата клиента][Configure an API to use a client certificate for gateway authentication] ниже.</span><span class="sxs-lookup"><span data-stu-id="7f241-128">If you have multiple certificates, make a note of the subject, or the last four characters of the thumbprint, which are used to select the certificate when configuring an API to use certificates, as covered in the following [Configure an API to use a client certificate for gateway authentication][Configure an API to use a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="7f241-129">Чтобы отключить проверку цепочки сертификатов при использовании, например, самозаверяющего сертификата, выполните действия, описанные в [этом разделе](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end) часто задаваемых вопросов.</span><span class="sxs-lookup"><span data-stu-id="7f241-129">To turn off certificate chain validation when using, for example, a self-signed certificate, follow the steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="7f241-130"><a name="step1a"> </a>Удаление сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="7f241-130"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="7f241-131">Чтобы удалить сертификат, щелкните рядом с ним ссылку **Delete** (Удалить).</span><span class="sxs-lookup"><span data-stu-id="7f241-131">To delete a certificate, click **Delete** beside the desired certificate.</span></span>

![Удаление сертификата][api-management-certificate-delete]

<span data-ttu-id="7f241-133">Чтобы подтвердить действие, нажмите кнопку **Yes, delete it** (Да, удалить).</span><span class="sxs-lookup"><span data-stu-id="7f241-133">Click **Yes, delete it** to confirm.</span></span>

![Подтверждение удаления][api-management-confirm-delete]

<span data-ttu-id="7f241-135">Если сертификат используется интерфейсом API, появляется предупреждение.</span><span class="sxs-lookup"><span data-stu-id="7f241-135">If the certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="7f241-136">Перед удалением сертификата нужно сначала удалить его из всех API, которые настроены на его использование.</span><span class="sxs-lookup"><span data-stu-id="7f241-136">To delete the certificate you must first remove the certificate from any APIs that are configured to use it.</span></span>

![Подтверждение удаления][api-management-confirm-delete-policy]

## <span data-ttu-id="7f241-138"><a name="step2"> </a>Настройка API для проверки подлинности шлюза с помощью сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="7f241-138"><a name="step2"> </a>Configure an API to use a client certificate for gateway authentication</span></span>
<span data-ttu-id="7f241-139">В левой части экрана в меню **Управление API** выберите пункт **Интерфейсы API**, щелкните имя нужного API и перейдите на вкладку **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="7f241-139">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, and click the **Security** tab.</span></span>

![Безопасность API][api-management-api-security]

<span data-ttu-id="7f241-141">В раскрывающемся списке **С учетными данными** выберите пункт **Сертификаты клиента**.</span><span class="sxs-lookup"><span data-stu-id="7f241-141">Select **Client certificates** from the **With credentials** drop-down list.</span></span>

![Client certificates][api-management-mutual-certificates]

<span data-ttu-id="7f241-143">В раскрывающемся списке **Client certificate** (Сертификат клиента) выберите нужный сертификат.</span><span class="sxs-lookup"><span data-stu-id="7f241-143">Select the desired certificate from the **Client certificate** drop-down list.</span></span> <span data-ttu-id="7f241-144">Если сертификатов несколько, то выбрать нужный можно по субъекту или последним четырем символам отпечатка, которые вы записали ранее.</span><span class="sxs-lookup"><span data-stu-id="7f241-144">If there are multiple certificates you can look at the subject or the last four characters of the thumbprint as noted in the previous section to determine the correct certificate.</span></span>

![Выбор сертификата][api-management-select-certificate]

<span data-ttu-id="7f241-146">Чтобы сохранить изменение конфигурации в API, нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="7f241-146">Click **Save** to save the configuration change to the API.</span></span>

> <span data-ttu-id="7f241-147">Изменение вступает в силу немедленно, и для проверки подлинности на фоновом сервере при вызове операций этого API теперь будет использоваться сертификат.</span><span class="sxs-lookup"><span data-stu-id="7f241-147">This change is effective immediately, and calls to operations of that API will use the certificate to authenticate on the back-end server.</span></span>
> 
> 

![Сохранение изменений в API][api-management-save-api]

> <span data-ttu-id="7f241-149">Если сертификат настроен для проверки подлинности шлюза при доступе к серверной службе API, он становится частью политики для этого API, и его можно увидеть в редакторе политики.</span><span class="sxs-lookup"><span data-stu-id="7f241-149">When a certificate is specified for gateway authentication for the back-end service of an API, it becomes part of the policy for that API, and can be viewed in the policy editor.</span></span>
> 
> 

![Политика сертификата][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="7f241-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f241-151">Next steps</span></span>
<span data-ttu-id="7f241-152">Дополнительные сведения о других способах защиты фоновой службы, таких как базовая проверка подлинности HTTP или проверка подлинности с общим секретом, см. в следующем видео.</span><span class="sxs-lookup"><span data-stu-id="7f241-152">For more information on other ways to secure your backend service, such as HTTP basic or shared secret authentication, see the following video.</span></span>

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



[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[to configure certificate authentication in Azure WebSites refer to this article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API to use a client certificate for gateway authentication]: #step2
[Test the configuration by calling an operation in the Developer Portal]: #step3
[Next steps]: #next-steps



