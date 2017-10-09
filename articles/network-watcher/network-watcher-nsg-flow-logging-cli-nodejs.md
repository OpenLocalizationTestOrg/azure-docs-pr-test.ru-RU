---
title: "Заносит в журнал aaaManage потока группы безопасности сети с Наблюдатель сети Azure — Azure CLI 1.0 | Документы Microsoft"
description: "На этой странице объясняется, как журналы toomanage потока группы безопасности сети в Azure Наблюдатель сети с помощью Azure CLI 1.0"
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
ms.openlocfilehash: 2535eea665a99cffe7569a8d976333435f946a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a><span data-ttu-id="41200-103">Настройка журналов потоков для групп безопасности сети с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="41200-103">Configuring Network Security Group Flow logs with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="41200-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="41200-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="41200-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="41200-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="41200-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="41200-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="41200-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="41200-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="41200-108">REST API</span><span class="sxs-lookup"><span data-stu-id="41200-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="41200-109">Сетевая группа безопасности потока журналы являются возможностью Наблюдатель сети, который позволяет вам tooview сведения о входящего и исходящего IP-трафика через группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="41200-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="41200-110">Эти потока журналы записываются в формате json и Показать исходящих и входящих потоков на основе каждого правила hello потока hello сетевого Адаптера, применяется 5-фрагментному сведения о потоке hello (источник и назначение IP-адрес, порт источника или целевой Protocol) и если hello был разрешен трафик или запрещено.</span><span class="sxs-lookup"><span data-stu-id="41200-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="41200-111">В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="41200-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="41200-112">Наблюдатель за сетями в настоящее время использует Azure CLI 1.0 в качестве интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="41200-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="41200-113">Регистрация поставщика Microsoft Insights</span><span class="sxs-lookup"><span data-stu-id="41200-113">Register Insights provider</span></span>

<span data-ttu-id="41200-114">В порядке для потока toowork ведения журнала успешно, hello **помощью Microsoft.Insights** должен быть зарегистрирован поставщик.</span><span class="sxs-lookup"><span data-stu-id="41200-114">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="41200-115">Если вы не уверены в том случае, если hello **помощью Microsoft.Insights** поставщик является зарегистрированным, запустите hello следующий скрипт.</span><span class="sxs-lookup"><span data-stu-id="41200-115">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="41200-116">Включение журналов потоков для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="41200-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="41200-117">Следующий пример hello показано Hello команда tooenable потока журналов:</span><span class="sxs-lookup"><span data-stu-id="41200-117">hello command tooenable flow logs is shown in hello following example:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="41200-118">Отключение журналов потоков для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="41200-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="41200-119">Hello используйте следующий пример toodisable потока журналов:</span><span class="sxs-lookup"><span data-stu-id="41200-119">Use hello following example toodisable flow logs:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="41200-120">Скачивание журнала потоков</span><span class="sxs-lookup"><span data-stu-id="41200-120">Download a Flow log</span></span>

<span data-ttu-id="41200-121">место хранения Hello потока журнала определяется при его создании.</span><span class="sxs-lookup"><span data-stu-id="41200-121">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="41200-122">Удобное средство tooaccess, эти учетной записи хранения потока сохраняться журналы tooa: Обозреватель хранилищ Microsoft Azure, которую можно загрузить здесь: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="41200-122">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="41200-123">При указании учетной записи хранилища пакетов отслеживания файлы сохраняются tooa учетной записи хранилища в hello следующие расположения:</span><span class="sxs-lookup"><span data-stu-id="41200-123">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="41200-124">Сведения о структуре hello hello журнала [потока группы безопасности сети журнала Обзор](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="41200-124">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="41200-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41200-125">Next Steps</span></span>

<span data-ttu-id="41200-126">Узнайте, каким образом слишком[визуализировать журналов потока NSG с PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="41200-126">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="41200-127">Узнайте, каким образом слишком[визуализировать NSG потока журналов с помощью средств с открытым исходным кодом](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="41200-127">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
