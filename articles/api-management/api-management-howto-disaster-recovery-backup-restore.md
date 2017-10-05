---
title: "Внедрение аварийного восстановления с помощью функций архивации и восстановления в службе управления API Azure | Документация Майкрософт"
description: "Использование архивации и восстановления для выполнения аварийного восстановления в службе управления API Azure."
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
ms.openlocfilehash: 07c0265490cfae733133b6e0c938f90f9b392da4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="d33eb-103">Реализация аварийного восстановления с помощью функций резервного копирования и восстановления службы в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="d33eb-103">How to implement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="d33eb-104">Выбрав службу Azure API Management для публикации интерфейсов API и управления ими, вы получаете множество возможностей по обеспечению отказоустойчивости и организации инфраструктуры, которые в противном случае вам пришлось бы проектировать и внедрять самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="d33eb-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span></span> <span data-ttu-id="d33eb-105">Платформа Azure устраняет большую часть потенциальных сбоев при относительно небольших затратах.</span><span class="sxs-lookup"><span data-stu-id="d33eb-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span></span>

<span data-ttu-id="d33eb-106">Чтобы обеспечить восстановление в случае проблем с доступностью в регионе, в котором размещена ваша служба API Management, необходимо быть готовым к ее воссозданию в другом регионе в любой момент.</span><span class="sxs-lookup"><span data-stu-id="d33eb-106">To recover from availability problems affecting the region where your API Management service is hosted you should be ready to reconstitute your service in a different region at any time.</span></span> <span data-ttu-id="d33eb-107">В зависимости от целевых показателей доступности и времени восстановления вам, возможно, потребуется создать резервную службу в одном или нескольких регионах, а затем наладить постоянную синхронизацию ее конфигурации и содержимого с активной службой.</span><span class="sxs-lookup"><span data-stu-id="d33eb-107">Depending on your availability goals and recovery time objective  you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span></span> <span data-ttu-id="d33eb-108">Функция резервного копирования и восстановления службы служит необходимым фундаментом для реализации стратегии аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="d33eb-108">The service backup and restore feature provides the necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="d33eb-109">В этом руководстве показано, как проверять подлинность запросов к диспетчеру ресурсов Azure, а также создавать резервные копии экземпляров служб управления API и восстанавливать их.</span><span class="sxs-lookup"><span data-stu-id="d33eb-109">This guide shows how to authenticate Azure Resource Manager requests, and how to backup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="d33eb-110">Процесс резервного копирования и аварийного восстановления экземпляра службы управления API может использоваться для репликации экземпляров службы управления API, например для реализации промежуточного хранения.</span><span class="sxs-lookup"><span data-stu-id="d33eb-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="d33eb-111">Обратите внимание, что срок действия каждой резервной копии истекает через 30 дней.</span><span class="sxs-lookup"><span data-stu-id="d33eb-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="d33eb-112">При попытке восстановления резервной копии по истечении 30 дней восстановление завершится сбоем и будет отображено сообщение `Cannot restore: backup expired`.</span><span class="sxs-lookup"><span data-stu-id="d33eb-112">If you attempt to restore a backup after the 30 day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="d33eb-113">Проверка подлинности запросов к диспетчеру ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="d33eb-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d33eb-114">Интерфейс REST API для резервного копирования и восстановления использует диспетчер ресурсов Azure и применяет механизм проверки подлинности, отличный от интерфейсов REST API, используемых для управления объектами службы управления API.</span><span class="sxs-lookup"><span data-stu-id="d33eb-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="d33eb-115">В этом разделе описываются действия, необходимые для проверки подлинности запросов к диспетчеру ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d33eb-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="d33eb-116">Дополнительные сведения см. в [справочнике REST API Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="d33eb-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="d33eb-117">Все задачи, выполняемые с ресурсами с помощью диспетчера ресурсов Azure, должны пройти проверку подлинности Azure Active Directory. Для этого:</span><span class="sxs-lookup"><span data-stu-id="d33eb-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps.</span></span>

