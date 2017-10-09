---
title: "aaaMonitor операции, события и счетчики для Nsg | Документы Microsoft"
description: "Узнайте, как tooenable счетчики, события и оперативной ведение журнала для Nsg"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="51823-103">Аналитика журналов для групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="51823-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="51823-104">Можно включить следующие категории журнала диагностики для Nsg hello:</span><span class="sxs-lookup"><span data-stu-id="51823-104">You can enable hello following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="51823-105">**Событие:** содержит записи, для какой NSG правила, примененных tooVMs и экземпляр роли, на основе MAC-адреса.</span><span class="sxs-lookup"><span data-stu-id="51823-105">**Event:** Contains entries for which NSG rules are applied tooVMs and instance roles based on MAC address.</span></span> <span data-ttu-id="51823-106">Сбор сведений о состоянии Hello для этих правил каждые 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="51823-106">hello status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="51823-107">**Счетчик правил:** содержит записи для сколько раз каждый NSG правило будет применяться toodeny или разрешить трафик.</span><span class="sxs-lookup"><span data-stu-id="51823-107">**Rule counter:** Contains entries for how many times each NSG rule is applied toodeny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="51823-108">Журналы диагностики доступны только для Nsg, развернутые с помощью модели развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="51823-108">Diagnostic logs are only available for NSGs deployed through hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="51823-109">Невозможно включить сбор данных диагностики для Nsg, развернутые с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="51823-109">You cannot enable diagnostic logging for NSGs deployed through hello classic deployment model.</span></span> <span data-ttu-id="51823-110">Для лучшего понимания hello двух моделей, ссылаются на hello [Azure основные сведения о моделях развертывания](../resource-manager-deployment-model.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="51823-110">For a better understanding of hello two models, reference hello [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="51823-111">Ведение журнала действий (ранее он назывался журналом аудита или рабочим журналом) включена по умолчанию для всех NSG, независимо от модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="51823-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="51823-112">toodetermine операции, которые были выполнены на Nsg в журнале активности hello, найдите записи, содержащие hello следующие типы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="51823-112">toodetermine which operations were completed on NSGs in hello activity log, look for entries that contain hello following resource types:</span></span> 

- <span data-ttu-id="51823-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="51823-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="51823-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="51823-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="51823-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="51823-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="51823-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="51823-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="51823-117">Чтение hello [Обзор hello журнал действий Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) toolearn статьи, Дополнительные сведения о журналах активности.</span><span class="sxs-lookup"><span data-stu-id="51823-117">Read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article toolearn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="51823-118">Включение ведения журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="51823-118">Enable diagnostic logging</span></span>

<span data-ttu-id="51823-119">Необходимо включить ведение журнала диагностики для *каждого* NSG требуется toocollect данные.</span><span class="sxs-lookup"><span data-stu-id="51823-119">Diagnostic logging must be enabled for *each* NSG you want toocollect data for.</span></span> <span data-ttu-id="51823-120">Hello [Обзор служб Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) статье объясняется, где можно отправить журналы диагностики.</span><span class="sxs-lookup"><span data-stu-id="51823-120">hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="51823-121">При отсутствии существующей NSG hello завершения шагов в hello [создайте группу безопасности сети](virtual-networks-create-nsg-arm-pportal.md) toocreate статье один.</span><span class="sxs-lookup"><span data-stu-id="51823-121">If you don't have an existing NSG, complete hello steps in hello [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article toocreate one.</span></span> <span data-ttu-id="51823-122">Можно включить NSG ведения журналов с помощью любого из следующих методов hello диагностики:</span><span class="sxs-lookup"><span data-stu-id="51823-122">You can enable NSG diagnostic logging using any of hello following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="51823-123">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="51823-123">Azure portal</span></span>

