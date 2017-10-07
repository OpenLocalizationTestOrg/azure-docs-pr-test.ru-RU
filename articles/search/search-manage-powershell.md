---
title: "aaaManage поиска Azure с помощью сценариев Powershell | Документы Microsoft"
description: "Управление службой поиска Azure с помощью сценариев PowerShell. Создание или обновление службы Поиска Azure и управление ключами администратора Поиска Azure"
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a>Управление службой поиска Azure с помощью PowerShell
> [!div class="op_single_selector"]
> * [Портал](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> 
> 

В этом разделе перечислены tooperform команд PowerShell hello hello задачи управления для службы поиска Azure. Мы рассмотрим создание службы поиска, ее масштабирование и управления ее ключами API.
Эти команды параллельные hello параметры управления, доступные в hello [API REST управления поиском Azure](http://msdn.microsoft.com/library/dn832684.aspx).

## <a name="prerequisites"></a>Предварительные требования
* Необходимо установить Azure PowerShell 1.0 или более поздней версии. Инструкции см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).
* Вы должны войти в tooyour подписки Azure в PowerShell, как описано ниже.

Во-первых, необходимо tooAzure входа с помощью следующей команды:

    Login-AzureRmAccount

Укажите адрес электронной почты hello учетную запись Azure и пароль в диалоговое окно входа hello Microsoft Azure.

Вы также можете [войти в неинтерактивном режиме с помощью субъекта-службы](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Если у вас несколько подписок Azure, вы должны tooset подписки Azure. toosee список ваши текущие подписки, выполните следующую команду.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify подписка hello, запустите следующую команду hello. В следующем примере hello, — имя подписки hello `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a>Команды toohelp вам начать работу
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a>Дальнейшие действия
После создания службы может занять hello дальнейшие действия: построение [индекс](search-what-is-an-index.md), [запроса индекса](search-query-overview.md)и наконец Создание и управление ими поиска приложения, использующего службы поиска Azure.

* [Создать индекс поиска Azure в hello портал Azure](search-create-index-portal.md)
* [Запрос индекс поиска Azure с помощью поиска обозревателя в hello портал Azure](search-explorer.md)
* [Настройка данных tooload индексатора от других служб](search-indexer-overview.md)
* [Как выполнить поиск Azure toouse в .NET](search-howto-dotnet-sdk.md)
* [Анализ трафика Поиска Azure](search-traffic-analytics.md)

