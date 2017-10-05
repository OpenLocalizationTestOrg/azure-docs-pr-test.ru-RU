---
title: "Решение хранилища ключей Azure в Log Analytics | Документация Майкрософт"
description: "Решение хранилища ключей Azure в Log Analytics позволяет просматривать журналы хранилища ключей Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 651586e0846ffb22a23e64b73c2cc614980d9b92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a><span data-ttu-id="1241e-103">Решение Azure Key Vault Analytics в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1241e-103">Azure Key Vault Analytics solution in Log Analytics</span></span>

![Символ Key Vault](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

<span data-ttu-id="1241e-105">Решение хранилища ключей Azure в Log Analytics позволяет просматривать журналы AuditEvent хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="1241e-105">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span>

<span data-ttu-id="1241e-106">Чтобы использовать решение, необходимо включить ведение журнала диагностики хранилища ключей Azure и направить диагностику в рабочую область Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1241e-106">To use the solution, you need to enable logging of Azure Key Vault diagnostics and direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="1241e-107">Необязательно записывать журналы в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="1241e-107">It is not necessary to write the logs to Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="1241e-108">В январе 2017 г. поддерживаемый способ отправки журналов из Key Vault в Log Analytics был изменен.</span><span class="sxs-lookup"><span data-stu-id="1241e-108">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="1241e-109">Если в используемом вами решении Key Vault в названии отображается *(не рекомендуется)*, то выполните действия, описанные в разделе [Миграция из устаревшего решения Key Vault](#migrating-from-the-old-key-vault-solution).</span><span class="sxs-lookup"><span data-stu-id="1241e-109">If the Key Vault solution you are using shows *(deprecated)* in the title, refer to [migrating from the old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need to follow.</span></span>
>
>

## <a name="install-and-configure-the-solution"></a><span data-ttu-id="1241e-110">Установка и настройка решения</span><span class="sxs-lookup"><span data-stu-id="1241e-110">Install and configure the solution</span></span>
<span data-ttu-id="1241e-111">Установите и настройте решение хранилища ключей Azure, выполнив следующие указания:</span><span class="sxs-lookup"><span data-stu-id="1241e-111">Use the following instructions to install and configure the Azure Key Vault solution:</span></span>

1. <span data-ttu-id="1241e-112">Включите решение Azure Key Vault из [Azure Мarketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) или в соответствии с инструкциями по [добавлению решений Log Analytics из коллекции решений](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="1241e-112">Enable the Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="1241e-113">Включите ведение журнала диагностики для мониторинга ресурсов Key Vault, используя [портал](#enable-key-vault-diagnostics-in-the-portal) или [PowerShell](#enable-key-vault-diagnostics-using-powershell).</span><span class="sxs-lookup"><span data-stu-id="1241e-113">Enable diagnostics logging for the Key Vault resources to monitor, using either the [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span></span>

### <a name="enable-key-vault-diagnostics-in-the-portal"></a><span data-ttu-id="1241e-114">Включение диагностики Key Vault на портале</span><span class="sxs-lookup"><span data-stu-id="1241e-114">Enable Key Vault diagnostics in the portal</span></span>

1. <span data-ttu-id="1241e-115">На портале Azure перейдите к ресурсу Key Vault, который необходимо отслеживать.</span><span class="sxs-lookup"><span data-stu-id="1241e-115">In the Azure portal, navigate to the Key Vault resource to monitor</span></span>
2. <span data-ttu-id="1241e-116">Выберите *Журналы диагностики*, чтобы открыть следующую страницу:</span><span class="sxs-lookup"><span data-stu-id="1241e-116">Select *Diagnostics logs* to open the following page</span></span>

   ![изображение плитки "Хранилище ключей Azure"](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. <span data-ttu-id="1241e-118">Щелкните *Включить диагностику*, чтобы открыть следующую страницу:</span><span class="sxs-lookup"><span data-stu-id="1241e-118">Click *Turn on diagnostics* to open the following page</span></span>

   ![изображение плитки "Хранилище ключей Azure"](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. <span data-ttu-id="1241e-120">Чтобы включить диагностику, нажмите кнопку *Вкл.* в разделе *Состояние*.</span><span class="sxs-lookup"><span data-stu-id="1241e-120">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="1241e-121">Установите флажок *Send to Log Analytics* (Отправить в Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="1241e-121">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="1241e-122">Выберите существующую рабочую область Log Analytics или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="1241e-122">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="1241e-123">Чтобы включить журналы *AuditEvent*, установите соответствующий флажок в разделе "Журнал".</span><span class="sxs-lookup"><span data-stu-id="1241e-123">To enable *AuditEvent* logs, click the checkbox under Log</span></span>
8. <span data-ttu-id="1241e-124">Щелкните *Сохранить*, чтобы включить ведение журнала диагностики в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1241e-124">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-key-vault-diagnostics-using-powershell"></a><span data-ttu-id="1241e-125">Включение диагностики Key Vault с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1241e-125">Enable Key Vault diagnostics using PowerShell</span></span>
<span data-ttu-id="1241e-126">Следующий сценарий PowerShell приведен в качестве примера того, как с помощью командлета `Set-AzureRmDiagnosticSetting` включить ведения журналов диагностики для Key Vault:</span><span class="sxs-lookup"><span data-stu-id="1241e-126">The following PowerShell script provides an example of how to use `Set-AzureRmDiagnosticSetting` to enable diagnostic logging for Key Vault:</span></span>
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a><span data-ttu-id="1241e-127">Просмотр сведений о сборе данных хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="1241e-127">Review Azure Key Vault data collection details</span></span>
<span data-ttu-id="1241e-128">Решение хранилища ключей Azure собирает журналы диагностики напрямую из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="1241e-128">Azure Key Vault solution collects diagnostics logs directly from the Key Vault.</span></span>
<span data-ttu-id="1241e-129">Необязательно записывать журналы в хранилище BLOB-объектов Azure. Для сбора данных агенты не требуются.</span><span class="sxs-lookup"><span data-stu-id="1241e-129">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="1241e-130">В следующей таблице приведены методы сбора данных и другие сведения о сборе данных для хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="1241e-130">The following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span></span>

| <span data-ttu-id="1241e-131">Платформа</span><span class="sxs-lookup"><span data-stu-id="1241e-131">Platform</span></span> | <span data-ttu-id="1241e-132">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="1241e-132">Direct agent</span></span> | <span data-ttu-id="1241e-133">Агент Systems Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="1241e-133">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="1241e-134">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="1241e-134">Azure</span></span> | <span data-ttu-id="1241e-135">Нужен ли Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="1241e-135">Operations Manager required?</span></span> | <span data-ttu-id="1241e-136">Отправка данных агента Operations Manager через группу управления</span><span class="sxs-lookup"><span data-stu-id="1241e-136">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="1241e-137">Частота сбора</span><span class="sxs-lookup"><span data-stu-id="1241e-137">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="1241e-138">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="1241e-138">Azure</span></span> |  |  |<span data-ttu-id="1241e-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1241e-139">&#8226;</span></span> |  |  | <span data-ttu-id="1241e-140">при получении</span><span class="sxs-lookup"><span data-stu-id="1241e-140">on arrival</span></span> |

## <a name="use-azure-key-vault"></a><span data-ttu-id="1241e-141">Использование хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="1241e-141">Use Azure Key Vault</span></span>
<span data-ttu-id="1241e-142">[Установив решение](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) просмотрите данные Key Vault, щелкнув плитку **Azure Key Vault** на странице **Обзор** в службе Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1241e-142">After you [install the solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view the Key Vault data by clicking the **Azure Key Vault** tile from the **Overview** page of Log Analytics.</span></span>

![изображение плитки "Хранилище ключей Azure"](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

<span data-ttu-id="1241e-144">Выбрав плитку **Обзор**, можно просмотреть сводные данные журналов и подробные сведения по следующим категориям:</span><span class="sxs-lookup"><span data-stu-id="1241e-144">After you click the **Overview** tile, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="1241e-145">количество всех операций хранилища ключей за определенный период;</span><span class="sxs-lookup"><span data-stu-id="1241e-145">Volume of all key vault operations over time</span></span>
* <span data-ttu-id="1241e-146">количество неудавшихся операций за определенный период;</span><span class="sxs-lookup"><span data-stu-id="1241e-146">Failed operation volumes over time</span></span>
* <span data-ttu-id="1241e-147">среднее время задержки для каждой операции;</span><span class="sxs-lookup"><span data-stu-id="1241e-147">Average operational latency by operation</span></span>
* <span data-ttu-id="1241e-148">качество обслуживания для операций с количеством операций, выполнявшихся более 1000 мс, и списком этих операций.</span><span class="sxs-lookup"><span data-stu-id="1241e-148">Quality of service for operations with the number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span></span>

![изображение панели мониторинга хранилища ключей Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![изображение панели мониторинга хранилища ключей Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="to-view-details-for-any-operation"></a><span data-ttu-id="1241e-151">Просмотр сведений об операциях</span><span class="sxs-lookup"><span data-stu-id="1241e-151">To view details for any operation</span></span>
1. <span data-ttu-id="1241e-152">На странице **Обзор** щелкните плитку **Хранилище ключей Azure**.</span><span class="sxs-lookup"><span data-stu-id="1241e-152">On the **Overview** page, click the **Azure Key Vault** tile.</span></span>
2. <span data-ttu-id="1241e-153">На панели мониторинга **Хранилище ключей Azure** просмотрите сводные данные в одной из колонок, а затем щелкните одну из них, чтобы просмотреть подробные сведения на странице поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="1241e-153">On the **Azure Key Vault** dashboard, review the summary information in one of the blades, and then click one to view detailed information about it in the log search page.</span></span>

    <span data-ttu-id="1241e-154">На любой из страниц поиска журналов можно просмотреть результаты по времени, подробные результаты и историю поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="1241e-154">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="1241e-155">Для сужения области результатов выполните фильтрацию по аспектам.</span><span class="sxs-lookup"><span data-stu-id="1241e-155">You can also filter by facets to narrow the results.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="1241e-156">Записи Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1241e-156">Log Analytics records</span></span>
<span data-ttu-id="1241e-157">Решение хранилища ключей Azure анализирует записи типа **KeyVaults**, полученные из [журналов AuditEvent](../key-vault/key-vault-logging.md) системы диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="1241e-157">The Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span></span>  <span data-ttu-id="1241e-158">Свойства этих записей приведены в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1241e-158">Properties for these records are in the following table:</span></span>  

| <span data-ttu-id="1241e-159">Свойство</span><span class="sxs-lookup"><span data-stu-id="1241e-159">Property</span></span> | <span data-ttu-id="1241e-160">Описание</span><span class="sxs-lookup"><span data-stu-id="1241e-160">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1241e-161">Тип</span><span class="sxs-lookup"><span data-stu-id="1241e-161">Type</span></span> |<span data-ttu-id="1241e-162">*AzureDiagnostics*</span><span class="sxs-lookup"><span data-stu-id="1241e-162">*AzureDiagnostics*</span></span> |
| <span data-ttu-id="1241e-163">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1241e-163">SourceSystem</span></span> |<span data-ttu-id="1241e-164">*Таблицы Azure*</span><span class="sxs-lookup"><span data-stu-id="1241e-164">*Azure*</span></span> |
| <span data-ttu-id="1241e-165">CallerIpAddress</span><span class="sxs-lookup"><span data-stu-id="1241e-165">CallerIpAddress</span></span> |<span data-ttu-id="1241e-166">IP-адрес клиента, отправившего запрос.</span><span class="sxs-lookup"><span data-stu-id="1241e-166">IP address of the client who made the request</span></span> |
| <span data-ttu-id="1241e-167">Категория</span><span class="sxs-lookup"><span data-stu-id="1241e-167">Category</span></span> | <span data-ttu-id="1241e-168">*AuditEvent*</span><span class="sxs-lookup"><span data-stu-id="1241e-168">*AuditEvent*</span></span> |
| <span data-ttu-id="1241e-169">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="1241e-169">CorrelationId</span></span> |<span data-ttu-id="1241e-170">Необязательный GUID, который клиент может передавать для сопоставления журналов на стороне клиента с журналами на стороне службы (хранилища ключей).</span><span class="sxs-lookup"><span data-stu-id="1241e-170">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="1241e-171">DurationMs</span><span class="sxs-lookup"><span data-stu-id="1241e-171">DurationMs</span></span> |<span data-ttu-id="1241e-172">Время обслуживания запроса REST API в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="1241e-172">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="1241e-173">Это время не включает в себя задержку сети, поэтому время, зарегистрированное на стороне клиента, может не соответствовать этому значению.</span><span class="sxs-lookup"><span data-stu-id="1241e-173">This time does not include network latency, so the time that you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="1241e-174">HttpStatusCode_d</span><span class="sxs-lookup"><span data-stu-id="1241e-174">httpStatusCode_d</span></span> |<span data-ttu-id="1241e-175">Код состояния HTTP, возвращаемый запросом (например, *200*)</span><span class="sxs-lookup"><span data-stu-id="1241e-175">HTTP status code returned by the request (for example, *200*)</span></span> |
| <span data-ttu-id="1241e-176">id_s</span><span class="sxs-lookup"><span data-stu-id="1241e-176">id_s</span></span> |<span data-ttu-id="1241e-177">Уникальный идентификатор запроса.</span><span class="sxs-lookup"><span data-stu-id="1241e-177">Unique ID of the request</span></span> |
| <span data-ttu-id="1241e-178">identity_claim_appid_g</span><span class="sxs-lookup"><span data-stu-id="1241e-178">identity_claim_appid_g</span></span> | <span data-ttu-id="1241e-179">GUID для идентификатора приложения</span><span class="sxs-lookup"><span data-stu-id="1241e-179">GUID for the application id</span></span> |
| <span data-ttu-id="1241e-180">OperationName</span><span class="sxs-lookup"><span data-stu-id="1241e-180">OperationName</span></span> |<span data-ttu-id="1241e-181">Имя операции, как описано в статье [Ведение журнала хранилища ключей Azure](../key-vault/key-vault-logging.md)</span><span class="sxs-lookup"><span data-stu-id="1241e-181">Name of the operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span></span> |
| <span data-ttu-id="1241e-182">OperationVersion</span><span class="sxs-lookup"><span data-stu-id="1241e-182">OperationVersion</span></span> |<span data-ttu-id="1241e-183">Запрошенная клиентом версия REST API (например, *2015-06-01*)</span><span class="sxs-lookup"><span data-stu-id="1241e-183">REST API version requested by the client (for example *2015-06-01*)</span></span> |
| <span data-ttu-id="1241e-184">requestUri_s</span><span class="sxs-lookup"><span data-stu-id="1241e-184">requestUri_s</span></span> |<span data-ttu-id="1241e-185">URI запроса</span><span class="sxs-lookup"><span data-stu-id="1241e-185">Uri of the request</span></span> |
| <span data-ttu-id="1241e-186">Ресурс</span><span class="sxs-lookup"><span data-stu-id="1241e-186">Resource</span></span> |<span data-ttu-id="1241e-187">Имя хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="1241e-187">Name of the key vault</span></span> |
| <span data-ttu-id="1241e-188">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1241e-188">ResourceGroup</span></span> |<span data-ttu-id="1241e-189">Группа ресурсов хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="1241e-189">Resource group of the key vault</span></span> |
| <span data-ttu-id="1241e-190">ResourceId</span><span class="sxs-lookup"><span data-stu-id="1241e-190">ResourceId</span></span> |<span data-ttu-id="1241e-191">Идентификатор ресурса диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="1241e-191">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="1241e-192">Для журналов хранилища ключей это идентификатор ресурса хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="1241e-192">For Key Vault logs, this is the Key Vault resource ID.</span></span> |
| <span data-ttu-id="1241e-193">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="1241e-193">ResourceProvider</span></span> |<span data-ttu-id="1241e-194">*MICROSOFT.KEYVAULT*</span><span class="sxs-lookup"><span data-stu-id="1241e-194">*MICROSOFT.KEYVAULT*</span></span> |
| <span data-ttu-id="1241e-195">ResourceType</span><span class="sxs-lookup"><span data-stu-id="1241e-195">ResourceType</span></span> | <span data-ttu-id="1241e-196">*VAULTS*</span><span class="sxs-lookup"><span data-stu-id="1241e-196">*VAULTS*</span></span> |
| <span data-ttu-id="1241e-197">ResultSignature</span><span class="sxs-lookup"><span data-stu-id="1241e-197">ResultSignature</span></span> |<span data-ttu-id="1241e-198">Код состояния HTTP (например, *ОК*)</span><span class="sxs-lookup"><span data-stu-id="1241e-198">HTTP status (for example, *OK*)</span></span> |
| <span data-ttu-id="1241e-199">ResultType</span><span class="sxs-lookup"><span data-stu-id="1241e-199">ResultType</span></span> |<span data-ttu-id="1241e-200">Результат запроса REST API (например, *Успешно*)</span><span class="sxs-lookup"><span data-stu-id="1241e-200">Result of REST API request (for example, *Success*)</span></span> |
| <span data-ttu-id="1241e-201">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="1241e-201">SubscriptionId</span></span> |<span data-ttu-id="1241e-202">Идентификатор подписки Azure, которая содержит хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="1241e-202">Azure subscription ID of the subscription containing the Key Vault</span></span> |

## <a name="migrating-from-the-old-key-vault-solution"></a><span data-ttu-id="1241e-203">Миграция из устаревшего решения Key Vault</span><span class="sxs-lookup"><span data-stu-id="1241e-203">Migrating from the old Key Vault solution</span></span>
<span data-ttu-id="1241e-204">В январе 2017 г. поддерживаемый способ отправки журналов из Key Vault в Log Analytics был изменен.</span><span class="sxs-lookup"><span data-stu-id="1241e-204">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="1241e-205">Эти изменения обеспечивают следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1241e-205">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="1241e-206">Журналы записываются непосредственно в Log Analytics без необходимости использования учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="1241e-206">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="1241e-207">Меньше задержка между моментом создания журналов и их доступностью в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1241e-207">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="1241e-208">Меньше этапов настройки.</span><span class="sxs-lookup"><span data-stu-id="1241e-208">Fewer configuration steps</span></span>
+ <span data-ttu-id="1241e-209">Общий формат для всех типов системы диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="1241e-209">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="1241e-210">Чтобы использовать обновленное решение, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1241e-210">To use the updated solution:</span></span>

1. <span data-ttu-id="1241e-211">[Настройте непосредственную отправку данных диагностики из Key Vault в Log Analytics](#enable-key-vault-diagnostics-in-the-portal).</span><span class="sxs-lookup"><span data-stu-id="1241e-211">[Configure diagnostics to be sent directly to Log Analytics from Key Vault](#enable-key-vault-diagnostics-in-the-portal)</span></span>  
2. <span data-ttu-id="1241e-212">Включите решение Azure Key Vault, как описано в статье [Добавление решений для управления Log Analytics](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="1241e-212">Enable the Azure Key Vault solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="1241e-213">Обновите все сохраненные запросы, панели мониторинга и оповещения, чтобы использовать новый тип данных.</span><span class="sxs-lookup"><span data-stu-id="1241e-213">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="1241e-214">Тип меняется с KeyVaults на AzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="1241e-214">Type is change from: KeyVaults to AzureDiagnostics.</span></span> <span data-ttu-id="1241e-215">Параметр ResourceType можно использовать для фильтрации по журналам Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1241e-215">You can use the ResourceType to filter to Key Vault Logs.</span></span>
  - <span data-ttu-id="1241e-216">Вместо `Type=KeyVaults` используйте `Type=AzureDiagnostics ResourceType=VAULTS`.</span><span class="sxs-lookup"><span data-stu-id="1241e-216">Instead of: `Type=KeyVaults`, use `Type=AzureDiagnostics ResourceType=VAULTS`</span></span>
  + <span data-ttu-id="1241e-217">Поля (в именах полей учитывается регистр).</span><span class="sxs-lookup"><span data-stu-id="1241e-217">Fields: (Field names are case-sensitive)</span></span>
  - <span data-ttu-id="1241e-218">Для любого поля, имя которого содержит суффикс \_s, \_d или \_g, переведите первый знак в нижний регистр.</span><span class="sxs-lookup"><span data-stu-id="1241e-218">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
  - <span data-ttu-id="1241e-219">Для любого поля, имя которого содержит суффикс \_o, данные разбиваются на отдельные поля на основе имен вложенных полей.</span><span class="sxs-lookup"><span data-stu-id="1241e-219">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span> <span data-ttu-id="1241e-220">Например, имя участника-пользователя вызывающего объекта сохраняется в поле `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`.</span><span class="sxs-lookup"><span data-stu-id="1241e-220">For example, the UPN of the caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span></span>
   - <span data-ttu-id="1241e-221">Поле CallerIpAddress меняется на CallerIPAddress.</span><span class="sxs-lookup"><span data-stu-id="1241e-221">Field CallerIpAddress changed to CallerIPAddress</span></span>
   - <span data-ttu-id="1241e-222">Поле RemoteIPCountry больше не используется.</span><span class="sxs-lookup"><span data-stu-id="1241e-222">Field RemoteIPCountry is no longer present</span></span>
4. <span data-ttu-id="1241e-223">Удалите устаревшее решение *Key Vault Analytics (не рекомендуется)*.</span><span class="sxs-lookup"><span data-stu-id="1241e-223">Remove the *Key Vault Analytics (Deprecated)* solution.</span></span> <span data-ttu-id="1241e-224">Если используется PowerShell, то выполните следующую команду: `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="1241e-224">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span></span>

<span data-ttu-id="1241e-225">Данные, собранные до этого изменения, не отображаются в новом решении.</span><span class="sxs-lookup"><span data-stu-id="1241e-225">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="1241e-226">Эти данные по-прежнему можно запрашивать с помощью старых имен типов и полей.</span><span class="sxs-lookup"><span data-stu-id="1241e-226">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1241e-227">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="1241e-227">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="1241e-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1241e-228">Next steps</span></span>
* <span data-ttu-id="1241e-229">Используйте [поиск по журналам в Log Analytics](log-analytics-log-searches.md) для просмотра подробных данных о хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="1241e-229">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure Key Vault data.</span></span>
