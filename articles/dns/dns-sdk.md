---
title: "зоны DNS aaaCreate и наборов записей в Azure DNS с помощью hello .NET SDK | Документы Microsoft"
description: "Как toocreate зон DNS и запись устанавливает в Azure DNS с помощью hello .NET SDK."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a><span data-ttu-id="7273c-103">Создание зоны DNS и наборы записей с помощью hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7273c-103">Create DNS zones and record sets using hello .NET SDK</span></span>

<span data-ttu-id="7273c-104">С помощью пакета SDK DNS с библиотекой .NET управления DNS можно автоматизировать операции toocreate, удаление или обновление зоны DNS, наборы записей и записи.</span><span class="sxs-lookup"><span data-stu-id="7273c-104">You can automate operations toocreate, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="7273c-105">Полный проект Visual Studio доступен [здесь](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True).</span><span class="sxs-lookup"><span data-stu-id="7273c-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="7273c-106">Создание учетной записи субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="7273c-106">Create a service principal account</span></span>

<span data-ttu-id="7273c-107">Как правило программный доступ к ресурсам tooAzure предоставляется через выделенную учетную запись, а не учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="7273c-107">Typically, programmatic access tooAzure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="7273c-108">Эти выделенные учетные записи называются учетными записями субъектов-служб.</span><span class="sxs-lookup"><span data-stu-id="7273c-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="7273c-109">toouse hello Azure DNS SDK пример проекта, требуется toocreate учетную запись участника службы и назначьте его hello правильные разрешения.</span><span class="sxs-lookup"><span data-stu-id="7273c-109">toouse hello Azure DNS SDK sample project, you first need toocreate a service principal account and assign it hello correct permissions.</span></span>

