---
title: "снимки aaaManage пакетов с Наблюдатель сети Azure — Azure CLI 2.0 | Документы Microsoft"
description: "На этой странице объясняется, как toomanage hello функция записи пакетов с помощью Azure CLI 2.0 Наблюдатель сети"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="7f8f9-103">Управление записью пакетов с помощью Наблюдателя за сетями Azure в Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7f8f9-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7f8f9-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="7f8f9-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="7f8f9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f8f9-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="7f8f9-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="7f8f9-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="7f8f9-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7f8f9-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="7f8f9-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="7f8f9-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="7f8f9-109">Захват пакетов Наблюдатель сети позволяет tooand toocreate отслеживания сеансов tootrack трафик от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="7f8f9-110">Можно записать только трафик hello нужные фильтры предоставляются для tooensure сеанс отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="7f8f9-111">Захват пакетов помогает аномалий toodiagnose сети как реактивный, так и заранее.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="7f8f9-112">Другим пользователям включать сбор статистики сети, получение сведений о сети вторжений, toodebug клиент сервер, связи и многое другое.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="7f8f9-113">Из-за захват пакетов может tooremotely триггера, эта возможность облегчает нагрузку hello выполнения захват пакетов на нужный машины hello, чтобы экономить время и вручную.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="7f8f9-114">В этой статье используется нашей следующего поколения CLI для модели развертывания управления ресурса hello Azure CLI 2.0, которая доступна для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-114">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="7f8f9-115">tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="7f8f9-115">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="7f8f9-116">В этой статье описывается hello задачи управления, которые в настоящее время доступны для получения пакетов.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-116">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="7f8f9-117">**Запуск записи пакета**</span><span class="sxs-lookup"><span data-stu-id="7f8f9-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="7f8f9-118">**Прекращение записи пакета**</span><span class="sxs-lookup"><span data-stu-id="7f8f9-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="7f8f9-119">**Удаление записи пакета**</span><span class="sxs-lookup"><span data-stu-id="7f8f9-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="7f8f9-120">**Скачивание записи пакета**</span><span class="sxs-lookup"><span data-stu-id="7f8f9-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="7f8f9-121">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="7f8f9-121">Before you begin</span></span>

