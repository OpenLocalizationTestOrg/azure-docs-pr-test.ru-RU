---
title: "Устранение неполадок шлюза виртуальной сети и подключений Azure (PowerShell) | Документация Майкрософт"
description: "На этой странице объясняется, как устранить неполадки с помощью Наблюдателя за сетями Azure и командлетов PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 0bdffbac18d1d236b7674feed4dbc784e50e0ea8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="59d0b-103">Устранение неполадок шлюза виртуальной сети и подключений с помощью Наблюдателя за сетями Azure и PowerShell</span><span class="sxs-lookup"><span data-stu-id="59d0b-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="59d0b-104">Портал</span><span class="sxs-lookup"><span data-stu-id="59d0b-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="59d0b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="59d0b-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="59d0b-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="59d0b-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="59d0b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="59d0b-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="59d0b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="59d0b-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="59d0b-109">Наблюдатель за сетями предоставляет множество возможностей, так как он позволяет проанализировать сетевые ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="59d0b-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="59d0b-110">Одна из этих возможностей — устранение неполадок в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="59d0b-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="59d0b-111">Процедуру устранения неполадок с ресурсами можно вызывать с помощью портала, PowerShell, интерфейса командной строки или API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="59d0b-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="59d0b-112">При вызове Наблюдатель за сетями проверяет работоспособность шлюза виртуальной сети или подключения и возвращает результаты.</span><span class="sxs-lookup"><span data-stu-id="59d0b-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="59d0b-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="59d0b-113">Before you begin</span></span>

<span data-ttu-id="59d0b-114">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create an Azure Network Watcher instance](network-watcher-create.md) (Наблюдатель за сетями: создание экземпляра службы).</span><span class="sxs-lookup"><span data-stu-id="59d0b-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="59d0b-115">Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="59d0b-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="59d0b-116">Обзор</span><span class="sxs-lookup"><span data-stu-id="59d0b-116">Overview</span></span>

<span data-ttu-id="59d0b-117">В ходе устранения неполадок с ресурсами вы можете устранить проблемы, возникающие со шлюзами виртуальной сети и подключениями.</span><span class="sxs-lookup"><span data-stu-id="59d0b-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="59d0b-118">При запросе на устранение неполадок с ресурсами запрашиваются и проверяются журналы.</span><span class="sxs-lookup"><span data-stu-id="59d0b-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="59d0b-119">По завершении проверки возвращаются результаты.</span><span class="sxs-lookup"><span data-stu-id="59d0b-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="59d0b-120">Запросы на устранение неполадок с ресурсами выполняются долго, поэтому для возвращения результатов может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="59d0b-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="59d0b-121">Журналы, используемые при устранении неполадок, хранятся в контейнере указанной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="59d0b-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="59d0b-122">Извлечение Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="59d0b-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="59d0b-123">Сначала необходимо извлечь экземпляр Наблюдателя за сетями.</span><span class="sxs-lookup"><span data-stu-id="59d0b-123">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="59d0b-124">Переменная `$networkWatcher` передается в командлет `Start-AzureRmNetworkWatcherResourceTroubleshooting` на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="59d0b-124">The `$networkWatcher` variable is passed to the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="59d0b-125">Получение сведений о подключении к шлюзу виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="59d0b-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="59d0b-126">В этом примере выполняется устранение неполадок с таким ресурсом, как подключение.</span><span class="sxs-lookup"><span data-stu-id="59d0b-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="59d0b-127">Его также можно передать шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="59d0b-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="59d0b-128">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="59d0b-128">Create a storage account</span></span>

<span data-ttu-id="59d0b-129">При устранении неполадок с ресурсами возвращаются данные о работоспособности ресурса, а также сохраняются журналы в учетную запись хранения для анализа.</span><span class="sxs-lookup"><span data-stu-id="59d0b-129">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="59d0b-130">На этом этапе мы создадим учетную запись хранения. При необходимости можно использовать имеющуюся учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="59d0b-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="59d0b-131">Выполнение устранения неполадок с ресурсами Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="59d0b-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="59d0b-132">Для устранения неполадок с ресурсами используется командлет `Start-AzureRmNetworkWatcherResourceTroubleshooting`.</span><span class="sxs-lookup"><span data-stu-id="59d0b-132">You troubleshoot resources with the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="59d0b-133">В командлет нужно передать объект Наблюдателя за сетями, идентификатор подключения или шлюза виртуальной сети, идентификатор учетной записи хранения и путь, по которому будут храниться результаты.</span><span class="sxs-lookup"><span data-stu-id="59d0b-133">We pass the cmdlet the Network Watcher object, the Id of the Connection or Virtual Network Gateway, the storage account id, and the path to store the results.</span></span>

> [!NOTE]
> <span data-ttu-id="59d0b-134">Командлет `Start-AzureRmNetworkWatcherResourceTroubleshooting` выполняется длительное время. Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="59d0b-134">The `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes to complete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="59d0b-135">После выполнения командлета Наблюдатель за сетями просматривает ресурсы, чтобы проверить их работоспособность.</span><span class="sxs-lookup"><span data-stu-id="59d0b-135">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="59d0b-136">Он возвращает результаты в оболочку и сохраняет журналы результатов в указанной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="59d0b-136">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="59d0b-137">Анализ результатов</span><span class="sxs-lookup"><span data-stu-id="59d0b-137">Understanding the results</span></span>

<span data-ttu-id="59d0b-138">Текст действий содержит общие рекомендации по устранению проблемы.</span><span class="sxs-lookup"><span data-stu-id="59d0b-138">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="59d0b-139">Если для устранения проблемы можно что-то сделать, предоставляется ссылка на дополнительные инструкции.</span><span class="sxs-lookup"><span data-stu-id="59d0b-139">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="59d0b-140">Если дополнительных рекомендаций нет, в ответе указывается URL-адрес, открыв который можно отправить запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="59d0b-140">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="59d0b-141">Дополнительные сведения о свойствах ответа, а также о данных, которые он содержит, см. в статье [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md) (Обзор устранения неполадок наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="59d0b-141">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="59d0b-142">Инструкции по скачиванию файлов из учетных записей хранения Azure см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="59d0b-142">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="59d0b-143">Кроме того, можно использовать такое средство, как Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="59d0b-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="59d0b-144">Дополнительные сведения об обозревателе хранилищ см. на [этой странице](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="59d0b-144">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="59d0b-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59d0b-145">Next steps</span></span>

<span data-ttu-id="59d0b-146">Если изменены параметры, которые мешают VPN-подключению, см. статью [Управление группами безопасности сети с помощью портала](../virtual-network/virtual-network-manage-nsg-arm-portal.md), чтобы найти сведения о группах безопасности сети и соответствующие правила безопасности.</span><span class="sxs-lookup"><span data-stu-id="59d0b-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