<span data-ttu-id="51823-124">Ведение журнала портала tooenable hello toouse, toohello входа [портала](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="51823-124">toouse hello portal tooenable logging, login toohello [portal](https://portal.azure.com).</span></span> <span data-ttu-id="51823-125">Щелкните **дополнительные службы**, затем введите *группы безопасности сети*.</span><span class="sxs-lookup"><span data-stu-id="51823-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="51823-126">Выберите hello требуется ведение журнала для tooenable NSG.</span><span class="sxs-lookup"><span data-stu-id="51823-126">Select hello NSG you want tooenable logging for.</span></span> <span data-ttu-id="51823-127">Следуйте инструкциям hello не вычислительные ресурсы на hello [включить журналы диагностики в портале hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) статьи.</span><span class="sxs-lookup"><span data-stu-id="51823-127">Follow hello instructions for non-compute resources in hello [Enable diagnostic logs in hello portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="51823-128">Выберите категории журналов: **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter** или обе сразу.</span><span class="sxs-lookup"><span data-stu-id="51823-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="51823-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51823-129">PowerShell</span></span>

<span data-ttu-id="51823-130">tooenable PowerShell toouse ведения журнала, выполните инструкции hello hello [включить журналы диагностики с помощью PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) статьи.</span><span class="sxs-lookup"><span data-stu-id="51823-130">toouse PowerShell tooenable logging, follow hello instructions in hello [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="51823-131">Оцените следующие сведения перед вводом команды из статьи hello hello.</span><span class="sxs-lookup"><span data-stu-id="51823-131">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="51823-132">Можно определить toouse значение hello для hello `-ResourceId` параметра, заменив hello после [текст] соответствующим образом, введя команду hello `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="51823-132">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="51823-133">выходные данные идентификатор Hello hello команды выглядят примерно слишком*/subscriptions/ [имя подписки Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="51823-133">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="51823-134">Toocollect данных из категории журнала требуется только добавить `-Categories [category]` toohello конец команды hello в статье hello, где категории равна *NetworkSecurityGroupEvent* или *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="51823-134">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="51823-135">Если вы не используете hello `-Categories` параметра, сбор данных включен для обоих журналов категорий.</span><span class="sxs-lookup"><span data-stu-id="51823-135">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="51823-136">интерфейс командной строки Azure (CLI)</span><span class="sxs-lookup"><span data-stu-id="51823-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="51823-137">toouse Здравствуйте ведения журнала tooenable CLI, следуйте инструкциям hello hello [включить журналы диагностики через CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) статьи.</span><span class="sxs-lookup"><span data-stu-id="51823-137">toouse hello CLI tooenable logging, follow hello instructions in hello [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="51823-138">Оцените следующие сведения перед вводом команды из статьи hello hello.</span><span class="sxs-lookup"><span data-stu-id="51823-138">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="51823-139">Можно определить toouse значение hello для hello `-ResourceId` параметра, заменив hello после [текст] соответствующим образом, введя команду hello `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="51823-139">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="51823-140">выходные данные идентификатор Hello hello команды выглядят примерно слишком*/subscriptions/ [имя подписки Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="51823-140">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="51823-141">Toocollect данных из категории журнала требуется только добавить `-Categories [category]` toohello конец команды hello в статье hello, где категории равна *NetworkSecurityGroupEvent* или *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="51823-141">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="51823-142">Если вы не используете hello `-Categories` параметра, сбор данных включен для обоих журналов категорий.</span><span class="sxs-lookup"><span data-stu-id="51823-142">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="51823-143">Собранные данные журнала</span><span class="sxs-lookup"><span data-stu-id="51823-143">Logged data</span></span>

<span data-ttu-id="51823-144">Данные в оба журнала записываются в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="51823-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="51823-145">в следующих разделах hello указывается Hello определенные данные, записанные для каждого типа журнала.</span><span class="sxs-lookup"><span data-stu-id="51823-145">hello specific data written for each log type is listed in hello following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="51823-146">Журнал событий</span><span class="sxs-lookup"><span data-stu-id="51823-146">Event log</span></span>
<span data-ttu-id="51823-147">Этот журнал содержит сведения о NSG, какие правила применяются tooVMs и облачной службы экземпляры роли, на основе MAC-адреса.</span><span class="sxs-lookup"><span data-stu-id="51823-147">This log contains information about which NSG rules are applied tooVMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="51823-148">Следующий пример данных Hello регистрируется для каждого события.</span><span class="sxs-lookup"><span data-stu-id="51823-148">hello following example data is logged for each event:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a><span data-ttu-id="51823-149">Журнал счетчиков правил</span><span class="sxs-lookup"><span data-stu-id="51823-149">Rule counter log</span></span>

<span data-ttu-id="51823-150">Этот журнал содержит сведения о каждом tooresources правило применяется.</span><span class="sxs-lookup"><span data-stu-id="51823-150">This log contains information about each rule applied tooresources.</span></span> <span data-ttu-id="51823-151">Hello следующий пример данных регистрируется каждый раз, когда применяется правило.</span><span class="sxs-lookup"><span data-stu-id="51823-151">hello following example data is logged each time a rule is applied:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a><span data-ttu-id="51823-152">Просмотр и анализ журналов</span><span class="sxs-lookup"><span data-stu-id="51823-152">View and analyze logs</span></span>

<span data-ttu-id="51823-153">toolearn tooview действия записываются в журнал, чтение hello [Обзор hello журнал действий Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="51823-153">toolearn how tooview activity log data, read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="51823-154">toolearn tooview диагностики ведения журнала данных, чтение hello [Обзор служб Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="51823-154">toolearn how tooview diagnostic log data, read hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="51823-155">При отправке данных диагностики tooLog Analytics, можно использовать hello [сетевой группы безопасности Azure analytics](../log-analytics/log-analytics-azure-networking-analytics.md) решение для управления (Предварительная версия) для расширенного анализа.</span><span class="sxs-lookup"><span data-stu-id="51823-155">If you send diagnostics data tooLog Analytics, you can use hello [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
