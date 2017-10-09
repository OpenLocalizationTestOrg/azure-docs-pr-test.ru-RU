---
title: "aaaHow toocreate API в службе управления API Azure"
description: "Узнайте, как toocreate и настройки API-интерфейсов в API управления Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a><span data-ttu-id="c3f69-103">Как toocreate API в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="c3f69-103">How toocreate APIs in Azure API Management</span></span>
<span data-ttu-id="c3f69-104">API в API Management представляет набор операций, которые могут быть вызваны клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="c3f69-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="c3f69-105">Новые интерфейсы API, создаются в портал издателя hello, а затем hello требуемого операции добавляются.</span><span class="sxs-lookup"><span data-stu-id="c3f69-105">New APIs are created in hello publisher portal, and then hello desired operations are added.</span></span> <span data-ttu-id="c3f69-106">После добавления операций hello hello API добавляется tooa продукта и могут быть опубликованы.</span><span class="sxs-lookup"><span data-stu-id="c3f69-106">Once hello operations are added, hello API is added tooa product and can be published.</span></span> <span data-ttu-id="c3f69-107">После публикации API-Интерфейс может быть подписанным tooand используется разработчиками.</span><span class="sxs-lookup"><span data-stu-id="c3f69-107">Once an API is published, it can be subscribed tooand used by developers.</span></span>

<span data-ttu-id="c3f69-108">В этом руководстве показано hello первым шагом в процессе hello: как toocreate и настройте новый интерфейс API в службе управления API.</span><span class="sxs-lookup"><span data-stu-id="c3f69-108">This guide shows hello first step in hello process: how toocreate and configure a new API in API Management.</span></span> <span data-ttu-id="c3f69-109">Дополнительные сведения о добавлении операций и публикация продукта см. в разделе [как tooan tooadd операций API] [ How tooadd operations tooan API] и [как toocreate и публикация продукта] [ How toocreate and publish a product].</span><span class="sxs-lookup"><span data-stu-id="c3f69-109">For more information on adding operations and publishing a product, see [How tooadd operations tooan API][How tooadd operations tooan API] and [How toocreate and publish a product][How toocreate and publish a product].</span></span>

## <span data-ttu-id="c3f69-110"><a name="create-new-api"> </a>Создание нового API</span><span class="sxs-lookup"><span data-stu-id="c3f69-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="c3f69-111">API-интерфейсы создаются и настраиваются на портале hello издателя.</span><span class="sxs-lookup"><span data-stu-id="c3f69-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="c3f69-112">tooaccess hello издателя, щелкните **портал издателя** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="c3f69-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="c3f69-114">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="c3f69-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="c3f69-115">Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **добавить API**.</span><span class="sxs-lookup"><span data-stu-id="c3f69-115">Click **APIs** from hello **API Management** menu on hello left, and then click **add API**.</span></span>

![Создание API][api-management-create-api]

<span data-ttu-id="c3f69-117">Используйте hello **добавьте новый интерфейс API** tooconfigure окно hello новый API.</span><span class="sxs-lookup"><span data-stu-id="c3f69-117">Use hello **Add new API** window tooconfigure hello new API.</span></span>

![Добавление нового API][api-management-add-new-api]

<span data-ttu-id="c3f69-119">Hello следующие поля, используемые tooconfigure hello новый API.</span><span class="sxs-lookup"><span data-stu-id="c3f69-119">hello following fields are used tooconfigure hello new API.</span></span>

* <span data-ttu-id="c3f69-120">**Имя веб-API** предоставляет уникальное и описательное имя для hello API.</span><span class="sxs-lookup"><span data-stu-id="c3f69-120">**Web API name** provides a unique and descriptive name for hello API.</span></span> <span data-ttu-id="c3f69-121">Он отображается в порталах hello разработчиком и издателем.</span><span class="sxs-lookup"><span data-stu-id="c3f69-121">It is displayed in hello developer and publisher portals.</span></span>
* <span data-ttu-id="c3f69-122">**URL-адрес службы веб-** ссылки hello реализации hello API службы HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3f69-122">**Web service URL** references hello HTTP service implementing hello API.</span></span> <span data-ttu-id="c3f69-123">API управления перенаправляет запросы toothis адрес.</span><span class="sxs-lookup"><span data-stu-id="c3f69-123">API management forwards requests toothis address.</span></span>
* <span data-ttu-id="c3f69-124">**Суффикс URL-адреса API Web** — присоединенных toohello базовый URL-адрес для службы управления hello API.</span><span class="sxs-lookup"><span data-stu-id="c3f69-124">**Web API URL suffix** is appended toohello base URL for hello API management service.</span></span> <span data-ttu-id="c3f69-125">Hello базовый URL-адрес является общим для всех интерфейсов API, расположенных в экземпляре службы управления API.</span><span class="sxs-lookup"><span data-stu-id="c3f69-125">hello base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="c3f69-126">API управления API-интерфейсы отличает их суффикс и таким образом суффикс hello должно быть уникальным для каждого API для данного издателя.</span><span class="sxs-lookup"><span data-stu-id="c3f69-126">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="c3f69-127">**Схема URL-адреса API Web** определяет, какие протоколы могут быть используется tooaccess hello API.</span><span class="sxs-lookup"><span data-stu-id="c3f69-127">**Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span> <span data-ttu-id="c3f69-128">По умолчанию указан протокол HTTPs.</span><span class="sxs-lookup"><span data-stu-id="c3f69-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="c3f69-129">toooptionally добавить этот новый продукт tooa API, нажмите кнопку hello **продуктов (необязательно)** раскрывающийся список и выберите продукт.</span><span class="sxs-lookup"><span data-stu-id="c3f69-129">toooptionally add this new API tooa product, click hello **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="c3f69-130">Этот шаг может быть повторяющихся несколько раз tooadd hello API toomultiple продуктов.</span><span class="sxs-lookup"><span data-stu-id="c3f69-130">This step can be repeated multiple times tooadd hello API toomultiple products.</span></span>

