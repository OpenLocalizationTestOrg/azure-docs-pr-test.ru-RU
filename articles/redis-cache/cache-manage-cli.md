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
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="92f6d-103">Как toocreate и управлять ими с помощью интерфейса командной строки Azure (Azure CLI) hello кэш Azure Redis</span><span class="sxs-lookup"><span data-stu-id="92f6d-103">How toocreate and manage Azure Redis Cache using hello Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="92f6d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="92f6d-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="92f6d-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="92f6d-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="92f6d-106">Hello Azure CLI является хорошим способом toomanage инфраструктуры Azure с любой платформы.</span><span class="sxs-lookup"><span data-stu-id="92f6d-106">hello Azure CLI is a great way toomanage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="92f6d-107">В этой статье показано, как toocreate и управлять ими с помощью Azure CLI hello экземплярами кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="92f6d-107">This article shows you how toocreate and manage your Azure Redis Cache instances using hello Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="92f6d-108">Эта статья относится tooa предыдущей версии Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="92f6d-108">This article applies tooa previous version of Azure CLI.</span></span> <span data-ttu-id="92f6d-109">Hello последнюю Azure CLI 2.0 образцы скриптов см. в разделе [примеры кэша Azure CLI Redis](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="92f6d-109">For hello latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="92f6d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="92f6d-110">Prerequisites</span></span>
<span data-ttu-id="92f6d-111">toocreate и управления экземплярами кэша Redis для Azure, с помощью Azure CLI, необходимо выполнить следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="92f6d-111">toocreate and manage Azure Redis Cache instances using Azure CLI, you must complete hello following steps.</span></span>

* <span data-ttu-id="92f6d-112">Необходимо иметь учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="92f6d-112">You must have an Azure account.</span></span> <span data-ttu-id="92f6d-113">Если ее нет, можно создать [бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/) всего за пару минут.</span><span class="sxs-lookup"><span data-stu-id="92f6d-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="92f6d-114">[Установка hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="92f6d-114">[Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="92f6d-115">Подключение установки Azure CLI с личной учетной записи Azure или с помощью рабочей или учебной учетной записи Azure, входить в систему с hello Azure CLI с помощью hello `azure login` команды.</span><span class="sxs-lookup"><span data-stu-id="92f6d-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from hello Azure CLI using hello `azure login` command.</span></span> <span data-ttu-id="92f6d-116">toounderstand hello различия и выберите см. в разделе [подключение tooan подписки Azure из hello Azure командной строки (CLI Azure)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="92f6d-116">toounderstand hello differences and choose, see [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="92f6d-117">Прежде чем выполнять hello, следующие команды, переключение hello Azure CLI в режим диспетчера ресурсов, выполнив hello `azure config mode arm` команды.</span><span class="sxs-lookup"><span data-stu-id="92f6d-117">Before running any of hello following commands, switch hello Azure CLI into Resource Manager mode by running hello `azure config mode arm` command.</span></span> <span data-ttu-id="92f6d-118">Дополнительные сведения см. в разделе [toomanage Azure CLI hello Azure использовать ресурсы и группы ресурсов](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="92f6d-118">For more information, see [Use hello Azure CLI toomanage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="92f6d-119">Свойства кэша Redis</span><span class="sxs-lookup"><span data-stu-id="92f6d-119">Redis Cache properties</span></span>
<span data-ttu-id="92f6d-120">Hello используются следующие свойства при создании и обновлении экземпляров кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="92f6d-120">hello following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="92f6d-121">Свойство</span><span class="sxs-lookup"><span data-stu-id="92f6d-121">Property</span></span> | <span data-ttu-id="92f6d-122">Switch</span><span class="sxs-lookup"><span data-stu-id="92f6d-122">Switch</span></span> | <span data-ttu-id="92f6d-123">Описание</span><span class="sxs-lookup"><span data-stu-id="92f6d-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92f6d-124">name</span><span class="sxs-lookup"><span data-stu-id="92f6d-124">name</span></span> |<span data-ttu-id="92f6d-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="92f6d-125">-n, --name</span></span> |<span data-ttu-id="92f6d-126">Имя hello кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="92f6d-126">Name of hello Redis Cache.</span></span> |
| <span data-ttu-id="92f6d-127">resource group</span><span class="sxs-lookup"><span data-stu-id="92f6d-127">resource group</span></span> |<span data-ttu-id="92f6d-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="92f6d-128">-g, --resource-group</span></span> |<span data-ttu-id="92f6d-129">Имя группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="92f6d-129">Name of hello Resource Group.</span></span> |
| <span data-ttu-id="92f6d-130">location</span><span class="sxs-lookup"><span data-stu-id="92f6d-130">location</span></span> |<span data-ttu-id="92f6d-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="92f6d-131">-l, --location</span></span> |<span data-ttu-id="92f6d-132">Кэш toocreate расположения.</span><span class="sxs-lookup"><span data-stu-id="92f6d-132">Location toocreate cache.</span></span> |
| <span data-ttu-id="92f6d-133">size</span><span class="sxs-lookup"><span data-stu-id="92f6d-133">size</span></span> |<span data-ttu-id="92f6d-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="92f6d-134">-z, --size</span></span> |<span data-ttu-id="92f6d-135">Размер кэша Redis hello.</span><span class="sxs-lookup"><span data-stu-id="92f6d-135">Size of hello Redis Cache.</span></span> <span data-ttu-id="92f6d-136">Допустимые значения: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="92f6d-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="92f6d-137">sku</span><span class="sxs-lookup"><span data-stu-id="92f6d-137">sku</span></span> |<span data-ttu-id="92f6d-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="92f6d-138">-x, --sku</span></span> |<span data-ttu-id="92f6d-139">Номер SKU Redis.</span><span class="sxs-lookup"><span data-stu-id="92f6d-139">Redis SKU.</span></span> <span data-ttu-id="92f6d-140">Должен иметь одно из этих значений: [Basic, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="92f6d-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="92f6d-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="92f6d-141">EnableNonSslPort</span></span> |<span data-ttu-id="92f6d-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="92f6d-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="92f6d-143">Свойство EnableNonSslPort hello кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="92f6d-143">EnableNonSslPort property of hello Redis Cache.</span></span> <span data-ttu-id="92f6d-144">Если порт SSL не hello tooenable своего кэша, добавьте этот флаг</span><span class="sxs-lookup"><span data-stu-id="92f6d-144">Add this flag if you want tooenable hello Non SSL Port for your cache</span></span> |
| <span data-ttu-id="92f6d-145">Конфигурация Redis</span><span class="sxs-lookup"><span data-stu-id="92f6d-145">Redis Configuration</span></span> |<span data-ttu-id="92f6d-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="92f6d-146">-c, --redis-configuration</span></span> |<span data-ttu-id="92f6d-147">Конфигурация Redis.</span><span class="sxs-lookup"><span data-stu-id="92f6d-147">Redis Configuration.</span></span> <span data-ttu-id="92f6d-148">Введите строку ключей и значений конфигурации в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="92f6d-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="92f6d-149">Формат:"{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="92f6d-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="92f6d-150">Конфигурация Redis</span><span class="sxs-lookup"><span data-stu-id="92f6d-150">Redis Configuration</span></span> |<span data-ttu-id="92f6d-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="92f6d-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="92f6d-152">Конфигурация Redis.</span><span class="sxs-lookup"><span data-stu-id="92f6d-152">Redis Configuration.</span></span> <span data-ttu-id="92f6d-153">Введите путь hello файл, содержащий ключи и значения здесь.</span><span class="sxs-lookup"><span data-stu-id="92f6d-153">Enter hello path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="92f6d-154">Формат для записи в файле hello: {»»: ««,»»:»»}</span><span class="sxs-lookup"><span data-stu-id="92f6d-154">Format for hello file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="92f6d-155">Число сегментов</span><span class="sxs-lookup"><span data-stu-id="92f6d-155">Shard Count</span></span> |<span data-ttu-id="92f6d-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="92f6d-156">-r, --shard-count</span></span> |<span data-ttu-id="92f6d-157">Количество сегментов toocreate кластера кэша Premium с кластеризацией.</span><span class="sxs-lookup"><span data-stu-id="92f6d-157">Number of Shards toocreate on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="92f6d-158">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="92f6d-158">Virtual Network</span></span> |<span data-ttu-id="92f6d-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="92f6d-159">-v, --virtual-network</span></span> |<span data-ttu-id="92f6d-160">Если размещение кэша в виртуальной сети, задает hello точное ARM идентификатор ресурса hello виртуальной сети toodeploy hello redis кэша в.</span><span class="sxs-lookup"><span data-stu-id="92f6d-160">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="92f6d-161">Пример формата: /subscriptions/{идентификатор_подписки}/resourceGroups/{имя_группы_ресурсов}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="92f6d-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="92f6d-162">key type</span><span class="sxs-lookup"><span data-stu-id="92f6d-162">key type</span></span> |<span data-ttu-id="92f6d-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="92f6d-163">-t, --key-type</span></span> |<span data-ttu-id="92f6d-164">Тип ключа toorenew.</span><span class="sxs-lookup"><span data-stu-id="92f6d-164">Type of key toorenew.</span></span> <span data-ttu-id="92f6d-165">Допустимые значения: [Primary, Secondary].</span><span class="sxs-lookup"><span data-stu-id="92f6d-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="92f6d-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="92f6d-166">StaticIP</span></span> |<span data-ttu-id="92f6d-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="92f6d-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="92f6d-168">При размещении вашего кэша в виртуальной сети, указывает уникальный IP-адрес в подсети hello для кэша hello.</span><span class="sxs-lookup"><span data-stu-id="92f6d-168">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="92f6d-169">Если не указано, одна из подсети hello выбирается автоматически.</span><span class="sxs-lookup"><span data-stu-id="92f6d-169">If not provided, one is chosen for you from hello subnet.</span></span> |
| <span data-ttu-id="92f6d-170">Подсеть</span><span class="sxs-lookup"><span data-stu-id="92f6d-170">Subnet</span></span> |<span data-ttu-id="92f6d-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="92f6d-171">t, --subnet <subnet></span></span> |<span data-ttu-id="92f6d-172">При размещении вашего кэша в виртуальной сети, указывает имя hello hello подсети, в какой кэш toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="92f6d-172">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> |
| <span data-ttu-id="92f6d-173">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="92f6d-173">VirtualNetwork</span></span> |<span data-ttu-id="92f6d-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="92f6d-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="92f6d-175">Если размещение кэша в виртуальной сети, задает hello точное ARM идентификатор ресурса hello виртуальной сети toodeploy hello redis кэша в.</span><span class="sxs-lookup"><span data-stu-id="92f6d-175">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="92f6d-176">Пример формата: /subscriptions/{идентификатор_подписки}/resourceGroups/{имя_группы_ресурсов}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="92f6d-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="92f6d-177">Подписки</span><span class="sxs-lookup"><span data-stu-id="92f6d-177">Subscription</span></span> |<span data-ttu-id="92f6d-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="92f6d-178">-s, --subscription</span></span> |<span data-ttu-id="92f6d-179">идентификатор подписки Hello.</span><span class="sxs-lookup"><span data-stu-id="92f6d-179">hello subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="92f6d-180">Просмотр всех команд кэша Redis</span><span class="sxs-lookup"><span data-stu-id="92f6d-180">See all Redis Cache commands</span></span>
<span data-ttu-id="92f6d-181">toosee все команды кэша Redis и их параметров, используйте hello `azure rediscache -h` команды.</span><span class="sxs-lookup"><span data-stu-id="92f6d-181">toosee all Redis Cache commands and their parameters, use hello `azure rediscache -h` command.</span></span>

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

## <a name="create-a-redis-cache"></a><span data-ttu-id="92f6d-182">Создание кэша Redis</span><span class="sxs-lookup"><span data-stu-id="92f6d-182">Create a Redis Cache</span></span>
<span data-ttu-id="92f6d-183">toocreate кэша Redis, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="92f6d-183">toocreate a Redis Cache, use hello following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="92f6d-184">Дополнительные сведения об этой команде запуска hello `azure rediscache create -h` команды.</span><span class="sxs-lookup"><span data-stu-id="92f6d-184">For more information about this command, run hello `azure rediscache create -h` command.</span></span>

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

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="92f6d-185">Удаление существующего кэша Redis</span><span class="sxs-lookup"><span data-stu-id="92f6d-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="92f6d-186">toodelete кэша Redis, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="92f6d-186">toodelete a Redis Cache, use hello following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="92f6d-187">Дополнительные сведения об этой команде запуска hello `azure rediscache delete -h` команды.</span><span class="sxs-lookup"><span data-stu-id="92f6d-187">For more information about this command, run hello `azure rediscache delete -h` command.</span></span>

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

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="92f6d-188">Вывод списка всех кэшей Redis в подписке или группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="92f6d-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="92f6d-189">toolist всех кэшей Redis в вашей подписке или группе ресурсов, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="92f6d-189">toolist all Redis Caches within your Subscription or Resource Group, use hello following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="92f6d-190">Дополнительные сведения об этой команде запуска hello `azure rediscache list -h` команды.</span><span class="sxs-lookup"><span data-stu-id="92f6d-190">For more information about this command, run hello `azure rediscache list -h` command.</span></span>

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

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="92f6d-191">Отображение свойств существующего кэша Redis</span><span class="sxs-lookup"><span data-stu-id="92f6d-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="92f6d-192">tooshow свойства для существующего кэша Redis, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="92f6d-192">tooshow properties of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="92f6d-193">Дополнительные сведения об этой команде запуска hello `azure rediscache show -h` команды.</span><span class="sxs-lookup"><span data-stu-id="92f6d-193">For more information about this command, run hello `azure rediscache show -h` command.</span></span>

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

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="92f6d-194">Изменение параметров существующего кэша Redis</span><span class="sxs-lookup"><span data-stu-id="92f6d-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="92f6d-195">Параметры toochange для существующего кэша Redis, используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="92f6d-195">toochange settings of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="92f6d-196">Дополнительные сведения об этой команде запуска hello `azure rediscache set -h` команды.</span><span class="sxs-lookup"><span data-stu-id="92f6d-196">For more information about this command, run hello `azure rediscache set -h` command.</span></span>

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

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="92f6d-197">Обновить hello ключ проверки подлинности для существующего кэша Redis</span><span class="sxs-lookup"><span data-stu-id="92f6d-197">Renew hello authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="92f6d-198">ключ проверки подлинности hello toorenew для существующего кэша Redis, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="92f6d-198">toorenew hello authentication key for an existing Redis Cache, use hello following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="92f6d-199">Укажите `Primary` или `Secondary` для `key-type`.</span><span class="sxs-lookup"><span data-stu-id="92f6d-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="92f6d-200">Дополнительные сведения об этой команде запуска hello `azure rediscache renew-key -h` команды.</span><span class="sxs-lookup"><span data-stu-id="92f6d-200">For more information about this command, run hello `azure rediscache renew-key -h` command.</span></span>

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

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="92f6d-201">Вывод первичного и вторичного ключей существующего кэша Redis</span><span class="sxs-lookup"><span data-stu-id="92f6d-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="92f6d-202">toolist первичный и вторичный ключи для существующего кэша Redis, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="92f6d-202">toolist Primary and Secondary keys of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="92f6d-203">Дополнительные сведения об этой команде запуска hello `azure rediscache list-keys -h` команды.</span><span class="sxs-lookup"><span data-stu-id="92f6d-203">For more information about this command, run hello `azure rediscache list-keys -h` command.</span></span>

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
