---
title: "Устранение неполадок шлюза виртуальной сети и подключений Azure — Azure CLI 1.0 | Документы Майкрософт"
description: "На этой странице объясняется, как устранить неполадки с помощью наблюдателя за сетями и Azure CLI 1.0"
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
ms.openlocfilehash: 9de4b2a0bdda7ffbd269883877a708d67312092f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="0cf90-103">Устранение неполадок шлюза виртуальной сети и подключений с помощью наблюдателя за сетями Azure и Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0cf90-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0cf90-104">Портал</span><span class="sxs-lookup"><span data-stu-id="0cf90-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="0cf90-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cf90-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="0cf90-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="0cf90-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="0cf90-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0cf90-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="0cf90-108">REST API</span><span class="sxs-lookup"><span data-stu-id="0cf90-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="0cf90-109">Наблюдатель за сетями предоставляет множество возможностей, так как он позволяет проанализировать сетевые ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="0cf90-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="0cf90-110">Одна из этих возможностей — устранение неполадок в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="0cf90-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="0cf90-111">Процедуру устранения неполадок с ресурсами можно вызывать с помощью портала, PowerShell, интерфейса командной строки или API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="0cf90-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="0cf90-112">При вызове Наблюдатель за сетями проверяет работоспособность шлюза виртуальной сети или подключения и возвращает результаты.</span><span class="sxs-lookup"><span data-stu-id="0cf90-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="0cf90-113">В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="0cf90-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="0cf90-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="0cf90-114">Before you begin</span></span>

<span data-ttu-id="0cf90-115">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create an Azure Network Watcher instance](network-watcher-create.md) (Наблюдатель за сетями: создание экземпляра службы).</span><span class="sxs-lookup"><span data-stu-id="0cf90-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="0cf90-116">Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="0cf90-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="0cf90-117">Обзор</span><span class="sxs-lookup"><span data-stu-id="0cf90-117">Overview</span></span>

<span data-ttu-id="0cf90-118">В ходе устранения неполадок с ресурсами вы можете устранить проблемы, возникающие со шлюзами виртуальной сети и подключениями.</span><span class="sxs-lookup"><span data-stu-id="0cf90-118">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="0cf90-119">При запросе на устранение неполадок с ресурсами запрашиваются и проверяются журналы.</span><span class="sxs-lookup"><span data-stu-id="0cf90-119">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="0cf90-120">По завершении проверки возвращаются результаты.</span><span class="sxs-lookup"><span data-stu-id="0cf90-120">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="0cf90-121">Запросы на устранение неполадок с ресурсами выполняются долго, поэтому для возвращения результатов может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="0cf90-121">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="0cf90-122">Журналы, используемые при устранении неполадок, хранятся в контейнере указанной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0cf90-122">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="0cf90-123">Получение сведений о подключении к шлюзу виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="0cf90-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="0cf90-124">В этом примере выполняется устранение неполадок с таким ресурсом, как подключение.</span><span class="sxs-lookup"><span data-stu-id="0cf90-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="0cf90-125">Его также можно передать шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0cf90-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="0cf90-126">Следующий командлет выдает список VPN-подключений в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0cf90-126">The following cmdlet lists the vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="0cf90-127">Кроме того, можно выполнить команду, чтобы получить список связей в подписке.</span><span class="sxs-lookup"><span data-stu-id="0cf90-127">You can also run the command to see the connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="0cf90-128">Получив имя подключения, можно выполнить приведенную ниже команду, чтобы получить его идентификатор ресурса.</span><span class="sxs-lookup"><span data-stu-id="0cf90-128">Once you have the name of the connection, you can run this command to get its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="0cf90-129">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="0cf90-129">Create a storage account</span></span>

<span data-ttu-id="0cf90-130">При устранении неполадок с ресурсами возвращаются данные о работоспособности ресурса, а также сохраняются журналы в учетную запись хранения для анализа.</span><span class="sxs-lookup"><span data-stu-id="0cf90-130">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="0cf90-131">На этом этапе мы создадим учетную запись хранения. При необходимости можно использовать имеющуюся учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="0cf90-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="0cf90-132">Создание учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="0cf90-132">Create the storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="0cf90-133">Получение ключей учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="0cf90-133">Get the storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="0cf90-134">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="0cf90-134">Create the container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="0cf90-135">Выполнение устранения неполадок с ресурсами Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="0cf90-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="0cf90-136">Для устранения неполадок с ресурсами используется командлет `network watcher troubleshoot`.</span><span class="sxs-lookup"><span data-stu-id="0cf90-136">You troubleshoot resources with the `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="0cf90-137">В командлет нужно передать группу ресурсов, имя экземпляра Наблюдателя за сетями, идентификатор подключения, идентификатор учетной записи хранения и путь к большому двоичному объекту, в котором будут храниться результаты устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="0cf90-137">We pass the cmdlet the resource group, the name of the Network Watcher, the Id of the connection, the Id of the storage account, and the path to the blob to store the troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="0cf90-138">После выполнения командлета Наблюдатель за сетями просматривает ресурсы, чтобы проверить их работоспособность.</span><span class="sxs-lookup"><span data-stu-id="0cf90-138">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="0cf90-139">Он возвращает результаты в оболочку и сохраняет журналы результатов в указанной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0cf90-139">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="0cf90-140">Анализ результатов</span><span class="sxs-lookup"><span data-stu-id="0cf90-140">Understanding the results</span></span>

<span data-ttu-id="0cf90-141">Текст действий содержит общие рекомендации по устранению проблемы.</span><span class="sxs-lookup"><span data-stu-id="0cf90-141">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="0cf90-142">Если для устранения проблемы можно что-то сделать, предоставляется ссылка на дополнительные инструкции.</span><span class="sxs-lookup"><span data-stu-id="0cf90-142">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="0cf90-143">Если дополнительных рекомендаций нет, в ответе указывается URL-адрес, открыв который можно отправить запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="0cf90-143">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="0cf90-144">Дополнительные сведения о свойствах ответа, а также о данных, которые он содержит, см. в статье [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md) (Обзор устранения неполадок наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="0cf90-144">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="0cf90-145">Инструкции по скачиванию файлов из учетных записей хранения Azure см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="0cf90-145">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="0cf90-146">Кроме того, можно использовать такое средство, как Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="0cf90-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="0cf90-147">Дополнительные сведения об обозревателе хранилищ см. на [этой странице](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="0cf90-147">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cf90-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0cf90-148">Next steps</span></span>

<span data-ttu-id="0cf90-149">Если изменены параметры, которые мешают VPN-подключению, см. статью [Управление группами безопасности сети с помощью портала](../virtual-network/virtual-network-manage-nsg-arm-portal.md), чтобы найти сведения о группах безопасности сети и соответствующие правила безопасности.</span><span class="sxs-lookup"><span data-stu-id="0cf90-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
