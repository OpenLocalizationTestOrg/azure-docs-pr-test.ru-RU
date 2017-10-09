---
title: "aaaTroubleshoot шлюз виртуальной сети Azure и соединений - Azure CLI 1.0 | Документы Microsoft"
description: "На этой странице объясняется, как toouse hello Наблюдатель сети Azure Устранение неполадок Azure CLI 1.0"
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
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="bc15d-103">Устранение неполадок шлюза виртуальной сети и подключений с помощью наблюдателя за сетями Azure и Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bc15d-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="bc15d-104">Портал</span><span class="sxs-lookup"><span data-stu-id="bc15d-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="bc15d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc15d-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="bc15d-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="bc15d-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="bc15d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bc15d-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="bc15d-108">REST API</span><span class="sxs-lookup"><span data-stu-id="bc15d-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="bc15d-109">Наблюдатель сети предоставляет множество возможностей, по отношению к сетевым ресурсам в Azure toounderstanding.</span><span class="sxs-lookup"><span data-stu-id="bc15d-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="bc15d-110">Одна из этих возможностей — устранение неполадок в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="bc15d-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="bc15d-111">Устранение неполадок ресурсов можно вызвать через портал hello, PowerShell, CLI или REST API.</span><span class="sxs-lookup"><span data-stu-id="bc15d-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="bc15d-112">При вызове Наблюдатель сети проверяет работоспособность hello шлюза виртуальной сети или подключения и возвращает результаты.</span><span class="sxs-lookup"><span data-stu-id="bc15d-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="bc15d-113">В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="bc15d-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="bc15d-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="bc15d-114">Before you begin</span></span>

<span data-ttu-id="bc15d-115">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="bc15d-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="bc15d-116">Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="bc15d-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="bc15d-117">Обзор</span><span class="sxs-lookup"><span data-stu-id="bc15d-117">Overview</span></span>

<span data-ttu-id="bc15d-118">Устранение неполадок ресурсов предоставляет возможность hello Устранение неполадок, возникающих с подключениями и шлюзах виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc15d-118">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="bc15d-119">При запросе tooresource Устранение неполадок, журналы, запросы и проверен.</span><span class="sxs-lookup"><span data-stu-id="bc15d-119">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="bc15d-120">После завершения проверки hello результатов.</span><span class="sxs-lookup"><span data-stu-id="bc15d-120">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="bc15d-121">Запрашивает ресурс, который долго выполняющиеся запросы по устранению неполадок, которой может занять несколько минут tooreturn результат.</span><span class="sxs-lookup"><span data-stu-id="bc15d-121">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="bc15d-122">Устранение неполадок журналы Hello хранятся в контейнер в учетной записи хранилища, который указан.</span><span class="sxs-lookup"><span data-stu-id="bc15d-122">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="bc15d-123">Получение сведений о подключении к шлюзу виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="bc15d-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="bc15d-124">В этом примере выполняется устранение неполадок с таким ресурсом, как подключение.</span><span class="sxs-lookup"><span data-stu-id="bc15d-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="bc15d-125">Его также можно передать шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc15d-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="bc15d-126">Hello следующий командлет отображает hello vpn подключений в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bc15d-126">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="bc15d-127">Также можно запустить команду toosee hello hello подключений в подписке.</span><span class="sxs-lookup"><span data-stu-id="bc15d-127">You can also run hello command toosee hello connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="bc15d-128">Получив имя hello подключения hello, tooget этой команды можно выполнить его идентификатором ресурса:</span><span class="sxs-lookup"><span data-stu-id="bc15d-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="bc15d-129">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="bc15d-129">Create a storage account</span></span>

<span data-ttu-id="bc15d-130">Устранение неполадок ресурсов возвращает данные о работоспособности hello hello ресурса, также сохраняет журналы tooa хранилища учетной записи toobe проверены.</span><span class="sxs-lookup"><span data-stu-id="bc15d-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="bc15d-131">На этом этапе мы создадим учетную запись хранения. При необходимости можно использовать имеющуюся учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="bc15d-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="bc15d-132">Создать учетную запись хранения hello</span><span class="sxs-lookup"><span data-stu-id="bc15d-132">Create hello storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="bc15d-133">Получить ключи учетной записи хранения hello</span><span class="sxs-lookup"><span data-stu-id="bc15d-133">Get hello storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="bc15d-134">Создание контейнера hello</span><span class="sxs-lookup"><span data-stu-id="bc15d-134">Create hello container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="bc15d-135">Выполнение устранения неполадок с ресурсами Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="bc15d-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="bc15d-136">Устранение ресурсы с hello `network watcher troubleshoot` командлета.</span><span class="sxs-lookup"><span data-stu-id="bc15d-136">You troubleshoot resources with hello `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="bc15d-137">Мы передаем группы ресурсов hello командлет hello, hello имя hello Наблюдатель сети, hello идентификатор соединения hello hello идентификатор учетной записи хранения hello и hello путь toohello большого двоичного объекта toostore hello диагностики результаты в.</span><span class="sxs-lookup"><span data-stu-id="bc15d-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="bc15d-138">После выполнения командлета hello Наблюдатель сети проверки работоспособности hello tooverify ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="bc15d-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="bc15d-139">Он возвращает результаты hello toohello оболочки и сохраняет журналы hello результатов в указанную учетную запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="bc15d-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="bc15d-140">Основные сведения о результатах hello</span><span class="sxs-lookup"><span data-stu-id="bc15d-140">Understanding hello results</span></span>

<span data-ttu-id="bc15d-141">текст Hello действия даются общие рекомендации по как tooresolve hello проблему.</span><span class="sxs-lookup"><span data-stu-id="bc15d-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="bc15d-142">Если действие может устранить проблему hello, ссылка предоставляется с Дополнительные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="bc15d-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="bc15d-143">В случае hello которых нет Дополнительные рекомендации, ответ hello предоставляет tooopen URL-адрес hello обращение в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="bc15d-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="bc15d-144">Дополнительные сведения о свойствах hello ответа hello и которые не включены [Общие сведения об устранении Наблюдатель сети](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bc15d-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="bc15d-145">Инструкции по загрузке файлов из учетных записей хранилища azure, см. в разделе слишком[приступить к работе с хранилищем больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="bc15d-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="bc15d-146">Кроме того, можно использовать такое средство, как Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="bc15d-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="bc15d-147">Дополнительные сведения об обозревателе хранилища можно найти по ссылке hello здесь: [обозреватель хранилищ](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="bc15d-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc15d-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc15d-148">Next steps</span></span>

<span data-ttu-id="bc15d-149">Если параметры были изменены, остановите подключения VPN, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, возможно, в вопросе.</span><span class="sxs-lookup"><span data-stu-id="bc15d-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
