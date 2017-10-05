---
title: "Управление версиями пакетов SDK клиента и сервера в мобильных приложениях и мобильных службах | Документация Майкрософт"
description: "Список пакетов SDK клиента и сведения о совместимости с версиями пакетов SDK сервера для мобильных служб и мобильных приложений Azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: f79e819b1547f81498ea213858faf3c75e374782
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="3c2dd-103">Управление версиями клиента и сервера в мобильных приложениях и мобильных службах</span><span class="sxs-lookup"><span data-stu-id="3c2dd-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="3c2dd-104">Последняя версия мобильных служб Azure — компонент **Мобильные приложения** службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-104">The latest version of Azure Mobile Services is the **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="3c2dd-105">Пакеты SDK для клиента и сервера мобильных приложений основаны на аналогичных пакетах мобильных служб, но *не совместимы* с ними.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-105">The Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="3c2dd-106">Другими словами, пакет SDK клиента *мобильных приложений* необходимо использовать с пакетом SDK сервера *мобильных приложений* (точно так же и для *мобильных служб*).</span><span class="sxs-lookup"><span data-stu-id="3c2dd-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="3c2dd-107">Этот контракт реализуется посредством специального значения заголовка, используемого пакетами SDK для клиента и сервера, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-107">This contract is enforced through a special header value used by the client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="3c2dd-108">Примечание. Когда в этом документе упоминается внутренний сервер *мобильных служб*, он не обязательно должен размещаться в мобильных службах.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-108">Note: whenever this document refers to a *Mobile Services* backend, it does not necessarily need to be hosted on Mobile Services.</span></span> <span data-ttu-id="3c2dd-109">Теперь можно выполнить миграцию мобильной службы для работы в службе приложений без внесения изменений в код, однако служба по-прежнему будет использовать версии пакета SDK для *мобильных служб*.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-109">It is now possible to migrate a mobile service to run on App Service without any code changes, but the service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="3c2dd-110">Дополнительные сведения о переносе в службу приложений, не изменяя код, см. в статье [Перенос существующей мобильной службы Azure в службу приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="3c2dd-110">To learn more about migrating to App Service without any code changes, see the article [Migrate a Mobile Service to Azure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="3c2dd-111">Спецификация заголовка</span><span class="sxs-lookup"><span data-stu-id="3c2dd-111">Header specification</span></span>
<span data-ttu-id="3c2dd-112">Ключ `ZUMO-API-VERSION` можно указать в заголовке HTTP или в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-112">The key `ZUMO-API-VERSION` may be specified in either the HTTP header or the query string.</span></span> <span data-ttu-id="3c2dd-113">Его значение представляет строку версии в формате **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-113">The value is a version string in the form **x.y.z**.</span></span>

<span data-ttu-id="3c2dd-114">Например:</span><span class="sxs-lookup"><span data-stu-id="3c2dd-114">For example:</span></span>

<span data-ttu-id="3c2dd-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="3c2dd-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="3c2dd-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="3c2dd-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="3c2dd-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="3c2dd-118">Отказ от проверки версий</span><span class="sxs-lookup"><span data-stu-id="3c2dd-118">Opting out of version checking</span></span>
<span data-ttu-id="3c2dd-119">От проверки версий можно отказаться, задав для параметра приложения **MS_SkipVersionCheck** значение **true**.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-119">You can opt out of version checking by setting a value of **true** for the app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="3c2dd-120">Укажите это значение в файле web.config или в разделе параметров приложения портала Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-120">Specify this either in your web.config or in the Application Settings section of the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3c2dd-121">Работа мобильных приложений отличается от мобильных служб в нескольких аспектах, в частности, в сфере автономной синхронизации, проверки подлинности и push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in the areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="3c2dd-122">Вы можете отказаться от проверки версий только после выполнения тщательного тестирования, чтобы изменения в работе не нарушили функциональность приложения.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-122">You should only opt out of version checking after complete testing to ensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="3c2dd-123">Сводные сведения о совместимости для всех версий</span><span class="sxs-lookup"><span data-stu-id="3c2dd-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="3c2dd-124">Ниже приведены сведения о совместимости между всеми типами клиентов и серверов.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-124">The chart below shows the compatibility between all client and server types.</span></span> <span data-ttu-id="3c2dd-125">Серверная часть называется мобильными **службами** или мобильными **приложениями** в зависимости от используемого пакета SDK сервера.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on the server SDK that it uses.</span></span>

