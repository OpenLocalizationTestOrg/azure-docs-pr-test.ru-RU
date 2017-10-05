---
title: "Как создавать интерфейсы API в Azure API Management"
description: "Сведения о создании и настройке API в службе управления API Azure."
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
ms.openlocfilehash: ab08256fbc3caca05bf23a12016ad2acf4fc7412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-apis-in-azure-api-management"></a><span data-ttu-id="977bf-103">Как создавать интерфейсы API в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="977bf-103">How to create APIs in Azure API Management</span></span>
<span data-ttu-id="977bf-104">API в API Management представляет набор операций, которые могут быть вызваны клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="977bf-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="977bf-105">Новые интерфейсы API создаются на портале издателя, после чего добавляются требуемые операции.</span><span class="sxs-lookup"><span data-stu-id="977bf-105">New APIs are created in the publisher portal, and then the desired operations are added.</span></span> <span data-ttu-id="977bf-106">После добавления операций интерфейс API добавляется к продукту и может быть опубликован.</span><span class="sxs-lookup"><span data-stu-id="977bf-106">Once the operations are added, the API is added to a product and can be published.</span></span> <span data-ttu-id="977bf-107">После публикации API на него могут подписаться разработчики для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="977bf-107">Once an API is published, it can be subscribed to and used by developers.</span></span>

<span data-ttu-id="977bf-108">В этом руководстве описывается первый этап в процессе создания и настройки нового интерфейса API в управлении API.</span><span class="sxs-lookup"><span data-stu-id="977bf-108">This guide shows the first step in the process: how to create and configure a new API in API Management.</span></span> <span data-ttu-id="977bf-109">Дополнительные сведения о добавлении операций и публикации продукта см. в статьях [Добавление операций в API в Azure API Management][How to add operations to an API] и [Создание и публикация продукта в службе управления API Azure][How to create and publish a product].</span><span class="sxs-lookup"><span data-stu-id="977bf-109">For more information on adding operations and publishing a product, see [How to add operations to an API][How to add operations to an API] and [How to create and publish a product][How to create and publish a product].</span></span>

## <span data-ttu-id="977bf-110"><a name="create-new-api"> </a>Создание нового API</span><span class="sxs-lookup"><span data-stu-id="977bf-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="977bf-111">API создаются и настраиваются на портале издателя.</span><span class="sxs-lookup"><span data-stu-id="977bf-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="977bf-112">Чтобы перейти на портал издателя, на портале Azure щелкните **Publisher portal** (Портал издателя) для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="977bf-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="977bf-114">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="977bf-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="977bf-115">Щелкните **API** в расположенном слева меню **Управление API**, а затем щелкните **Добавить API**.</span><span class="sxs-lookup"><span data-stu-id="977bf-115">Click **APIs** from the **API Management** menu on the left, and then click **add API**.</span></span>

![Создание API][api-management-create-api]

<span data-ttu-id="977bf-117">Для настройки нового API используйте окно **Добавление нового API** .</span><span class="sxs-lookup"><span data-stu-id="977bf-117">Use the **Add new API** window to configure the new API.</span></span>

![Добавление нового API][api-management-add-new-api]

<span data-ttu-id="977bf-119">Следующие поля используются для настройки нового API.</span><span class="sxs-lookup"><span data-stu-id="977bf-119">The following fields are used to configure the new API.</span></span>

* <span data-ttu-id="977bf-120">**Название веб-API** представляет собой уникальное описательное имя для API.</span><span class="sxs-lookup"><span data-stu-id="977bf-120">**Web API name** provides a unique and descriptive name for the API.</span></span> <span data-ttu-id="977bf-121">Оно выводится на порталах разработчика и издателя.</span><span class="sxs-lookup"><span data-stu-id="977bf-121">It is displayed in the developer and publisher portals.</span></span>
* <span data-ttu-id="977bf-122">**URL-адрес веб-службы** ссылается на реализующую API HTTP-службу.</span><span class="sxs-lookup"><span data-stu-id="977bf-122">**Web service URL** references the HTTP service implementing the API.</span></span> <span data-ttu-id="977bf-123">Портал управления API направит запросы по этому адресу.</span><span class="sxs-lookup"><span data-stu-id="977bf-123">API management forwards requests to this address.</span></span>
* <span data-ttu-id="977bf-124">**Суффикс URL-адреса веб-API** добавляется к основному URL-адресу для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="977bf-124">**Web API URL suffix** is appended to the base URL for the API management service.</span></span> <span data-ttu-id="977bf-125">Основной URL-адрес является общим для всех интерфейсов API, размещенных в экземпляре службы API Management.</span><span class="sxs-lookup"><span data-stu-id="977bf-125">The base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="977bf-126">API Management отличает интерфейсы API по их суффиксу. Следовательно, суффикс должен быть уникальным для каждого API для заданного издателя.</span><span class="sxs-lookup"><span data-stu-id="977bf-126">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="977bf-127">**Схема URL-адреса веб-API** определяет, какой протокол будет использоваться для доступа к API.</span><span class="sxs-lookup"><span data-stu-id="977bf-127">**Web API URL scheme** determines which protocols can be used to access the API.</span></span> <span data-ttu-id="977bf-128">По умолчанию указан протокол HTTPs.</span><span class="sxs-lookup"><span data-stu-id="977bf-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="977bf-129">Чтобы при необходимости добавить этот новый API в продукт, в раскрывающемся списке **Продукты (необязательно)** выберите продукт.</span><span class="sxs-lookup"><span data-stu-id="977bf-129">To optionally add this new API to a product, click the **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="977bf-130">Этот шаг можно повторить несколько раз, чтобы добавить API в несколько продуктов.</span><span class="sxs-lookup"><span data-stu-id="977bf-130">This step can be repeated multiple times to add the API to multiple products.</span></span>

