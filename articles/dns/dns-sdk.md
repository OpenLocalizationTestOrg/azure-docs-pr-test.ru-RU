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
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a>Создание зоны DNS и наборы записей с помощью hello .NET SDK

С помощью пакета SDK DNS с библиотекой .NET управления DNS можно автоматизировать операции toocreate, удаление или обновление зоны DNS, наборы записей и записи. Полный проект Visual Studio доступен [здесь](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True).

## <a name="create-a-service-principal-account"></a>Создание учетной записи субъекта-службы

Как правило программный доступ к ресурсам tooAzure предоставляется через выделенную учетную запись, а не учетные данные пользователя. Эти выделенные учетные записи называются учетными записями субъектов-служб. toouse hello Azure DNS SDK пример проекта, требуется toocreate учетную запись участника службы и назначьте его hello правильные разрешения.

1. Выполните [эти инструкции](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate учетную запись участника службы (пример проекта hello DNS Azure SDK предполагается проверки подлинности на основе пароля).
2. Создайте группу ресурсов (см. сведения [здесь](../azure-resource-manager/resource-group-template-deploy-portal.md)).
3. Используйте Azure RBAC toogrant hello учетная запись участника «Участник зоны DNS» разрешения toohello группа ресурсов службы ([Вот как](../active-directory/role-based-access-control-configure.md).)
4. При использовании примера проекта hello DNS Azure SDK, измените файл «program.cs» hello следующим образом:

   * Вставьте hello правильные значения для hello идентификатора клиента, clientId (также известный как идентификатор учетной записи), секретные данные (пароль учетная запись участника службы) и идентификатор подписки, как в шаге 1.
   * Введите имя группы ресурсов hello, выбранного в шаге 2.
   * Введите имя зоны DNS по своему выбору.

## <a name="nuget-packages-and-namespace-declarations"></a>Пакеты NuGet и объявления пространств имен

toouse hello Azure DNS .NET SDK необходимо tooinstall hello **Библиотека управления DNS Azure** пакета NuGet и другие необходимые пакеты Azure.

1. В **Visual Studio**, откройте существующий или новый проект.
2. Go слишком**средства**  **>**  **диспетчера пакетов NuGet**  **>**  **управление пакетами NuGet для Решения...** .
3. Нажмите кнопку **Обзор**, включите hello **включить предварительный выпуск** флажок и введите **Microsoft.Azure.Management.Dns** в поле поиска hello.
4. Выберите пакет hello и нажмите кнопку **установить** tooadd его tooyour проекта Visual Studio.
5. Повторите процесс hello выше hello установки tooalso следующие пакеты: **Microsoft.Rest.ClientRuntime.Azure.Authentication** и **Microsoft.Azure.Management.ResourceManager**.

## <a name="add-namespace-declarations"></a>Добавление объявлений пространств имен

Добавьте следующие объявления пространств имен hello

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a>Инициализировать клиент управления DNS hello

Hello *DnsManagementClient* содержит hello методы и свойства, необходимые для управления DNS-зон и наборы данных.  Hello следующий код входит учетная запись участника службы toohello и создает объект DnsManagementClient.

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a>Создание или обновление зоны DNS

toocreate зоны DNS, сначала объект «Зону» создается параметры зоны DNS toocontain hello. Поскольку зоны DNS определенного региона связанного tooa, too'global задано местоположение hello ". В этом примере [диспетчера ресурсов Azure «тег»](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) добавляется toohello зоны.

tooactually создать или обновить зону hello в Azure DNS, hello зоны объект, содержащий параметры зоны hello передается toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* метод.

> [!NOTE]
> DnsManagementClient поддерживает три режима работы: синхронные («CreateOrUpdate»), асинхронную («CreateOrUpdateAsync»), или асинхронном ответ toohello HTTP доступа (CreateOrUpdateWithHttpMessagesAsync).  Вы можете выбрать любой из этих режимов в зависимости от потребностей приложения.

Служба Azure DNS поддерживает оптимистичный параллелизм с помощью [тегов Etag](dns-getstarted-create-dnszone.md). В этом примере указания «*» для заголовка hello «If-None-Match» зону DNS сообщает toocreate Azure DNS, если еще не существует.  Hello Если возникнет ошибка зоны с помощью hello заданным именем уже существует в hello группы ресурсов.

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

## <a name="create-dns-record-sets-and-records"></a>Создание записей и наборов записей DNS

Записи DNS управляются как набор записей. Набор записей — это набор записей с hello таким же именем и запишите типа в пределах зоны.  Имя набора записей Hello toohello относительное имя зоны, не hello полное DNS-имя.

toocreate или обновить набор записей, объект параметров «Набор записей» создается и передается слишком*DnsManagementClient.RecordSets.CreateOrUpdateAsync*. С зонами DNS, имеется три режима работы: синхронные («CreateOrUpdate»), асинхронную («CreateOrUpdateAsync»), или асинхронном ответ toohello HTTP доступа (CreateOrUpdateWithHttpMessagesAsync).

Как и в случае с зонами DNS, операции с наборами записей поддерживают оптимистичный параллелизм.  В этом примере поскольку указаны не «If-Match» и «If-None-Match», hello набора записей создается всегда.  Этот вызов перезаписывает все существующие записей с hello таким же именем и запишите тип в этой зоне DNS.

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

## <a name="get-zones-and-record-sets"></a>Получение зон и наборов записей

Hello *DnsManagementClient.Zones.Get* и *DnsManagementClient.RecordSets.Get* получать отдельные зоны и наборы записей, соответственно. Наборы записей идентифицируются по их тип, имя и hello зоны и группе ресурсов которой находятся. Зоны идентифицируются по их группе ресурсов имя и hello, они существуют в.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a>Обновление имеющегося набора записей

tooupdate DNS-запись существующего набора, сначала получить набор записей hello, а затем обновить запись hello содержимое набора, а затем отправить изменения hello.  В этом примере мы указываем hello 'Etag' из hello получить запись, задайте в параметре «If-Match» hello. Hello вызов завершается сбоем, если параллельная операция изменил запись hello, пока задание в hello.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a>Вывод списка зон и наборов записей

использовать зоны toolist hello *DnsManagementClient.Zones.List...*  использовать методы, которые поддерживает список всех зон в данной группы ресурсов либо всех зон в наборы записей toolist подписки Azure (для ресурсов групп.), *DnsManagementClient.RecordSets.List...*  методы, которые поддерживает список всех наборов записей в данной зоны или только этих наборов записей определенного типа.

Обратите внимание, что при выводе списка зон и наборов записей может быть применена разбивка на страницы.  Следующий пример показывает как Hello tooiterate через hello страницы результатов. (Искусственно небольшой размер "2" является tooforce используется разбиение на страницы на практике этот параметр должен быть опущен и hello размер страницы по умолчанию, используемый.)

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

## <a name="next-steps"></a>Дальнейшие действия

Загрузите hello [пакета SDK .NET Azure DNS образец проекта](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), который включает дополнительные примеры как toouse hello SDK .NET Azure DNS, включая примеры для других типов записей DNS.
