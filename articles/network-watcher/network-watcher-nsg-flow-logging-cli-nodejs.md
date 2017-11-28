---
title: "Управление журналами потоков для групп безопасности сети с помощью Наблюдателя за сетями (Azure CLI 1.0) | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как управлять журналами потоков для групп безопасности сети с помощью Наблюдателя за сетями в Azure CLI 1.0."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ea8543857c062e76f96da99fb295ce831c3c5f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a><span data-ttu-id="ba8e8-103">Настройка журналов потоков для групп безопасности сети с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ba8e8-103">Configuring Network Security Group Flow logs with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ba8e8-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ba8e8-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="ba8e8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba8e8-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="ba8e8-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="ba8e8-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="ba8e8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ba8e8-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="ba8e8-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ba8e8-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="ba8e8-109">Журналы потоков для групп безопасности сети — это компонент Наблюдателя за сетями, который позволяет просматривать сведения о входящем и исходящем IP-трафике через группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="ba8e8-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="ba8e8-110">Эти журналы потоков записываются в формате JSON. В них отображаются входящие и исходящие потоки по каждому правилу, сетевая карта, с которой связан поток, сведения о 5 кортежах потока (IP-адрес источника и места назначения, порт источника и места назначения, протокол), а также сведения о состоянии трафика (разрешен или запрещен).</span><span class="sxs-lookup"><span data-stu-id="ba8e8-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="ba8e8-111">В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="ba8e8-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="ba8e8-112">Наблюдатель за сетями в настоящее время использует Azure CLI 1.0 в качестве интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="ba8e8-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="ba8e8-113">Регистрация поставщика Microsoft Insights</span><span class="sxs-lookup"><span data-stu-id="ba8e8-113">Register Insights provider</span></span>

<span data-ttu-id="ba8e8-114">Для успешного ведения журналов потоков должен быть зарегистрирован поставщик **Microsoft.Insights**.</span><span class="sxs-lookup"><span data-stu-id="ba8e8-114">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="ba8e8-115">Если вы не знаете, зарегистрирован ли поставщик **Microsoft.Insights**, выполните следующий сценарий.</span><span class="sxs-lookup"><span data-stu-id="ba8e8-115">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="ba8e8-116">Включение журналов потоков для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="ba8e8-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="ba8e8-117">Команда для включения журналов потоков показана в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="ba8e8-117">The command to enable flow logs is shown in the following example:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="ba8e8-118">Отключение журналов потоков для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="ba8e8-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="ba8e8-119">Чтобы отключить журналы потоков, используйте следующий пример:</span><span class="sxs-lookup"><span data-stu-id="ba8e8-119">Use the following example to disable flow logs:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="ba8e8-120">Скачивание журнала потоков</span><span class="sxs-lookup"><span data-stu-id="ba8e8-120">Download a Flow log</span></span>

<span data-ttu-id="ba8e8-121">Место хранения журнала потоков определяется при его создании.</span><span class="sxs-lookup"><span data-stu-id="ba8e8-121">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="ba8e8-122">Удобное средство для доступа к этим журналам потоков, сохраненным в учетной записи хранения — обозреватель службы хранилища Microsoft Azure, который можно скачать по адресу http://storageexplorer.com/.</span><span class="sxs-lookup"><span data-stu-id="ba8e8-122">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="ba8e8-123">При указании учетной записи хранения файлы записи пакетов сохраняются в ней по следующему адресу:</span><span class="sxs-lookup"><span data-stu-id="ba8e8-123">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="ba8e8-124">Сведения о структуре журнала см. в статье [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md) (Обзор журнала потоков для группы безопасности сети).</span><span class="sxs-lookup"><span data-stu-id="ba8e8-124">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba8e8-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba8e8-125">Next Steps</span></span>

<span data-ttu-id="ba8e8-126">Узнайте, как [визуализировать сведения журналов потоков группы безопасности сети с помощью PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="ba8e8-126">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="ba8e8-127">Узнайте, как [визуализировать сведения журналов потоков группы безопасности сети с помощью средств с открытым кодом](network-watcher-visualize-nsg-flow-logs-open-source-tools.md).</span><span class="sxs-lookup"><span data-stu-id="ba8e8-127">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
