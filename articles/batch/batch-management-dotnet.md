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
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a>Управление учетными записями пакетной и квоты с hello пакета управления клиентской библиотеки для .NET

> [!div class="op_single_selector"]
> * [Портал Azure](batch-account-create-portal.md)
> * [Библиотека .NET для управления пакетной службой](batch-management-dotnet.md)
> 
> 

Можно понизить обслуживания издержек в приложениях пакетной службы Azure с помощью hello [пакета управления .NET] [ api_mgmt_net] библиотеки tooautomate пакетной учетной записи создание, удаление, управление ключами и обнаружения квоты.

* **Создание и удаление учетных записей пакетной службы** в любом регионе. Если, например, как независимый поставщик программного (обеспечения ISV) предоставляет службы для клиентов в которых каждый назначается отдельной учетной записи пакета для выставления счетов, можно добавить портал учетных записей создание и удаление возможности tooyour клиента.
* **Получение и повторное создание ключей учетных записей** для всех учетных записей пакетной службы программным образом. Это особенно удобно для обеспечения соответствия политикам безопасности, которые могут требовать периодической смены ключей и определять сроки действия ключей учетных записей. Если у вас есть несколько учетных записей пакетной службы в разных регионах Azure, автоматизация смены ключей повысит эффективность вашего решения.
* **Проверьте учетную запись квоты** и принимать hello организации проб и ошибок и определения, имеют какие ограничений, какие учетные записи пакета. Проверка квот учетной записи до запуска заданий, создание пулов или добавление вычислительных узлов позволит вам заранее выбирать время и место создания вычислительных ресурсов. Вы можете определить учетные записи, требующие повышения квот, прежде чем выделить дополнительные ресурсы в этих учетных записях.
* **Объединить возможности других служб Azure** взаимодействие полнофункционального управления — с помощью пакета управления .NET, [Azure Active Directory][aad_about]и hello [Azure Диспетчер ресурсов] [ resman_overview] вместе в hello того же приложения. С помощью этих функций и их интерфейсы API, можно полноценного издержками проверки подлинности, hello toocreate возможности и удаления группы ресурсов и возможности hello, описанных выше для решения управления начала до конца.

> [!NOTE]
> Хотя данная статья посвящена hello программное управление учетными записями, ключи и квоты пакета, можно выполнять многие из этих действий с помощью hello [портал Azure][azure_portal]. Дополнительные сведения см. в разделе [создать учетную запись пакетной службы Azure с помощью портала Azure hello](batch-account-create-portal.md) и [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md).
> 
> 

## <a name="create-and-delete-batch-accounts"></a>Создание и удаление учетных записей пакетной службы
Как уже упоминалось, одной из функций hello основной hello API управления пакета является toocreate и удалять учетные записи пакета в регионе Azure. Таким образом, используйте toodo [BatchManagementClient.Account.CreateAsync] [ net_create] и [DeleteAsync][net_delete], или их синхронных аналогов.