<span data-ttu-id="977bf-131">После настройки нужных значений нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="977bf-131">Once the desired values are configured, click **Save**.</span></span> <span data-ttu-id="977bf-132">После создания нового API на портале издателя выводится страница сводных данных для API.</span><span class="sxs-lookup"><span data-stu-id="977bf-132">Once the new API is created, the summary page for the API is displayed in the publisher portal.</span></span>

![Сводные данные API][api-management-api-summary]

## <span data-ttu-id="977bf-134"><a name="configure-api-settings"> </a>Настройка параметров API</span><span class="sxs-lookup"><span data-stu-id="977bf-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="977bf-135">Для проверки и изменения конфигурации для API можно использовать вкладку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="977bf-135">You can use the **Settings** tab to verify and edit the configuration for an API.</span></span> <span data-ttu-id="977bf-136">**Имя веб-API**, **URL-адрес веб-службы** и **суффикс URL-адреса веб-API** изначально настраиваются при создании интерфейса API и могут быть изменены здесь.</span><span class="sxs-lookup"><span data-stu-id="977bf-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when the API is created and can be modified here.</span></span> <span data-ttu-id="977bf-137">Параметр **Описание** содержит необязательное описание, а параметр **Схема URL-адреса веб-API** определяет, какие протоколы будут использоваться для доступа к API.</span><span class="sxs-lookup"><span data-stu-id="977bf-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used to access the API.</span></span>

![Параметры API][api-management-api-settings]

<span data-ttu-id="977bf-139">Чтобы настроить проверку подлинности шлюза для серверной службы, реализующей API, перейдите на вкладку **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="977bf-139">To configure gateway authentication for the backend service implementing the API, select the **Security** tab.</span></span> <span data-ttu-id="977bf-140">Для настройки **обычной проверки подлинности HTTP** или проверки подлинности с помощью **сертификатов клиента** можно использовать раскрывающийся список **С учетными данными**.</span><span class="sxs-lookup"><span data-stu-id="977bf-140">The **With credentials** drop-down can be used to configure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="977bf-141">Чтобы использовать обычную проверку подлинности HTTP, просто введите нужные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="977bf-141">To use HTTP basic authentication, simply enter the desired credentials.</span></span> <span data-ttu-id="977bf-142">Сведения об использовании аутентификации с помощью сертификатов клиента см. в статье [Защита фоновых служб посредством проверки подлинности с помощью сертификата клиента в службе Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="977bf-142">For information on using client certificate authentication, see [How to secure back-end services using client certificate authentication in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="977bf-143">На вкладке **Безопасность** также можно настроить **авторизацию пользователя** с помощью OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="977bf-143">The **Security** tab can also be used to configure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="977bf-144">Дополнительные сведения см. в статье [Авторизация учетных записей разработчиков с помощью протокола OAuth 2.0 в службе управления Azure API][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="977bf-144">For more information, see [How to authorize developer accounts using OAuth 2.0 in Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Параметры базовой проверки подлинности][api-management-api-settings-credentials]

<span data-ttu-id="977bf-146">Щелкните **Сохранить** для сохранения любых изменений, внесенных в параметры API.</span><span class="sxs-lookup"><span data-stu-id="977bf-146">Click **Save** to save any changes you make to the API settings.</span></span>

## <span data-ttu-id="977bf-147"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="977bf-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="977bf-148">После того, как API создан, и параметры настроены, следует добавить операции в API, добавить API к продукту и опубликовать его, чтобы данный интерфейс стал доступен для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="977bf-148">Once an API is created and the settings configured, the next steps are to add the operations to the API, add the API to a product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="977bf-149">Дополнительные сведения см. в следующих руководствах.</span><span class="sxs-lookup"><span data-stu-id="977bf-149">For more information, see the following articles.</span></span>

* <span data-ttu-id="977bf-150">[Добавление операций в API в Azure API Management][How to add operations to an API]</span><span class="sxs-lookup"><span data-stu-id="977bf-150">[How to add operations to an API][How to add operations to an API]</span></span>
* <span data-ttu-id="977bf-151">[Создание и публикация продукта в службе управления API Azure][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="977bf-151">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How to secure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How to authorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
