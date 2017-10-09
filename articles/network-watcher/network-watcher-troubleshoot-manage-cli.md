---
title: "aaaTroubleshoot шлюз виртуальной сети Azure и соединений - CLI Azure 2.0 | Документы Microsoft"
description: "На этой странице объясняется, как toouse hello Наблюдатель сети Azure Устранение неполадок Azure CLI 2.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 389e86f247722412a1d0e2e722dbf80bb7cff291
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a><span data-ttu-id="a09d7-103">Устранение неполадок шлюза виртуальной сети и подключений с помощью наблюдателя за сетями Azure и Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a09d7-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a09d7-104">Портал</span><span class="sxs-lookup"><span data-stu-id="a09d7-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="a09d7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a09d7-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="a09d7-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="a09d7-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="a09d7-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a09d7-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="a09d7-108">REST API</span><span class="sxs-lookup"><span data-stu-id="a09d7-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="a09d7-109">Наблюдатель сети предоставляет множество возможностей, по отношению к сетевым ресурсам в Azure toounderstanding.</span><span class="sxs-lookup"><span data-stu-id="a09d7-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="a09d7-110">Одна из этих возможностей — устранение неполадок в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="a09d7-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="a09d7-111">Устранение неполадок ресурсов можно вызвать через портал hello, PowerShell, CLI или REST API.</span><span class="sxs-lookup"><span data-stu-id="a09d7-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="a09d7-112">При вызове Наблюдатель сети проверяет работоспособность hello шлюза виртуальной сети или подключения и возвращает результаты.</span><span class="sxs-lookup"><span data-stu-id="a09d7-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="a09d7-113">В этой статье используется нашей следующего поколения CLI для модели развертывания управления ресурса hello Azure CLI 2.0, которая доступна для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="a09d7-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="a09d7-114">tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a09d7-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a09d7-115">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a09d7-115">Before you begin</span></span>

<span data-ttu-id="a09d7-116">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="a09d7-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="a09d7-117">Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="a09d7-117">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="a09d7-118">Обзор</span><span class="sxs-lookup"><span data-stu-id="a09d7-118">Overview</span></span>

<span data-ttu-id="a09d7-119">Устранение неполадок ресурсов предоставляет возможность hello Устранение неполадок, возникающих с подключениями и шлюзах виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a09d7-119">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="a09d7-120">При запросе tooresource Устранение неполадок, журналы, запросы и проверен.</span><span class="sxs-lookup"><span data-stu-id="a09d7-120">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="a09d7-121">После завершения проверки hello результатов.</span><span class="sxs-lookup"><span data-stu-id="a09d7-121">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="a09d7-122">Запрашивает ресурс, который долго выполняющиеся запросы по устранению неполадок, которой может занять несколько минут tooreturn результат.</span><span class="sxs-lookup"><span data-stu-id="a09d7-122">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="a09d7-123">Устранение неполадок журналы Hello хранятся в контейнер в учетной записи хранилища, который указан.</span><span class="sxs-lookup"><span data-stu-id="a09d7-123">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="a09d7-124">Получение сведений о подключении к шлюзу виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="a09d7-124">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="a09d7-125">В этом примере выполняется устранение неполадок с таким ресурсом, как подключение.</span><span class="sxs-lookup"><span data-stu-id="a09d7-125">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="a09d7-126">Его также можно передать шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a09d7-126">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="a09d7-127">Hello следующий командлет отображает hello vpn подключений в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a09d7-127">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

<span data-ttu-id="a09d7-128">Получив имя hello подключения hello, tooget этой команды можно выполнить его идентификатором ресурса:</span><span class="sxs-lookup"><span data-stu-id="a09d7-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a><span data-ttu-id="a09d7-129">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="a09d7-129">Create a storage account</span></span>

<span data-ttu-id="a09d7-130">Устранение неполадок ресурсов возвращает данные о работоспособности hello hello ресурса, также сохраняет журналы tooa хранилища учетной записи toobe проверены.</span><span class="sxs-lookup"><span data-stu-id="a09d7-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="a09d7-131">На этом этапе мы создадим учетную запись хранения. При необходимости можно использовать имеющуюся учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="a09d7-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="a09d7-132">Создать учетную запись хранения hello</span><span class="sxs-lookup"><span data-stu-id="a09d7-132">Create hello storage account</span></span>

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. <span data-ttu-id="a09d7-133">Получить ключи учетной записи хранения hello</span><span class="sxs-lookup"><span data-stu-id="a09d7-133">Get hello storage account keys</span></span>

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. <span data-ttu-id="a09d7-134">Создание контейнера hello</span><span class="sxs-lookup"><span data-stu-id="a09d7-134">Create hello container</span></span>

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="a09d7-135">Выполнение устранения неполадок с ресурсами Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="a09d7-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="a09d7-136">Устранение ресурсы с hello `az network watcher troubleshooting` командлета.</span><span class="sxs-lookup"><span data-stu-id="a09d7-136">You troubleshoot resources with hello `az network watcher troubleshooting` cmdlet.</span></span> <span data-ttu-id="a09d7-137">Мы передаем группы ресурсов hello командлет hello, hello имя hello Наблюдатель сети, hello идентификатор соединения hello hello идентификатор учетной записи хранения hello и hello путь toohello большого двоичного объекта toostore hello диагностики результаты в.</span><span class="sxs-lookup"><span data-stu-id="a09d7-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

<span data-ttu-id="a09d7-138">После выполнения командлета hello Наблюдатель сети проверки работоспособности hello tooverify ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="a09d7-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="a09d7-139">Он возвращает результаты hello toohello оболочки и сохраняет журналы hello результатов в указанную учетную запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="a09d7-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="a09d7-140">Основные сведения о результатах hello</span><span class="sxs-lookup"><span data-stu-id="a09d7-140">Understanding hello results</span></span>

<span data-ttu-id="a09d7-141">текст Hello действия даются общие рекомендации по как tooresolve hello проблему.</span><span class="sxs-lookup"><span data-stu-id="a09d7-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="a09d7-142">Если действие может устранить проблему hello, ссылка предоставляется с Дополнительные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="a09d7-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="a09d7-143">В случае hello которых нет Дополнительные рекомендации, ответ hello предоставляет tooopen URL-адрес hello обращение в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="a09d7-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="a09d7-144">Дополнительные сведения о свойствах hello ответа hello и которые не включены [Общие сведения об устранении Наблюдатель сети](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a09d7-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="a09d7-145">Инструкции по загрузке файлов из учетных записей хранилища azure, см. в разделе слишком[приступить к работе с хранилищем больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="a09d7-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="a09d7-146">Кроме того, можно использовать такое средство, как Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="a09d7-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="a09d7-147">Дополнительные сведения об обозревателе хранилища можно найти по ссылке hello здесь: [обозреватель хранилищ](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="a09d7-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a09d7-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a09d7-148">Next steps</span></span>

<span data-ttu-id="a09d7-149">Если параметры были изменены, остановите подключения VPN, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, возможно, в вопросе.</span><span class="sxs-lookup"><span data-stu-id="a09d7-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
