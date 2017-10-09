---
title: "Заносит в журнал aaaManage потока сетевой группы безопасности с Наблюдатель сети Azure — REST API | Документы Microsoft"
description: "На этой странице объясняется, как toomanage группы безопасности сети поток входит в Наблюдатель сети Azure с помощью REST API"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: be81e35f4d01c67efef99773e9b4e2ae4b8e209e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="f64fb-103">Настройка журналов потоков для групп безопасности сети с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="f64fb-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f64fb-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="f64fb-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="f64fb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f64fb-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="f64fb-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="f64fb-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="f64fb-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f64fb-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="f64fb-108">REST API</span><span class="sxs-lookup"><span data-stu-id="f64fb-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="f64fb-109">Сетевая группа безопасности потока журналы являются возможностью Наблюдатель сети, который позволяет вам tooview сведения о входящего и исходящего IP-трафика через группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="f64fb-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="f64fb-110">Эти потока журналы записываются в формате json и Показать исходящих и входящих потоков на основе каждого правила hello потока hello сетевого Адаптера, применяется 5-фрагментному сведения о потоке hello (источник и назначение IP-адрес, порт источника или целевой Protocol) и если hello был разрешен трафик или запрещено.</span><span class="sxs-lookup"><span data-stu-id="f64fb-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f64fb-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="f64fb-111">Before you begin</span></span>

<span data-ttu-id="f64fb-112">ARMclient — используется toocall hello REST API с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f64fb-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="f64fb-113">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="f64fb-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="f64fb-114">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="f64fb-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="f64fb-115">Для API-интерфейса REST Наблюдатель сети вызовы hello имя группы ресурсов в запросе hello, что URI является hello группы ресурсов, содержащий hello Наблюдатель сети не hello ресурсы при выполнении hello диагностических действий на.</span><span class="sxs-lookup"><span data-stu-id="f64fb-115">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="f64fb-116">Сценарий</span><span class="sxs-lookup"><span data-stu-id="f64fb-116">Scenario</span></span>

<span data-ttu-id="f64fb-117">Hello сценарий, описанный в этой статье показано, как поток журналы с помощью API-интерфейса REST hello tooenable, отключения и запроса.</span><span class="sxs-lookup"><span data-stu-id="f64fb-117">hello scenario covered in this article shows you how tooenable, disable, and query flow logs using hello REST API.</span></span> <span data-ttu-id="f64fb-118">Посетите toolearn Дополнительные сведения о loggings потока сетевой группы безопасности, [сетевой группы безопасности потока регистрации – Обзор](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f64fb-118">toolearn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="f64fb-119">Вам предстоит:</span><span class="sxs-lookup"><span data-stu-id="f64fb-119">In this scenario, you will:</span></span>

* <span data-ttu-id="f64fb-120">включить журналы потоков;</span><span class="sxs-lookup"><span data-stu-id="f64fb-120">Enable flow logs</span></span>
* <span data-ttu-id="f64fb-121">отключить журналы потоков;</span><span class="sxs-lookup"><span data-stu-id="f64fb-121">Disable flow logs</span></span>
* <span data-ttu-id="f64fb-122">запросить состояние журналов потоков.</span><span class="sxs-lookup"><span data-stu-id="f64fb-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="f64fb-123">Вход с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="f64fb-123">Log in with ARMClient</span></span>

<span data-ttu-id="f64fb-124">Войдите в tooarmclient с учетными данными Azure.</span><span class="sxs-lookup"><span data-stu-id="f64fb-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="f64fb-125">Регистрация поставщика Microsoft Insights</span><span class="sxs-lookup"><span data-stu-id="f64fb-125">Register Insights provider</span></span>

<span data-ttu-id="f64fb-126">В порядке для потока toowork ведения журнала успешно, hello **помощью Microsoft.Insights** должен быть зарегистрирован поставщик.</span><span class="sxs-lookup"><span data-stu-id="f64fb-126">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="f64fb-127">Если вы не уверены в том случае, если hello **помощью Microsoft.Insights** поставщик является зарегистрированным, запустите hello следующий скрипт.</span><span class="sxs-lookup"><span data-stu-id="f64fb-127">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="f64fb-128">Включение журналов потоков для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="f64fb-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="f64fb-129">Следующий пример hello показано Hello команда tooenable потока журналов:</span><span class="sxs-lookup"><span data-stu-id="f64fb-129">hello command tooenable flow logs is shown in hello following example:</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="f64fb-130">ответ Hello вернул hello выше пример следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f64fb-130">hello response returned from hello preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="f64fb-131">Отключение журналов потоков для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="f64fb-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="f64fb-132">Регистрирует hello используйте следующий пример toodisable потока.</span><span class="sxs-lookup"><span data-stu-id="f64fb-132">Use hello following example toodisable flow logs.</span></span> <span data-ttu-id="f64fb-133">Hello вызывается Здравствуйте таким же, как включение потока журналы, кроме **false** задано для свойства hello включена.</span><span class="sxs-lookup"><span data-stu-id="f64fb-133">hello call is hello same as enabling flow logs, except **false** is set for hello enabled property.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="f64fb-134">ответ Hello вернул hello выше пример следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f64fb-134">hello response returned from hello preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a><span data-ttu-id="f64fb-135">Запрос журналов потоков</span><span class="sxs-lookup"><span data-stu-id="f64fb-135">Query flow logs</span></span>

<span data-ttu-id="f64fb-136">После вызова REST, что запросы hello состояние потока Hello журналов на группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="f64fb-136">hello following REST call queries hello status of flow logs on a Network Security Group.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="f64fb-137">Hello ниже приведен пример hello ответ, возвращаемый:</span><span class="sxs-lookup"><span data-stu-id="f64fb-137">hello following is an example of hello response returned:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a><span data-ttu-id="f64fb-138">Скачивание журнала потоков</span><span class="sxs-lookup"><span data-stu-id="f64fb-138">Download a flow log</span></span>

<span data-ttu-id="f64fb-139">место хранения Hello потока журнала определяется при его создании.</span><span class="sxs-lookup"><span data-stu-id="f64fb-139">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="f64fb-140">Удобное средство tooaccess, эти учетной записи хранения потока сохраняться журналы tooa: Обозреватель хранилищ Microsoft Azure, которую можно загрузить здесь: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="f64fb-140">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="f64fb-141">При указании учетной записи хранилища пакетов отслеживания файлы сохраняются tooa учетной записи хранилища в hello следующие расположения:</span><span class="sxs-lookup"><span data-stu-id="f64fb-141">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="f64fb-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f64fb-142">Next steps</span></span>

<span data-ttu-id="f64fb-143">Узнайте, каким образом слишком[визуализировать журналов потока NSG с PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="f64fb-143">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="f64fb-144">Узнайте, каким образом слишком[визуализировать NSG потока журналов с помощью средств с открытым исходным кодом](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="f64fb-144">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
