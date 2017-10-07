---
title: "aaaImplement аварийного восстановления с помощью резервного копирования и восстановления в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toouse резервного копирования и восстановления tooperform аварийного восстановления в Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="38164-103">Как tooimplement аварийного восстановления с помощью службы резервного копирования и восстановления в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="38164-103">How tooimplement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="38164-104">Путем выбора toopublish и управлять собственные интерфейсы API через API управления Azure, вы пользуетесь преимуществами многие ошибки отказоустойчивость и инфраструктуры, в противном случае пришлось бы toodesign, реализации и управления.</span><span class="sxs-lookup"><span data-stu-id="38164-104">By choosing toopublish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have toodesign, implement, and manage.</span></span> <span data-ttu-id="38164-105">Hello платформы Azure уменьшает большую часть потенциальных сбоев в малую долю стоимости hello.</span><span class="sxs-lookup"><span data-stu-id="38164-105">hello Azure platform mitigates a large fraction of potential failures at a fraction of hello cost.</span></span>

<span data-ttu-id="38164-106">размещенные toorecover от доступности проблем, влияющих на hello регион, где служба управления API вы должно быть готово tooreconstitute службы в другом регионе, в любое время.</span><span class="sxs-lookup"><span data-stu-id="38164-106">toorecover from availability problems affecting hello region where your API Management service is hosted you should be ready tooreconstitute your service in a different region at any time.</span></span> <span data-ttu-id="38164-107">В зависимости от целей доступности и цель времени восстановления может требуется tooreserve службы резервного копирования в одной или несколькими областями и повторите toomaintain своей конфигурации и содержимого в соответствии с hello активной службы.</span><span class="sxs-lookup"><span data-stu-id="38164-107">Depending on your availability goals and recovery time objective  you might want tooreserve a backup service in one or more regions and try toomaintain their configuration and content in sync with hello active service.</span></span> <span data-ttu-id="38164-108">резервное копирование службы Hello и функция восстановления предоставляет необходимые стандартного блока hello для реализации стратегии аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="38164-108">hello service backup and restore feature provides hello necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="38164-109">В этом руководстве показано, как запросы tooauthenticate диспетчера ресурсов Azure и как toobackup и восстановлении экземпляров служб управления API.</span><span class="sxs-lookup"><span data-stu-id="38164-109">This guide shows how tooauthenticate Azure Resource Manager requests, and how toobackup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="38164-110">Hello процесс резервного копирования и восстановления экземпляра службы управления API для аварийного восстановления можно использовать также для репликации экземпляров службы управления API для сценариев, например промежуточного хранения.</span><span class="sxs-lookup"><span data-stu-id="38164-110">hello process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="38164-111">Обратите внимание, что срок действия каждой резервной копии истекает через 30 дней.</span><span class="sxs-lookup"><span data-stu-id="38164-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="38164-112">При попытке toorestore резервной копии hello 30-дневный срок действия которого истек, hello восстановление с `Cannot restore: backup expired` сообщения.</span><span class="sxs-lookup"><span data-stu-id="38164-112">If you attempt toorestore a backup after hello 30 day expiration period has expired, hello restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="38164-113">Проверка подлинности запросов к диспетчеру ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="38164-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="38164-114">Hello API REST для резервного копирования и восстановления использует диспетчера ресурсов Azure и содержит другой механизм проверки подлинности, чем hello API-интерфейс REST управления API управления сущностей.</span><span class="sxs-lookup"><span data-stu-id="38164-114">hello REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than hello REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="38164-115">Hello в этом разделе описывается, каким образом запросы tooauthenticate диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="38164-115">hello steps in this section describe how tooauthenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="38164-116">Дополнительные сведения см. в [справочнике REST API Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="38164-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="38164-117">Все hello задачи, выполняемые с ресурсами с помощью диспетчера ресурсов Azure hello должен пройти проверку подлинности в Azure Active Directory с помощью hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="38164-117">All of hello tasks that you do on resources using hello Azure Resource Manager must be authenticated with Azure Active Directory using hello following steps.</span></span>

* <span data-ttu-id="38164-118">Добавление клиента Azure Active Directory toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="38164-118">Add an application toohello Azure Active Directory tenant.</span></span>
* <span data-ttu-id="38164-119">Разрешения для приложения hello, который был добавлен.</span><span class="sxs-lookup"><span data-stu-id="38164-119">Set permissions for hello application that you added.</span></span>
* <span data-ttu-id="38164-120">Получите токен hello для проверки подлинности запросов tooAzure диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="38164-120">Get hello token for authenticating requests tooAzure Resource Manager.</span></span>

<span data-ttu-id="38164-121">Hello первым шагом является toocreate приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="38164-121">hello first step is toocreate an Azure Active Directory application.</span></span> <span data-ttu-id="38164-122">Войти в hello [классический портал Azure](http://manage.windowsazure.com/) hello подписку, которая содержит службу управления API с помощью экземпляра и перейдите toohello **приложений** вкладка по умолчанию, Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="38164-122">Log into hello [Azure Classic Portal](http://manage.windowsazure.com/) using hello subscription that contains your API Management service instance and navigate toohello **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="38164-123">Если каталог по умолчанию hello Azure Active Directory не видны tooyour учетной записи, обратитесь в службу hello администратор hello toogrant hello подписки Azure требуется учетной записи разрешения tooyour.</span><span class="sxs-lookup"><span data-stu-id="38164-123">If hello Azure Active Directory default directory is not visible tooyour account, contact hello administrator of hello Azure subscription toogrant hello required permissions tooyour account.</span></span>

![Создание приложения Azure Active Directory][api-management-add-aad-application]

<span data-ttu-id="38164-125">Щелкните **Добавить**, выберите **Добавить приложение, разрабатываемое моей организацией**, а затем — **Собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="38164-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="38164-126">Введите описательное имя и нажмите стрелку hello.</span><span class="sxs-lookup"><span data-stu-id="38164-126">Enter a descriptive name, and click hello next arrow.</span></span> <span data-ttu-id="38164-127">Введите URL-адрес заполнителя, например `http://resources` для hello **URI перенаправления**, как это поле является обязательным, но значение hello не будет использоваться позднее.</span><span class="sxs-lookup"><span data-stu-id="38164-127">Enter a placeholder URL such as `http://resources` for hello **Redirect URI**, as it is a required field, but hello value is not used later.</span></span> <span data-ttu-id="38164-128">Щелкните приложение hello toosave флажок hello.</span><span class="sxs-lookup"><span data-stu-id="38164-128">Click hello check box toosave hello application.</span></span>

<span data-ttu-id="38164-129">После сохранения приложения hello, нажмите кнопку **Настройка**, прокрутите вниз toohello **разрешения приложений tooother** и нажмите кнопку **добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="38164-129">Once hello application is saved, click **Configure**, scroll down toohello **permissions tooother applications** section, and click **Add application**.</span></span>

![Добавление разрешений][api-management-aad-permissions-add]

<span data-ttu-id="38164-131">Выберите **Windows** **API управления службами Azure** и выберите приложение hello tooadd флажок hello.</span><span class="sxs-lookup"><span data-stu-id="38164-131">Select **Windows** **Azure Service Management API** and click hello checkbox tooadd hello application.</span></span>

![Добавление разрешений][api-management-aad-permissions]

<span data-ttu-id="38164-133">Нажмите кнопку **делегированные разрешения** рядом с добавленным hello **Windows** **API управления службами Azure** приложения hello флажок для **доступ к Azure Управление службами (Предварительная версия)**и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="38164-133">Click **Delegated Permissions** beside hello newly added **Windows** **Azure Service Management API** application, check hello box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Добавление разрешений][api-management-aad-delegated-permissions]

<span data-ttu-id="38164-135">Hello предыдущих tooinvoking API-интерфейсы для создания hello резервного копирования и восстановления, необходимые tooget маркер.</span><span class="sxs-lookup"><span data-stu-id="38164-135">Prior tooinvoking hello APIs that generate hello backup and restore it, it is necessary tooget a token.</span></span> <span data-ttu-id="38164-136">Hello следующий пример использует hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) токен hello tooretrieve пакета nuget.</span><span class="sxs-lookup"><span data-stu-id="38164-136">hello following example uses hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package tooretrieve hello token.</span></span>

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="38164-137">Замените `{tentand id}`, `{application id}`, и `{redirect uri}` с помощью hello, следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="38164-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using hello following instructions.</span></span>

