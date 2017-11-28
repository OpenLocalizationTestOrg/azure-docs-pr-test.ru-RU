---
title: "Решение для анализа сетей Azure в Log Analytics | Документация Майкрософт"
description: "Решение для анализа сетей Azure можно использовать в Log Analytics для просмотра журналов групп безопасности сети Azure и шлюза приложений Azure."
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
ms.openlocfilehash: 06b67322b3812a668a515ecc357171ede1d85441
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="466d9-103">Решения для мониторинга сетей Azure в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="466d9-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="466d9-104">Log Analytics предлагает следующие решения для мониторинга сетей.</span><span class="sxs-lookup"><span data-stu-id="466d9-104">Log Analytics offers the following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="466d9-105">Монитор производительности сети (NPM):</span><span class="sxs-lookup"><span data-stu-id="466d9-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="466d9-106">отслеживание работоспособности сети.</span><span class="sxs-lookup"><span data-stu-id="466d9-106">Monitor the health of your network</span></span>
* <span data-ttu-id="466d9-107">Анализ шлюзов приложений Azure для проверки:</span><span class="sxs-lookup"><span data-stu-id="466d9-107">Azure Application Gateway analytics to review</span></span>
 * <span data-ttu-id="466d9-108">журналы шлюза приложений Azure;</span><span class="sxs-lookup"><span data-stu-id="466d9-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="466d9-109">метрику шлюза приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="466d9-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="466d9-110">Анализ групп безопасности сети Azure для проверки:</span><span class="sxs-lookup"><span data-stu-id="466d9-110">Azure Network Security Group analytics to review</span></span>
 * <span data-ttu-id="466d9-111">журналы групп безопасности сети Azure.</span><span class="sxs-lookup"><span data-stu-id="466d9-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="466d9-112">Монитор производительности сети</span><span class="sxs-lookup"><span data-stu-id="466d9-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="466d9-113">Решение по управлению [Монитор производительности сети](log-analytics-network-performance-monitor.md) — это решение для мониторинга сети, которое отслеживает работоспособность и доступность сетей.</span><span class="sxs-lookup"><span data-stu-id="466d9-113">The [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors the health, availability and reachability of networks.</span></span>  <span data-ttu-id="466d9-114">Оно используется для отслеживания подключения между следующими ресурсами:</span><span class="sxs-lookup"><span data-stu-id="466d9-114">It is used to monitor connectivity between:</span></span>

* <span data-ttu-id="466d9-115">общедоступное облако и локальная среда;</span><span class="sxs-lookup"><span data-stu-id="466d9-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="466d9-116">центры обработки данных и расположения пользователей (филиалы);</span><span class="sxs-lookup"><span data-stu-id="466d9-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="466d9-117">подсети, в которых размещены различные уровни многоуровневого приложения.</span><span class="sxs-lookup"><span data-stu-id="466d9-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="466d9-118">Дополнительную информацию см. в статье [Решение монитора производительности сети в Azure Log Analytics](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="466d9-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="466d9-119">Шлюз приложений Azure и анализ групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="466d9-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="466d9-120">Чтобы использовать эти решения, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="466d9-120">To use the solutions:</span></span>
1. <span data-ttu-id="466d9-121">Добавьте решение по управлению в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="466d9-121">Add the management solution to Log Analytics, and</span></span>
2. <span data-ttu-id="466d9-122">Включите диагностику для аналитики журналов в рабочей области Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="466d9-122">Enable diagnostics to direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="466d9-123">Необязательно записывать журналы в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="466d9-123">It is not necessary to write the logs to Azure Blob storage.</span></span>

<span data-ttu-id="466d9-124">Диагностику и соответствующее решение можно включить как для одного, так и для обоих компонентов (шлюз приложений и группы безопасности сети).</span><span class="sxs-lookup"><span data-stu-id="466d9-124">You can enable diagnostics and the corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="466d9-125">Если не включить ведение журналов диагностики для определенного типа ресурсов, но установить решение, то колонки панели мониторинга для этого ресурса будут пустыми, а также появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="466d9-125">If you do not enable diagnostic logging for a particular resource type, but install the solution, the dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="466d9-126">В январе 2017 г. поддерживаемый способ отправки журналов из шлюзов приложений и групп безопасности сети в Log Analytics был изменен.</span><span class="sxs-lookup"><span data-stu-id="466d9-126">In January 2017, the supported way of sending logs from Application Gateways and Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="466d9-127">Если отобразится устаревшее решение **Анализ сетевой активности Azure (не рекомендуется)**, то выполните действия, описанные в разделе [Миграция из устаревшего решения для анализа сетевой активности](#migrating-from-the-old-networking-analytics-solution).</span><span class="sxs-lookup"><span data-stu-id="466d9-127">If you see the **Azure Networking Analytics (deprecated)** solution, refer to [migrating from the old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need to follow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="466d9-128">Просмотр сведений о сборе данных о сетях Azure</span><span class="sxs-lookup"><span data-stu-id="466d9-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="466d9-129">Решения для управления анализом шлюзов приложений и групп безопасности сети Azure собирают журналы диагностики непосредственно из шлюзов приложений и групп безопасности сети Azure.</span><span class="sxs-lookup"><span data-stu-id="466d9-129">The Azure Application Gateway analytics and the Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="466d9-130">Необязательно записывать журналы в хранилище BLOB-объектов Azure. Для сбора данных агенты не требуются.</span><span class="sxs-lookup"><span data-stu-id="466d9-130">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="466d9-131">В следующей таблице приведены методы сбора данных и другие сведения о сборе данных для анализа шлюзов приложений и групп безопасности сети Azure.</span><span class="sxs-lookup"><span data-stu-id="466d9-131">The following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and the Network Security Group analytics.</span></span>

| <span data-ttu-id="466d9-132">платформа</span><span class="sxs-lookup"><span data-stu-id="466d9-132">Platform</span></span> | <span data-ttu-id="466d9-133">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="466d9-133">Direct agent</span></span> | <span data-ttu-id="466d9-134">Агент Systems Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="466d9-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="466d9-135">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="466d9-135">Azure</span></span> | <span data-ttu-id="466d9-136">Нужен ли Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="466d9-136">Operations Manager required?</span></span> | <span data-ttu-id="466d9-137">Отправка данных агента Operations Manager через группу управления</span><span class="sxs-lookup"><span data-stu-id="466d9-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="466d9-138">Частота сбора</span><span class="sxs-lookup"><span data-stu-id="466d9-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="466d9-139">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="466d9-139">Azure</span></span> |  |  |<span data-ttu-id="466d9-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="466d9-140">&#8226;</span></span> |  |  |<span data-ttu-id="466d9-141">при входе</span><span class="sxs-lookup"><span data-stu-id="466d9-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="466d9-142">Решение для анализа шлюзов приложений Azure в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="466d9-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Символ "Аналитика службы приложений Azure"](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="466d9-144">Шлюзы приложений поддерживают следующие журналы:</span><span class="sxs-lookup"><span data-stu-id="466d9-144">The following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="466d9-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="466d9-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="466d9-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="466d9-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="466d9-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="466d9-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="466d9-148">Шлюзы приложений поддерживают следующие метрики:</span><span class="sxs-lookup"><span data-stu-id="466d9-148">The following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="466d9-149">пропускная способность за 5 минут.</span><span class="sxs-lookup"><span data-stu-id="466d9-149">5 minute throughput</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="466d9-150">Установка и настройка решения</span><span class="sxs-lookup"><span data-stu-id="466d9-150">Install and configure the solution</span></span>
<span data-ttu-id="466d9-151">Установите и настройте решение для анализа шлюзов приложений Azure, выполнив следующие указания:</span><span class="sxs-lookup"><span data-stu-id="466d9-151">Use the following instructions to install and configure the Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="466d9-152">Включите решение для анализа шлюзов приложений Azure из [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) или выполните инструкции из статьи [Добавление решений для управления Azure Log Analytics в рабочую область](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="466d9-152">Enable the Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="466d9-153">Включите ведение журнала диагностики для [шлюзов приложений](../application-gateway/application-gateway-diagnostics.md), для которых требуется выполнять мониторинг.</span><span class="sxs-lookup"><span data-stu-id="466d9-153">Enable diagnostics logging for the [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want to monitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-the-portal"></a><span data-ttu-id="466d9-154">Включение диагностики шлюза приложений Azure на портале</span><span class="sxs-lookup"><span data-stu-id="466d9-154">Enable Azure Application Gateway diagnostics in the portal</span></span>

1. <span data-ttu-id="466d9-155">На портале Azure перейдите к ресурсу шлюза приложений, который необходимо отслеживать.</span><span class="sxs-lookup"><span data-stu-id="466d9-155">In the Azure portal, navigate to the Application Gateway resource to monitor</span></span>
2. <span data-ttu-id="466d9-156">Выберите *Журналы диагностики*, чтобы открыть следующую страницу:</span><span class="sxs-lookup"><span data-stu-id="466d9-156">Select *Diagnostics logs* to open the following page</span></span>

   ![снимок экрана: ресурс шлюза приложений Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="466d9-158">Щелкните *Включить диагностику*, чтобы открыть следующую страницу:</span><span class="sxs-lookup"><span data-stu-id="466d9-158">Click *Turn on diagnostics* to open the following page</span></span>

   ![снимок экрана: ресурс шлюза приложений Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="466d9-160">Чтобы включить диагностику, нажмите кнопку *Вкл.* в разделе *Состояние*.</span><span class="sxs-lookup"><span data-stu-id="466d9-160">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="466d9-161">Установите флажок *Send to Log Analytics* (Отправить в Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="466d9-161">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="466d9-162">Выберите существующую рабочую область Log Analytics или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="466d9-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="466d9-163">В разделе **Журнал** установите флажки для всех типов журналов, которые необходимо собирать.</span><span class="sxs-lookup"><span data-stu-id="466d9-163">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="466d9-164">Щелкните *Сохранить*, чтобы включить ведение журнала диагностики в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="466d9-164">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="466d9-165">Включение диагностики сети Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="466d9-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="466d9-166">Следующий сценарий PowerShell приведен в качестве примера того, как включить ведение журналов диагностики для шлюзов приложений:</span><span class="sxs-lookup"><span data-stu-id="466d9-166">The following PowerShell script provides an example of how to enable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="466d9-167">Использование анализа шлюзов приложений Azure</span><span class="sxs-lookup"><span data-stu-id="466d9-167">Use Azure Application Gateway analytics</span></span>
![снимок экрана: элемент "Анализ шлюзов приложений Azure"](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="466d9-169">Выбрав элемент **Azure Application Gateway analytics** (Анализ шлюзов приложений Azure) в разделе "Обзор", можно просмотреть сводные данные журналов и подробные сведения по следующим категориям:</span><span class="sxs-lookup"><span data-stu-id="466d9-169">After you click the **Azure Application Gateway analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="466d9-170">Журналы доступа к шлюзу приложений:</span><span class="sxs-lookup"><span data-stu-id="466d9-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="466d9-171">ошибки клиента и сервера для журналов доступа шлюза приложений;</span><span class="sxs-lookup"><span data-stu-id="466d9-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="466d9-172">количество запросов в час для каждого шлюза приложений;</span><span class="sxs-lookup"><span data-stu-id="466d9-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="466d9-173">количество неудачных запросов в час для каждого шлюза приложений;</span><span class="sxs-lookup"><span data-stu-id="466d9-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="466d9-174">ошибки агентов пользователя для шлюзов приложений.</span><span class="sxs-lookup"><span data-stu-id="466d9-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="466d9-175">Производительность шлюза приложений:</span><span class="sxs-lookup"><span data-stu-id="466d9-175">Application Gateway performance</span></span>
  * <span data-ttu-id="466d9-176">работоспособность узла для шлюза приложений;</span><span class="sxs-lookup"><span data-stu-id="466d9-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="466d9-177">максимальное количество и 95-й процентиль для неудачных запросов шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="466d9-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![снимок экрана: панель мониторинга "Анализ шлюзов приложений Azure"](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![снимок экрана: панель мониторинга "Анализ шлюзов приложений Azure"](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="466d9-180">На панели мониторинга **Azure Application Gateway analytics** (Анализ шлюзов приложений Azure) просмотрите сводные данные в колонках, а затем щелкните одну из них, чтобы просмотреть подробные сведения на странице поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="466d9-180">On the **Azure Application Gateway analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="466d9-181">На любой из страниц поиска журналов можно просмотреть результаты по времени, подробные результаты и историю поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="466d9-181">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="466d9-182">Для сужения области результатов выполните фильтрацию по аспектам.</span><span class="sxs-lookup"><span data-stu-id="466d9-182">You can also filter by facets to narrow the results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="466d9-183">Решение для анализа групп безопасности сети Azure в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="466d9-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Символ "Аналитика групп безопасности сетей Azure"](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="466d9-185">Группы безопасности сети поддерживают следующие журналы:</span><span class="sxs-lookup"><span data-stu-id="466d9-185">The following logs are supported for network security groups:</span></span>

* <span data-ttu-id="466d9-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="466d9-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="466d9-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="466d9-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="466d9-188">Установка и настройка решения</span><span class="sxs-lookup"><span data-stu-id="466d9-188">Install and configure the solution</span></span>
<span data-ttu-id="466d9-189">Установите и настройте решение для анализа сетей Azure, выполнив следующие указания:</span><span class="sxs-lookup"><span data-stu-id="466d9-189">Use the following instructions to install and configure the Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="466d9-190">Включите решение для анализа групп безопасности сети Azure из [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) или выполните инструкции из статьи [Добавление решений для управления Azure Log Analytics в рабочую область](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="466d9-190">Enable the Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="466d9-191">Включите ведение журнала диагностики для ресурсов [групп безопасности сети](../virtual-network/virtual-network-nsg-manage-log.md), для которых требуется выполнять мониторинг.</span><span class="sxs-lookup"><span data-stu-id="466d9-191">Enable diagnostics logging for the [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want to monitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-the-portal"></a><span data-ttu-id="466d9-192">Включение диагностики групп безопасности сети Azure на портале</span><span class="sxs-lookup"><span data-stu-id="466d9-192">Enable Azure network security group diagnostics in the portal</span></span>

1. <span data-ttu-id="466d9-193">На портале Azure перейдите к ресурсу группы безопасности сети, который необходимо отслеживать.</span><span class="sxs-lookup"><span data-stu-id="466d9-193">In the Azure portal, navigate to the Network Security Group resource to monitor</span></span>
2. <span data-ttu-id="466d9-194">Выберите *Журналы диагностики*, чтобы открыть следующую страницу:</span><span class="sxs-lookup"><span data-stu-id="466d9-194">Select *Diagnostics logs* to open the following page</span></span>

   ![снимок экрана: ресурс группы безопасности сети Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="466d9-196">Щелкните *Включить диагностику*, чтобы открыть следующую страницу:</span><span class="sxs-lookup"><span data-stu-id="466d9-196">Click *Turn on diagnostics* to open the following page</span></span>

   ![снимок экрана: ресурс группы безопасности сети Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="466d9-198">Чтобы включить диагностику, нажмите кнопку *Вкл.* в разделе *Состояние*.</span><span class="sxs-lookup"><span data-stu-id="466d9-198">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="466d9-199">Установите флажок *Send to Log Analytics* (Отправить в Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="466d9-199">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="466d9-200">Выберите существующую рабочую область Log Analytics или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="466d9-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="466d9-201">В разделе **Журнал** установите флажки для всех типов журналов, которые необходимо собирать.</span><span class="sxs-lookup"><span data-stu-id="466d9-201">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="466d9-202">Щелкните *Сохранить*, чтобы включить ведение журнала диагностики в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="466d9-202">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="466d9-203">Включение диагностики сети Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="466d9-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="466d9-204">Следующий сценарий PowerShell приведен в качестве примера того, как включить ведение журналов диагностики для групп безопасности сети:</span><span class="sxs-lookup"><span data-stu-id="466d9-204">The following PowerShell script provides an example of how to enable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="466d9-205">Использование анализа групп безопасности сети Azure</span><span class="sxs-lookup"><span data-stu-id="466d9-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="466d9-206">Выбрав элемент **Azure Network Security Group analytics** (Анализ групп безопасности сети Azure) в разделе "Обзор", можно просмотреть сводные данные журналов и подробные сведения по следующим категориям:</span><span class="sxs-lookup"><span data-stu-id="466d9-206">After you click the **Azure Network Security Group analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="466d9-207">Заблокированные потоки группы безопасности сети:</span><span class="sxs-lookup"><span data-stu-id="466d9-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="466d9-208">правила группы безопасности сети с заблокированными потоками;</span><span class="sxs-lookup"><span data-stu-id="466d9-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="466d9-209">MAC-адреса c заблокированными потоками.</span><span class="sxs-lookup"><span data-stu-id="466d9-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="466d9-210">Разрешенные потоки группы безопасности сети:</span><span class="sxs-lookup"><span data-stu-id="466d9-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="466d9-211">правила группы безопасности сети с разрешенными потоками;</span><span class="sxs-lookup"><span data-stu-id="466d9-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="466d9-212">MAC-адреса c разрешенными потоками.</span><span class="sxs-lookup"><span data-stu-id="466d9-212">MAC addresses with allowed flows</span></span>

![снимок экрана: панель мониторинга "Анализ групп безопасности сети Azure"](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![снимок экрана: панель мониторинга "Анализ групп безопасности сети Azure"](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="466d9-215">На панели мониторинга **Azure Network Security Group analytics** (Анализ групп безопасности сети Azure) просмотрите сводные данные в колонках, а затем щелкните одну из них, чтобы просмотреть подробные сведения на странице поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="466d9-215">On the **Azure Network Security Group analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="466d9-216">На любой из страниц поиска журналов можно просмотреть результаты по времени, подробные результаты и историю поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="466d9-216">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="466d9-217">Для сужения области результатов выполните фильтрацию по аспектам.</span><span class="sxs-lookup"><span data-stu-id="466d9-217">You can also filter by facets to narrow the results.</span></span>

## <a name="migrating-from-the-old-networking-analytics-solution"></a><span data-ttu-id="466d9-218">Миграция из устаревшего решения для анализа сетевой активности</span><span class="sxs-lookup"><span data-stu-id="466d9-218">Migrating from the old Networking Analytics solution</span></span>
<span data-ttu-id="466d9-219">В январе 2017 г. поддерживаемый способ отправки журналов из шлюзов приложений Azure и групп безопасности сети Azure в Log Analytics был изменен.</span><span class="sxs-lookup"><span data-stu-id="466d9-219">In January 2017, the supported way of sending logs from Azure Application Gateways and Azure Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="466d9-220">Эти изменения обеспечивают следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="466d9-220">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="466d9-221">Журналы записываются непосредственно в Log Analytics без необходимости использования учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="466d9-221">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="466d9-222">Меньше задержка между моментом создания журналов и их доступностью в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="466d9-222">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="466d9-223">Меньше этапов настройки.</span><span class="sxs-lookup"><span data-stu-id="466d9-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="466d9-224">Общий формат для всех типов системы диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="466d9-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="466d9-225">Чтобы использовать обновленные решения, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="466d9-225">To use the updated solutions:</span></span>

1. <span data-ttu-id="466d9-226">[Настройте непосредственную отправку данных диагностики из шлюзов приложений Azure в Log Analytics](#enable-azure-application-gateway-diagnostics-in-the-portal).</span><span class="sxs-lookup"><span data-stu-id="466d9-226">[Configure diagnostics to be sent directly to Log Analytics from Azure Application Gateways](#enable-azure-application-gateway-diagnostics-in-the-portal)</span></span>
2. <span data-ttu-id="466d9-227">[Настройте непосредственную отправку данных диагностики из групп безопасности сети Azure в Log Analytics](#enable-azure-network-security-group-diagnostics-in-the-portal).</span><span class="sxs-lookup"><span data-stu-id="466d9-227">[Configure diagnostics to be sent directly to Log Analytics from Azure Network Security Groups](#enable-azure-network-security-group-diagnostics-in-the-portal)</span></span>
2. <span data-ttu-id="466d9-228">Включите решения для *анализа шлюзов приложений Azure* и *анализа групп безопасности сети Azure*, как описано в статье [Добавление решений для управления Log Analytics](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="466d9-228">Enable the *Azure Application Gateway Analytics* and the *Azure Network Security Group Analytics* solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="466d9-229">Обновите все сохраненные запросы, панели мониторинга и оповещения, чтобы использовать новый тип данных.</span><span class="sxs-lookup"><span data-stu-id="466d9-229">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="466d9-230">Тип меняется на AzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="466d9-230">Type is to AzureDiagnostics.</span></span> <span data-ttu-id="466d9-231">Параметр ResourceType можно использовать для фильтрации по журналам сети.</span><span class="sxs-lookup"><span data-stu-id="466d9-231">You can use the ResourceType to filter to Azure networking logs.</span></span>

    | <span data-ttu-id="466d9-232">Используйте такую замену:</span><span class="sxs-lookup"><span data-stu-id="466d9-232">Instead of:</span></span> | <span data-ttu-id="466d9-233">Используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="466d9-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="466d9-234">Для любого поля, имя которого содержит суффикс \_s, \_d или \_g, переведите первый знак в нижний регистр.</span><span class="sxs-lookup"><span data-stu-id="466d9-234">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
   + <span data-ttu-id="466d9-235">Для любого поля, имя которого содержит суффикс \_o, данные разбиваются на отдельные поля на основе имен вложенных полей.</span><span class="sxs-lookup"><span data-stu-id="466d9-235">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span>
4. <span data-ttu-id="466d9-236">Удалите устаревшее решение *Анализ сетевой активности Azure (не рекомендуется)*.</span><span class="sxs-lookup"><span data-stu-id="466d9-236">Remove the *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="466d9-237">Если используется PowerShell, то выполните следующую команду: `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="466d9-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="466d9-238">Данные, собранные до этого изменения, не отображаются в новом решении.</span><span class="sxs-lookup"><span data-stu-id="466d9-238">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="466d9-239">Эти данные по-прежнему можно запрашивать с помощью старых имен типов и полей.</span><span class="sxs-lookup"><span data-stu-id="466d9-239">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="466d9-240">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="466d9-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="466d9-241">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="466d9-241">Next steps</span></span>
* <span data-ttu-id="466d9-242">Используйте [поиск по журналам в Log Analytics](log-analytics-log-searches.md) для просмотра подробных данных диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="466d9-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure diagnostics data.</span></span>