<span data-ttu-id="c3f69-131">После hello требуемого значения настроены, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c3f69-131">Once hello desired values are configured, click **Save**.</span></span> <span data-ttu-id="c3f69-132">После создания нового API hello hello сводной страницы для hello API отображается в портал издателя hello.</span><span class="sxs-lookup"><span data-stu-id="c3f69-132">Once hello new API is created, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Сводные данные API][api-management-api-summary]

## <span data-ttu-id="c3f69-134"><a name="configure-api-settings"> </a>Настройка параметров API</span><span class="sxs-lookup"><span data-stu-id="c3f69-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="c3f69-135">Можно использовать hello **параметры** tooverify и измените конфигурацию hello API.</span><span class="sxs-lookup"><span data-stu-id="c3f69-135">You can use hello **Settings** tab tooverify and edit hello configuration for an API.</span></span> <span data-ttu-id="c3f69-136">**Имя веб-API**, **веб-URL-адрес службы**, и **суффикс URL-адрес API** изначально устанавливаются при создании hello API и можно изменить здесь.</span><span class="sxs-lookup"><span data-stu-id="c3f69-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when hello API is created and can be modified here.</span></span> <span data-ttu-id="c3f69-137">**Описание** предоставляет дополнительное описание, и **схему URL-адрес API** определяет, какие протоколы могут быть используется tooaccess hello API.</span><span class="sxs-lookup"><span data-stu-id="c3f69-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span>

![Параметры API][api-management-api-settings]

<span data-ttu-id="c3f69-139">Проверка подлинности шлюза tooconfigure hello серверной реализации hello API службы, рекомендуется выбрать hello **безопасности** hello вкладку **с учетными данными** раскрывающегося списка можно использовать tooconfigure **HTTP Основные** или **клиентские сертификаты** проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c3f69-139">tooconfigure gateway authentication for hello backend service implementing hello API, select hello **Security** tab. hello **With credentials** drop-down can be used tooconfigure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="c3f69-140">Обычная проверка подлинности toouse HTTP, просто введите учетные данные требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="c3f69-140">toouse HTTP basic authentication, simply enter hello desired credentials.</span></span> <span data-ttu-id="c3f69-141">Сведения об использовании проверки подлинности сертификата клиента см. в разделе [как toosecure серверными службами с помощью клиента сертификат проверки подлинности в Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="c3f69-141">For information on using client certificate authentication, see [How toosecure back-end services using client certificate authentication in Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="c3f69-142">Hello **безопасности** вкладке также можно использовать tooconfigure **авторизации пользователей** с помощью OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="c3f69-142">hello **Security** tab can also be used tooconfigure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="c3f69-143">Дополнительные сведения см. в разделе [как разработчик tooauthorize учетных записей с помощью OAuth 2.0 в Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="c3f69-143">For more information, see [How tooauthorize developer accounts using OAuth 2.0 in Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Параметры базовой проверки подлинности][api-management-api-settings-credentials]

<span data-ttu-id="c3f69-145">Нажмите кнопку **Сохранить** toosave можно производить любые изменения toohello параметры API.</span><span class="sxs-lookup"><span data-stu-id="c3f69-145">Click **Save** toosave any changes you make toohello API settings.</span></span>

## <span data-ttu-id="c3f69-146"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3f69-146"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="c3f69-147">После создания API и заданы параметры hello, следующие действия hello, tooadd hello операций toohello API, добавьте hello API tooa продукта и опубликовать его, чтобы он был доступен для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="c3f69-147">Once an API is created and hello settings configured, hello next steps are tooadd hello operations toohello API, add hello API tooa product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="c3f69-148">Дополнительные сведения см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="c3f69-148">For more information, see hello following articles.</span></span>

* <span data-ttu-id="c3f69-149">[Как tooan tooadd операций API][How tooadd operations tooan API]</span><span class="sxs-lookup"><span data-stu-id="c3f69-149">[How tooadd operations tooan API][How tooadd operations tooan API]</span></span>
* <span data-ttu-id="c3f69-150">[Как toocreate и публикация продукта][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="c3f69-150">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
