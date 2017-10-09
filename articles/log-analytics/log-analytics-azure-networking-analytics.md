---
title: "решения для анализа сети в службе анализа журналов aaaAzure | Документы Microsoft"
description: "Можно использовать hello решения для анализа сети Azure в журналах шлюза приложения Azure и журналы группы безопасности сети Azure tooreview анализа журналов."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="a13f7-103">Решения для мониторинга сетей Azure в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a13f7-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="a13f7-104">Аналитика журналов предлагает следующие решения для мониторинга сети hello.</span><span class="sxs-lookup"><span data-stu-id="a13f7-104">Log Analytics offers hello following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="a13f7-105">Монитор производительности сети (NPM):</span><span class="sxs-lookup"><span data-stu-id="a13f7-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="a13f7-106">Монитор работоспособности hello сети</span><span class="sxs-lookup"><span data-stu-id="a13f7-106">Monitor hello health of your network</span></span>
* <span data-ttu-id="a13f7-107">Tooreview аналитика Azure шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a13f7-107">Azure Application Gateway analytics tooreview</span></span>
 * <span data-ttu-id="a13f7-108">журналы шлюза приложений Azure;</span><span class="sxs-lookup"><span data-stu-id="a13f7-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="a13f7-109">метрику шлюза приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="a13f7-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="a13f7-110">Tooreview аналитика сетевой группы безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="a13f7-110">Azure Network Security Group analytics tooreview</span></span>
 * <span data-ttu-id="a13f7-111">журналы групп безопасности сети Azure.</span><span class="sxs-lookup"><span data-stu-id="a13f7-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="a13f7-112">Монитор производительности сети</span><span class="sxs-lookup"><span data-stu-id="a13f7-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="a13f7-113">Hello [сетевой монитор производительности](log-analytics-network-performance-monitor.md) решение по управлению, решения, отслеживающий hello работоспособности, доступности и возможность сетей мониторинга сети.</span><span class="sxs-lookup"><span data-stu-id="a13f7-113">hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors hello health, availability and reachability of networks.</span></span>  <span data-ttu-id="a13f7-114">Это подключение используется toomonitor между:</span><span class="sxs-lookup"><span data-stu-id="a13f7-114">It is used toomonitor connectivity between:</span></span>

* <span data-ttu-id="a13f7-115">общедоступное облако и локальная среда;</span><span class="sxs-lookup"><span data-stu-id="a13f7-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="a13f7-116">центры обработки данных и расположения пользователей (филиалы);</span><span class="sxs-lookup"><span data-stu-id="a13f7-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="a13f7-117">подсети, в которых размещены различные уровни многоуровневого приложения.</span><span class="sxs-lookup"><span data-stu-id="a13f7-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="a13f7-118">Дополнительную информацию см. в статье [Решение монитора производительности сети в Azure Log Analytics](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="a13f7-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="a13f7-119">Шлюз приложений Azure и анализ групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="a13f7-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="a13f7-120">решения toouse hello.</span><span class="sxs-lookup"><span data-stu-id="a13f7-120">toouse hello solutions:</span></span>
1. <span data-ttu-id="a13f7-121">Добавить tooLog решение управления hello аналитика, и</span><span class="sxs-lookup"><span data-stu-id="a13f7-121">Add hello management solution tooLog Analytics, and</span></span>
2. <span data-ttu-id="a13f7-122">Включение анализа журналов диагностики toodirect hello диагностики tooa рабочей.</span><span class="sxs-lookup"><span data-stu-id="a13f7-122">Enable diagnostics toodirect hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="a13f7-123">Это не hello журналы необходимые toowrite tooAzure-хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="a13f7-123">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

