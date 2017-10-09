---
title: "aaaTroubleshoot шлюз виртуальной сети Azure и соединения — PowerShell | Документы Microsoft"
description: "На этой странице объясняется, как toouse hello Наблюдатель сети Azure устранения командлет PowerShell"
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
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="bb972-103">Устранение неполадок шлюза виртуальной сети и подключений с помощью Наблюдателя за сетями Azure и PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb972-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="bb972-104">Портал</span><span class="sxs-lookup"><span data-stu-id="bb972-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="bb972-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb972-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="bb972-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="bb972-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="bb972-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bb972-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="bb972-108">REST API</span><span class="sxs-lookup"><span data-stu-id="bb972-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="bb972-109">Наблюдатель сети предоставляет множество возможностей, по отношению к сетевым ресурсам в Azure toounderstanding.</span><span class="sxs-lookup"><span data-stu-id="bb972-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="bb972-110">Одна из этих возможностей — устранение неполадок в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="bb972-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="bb972-111">Устранение неполадок ресурсов можно вызвать через портал hello, PowerShell, CLI или REST API.</span><span class="sxs-lookup"><span data-stu-id="bb972-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="bb972-112">При вызове Наблюдатель сети проверяет работоспособность hello шлюза виртуальной сети или подключения и возвращает результаты.</span><span class="sxs-lookup"><span data-stu-id="bb972-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bb972-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="bb972-113">Before you begin</span></span>

<span data-ttu-id="bb972-114">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="bb972-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="bb972-115">Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="bb972-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="bb972-116">Обзор</span><span class="sxs-lookup"><span data-stu-id="bb972-116">Overview</span></span>

<span data-ttu-id="bb972-117">Устранение неполадок ресурсов предоставляет возможность hello Устранение неполадок, возникающих с подключениями и шлюзах виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bb972-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="bb972-118">При запросе tooresource Устранение неполадок, журналы, запросы и проверен.</span><span class="sxs-lookup"><span data-stu-id="bb972-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="bb972-119">После завершения проверки hello результатов.</span><span class="sxs-lookup"><span data-stu-id="bb972-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="bb972-120">Запрашивает ресурс, который долго выполняющиеся запросы по устранению неполадок, которой может занять несколько минут tooreturn результат.</span><span class="sxs-lookup"><span data-stu-id="bb972-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="bb972-121">Устранение неполадок журналы Hello хранятся в контейнер в учетной записи хранилища, который указан.</span><span class="sxs-lookup"><span data-stu-id="bb972-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="bb972-122">Извлечение Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="bb972-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="bb972-123">Первым шагом Hello — экземпляр Наблюдатель сети tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="bb972-123">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="bb972-124">Hello `$networkWatcher` переменной передается toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` командлет на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="bb972-124">hello `$networkWatcher` variable is passed toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="bb972-125">Получение сведений о подключении к шлюзу виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="bb972-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="bb972-126">В этом примере выполняется устранение неполадок с таким ресурсом, как подключение.</span><span class="sxs-lookup"><span data-stu-id="bb972-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="bb972-127">Его также можно передать шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bb972-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="bb972-128">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="bb972-128">Create a storage account</span></span>

<span data-ttu-id="bb972-129">Устранение неполадок ресурсов возвращает данные о работоспособности hello hello ресурса, также сохраняет журналы tooa хранилища учетной записи toobe проверены.</span><span class="sxs-lookup"><span data-stu-id="bb972-129">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="bb972-130">На этом этапе мы создадим учетную запись хранения. При необходимости можно использовать имеющуюся учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="bb972-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="bb972-131">Выполнение устранения неполадок с ресурсами Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="bb972-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="bb972-132">Устранение ресурсы с hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` командлета.</span><span class="sxs-lookup"><span data-stu-id="bb972-132">You troubleshoot resources with hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="bb972-133">Мы передаем объект Наблюдатель сети hello командлета hello, hello идентификатор hello подключения или шлюза виртуальной сети, ИД учетной записи хранилища hello и hello путь toostore hello результаты.</span><span class="sxs-lookup"><span data-stu-id="bb972-133">We pass hello cmdlet hello Network Watcher object, hello Id of hello Connection or Virtual Network Gateway, hello storage account id, and hello path toostore hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="bb972-134">Hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` командлета является долго выполняющихся и может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="bb972-134">hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes toocomplete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="bb972-135">После выполнения командлета hello Наблюдатель сети проверки работоспособности hello tooverify ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="bb972-135">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="bb972-136">Он возвращает результаты hello toohello оболочки и сохраняет журналы hello результатов в указанную учетную запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="bb972-136">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="bb972-137">Основные сведения о результатах hello</span><span class="sxs-lookup"><span data-stu-id="bb972-137">Understanding hello results</span></span>

<span data-ttu-id="bb972-138">текст Hello действия даются общие рекомендации по как tooresolve hello проблему.</span><span class="sxs-lookup"><span data-stu-id="bb972-138">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="bb972-139">Если действие может устранить проблему hello, ссылка предоставляется с Дополнительные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="bb972-139">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="bb972-140">В случае hello которых нет Дополнительные рекомендации, ответ hello предоставляет tooopen URL-адрес hello обращение в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="bb972-140">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="bb972-141">Дополнительные сведения о свойствах hello ответа hello и которые не включены [Общие сведения об устранении Наблюдатель сети](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bb972-141">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="bb972-142">Инструкции по загрузке файлов из учетных записей хранилища azure, см. в разделе слишком[приступить к работе с хранилищем больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="bb972-142">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="bb972-143">Кроме того, можно использовать такое средство, как Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="bb972-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="bb972-144">Дополнительные сведения об обозревателе хранилища можно найти по ссылке hello здесь: [обозреватель хранилищ](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="bb972-144">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb972-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb972-145">Next steps</span></span>

<span data-ttu-id="bb972-146">Если параметры были изменены, остановите подключения VPN, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, возможно, в вопросе.</span><span class="sxs-lookup"><span data-stu-id="bb972-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
