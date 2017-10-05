---
title: "Автоматизация управления Azure Cosmos DB с помощью PowerShell | Документация Майкрософт"
description: "Сведения об управлении учетными записями базы данных Azure Cosmos DB с помощью Azure PowerShell."
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 25c543528119410dff0684845a713dcb0d6151d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="8b96c-103">Создание учетной записи Azure Cosmos DB с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b96c-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="8b96c-104">В этом руководстве содержатся команды Azure PowerShell, используемые для автоматизации управления учетными записями баз данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-104">The following guide describes commands to automate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="8b96c-105">Здесь также приведены команды для управления ключами учетных записей и изменения порядка при отработке отказа в [межрегиональных учетных записях баз данных][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="8b96c-105">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="8b96c-106">Вы можете изменить политики согласованности, а также добавить или удалить регионы в учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="8b96c-106">Updating your database account allows you to modify consistency policies and add/remove regions.</span></span> <span data-ttu-id="8b96c-107">Чтобы управлять своей учетной записью базы данных Azure Cosmos DB между несколькими регионами, можно использовать [Azure CLI](cli-samples.md), [REST API поставщика ресурсов][rp-rest-api] или [портал Azure](create-documentdb-dotnet.md#create-account).</span><span class="sxs-lookup"><span data-stu-id="8b96c-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](create-documentdb-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="8b96c-108">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="8b96c-108">Getting Started</span></span>

<span data-ttu-id="8b96c-109">Следуйте инструкциям из статьи [Приступая к работе с командлетами Azure PowerShell][powershell-install-configure], чтобы установить PowerShell и подключиться к учетной записи Azure Resource Manager через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b96c-109">Follow the instructions in [How to install and configure Azure PowerShell][powershell-install-configure] to install and log in to your Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="8b96c-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="8b96c-110">Notes</span></span>

* <span data-ttu-id="8b96c-111">Чтобы выполнять следующие команды без запроса пользовательского подтверждения, добавьте в команду флаг `-Force`.</span><span class="sxs-lookup"><span data-stu-id="8b96c-111">If you would like to execute the following commands without requiring user confirmation, append the `-Force` flag to the command.</span></span>
* <span data-ttu-id="8b96c-112">Все следующие команды синхронные.</span><span class="sxs-lookup"><span data-stu-id="8b96c-112">All the following commands are synchronous.</span></span>

## <span data-ttu-id="8b96c-113"><a id="create-documentdb-account-powershell"></a>Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8b96c-113"><a id="create-documentdb-account-powershell"></a> Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="8b96c-114">Эта команда позволяет создать учетную запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-114">This command allows you to create an Azure Cosmos DB database account.</span></span> <span data-ttu-id="8b96c-115">Настройте новую учетную запись для использования в одном или [нескольких регионах][scaling-globally] и добавьте определенную [политику согласованности](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8b96c-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="8b96c-116">`<write-region-location>` — имя расположения региона для записи учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="8b96c-116">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="8b96c-117">Значение приоритета отработки отказа для этого расположения должно быть равно 0.</span><span class="sxs-lookup"><span data-stu-id="8b96c-117">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="8b96c-118">Каждая учетная запись базы данных должна иметь только один регион для записи.</span><span class="sxs-lookup"><span data-stu-id="8b96c-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="8b96c-119">`<read-region-location>` — имя расположения региона для чтения учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="8b96c-119">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="8b96c-120">Значение приоритета отработки отказа для этого расположения должно быть больше 0.</span><span class="sxs-lookup"><span data-stu-id="8b96c-120">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="8b96c-121">Каждая учетная запись базы данных может иметь несколько регионов для чтения.</span><span class="sxs-lookup"><span data-stu-id="8b96c-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="8b96c-122">`<ip-range-filter>` — указывает набор IP-адресов или их диапазонов в нотации CIDR, которые добавляются в список разрешенных клиентских IP-адресов для указанной учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="8b96c-122">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="8b96c-123">IP-адреса и их диапазоны должны быть разделены запятой без пробелов.</span><span class="sxs-lookup"><span data-stu-id="8b96c-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="8b96c-124">Дополнительные сведения см. в статье о [поддержке брандмауэра Azure Cosmos DB](firewall-support.md).</span><span class="sxs-lookup"><span data-stu-id="8b96c-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="8b96c-125">`<default-consistency-level>` — уровень согласованности по умолчанию учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-125">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="8b96c-126">Дополнительные сведения см. в статье о [настраиваемых уровнях согласованности в Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8b96c-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="8b96c-127">`<max-interval>`. При использовании согласованности с ограниченным устареванием это значение указывает допустимое время устаревания (в секундах).</span><span class="sxs-lookup"><span data-stu-id="8b96c-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="8b96c-128">Допустимый диапазон — 1–100.</span><span class="sxs-lookup"><span data-stu-id="8b96c-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="8b96c-129">`<max-staleness-prefix>`. При использовании согласованности с ограниченным устареванием это значение указывает допустимое количество устаревших запросов.</span><span class="sxs-lookup"><span data-stu-id="8b96c-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="8b96c-130">Допустимый диапазон — 1–2 147 483 647.</span><span class="sxs-lookup"><span data-stu-id="8b96c-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="8b96c-131">`<resource-group-name>` — имя [группы ресурсов Azure][azure-resource-groups], в которую входит новая учетная запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-131">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="8b96c-132">`<resource-group-location>` — расположение группы ресурсов Azure, в которую входит новая учетная запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-132">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="8b96c-133">`<database-account-name>` — имя создаваемой учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-133">`<database-account-name>` The name of the Azure Cosmos DB database account to be created.</span></span> <span data-ttu-id="8b96c-134">В нем могут использоваться только строчные буквы, цифры и символ "-", а его длина должна составлять от 3 до 50 символов.</span><span class="sxs-lookup"><span data-stu-id="8b96c-134">It can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="8b96c-135">Пример:</span><span class="sxs-lookup"><span data-stu-id="8b96c-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="8b96c-136">Примечания</span><span class="sxs-lookup"><span data-stu-id="8b96c-136">Notes</span></span>
* <span data-ttu-id="8b96c-137">В предыдущем примере создается учетная запись базы данных с двумя регионами.</span><span class="sxs-lookup"><span data-stu-id="8b96c-137">The preceding example creates a database account with two regions.</span></span> <span data-ttu-id="8b96c-138">Кроме того, можно также создать учетную запись базы данных с одним регионом (регион для записи со значением приоритета отработки отказа 0) или с несколькими регионами (более двух).</span><span class="sxs-lookup"><span data-stu-id="8b96c-138">It is also possible to create a database account with either one region (which is designated as the write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="8b96c-139">Дополнительные сведения см. в разделе [Масштабирование по всей планете][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="8b96c-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="8b96c-140">В качестве расположений используйте регионы, в которых база данных Azure Cosmos DB общедоступна.</span><span class="sxs-lookup"><span data-stu-id="8b96c-140">The locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="8b96c-141">Текущий список регионов см. на [странице регионов Azure](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="8b96c-141">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <span data-ttu-id="8b96c-142"><a id="update-documentdb-account-powershell"></a> Обновление учетной записи базы данных DocumentDB</span><span class="sxs-lookup"><span data-stu-id="8b96c-142"><a id="update-documentdb-account-powershell"></a> Update a DocumentDB Database Account</span></span>

<span data-ttu-id="8b96c-143">Эта команда позволяет обновить свойства учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-143">This command allows you to update your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="8b96c-144">К ним относятся политика согласованности и расположения учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="8b96c-144">This includes the consistency policy and the locations which the database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="8b96c-145">Кроме того, эта команда позволяет добавлять или удалять регионы, но не изменять приоритеты при отработке отказа.</span><span class="sxs-lookup"><span data-stu-id="8b96c-145">This command allows you to add and remove regions but does not allow you to modify failover priorities.</span></span> <span data-ttu-id="8b96c-146">Сведения об изменении приоритетов при отработке отказа см. [ниже](#modify-failover-priority-powershell).</span><span class="sxs-lookup"><span data-stu-id="8b96c-146">To modify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="8b96c-147">`<write-region-location>` — имя расположения региона для записи учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="8b96c-147">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="8b96c-148">Значение приоритета отработки отказа для этого расположения должно быть равно 0.</span><span class="sxs-lookup"><span data-stu-id="8b96c-148">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="8b96c-149">Каждая учетная запись базы данных должна иметь только один регион для записи.</span><span class="sxs-lookup"><span data-stu-id="8b96c-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="8b96c-150">`<read-region-location>` — имя расположения региона для чтения учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="8b96c-150">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="8b96c-151">Значение приоритета отработки отказа для этого расположения должно быть больше 0.</span><span class="sxs-lookup"><span data-stu-id="8b96c-151">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="8b96c-152">Каждая учетная запись базы данных может иметь несколько регионов для чтения.</span><span class="sxs-lookup"><span data-stu-id="8b96c-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="8b96c-153">`<default-consistency-level>` — уровень согласованности по умолчанию учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-153">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="8b96c-154">Дополнительные сведения см. в статье о [настраиваемых уровнях согласованности в Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8b96c-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="8b96c-155">`<ip-range-filter>` — указывает набор IP-адресов или их диапазонов в нотации CIDR, которые добавляются в список разрешенных клиентских IP-адресов для указанной учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="8b96c-155">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="8b96c-156">IP-адреса и их диапазоны должны быть разделены запятой без пробелов.</span><span class="sxs-lookup"><span data-stu-id="8b96c-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="8b96c-157">Дополнительные сведения см. в статье о [поддержке брандмауэра Azure Cosmos DB](firewall-support.md).</span><span class="sxs-lookup"><span data-stu-id="8b96c-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="8b96c-158">`<max-interval>`. При использовании согласованности с ограниченным устареванием это значение указывает допустимое время устаревания (в секундах).</span><span class="sxs-lookup"><span data-stu-id="8b96c-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="8b96c-159">Допустимый диапазон — 1–100.</span><span class="sxs-lookup"><span data-stu-id="8b96c-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="8b96c-160">`<max-staleness-prefix>`. При использовании согласованности с ограниченным устареванием это значение указывает допустимое количество устаревших запросов.</span><span class="sxs-lookup"><span data-stu-id="8b96c-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="8b96c-161">Допустимый диапазон — 1–2 147 483 647.</span><span class="sxs-lookup"><span data-stu-id="8b96c-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="8b96c-162">`<resource-group-name>` — имя [группы ресурсов Azure][azure-resource-groups], в которую входит новая учетная запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-162">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="8b96c-163">`<resource-group-location>` — расположение группы ресурсов Azure, в которую входит новая учетная запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-163">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="8b96c-164">`<database-account-name>` — имя обновляемой учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-164">`<database-account-name>` The name of the Azure Cosmos DB database account to be updated.</span></span>

<span data-ttu-id="8b96c-165">Пример:</span><span class="sxs-lookup"><span data-stu-id="8b96c-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <span data-ttu-id="8b96c-166"><a id="delete-documentdb-account-powershell"></a> Удаление учетной записи базы данных DocumentDB</span><span class="sxs-lookup"><span data-stu-id="8b96c-166"><a id="delete-documentdb-account-powershell"></a> Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="8b96c-167">Эта команда позволяет удалить имеющуюся учетную запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-167">This command allows you to delete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="8b96c-168">`<resource-group-name>` — имя [группы ресурсов Azure][azure-resource-groups], в которую входит новая учетная запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-168">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="8b96c-169">`<database-account-name>` — имя удаляемой учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-169">`<database-account-name>` The name of the Azure Cosmos DB database account to be deleted.</span></span>

<span data-ttu-id="8b96c-170">Пример:</span><span class="sxs-lookup"><span data-stu-id="8b96c-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="8b96c-171"><a id="get-documentdb-properties-powershell"></a> Получение свойств учетной записи базы данных DocumentDB</span><span class="sxs-lookup"><span data-stu-id="8b96c-171"><a id="get-documentdb-properties-powershell"></a> Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="8b96c-172">Эта команда позволяет получить свойства имеющейся учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-172">This command allows you to get the properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="8b96c-173">`<resource-group-name>` — имя [группы ресурсов Azure][azure-resource-groups], в которую входит новая учетная запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-173">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="8b96c-174">`<database-account-name>` — имя учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-174">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="8b96c-175">Пример:</span><span class="sxs-lookup"><span data-stu-id="8b96c-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="8b96c-176"><a id="update-tags-powershell"></a>Обновление тегов учетной записи базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8b96c-176"><a id="update-tags-powershell"></a> Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="8b96c-177">Указанная ниже команда позволяет установить [теги ресурсов Azure][azure-resource-tags] для учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-177">The following example describes how to set [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="8b96c-178">Эту команду можно выполнять вместе с командами создания или обновления. Для этого необходимо добавить флаг `-Tags` с соответствующим параметром.</span><span class="sxs-lookup"><span data-stu-id="8b96c-178">This command can be combined with the create or update commands by appending the `-Tags` flag with the corresponding parameter.</span></span>

<span data-ttu-id="8b96c-179">Пример:</span><span class="sxs-lookup"><span data-stu-id="8b96c-179">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <span data-ttu-id="8b96c-180"><a id="list-account-keys-powershell"></a> Вывод ключей учетной записи</span><span class="sxs-lookup"><span data-stu-id="8b96c-180"><a id="list-account-keys-powershell"></a> List Account Keys</span></span>

<span data-ttu-id="8b96c-181">При создании учетной записи Azure Cosmos DB служба создает два главных ключа доступа, которые можно использовать для проверки подлинности при доступе к учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-181">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="8b96c-182">Предоставляя два ключа, Azure Cosmos DB позволяет вам повторно создавать ключи без перерывов в работе учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-182">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> <span data-ttu-id="8b96c-183">Ключи только для чтения, используемые для выполнения проверки подлинности операций чтения, также доступны.</span><span class="sxs-lookup"><span data-stu-id="8b96c-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="8b96c-184">Доступны два ключа для чтения и записи (первичный и вторичный), а также два ключа только для чтения (первичный и вторичный).</span><span class="sxs-lookup"><span data-stu-id="8b96c-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="8b96c-185">`<resource-group-name>` — имя [группы ресурсов Azure][azure-resource-groups], в которую входит новая учетная запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-185">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="8b96c-186">`<database-account-name>` — имя учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-186">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="8b96c-187">Пример:</span><span class="sxs-lookup"><span data-stu-id="8b96c-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="8b96c-188"><a id="list-connection-strings-powershell"></a> Вывод строк подключения</span><span class="sxs-lookup"><span data-stu-id="8b96c-188"><a id="list-connection-strings-powershell"></a> List Connection Strings</span></span>

<span data-ttu-id="8b96c-189">Для учетных записей MongoDB строку подключения приложения MongoDB к учетной записи базы данных можно получить с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="8b96c-189">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="8b96c-190">`<resource-group-name>` — имя [группы ресурсов Azure][azure-resource-groups], в которую входит новая учетная запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-190">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="8b96c-191">`<database-account-name>` — имя учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-191">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="8b96c-192">Пример:</span><span class="sxs-lookup"><span data-stu-id="8b96c-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="8b96c-193"><a id="regenerate-account-key-powershell"></a> Повторное создание ключей учетных записей</span><span class="sxs-lookup"><span data-stu-id="8b96c-193"><a id="regenerate-account-key-powershell"></a> Regenerate Account Key</span></span>

<span data-ttu-id="8b96c-194">Вам следует периодически менять ключи доступа для своей учетной записи Azure Cosmos DB, чтобы повысить уровень безопасности соединений.</span><span class="sxs-lookup"><span data-stu-id="8b96c-194">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="8b96c-195">Назначается два ключа доступа, что позволяет поддерживать подключения к учетной записи Azure Cosmos DB с помощью одного ключа, одновременно повторно создавая второй ключ.</span><span class="sxs-lookup"><span data-stu-id="8b96c-195">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="8b96c-196">`<resource-group-name>` — имя [группы ресурсов Azure][azure-resource-groups], в которую входит новая учетная запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-196">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="8b96c-197">`<database-account-name>` — имя учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-197">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="8b96c-198">`<key-kind>` — один из четырех типов ключей, которые можно повторно создать: Primary, Secondary, PrimaryReadonly, SecondaryReadonly.</span><span class="sxs-lookup"><span data-stu-id="8b96c-198">`<key-kind>` One of the four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like to regenerate.</span></span>

<span data-ttu-id="8b96c-199">Пример:</span><span class="sxs-lookup"><span data-stu-id="8b96c-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <span data-ttu-id="8b96c-200"><a id="modify-failover-priority-powershell"></a> Изменение приоритета при отработке отказа в учетной записи базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8b96c-200"><a id="modify-failover-priority-powershell"></a> Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="8b96c-201">Для межрегиональных учетных записей баз данных можно изменить приоритет при отработке отказа в разных регионах, в которых они используются.</span><span class="sxs-lookup"><span data-stu-id="8b96c-201">For multi-region database accounts, you can change the failover priority of the various regions which the Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="8b96c-202">Дополнительные сведения об отработке отказа в учетной записи базы данных Azure Cosmos DB см. в статье [Как работает глобальное распределение данных в Azure Cosmos DB?][distribute-data-globally]</span><span class="sxs-lookup"><span data-stu-id="8b96c-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="8b96c-203">`<write-region-location>` — имя расположения региона для записи учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="8b96c-203">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="8b96c-204">Значение приоритета отработки отказа для этого расположения должно быть равно 0.</span><span class="sxs-lookup"><span data-stu-id="8b96c-204">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="8b96c-205">Каждая учетная запись базы данных должна иметь только один регион для записи.</span><span class="sxs-lookup"><span data-stu-id="8b96c-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="8b96c-206">`<read-region-location>` — имя расположения региона для чтения учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="8b96c-206">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="8b96c-207">Значение приоритета отработки отказа для этого расположения должно быть больше 0.</span><span class="sxs-lookup"><span data-stu-id="8b96c-207">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="8b96c-208">Каждая учетная запись базы данных может иметь несколько регионов для чтения.</span><span class="sxs-lookup"><span data-stu-id="8b96c-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="8b96c-209">`<resource-group-name>` — имя [группы ресурсов Azure][azure-resource-groups], в которую входит новая учетная запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-209">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="8b96c-210">`<database-account-name>` — имя учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b96c-210">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="8b96c-211">Пример:</span><span class="sxs-lookup"><span data-stu-id="8b96c-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="8b96c-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b96c-212">Next steps</span></span>

* <span data-ttu-id="8b96c-213">Дополнительные сведения см. в статье о [подключении и создании запросов с помощью .NET](create-documentdb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8b96c-213">To connect using .NET, see [Connect and query with .NET](create-documentdb-dotnet.md).</span></span>
* <span data-ttu-id="8b96c-214">Дополнительные сведения см. в статье о [подключении и создании запросов с помощью .NET Core](create-documentdb-dotnet-core.md).</span><span class="sxs-lookup"><span data-stu-id="8b96c-214">To connect using .NET Core, see [Connect and query with .NET Core](create-documentdb-dotnet-core.md).</span></span>
* <span data-ttu-id="8b96c-215">Дополнительные сведения см. в статье о [подключении и создании запросов с помощью Node.js и приложения MongoDB](create-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8b96c-215">To connect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