* <span data-ttu-id="d33eb-118">добавьте приложение в клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="d33eb-118">Add an application to the Azure Active Directory tenant.</span></span>
* <span data-ttu-id="d33eb-119">настройте разрешения для добавленного приложения;</span><span class="sxs-lookup"><span data-stu-id="d33eb-119">Set permissions for the application that you added.</span></span>
* <span data-ttu-id="d33eb-120">получите маркер для проверки подлинности запросов к диспетчеру ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d33eb-120">Get the token for authenticating requests to Azure Resource Manager.</span></span>

<span data-ttu-id="d33eb-121">В первую очередь необходимо создать приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33eb-121">The first step is to create an Azure Active Directory application.</span></span> <span data-ttu-id="d33eb-122">Войдите на [классический портал Azure](http://manage.windowsazure.com/) , используя подписку, включающую экземпляр службы управления API, и перейдите на вкладку **Приложения** , чтобы открыть используемый по умолчанию каталог Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33eb-122">Log into the [Azure Classic Portal](http://manage.windowsazure.com/) using the subscription that contains your API Management service instance and navigate to the **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="d33eb-123">Если этот каталог не отображается в вашей учетной записи, обратитесь к администратору подписки Azure, чтобы получить необходимые разрешения для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d33eb-123">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span></span>

![Создание приложения Azure Active Directory][api-management-add-aad-application]

<span data-ttu-id="d33eb-125">Щелкните **Добавить**, выберите **Добавить приложение, разрабатываемое моей организацией**, а затем — **Собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="d33eb-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="d33eb-126">Введите описательное имя и нажмите кнопку «Далее».</span><span class="sxs-lookup"><span data-stu-id="d33eb-126">Enter a descriptive name, and click the next arrow.</span></span> <span data-ttu-id="d33eb-127">Введите в поле **URI перенаправления** любой URL-адрес, например `http://resources`. Это поле является обязательным, но введенное значение впоследствии не используется.</span><span class="sxs-lookup"><span data-stu-id="d33eb-127">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span></span> <span data-ttu-id="d33eb-128">Установите флажок, чтобы сохранить приложение.</span><span class="sxs-lookup"><span data-stu-id="d33eb-128">Click the check box to save the application.</span></span>

<span data-ttu-id="d33eb-129">После того как приложение будет сохранено, щелкните **Настройка**, прокрутите страницу вниз до раздела **Разрешения для других приложений** и нажмите кнопку **Добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="d33eb-129">Once the application is saved, click **Configure**, scroll down to the **permissions to other applications** section, and click **Add application**.</span></span>

![Добавление разрешений][api-management-aad-permissions-add]

<span data-ttu-id="d33eb-131">Выберите **API управления службами** **Microsoft** Azure и установите флажок, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="d33eb-131">Select **Windows** **Azure Service Management API** and click the checkbox to add the application.</span></span>

![Добавление разрешений][api-management-aad-permissions]

<span data-ttu-id="d33eb-133">Щелкните **Делегированные разрешения** рядом с только что добавленным приложением API управления службами **Microsoft** **Azure**, установите флажок **Доступ к управлению службами Azure (предварительная версия)** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d33eb-133">Click **Delegated Permissions** beside the newly added **Windows** **Azure Service Management API** application, check the box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Добавление разрешений][api-management-aad-delegated-permissions]

<span data-ttu-id="d33eb-135">Прежде чем вызывать API, выполняющие резервное копирование и восстановление, необходимо получить маркер.</span><span class="sxs-lookup"><span data-stu-id="d33eb-135">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span></span> <span data-ttu-id="d33eb-136">В следующем примере для получения маркера используется пакет NuGet [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) .</span><span class="sxs-lookup"><span data-stu-id="d33eb-136">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package to retrieve the token.</span></span>

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
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="d33eb-137">Замените `{tentand id}`, `{application id}` и `{redirect uri}`, следуя приведенным инструкциям.</span><span class="sxs-lookup"><span data-stu-id="d33eb-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions.</span></span>

<span data-ttu-id="d33eb-138">Замените `{tenant id}` на идентификатор клиента для приложения Azure Active Directory, которое вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="d33eb-138">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you just created.</span></span> <span data-ttu-id="d33eb-139">Чтобы получить доступ к идентификатору, щелкните **Просмотр конечных точек**.</span><span class="sxs-lookup"><span data-stu-id="d33eb-139">You can access the id by clicking **View endpoints**.</span></span>

![Endpoints][api-management-aad-default-directory]

![Endpoints][api-management-endpoint]

<span data-ttu-id="d33eb-142">Замените `{application id}` и `{redirect uri}`, используя **идентификатор клиента** и URL-адрес из раздела **URI перенаправления** на вкладке **Настройка** приложения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d33eb-142">Replace `{application id}` and `{redirect uri}` using the **Client Id** and  the URL from the **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Ресурсы][api-management-aad-resources]

<span data-ttu-id="d33eb-144">Когда все значения будут указаны, код должен вернуть примерно такой маркер:</span><span class="sxs-lookup"><span data-stu-id="d33eb-144">Once the values are specified, the code example should return a token similar to the following example.</span></span>

![Маркер][api-management-arm-token]

<span data-ttu-id="d33eb-146">Прежде чем выполнять операции резервного копирования и восстановления, описанные в следующих разделах, задайте заголовок запроса проверки подлинности для вызова REST.</span><span class="sxs-lookup"><span data-stu-id="d33eb-146">Before calling the backup and restore operations described in the following sections, set the authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="d33eb-147"><a name="step1"> </a>Архивация службы управления API</span><span class="sxs-lookup"><span data-stu-id="d33eb-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="d33eb-148">Чтобы выполнить архивацию службы управления API, отправьте следующий HTTP-запрос:</span><span class="sxs-lookup"><span data-stu-id="d33eb-148">To back up an API Management service issue the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="d33eb-149">Описание:</span><span class="sxs-lookup"><span data-stu-id="d33eb-149">where:</span></span>

* <span data-ttu-id="d33eb-150">`subscriptionId` — идентификатор подписки, включающей в себя службу управления API, резервное копирование которой вы пытаетесь выполнить;</span><span class="sxs-lookup"><span data-stu-id="d33eb-150">`subscriptionId` - id of the subscription containing the API Management service you are attempting to backup</span></span>
* <span data-ttu-id="d33eb-151">`resourceGroupName` — строка в формате "Api-Default-{service-region}", где `service-region` — это регион Azure, в котором размещена служба управления API для резервного копирования (например, `North-Central-US`);</span><span class="sxs-lookup"><span data-stu-id="d33eb-151">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are trying to backup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="d33eb-152">`serviceName` — имя службы управления API, резервное копирование которой вы выполняете, на момент ее создания;</span><span class="sxs-lookup"><span data-stu-id="d33eb-152">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span></span>
* <span data-ttu-id="d33eb-153">`api-version` замените `2014-02-14`.</span><span class="sxs-lookup"><span data-stu-id="d33eb-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="d33eb-154">В тексте запроса укажите целевую учетную запись хранения Azure, ключ доступа, имя контейнера BLOB-объектов и имя резервной копии:</span><span class="sxs-lookup"><span data-stu-id="d33eb-154">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="d33eb-155">Для заголовка запроса `Content-Type` установите значение `application/json`.</span><span class="sxs-lookup"><span data-stu-id="d33eb-155">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="d33eb-156">Резервное копирование — это длительная операция, которая может занять много минут.</span><span class="sxs-lookup"><span data-stu-id="d33eb-156">Backup is a long running operation that may take multiple minutes to complete.</span></span>  <span data-ttu-id="d33eb-157">Если запрос выполнен успешно и процесс резервного копирования инициирован, вы получите код состояния ответа `202 Accepted` с заголовком `Location`.</span><span class="sxs-lookup"><span data-stu-id="d33eb-157">If the request was successful and the backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="d33eb-158">Чтобы отслеживать состояние операции, отправляйте запросы GET на URL-адрес, указанный в заголовке `Location` .</span><span class="sxs-lookup"><span data-stu-id="d33eb-158">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="d33eb-159">Пока резервное копирование выполняется, вы будете получать код состояния "202 Accepted".</span><span class="sxs-lookup"><span data-stu-id="d33eb-159">While the backup is in progress you will continue to receive a '202 Accepted' status code.</span></span> <span data-ttu-id="d33eb-160">Код ответа `200 OK` указывает на то, что резервное копирование успешно завершено.</span><span class="sxs-lookup"><span data-stu-id="d33eb-160">A Response code of `200 OK` will indicate successful completion of the backup operation.</span></span>

<span data-ttu-id="d33eb-161">Обратите внимание на то, что к запросу на архивацию применяются приведенные ниже ограничения.</span><span class="sxs-lookup"><span data-stu-id="d33eb-161">Please note the following constraints when making a backup request.</span></span>

* <span data-ttu-id="d33eb-162">**Контейнер**, указанный в теле запроса, **должен существовать**.</span><span class="sxs-lookup"><span data-stu-id="d33eb-162">**Container** specified in the request body **must exist**.</span></span>
* <span data-ttu-id="d33eb-163">Пока выполняется резервное копирование, **не предпринимайте никаких действий по управлению службами**, таких как повышение или понижение уровня SKU, смена доменного имени и т. д.</span><span class="sxs-lookup"><span data-stu-id="d33eb-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="d33eb-164">Восстановление **резервной копии гарантируется только в течение 30 дней** с момента ее создания.</span><span class="sxs-lookup"><span data-stu-id="d33eb-164">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span></span>
* <span data-ttu-id="d33eb-165">**Данные об использовании**, применяемые при создании аналитических отчетов, **не включаются** в резервную копию.</span><span class="sxs-lookup"><span data-stu-id="d33eb-165">**Usage data** used for creating analytics reports **is not included** in the backup.</span></span> <span data-ttu-id="d33eb-166">Для периодического извлечения аналитических отчетов с целью их дальнейшего помещения на хранение используйте интерфейс [REST API управления API Azure][Azure API Management REST API].</span><span class="sxs-lookup"><span data-stu-id="d33eb-166">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="d33eb-167">Частота резервного копирования службы влияет на цель точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="d33eb-167">The frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="d33eb-168">Чтобы максимально снизить этот показатель, мы советуем настроить регулярное резервное копирование, а также выполнять резервное копирование по требованию после внесения важных изменений в службу API Management.</span><span class="sxs-lookup"><span data-stu-id="d33eb-168">To minimize it we advise implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span></span>
* <span data-ttu-id="d33eb-169">**Изменения**, внесенные в конфигурацию службы (например, интерфейсы API, политики, внешний вид портала разработчика) во время резервного копирования, **возможно, не включены в резервную копию. В этом случае они будут утеряны**.</span><span class="sxs-lookup"><span data-stu-id="d33eb-169">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span></span>

## <span data-ttu-id="d33eb-170"><a name="step2"> </a>Восстановление службы управления API</span><span class="sxs-lookup"><span data-stu-id="d33eb-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="d33eb-171">Чтобы восстановить службу API Management из ранее созданной резервной копии, отправьте следующий HTTP-запрос:</span><span class="sxs-lookup"><span data-stu-id="d33eb-171">To restore an API Management service from a previously created backup make the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="d33eb-172">где:</span><span class="sxs-lookup"><span data-stu-id="d33eb-172">where:</span></span>

* <span data-ttu-id="d33eb-173">`subscriptionId` — идентификатор подписки, включающей в себя службу управления API, которую нужно восстановить из резервной копии;</span><span class="sxs-lookup"><span data-stu-id="d33eb-173">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="d33eb-174">`resourceGroupName` — строка в формате "Api-Default-{service-region}", где `service-region` — это регион Azure, в котором размещена восстанавливаемая из резервной копии служба управления API (например, `North-Central-US`);</span><span class="sxs-lookup"><span data-stu-id="d33eb-174">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="d33eb-175">`serviceName` — имя восстанавливаемой службы управления API на момент ее создания;</span><span class="sxs-lookup"><span data-stu-id="d33eb-175">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span></span>
* <span data-ttu-id="d33eb-176">`api-version` замените `2014-02-14`.</span><span class="sxs-lookup"><span data-stu-id="d33eb-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="d33eb-177">В тексте запроса укажите расположение файла резервной копии, т. е. учетную запись хранения Azure, ключ доступа, имя контейнера BLOB-объектов и имя резервной копии:</span><span class="sxs-lookup"><span data-stu-id="d33eb-177">In the body of the request, specify the backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="d33eb-178">Для заголовка запроса `Content-Type` установите значение `application/json`.</span><span class="sxs-lookup"><span data-stu-id="d33eb-178">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="d33eb-179">Восстановление — это длительная операция, которая может занять до 30 минут и более.</span><span class="sxs-lookup"><span data-stu-id="d33eb-179">Restore is a long running operation that may take up to 30 or more minutes to complete.</span></span>  <span data-ttu-id="d33eb-180">Если запрос выполнен успешно и процесс восстановления инициирован, вы получите код состояния ответа `202 Accepted` с заголовком `Location`.</span><span class="sxs-lookup"><span data-stu-id="d33eb-180">If the request was successful and the restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="d33eb-181">Чтобы отслеживать состояние операции, отправляйте запросы GET на URL-адрес, указанный в заголовке `Location` .</span><span class="sxs-lookup"><span data-stu-id="d33eb-181">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="d33eb-182">Пока восстановление выполняется, вы будете получать код состояния "202 Accepted".</span><span class="sxs-lookup"><span data-stu-id="d33eb-182">While the restore is in progress you will continue to receive '202 Accepted' status code.</span></span> <span data-ttu-id="d33eb-183">Код ответа `200 OK` указывает на то, что восстановление успешно завершено.</span><span class="sxs-lookup"><span data-stu-id="d33eb-183">A response code of `200 OK` will indicate successful completion of the restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d33eb-184">**SKU** восстанавливаемой службы **должен соответствовать** SKU службы в резервной копии.</span><span class="sxs-lookup"><span data-stu-id="d33eb-184">**The SKU** of the service being restored into **must match** the SKU of the backed up service being restored.</span></span>
>
> <span data-ttu-id="d33eb-185">**Изменения**, внесенные в конфигурацию службы (например, интерфейсы API, политики, внешний вид портала разработчика) во время восстановления, **могут быть перезаписаны**.</span><span class="sxs-lookup"><span data-stu-id="d33eb-185">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d33eb-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d33eb-186">Next steps</span></span>
<span data-ttu-id="d33eb-187">Чтобы ознакомиться с двумя другими способами резервного копирования и восстановления, прочитайте следующие записи в блогах по решениям Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d33eb-187">Check out the following Microsoft blogs for two different walkthroughs of the backup/restore process.</span></span>

* [<span data-ttu-id="d33eb-188">Репликация учетных записей управления API Azure</span><span class="sxs-lookup"><span data-stu-id="d33eb-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="d33eb-189">Благодарим Джизелу за материалы для этой статьи.</span><span class="sxs-lookup"><span data-stu-id="d33eb-189">Thank you to Gisela for her contribution to this article.</span></span>
* [<span data-ttu-id="d33eb-190">Управление API Azure: резервное копирование и восстановление конфигурации</span><span class="sxs-lookup"><span data-stu-id="d33eb-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="d33eb-191">Стюарт подробно описывает альтернативный подход, который не соответствует официальным рекомендациям, но тоже очень интересен.</span><span class="sxs-lookup"><span data-stu-id="d33eb-191">The approach detailed by Stuart does not match the official guidance but it is very interesting.</span></span>

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