<span data-ttu-id="38164-138">Замените `{tenant id}` с идентификатором клиента hello hello приложения Azure Active Directory, вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="38164-138">Replace `{tenant id}` with hello tenant id of hello Azure Active Directory application you just created.</span></span> <span data-ttu-id="38164-139">Идентификатор hello можно открыть, щелкнув **просмотреть конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="38164-139">You can access hello id by clicking **View endpoints**.</span></span>

![Endpoints][api-management-aad-default-directory]

![Endpoints][api-management-endpoint]

<span data-ttu-id="38164-142">Замените `{application id}` и `{redirect uri}` с помощью hello **идентификатор клиента** и hello URL-адрес из hello **URI перенаправления** раздела из приложения Azure Active Directory **Настройка**  вкладки.</span><span class="sxs-lookup"><span data-stu-id="38164-142">Replace `{application id}` and `{redirect uri}` using hello **Client Id** and  hello URL from hello **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Ресурсы][api-management-aad-resources]

<span data-ttu-id="38164-144">После hello значения указаны, пример кода hello должен вернуться маркера аналогичные toohello, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="38164-144">Once hello values are specified, hello code example should return a token similar toohello following example.</span></span>

![Маркер][api-management-arm-token]

<span data-ttu-id="38164-146">Перед вызовом hello резервного копирования и восстановления операции, описанные в следующих разделах hello, задайте заголовок запроса hello авторизации для своего вызова REST.</span><span class="sxs-lookup"><span data-stu-id="38164-146">Before calling hello backup and restore operations described in hello following sections, set hello authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="38164-147"><a name="step1"> </a>Архивация службы управления API</span><span class="sxs-lookup"><span data-stu-id="38164-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="38164-148">tooback копирование hello проблемы службы управления API, следующие HTTP-запроса:</span><span class="sxs-lookup"><span data-stu-id="38164-148">tooback up an API Management service issue hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="38164-149">Описание:</span><span class="sxs-lookup"><span data-stu-id="38164-149">where:</span></span>