|  | <span data-ttu-id="3c2dd-126">**мобильных служб** </span><span class="sxs-lookup"><span data-stu-id="3c2dd-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="3c2dd-127">**Мобильные приложения** </span><span class="sxs-lookup"><span data-stu-id="3c2dd-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c2dd-128">[Клиенты мобильных служб]</span><span class="sxs-lookup"><span data-stu-id="3c2dd-128">[Mobile Services clients]</span></span> |<span data-ttu-id="3c2dd-129">кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="3c2dd-129">Ok</span></span> |<span data-ttu-id="3c2dd-130">Ошибка\*</span><span class="sxs-lookup"><span data-stu-id="3c2dd-130">Error\*</span></span> |
| <span data-ttu-id="3c2dd-131">[Клиенты мобильных приложений]</span><span class="sxs-lookup"><span data-stu-id="3c2dd-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="3c2dd-132">Ошибка\*</span><span class="sxs-lookup"><span data-stu-id="3c2dd-132">Error\*</span></span> |<span data-ttu-id="3c2dd-133">кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="3c2dd-133">Ok</span></span> |

<span data-ttu-id="3c2dd-134">\*Это поведение можно изменить, указав параметр **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  The anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: the fwlink to this document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="3c2dd-135"><a name="1.0.0"></a>Клиент и сервер мобильных служб</span><span class="sxs-lookup"><span data-stu-id="3c2dd-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="3c2dd-136">Пакеты SDK клиента в таблице ниже совместимы с **мобильными службами**.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-136">The client SDKs in the table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="3c2dd-137">Примечание. Пакеты SDK для клиента мобильных служб *не* отправляют значение заголовка для `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="3c2dd-137">Note: the Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="3c2dd-138">Если служба получает этот заголовок или значение строки запроса, будет возвращена ошибка, если только вы явно не отказались от проверки версий (см. выше).</span><span class="sxs-lookup"><span data-stu-id="3c2dd-138">If the service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="3c2dd-139"><a name="MobileServicesClients"></a> Пакеты SDK для клиента мобильных *служб*</span><span class="sxs-lookup"><span data-stu-id="3c2dd-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="3c2dd-140">Платформа клиента</span><span class="sxs-lookup"><span data-stu-id="3c2dd-140">Client platform</span></span> | <span data-ttu-id="3c2dd-141">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="3c2dd-141">Version</span></span> | <span data-ttu-id="3c2dd-142">Значение заголовка версии</span><span class="sxs-lookup"><span data-stu-id="3c2dd-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c2dd-143">Управляемый клиент (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="3c2dd-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="3c2dd-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="3c2dd-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="3c2dd-145">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3c2dd-145">n/a</span></span> |
| <span data-ttu-id="3c2dd-146">iOS</span><span class="sxs-lookup"><span data-stu-id="3c2dd-146">iOS</span></span> |[<span data-ttu-id="3c2dd-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="3c2dd-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="3c2dd-148">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3c2dd-148">n/a</span></span> |
| <span data-ttu-id="3c2dd-149">Android</span><span class="sxs-lookup"><span data-stu-id="3c2dd-149">Android</span></span> |[<span data-ttu-id="3c2dd-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="3c2dd-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="3c2dd-151">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3c2dd-151">n/a</span></span> |
| <span data-ttu-id="3c2dd-152">HTML</span><span class="sxs-lookup"><span data-stu-id="3c2dd-152">HTML</span></span> |[<span data-ttu-id="3c2dd-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="3c2dd-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="3c2dd-154">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3c2dd-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="3c2dd-155">Пакеты SDK для сервера мобильных *служб*</span><span class="sxs-lookup"><span data-stu-id="3c2dd-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="3c2dd-156">Платформа сервера</span><span class="sxs-lookup"><span data-stu-id="3c2dd-156">Server platform</span></span> | <span data-ttu-id="3c2dd-157">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="3c2dd-157">Version</span></span> | <span data-ttu-id="3c2dd-158">Принятый заголовок версии</span><span class="sxs-lookup"><span data-stu-id="3c2dd-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c2dd-159">.NET</span><span class="sxs-lookup"><span data-stu-id="3c2dd-159">.NET</span></span> |[<span data-ttu-id="3c2dd-160">WindowsAzure.MobileServices.Backend.* версия 1.0.x</span><span class="sxs-lookup"><span data-stu-id="3c2dd-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="3c2dd-161">** Отсутствует заголовок версии **</span><span class="sxs-lookup"><span data-stu-id="3c2dd-161">**No version header **</span></span> |
| <span data-ttu-id="3c2dd-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="3c2dd-162">Node.js</span></span> |<span data-ttu-id="3c2dd-163">(ожидается в ближайшее время)</span><span class="sxs-lookup"><span data-stu-id="3c2dd-163">(coming soon)</span></span> |<span data-ttu-id="3c2dd-164">**Отсутствует заголовок версии**</span><span class="sxs-lookup"><span data-stu-id="3c2dd-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="3c2dd-165">Поведение внутренних серверов мобильных служб</span><span class="sxs-lookup"><span data-stu-id="3c2dd-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="3c2dd-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="3c2dd-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="3c2dd-167">Значение параметра MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="3c2dd-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="3c2dd-168">Ответ</span><span class="sxs-lookup"><span data-stu-id="3c2dd-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c2dd-169">Не указан</span><span class="sxs-lookup"><span data-stu-id="3c2dd-169">Not specified</span></span> |<span data-ttu-id="3c2dd-170">Любой</span><span class="sxs-lookup"><span data-stu-id="3c2dd-170">Any</span></span> |<span data-ttu-id="3c2dd-171">200 – OK</span><span class="sxs-lookup"><span data-stu-id="3c2dd-171">200 - OK</span></span> |
| <span data-ttu-id="3c2dd-172">Любое значение</span><span class="sxs-lookup"><span data-stu-id="3c2dd-172">Any value</span></span> |<span data-ttu-id="3c2dd-173">Истина</span><span class="sxs-lookup"><span data-stu-id="3c2dd-173">True</span></span> |<span data-ttu-id="3c2dd-174">200 – OK</span><span class="sxs-lookup"><span data-stu-id="3c2dd-174">200 - OK</span></span> |
| <span data-ttu-id="3c2dd-175">Любое значение</span><span class="sxs-lookup"><span data-stu-id="3c2dd-175">Any value</span></span> |<span data-ttu-id="3c2dd-176">False/не указан</span><span class="sxs-lookup"><span data-stu-id="3c2dd-176">False/Not Specified</span></span> |<span data-ttu-id="3c2dd-177">400 – неверный запрос</span><span class="sxs-lookup"><span data-stu-id="3c2dd-177">400 - Bad Request</span></span> |

## <span data-ttu-id="3c2dd-178"><a name="2.0.0"></a>Клиент и сервер мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="3c2dd-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="3c2dd-179"><a name="MobileAppsClients"></a> Пакеты SDK для клиента мобильных *приложений*</span><span class="sxs-lookup"><span data-stu-id="3c2dd-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="3c2dd-180">Проверка версии была добавлена, начиная со следующих версий пакета SDK для клиента **мобильных приложений Azure**:</span><span class="sxs-lookup"><span data-stu-id="3c2dd-180">Version checking was introduced starting with the following versions of the client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="3c2dd-181">Платформа клиента</span><span class="sxs-lookup"><span data-stu-id="3c2dd-181">Client platform</span></span> | <span data-ttu-id="3c2dd-182">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="3c2dd-182">Version</span></span> | <span data-ttu-id="3c2dd-183">Значение заголовка версии</span><span class="sxs-lookup"><span data-stu-id="3c2dd-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c2dd-184">Управляемый клиент (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="3c2dd-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="3c2dd-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="3c2dd-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="3c2dd-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="3c2dd-186">2.0.0</span></span> |
| <span data-ttu-id="3c2dd-187">iOS</span><span class="sxs-lookup"><span data-stu-id="3c2dd-187">iOS</span></span> |[<span data-ttu-id="3c2dd-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="3c2dd-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="3c2dd-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="3c2dd-189">2.0.0</span></span> |
| <span data-ttu-id="3c2dd-190">Android</span><span class="sxs-lookup"><span data-stu-id="3c2dd-190">Android</span></span> |[<span data-ttu-id="3c2dd-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="3c2dd-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="3c2dd-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="3c2dd-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="3c2dd-193">Пакеты SDK для сервера мобильных *приложений*</span><span class="sxs-lookup"><span data-stu-id="3c2dd-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="3c2dd-194">Проверка версий входит в состав следующих версий пакета SDK сервера:</span><span class="sxs-lookup"><span data-stu-id="3c2dd-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="3c2dd-195">Платформа сервера</span><span class="sxs-lookup"><span data-stu-id="3c2dd-195">Server platform</span></span> | <span data-ttu-id="3c2dd-196">SDK</span><span class="sxs-lookup"><span data-stu-id="3c2dd-196">SDK</span></span> | <span data-ttu-id="3c2dd-197">Принятый заголовок версии</span><span class="sxs-lookup"><span data-stu-id="3c2dd-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c2dd-198">.NET</span><span class="sxs-lookup"><span data-stu-id="3c2dd-198">.NET</span></span> |[<span data-ttu-id="3c2dd-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="3c2dd-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="3c2dd-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="3c2dd-200">2.0.0</span></span> |
| <span data-ttu-id="3c2dd-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="3c2dd-201">Node.js</span></span> |[<span data-ttu-id="3c2dd-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="3c2dd-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="3c2dd-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="3c2dd-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="3c2dd-204">Поведение внутренних серверов мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="3c2dd-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="3c2dd-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="3c2dd-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="3c2dd-206">Значение параметра MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="3c2dd-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="3c2dd-207">Ответ</span><span class="sxs-lookup"><span data-stu-id="3c2dd-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c2dd-208">x.y.z или значение NULL</span><span class="sxs-lookup"><span data-stu-id="3c2dd-208">x.y.z or Null</span></span> |<span data-ttu-id="3c2dd-209">Истина</span><span class="sxs-lookup"><span data-stu-id="3c2dd-209">True</span></span> |<span data-ttu-id="3c2dd-210">200 – OK</span><span class="sxs-lookup"><span data-stu-id="3c2dd-210">200 - OK</span></span> |
| <span data-ttu-id="3c2dd-211">Null</span><span class="sxs-lookup"><span data-stu-id="3c2dd-211">Null</span></span> |<span data-ttu-id="3c2dd-212">False/не указан</span><span class="sxs-lookup"><span data-stu-id="3c2dd-212">False/Not Specified</span></span> |<span data-ttu-id="3c2dd-213">400 – неверный запрос</span><span class="sxs-lookup"><span data-stu-id="3c2dd-213">400 - Bad Request</span></span> |
| <span data-ttu-id="3c2dd-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="3c2dd-214">1.x.y</span></span> |<span data-ttu-id="3c2dd-215">False/не указан</span><span class="sxs-lookup"><span data-stu-id="3c2dd-215">False/Not Specified</span></span> |<span data-ttu-id="3c2dd-216">400 – неверный запрос</span><span class="sxs-lookup"><span data-stu-id="3c2dd-216">400 - Bad Request</span></span> |
| <span data-ttu-id="3c2dd-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="3c2dd-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="3c2dd-218">False/не указан</span><span class="sxs-lookup"><span data-stu-id="3c2dd-218">False/Not Specified</span></span> |<span data-ttu-id="3c2dd-219">200 – OK</span><span class="sxs-lookup"><span data-stu-id="3c2dd-219">200 - OK</span></span> |
| <span data-ttu-id="3c2dd-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="3c2dd-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="3c2dd-221">False/не указан</span><span class="sxs-lookup"><span data-stu-id="3c2dd-221">False/Not Specified</span></span> |<span data-ttu-id="3c2dd-222">400 – неверный запрос</span><span class="sxs-lookup"><span data-stu-id="3c2dd-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3c2dd-223">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c2dd-223">Next Steps</span></span>
* <span data-ttu-id="3c2dd-224">[Перенос существующей мобильной службы Azure в службу приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="3c2dd-224">[Migrate a Mobile Service to Azure App Service]</span></span>

<span data-ttu-id="3c2dd-225">[Клиенты мобильных служб]: #MobileServicesClients</span><span class="sxs-lookup"><span data-stu-id="3c2dd-225">[Mobile Services clients]: #MobileServicesClients</span></span>
<span data-ttu-id="3c2dd-226">[Клиенты мобильных приложений]: #MobileAppsClients</span><span class="sxs-lookup"><span data-stu-id="3c2dd-226">[Mobile Apps clients]: #MobileAppsClients</span></span>


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
<span data-ttu-id="3c2dd-227">[Перенос существующей мобильной службы Azure в службу приложений Azure]: app-service-mobile-migrating-from-mobile-services.md</span><span class="sxs-lookup"><span data-stu-id="3c2dd-227">[Migrate a Mobile Service to Azure App Service]: app-service-mobile-migrating-from-mobile-services.md</span></span>