<span data-ttu-id="a13f7-124">Можно включить диагностику и hello соответствующее решение для одного или обоих шлюза приложения и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="a13f7-124">You can enable diagnostics and hello corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="a13f7-125">Если не включить сбор данных диагностики для определенного типа ресурсов, но установка решения hello, колонках hello панели мониторинга для этого ресурса пусты и сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="a13f7-125">If you do not enable diagnostic logging for a particular resource type, but install hello solution, hello dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="a13f7-126">В января 2017 г hello поддерживается способ отправки журналов из шлюзы приложений и группы безопасности сети tooLog Analytics изменено.</span><span class="sxs-lookup"><span data-stu-id="a13f7-126">In January 2017, hello supported way of sending logs from Application Gateways and Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="a13f7-127">Если вы видите hello **анализа сети Azure (устарело)** решения, ссылаться слишком[миграция из старого решения сети Analytics hello](#migrating-from-the-old-networking-analytics-solution) для действия необходимы toofollow.</span><span class="sxs-lookup"><span data-stu-id="a13f7-127">If you see hello **Azure Networking Analytics (deprecated)** solution, refer too[migrating from hello old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need toofollow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="a13f7-128">Просмотр сведений о сборе данных о сетях Azure</span><span class="sxs-lookup"><span data-stu-id="a13f7-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="a13f7-129">Шлюз приложений Azure analytics Hello и решений по управлению analytics сетевой группы безопасности hello собирать журналы диагностики непосредственно из шлюзы приложений Azure и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="a13f7-129">hello Azure Application Gateway analytics and hello Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="a13f7-130">Не является tooAzure журналы hello необходимые toowrite хранилища больших двоичных объектов и агент не требуется для сбора данных.</span><span class="sxs-lookup"><span data-stu-id="a13f7-130">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="a13f7-131">Hello ниже приведены методы сбора данных и другие сведения о сборе данных для анализа шлюза приложения Azure и аналитика hello группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="a13f7-131">hello following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and hello Network Security Group analytics.</span></span>

| <span data-ttu-id="a13f7-132">Платформа</span><span class="sxs-lookup"><span data-stu-id="a13f7-132">Platform</span></span> | <span data-ttu-id="a13f7-133">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="a13f7-133">Direct agent</span></span> | <span data-ttu-id="a13f7-134">Агент Systems Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="a13f7-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="a13f7-135">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="a13f7-135">Azure</span></span> | <span data-ttu-id="a13f7-136">Нужен ли Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="a13f7-136">Operations Manager required?</span></span> | <span data-ttu-id="a13f7-137">Отправка данных агента Operations Manager через группу управления</span><span class="sxs-lookup"><span data-stu-id="a13f7-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="a13f7-138">Частота сбора</span><span class="sxs-lookup"><span data-stu-id="a13f7-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="a13f7-139">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="a13f7-139">Azure</span></span> |  |  |<span data-ttu-id="a13f7-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a13f7-140">&#8226;</span></span> |  |  |<span data-ttu-id="a13f7-141">при входе</span><span class="sxs-lookup"><span data-stu-id="a13f7-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="a13f7-142">Решение для анализа шлюзов приложений Azure в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a13f7-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Символ "Аналитика службы приложений Azure"](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="a13f7-144">Шлюзы приложений поддерживаются следующие журналы Hello.</span><span class="sxs-lookup"><span data-stu-id="a13f7-144">hello following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="a13f7-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="a13f7-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="a13f7-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="a13f7-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="a13f7-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="a13f7-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="a13f7-148">Шлюзы приложений поддерживаются следующие метрики Hello.</span><span class="sxs-lookup"><span data-stu-id="a13f7-148">hello following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="a13f7-149">пропускная способность за 5 минут.</span><span class="sxs-lookup"><span data-stu-id="a13f7-149">5 minute throughput</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="a13f7-150">Установка и настройка решения hello</span><span class="sxs-lookup"><span data-stu-id="a13f7-150">Install and configure hello solution</span></span>
<span data-ttu-id="a13f7-151">Используйте следующие инструкции tooinstall hello и настройка решения для анализа hello шлюза приложения Azure:</span><span class="sxs-lookup"><span data-stu-id="a13f7-151">Use hello following instructions tooinstall and configure hello Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="a13f7-152">Включить решения для анализа hello шлюза приложения Azure из [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="a13f7-152">Enable hello Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="a13f7-153">Включить ведение журнала диагностики для hello [шлюзы приложений](../application-gateway/application-gateway-diagnostics.md) требуется toomonitor.</span><span class="sxs-lookup"><span data-stu-id="a13f7-153">Enable diagnostics logging for hello [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want toomonitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a><span data-ttu-id="a13f7-154">Включить диагностику шлюза приложения Azure в портале hello</span><span class="sxs-lookup"><span data-stu-id="a13f7-154">Enable Azure Application Gateway diagnostics in hello portal</span></span>

1. <span data-ttu-id="a13f7-155">Hello портал Azure перейдите toomonitor ресурсов toohello шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a13f7-155">In hello Azure portal, navigate toohello Application Gateway resource toomonitor</span></span>
2. <span data-ttu-id="a13f7-156">Выберите *журналы диагностики* после страницы приветствия tooopen</span><span class="sxs-lookup"><span data-stu-id="a13f7-156">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![снимок экрана: ресурс шлюза приложений Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="a13f7-158">Нажмите кнопку *включить диагностику* после страницы приветствия tooopen</span><span class="sxs-lookup"><span data-stu-id="a13f7-158">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![снимок экрана: ресурс шлюза приложений Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="a13f7-160">Щелкните tooturn диагностику, *на* под *состояния*</span><span class="sxs-lookup"><span data-stu-id="a13f7-160">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="a13f7-161">Щелкните флажок hello *отправки tooLog аналитика*</span><span class="sxs-lookup"><span data-stu-id="a13f7-161">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="a13f7-162">Выберите существующую рабочую область Log Analytics или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="a13f7-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="a13f7-163">Установите флажок hello под **журнала** для каждого из типов toocollect hello журнала</span><span class="sxs-lookup"><span data-stu-id="a13f7-163">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="a13f7-164">Нажмите кнопку *Сохранить* tooenable hello ведение журнала диагностики tooLog аналитика</span><span class="sxs-lookup"><span data-stu-id="a13f7-164">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="a13f7-165">Включение диагностики сети Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a13f7-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="a13f7-166">Hello следующий скрипт PowerShell приведен пример того, как tooenable ведения журналов диагностики для шлюзы приложений.</span><span class="sxs-lookup"><span data-stu-id="a13f7-166">hello following PowerShell script provides an example of how tooenable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="a13f7-167">Использование анализа шлюзов приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a13f7-167">Use Azure Application Gateway analytics</span></span>
![снимок экрана: элемент "Анализ шлюзов приложений Azure"](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="a13f7-169">После нажатия кнопки hello **шлюза приложения Azure analytics** плитки на hello Обзор, можно просмотреть сводные данные журналов и затем можно перейти в toodetails для hello, следующие категории:</span><span class="sxs-lookup"><span data-stu-id="a13f7-169">After you click hello **Azure Application Gateway analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="a13f7-170">Журналы доступа к шлюзу приложений:</span><span class="sxs-lookup"><span data-stu-id="a13f7-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="a13f7-171">ошибки клиента и сервера для журналов доступа шлюза приложений;</span><span class="sxs-lookup"><span data-stu-id="a13f7-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="a13f7-172">количество запросов в час для каждого шлюза приложений;</span><span class="sxs-lookup"><span data-stu-id="a13f7-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="a13f7-173">количество неудачных запросов в час для каждого шлюза приложений;</span><span class="sxs-lookup"><span data-stu-id="a13f7-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="a13f7-174">ошибки агентов пользователя для шлюзов приложений.</span><span class="sxs-lookup"><span data-stu-id="a13f7-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="a13f7-175">Производительность шлюза приложений:</span><span class="sxs-lookup"><span data-stu-id="a13f7-175">Application Gateway performance</span></span>
  * <span data-ttu-id="a13f7-176">работоспособность узла для шлюза приложений;</span><span class="sxs-lookup"><span data-stu-id="a13f7-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="a13f7-177">максимальное количество и 95-й процентиль для неудачных запросов шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a13f7-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![снимок экрана: панель мониторинга "Анализ шлюзов приложений Azure"](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![снимок экрана: панель мониторинга "Анализ шлюзов приложений Azure"](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="a13f7-180">На hello **шлюза приложения Azure analytics** панели мониторинга, просмотрите сводные сведения о hello в одной из колонок hello и выберите один tooview подробные сведения на странице поиска журналов hello.</span><span class="sxs-lookup"><span data-stu-id="a13f7-180">On hello **Azure Application Gateway analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="a13f7-181">На любой из страниц поиска журналов hello можно просмотреть результаты по времени, подробные результаты и историю поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="a13f7-181">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="a13f7-182">Можно также фильтровать по результатам hello toonarrow аспектов.</span><span class="sxs-lookup"><span data-stu-id="a13f7-182">You can also filter by facets toonarrow hello results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="a13f7-183">Решение для анализа групп безопасности сети Azure в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a13f7-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Символ "Аналитика групп безопасности сетей Azure"](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="a13f7-185">для групп безопасности сети поддерживаются Hello следующие журналы:</span><span class="sxs-lookup"><span data-stu-id="a13f7-185">hello following logs are supported for network security groups:</span></span>

* <span data-ttu-id="a13f7-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="a13f7-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="a13f7-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="a13f7-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="a13f7-188">Установка и настройка решения hello</span><span class="sxs-lookup"><span data-stu-id="a13f7-188">Install and configure hello solution</span></span>
<span data-ttu-id="a13f7-189">Используйте следующие инструкции tooinstall hello и настроить решение hello Azure Analytics сети:</span><span class="sxs-lookup"><span data-stu-id="a13f7-189">Use hello following instructions tooinstall and configure hello Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="a13f7-190">Включить решения для анализа hello Azure сетевую группу безопасности из [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="a13f7-190">Enable hello Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="a13f7-191">Включить ведение журнала диагностики для hello [сетевой группы безопасности](../virtual-network/virtual-network-nsg-manage-log.md) toomonitor ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a13f7-191">Enable diagnostics logging for hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want toomonitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a><span data-ttu-id="a13f7-192">Включение диагностики группы безопасности сети Azure на портале hello</span><span class="sxs-lookup"><span data-stu-id="a13f7-192">Enable Azure network security group diagnostics in hello portal</span></span>

1. <span data-ttu-id="a13f7-193">Hello портал Azure перейдите toomonitor ресурсов toohello группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="a13f7-193">In hello Azure portal, navigate toohello Network Security Group resource toomonitor</span></span>
2. <span data-ttu-id="a13f7-194">Выберите *журналы диагностики* после страницы приветствия tooopen</span><span class="sxs-lookup"><span data-stu-id="a13f7-194">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![снимок экрана: ресурс группы безопасности сети Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="a13f7-196">Нажмите кнопку *включить диагностику* после страницы приветствия tooopen</span><span class="sxs-lookup"><span data-stu-id="a13f7-196">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![снимок экрана: ресурс группы безопасности сети Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="a13f7-198">Щелкните tooturn диагностику, *на* под *состояния*</span><span class="sxs-lookup"><span data-stu-id="a13f7-198">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="a13f7-199">Щелкните флажок hello *отправки tooLog аналитика*</span><span class="sxs-lookup"><span data-stu-id="a13f7-199">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="a13f7-200">Выберите существующую рабочую область Log Analytics или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="a13f7-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="a13f7-201">Установите флажок hello под **журнала** для каждого из типов toocollect hello журнала</span><span class="sxs-lookup"><span data-stu-id="a13f7-201">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="a13f7-202">Нажмите кнопку *Сохранить* tooenable hello ведение журнала диагностики tooLog аналитика</span><span class="sxs-lookup"><span data-stu-id="a13f7-202">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="a13f7-203">Включение диагностики сети Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a13f7-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="a13f7-204">Hello следующий скрипт PowerShell приведен пример того, как tooenable ведения журналов диагностики для групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="a13f7-204">hello following PowerShell script provides an example of how tooenable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="a13f7-205">Использование анализа групп безопасности сети Azure</span><span class="sxs-lookup"><span data-stu-id="a13f7-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="a13f7-206">После нажатия кнопки hello **сетевой группы безопасности Azure analytics** плитки на hello Обзор, можно просмотреть сводные данные журналов и затем можно перейти в toodetails для hello, следующие категории:</span><span class="sxs-lookup"><span data-stu-id="a13f7-206">After you click hello **Azure Network Security Group analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="a13f7-207">Заблокированные потоки группы безопасности сети:</span><span class="sxs-lookup"><span data-stu-id="a13f7-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="a13f7-208">правила группы безопасности сети с заблокированными потоками;</span><span class="sxs-lookup"><span data-stu-id="a13f7-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="a13f7-209">MAC-адреса c заблокированными потоками.</span><span class="sxs-lookup"><span data-stu-id="a13f7-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="a13f7-210">Разрешенные потоки группы безопасности сети:</span><span class="sxs-lookup"><span data-stu-id="a13f7-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="a13f7-211">правила группы безопасности сети с разрешенными потоками;</span><span class="sxs-lookup"><span data-stu-id="a13f7-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="a13f7-212">MAC-адреса c разрешенными потоками.</span><span class="sxs-lookup"><span data-stu-id="a13f7-212">MAC addresses with allowed flows</span></span>

![снимок экрана: панель мониторинга "Анализ групп безопасности сети Azure"](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![снимок экрана: панель мониторинга "Анализ групп безопасности сети Azure"](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="a13f7-215">На hello **сетевой группы безопасности Azure analytics** панели мониторинга, просмотрите сводные сведения о hello в одной из колонок hello и выберите один tooview подробные сведения на странице поиска журналов hello.</span><span class="sxs-lookup"><span data-stu-id="a13f7-215">On hello **Azure Network Security Group analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="a13f7-216">На любой из страниц поиска журналов hello можно просмотреть результаты по времени, подробные результаты и историю поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="a13f7-216">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="a13f7-217">Можно также фильтровать по результатам hello toonarrow аспектов.</span><span class="sxs-lookup"><span data-stu-id="a13f7-217">You can also filter by facets toonarrow hello results.</span></span>

## <a name="migrating-from-hello-old-networking-analytics-solution"></a><span data-ttu-id="a13f7-218">Миграция из старого решения сети Analytics hello</span><span class="sxs-lookup"><span data-stu-id="a13f7-218">Migrating from hello old Networking Analytics solution</span></span>
<span data-ttu-id="a13f7-219">В января 2017 г hello поддерживается способ отправки журналов из tooLog шлюзы приложений Azure и группы безопасности сети Azure Analytics изменено.</span><span class="sxs-lookup"><span data-stu-id="a13f7-219">In January 2017, hello supported way of sending logs from Azure Application Gateways and Azure Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="a13f7-220">Эти изменения обеспечивают hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a13f7-220">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="a13f7-221">Журналы записываются напрямую tooLog Analytics без hello требуется toouse учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="a13f7-221">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="a13f7-222">Меньше задержка из hello время, когда журналы, созданные toothem, недоступными в службе анализа журналов</span><span class="sxs-lookup"><span data-stu-id="a13f7-222">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="a13f7-223">Меньше этапов настройки.</span><span class="sxs-lookup"><span data-stu-id="a13f7-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="a13f7-224">Общий формат для всех типов системы диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="a13f7-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="a13f7-225">toouse hello обновление решения:</span><span class="sxs-lookup"><span data-stu-id="a13f7-225">toouse hello updated solutions:</span></span>

1. [<span data-ttu-id="a13f7-226">Настройка диагностики toobe tooLog Analytics отправляется непосредственно из шлюзы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a13f7-226">Configure diagnostics toobe sent directly tooLog Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="a13f7-227">Настройка диагностики toobe tooLog Analytics отправляется непосредственно из групп безопасности сети Azure</span><span class="sxs-lookup"><span data-stu-id="a13f7-227">Configure diagnostics toobe sent directly tooLog Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="a13f7-228">Включить hello *шлюза приложения Azure Analytics* и hello *аналитика группы безопасности сети Azure* описано решение с помощью процесса hello в [решений добавьте анализа журналов из Hello коллекции решений](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="a13f7-228">Enable hello *Azure Application Gateway Analytics* and hello *Azure Network Security Group Analytics* solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="a13f7-229">Обновить все сохраненные запросы, панели мониторинга и новый тип данных оповещения toouse hello</span><span class="sxs-lookup"><span data-stu-id="a13f7-229">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="a13f7-230">Тип — tooAzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="a13f7-230">Type is tooAzureDiagnostics.</span></span> <span data-ttu-id="a13f7-231">Вы можете использовать сетевые журналы toofilter ResourceType tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="a13f7-231">You can use hello ResourceType toofilter tooAzure networking logs.</span></span>

    | <span data-ttu-id="a13f7-232">Используйте такую замену:</span><span class="sxs-lookup"><span data-stu-id="a13f7-232">Instead of:</span></span> | <span data-ttu-id="a13f7-233">Используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a13f7-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="a13f7-234">Для любого поля, имеет суффикс \_s, \_d, или \_g в поле имя hello hello первый символ toolower регистр</span><span class="sxs-lookup"><span data-stu-id="a13f7-234">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
   + <span data-ttu-id="a13f7-235">Для любого поля, имеет суффикс \_«o» в имени hello данных разбивается на отдельные поля на основе имен hello вложенные поля.</span><span class="sxs-lookup"><span data-stu-id="a13f7-235">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span>
4. <span data-ttu-id="a13f7-236">Удалите hello *анализа сети Azure (не рекомендуется)* решения.</span><span class="sxs-lookup"><span data-stu-id="a13f7-236">Remove hello *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="a13f7-237">Если используется PowerShell, то выполните следующую команду: `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="a13f7-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="a13f7-238">Данные, собранные до вызова hello изменений не отображается в новом решении hello.</span><span class="sxs-lookup"><span data-stu-id="a13f7-238">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="a13f7-239">Вы можете продолжить tooquery для этого данные с помощью hello и старый тип и имена полей.</span><span class="sxs-lookup"><span data-stu-id="a13f7-239">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a13f7-240">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="a13f7-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="a13f7-241">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a13f7-241">Next steps</span></span>
* <span data-ttu-id="a13f7-242">Используйте [входа поиска аналитики журналов](log-analytics-log-searches.md) tooview подробных данных диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="a13f7-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure diagnostics data.</span></span>
