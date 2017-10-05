---
title: "Управление кэшем Redis для Azure с помощью Azure CLI | Документация Майкрософт"
description: "Узнайте, как установить Azure CLI на любой платформе, как его использовать для подключения к учетной записи Azure и как с его помощью создать кэш Redis и управлять им."
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
ms.openlocfilehash: ba078a870a3998568170cc197bd6698b97b7fadb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-azure-redis-cache-using-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="13834-103">Как создать кэш Redis для Azure и управлять им с помощью интерфейса командной строки Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="13834-103">How to create and manage Azure Redis Cache using the Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13834-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13834-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="13834-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="13834-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="13834-106">Интерфейс CLI Azure позволяет управлять инфраструктурой Azure с любой платформы.</span><span class="sxs-lookup"><span data-stu-id="13834-106">The Azure CLI is a great way to manage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="13834-107">В этой статье показано, как создавать экземпляры кэша Redis для Azure и управлять ими с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="13834-107">This article shows you how to create and manage your Azure Redis Cache instances using the Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="13834-108">Эта статья относится к предыдущей версии Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="13834-108">This article applies to a previous version of Azure CLI.</span></span> <span data-ttu-id="13834-109">Последние примеры сценариев Azure CLI 2.0 см. в статье [Примеры Azure CLI для виртуальных машин Windows](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="13834-109">For the latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="13834-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="13834-110">Prerequisites</span></span>
<span data-ttu-id="13834-111">Для создания экземпляров кэша Redis для Azure и управления ими с помощью Azure CLI необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="13834-111">To create and manage Azure Redis Cache instances using Azure CLI, you must complete the following steps.</span></span>

* <span data-ttu-id="13834-112">Необходимо иметь учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="13834-112">You must have an Azure account.</span></span> <span data-ttu-id="13834-113">Если ее нет, можно создать [бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/) всего за пару минут.</span><span class="sxs-lookup"><span data-stu-id="13834-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="13834-114">[Установка Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="13834-114">[Install the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="13834-115">Подключите установленный интерфейс Azure CLI к личной либо рабочей или учебной учетной записи Azure, затем выполните вход из Azure CLI с помощью команды `azure login` .</span><span class="sxs-lookup"><span data-stu-id="13834-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from the Azure CLI using the `azure login` command.</span></span> <span data-ttu-id="13834-116">Чтобы разобраться в различиях и сделать правильный выбор, изучите статью [Подключение к среде Azure с использованием интерфейса командной строки Azure (Azure CLI)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="13834-116">To understand the differences and choose, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="13834-117">Перед выполнением любой из указанных ниже команд переключите Azure CLI в режим диспетчера ресурсов, выполнив команду `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="13834-117">Before running any of the following commands, switch the Azure CLI into Resource Manager mode by running the `azure config mode arm` command.</span></span> <span data-ttu-id="13834-118">Дополнительные сведения см. в разделе [Управление ресурсами и группами ресурсов Azure с помощью интерфейса командной строки Azure](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="13834-118">For more information, see [Use the Azure CLI to manage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="13834-119">Свойства кэша Redis</span><span class="sxs-lookup"><span data-stu-id="13834-119">Redis Cache properties</span></span>
<span data-ttu-id="13834-120">При создании и обновлении экземпляров кэша Redis используются следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="13834-120">The following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="13834-121">Свойство</span><span class="sxs-lookup"><span data-stu-id="13834-121">Property</span></span> | <span data-ttu-id="13834-122">Switch</span><span class="sxs-lookup"><span data-stu-id="13834-122">Switch</span></span> | <span data-ttu-id="13834-123">Описание</span><span class="sxs-lookup"><span data-stu-id="13834-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13834-124">name</span><span class="sxs-lookup"><span data-stu-id="13834-124">name</span></span> |<span data-ttu-id="13834-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="13834-125">-n, --name</span></span> |<span data-ttu-id="13834-126">Имя кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="13834-126">Name of the Redis Cache.</span></span> |
| <span data-ttu-id="13834-127">resource group</span><span class="sxs-lookup"><span data-stu-id="13834-127">resource group</span></span> |<span data-ttu-id="13834-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="13834-128">-g, --resource-group</span></span> |<span data-ttu-id="13834-129">Имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="13834-129">Name of the Resource Group.</span></span> |
| <span data-ttu-id="13834-130">location</span><span class="sxs-lookup"><span data-stu-id="13834-130">location</span></span> |<span data-ttu-id="13834-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="13834-131">-l, --location</span></span> |<span data-ttu-id="13834-132">Расположение для создания кэша.</span><span class="sxs-lookup"><span data-stu-id="13834-132">Location to create cache.</span></span> |
| <span data-ttu-id="13834-133">size</span><span class="sxs-lookup"><span data-stu-id="13834-133">size</span></span> |<span data-ttu-id="13834-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="13834-134">-z, --size</span></span> |<span data-ttu-id="13834-135">Размер кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="13834-135">Size of the Redis Cache.</span></span> <span data-ttu-id="13834-136">Допустимые значения: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="13834-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="13834-137">sku</span><span class="sxs-lookup"><span data-stu-id="13834-137">sku</span></span> |<span data-ttu-id="13834-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="13834-138">-x, --sku</span></span> |<span data-ttu-id="13834-139">Номер SKU Redis.</span><span class="sxs-lookup"><span data-stu-id="13834-139">Redis SKU.</span></span> <span data-ttu-id="13834-140">Должен иметь одно из этих значений: [Basic, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="13834-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="13834-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="13834-141">EnableNonSslPort</span></span> |<span data-ttu-id="13834-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="13834-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="13834-143">Свойство EnableNonSslPort кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="13834-143">EnableNonSslPort property of the Redis Cache.</span></span> <span data-ttu-id="13834-144">Добавьте этот флаг, если хотите включить для кэша порт без SSL.</span><span class="sxs-lookup"><span data-stu-id="13834-144">Add this flag if you want to enable the Non SSL Port for your cache</span></span> |
| <span data-ttu-id="13834-145">Конфигурация Redis</span><span class="sxs-lookup"><span data-stu-id="13834-145">Redis Configuration</span></span> |<span data-ttu-id="13834-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="13834-146">-c, --redis-configuration</span></span> |<span data-ttu-id="13834-147">Конфигурация Redis.</span><span class="sxs-lookup"><span data-stu-id="13834-147">Redis Configuration.</span></span> <span data-ttu-id="13834-148">Введите строку ключей и значений конфигурации в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="13834-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="13834-149">Формат:"{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="13834-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="13834-150">Конфигурация Redis</span><span class="sxs-lookup"><span data-stu-id="13834-150">Redis Configuration</span></span> |<span data-ttu-id="13834-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="13834-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="13834-152">Конфигурация Redis.</span><span class="sxs-lookup"><span data-stu-id="13834-152">Redis Configuration.</span></span> <span data-ttu-id="13834-153">Введите путь к файлу, содержащему ключи и значения.</span><span class="sxs-lookup"><span data-stu-id="13834-153">Enter the path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="13834-154">Формат записи в файле: {"":"","":""}</span><span class="sxs-lookup"><span data-stu-id="13834-154">Format for the file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="13834-155">Число сегментов</span><span class="sxs-lookup"><span data-stu-id="13834-155">Shard Count</span></span> |<span data-ttu-id="13834-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="13834-156">-r, --shard-count</span></span> |<span data-ttu-id="13834-157">Число сегментов, которые будут созданы при создании кэша уровня "Премиум" с включенной кластеризацией.</span><span class="sxs-lookup"><span data-stu-id="13834-157">Number of Shards to create on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="13834-158">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="13834-158">Virtual Network</span></span> |<span data-ttu-id="13834-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="13834-159">-v, --virtual-network</span></span> |<span data-ttu-id="13834-160">При размещении кэша в виртуальной сети определяет точный идентификатор ресурса ARM виртуальной сети, в которой будет развернут кэш Redis.</span><span class="sxs-lookup"><span data-stu-id="13834-160">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="13834-161">Пример формата: /subscriptions/{идентификатор_подписки}/resourceGroups/{имя_группы_ресурсов}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="13834-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="13834-162">key type</span><span class="sxs-lookup"><span data-stu-id="13834-162">key type</span></span> |<span data-ttu-id="13834-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="13834-163">-t, --key-type</span></span> |<span data-ttu-id="13834-164">Тип обновляемого ключа.</span><span class="sxs-lookup"><span data-stu-id="13834-164">Type of key to renew.</span></span> <span data-ttu-id="13834-165">Допустимые значения: [Primary, Secondary].</span><span class="sxs-lookup"><span data-stu-id="13834-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="13834-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="13834-166">StaticIP</span></span> |<span data-ttu-id="13834-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="13834-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="13834-168">При размещении кэша в виртуальной сети определяет уникальный IP-адрес подсети для кэша.</span><span class="sxs-lookup"><span data-stu-id="13834-168">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="13834-169">Если IP-адрес не указан, он автоматически выбирается из подсети.</span><span class="sxs-lookup"><span data-stu-id="13834-169">If not provided, one is chosen for you from the subnet.</span></span> |
| <span data-ttu-id="13834-170">Подсеть</span><span class="sxs-lookup"><span data-stu-id="13834-170">Subnet</span></span> |<span data-ttu-id="13834-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="13834-171">t, --subnet <subnet></span></span> |<span data-ttu-id="13834-172">При размещении кэша в виртуальной сети определяет имя подсети, в которой будет развернут кэш.</span><span class="sxs-lookup"><span data-stu-id="13834-172">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> |
| <span data-ttu-id="13834-173">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="13834-173">VirtualNetwork</span></span> |<span data-ttu-id="13834-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="13834-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="13834-175">При размещении кэша в виртуальной сети определяет точный идентификатор ресурса ARM виртуальной сети, в которой будет развернут кэш Redis.</span><span class="sxs-lookup"><span data-stu-id="13834-175">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="13834-176">Пример формата: /subscriptions/{идентификатор_подписки}/resourceGroups/{имя_группы_ресурсов}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="13834-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="13834-177">Подписки</span><span class="sxs-lookup"><span data-stu-id="13834-177">Subscription</span></span> |<span data-ttu-id="13834-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="13834-178">-s, --subscription</span></span> |<span data-ttu-id="13834-179">Идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="13834-179">The subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="13834-180">Просмотр всех команд кэша Redis</span><span class="sxs-lookup"><span data-stu-id="13834-180">See all Redis Cache commands</span></span>
<span data-ttu-id="13834-181">Для просмотра всех команд кэша Redis и их параметров используйте команду `azure rediscache -h` .</span><span class="sxs-lookup"><span data-stu-id="13834-181">To see all Redis Cache commands and their parameters, use the `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands to manage your Azure Redis Cache(s)
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
    help:    Renew the authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="13834-182">Создание кэша Redis</span><span class="sxs-lookup"><span data-stu-id="13834-182">Create a Redis Cache</span></span>
<span data-ttu-id="13834-183">Чтобы создать кэш Redis, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="13834-183">To create a Redis Cache, use the following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="13834-184">Чтобы получить дополнительные сведения об этой команде, выполните команду `azure rediscache create -h` .</span><span class="sxs-lookup"><span data-stu-id="13834-184">For more information about this command, run the `azure rediscache create -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -l, --location <location>                                Location to create cache.
    help:      -z, --size <size>                                        Size of the Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of the Redis Cache. Add this flag if you want to enable the Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here. Format for the file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards to create on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="13834-185">Удаление существующего кэша Redis</span><span class="sxs-lookup"><span data-stu-id="13834-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="13834-186">Чтобы удалить кэш Redis, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="13834-186">To delete a Redis Cache, use the following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="13834-187">Чтобы получить дополнительные сведения об этой команде, выполните команду `azure rediscache delete -h` .</span><span class="sxs-lookup"><span data-stu-id="13834-187">For more information about this command, run the `azure rediscache delete -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which the cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="13834-188">Вывод списка всех кэшей Redis в подписке или группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="13834-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="13834-189">Чтобы вывести список всех кэшей Redis в подписке или группе ресурсов, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="13834-189">To list all Redis Caches within your Subscription or Resource Group, use the following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="13834-190">Чтобы получить дополнительные сведения об этой команде, выполните команду `azure rediscache list -h` .</span><span class="sxs-lookup"><span data-stu-id="13834-190">For more information about this command, run the `azure rediscache list -h` command.</span></span>

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
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="13834-191">Отображение свойств существующего кэша Redis</span><span class="sxs-lookup"><span data-stu-id="13834-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="13834-192">Чтобы отобразить свойства существующего кэша Redis, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="13834-192">To show properties of an existing Redis Cache, use the following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="13834-193">Чтобы получить дополнительные сведения об этой команде, выполните команду `azure rediscache show -h` .</span><span class="sxs-lookup"><span data-stu-id="13834-193">For more information about this command, run the `azure rediscache show -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="13834-194">Изменение параметров существующего кэша Redis</span><span class="sxs-lookup"><span data-stu-id="13834-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="13834-195">Чтобы изменить параметры существующего кэша Redis, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="13834-195">To change settings of an existing Redis Cache, use the following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="13834-196">Чтобы получить дополнительные сведения об этой команде, выполните команду `azure rediscache set -h` .</span><span class="sxs-lookup"><span data-stu-id="13834-196">For more information about this command, run the `azure rediscache set -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-the-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="13834-197">Обновление ключа аутентификации для существующего кэша Redis</span><span class="sxs-lookup"><span data-stu-id="13834-197">Renew the authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="13834-198">Чтобы обновить ключ аутентификации для существующего кэша Redis, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="13834-198">To renew the authentication key for an existing Redis Cache, use the following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="13834-199">Укажите `Primary` или `Secondary` для `key-type`.</span><span class="sxs-lookup"><span data-stu-id="13834-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="13834-200">Чтобы получить дополнительные сведения об этой команде, выполните команду `azure rediscache renew-key -h`.</span><span class="sxs-lookup"><span data-stu-id="13834-200">For more information about this command, run the `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew the authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key to renew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="13834-201">Вывод первичного и вторичного ключей существующего кэша Redis</span><span class="sxs-lookup"><span data-stu-id="13834-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="13834-202">Чтобы вывести первичный и вторичный ключи существующего кэша Redis, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="13834-202">To list Primary and Secondary keys of an existing Redis Cache, use the following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="13834-203">Чтобы получить дополнительные сведения об этой команде, выполните команду `azure rediscache list-keys -h` .</span><span class="sxs-lookup"><span data-stu-id="13834-203">For more information about this command, run the `azure rediscache list-keys -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
