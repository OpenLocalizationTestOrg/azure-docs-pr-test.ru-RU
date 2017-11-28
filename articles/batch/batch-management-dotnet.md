---
title: "Управление ресурсами учетной записи пакетной службы с помощью клиентской библиотеки для .NET в Azure | Документация Майкрософт"
description: "Создание, удаление и изменение ресурсов учетных записей пакетной службы Azure с помощью библиотеки .NET для управления пакетной службой."
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
ms.openlocfilehash: eafde9258222a2ab09ade2e366f9cc595a303dec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-batch-accounts-and-quotas-with-the-batch-management-client-library-for-net"></a><span data-ttu-id="b4a1d-103">Управление учетными записями и квотами пакетной службы с помощью клиентской библиотеки .NET для управления пакетной службой</span><span class="sxs-lookup"><span data-stu-id="b4a1d-103">Manage Batch accounts and quotas with the Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4a1d-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b4a1d-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="b4a1d-105">Библиотека .NET для управления пакетной службой</span><span class="sxs-lookup"><span data-stu-id="b4a1d-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="b4a1d-106">С помощью [библиотеки .NET для управления пакетной службой][api_mgmt_net] можно снизить издержки на обслуживание приложений пакетной службы Azure. Эта библиотека позволяет автоматизировать создание и удаление учетных записей пакетной службы, управление ключами и определение квот.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-106">You can lower maintenance overhead in your Azure Batch applications by using the [Batch Management .NET][api_mgmt_net] library to automate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="b4a1d-107">**Создание и удаление учетных записей пакетной службы** в любом регионе.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="b4a1d-108">Например, вы являетесь независимым поставщиком программного обеспечения и оказываете услуги клиентам, каждому из которых назначена соответствующая учетная запись пакетной службы для выставления счетов. Для повышения удобства вы можете добавить на портал для пользователей возможность создания и удаления учетных записей.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities to your customer portal.</span></span>
* <span data-ttu-id="b4a1d-109">**Получение и повторное создание ключей учетных записей** для всех учетных записей пакетной службы программным образом.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="b4a1d-110">Это особенно удобно для обеспечения соответствия политикам безопасности, которые могут требовать периодической смены ключей и определять сроки действия ключей учетных записей.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="b4a1d-111">Если у вас есть несколько учетных записей пакетной службы в разных регионах Azure, автоматизация смены ключей повысит эффективность вашего решения.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="b4a1d-112">**Проверка квот учетных записей** и исключение метода проб и ошибок из процедуры определения ограничений учетных записей пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-112">**Check account quotas** and take the trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="b4a1d-113">Проверка квот учетной записи до запуска заданий, создание пулов или добавление вычислительных узлов позволит вам заранее выбирать время и место создания вычислительных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="b4a1d-114">Вы можете определить учетные записи, требующие повышения квот, прежде чем выделить дополнительные ресурсы в этих учетных записях.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="b4a1d-115">**Объедините функции других служб Azure** для создания полнофункционального приложения для управления, в котором одновременно используются библиотека .NET для управления пакетной службой, [Azure Active Directory][aad_about] и [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and the [Azure Resource Manager][resman_overview] together in the same application.</span></span> <span data-ttu-id="b4a1d-116">С помощью этих функций и соответствующих API вы можете предоставлять клиентам удобные возможности проверки подлинности, создания и удаления групп ресурсов, а также доступа к описанным выше функциям.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-116">By using these features and their APIs, you can provide a frictionless authentication experience, the ability to create and delete resource groups, and the capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="b4a1d-117">Несмотря на то, что в этой статье акцент сделан на программное управление учетными записями пакетной службы, ключами и квотами, большую часть описываемых действий можно выполнить на [портале Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-117">While this article focuses on the programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using the [Azure portal][azure_portal].</span></span> <span data-ttu-id="b4a1d-118">Дополнительные сведения см. в статьях [Создание учетной записи пакетной службы Azure на портале Azure](batch-account-create-portal.md) и [Квоты и ограничения пакетной службы Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="b4a1d-118">For more information, see [Create an Azure Batch account using the Azure portal](batch-account-create-portal.md) and [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="b4a1d-119">Создание и удаление учетных записей пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b4a1d-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="b4a1d-120">Как упоминалось выше, одной из основных функций API управления пакетной службой является возможность создания и удаления учетных записей пакетной службы в определенном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-120">As mentioned, one of the primary features of the Batch Management API is to create and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="b4a1d-121">Для этого используйте методы [BatchManagementClient.Account.CreateAsync][net_create] и [DeleteAsync][net_delete], а также их синхронные аналоги.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-121">To do so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="b4a1d-122">В следующем фрагменте кода создается учетная запись, выполняется получение созданной учетной записи из пакетной службы, а затем она удаляется.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-122">The following code snippet creates an account, obtains the newly created account from the Batch service, and then deletes it.</span></span> <span data-ttu-id="b4a1d-123">В этом и других фрагментах кода, приведенных в этой статье, `batchManagementClient` представляет собой полностью инициализированный экземпляр [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-123">In this snippet and the others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get the new account from the Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete the account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="b4a1d-124">Приложениям, использующим библиотеку .NET для управления пакетной службой и класс BatchManagementClient, необходимы права **администратора службы** или **соадминистратора** для доступа к подписке, которой принадлежит управляемая учетная запись пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-124">Applications that use the Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access to the subscription that owns the Batch account to be managed.</span></span> <span data-ttu-id="b4a1d-125">Дополнительные сведения можно получить, ознакомившись с разделом [Azure Active Directory](#azure-active-directory) ниже и примером кода [AccountManagement][acct_mgmt_sample].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-125">For more information, see the [Azure Active Directory](#azure-active-directory) section and the [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="b4a1d-126">Получение и повторное создание ключей учетных записей</span><span class="sxs-lookup"><span data-stu-id="b4a1d-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="b4a1d-127">Получите первичный и вторичный ключи из любой учетной записи пакетной службы в своей подписке с помощью метода [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="b4a1d-128">Для повторного создания этих ключей используется метод [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print the primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate the primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="b4a1d-129">Вы можете упростить процедуру подключения в своем приложении для управления.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="b4a1d-130">Сначала получите ключ учетной записи пакетной службы, которой вы хотите управлять, с помощью метода [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-130">First, obtain an account key for the Batch account you wish to manage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="b4a1d-131">Затем используйте этот ключ при инициализации класса [BatchSharedKeyCredentials][net_sharedkeycred] библиотеки .NET пакетной службы, который применяется при инициализации [BatchClient][net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-131">Then, use this key when initializing the Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="b4a1d-132">Проверка подписки Azure и квот учетной записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b4a1d-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="b4a1d-133">Подписки Azure и отдельные службы Azure, такие как пакетная служба, имеют стандартные квоты для ограничения количества определенных в них сущностей.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-133">Azure subscriptions and the individual Azure services like Batch all have default quotas that limit the number of certain entities within them.</span></span> <span data-ttu-id="b4a1d-134">Квоты по умолчанию для подписок Azure см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="b4a1d-134">For the default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="b4a1d-135">Квоты пакетной службы по умолчанию см. в статье [Квоты и ограничения пакетной службы Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="b4a1d-135">For the default quotas of the Batch service, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="b4a1d-136">С помощью библиотеки .NET для управления пакетной службой можно проверять эти квоты в приложениях.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-136">By using the Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="b4a1d-137">Это позволяет принимать решения о выделении ресурсов перед добавлением учетных записей или вычислительных ресурсов, таких как пулы и вычислительные узлы.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-137">This enables you to make allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="b4a1d-138">Определение квот для учетной записи пакетной службы в подписке Azure</span><span class="sxs-lookup"><span data-stu-id="b4a1d-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="b4a1d-139">Прежде чем создавать учетную запись пакетной службы в определенном регионе, вы можете проверить данные подписки Azure, чтобы узнать о возможности создания учетной записи в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-139">Before creating a Batch account in a region, you can check your Azure subscription to see whether you are able to add an account in that region.</span></span>

<span data-ttu-id="b4a1d-140">В следующем фрагменте кода мы сначала используем метод [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts], чтобы получить коллекцию всех учетных записей пакетной службы в подписке.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-140">In the code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] to get a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="b4a1d-141">После получения этой коллекции мы определяем количество учетных записей в целевом регионе.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-141">Once we've obtained this collection, we determine how many accounts are in the target region.</span></span> <span data-ttu-id="b4a1d-142">Затем мы используем метод [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] для получения квоты учетной записи пакетной службы и определения количества учетных записей, которые могут создаваться в этом регионе (если таковые имеются).</span><span class="sxs-lookup"><span data-stu-id="b4a1d-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] to obtain the Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within the subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within the target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get the account quota for the specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in the target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in the {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="b4a1d-143">В приведенном выше фрагменте `creds` является экземпляром [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-143">In the snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="b4a1d-144">Пример создания этого объекта см. в примере [AccountManagement][acct_mgmt_sample] на GitHub.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-144">To see an example of creating this object, see the [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="b4a1d-145">Определение квоты вычислительных ресурсов для учетной записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b4a1d-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="b4a1d-146">Прежде чем увеличивать количество вычислительных ресурсов в решении пакетной службы, убедитесь, что выделяемые ресурсы не превысят квоты для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-146">Before increasing compute resources in your Batch solution, you can check to ensure the resources you want to allocate won't exceed the account's quotas.</span></span> <span data-ttu-id="b4a1d-147">В следующем фрагменте кода мы выводим сведения о квотах для учетной записи пакетной службы с именем `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-147">In the code snippet below, we print the quota information for the Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="b4a1d-148">В своем приложении с помощью этих сведений можно определить, способна ли учетная запись обрабатывать дополнительные ресурсы, которые вы хотите создать.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-148">In your own application, you could use such information to determine whether the account can handle the additional resources to be created.</span></span>

```csharp
// First obtain the Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print the compute resource quotas for the account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="b4a1d-149">Несмотря на наличие стандартных квот для подписок и служб Azure, многие из ограничений можно увеличить путем создания соответствующего запроса на [портале Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in the [Azure portal][azure_portal].</span></span> <span data-ttu-id="b4a1d-150">В качестве примера обратитесь к инструкциям по увеличению квот для учетной записи пакетной службы в статье [Квоты и ограничения пакетной службы Azure](batch-quota-limit.md) .</span><span class="sxs-lookup"><span data-stu-id="b4a1d-150">For example, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="b4a1d-151">Использование Azure AD с библиотекой .NET для управления пакетной службой</span><span class="sxs-lookup"><span data-stu-id="b4a1d-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="b4a1d-152">Данная библиотека является клиентом поставщика ресурсов Azure и используется совместно с [Azure Resource Manager][resman_overview] для программного управления ресурсами учетных записей.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-152">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage account resources programmatically.</span></span> <span data-ttu-id="b4a1d-153">Служба Azure AD необходима для аутентификации запросов, выполненных с помощью любого клиента поставщика ресурсов Azure, а также библиотеки .NET для управления пакетной службой и [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-153">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="b4a1d-154">Сведения об использовании Azure AD с библиотекой .NET для управления пакетной службой см. в разделе [Authenticate from Batch solutions with Active Directory](batch-aad-auth.md) (Аутентификация решений пакетной службы в Active Directory).</span><span class="sxs-lookup"><span data-stu-id="b4a1d-154">For information about using Azure AD with the Batch Management .NET library, see [Use Azure Active Directory to authenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="b4a1d-155">Пример проекта на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="b4a1d-155">Sample project on GitHub</span></span>

<span data-ttu-id="b4a1d-156">Работу библиотеки .NET для управления пакетной службой можно посмотреть на примере проекта [AccountManagment][acct_mgmt_sample] на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-156">To see Batch Management .NET in action, check out the [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="b4a1d-157">В примере приложения AccountManagment демонстрируются следующие операции.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-157">The AccountManagment sample application demonstrates the following operations:</span></span>

1. <span data-ttu-id="b4a1d-158">Получение маркера безопасности из Active Directory Azure с помощью библиотеки [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="b4a1d-159">Если пользователь не выполнил вход, ему будет предложено ввести учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-159">If the user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="b4a1d-160">Создание [SubscriptionClient][resman_subclient] для отправки запроса к Azure на получение списка подписок, связанных с учетной записью, с помощью маркера безопасности, полученного из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-160">With the security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] to query Azure for a list of subscriptions associated with the account.</span></span> <span data-ttu-id="b4a1d-161">Пользователь может выбрать подписку из списка, если он содержит более одной подписки.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-161">The user can select a subscription from the list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="b4a1d-162">Получение учетных данных, связанных с выбранной подпиской.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-162">Get credentials associated with the selected subscription.</span></span>
4. <span data-ttu-id="b4a1d-163">Создание объекта [ResourceManagementClient][resman_client] с использованием учетных данных.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-163">Create a [ResourceManagementClient][resman_client] object by using the credentials.</span></span>
5. <span data-ttu-id="b4a1d-164">Создание группы ресурсов с помощью объекта [ResourceManagementClient][resman_client].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-164">Use a [ResourceManagementClient][resman_client] object to create a resource group.</span></span>
6. <span data-ttu-id="b4a1d-165">Выполнение нескольких операций с учетной записью пакетной службы с помощью объекта [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-165">Use a [BatchManagementClient][net_mgmt_client] object to perform several Batch account operations:</span></span>
   * <span data-ttu-id="b4a1d-166">Создание учетной записи пакетной службы в новой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-166">Create a Batch account in the new resource group.</span></span>
   * <span data-ttu-id="b4a1d-167">Получение созданной учетной записи из пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-167">Get the newly created account from the Batch service.</span></span>
   * <span data-ttu-id="b4a1d-168">Вывод ключей учетной записи для новой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-168">Print the account keys for the new account.</span></span>
   * <span data-ttu-id="b4a1d-169">Повторное создание первичного ключа для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-169">Regenerate a new primary key for the account.</span></span>
   * <span data-ttu-id="b4a1d-170">Вывод сведений о квотах для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-170">Print the quota information for the account.</span></span>
   * <span data-ttu-id="b4a1d-171">Вывод сведений о квотах для подписки.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-171">Print the quota information for the subscription.</span></span>
   * <span data-ttu-id="b4a1d-172">Вывод всех учетных записей в подписке.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-172">Print all accounts within the subscription.</span></span>
   * <span data-ttu-id="b4a1d-173">Удаление созданной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-173">Delete newly created account.</span></span>
7. <span data-ttu-id="b4a1d-174">Удалите ее.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-174">Delete the resource group.</span></span>

<span data-ttu-id="b4a1d-175">Перед удалением новой учетной записи пакетной службы или группы ресурсов вы можете просмотреть их на [портале Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="b4a1d-175">Before deleting the newly created Batch account and resource group, you can view them in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="b4a1d-176">Для успешного выполнения примера приложения необходимо зарегистрировать его в клиенте Azure AD на портале Azure и предоставить разрешения для API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b4a1d-176">To run the sample application successfully, you must first register it with your Azure AD tenant in the Azure portal and grant permissions to the Azure Resource Manager API.</span></span> <span data-ttu-id="b4a1d-177">Выполните инструкции, описанные в статье [Аутентификация решений по управлению пакетной службой с помощью Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="b4a1d-177">Follow the steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


<span data-ttu-id="b4a1d-178">[aad_about]: ../active-directory/active-directory-whatis.md "Что такое Microsoft Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="b4a1d-178">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="b4a1d-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Сценарии аутентификации в Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="b4a1d-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="b4a1d-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Интеграция приложений с Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="b4a1d-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
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
