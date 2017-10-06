---
title: "Кэш Redis для Azure с помощью Azure CLI aaaManage | Документы Microsoft"
description: "Узнайте, как tooinstall hello Azure CLI на любой платформе как toouse его tooconnect tooyour учетная запись Azure и как toocreate и управлять кэша Redis с hello Azure CLI."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a>Как toocreate и управлять ими с помощью интерфейса командной строки Azure (Azure CLI) hello кэш Azure Redis
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Интерфейс командной строки Azure](cache-manage-cli.md)
>
>

Hello Azure CLI является хорошим способом toomanage инфраструктуры Azure с любой платформы. В этой статье показано, как toocreate и управлять ими с помощью Azure CLI hello экземплярами кэша Redis для Azure.

> [!NOTE]
> Эта статья относится tooa предыдущей версии Azure CLI. Hello последнюю Azure CLI 2.0 образцы скриптов см. в разделе [примеры кэша Azure CLI Redis](cli-samples.md).
> 
> 

## <a name="prerequisites"></a>Предварительные требования
toocreate и управления экземплярами кэша Redis для Azure, с помощью Azure CLI, необходимо выполнить следующие шаги hello.

* Необходимо иметь учетную запись Azure. Если ее нет, можно создать [бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/) всего за пару минут.
* [Установка hello Azure CLI](../cli-install-nodejs.md).
* Подключение установки Azure CLI с личной учетной записи Azure или с помощью рабочей или учебной учетной записи Azure, входить в систему с hello Azure CLI с помощью hello `azure login` команды. toounderstand hello различия и выберите см. в разделе [подключение tooan подписки Azure из hello Azure командной строки (CLI Azure)](../xplat-cli-connect.md).
* Прежде чем выполнять hello, следующие команды, переключение hello Azure CLI в режим диспетчера ресурсов, выполнив hello `azure config mode arm` команды. Дополнительные сведения см. в разделе [toomanage Azure CLI hello Azure использовать ресурсы и группы ресурсов](../xplat-cli-azure-resource-manager.md).

## <a name="redis-cache-properties"></a>Свойства кэша Redis
Hello используются следующие свойства при создании и обновлении экземпляров кэша Redis.

| Свойство | Switch | Описание |
| --- | --- | --- |
| name |-n, --name |Имя hello кэша Redis. |
| resource group |-g, --resource-group |Имя группы ресурсов hello. |
| location |-l, --location |Кэш toocreate расположения. |
| size |-z, --size |Размер кэша Redis hello. Допустимые значения: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
| sku |-x, --sku |Номер SKU Redis. Должен иметь одно из этих значений: [Basic, Standard, Premium] |
| EnableNonSslPort |-e, --enable-non-ssl-port |Свойство EnableNonSslPort hello кэша Redis. Если порт SSL не hello tooenable своего кэша, добавьте этот флаг |
| Конфигурация Redis |-c, --redis-configuration |Конфигурация Redis. Введите строку ключей и значений конфигурации в формате JSON. Формат:"{"":"","":""}" |
| Конфигурация Redis |-f, --redis-configuration-file |Конфигурация Redis. Введите путь hello файл, содержащий ключи и значения здесь. Формат для записи в файле hello: {»»: ««,»»:»»} |
| Число сегментов |-r, --shard-count |Количество сегментов toocreate кластера кэша Premium с кластеризацией. |
| Виртуальная сеть |-v, --virtual-network |Если размещение кэша в виртуальной сети, задает hello точное ARM идентификатор ресурса hello виртуальной сети toodeploy hello redis кэша в. Пример формата: /subscriptions/{идентификатор_подписки}/resourceGroups/{имя_группы_ресурсов}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| key type |-t, --key-type |Тип ключа toorenew. Допустимые значения: [Primary, Secondary]. |
| StaticIP |-p, --static-ip <static-ip> |При размещении вашего кэша в виртуальной сети, указывает уникальный IP-адрес в подсети hello для кэша hello. Если не указано, одна из подсети hello выбирается автоматически. |
| Подсеть |t, --subnet <subnet> |При размещении вашего кэша в виртуальной сети, указывает имя hello hello подсети, в какой кэш toodeploy hello. |
| Виртуальная сеть |-v, --virtual-network <virtual-network> |Если размещение кэша в виртуальной сети, задает hello точное ARM идентификатор ресурса hello виртуальной сети toodeploy hello redis кэша в. Пример формата: /subscriptions/{идентификатор_подписки}/resourceGroups/{имя_группы_ресурсов}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| Подписки |-s, --subscription |идентификатор подписки Hello. |

## <a name="see-all-redis-cache-commands"></a>Просмотр всех команд кэша Redis
toosee все команды кэша Redis и их параметров, используйте hello `azure rediscache -h` команды.

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a>Создание кэша Redis
toocreate кэша Redis, hello используйте следующую команду:

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

Дополнительные сведения об этой команде запуска hello `azure rediscache create -h` команды.

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a>Удаление существующего кэша Redis
toodelete кэша Redis, hello используйте следующую команду:

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

Дополнительные сведения об этой команде запуска hello `azure rediscache delete -h` команды.

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a>Вывод списка всех кэшей Redis в подписке или группе ресурсов
toolist всех кэшей Redis в вашей подписке или группе ресурсов, используйте hello следующую команду:

    azure rediscache list [options]

Дополнительные сведения об этой команде запуска hello `azure rediscache list -h` команды.

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a>Отображение свойств существующего кэша Redis
tooshow свойства для существующего кэша Redis, используйте hello следующую команду:

    azure rediscache show [--name <name> --resource-group <resource-group>]

Дополнительные сведения об этой команде запуска hello `azure rediscache show -h` команды.

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a>Изменение параметров существующего кэша Redis
Параметры toochange для существующего кэша Redis, используйте следующую команду hello.

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

Дополнительные сведения об этой команде запуска hello `azure rediscache set -h` команды.

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a>Обновить hello ключ проверки подлинности для существующего кэша Redis
ключ проверки подлинности hello toorenew для существующего кэша Redis, hello используйте следующую команду:

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

Укажите `Primary` или `Secondary` для `key-type`.

Дополнительные сведения об этой команде запуска hello `azure rediscache renew-key -h` команды.

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a>Вывод первичного и вторичного ключей существующего кэша Redis
toolist первичный и вторичный ключи для существующего кэша Redis, используйте hello следующую команду:

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

Дополнительные сведения об этой команде запуска hello `azure rediscache list-keys -h` команды.

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
