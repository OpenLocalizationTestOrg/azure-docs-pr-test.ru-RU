---
title: "Кэш Redis для Azure с помощью Azure PowerShell aaaManage | Документы Microsoft"
description: "Узнайте, как tooperform административных задач для кэша Redis для Azure с помощью Azure PowerShell."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a>Управление кэшем Redis для Azure с использованием Azure PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Интерфейс командной строки Azure](cache-manage-cli.md)
> 
> 

В этом разделе показано, как tooperform общие задачи, такие как создание, обновление и масштабирования ваших экземпляров кэша Redis для Azure как tooregenerate клавиши доступа и как tooview сведения о ваших кэшей. См. полный список [командлетов PowerShell для работы с кэшем Redis для Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

Дополнительные сведения о hello классической модели развертывания см. в разделе [диспетчера ресурсов Azure и классическое развертывание: Обзор модели развертывания и hello состояния ресурсов](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).

## <a name="prerequisites"></a>Предварительные требования
Если вы уже установили Azure PowerShell, необходимо использовать Azure PowerShell 1.0.0 или более поздней версии. Можно проверить версию hello Azure PowerShell, установленный с помощью этой команды в командной строке Azure PowerShell hello.

    Get-Module azure | format-table version


Во-первых необходимо войти в tooAzure с помощью этой команды.

    Login-AzureRmAccount

Укажите адрес электронной почты hello учетную запись Azure и пароль в диалоговом окне приветствия вход в Microsoft Azure.

Затем Если у вас несколько подписок Azure, следует записать tooset подписки Azure. toosee список ваши текущие подписки, выполните следующую команду.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify подписка hello, запустите следующую команду hello. В следующем примере hello, — имя подписки hello `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

Прежде чем использовать Windows PowerShell с помощью диспетчера ресурсов Azure, требуется hello следующее:

* Windows PowerShell версии 3.0 или 4.0. toofind hello версии Windows PowerShell, введите:`$PSVersionTable` и проверьте значение hello `PSVersion` 3.0 или 4.0. tooinstall совместимую версию в разделе [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) или [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

tooget подробную справку для любого командлета, отображаемые в этом учебнике, используйте командлет Get-Help hello.

    Get-Help <cmdlet-name> -Detailed

Например, tooget справку для hello `New-AzureRmRedisCache` командлета введите:

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a>Как tooconnect tooother облака
По умолчанию hello Azure — среды `AzureCloud`, которое представляет hello облако Azure как глобальный экземпляр. другой экземпляр tooa tooconnect, используйте hello `Add-AzureRmAccount` с hello `-Environment` или -`EnvironmentName` переключатель командной строки с требуемой среде hello или имя среды.

Список доступных сред, запустите hello hello toosee `Get-AzureRmEnvironment` командлета.

### <a name="tooconnect-toohello-azure-government-cloud"></a>tooconnect toohello облако Azure государственных организаций
toohello tooconnect государственных облако Azure, выполните одну из следующих команд hello.

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

или

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

toocreate кэша в hello государственных облако Azure, используйте один из следующих элементов hello.

* Правительство штата Вирджиния
* Правительство штата Айова

Дополнительные сведения о hello государственных облако Azure. в разделе [Microsoft Azure для государственных](https://azure.microsoft.com/features/gov/) и [руководстве разработчика Microsoft Azure государственных](../azure-government-developer-guide.md).

### <a name="tooconnect-toohello-azure-china-cloud"></a>tooconnect toohello Китая облако Azure
toohello tooconnect облако Azure Китая, используйте один из следующих команд hello.

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

или

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

toocreate кэша в облако Azure Китая, используйте один из следующих элементов hello hello.

* Восток Китая
* Север Китая

Дополнительные сведения о hello облако Azure China. в разделе [AzureChinaCloud для Azure обслуживается 21Vianet в Китае](http://www.windowsazure.cn/).

### <a name="tooconnect-toomicrosoft-azure-germany"></a>tooconnect tooMicrosoft Германия Azure
tooMicrosoft tooconnect Германии Azure, выполните одну из следующих команд hello.

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


или

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

toocreate кэша в Германии Microsoft Azure, используйте одну из следующих ссылок hello.

* Центральная Германия
* Северо-восточная Германия

Дополнительные сведения о Microsoft Azure для Германии см. [здесь](https://azure.microsoft.com/overview/clouds/germany/).

### <a name="properties-used-for-azure-redis-cache-powershell"></a>Свойства, используемые в командлетах PowerShell кэша Redis для Azure
в следующей таблице Hello содержит свойства и описания для часто используемых параметров при создании и управления экземплярами кэша Redis для Azure с помощью Azure PowerShell.

| Параметр | Описание | значение по умолчанию |
| --- | --- | --- |
| Имя |Имя кэша hello | |
| Расположение |Расположение кэша hello | |
| ResourceGroupName |Имя группы ресурсов, в какой кэш toocreate hello | |
| Размер |размер кэша hello Hello. Допустимые значения: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 МБ, 1 ГБ, 2,5 ГБ, 6 ГБ, 13 ГБ, 26 ГБ, 53 ГБ |1 ГБ |
| ShardCount |Количество сегментов toocreate при создании кэша premium с включенной кластеризацией Hello. Допустимые значения: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 | |
| SKU |Указывает hello SKU hello кэша. Допустимые значения: Basic, Standard, Premium |Стандарт |
| RedisConfiguration |Задает параметры конфигурации кластера Redis. Сведения о каждом параметре см. ниже hello [RedisConfiguration свойства](#redisconfiguration-properties) таблицы. | |
| EnableNonSslPort |Указывает, включен ли hello не SSL-порт. |Ложь |
| MaxMemoryPolicy |Этот параметр устарел, вместо него используется параметр RedisConfiguration. | |
| StaticIP |При размещении вашего кэша в виртуальной сети, указывает уникальный IP-адрес в подсети hello для кэша hello. Если не указано, одна из подсети hello выбирается автоматически. | |
| Подсеть |При размещении вашего кэша в виртуальной сети, указывает имя hello hello подсети, в какой кэш toodeploy hello. | |
| Виртуальная сеть |Если размещение кэша в виртуальной сети, задает идентификатор ресурса hello hello виртуальной сети, в какой кэш toodeploy hello. | |
| KeyType |Указывает, какой ключ доступа tooregenerate при обновлении ключей доступа. Допустимые значения: Primary, Secondary | |

### <a name="redisconfiguration-properties"></a>Свойства RedisConfiguration
| Свойство | Описание | Ценовые категории |
| --- | --- | --- |
| rdb-backup-enabled |Указывает на то, включен ли параметр [Сохраняемость данных Redis](cache-how-to-premium-persistence.md) . |Только "Премиум" |
| rdb-storage-connection-string |Здравствуйте, учетная запись хранения строки подключения с toohello для [сохраняемости данных Redis](cache-how-to-premium-persistence.md) |Только "Премиум" |
| rdb-backup-frequency |Здравствуйте, интервал резервного копирования для [сохраняемости данных Redis](cache-how-to-premium-persistence.md) |Только "Премиум" |
| maxmemory-reserved |Настраивает hello [памяти, зарезервированной](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) для процессов не из кэша |"Стандартный" и "Премиум" |
| maxmemory-policy |Настраивает hello [политика вытеснения](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) для кэша hello |Все ценовые категории |
| notify-keyspace-events |Настраивает [уведомления пространства ключей](cache-configure.md#keyspace-notifications-advanced-settings) |"Стандартный" и "Премиум" |
| hash-max-ziplist-entries |Настраивает [оптимизацию памяти](http://redis.io/topics/memory-optimization) для небольших сводных данных. |"Стандартный" и "Премиум" |
| hash-max-ziplist-value |Настраивает [оптимизацию памяти](http://redis.io/topics/memory-optimization) для небольших сводных данных. |"Стандартный" и "Премиум" |
| set-max-intset-entries |Настраивает [оптимизацию памяти](http://redis.io/topics/memory-optimization) для небольших сводных данных. |"Стандартный" и "Премиум" |
| zset-max-ziplist-entries |Настраивает [оптимизацию памяти](http://redis.io/topics/memory-optimization) для небольших сводных данных. |"Стандартный" и "Премиум" |
| zset-max-ziplist-value |Настраивает [оптимизацию памяти](http://redis.io/topics/memory-optimization) для небольших сводных данных. |"Стандартный" и "Премиум" |
| databases |Настраивает hello число баз данных. Это свойство можно настроить только в момент создания кэша. |"Стандартный" и "Премиум" |

## <a name="toocreate-a-redis-cache"></a>toocreate кэша Redis
Создаются новые экземпляры кэша Redis для Azure с помощью hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) командлета.

> [!IMPORTANT]
> Hello первом создании кэша Redis в подписку с помощью портала Azure hello hello портала регистрирует hello `Microsoft.Cache` пространство имен для этой подписки. При попытке toocreate hello сначала Redis кэша в подписке с помощью PowerShell, необходимо сначала зарегистрировать это пространство имен, используя следующую команду; hello в противном случае командлеты, такие как `New-AzureRmRedisCache` и `Get-AzureRmRedisCache` ошибкой.
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

Список доступных параметров и их описания для toosee `New-AzureRmRedisCache`, запустите hello следующую команду.

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

toocreate кэш с параметрами по умолчанию, запустите следующую команду hello.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

`ResourceGroupName`, `Name`, и `Location` являются обязательными параметрами, но hello rest являются необязательными и принимают значения по умолчанию. Запущена предыдущая команда hello создает экземпляр кэша Redis для Azure стандартные SKU с указанным именем hello, расположение и группу ресурсов, составляет 1 ГБ емкости hello не SSL-порт отключен.

размер P1 (6 ГБ — 60 ГБ), P2 (13-130 ГБ), укажите toocreate кэша premium P3 (26-260 ГБ), или P4 (53-530 ГБ). tooenable кластеризации, укажите количество сегментов, с помощью hello `ShardCount` параметра. Hello следующий пример создает кэша premium P1 с 3 сегментов. Размера кэша premium P1 — 6 ГБ, размер, и поскольку мы указали, что три сегментов hello общий размер 18 ГБ (3 x 6 ГБ).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

toospecify значения для hello `RedisConfiguration` параметра, заключите hello значения внутри `{}` как ключ значение как пары `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`. Hello следующий пример создает стандартный 1 ГБ кэша с `allkeys-random` maxmemory политики и пространство ключей уведомлений, настроенной с `KEA`. Дополнительные сведения см. в разделах [Уведомления пространства ключей (дополнительные параметры)](cache-configure.md#keyspace-notifications-advanced-settings) и [Политики памяти](cache-configure.md#memory-policies).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a>hello tooconfigure баз данных, можно задать во время создания кэша
Hello `databases` параметр можно настроить только во время создания кэша. Hello следующий пример создает premium P3 (26 ГБ) кэш с 48 баз данных, с помощью hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) командлета.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

Дополнительные сведения о hello `databases` свойство, в разделе [конфигурации сервера по умолчанию кэш Azure Redis](cache-configure.md#default-redis-server-configuration). Дополнительные сведения о создании кэша с использованием hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) командлета, см. предыдущие hello [toocreate кэша Redis](#to-create-a-redis-cache) раздела.

## <a name="tooupdate-a-redis-cache"></a>tooupdate кэш Redis
Экземпляры кэша Redis для Azure обновляются с помощью hello [AzureRmRedisCache набор](https://msdn.microsoft.com/library/azure/mt634518.aspx) командлета.

Список доступных параметров и их описания для toosee `Set-AzureRmRedisCache`, запустите hello следующую команду.

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Hello `Set-AzureRmRedisCache` командлет можно использовать tooupdate свойств, таких как `Size`, `Sku`, `EnableNonSslPort`и hello `RedisConfiguration` значения. 

Hello следующую команду, что политика максимальной памяти для кэша Redis hello hello обновления с именем myCache.

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a>tooscale кэш Redis
`Set-AzureRmRedisCache`может быть tooscale используется экземпляр кэша redis для Azure — при hello `Size`, `Sku`, или `ShardCount` свойства изменяются. 

> [!NOTE]
> Масштабирование кэша, с помощью PowerShell — тема toohello такие же ограничения и правила, что масштабирование кэша из hello портал Azure. Можно масштабировать tooa различных ценовой категории с hello следующие ограничения.
> 
> * Нельзя масштабировать из выше ценовой уровень tooa ниже ценовой категории.
> * Нельзя масштабировать из **Premium** кэша вниз tooa **Стандартная** или **основные** кэша.
> * Нельзя масштабировать из **Стандартная** кэша вниз tooa **основные** кэша.
> * Можно масштабировать от **основные** кэшировать tooa **Стандартная** кэш, но не может изменить размер hello в hello то же время. Если требуется другой размер, можно сделать последующих размер toohello требуемой операции масштабирования.
> * Нельзя масштабировать из **основные** кэшировать непосредственно tooa **Premium** кэша. Требуется расширение из **основные** слишком**Стандартная** за одну операцию масштабирования, а затем с **Стандартная** слишком**Premium** последующих масштабирования операция.
> * Нельзя масштабировать от большего вниз toohello **C0 (250 МБ)** размер.
> 
> Дополнительные сведения см. в разделе [как tooScale Redis для Azure кэшировать](cache-how-to-scale.md).
> 
> 

Hello следующем примере показано, как tooscale кэш именоваться `myCache` tooa 2,5 ГБ кэша. Обратите внимание, что команда будет работать в кэше уровня "Базовый" или "Стандартный".

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

После этого команды, возвращается состояние hello hello кэша (аналогично toocalling `Get-AzureRmRedisCache`). Обратите внимание, что hello `ProvisioningState` — `Scaling`.

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

По завершении hello операция масштабирования hello `ProvisioningState` изменяет слишком`Succeeded`. При необходимости toomake последующей операции масштабирования, таких как изменение из основных tooStandard и затем изменив размер hello, необходимо дождаться завершения предыдущей операции hello или появится ошибка примерно toohello следующее.

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a>tooget сведения о кэше Redis
Можно получить сведения о кэше, используя hello [Get AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) командлета.

Список доступных параметров и их описания для toosee `Get-AzureRmRedisCache`, запустите hello следующую команду.

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Запустите tooreturn сведения о всех кэшей в текущей подписке hello, `Get-AzureRmRedisCache` без параметров.

    Get-AzureRmRedisCache

Запустите tooreturn сведения о всех кэшей в определенной группе ресурсов, `Get-AzureRmRedisCache` с hello `ResourceGroupName` параметра.

    Get-AzureRmRedisCache -ResourceGroupName myGroup

Запустите tooreturn сведения о конкретных кэш, `Get-AzureRmRedisCache` с hello `Name` параметр, содержащий имя hello кэша hello и hello `ResourceGroupName` параметр с группой ресурсов hello, содержащей этот кэш.

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a>клавиши доступа hello tooretrieve для кэша Redis
tooretrieve hello ключи доступа для кэша, можно использовать hello [Get AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) командлета.

Список доступных параметров и их описания для toosee `Get-AzureRmRedisCacheKey`, запустите hello следующую команду.

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

tooretrieve hello ключи для кэша, вызов hello `Get-AzureRmRedisCacheKey` командлета и передайте имя hello кэша hello имя группы ресурсов hello, содержащий кэш hello.

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a>tooregenerate клавиши доступа для кэша Redis
tooregenerate hello ключи доступа для кэша, можно использовать hello [New AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) командлета.

Список доступных параметров и их описания для toosee `New-AzureRmRedisCacheKey`, запустите hello следующую команду.

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

tooregenerate hello первичный или вторичный ключ для кэша, вызов hello `New-AzureRmRedisCacheKey` командлета передайте hello, группа ресурсов и имя либо укажите `Primary` или `Secondary` для hello `KeyType` параметра. В следующем примере hello генерируется hello вторичный ключ доступа для кэша.

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a>toodelete кэш Redis
кэш Redis, toodelete использовать hello [AzureRmRedisCache удаление](https://msdn.microsoft.com/library/azure/mt634515.aspx) командлета.

Список доступных параметров и их описания для toosee `Remove-AzureRmRedisCache`, запустите hello следующую команду.

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

В следующем примере hello, hello кэша с именем `myCache` удаляется.

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a>tooimport кэш Redis
Можно импортировать данные в экземпляр кэша Redis для Azure, с помощью hello `Import-AzureRmRedisCache` командлета.

> [!IMPORTANT]
> Функция импорта и экспорта доступна только для кэшей категории [Премиум](cache-premium-tier-intro.md). Дополнительные сведения об импорте и экспорте см. в статье [Импорт и экспорт данных в кэше Redis для Azure](cache-how-to-import-export-data.md).
> 
> 

Список доступных параметров и их описания для toosee `Import-AzureRmRedisCache`, запустите hello следующую команду.

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello следующая команда импортирует данные из большого двоичного объекта hello указанного hello SAS uri в кэше Redis для Azure.

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a>tooexport кэш Redis
Можно экспортировать данные из экземпляра кэша Redis для Azure с помощью hello `Export-AzureRmRedisCache` командлета.

> [!IMPORTANT]
> Функция импорта и экспорта доступна только для кэшей категории [Премиум](cache-premium-tier-intro.md). Дополнительные сведения об импорте и экспорте см. в статье [Импорт и экспорт данных в кэше Redis для Azure](cache-how-to-import-export-data.md).
> 
> 

Список доступных параметров и их описания для toosee `Export-AzureRmRedisCache`, запустите hello следующую команду.

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello следующая команда экспортирует данные из экземпляра кэша Redis для Azure в контейнер hello указанного hello SAS uri.

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a>tooreboot кэш Redis
Можно перезагрузить экземпляр кэша Redis для Azure с помощью hello `Reset-AzureRmRedisCache` командлета.

> [!IMPORTANT]
> Функция перезагрузки доступна только для кэшей [уровня "Премиум"](cache-premium-tier-intro.md). Дополнительные сведения о перезапуске кэша см. в разделе [Reboot](cache-administration.md#reboot) статьи "Администрирование кэша Redis для Azure".
> 
> 

Список доступных параметров и их описания для toosee `Reset-AzureRmRedisCache`, запустите hello следующую команду.

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello следующая команда перезагружает обоих узлов hello указанного кэша.

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a>Дальнейшие действия
toolearn Подробнее об использовании Windows PowerShell с помощью Azure см. следующие ресурсы hello.

* [Документация по командлету кэша Redis для Azure на MSDN](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* [Командлеты диспетчера ресурсов Azure](http://go.microsoft.com/fwlink/?LinkID=394765): узнать toouse hello командлеты в модуле Azure Resource Manager hello.
* [С помощью ресурса группы toomanage ресурсам Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): Узнайте, как toocreate групп ресурсов в hello портал Azure и управление ими.
* [Блог Azure](http://blogs.msdn.com/windowsazure): узнайте о новых возможностях в Azure.
* [Блог Windows PowerShell](http://blogs.msdn.com/powershell): узнайте о новых возможностях в Windows PowerShell.
* [Блог "Hey, Scripting Блог](http://blogs.technet.com/b/heyscriptingguy/): получить советы реальных из hello сообщества Windows PowerShell.