* <span data-ttu-id="38164-150">`subscriptionId`— идентификатор подписки hello, содержащего службу управления API hello, вы пытаетесь toobackup</span><span class="sxs-lookup"><span data-stu-id="38164-150">`subscriptionId` - id of hello subscription containing hello API Management service you are attempting toobackup</span></span>
* <span data-ttu-id="38164-151">`resourceGroupName`-Строка в форме «Api - по умолчанию — {региона службы}» hello где `service-region` идентифицирует hello регион Azure, где размещена служба управления API, которые вы пытаетесь toobackup hello, например`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="38164-151">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are trying toobackup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="38164-152">`serviceName`-Имя hello hello службы управления API, создании резервной копии указан во время его создания hello</span><span class="sxs-lookup"><span data-stu-id="38164-152">`serviceName` - hello name of hello API Management service you are making a backup of specified at hello time of its creation</span></span>
* <span data-ttu-id="38164-153">`api-version` замените `2014-02-14`.</span><span class="sxs-lookup"><span data-stu-id="38164-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="38164-154">В тексте hello hello запроса укажите имя учетной записи хранилища Azure целевой hello, ключ доступа, имя контейнера BLOB-объекта и имя архива:</span><span class="sxs-lookup"><span data-stu-id="38164-154">In hello body of hello request, specify hello target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="38164-155">Задайте значение hello hello `Content-Type` заголовок запроса слишком`application/json`.</span><span class="sxs-lookup"><span data-stu-id="38164-155">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="38164-156">Резервная копия — это длительная операция, может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="38164-156">Backup is a long running operation that may take multiple minutes toocomplete.</span></span>  <span data-ttu-id="38164-157">Если hello запрос выполнен успешно, и была инициирована hello процесс резервного копирования вы получите `202 Accepted` код состояния ответа с `Location` заголовок.</span><span class="sxs-lookup"><span data-stu-id="38164-157">If hello request was successful and hello backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="38164-158">Создание «GET» запрашивает toohello URL-адрес в hello `Location` toofind заголовок hello состояние операции hello.</span><span class="sxs-lookup"><span data-stu-id="38164-158">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="38164-159">Во время резервного копирования hello tooreceive код состояния 202 Accepted будет продолжено.</span><span class="sxs-lookup"><span data-stu-id="38164-159">While hello backup is in progress you will continue tooreceive a '202 Accepted' status code.</span></span> <span data-ttu-id="38164-160">Код ответа `200 OK` покажет успешного завершения операции резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="38164-160">A Response code of `200 OK` will indicate successful completion of hello backup operation.</span></span>

<span data-ttu-id="38164-161">Следует учитывать следующие ограничения при выполнении резервного копирования запроса hello.</span><span class="sxs-lookup"><span data-stu-id="38164-161">Please note hello following constraints when making a backup request.</span></span>

* <span data-ttu-id="38164-162">**Контейнер** указан в тексте запроса hello **должен существовать**.</span><span class="sxs-lookup"><span data-stu-id="38164-162">**Container** specified in hello request body **must exist**.</span></span>
* <span data-ttu-id="38164-163">Пока выполняется резервное копирование, **не предпринимайте никаких действий по управлению службами**, таких как повышение или понижение уровня SKU, смена доменного имени и т. д.</span><span class="sxs-lookup"><span data-stu-id="38164-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="38164-164">Восстановление **резервного копирования гарантируется только в течение 30 дней** с момента hello момент его создания.</span><span class="sxs-lookup"><span data-stu-id="38164-164">Restore of a **backup is guaranteed only for 30 days** since hello moment of its creation.</span></span>
* <span data-ttu-id="38164-165">**Данные об использовании** используется для создания отчетов аналитики **не включено** hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="38164-165">**Usage data** used for creating analytics reports **is not included** in hello backup.</span></span> <span data-ttu-id="38164-166">Используйте [API REST управления API Azure] [ Azure API Management REST API] tooperiodically извлечь аналитика отчеты для длительного хранения.</span><span class="sxs-lookup"><span data-stu-id="38164-166">Use [Azure API Management REST API][Azure API Management REST API] tooperiodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="38164-167">Hello частоту, с которой создавать резервные копии службы будет влиять на вашей цели точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="38164-167">hello frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="38164-168">его мы рекомендуем регулярного создания резервных копий, а также для выполнения резервного копирования по запросу после внесения важных toominimize изменяет tooyour службы управления API.</span><span class="sxs-lookup"><span data-stu-id="38164-168">toominimize it we advise implementing regular backups as well as performing on-demand backups after making important changes tooyour API Management service.</span></span>
* <span data-ttu-id="38164-169">**Изменения** сделан toohello конфигурации службы (например, API-интерфейсы, политики, внешний вид портала разработчиков) во время операции резервного копирования находится в процессе **не могут быть включены в резервную копию hello и поэтому будут потеряны**.</span><span class="sxs-lookup"><span data-stu-id="38164-169">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in hello backup and therefore will be lost**.</span></span>

## <span data-ttu-id="38164-170"><a name="step2"> </a>Восстановление службы управления API</span><span class="sxs-lookup"><span data-stu-id="38164-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="38164-171">toorestore службу управления API из ранее созданной резервной копии внести hello, выполнив HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="38164-171">toorestore an API Management service from a previously created backup make hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="38164-172">Описание:</span><span class="sxs-lookup"><span data-stu-id="38164-172">where:</span></span>

* <span data-ttu-id="38164-173">`subscriptionId`— идентификатор подписки hello, содержащий восстановлении резервной копии в службе управления API hello</span><span class="sxs-lookup"><span data-stu-id="38164-173">`subscriptionId` - id of hello subscription containing hello API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="38164-174">`resourceGroupName`-Строка в форме «Api - по умолчанию — {региона службы}» hello где `service-region` идентифицирует hello регион Azure, где размещается hello восстановлении резервной копии в службе управления API, например`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="38164-174">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="38164-175">`serviceName`-Имя hello hello во время его создания hello. Указанная служба выполняется восстановление в службе управления API</span><span class="sxs-lookup"><span data-stu-id="38164-175">`serviceName` - hello name of hello API Management service being restored into specified at hello time of its creation</span></span>
* <span data-ttu-id="38164-176">`api-version` замените `2014-02-14`.</span><span class="sxs-lookup"><span data-stu-id="38164-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="38164-177">В тексте hello hello запроса укажите расположение файла резервной копии hello, т. е. имя учетной записи хранилища Azure, ключ доступа, имя контейнера BLOB-объекта и имя архива:</span><span class="sxs-lookup"><span data-stu-id="38164-177">In hello body of hello request, specify hello backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="38164-178">Задайте значение hello hello `Content-Type` заголовок запроса слишком`application/json`.</span><span class="sxs-lookup"><span data-stu-id="38164-178">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="38164-179">Восстановление проводится длительная операция, которая может занять до too30 или дополнительные toocomplete минут.</span><span class="sxs-lookup"><span data-stu-id="38164-179">Restore is a long running operation that may take up too30 or more minutes toocomplete.</span></span>  <span data-ttu-id="38164-180">Если hello запрос выполнен успешно, и процесс восстановления hello была инициирована вы получите `202 Accepted` код состояния ответа с `Location` заголовок.</span><span class="sxs-lookup"><span data-stu-id="38164-180">If hello request was successful and hello restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="38164-181">Создание «GET» запрашивает toohello URL-адрес в hello `Location` toofind заголовок hello состояние операции hello.</span><span class="sxs-lookup"><span data-stu-id="38164-181">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="38164-182">Во время восстановления hello код состояния "202 принято» tooreceive будет продолжено.</span><span class="sxs-lookup"><span data-stu-id="38164-182">While hello restore is in progress you will continue tooreceive '202 Accepted' status code.</span></span> <span data-ttu-id="38164-183">Код ответа `200 OK` покажет успешного завершения операции восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="38164-183">A response code of `200 OK` will indicate successful completion of hello restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38164-184">**Hello SKU** службы hello, восстанавливаемой в **должно соответствовать** hello SKU hello резервная копия службы выполняется восстановление.</span><span class="sxs-lookup"><span data-stu-id="38164-184">**hello SKU** of hello service being restored into **must match** hello SKU of hello backed up service being restored.</span></span>
>
> <span data-ttu-id="38164-185">**Изменения** сделан toohello конфигурации службы (например, API-интерфейсы, политики, внешний вид портала разработчиков) во время операции восстановления идет **, могут быть заменены**.</span><span class="sxs-lookup"><span data-stu-id="38164-185">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="38164-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="38164-186">Next steps</span></span>
<span data-ttu-id="38164-187">Извлечь hello, следуя блогов Майкрософт для двух разных пошаговых hello процесса резервного копирования и восстановления.</span><span class="sxs-lookup"><span data-stu-id="38164-187">Check out hello following Microsoft blogs for two different walkthroughs of hello backup/restore process.</span></span>

* [<span data-ttu-id="38164-188">Репликация учетных записей управления API Azure</span><span class="sxs-lookup"><span data-stu-id="38164-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="38164-189">Благодарим вас tooGisela для статьи toothis свой вклад.</span><span class="sxs-lookup"><span data-stu-id="38164-189">Thank you tooGisela for her contribution toothis article.</span></span>
* [<span data-ttu-id="38164-190">Управление API Azure: резервное копирование и восстановление конфигурации</span><span class="sxs-lookup"><span data-stu-id="38164-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="38164-191">Подробные с Стюарт подход Hello не соответствует hello официальные рекомендации, но очень интересно.</span><span class="sxs-lookup"><span data-stu-id="38164-191">hello approach detailed by Stuart does not match hello official guidance but it is very interesting.</span></span>

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
