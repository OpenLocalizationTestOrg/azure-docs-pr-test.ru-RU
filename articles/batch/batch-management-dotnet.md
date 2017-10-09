---
title: "aaaManage пакетной учетной записи ресурсов с hello клиентская библиотека для .NET — Azure | Документы Microsoft"
description: "Создание, удаление и изменение ресурсов учетной записи пакетной службы Azure с библиотекой hello пакета управления .NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 638d8129f3841ffcfb2e10f5d531a319bcbb7701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a><span data-ttu-id="94fed-103">Управление учетными записями пакетной и квоты с hello пакета управления клиентской библиотеки для .NET</span><span class="sxs-lookup"><span data-stu-id="94fed-103">Manage Batch accounts and quotas with hello Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="94fed-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="94fed-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="94fed-105">Библиотека .NET для управления пакетной службой</span><span class="sxs-lookup"><span data-stu-id="94fed-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="94fed-106">Можно понизить обслуживания издержек в приложениях пакетной службы Azure с помощью hello [пакета управления .NET] [ api_mgmt_net] библиотеки tooautomate пакетной учетной записи создание, удаление, управление ключами и обнаружения квоты.</span><span class="sxs-lookup"><span data-stu-id="94fed-106">You can lower maintenance overhead in your Azure Batch applications by using hello [Batch Management .NET][api_mgmt_net] library tooautomate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="94fed-107">**Создание и удаление учетных записей пакетной службы** в любом регионе.</span><span class="sxs-lookup"><span data-stu-id="94fed-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="94fed-108">Если, например, как независимый поставщик программного (обеспечения ISV) предоставляет службы для клиентов в которых каждый назначается отдельной учетной записи пакета для выставления счетов, можно добавить портал учетных записей создание и удаление возможности tooyour клиента.</span><span class="sxs-lookup"><span data-stu-id="94fed-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities tooyour customer portal.</span></span>
* <span data-ttu-id="94fed-109">**Получение и повторное создание ключей учетных записей** для всех учетных записей пакетной службы программным образом.</span><span class="sxs-lookup"><span data-stu-id="94fed-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="94fed-110">Это особенно удобно для обеспечения соответствия политикам безопасности, которые могут требовать периодической смены ключей и определять сроки действия ключей учетных записей.</span><span class="sxs-lookup"><span data-stu-id="94fed-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="94fed-111">Если у вас есть несколько учетных записей пакетной службы в разных регионах Azure, автоматизация смены ключей повысит эффективность вашего решения.</span><span class="sxs-lookup"><span data-stu-id="94fed-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="94fed-112">**Проверьте учетную запись квоты** и принимать hello организации проб и ошибок и определения, имеют какие ограничений, какие учетные записи пакета.</span><span class="sxs-lookup"><span data-stu-id="94fed-112">**Check account quotas** and take hello trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="94fed-113">Проверка квот учетной записи до запуска заданий, создание пулов или добавление вычислительных узлов позволит вам заранее выбирать время и место создания вычислительных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="94fed-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="94fed-114">Вы можете определить учетные записи, требующие повышения квот, прежде чем выделить дополнительные ресурсы в этих учетных записях.</span><span class="sxs-lookup"><span data-stu-id="94fed-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="94fed-115">**Объединить возможности других служб Azure** взаимодействие полнофункционального управления — с помощью пакета управления .NET, [Azure Active Directory][aad_about]и hello [Azure Диспетчер ресурсов] [ resman_overview] вместе в hello того же приложения.</span><span class="sxs-lookup"><span data-stu-id="94fed-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and hello [Azure Resource Manager][resman_overview] together in hello same application.</span></span> <span data-ttu-id="94fed-116">С помощью этих функций и их интерфейсы API, можно полноценного издержками проверки подлинности, hello toocreate возможности и удаления группы ресурсов и возможности hello, описанных выше для решения управления начала до конца.</span><span class="sxs-lookup"><span data-stu-id="94fed-116">By using these features and their APIs, you can provide a frictionless authentication experience, hello ability toocreate and delete resource groups, and hello capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="94fed-117">Хотя данная статья посвящена hello программное управление учетными записями, ключи и квоты пакета, можно выполнять многие из этих действий с помощью hello [портал Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="94fed-117">While this article focuses on hello programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="94fed-118">Дополнительные сведения см. в разделе [создать учетную запись пакетной службы Azure с помощью портала Azure hello](batch-account-create-portal.md) и [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="94fed-118">For more information, see [Create an Azure Batch account using hello Azure portal](batch-account-create-portal.md) and [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="94fed-119">Создание и удаление учетных записей пакетной службы</span><span class="sxs-lookup"><span data-stu-id="94fed-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="94fed-120">Как уже упоминалось, одной из функций hello основной hello API управления пакета является toocreate и удалять учетные записи пакета в регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="94fed-120">As mentioned, one of hello primary features of hello Batch Management API is toocreate and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="94fed-121">Таким образом, используйте toodo [BatchManagementClient.Account.CreateAsync] [ net_create] и [DeleteAsync][net_delete], или их синхронных аналогов.</span><span class="sxs-lookup"><span data-stu-id="94fed-121">toodo so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="94fed-122">Hello следующий фрагмент кода создает учетную запись, получает вновь созданные учетной записи из hello пакетная служба hello, а затем удаляет его.</span><span class="sxs-lookup"><span data-stu-id="94fed-122">hello following code snippet creates an account, obtains hello newly created account from hello Batch service, and then deletes it.</span></span> <span data-ttu-id="94fed-123">В этом фрагменте кода и hello другим пользователям в этой статье `batchManagementClient` — это полностью инициализированный экземпляр [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="94fed-123">In this snippet and hello others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get hello new account from hello Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete hello account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="94fed-124">Требуется для приложений, использующих библиотеки пакета управления .NET hello и его класс BatchManagementClient **администратора службы** или **coadministrator** получить доступ к подписке toohello, которому принадлежит hello Управлять toobe пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="94fed-124">Applications that use hello Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access toohello subscription that owns hello Batch account toobe managed.</span></span> <span data-ttu-id="94fed-125">Дополнительные сведения см. в разделе hello [Azure Active Directory](#azure-active-directory) раздел и hello [AccountManagement] [ acct_mgmt_sample] образец кода.</span><span class="sxs-lookup"><span data-stu-id="94fed-125">For more information, see hello [Azure Active Directory](#azure-active-directory) section and hello [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="94fed-126">Получение и повторное создание ключей учетных записей</span><span class="sxs-lookup"><span data-stu-id="94fed-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="94fed-127">Получите первичный и вторичный ключи из любой учетной записи пакетной службы в своей подписке с помощью метода [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="94fed-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="94fed-128">Для повторного создания этих ключей используется метод [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="94fed-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print hello primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate hello primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="94fed-129">Вы можете упростить процедуру подключения в своем приложении для управления.</span><span class="sxs-lookup"><span data-stu-id="94fed-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="94fed-130">Во-первых, получить ключ учетной записи для учетной записи пакетной hello нужно toomanage с [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="94fed-130">First, obtain an account key for hello Batch account you wish toomanage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="94fed-131">Затем используйте этот ключ при инициализации библиотеки .NET пакета hello [BatchSharedKeyCredentials] [ net_sharedkeycred] класс, который используется при инициализации [BatchClient] [net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="94fed-131">Then, use this key when initializing hello Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="94fed-132">Проверка подписки Azure и квот учетной записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="94fed-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="94fed-133">Подписки Azure и hello отдельных служб Azure, как все пакета имеют квот по умолчанию, максимальное число сущностей, определенных в них hello.</span><span class="sxs-lookup"><span data-stu-id="94fed-133">Azure subscriptions and hello individual Azure services like Batch all have default quotas that limit hello number of certain entities within them.</span></span> <span data-ttu-id="94fed-134">Hello квоты по умолчанию для подписок Azure, в разделе [подписка Azure и ограничения служб, квоты и ограничения](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="94fed-134">For hello default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="94fed-135">Квоты по умолчанию hello hello пакетная служба, в разделе [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="94fed-135">For hello default quotas of hello Batch service, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="94fed-136">С помощью библиотеки .NET пакета управления hello, можно проверить эти квоты в ваших приложениях.</span><span class="sxs-lookup"><span data-stu-id="94fed-136">By using hello Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="94fed-137">Это позволит вам решений по распределению toomake перед добавлением учетных записей или вычислительные ресурсы, такие как пулы и вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="94fed-137">This enables you toomake allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="94fed-138">Определение квот для учетной записи пакетной службы в подписке Azure</span><span class="sxs-lookup"><span data-stu-id="94fed-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="94fed-139">Перед созданием пакетную учетную запись в области, можно проверить вашей подписки Azure toosee ли вы могли tooadd учетную запись в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="94fed-139">Before creating a Batch account in a region, you can check your Azure subscription toosee whether you are able tooadd an account in that region.</span></span>

<span data-ttu-id="94fed-140">В приведенном ниже фрагменте кода hello, сначала используется [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget коллекцию все учетные записи пакета, которые находятся в пределах подписки.</span><span class="sxs-lookup"><span data-stu-id="94fed-140">In hello code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] tooget a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="94fed-141">После получения этой коллекции мы мы определили сколько учетных записей в целевой области hello.</span><span class="sxs-lookup"><span data-stu-id="94fed-141">Once we've obtained this collection, we determine how many accounts are in hello target region.</span></span> <span data-ttu-id="94fed-142">Затем мы используем [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain hello Квота пакетной учетной записи и определите, сколько учетных записей (если таковые имеются), которые могут создаваться в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="94fed-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] tooobtain hello Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within hello subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within hello target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get hello account quota for hello specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in hello target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in hello {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="94fed-143">В приведенном выше фрагменте hello `creds` является экземпляром класса [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="94fed-143">In hello snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="94fed-144">toosee пример создания этого объекта. в разделе hello [AccountManagement] [ acct_mgmt_sample] образец кода на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="94fed-144">toosee an example of creating this object, see hello [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="94fed-145">Определение квоты вычислительных ресурсов для учетной записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="94fed-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="94fed-146">Перед увеличением вычислительные ресурсы в пакет решения, можно проверить tooensure hello ресурсов, tooallocate не будет превышать квоты hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="94fed-146">Before increasing compute resources in your Batch solution, you can check tooensure hello resources you want tooallocate won't exceed hello account's quotas.</span></span> <span data-ttu-id="94fed-147">В приведенном ниже фрагменте кода hello, мы печати hello данные квоты для hello пакетной учетной записи с именем `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="94fed-147">In hello code snippet below, we print hello quota information for hello Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="94fed-148">В приложении можно использовать такие сведения toodetermine ли hello учетной записи может обрабатывать toobe дополнительные ресурсы hello создан.</span><span class="sxs-lookup"><span data-stu-id="94fed-148">In your own application, you could use such information toodetermine whether hello account can handle hello additional resources toobe created.</span></span>

```csharp
// First obtain hello Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print hello compute resource quotas for hello account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="94fed-149">Хотя по умолчанию квоты для подписки Azure и служб, многие из этих ограничений может быть повышен путем выполнения запроса в hello [портал Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="94fed-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="94fed-150">Например, в разделе [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md) инструкции об увеличении квот пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="94fed-150">For example, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="94fed-151">Использование Azure AD с библиотекой .NET для управления пакетной службой</span><span class="sxs-lookup"><span data-stu-id="94fed-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="94fed-152">Библиотека пакета управления .NET Hello является клиента поставщика ресурсов Azure и используется вместе с [диспетчера ресурсов Azure] [ resman_overview] toomanage записи ресурсам программными средствами.</span><span class="sxs-lookup"><span data-stu-id="94fed-152">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage account resources programmatically.</span></span> <span data-ttu-id="94fed-153">Azure AD — необходимые tooauthenticate запросов, выполненных при помощи любого клиента поставщика ресурсов Azure, включая библиотеку .NET пакета управления hello, а по [диспетчера ресурсов Azure][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="94fed-153">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="94fed-154">Сведения об использовании Azure AD с библиотекой hello пакета управления .NET см. в разделе [использование Azure Active Directory tooauthenticate пакета решения](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="94fed-154">For information about using Azure AD with hello Batch Management .NET library, see [Use Azure Active Directory tooauthenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="94fed-155">Пример проекта на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="94fed-155">Sample project on GitHub</span></span>

<span data-ttu-id="94fed-156">toosee пакета управления .NET в действии, извлечь hello [AccountManagment] [ acct_mgmt_sample] примера проекта на GitHub.</span><span class="sxs-lookup"><span data-stu-id="94fed-156">toosee Batch Management .NET in action, check out hello [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="94fed-157">AccountManagment пример приложения Hello демонстрирует hello следующие операции:</span><span class="sxs-lookup"><span data-stu-id="94fed-157">hello AccountManagment sample application demonstrates hello following operations:</span></span>

1. <span data-ttu-id="94fed-158">Получение маркера безопасности из Active Directory Azure с помощью библиотеки [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="94fed-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="94fed-159">Если пользователь hello не уже выполнил вход, запрос для своих учетных данных Azure.</span><span class="sxs-lookup"><span data-stu-id="94fed-159">If hello user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="94fed-160">С помощью маркера безопасности hello, полученный из Azure AD, создавать [SubscriptionClient] [ resman_subclient] tooquery Azure список подписок, связанных с учетной записью hello.</span><span class="sxs-lookup"><span data-stu-id="94fed-160">With hello security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] tooquery Azure for a list of subscriptions associated with hello account.</span></span> <span data-ttu-id="94fed-161">Hello пользователь может выбрать подписку из списка hello, если он содержит более одной подписки.</span><span class="sxs-lookup"><span data-stu-id="94fed-161">hello user can select a subscription from hello list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="94fed-162">Получите учетные данные, связанные с hello выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="94fed-162">Get credentials associated with hello selected subscription.</span></span>
4. <span data-ttu-id="94fed-163">Создание [ResourceManagementClient] [ resman_client] объекта с использованием учетных данных hello.</span><span class="sxs-lookup"><span data-stu-id="94fed-163">Create a [ResourceManagementClient][resman_client] object by using hello credentials.</span></span>
5. <span data-ttu-id="94fed-164">Используйте [ResourceManagementClient] [ resman_client] объекта toocreate группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="94fed-164">Use a [ResourceManagementClient][resman_client] object toocreate a resource group.</span></span>
6. <span data-ttu-id="94fed-165">Используйте [BatchManagementClient] [ net_mgmt_client] объекта tooperform несколько операций пакетной учетной записи:</span><span class="sxs-lookup"><span data-stu-id="94fed-165">Use a [BatchManagementClient][net_mgmt_client] object tooperform several Batch account operations:</span></span>
   * <span data-ttu-id="94fed-166">Создайте учетную запись пакета в новую группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="94fed-166">Create a Batch account in hello new resource group.</span></span>
   * <span data-ttu-id="94fed-167">Получение hello вновь созданные учетной записи из hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="94fed-167">Get hello newly created account from hello Batch service.</span></span>
   * <span data-ttu-id="94fed-168">Здравствуй, мир ключи учетной записи для новой учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="94fed-168">Print hello account keys for hello new account.</span></span>
   * <span data-ttu-id="94fed-169">Повторно создать новый первичный ключ для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="94fed-169">Regenerate a new primary key for hello account.</span></span>
   * <span data-ttu-id="94fed-170">Сведения о квоте Здравствуй, мир hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="94fed-170">Print hello quota information for hello account.</span></span>
   * <span data-ttu-id="94fed-171">Здравствуй, мир данные квоты для подписки hello.</span><span class="sxs-lookup"><span data-stu-id="94fed-171">Print hello quota information for hello subscription.</span></span>
   * <span data-ttu-id="94fed-172">Печать всех учетных записей в рамках подписки hello.</span><span class="sxs-lookup"><span data-stu-id="94fed-172">Print all accounts within hello subscription.</span></span>
   * <span data-ttu-id="94fed-173">Удаление созданной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="94fed-173">Delete newly created account.</span></span>
7. <span data-ttu-id="94fed-174">Удалите группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="94fed-174">Delete hello resource group.</span></span>

<span data-ttu-id="94fed-175">Перед удалением группы учетных записей и ресурсов пакета только что созданный hello, их можно просмотреть в hello [портал Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="94fed-175">Before deleting hello newly created Batch account and resource group, you can view them in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="94fed-176">Пример приложения hello toorun успешно, необходимо сначала зарегистрировать его с вашим клиентом Azure AD в hello Azure portal и предоставьте разрешения toohello API диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="94fed-176">toorun hello sample application successfully, you must first register it with your Azure AD tenant in hello Azure portal and grant permissions toohello Azure Resource Manager API.</span></span> <span data-ttu-id="94fed-177">Выполните шаги hello в [решения для проверки подлинности пакета управления с помощью Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="94fed-177">Follow hello steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


[aad_about]: ../active-directory/active-directory-whatis.md "Что такое Microsoft Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Сценарии аутентификации в Azure Active Directory"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Интеграция приложений с Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