Hello следующий фрагмент кода создает учетную запись, получает вновь созданные учетной записи из hello пакетная служба hello, а затем удаляет его. В этом фрагменте кода и hello другим пользователям в этой статье `batchManagementClient` — это полностью инициализированный экземпляр [BatchManagementClient][net_mgmt_client].

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
> Требуется для приложений, использующих библиотеки пакета управления .NET hello и его класс BatchManagementClient **администратора службы** или **coadministrator** получить доступ к подписке toohello, которому принадлежит hello Управлять toobe пакетной учетной записи. Дополнительные сведения см. в разделе hello [Azure Active Directory](#azure-active-directory) раздел и hello [AccountManagement] [ acct_mgmt_sample] образец кода.
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a>Получение и повторное создание ключей учетных записей
Получите первичный и вторичный ключи из любой учетной записи пакетной службы в своей подписке с помощью метода [ListKeysAsync][net_list_keys]. Для повторного создания этих ключей используется метод [RegenerateKeyAsync][net_regenerate_keys].

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
> Вы можете упростить процедуру подключения в своем приложении для управления. Во-первых, получить ключ учетной записи для учетной записи пакетной hello нужно toomanage с [ListKeysAsync][net_list_keys]. Затем используйте этот ключ при инициализации библиотеки .NET пакета hello [BatchSharedKeyCredentials] [ net_sharedkeycred] класс, который используется при инициализации [BatchClient] [net_batch_client].
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a>Проверка подписки Azure и квот учетной записи пакетной службы
Подписки Azure и hello отдельных служб Azure, как все пакета имеют квот по умолчанию, максимальное число сущностей, определенных в них hello. Hello квоты по умолчанию для подписок Azure, в разделе [подписка Azure и ограничения служб, квоты и ограничения](../azure-subscription-service-limits.md). Квоты по умолчанию hello hello пакетная служба, в разделе [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md). С помощью библиотеки .NET пакета управления hello, можно проверить эти квоты в ваших приложениях. Это позволит вам решений по распределению toomake перед добавлением учетных записей или вычислительные ресурсы, такие как пулы и вычислительных узлов.

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a>Определение квот для учетной записи пакетной службы в подписке Azure
Перед созданием пакетную учетную запись в области, можно проверить вашей подписки Azure toosee ли вы могли tooadd учетную запись в этом регионе.

В приведенном ниже фрагменте кода hello, сначала используется [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget коллекцию все учетные записи пакета, которые находятся в пределах подписки. После получения этой коллекции мы мы определили сколько учетных записей в целевой области hello. Затем мы используем [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain hello Квота пакетной учетной записи и определите, сколько учетных записей (если таковые имеются), которые могут создаваться в этом регионе.

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

В приведенном выше фрагменте hello `creds` является экземпляром класса [TokenCloudCredentials][azure_tokencreds]. toosee пример создания этого объекта. в разделе hello [AccountManagement] [ acct_mgmt_sample] образец кода на сайте GitHub.

### <a name="check-a-batch-account-for-compute-resource-quotas"></a>Определение квоты вычислительных ресурсов для учетной записи пакетной службы
Перед увеличением вычислительные ресурсы в пакет решения, можно проверить tooensure hello ресурсов, tooallocate не будет превышать квоты hello учетной записи. В приведенном ниже фрагменте кода hello, мы печати hello данные квоты для hello пакетной учетной записи с именем `mybatchaccount`. В приложении можно использовать такие сведения toodetermine ли hello учетной записи может обрабатывать toobe дополнительные ресурсы hello создан.

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
> Хотя по умолчанию квоты для подписки Azure и служб, многие из этих ограничений может быть повышен путем выполнения запроса в hello [портал Azure][azure_portal]. Например, в разделе [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md) инструкции об увеличении квот пакетной учетной записи.
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a>Использование Azure AD с библиотекой .NET для управления пакетной службой

Библиотека пакета управления .NET Hello является клиента поставщика ресурсов Azure и используется вместе с [диспетчера ресурсов Azure] [ resman_overview] toomanage записи ресурсам программными средствами. Azure AD — необходимые tooauthenticate запросов, выполненных при помощи любого клиента поставщика ресурсов Azure, включая библиотеку .NET пакета управления hello, а по [диспетчера ресурсов Azure][resman_overview]. Сведения об использовании Azure AD с библиотекой hello пакета управления .NET см. в разделе [использование Azure Active Directory tooauthenticate пакета решения](batch-aad-auth.md). 

## <a name="sample-project-on-github"></a>Пример проекта на сайте GitHub

toosee пакета управления .NET в действии, извлечь hello [AccountManagment] [ acct_mgmt_sample] примера проекта на GitHub. AccountManagment пример приложения Hello демонстрирует hello следующие операции:

1. Получение маркера безопасности из Active Directory Azure с помощью библиотеки [ADAL][aad_adal]. Если пользователь hello не уже выполнил вход, запрос для своих учетных данных Azure.
2. С помощью маркера безопасности hello, полученный из Azure AD, создавать [SubscriptionClient] [ resman_subclient] tooquery Azure список подписок, связанных с учетной записью hello. Hello пользователь может выбрать подписку из списка hello, если он содержит более одной подписки.
3. Получите учетные данные, связанные с hello выбранной подписки.
4. Создание [ResourceManagementClient] [ resman_client] объекта с использованием учетных данных hello.
5. Используйте [ResourceManagementClient] [ resman_client] объекта toocreate группу ресурсов.
6. Используйте [BatchManagementClient] [ net_mgmt_client] объекта tooperform несколько операций пакетной учетной записи:
   * Создайте учетную запись пакета в новую группу ресурсов hello.
   * Получение hello вновь созданные учетной записи из hello пакетной службы.
   * Здравствуй, мир ключи учетной записи для новой учетной записи hello.
   * Повторно создать новый первичный ключ для учетной записи hello.
   * Сведения о квоте Здравствуй, мир hello учетной записи.
   * Здравствуй, мир данные квоты для подписки hello.
   * Печать всех учетных записей в рамках подписки hello.
   * Удаление созданной учетной записи.
7. Удалите группу ресурсов hello.

Перед удалением группы учетных записей и ресурсов пакета только что созданный hello, их можно просмотреть в hello [портал Azure][azure_portal]:

Пример приложения hello toorun успешно, необходимо сначала зарегистрировать его с вашим клиентом Azure AD в hello Azure portal и предоставьте разрешения toohello API диспетчера ресурсов Azure. Выполните шаги hello в [решения для проверки подлинности пакета управления с помощью Active Directory](batch-aad-auth-management.md).


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