<span data-ttu-id="7f8f9-122">В этой статье предполагается, что hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="7f8f9-122">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="7f8f9-123">Экземпляр Наблюдатель сети в регионе hello нужно toocreate захват пакетов</span><span class="sxs-lookup"><span data-stu-id="7f8f9-123">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="7f8f9-124">Виртуальная машина с пакет приветствия записать расширение включено.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-124">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f8f9-125">Захват пакетов требуется toobe агент, работающий на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-125">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="7f8f9-126">Hello агент установлен в качестве расширения.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-126">hello Agent is installed as an extension.</span></span> <span data-ttu-id="7f8f9-127">Инструкции по расширениям виртуальных машин см. в статье [Обзор расширений и компонентов виртуальной машины под управлением Windows](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="7f8f9-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="7f8f9-128">Установка расширения виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7f8f9-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="7f8f9-129">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="7f8f9-129">Step 1</span></span>

<span data-ttu-id="7f8f9-130">Запустите hello `az vm extension set` агент командлет tooinstall hello пакет отслеживания на hello гостевой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-130">Run hello `az vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="7f8f9-131">Для виртуальных машин Windows:</span><span class="sxs-lookup"><span data-stu-id="7f8f9-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="7f8f9-132">Для виртуальных машин Linux:</span><span class="sxs-lookup"><span data-stu-id="7f8f9-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="7f8f9-133">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="7f8f9-133">Step 2</span></span>

<span data-ttu-id="7f8f9-134">tooensure, hello агент установлен, запустите hello `vm extension get` командлета и передать его в группу ресурсов hello и имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-134">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="7f8f9-135">Убедитесь, что установлен hello полученный список tooensure hello агент.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-135">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="7f8f9-136">Следующий образец Hello приведен пример ответа hello, запуск`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="7f8f9-136">hello following sample is an example of hello response from running `az vm extension show`</span></span>

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="7f8f9-137">Запуск записи пакета</span><span class="sxs-lookup"><span data-stu-id="7f8f9-137">Start a packet capture</span></span>

<span data-ttu-id="7f8f9-138">После hello предыдущего выполнения действий, hello пакет отслеживания агент устанавливается на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="7f8f9-139">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="7f8f9-139">Step 1</span></span>

<span data-ttu-id="7f8f9-140">Hello следующим шагом является экземпляр Наблюдатель сети tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="7f8f9-141">Указанное имя hello Наблюдатель сети передается toohello `az network watcher show` командлет на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-141">TThe name of hello Network Watcher is passed toohello `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="7f8f9-142">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="7f8f9-142">Step 2</span></span>

<span data-ttu-id="7f8f9-143">Получите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-143">Retrieve a storage account.</span></span> <span data-ttu-id="7f8f9-144">Эта учетная запись хранения — файл записи пакетов используется toostore hello.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-144">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="7f8f9-145">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-145">Step 3</span></span>

<span data-ttu-id="7f8f9-146">Фильтры можно использовать toolimit hello данные, которые хранятся с захватом пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="7f8f9-147">Hello следующий пример устанавливает захват пакетов с несколькими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-147">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="7f8f9-148">Hello первые три фильтры собирать исходящего трафика TCP только с локального IP-адреса 10.0.0.3 toodestination порты 20, 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-148">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="7f8f9-149">последний фильтр Hello собирает только трафик UDP.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-149">hello last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="7f8f9-150">Hello следующий пример является hello ожидалось результатов выполнения hello `az network watcher packet-capture create` командлета.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-150">hello following example is hello expected output from running hello `az network watcher packet-capture create` cmdlet.</span></span>

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="7f8f9-151">Получение записи пакета</span><span class="sxs-lookup"><span data-stu-id="7f8f9-151">Get a packet capture</span></span>

<span data-ttu-id="7f8f9-152">Под управлением hello `az network watcher packet-capture show` , получает hello состояние выполняющегося или завершенного отслеживания пакетов.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-152">Running hello `az network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="7f8f9-153">Hello ниже приведен вывод hello hello `az network watcher packet-capture show` командлета.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-153">hello following example is hello output from hello `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="7f8f9-154">Hello следующий пример — после завершения записи hello.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-154">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="7f8f9-155">Hello значение PacketCaptureStatus остановлена с StopReason TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-155">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="7f8f9-156">Это значение показывает, что захват пакетов hello прошла успешно и время его запуска.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-156">This value shows that hello packet capture was successful and ran its time.</span></span>

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="7f8f9-157">Прекращение записи пакета</span><span class="sxs-lookup"><span data-stu-id="7f8f9-157">Stop a packet capture</span></span>

<span data-ttu-id="7f8f9-158">Запустив hello `az network watcher packet-capture stop` командлета, если записи сеанса выполняется она остановлена.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-158">By running hello `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="7f8f9-159">Hello командлет не возвращает ответа при выполнялись в момент записи сеанса или существующего сеанса, который уже был остановлен.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-159">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="7f8f9-160">Удаление записи пакета</span><span class="sxs-lookup"><span data-stu-id="7f8f9-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="7f8f9-161">Удаление захват пакетов не приводит к удалению файла hello в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-161">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="7f8f9-162">Скачивание записи пакета</span><span class="sxs-lookup"><span data-stu-id="7f8f9-162">Download a packet capture</span></span>

<span data-ttu-id="7f8f9-163">После завершения сеанса записи пакета файл записи hello может быть загруженного tooblob хранилища или tooa локальный файл на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-163">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="7f8f9-164">место хранения Hello hello захват пакетов определяется при создании сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="7f8f9-164">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="7f8f9-165">Tooaccess удобное средство их записывать файлы, сохраненные tooa учетную запись хранения является обозреватель хранилищ Microsoft Azure, которую можно загрузить здесь: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="7f8f9-165">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="7f8f9-166">При указании учетной записи хранилища пакетов отслеживания файлы сохраняются tooa учетной записи хранилища в hello следующие расположения:</span><span class="sxs-lookup"><span data-stu-id="7f8f9-166">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="7f8f9-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f8f9-167">Next steps</span></span>

<span data-ttu-id="7f8f9-168">Узнайте, как снимки tooautomate пакетов с оповещениями виртуальной машины, просмотрев [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="7f8f9-168">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="7f8f9-169">Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7f8f9-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
