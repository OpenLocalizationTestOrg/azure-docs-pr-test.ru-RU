---
title: "Управление версиями пакета SDK aaaClient и сервера в мобильные приложения и мобильные службы | Документы Microsoft"
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
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="d174d-103">Управление версиями клиента и сервера в мобильных приложениях и мобильных службах</span><span class="sxs-lookup"><span data-stu-id="d174d-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="d174d-104">последнюю версию Hello мобильных служб Azure — hello **мобильные приложения** функции службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="d174d-104">hello latest version of Azure Mobile Services is hello **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="d174d-105">Здравствуйте, мобильные приложения клиента и пакеты SDK сервера изначально основаны на их в мобильных службах, но это *не* совместимы друг с другом.</span><span class="sxs-lookup"><span data-stu-id="d174d-105">hello Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="d174d-106">Другими словами, пакет SDK клиента *мобильных приложений* необходимо использовать с пакетом SDK сервера *мобильных приложений* (точно так же и для *мобильных служб*).</span><span class="sxs-lookup"><span data-stu-id="d174d-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="d174d-107">Этот контракт достигается посредством значение специальный заголовок используется hello клиентские и серверные пакеты SDK, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="d174d-107">This contract is enforced through a special header value used by hello client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="d174d-108">Примечание: каждый раз, когда этот документ относится tooa *мобильных служб* серверной части, она не должна обязательно toobe, размещенных на мобильных служб.</span><span class="sxs-lookup"><span data-stu-id="d174d-108">Note: whenever this document refers tooa *Mobile Services* backend, it does not necessarily need toobe hosted on Mobile Services.</span></span> <span data-ttu-id="d174d-109">Теперь стало возможно toomigrate toorun мобильной службы в службе приложений без необходимости изменения кода, но по-прежнему будет использоваться служба hello *мобильных служб* версии пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="d174d-109">It is now possible toomigrate a mobile service toorun on App Service without any code changes, but hello service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="d174d-110">Дополнительные сведения о toolearn миграция tooApp службы без необходимости изменения кода, см. в статье hello [миграции мобильной службы tooAzure службы приложений].</span><span class="sxs-lookup"><span data-stu-id="d174d-110">toolearn more about migrating tooApp Service without any code changes, see hello article [Migrate a Mobile Service tooAzure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="d174d-111">Спецификация заголовка</span><span class="sxs-lookup"><span data-stu-id="d174d-111">Header specification</span></span>
<span data-ttu-id="d174d-112">ключ Hello `ZUMO-API-VERSION` могут быть указаны в hello HTTP-заголовок или строку запроса hello.</span><span class="sxs-lookup"><span data-stu-id="d174d-112">hello key `ZUMO-API-VERSION` may be specified in either hello HTTP header or hello query string.</span></span> <span data-ttu-id="d174d-113">значение Hello — строка версии в виде hello **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="d174d-113">hello value is a version string in hello form **x.y.z**.</span></span>

<span data-ttu-id="d174d-114">Например:</span><span class="sxs-lookup"><span data-stu-id="d174d-114">For example:</span></span>

<span data-ttu-id="d174d-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="d174d-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="d174d-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d174d-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="d174d-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d174d-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="d174d-118">Отказ от проверки версий</span><span class="sxs-lookup"><span data-stu-id="d174d-118">Opting out of version checking</span></span>
<span data-ttu-id="d174d-119">Можно отключить проверку, задав значение версии **true** для параметра приложения hello **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="d174d-119">You can opt out of version checking by setting a value of **true** for hello app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="d174d-120">Укажите это в файл web.config, либо в составе hello раздел параметров приложения hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d174d-120">Specify this either in your web.config or in hello Application Settings section of hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d174d-121">Существует несколько изменений в поведении между мобильными службами и мобильные приложения, особенно в областях hello автономной синхронизации, проверки подлинности и push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="d174d-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in hello areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="d174d-122">Только следует отказаться проверку после завершения тестирования tooensure, не нарушают эти изменения поведения приложения его функциональность версии.</span><span class="sxs-lookup"><span data-stu-id="d174d-122">You should only opt out of version checking after complete testing tooensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="d174d-123">Сводные сведения о совместимости для всех версий</span><span class="sxs-lookup"><span data-stu-id="d174d-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="d174d-124">Hello представленной ниже диаграмме показаны hello совместимость всех типов клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="d174d-124">hello chart below shows hello compatibility between all client and server types.</span></span> <span data-ttu-id="d174d-125">Серверной части, классифицируется как либо Mobile **службы** или Mobile **приложений** на основе hello server SDK, который его использует.</span><span class="sxs-lookup"><span data-stu-id="d174d-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on hello server SDK that it uses.</span></span>

|  | <span data-ttu-id="d174d-126">**мобильных служб** </span><span class="sxs-lookup"><span data-stu-id="d174d-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="d174d-127">**Мобильные приложения** </span><span class="sxs-lookup"><span data-stu-id="d174d-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d174d-128">[Клиенты мобильных служб]</span><span class="sxs-lookup"><span data-stu-id="d174d-128">[Mobile Services clients]</span></span> |<span data-ttu-id="d174d-129">кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="d174d-129">Ok</span></span> |<span data-ttu-id="d174d-130">Ошибка\*</span><span class="sxs-lookup"><span data-stu-id="d174d-130">Error\*</span></span> |
| <span data-ttu-id="d174d-131">[Клиенты мобильных приложений]</span><span class="sxs-lookup"><span data-stu-id="d174d-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="d174d-132">Ошибка\*</span><span class="sxs-lookup"><span data-stu-id="d174d-132">Error\*</span></span> |<span data-ttu-id="d174d-133">кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="d174d-133">Ok</span></span> |

<span data-ttu-id="d174d-134">\*Это поведение можно изменить, указав параметр **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="d174d-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="d174d-135"><a name="1.0.0"></a>Клиент и сервер мобильных служб</span><span class="sxs-lookup"><span data-stu-id="d174d-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="d174d-136">Hello клиентских SDK в следующей таблице hello совместимы с **мобильных служб**.</span><span class="sxs-lookup"><span data-stu-id="d174d-136">hello client SDKs in hello table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="d174d-137">Примечание: hello SDK клиента мобильных служб *не* отправлять значение заголовка для `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="d174d-137">Note: hello Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="d174d-138">Если служба hello получает этот заголовок или значение строки запроса, будет возвращена ошибка, если не был явно указан параметр out, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="d174d-138">If hello service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="d174d-139"><a name="MobileServicesClients"></a> Пакеты SDK для клиента мобильных *служб*</span><span class="sxs-lookup"><span data-stu-id="d174d-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="d174d-140">Платформа клиента</span><span class="sxs-lookup"><span data-stu-id="d174d-140">Client platform</span></span> | <span data-ttu-id="d174d-141">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="d174d-141">Version</span></span> | <span data-ttu-id="d174d-142">Значение заголовка версии</span><span class="sxs-lookup"><span data-stu-id="d174d-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d174d-143">Управляемый клиент (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="d174d-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="d174d-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="d174d-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="d174d-145">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d174d-145">n/a</span></span> |
| <span data-ttu-id="d174d-146">iOS</span><span class="sxs-lookup"><span data-stu-id="d174d-146">iOS</span></span> |[<span data-ttu-id="d174d-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="d174d-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="d174d-148">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d174d-148">n/a</span></span> |
| <span data-ttu-id="d174d-149">Android</span><span class="sxs-lookup"><span data-stu-id="d174d-149">Android</span></span> |[<span data-ttu-id="d174d-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="d174d-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="d174d-151">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d174d-151">n/a</span></span> |
| <span data-ttu-id="d174d-152">HTML</span><span class="sxs-lookup"><span data-stu-id="d174d-152">HTML</span></span> |[<span data-ttu-id="d174d-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="d174d-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="d174d-154">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d174d-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="d174d-155">Пакеты SDK для сервера мобильных *служб*</span><span class="sxs-lookup"><span data-stu-id="d174d-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="d174d-156">Платформа сервера</span><span class="sxs-lookup"><span data-stu-id="d174d-156">Server platform</span></span> | <span data-ttu-id="d174d-157">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="d174d-157">Version</span></span> | <span data-ttu-id="d174d-158">Принятый заголовок версии</span><span class="sxs-lookup"><span data-stu-id="d174d-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d174d-159">.NET</span><span class="sxs-lookup"><span data-stu-id="d174d-159">.NET</span></span> |[<span data-ttu-id="d174d-160">WindowsAzure.MobileServices.Backend.* версия 1.0.x</span><span class="sxs-lookup"><span data-stu-id="d174d-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="d174d-161">** Отсутствует заголовок версии **</span><span class="sxs-lookup"><span data-stu-id="d174d-161">**No version header **</span></span> |
| <span data-ttu-id="d174d-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="d174d-162">Node.js</span></span> |<span data-ttu-id="d174d-163">(ожидается в ближайшее время)</span><span class="sxs-lookup"><span data-stu-id="d174d-163">(coming soon)</span></span> |<span data-ttu-id="d174d-164">**Отсутствует заголовок версии**</span><span class="sxs-lookup"><span data-stu-id="d174d-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="d174d-165">Поведение внутренних серверов мобильных служб</span><span class="sxs-lookup"><span data-stu-id="d174d-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="d174d-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="d174d-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="d174d-167">Значение параметра MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="d174d-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="d174d-168">Ответ</span><span class="sxs-lookup"><span data-stu-id="d174d-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d174d-169">Не указан</span><span class="sxs-lookup"><span data-stu-id="d174d-169">Not specified</span></span> |<span data-ttu-id="d174d-170">Любой</span><span class="sxs-lookup"><span data-stu-id="d174d-170">Any</span></span> |<span data-ttu-id="d174d-171">200 – OK</span><span class="sxs-lookup"><span data-stu-id="d174d-171">200 - OK</span></span> |
| <span data-ttu-id="d174d-172">Любое значение</span><span class="sxs-lookup"><span data-stu-id="d174d-172">Any value</span></span> |<span data-ttu-id="d174d-173">Истина</span><span class="sxs-lookup"><span data-stu-id="d174d-173">True</span></span> |<span data-ttu-id="d174d-174">200 – OK</span><span class="sxs-lookup"><span data-stu-id="d174d-174">200 - OK</span></span> |
| <span data-ttu-id="d174d-175">Любое значение</span><span class="sxs-lookup"><span data-stu-id="d174d-175">Any value</span></span> |<span data-ttu-id="d174d-176">False/не указан</span><span class="sxs-lookup"><span data-stu-id="d174d-176">False/Not Specified</span></span> |<span data-ttu-id="d174d-177">400 – неверный запрос</span><span class="sxs-lookup"><span data-stu-id="d174d-177">400 - Bad Request</span></span> |

## <span data-ttu-id="d174d-178"><a name="2.0.0"></a>Клиент и сервер мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="d174d-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="d174d-179"><a name="MobileAppsClients"></a> Пакеты SDK для клиента мобильных *приложений*</span><span class="sxs-lookup"><span data-stu-id="d174d-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="d174d-180">Проверка версий была введена в следующие версии пакета SDK клиента hello hello для **мобильных приложений Azure**:</span><span class="sxs-lookup"><span data-stu-id="d174d-180">Version checking was introduced starting with hello following versions of hello client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="d174d-181">Платформа клиента</span><span class="sxs-lookup"><span data-stu-id="d174d-181">Client platform</span></span> | <span data-ttu-id="d174d-182">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="d174d-182">Version</span></span> | <span data-ttu-id="d174d-183">Значение заголовка версии</span><span class="sxs-lookup"><span data-stu-id="d174d-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d174d-184">Управляемый клиент (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="d174d-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="d174d-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d174d-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="d174d-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d174d-186">2.0.0</span></span> |
| <span data-ttu-id="d174d-187">iOS</span><span class="sxs-lookup"><span data-stu-id="d174d-187">iOS</span></span> |[<span data-ttu-id="d174d-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="d174d-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="d174d-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d174d-189">2.0.0</span></span> |
| <span data-ttu-id="d174d-190">Android</span><span class="sxs-lookup"><span data-stu-id="d174d-190">Android</span></span> |[<span data-ttu-id="d174d-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="d174d-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="d174d-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="d174d-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="d174d-193">Пакеты SDK для сервера мобильных *приложений*</span><span class="sxs-lookup"><span data-stu-id="d174d-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="d174d-194">Проверка версий входит в состав следующих версий пакета SDK сервера:</span><span class="sxs-lookup"><span data-stu-id="d174d-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="d174d-195">Платформа сервера</span><span class="sxs-lookup"><span data-stu-id="d174d-195">Server platform</span></span> | <span data-ttu-id="d174d-196">SDK</span><span class="sxs-lookup"><span data-stu-id="d174d-196">SDK</span></span> | <span data-ttu-id="d174d-197">Принятый заголовок версии</span><span class="sxs-lookup"><span data-stu-id="d174d-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d174d-198">.NET</span><span class="sxs-lookup"><span data-stu-id="d174d-198">.NET</span></span> |[<span data-ttu-id="d174d-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="d174d-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="d174d-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d174d-200">2.0.0</span></span> |
| <span data-ttu-id="d174d-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="d174d-201">Node.js</span></span> |[<span data-ttu-id="d174d-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="d174d-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="d174d-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d174d-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="d174d-204">Поведение внутренних серверов мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="d174d-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="d174d-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="d174d-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="d174d-206">Значение параметра MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="d174d-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="d174d-207">Ответ</span><span class="sxs-lookup"><span data-stu-id="d174d-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d174d-208">x.y.z или значение NULL</span><span class="sxs-lookup"><span data-stu-id="d174d-208">x.y.z or Null</span></span> |<span data-ttu-id="d174d-209">Истина</span><span class="sxs-lookup"><span data-stu-id="d174d-209">True</span></span> |<span data-ttu-id="d174d-210">200 – OK</span><span class="sxs-lookup"><span data-stu-id="d174d-210">200 - OK</span></span> |
| <span data-ttu-id="d174d-211">Null</span><span class="sxs-lookup"><span data-stu-id="d174d-211">Null</span></span> |<span data-ttu-id="d174d-212">False/не указан</span><span class="sxs-lookup"><span data-stu-id="d174d-212">False/Not Specified</span></span> |<span data-ttu-id="d174d-213">400 – неверный запрос</span><span class="sxs-lookup"><span data-stu-id="d174d-213">400 - Bad Request</span></span> |
| <span data-ttu-id="d174d-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="d174d-214">1.x.y</span></span> |<span data-ttu-id="d174d-215">False/не указан</span><span class="sxs-lookup"><span data-stu-id="d174d-215">False/Not Specified</span></span> |<span data-ttu-id="d174d-216">400 – неверный запрос</span><span class="sxs-lookup"><span data-stu-id="d174d-216">400 - Bad Request</span></span> |
| <span data-ttu-id="d174d-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="d174d-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="d174d-218">False/не указан</span><span class="sxs-lookup"><span data-stu-id="d174d-218">False/Not Specified</span></span> |<span data-ttu-id="d174d-219">200 – OK</span><span class="sxs-lookup"><span data-stu-id="d174d-219">200 - OK</span></span> |
| <span data-ttu-id="d174d-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="d174d-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="d174d-221">False/не указан</span><span class="sxs-lookup"><span data-stu-id="d174d-221">False/Not Specified</span></span> |<span data-ttu-id="d174d-222">400 – неверный запрос</span><span class="sxs-lookup"><span data-stu-id="d174d-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d174d-223">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d174d-223">Next Steps</span></span>
* <span data-ttu-id="d174d-224">[миграции мобильной службы tooAzure службы приложений]</span><span class="sxs-lookup"><span data-stu-id="d174d-224">[Migrate a Mobile Service tooAzure App Service]</span></span>

[Клиенты мобильных служб]: #MobileServicesClients
[Клиенты мобильных приложений]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[миграции мобильной службы tooAzure службы приложений]: app-service-mobile-migrating-from-mobile-services.md