1. <span data-ttu-id="7273c-110">Выполните [эти инструкции](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate учетную запись участника службы (пример проекта hello DNS Azure SDK предполагается проверки подлинности на основе пароля).</span><span class="sxs-lookup"><span data-stu-id="7273c-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate a service principal account (hello Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="7273c-111">Создайте группу ресурсов (см. сведения [здесь](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="7273c-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="7273c-112">Используйте Azure RBAC toogrant hello учетная запись участника «Участник зоны DNS» разрешения toohello группа ресурсов службы ([Вот как](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="7273c-112">Use Azure RBAC toogrant hello service principal account 'DNS Zone Contributor' permissions toohello resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="7273c-113">При использовании примера проекта hello DNS Azure SDK, измените файл «program.cs» hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7273c-113">If using hello Azure DNS SDK sample project, edit hello 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="7273c-114">Вставьте hello правильные значения для hello идентификатора клиента, clientId (также известный как идентификатор учетной записи), секретные данные (пароль учетная запись участника службы) и идентификатор подписки, как в шаге 1.</span><span class="sxs-lookup"><span data-stu-id="7273c-114">Insert hello correct values for hello tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="7273c-115">Введите имя группы ресурсов hello, выбранного в шаге 2.</span><span class="sxs-lookup"><span data-stu-id="7273c-115">Enter hello resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="7273c-116">Введите имя зоны DNS по своему выбору.</span><span class="sxs-lookup"><span data-stu-id="7273c-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="7273c-117">Пакеты NuGet и объявления пространств имен</span><span class="sxs-lookup"><span data-stu-id="7273c-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="7273c-118">toouse hello Azure DNS .NET SDK необходимо tooinstall hello **Библиотека управления DNS Azure** пакета NuGet и другие необходимые пакеты Azure.</span><span class="sxs-lookup"><span data-stu-id="7273c-118">toouse hello Azure DNS .NET SDK, you need tooinstall hello **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="7273c-119">В **Visual Studio**, откройте существующий или новый проект.</span><span class="sxs-lookup"><span data-stu-id="7273c-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="7273c-120">Go слишком**средства**  **>**  **диспетчера пакетов NuGet**  **>**  **управление пакетами NuGet для Решения...** .</span><span class="sxs-lookup"><span data-stu-id="7273c-120">Go too**Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="7273c-121">Нажмите кнопку **Обзор**, включите hello **включить предварительный выпуск** флажок и введите **Microsoft.Azure.Management.Dns** в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="7273c-121">Click **Browse**, enable hello **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in hello search box.</span></span>
4. <span data-ttu-id="7273c-122">Выберите пакет hello и нажмите кнопку **установить** tooadd его tooyour проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7273c-122">Select hello package and click **Install** tooadd it tooyour Visual Studio project.</span></span>
5. <span data-ttu-id="7273c-123">Повторите процесс hello выше hello установки tooalso следующие пакеты: **Microsoft.Rest.ClientRuntime.Azure.Authentication** и **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="7273c-123">Repeat hello process above tooalso install hello following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="7273c-124">Добавление объявлений пространств имен</span><span class="sxs-lookup"><span data-stu-id="7273c-124">Add namespace declarations</span></span>

<span data-ttu-id="7273c-125">Добавьте следующие объявления пространств имен hello</span><span class="sxs-lookup"><span data-stu-id="7273c-125">Add hello following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a><span data-ttu-id="7273c-126">Инициализировать клиент управления DNS hello</span><span class="sxs-lookup"><span data-stu-id="7273c-126">Initialize hello DNS management client</span></span>

<span data-ttu-id="7273c-127">Hello *DnsManagementClient* содержит hello методы и свойства, необходимые для управления DNS-зон и наборы данных.</span><span class="sxs-lookup"><span data-stu-id="7273c-127">hello *DnsManagementClient* contains hello methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="7273c-128">Hello следующий код входит учетная запись участника службы toohello и создает объект DnsManagementClient.</span><span class="sxs-lookup"><span data-stu-id="7273c-128">hello following code logs in toohello service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="7273c-129">Создание или обновление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="7273c-129">Create or update a DNS zone</span></span>

<span data-ttu-id="7273c-130">toocreate зоны DNS, сначала объект «Зону» создается параметры зоны DNS toocontain hello.</span><span class="sxs-lookup"><span data-stu-id="7273c-130">toocreate a DNS zone, first a "Zone" object is created toocontain hello DNS zone parameters.</span></span> <span data-ttu-id="7273c-131">Поскольку зоны DNS определенного региона связанного tooa, too'global задано местоположение hello ".</span><span class="sxs-lookup"><span data-stu-id="7273c-131">Because DNS zones are not linked tooa specific region, hello location is set too'global'.</span></span> <span data-ttu-id="7273c-132">В этом примере [диспетчера ресурсов Azure «тег»](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) добавляется toohello зоны.</span><span class="sxs-lookup"><span data-stu-id="7273c-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added toohello zone.</span></span>

<span data-ttu-id="7273c-133">tooactually создать или обновить зону hello в Azure DNS, hello зоны объект, содержащий параметры зоны hello передается toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* метод.</span><span class="sxs-lookup"><span data-stu-id="7273c-133">tooactually create or update hello zone in Azure DNS, hello zone object containing hello zone parameters is passed toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="7273c-134">DnsManagementClient поддерживает три режима работы: синхронные («CreateOrUpdate»), асинхронную («CreateOrUpdateAsync»), или асинхронном ответ toohello HTTP доступа (CreateOrUpdateWithHttpMessagesAsync).</span><span class="sxs-lookup"><span data-stu-id="7273c-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="7273c-135">Вы можете выбрать любой из этих режимов в зависимости от потребностей приложения.</span><span class="sxs-lookup"><span data-stu-id="7273c-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="7273c-136">Служба Azure DNS поддерживает оптимистичный параллелизм с помощью [тегов Etag](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="7273c-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="7273c-137">В этом примере указания «*» для заголовка hello «If-None-Match» зону DNS сообщает toocreate Azure DNS, если еще не существует.</span><span class="sxs-lookup"><span data-stu-id="7273c-137">In this example, specifying "*" for hello 'If-None-Match' header tells Azure DNS toocreate a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="7273c-138">Hello Если возникнет ошибка зоны с помощью hello заданным именем уже существует в hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7273c-138">hello call fails if a zone with hello given name already exists in hello given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="7273c-139">Создание записей и наборов записей DNS</span><span class="sxs-lookup"><span data-stu-id="7273c-139">Create DNS record sets and records</span></span>

<span data-ttu-id="7273c-140">Записи DNS управляются как набор записей.</span><span class="sxs-lookup"><span data-stu-id="7273c-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="7273c-141">Набор записей — это набор записей с hello таким же именем и запишите типа в пределах зоны.</span><span class="sxs-lookup"><span data-stu-id="7273c-141">A record set is a set of records with hello same name and record type within a zone.</span></span>  <span data-ttu-id="7273c-142">Имя набора записей Hello toohello относительное имя зоны, не hello полное DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="7273c-142">hello record set name is relative toohello zone name, not hello fully qualified DNS name.</span></span>

<span data-ttu-id="7273c-143">toocreate или обновить набор записей, объект параметров «Набор записей» создается и передается слишком*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="7273c-143">toocreate or update a record set, a "RecordSet" parameters object is created and passed too*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="7273c-144">С зонами DNS, имеется три режима работы: синхронные («CreateOrUpdate»), асинхронную («CreateOrUpdateAsync»), или асинхронном ответ toohello HTTP доступа (CreateOrUpdateWithHttpMessagesAsync).</span><span class="sxs-lookup"><span data-stu-id="7273c-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="7273c-145">Как и в случае с зонами DNS, операции с наборами записей поддерживают оптимистичный параллелизм.</span><span class="sxs-lookup"><span data-stu-id="7273c-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="7273c-146">В этом примере поскольку указаны не «If-Match» и «If-None-Match», hello набора записей создается всегда.</span><span class="sxs-lookup"><span data-stu-id="7273c-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, hello record set is always created.</span></span>  <span data-ttu-id="7273c-147">Этот вызов перезаписывает все существующие записей с hello таким же именем и запишите тип в этой зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="7273c-147">This call overwrites any existing record set with hello same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="7273c-148">Получение зон и наборов записей</span><span class="sxs-lookup"><span data-stu-id="7273c-148">Get zones and record sets</span></span>

<span data-ttu-id="7273c-149">Hello *DnsManagementClient.Zones.Get* и *DnsManagementClient.RecordSets.Get* получать отдельные зоны и наборы записей, соответственно.</span><span class="sxs-lookup"><span data-stu-id="7273c-149">hello *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="7273c-150">Наборы записей идентифицируются по их тип, имя и hello зоны и группе ресурсов которой находятся.</span><span class="sxs-lookup"><span data-stu-id="7273c-150">RecordSets are identified by their type, name, and hello zone and resource group they exist in.</span></span> <span data-ttu-id="7273c-151">Зоны идентифицируются по их группе ресурсов имя и hello, они существуют в.</span><span class="sxs-lookup"><span data-stu-id="7273c-151">Zones are identified by their name and hello resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="7273c-152">Обновление имеющегося набора записей</span><span class="sxs-lookup"><span data-stu-id="7273c-152">Update an existing record set</span></span>

<span data-ttu-id="7273c-153">tooupdate DNS-запись существующего набора, сначала получить набор записей hello, а затем обновить запись hello содержимое набора, а затем отправить изменения hello.</span><span class="sxs-lookup"><span data-stu-id="7273c-153">tooupdate an existing DNS record set, first retrieve hello record set, then update hello record set contents, then submit hello change.</span></span>  <span data-ttu-id="7273c-154">В этом примере мы указываем hello 'Etag' из hello получить запись, задайте в параметре «If-Match» hello.</span><span class="sxs-lookup"><span data-stu-id="7273c-154">In this example, we specify hello 'Etag' from hello retrieved record set in hello 'If-Match' parameter.</span></span> <span data-ttu-id="7273c-155">Hello вызов завершается сбоем, если параллельная операция изменил запись hello, пока задание в hello.</span><span class="sxs-lookup"><span data-stu-id="7273c-155">hello call fails if a concurrent operation has modified hello record set in hello meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="7273c-156">Вывод списка зон и наборов записей</span><span class="sxs-lookup"><span data-stu-id="7273c-156">List zones and record sets</span></span>

<span data-ttu-id="7273c-157">использовать зоны toolist hello *DnsManagementClient.Zones.List...*  использовать методы, которые поддерживает список всех зон в данной группы ресурсов либо всех зон в наборы записей toolist подписки Azure (для ресурсов групп.), *DnsManagementClient.RecordSets.List...*  методы, которые поддерживает список всех наборов записей в данной зоны или только этих наборов записей определенного типа.</span><span class="sxs-lookup"><span data-stu-id="7273c-157">toolist zones, use hello *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) toolist record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="7273c-158">Обратите внимание, что при выводе списка зон и наборов записей может быть применена разбивка на страницы.</span><span class="sxs-lookup"><span data-stu-id="7273c-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="7273c-159">Следующий пример показывает как Hello tooiterate через hello страницы результатов.</span><span class="sxs-lookup"><span data-stu-id="7273c-159">hello following example shows how tooiterate through hello pages of results.</span></span> <span data-ttu-id="7273c-160">(Искусственно небольшой размер "2" является tooforce используется разбиение на страницы на практике этот параметр должен быть опущен и hello размер страницы по умолчанию, используемый.)</span><span class="sxs-lookup"><span data-stu-id="7273c-160">(An artificially small page size of '2' is used tooforce paging; in practice this parameter should be omitted and hello default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="7273c-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7273c-161">Next steps</span></span>

<span data-ttu-id="7273c-162">Загрузите hello [пакета SDK .NET Azure DNS образец проекта](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), который включает дополнительные примеры как toouse hello SDK .NET Azure DNS, включая примеры для других типов записей DNS.</span><span class="sxs-lookup"><span data-stu-id="7273c-162">Download hello [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how toouse hello Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
