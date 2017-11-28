---
title: "aaaMonitor доступ к журналов, журналов производительности, работоспособности серверной части и метрики для шлюза приложения | Документы Microsoft"
description: "Узнайте, как tooenable и управление журналы событий и журналы производительности для шлюза приложений"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="0e9cd-103">Работоспособность серверной части, журналы диагностики и метрики для шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="0e9cd-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="0e9cd-104">С помощью шлюза приложения Azure, можно отслеживать ресурсы hello следующих способов:</span><span class="sxs-lookup"><span data-stu-id="0e9cd-104">By using Azure Application Gateway, you can monitor resources in hello following ways:</span></span>

* <span data-ttu-id="0e9cd-105">[Тыловой работоспособности](#back-end-health): использование шлюза приложений предоставляет hello toomonitor возможность hello работоспособности серверов hello в hello пулы серверной части через портал Azure hello и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-105">[Back-end health](#back-end-health): Application Gateway provides hello capability toomonitor hello health of hello servers in hello back-end pools through hello Azure portal and through PowerShell.</span></span> <span data-ttu-id="0e9cd-106">Также можно найти работоспособности hello hello пулов серверной части через журналы диагностики производительности hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-106">You can also find hello health of hello back-end pools through hello performance diagnostic logs.</span></span>

* <span data-ttu-id="0e9cd-107">[Журналы](#diagnostic-logs): разрешить журналы для доступа, производительности и других данных toobe сохранения или извлечена из ресурса в целях мониторинга.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data toobe saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="0e9cd-108">[Метрики.](#metrics) Сейчас в шлюзе приложений используется одна метрика.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="0e9cd-109">Этот показатель измеряет hello пропускная способность шлюза приложения hello в байтах в секунду.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-109">This metric measures hello throughput of hello application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="0e9cd-110">Работоспособность серверной части</span><span class="sxs-lookup"><span data-stu-id="0e9cd-110">Back-end health</span></span>

<span data-ttu-id="0e9cd-111">Шлюз приложений предоставляет возможность hello toomonitor работоспособности hello отдельных членов hello пулов серверной части через портал hello, PowerShell и hello командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="0e9cd-111">Application Gateway provides hello capability toomonitor hello health of individual members of hello back-end pools through hello portal, PowerShell, and hello command-line interface (CLI).</span></span> <span data-ttu-id="0e9cd-112">Можно также найти сводной работоспособности сводки пулов серверной части через журналы диагностики производительности hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-112">You can also find an aggregated health summary of back-end pools through hello performance diagnostic logs.</span></span> 

<span data-ttu-id="0e9cd-113">отчет о работоспособности серверной части Hello отражает hello выходные данные экземпляров hello шлюз приложений работоспособности проверки toohello серверной части.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-113">hello back-end health report reflects hello output of hello Application Gateway health probe toohello back-end instances.</span></span> <span data-ttu-id="0e9cd-114">Если проверка прошла успешно и обратно hello end могут получать трафик, считается исправной.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-114">When probing is successful and hello back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="0e9cd-115">В противном случае серверная часть считается неработоспособной.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e9cd-116">Если имеется группа безопасности сети (NSG) в подсети шлюза приложений, откройте диапазоны портов 65503 65534 в подсети шлюза приложения hello для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on hello Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="0e9cd-117">Эти порты являются обязательными для API toowork hello работоспособности серверной части.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-117">These ports are required for hello back-end health API toowork.</span></span>


### <a name="view-back-end-health-through-hello-portal"></a><span data-ttu-id="0e9cd-118">Просмотр состояния работоспособности серверной части через портал hello</span><span class="sxs-lookup"><span data-stu-id="0e9cd-118">View back-end health through hello portal</span></span>

<span data-ttu-id="0e9cd-119">На портале hello работоспособности серверной части предоставляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-119">In hello portal, back-end health is provided automatically.</span></span> <span data-ttu-id="0e9cd-120">В существующем шлюзе приложений выберите **Мониторинг** > **Оценка работоспособности серверной части**.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="0e9cd-121">Каждый член пула внутренней hello значится на этой странице (будь то, что сетевой Адаптер, IP или полное доменное имя).</span><span class="sxs-lookup"><span data-stu-id="0e9cd-121">Each member in hello back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="0e9cd-122">На ней показаны имя внутреннего пула, порт, параметры HTTP внутреннего пула и его состояние работоспособности.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="0e9cd-123">Допустимые значения состояния работоспособности: **Работоспособен**, **Неработоспособен** и **Неизвестно**.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="0e9cd-124">Если вы видите состояние работоспособности серверной части **Неизвестный**, серверной части toohello доступ, не заблокирован, правило NSG, определяемых пользователем маршрутов (UDR) или пользовательского DNS-сервер в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-124">If you see a back-end health status of **Unknown**, ensure that access toohello back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in hello virtual network.</span></span>

![Работоспособность серверной части][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="0e9cd-126">Просмотр данных о работоспособности серверной части с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e9cd-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="0e9cd-127">Привет, следующий код PowerShell показано, как hello tooview работоспособности серверной части с помощью `Get-AzureRmApplicationGatewayBackendHealth` командлета:</span><span class="sxs-lookup"><span data-stu-id="0e9cd-127">hello following PowerShell code shows how tooview back-end health by using hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="0e9cd-128">Просмотр данных о работоспособности серверной части с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0e9cd-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="0e9cd-129">Результаты</span><span class="sxs-lookup"><span data-stu-id="0e9cd-129">Results</span></span>

<span data-ttu-id="0e9cd-130">Следующий фрагмент кода Hello показан пример hello ответа.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-130">hello following snippet shows an example of hello response:</span></span>

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <span data-ttu-id="0e9cd-131"><a name="diagnostic-logging"></a>Журналы диагностики</span><span class="sxs-lookup"><span data-stu-id="0e9cd-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="0e9cd-132">Можно использовать различные типы журналов в Azure toomanage и устранение неполадок шлюзы приложений.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-132">You can use different types of logs in Azure toomanage and troubleshoot application gateways.</span></span> <span data-ttu-id="0e9cd-133">Некоторые из этих журналах доступны через портал hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-133">You can access some of these logs through hello portal.</span></span> <span data-ttu-id="0e9cd-134">Также можно извлечь все журналы из хранилища BLOB-объектов Azure и просматривать их с помощью таких средств, как [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel и Power BI.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="0e9cd-135">Дополнительные сведения о различных типах hello журналов из hello после списка.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-135">You can learn more about hello different types of logs from hello following list:</span></span>

* <span data-ttu-id="0e9cd-136">**Журнал действий**: можно использовать [журналы действий Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (ранее называвшейся операционные журналы и журналы аудита) tooview все операции, которые будут отправлены tooyour подписки Azure и их состояние.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) tooview all operations that are submitted tooyour Azure subscription, and their status.</span></span> <span data-ttu-id="0e9cd-137">По умолчанию собираются записи журнала действий и их можно просмотреть в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-137">Activity log entries are collected by default, and you can view them in hello Azure portal.</span></span>
* <span data-ttu-id="0e9cd-138">**Журнал доступа**: можно использовать шаблоны доступа к шлюз приложений этот журнал tooview и проанализировать важные сведения, включая hello вызывающего IP, запрошенного URL-адреса, задержка отклика, код возврата и байт и выхода из системы. Данные для журнала доступа собираются каждые 300 секунд.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-138">**Access log**: You can use this log tooview Application Gateway access patterns and analyze important information, including hello caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="0e9cd-139">Этот журнал содержит одну запись для каждого экземпляра шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="0e9cd-140">экземпляр шлюза приложения Hello определяться свойство instanceId hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-140">hello Application Gateway instance can be identified by hello instanceId property.</span></span>
* <span data-ttu-id="0e9cd-141">**Журнал производительности**: можно использовать этот tooview журнала, как выполняются экземпляры шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-141">**Performance log**: You can use this log tooview how Application Gateway instances are performing.</span></span> <span data-ttu-id="0e9cd-142">В этот журнал записываются сведения о производительности каждого экземпляра, включая общее число обработанных запросов, пропускную способность в байтах, число неудачных запросов, а также число работоспособных и неработоспособных серверных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="0e9cd-143">Данные для журнала производительности собираются каждые 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="0e9cd-144">**Журнал брандмауэра**: можно использовать этот протокол tooview hello запросов, регистрируются через режим обнаружения или Предотвращение шлюза приложения, настроенного с hello брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-144">**Firewall log**: You can use this log tooview hello requests that are logged through either detection or prevention mode of an application gateway that is configured with hello web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="0e9cd-145">Журналы доступны только для ресурсов, развернутых в модели развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-145">Logs are available only for resources deployed in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="0e9cd-146">Нельзя использовать журналы для ресурсов в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-146">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="0e9cd-147">Для лучшего понимания hello двух моделей, в разделе hello [сведения о диспетчере ресурсов и классического развертывания](../azure-resource-manager/resource-manager-deployment-model.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-147">For a better understanding of hello two models, see hello [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="0e9cd-148">Существует три способа хранения журналов:</span><span class="sxs-lookup"><span data-stu-id="0e9cd-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="0e9cd-149">**Учетная запись хранения** лучше всего подходит для длительного хранения журналов и их просмотра по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="0e9cd-150">**Концентраторы событий**: концентраторы событий являются прекрасно подходит для интеграции с другими данными, безопасности и управления событиями (SEIM) средств tooget оповещения на ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools tooget alerts on your resources.</span></span>
* <span data-ttu-id="0e9cd-151">**Log Analytics** лучше всего подходит для общего мониторинга приложения в реальном времени и изучения тенденций.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="0e9cd-152">Включение ведения журнала с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e9cd-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="0e9cd-153">Ведение журнала действий автоматически включается для каждого ресурса Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="0e9cd-154">Необходимо включить доступа и toostart ведения журнала производительности, сбор данных hello, доступные через эти журналы.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-154">You must enable access and performance logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="0e9cd-155">tooenable входа hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="0e9cd-155">tooenable logging, use hello following steps:</span></span>

1. <span data-ttu-id="0e9cd-156">Обратите внимание, идентификатор ресурса вашей учетной записи хранилища, где хранятся данные журнала hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-156">Note your storage account's resource ID, where hello log data is stored.</span></span> <span data-ttu-id="0e9cd-157">Это значение имеет вид hello: /subscriptions/\<subscriptionId\>/resourceGroups/\<имя группы ресурсов\>/providers/Microsoft.Storage/storageAccounts/\<имя учетной записи хранения\>.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-157">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="0e9cd-158">Можно использовать любую учетную запись хранения в подписке.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="0e9cd-159">Эти сведения можно использовать hello Azure toofind портала.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-159">You can use hello Azure portal toofind this information.</span></span>

    ![ИД ресурса для учетной записи хранения на портале](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="0e9cd-161">Запишите или запомните идентификатор ресурса шлюза приложений, для которого нужно включить ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="0e9cd-162">Это значение имеет вид hello: /subscriptions/\<subscriptionId\>/resourceGroups/\<имя группы ресурсов\>/providers/Microsoft.Network/applicationGateways/\<шлюза приложений имя\>.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-162">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="0e9cd-163">Эти сведения можно использовать портала toofind hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-163">You can use hello portal toofind this information.</span></span>

    ![ИД ресурса для шлюза приложений на портале](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="0e9cd-165">Включите ведение журнала диагностики с помощью hello, выполнив командлет PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0e9cd-165">Enable diagnostic logging by using hello following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="0e9cd-166">Для журналов действий отдельная учетная запись хранения не требуется.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="0e9cd-167">Использование Hello хранилища для доступа и ведение журнала производительности влечет за собой службы оплаты.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-167">hello use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-hello-azure-portal"></a><span data-ttu-id="0e9cd-168">Включить ведение журнала через hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0e9cd-168">Enable logging through hello Azure portal</span></span>

1. <span data-ttu-id="0e9cd-169">В hello портал Azure, ресурс и нажмите кнопку **журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-169">In hello Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="0e9cd-170">Для шлюза приложений доступны три журнала:</span><span class="sxs-lookup"><span data-stu-id="0e9cd-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="0e9cd-171">журнал доступа;</span><span class="sxs-lookup"><span data-stu-id="0e9cd-171">Access log</span></span>
   * <span data-ttu-id="0e9cd-172">журнал производительности;</span><span class="sxs-lookup"><span data-stu-id="0e9cd-172">Performance log</span></span>
   * <span data-ttu-id="0e9cd-173">журнал брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-173">Firewall log</span></span>

2. <span data-ttu-id="0e9cd-174">Сбор данных о toostart, нажмите кнопку **включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-174">toostart collecting data, click **Turn on diagnostics**.</span></span>

   ![Включение диагностики][1]

3. <span data-ttu-id="0e9cd-176">Hello **параметры диагностики** колонке предоставляет параметры hello для hello журналы диагностики.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-176">hello **Diagnostics settings** blade provides hello settings for hello diagnostic logs.</span></span> <span data-ttu-id="0e9cd-177">В этом примере служба аналитики журналов хранятся журналы hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-177">In this example, Log Analytics stores hello logs.</span></span> <span data-ttu-id="0e9cd-178">Нажмите кнопку **Настройка** под **анализа журналов** tooconfigure рабочей области.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-178">Click **Configure** under **Log Analytics** tooconfigure your workspace.</span></span> <span data-ttu-id="0e9cd-179">Можно также использовать концентраторов событий и журналы учетной записи хранения toosave hello диагностики.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-179">You can also use event hubs and a storage account toosave hello diagnostic logs.</span></span>

   ![При запуске процесса конфигурации hello][2]

4. <span data-ttu-id="0e9cd-181">Выберите существующую рабочую область Operations Management Suite (OMS) или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="0e9cd-182">В этом примере используется существующая рабочая область.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-182">This example uses an existing one.</span></span>

   ![Параметры для рабочих областей OMS][3]

5. <span data-ttu-id="0e9cd-184">Подтверждение параметров hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-184">Confirm hello settings and click **Save**.</span></span>

   ![Колонка "Параметры диагностики" с выбранными значениями][4]

### <a name="activity-log"></a><span data-ttu-id="0e9cd-186">Журнал действий</span><span class="sxs-lookup"><span data-stu-id="0e9cd-186">Activity log</span></span>

<span data-ttu-id="0e9cd-187">Azure создает hello журнал действий по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-187">Azure generates hello activity log by default.</span></span> <span data-ttu-id="0e9cd-188">журналы Hello сохраняются в течение 90 дней в хранилище Azure журналы событий hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-188">hello logs are preserved for 90 days in hello Azure event logs store.</span></span> <span data-ttu-id="0e9cd-189">Дополнительные сведения об этих журналов, считывая hello [просматривать события и журнал действий](../monitoring-and-diagnostics/insights-debugging-with-events.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-189">Learn more about these logs by reading hello [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="0e9cd-190">журнал доступа;</span><span class="sxs-lookup"><span data-stu-id="0e9cd-190">Access log</span></span>

<span data-ttu-id="0e9cd-191">Журнал доступа Hello создается только в том случае, если он включен на каждом экземпляре шлюза приложения, как описано в предыдущих шагах hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-191">hello access log is generated only if you've enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="0e9cd-192">Hello данные хранятся в учетной записи хранения hello, указанного при включении ведения журнала hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-192">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="0e9cd-193">Каждый доступа шлюза приложение регистрируется в формате JSON, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="0e9cd-193">Each access of Application Gateway is logged in JSON format, as shown in hello following example:</span></span>


|<span data-ttu-id="0e9cd-194">Значение</span><span class="sxs-lookup"><span data-stu-id="0e9cd-194">Value</span></span>  |<span data-ttu-id="0e9cd-195">Описание</span><span class="sxs-lookup"><span data-stu-id="0e9cd-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="0e9cd-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="0e9cd-196">instanceId</span></span>     | <span data-ttu-id="0e9cd-197">Шлюз приложений экземпляра запроса обслуживаются hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-197">Application Gateway instance that served hello request.</span></span>        |
|<span data-ttu-id="0e9cd-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="0e9cd-198">clientIP</span></span>     | <span data-ttu-id="0e9cd-199">IP-адреса для запроса hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-199">Originating IP for hello request.</span></span>        |
|<span data-ttu-id="0e9cd-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="0e9cd-200">clientPort</span></span>     | <span data-ttu-id="0e9cd-201">Исходный порт для запроса hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-201">Originating port for hello request.</span></span>       |
|<span data-ttu-id="0e9cd-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="0e9cd-202">httpMethod</span></span>     | <span data-ttu-id="0e9cd-203">Метод HTTP, используемый запросом hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-203">HTTP method used by hello request.</span></span>       |
|<span data-ttu-id="0e9cd-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="0e9cd-204">requestUri</span></span>     | <span data-ttu-id="0e9cd-205">URI hello получен запрос.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-205">URI of hello received request.</span></span>        |
|<span data-ttu-id="0e9cd-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="0e9cd-206">RequestQuery</span></span>     | <span data-ttu-id="0e9cd-207">**Сервер маршрутизации**: экземпляр пула серверной части, отправленного запроса hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-207">**Server-Routed**: Back-end pool instance that was sent hello request.</span></span> </br> <span data-ttu-id="0e9cd-208">**X-AzureApplicationGateway-ЖУРНАЛА-ID**: идентификатор корреляции, используемый для запроса hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for hello request.</span></span> <span data-ttu-id="0e9cd-209">Это может быть используется tootroubleshoot проблемы трафика на внутренних серверах hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-209">It can be used tootroubleshoot traffic issues on hello back-end servers.</span></span> </br><span data-ttu-id="0e9cd-210">**Состояние сервера**: код ответа HTTP, полученные шлюз приложений от hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from hello back end.</span></span>       |
|<span data-ttu-id="0e9cd-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="0e9cd-211">UserAgent</span></span>     | <span data-ttu-id="0e9cd-212">Агент пользователя из заголовка запроса hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-212">User agent from hello HTTP request header.</span></span>        |
|<span data-ttu-id="0e9cd-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="0e9cd-213">httpStatus</span></span>     | <span data-ttu-id="0e9cd-214">Код состояния HTTP, возвращаемый клиента toohello шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-214">HTTP status code returned toohello client from Application Gateway.</span></span>       |
|<span data-ttu-id="0e9cd-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="0e9cd-215">httpVersion</span></span>     | <span data-ttu-id="0e9cd-216">Версия HTTP запроса hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-216">HTTP version of hello request.</span></span>        |
|<span data-ttu-id="0e9cd-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="0e9cd-217">receivedBytes</span></span>     | <span data-ttu-id="0e9cd-218">Размер полученного пакета (в байтах).</span><span class="sxs-lookup"><span data-stu-id="0e9cd-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="0e9cd-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="0e9cd-219">sentBytes</span></span>| <span data-ttu-id="0e9cd-220">Размер отправленного пакета (в байтах).</span><span class="sxs-lookup"><span data-stu-id="0e9cd-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="0e9cd-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="0e9cd-221">timeTaken</span></span>| <span data-ttu-id="0e9cd-222">Интервал времени (в миллисекундах), необходимое для запроса toobe обработки и его toobe ответа отправлены.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-222">Length of time (in milliseconds) that it takes for a request toobe processed and its response toobe sent.</span></span> <span data-ttu-id="0e9cd-223">Рассчитывается как интервал приветствия hello время, когда шлюз приложений получает первый байт hello HTTP время toohello запроса, когда ответ hello отправки по завершении операции.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-223">This is calculated as hello interval from hello time when Application Gateway receives hello first byte of an HTTP request toohello time when hello response send operation finishes.</span></span> <span data-ttu-id="0e9cd-224">Очень важно, что toonote, обычно hello поле затраченное время включает время hello приветственных пакетов запросов и ответов передаваемых по сети hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-224">It's important toonote that hello Time-Taken field usually includes hello time that hello request and response packets are traveling over hello network.</span></span> |
|<span data-ttu-id="0e9cd-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="0e9cd-225">sslEnabled</span></span>| <span data-ttu-id="0e9cd-226">Используется ли пулы внутренней связи toohello SSL.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-226">Whether communication toohello back-end pools used SSL.</span></span> <span data-ttu-id="0e9cd-227">Допустимые значения: on и off.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-227">Valid values are on and off.</span></span>|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a><span data-ttu-id="0e9cd-228">журнал производительности;</span><span class="sxs-lookup"><span data-stu-id="0e9cd-228">Performance log</span></span>

<span data-ttu-id="0e9cd-229">Журнал производительности Hello создается только в том случае, если она включена на каждом экземпляре шлюза приложения, как описано в предыдущих шагах hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-229">hello performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="0e9cd-230">Hello данные хранятся в учетной записи хранения hello, указанного при включении ведения журнала hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-230">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="0e9cd-231">данные журнала производительности Hello создается с интервалом в 1 минуту.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-231">hello performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="0e9cd-232">регистрируется Hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="0e9cd-232">hello following data is logged:</span></span>


|<span data-ttu-id="0e9cd-233">Значение</span><span class="sxs-lookup"><span data-stu-id="0e9cd-233">Value</span></span>  |<span data-ttu-id="0e9cd-234">Описание</span><span class="sxs-lookup"><span data-stu-id="0e9cd-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="0e9cd-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="0e9cd-235">instanceId</span></span>     |  <span data-ttu-id="0e9cd-236">Экземпляр шлюза приложений, для которого формируются данные о производительности.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="0e9cd-237">Если экземпляров шлюза приложений несколько, каждому экземпляру будет соответствовать определенная строка.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="0e9cd-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="0e9cd-238">healthyHostCount</span></span>     | <span data-ttu-id="0e9cd-239">Номер работоспособное узлов в пуле hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-239">Number of healthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="0e9cd-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="0e9cd-240">unHealthyHostCount</span></span>     | <span data-ttu-id="0e9cd-241">Номер неработоспособное узлов в пуле hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-241">Number of unhealthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="0e9cd-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="0e9cd-242">requestCount</span></span>     | <span data-ttu-id="0e9cd-243">Число обрабатываемых запросов.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-243">Number of requests served.</span></span>        |
|<span data-ttu-id="0e9cd-244">latency</span><span class="sxs-lookup"><span data-stu-id="0e9cd-244">latency</span></span> | <span data-ttu-id="0e9cd-245">Задержка (в миллисекундах) запросов от экземпляра toohello hello серверный компонент, выполняющий запросы hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-245">Latency (in milliseconds) of requests from hello instance toohello back end that serves hello requests.</span></span> |
|<span data-ttu-id="0e9cd-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="0e9cd-246">failedRequestCount</span></span>| <span data-ttu-id="0e9cd-247">Количество невыполненных запросов.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-247">Number of failed requests.</span></span>|
|<span data-ttu-id="0e9cd-248">throughput</span><span class="sxs-lookup"><span data-stu-id="0e9cd-248">throughput</span></span>| <span data-ttu-id="0e9cd-249">Средняя пропускная способность с момента последнего входа hello, измеряемое в байтах в секунду.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-249">Average throughput since hello last log, measured in bytes per second.</span></span>|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> <span data-ttu-id="0e9cd-250">Задержка вычисляется на основе hello время, когда первый байт hello hello HTTP-запрос получен toohello время отправки последнего байта hello hello HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-250">Latency is calculated from hello time when hello first byte of hello HTTP request is received toohello time when hello last byte of hello HTTP response is sent.</span></span> <span data-ttu-id="0e9cd-251">Его hello сумма hello шлюза приложения, время обработки, а также hello toohello стоимости сети обратно завершить, плюс время hello hello tooprocess hello серверной части принимает запрос.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-251">It's hello sum of hello Application Gateway processing time plus hello network cost toohello back end, plus hello time that hello back end takes tooprocess hello request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="0e9cd-252">журнал брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-252">Firewall log</span></span>

<span data-ttu-id="0e9cd-253">Журнал брандмауэра Hello создается только в том случае, если она включена для всех шлюзов, приложения, как описано в предыдущих шагах hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-253">hello firewall log is generated only if you have enabled it for each application gateway, as detailed in hello preceding steps.</span></span> <span data-ttu-id="0e9cd-254">Этот журнал также требует, что брандмауэр веб-приложения, hello настроен на использование шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-254">This log also requires that hello web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="0e9cd-255">Hello данные хранятся в учетной записи хранения hello, указанного при включении ведения журнала hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-255">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="0e9cd-256">регистрируется Hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="0e9cd-256">hello following data is logged:</span></span>


|<span data-ttu-id="0e9cd-257">Значение</span><span class="sxs-lookup"><span data-stu-id="0e9cd-257">Value</span></span>  |<span data-ttu-id="0e9cd-258">Описание</span><span class="sxs-lookup"><span data-stu-id="0e9cd-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="0e9cd-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="0e9cd-259">instanceId</span></span>     | <span data-ttu-id="0e9cd-260">Экземпляр шлюза приложений, для которого формируются данные о брандмауэре.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="0e9cd-261">Если экземпляров шлюза приложений несколько, каждому экземпляру будет соответствовать определенная строка.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="0e9cd-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="0e9cd-262">clientIp</span></span>     |   <span data-ttu-id="0e9cd-263">IP-адреса для запроса hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-263">Originating IP for hello request.</span></span>      |
|<span data-ttu-id="0e9cd-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="0e9cd-264">clientPort</span></span>     |  <span data-ttu-id="0e9cd-265">Исходный порт для запроса hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-265">Originating port for hello request.</span></span>       |
|<span data-ttu-id="0e9cd-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="0e9cd-266">requestUri</span></span>     | <span data-ttu-id="0e9cd-267">URL-адрес hello получила запрос.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-267">URL of hello received request.</span></span>       |
|<span data-ttu-id="0e9cd-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="0e9cd-268">ruleSetType</span></span>     | <span data-ttu-id="0e9cd-269">Тип набора правил.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-269">Rule set type.</span></span> <span data-ttu-id="0e9cd-270">доступное значение Hello — OWASP.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-270">hello available value is OWASP.</span></span>        |
|<span data-ttu-id="0e9cd-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="0e9cd-271">ruleSetVersion</span></span>     | <span data-ttu-id="0e9cd-272">Используемая версия набора правил.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-272">Rule set version used.</span></span> <span data-ttu-id="0e9cd-273">Возможные значения: 2.2.9 и 3.0.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="0e9cd-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="0e9cd-274">ruleId</span></span>     | <span data-ttu-id="0e9cd-275">Код правила hello инициации события.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-275">Rule ID of hello triggering event.</span></span>        |
|<span data-ttu-id="0e9cd-276">Message</span><span class="sxs-lookup"><span data-stu-id="0e9cd-276">message</span></span>     | <span data-ttu-id="0e9cd-277">Понятное сообщение hello инициации события.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-277">User-friendly message for hello triggering event.</span></span> <span data-ttu-id="0e9cd-278">Дополнительные сведения приведены в разделе "Сведения" hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-278">More details are provided in hello details section.</span></span>        |
|<span data-ttu-id="0e9cd-279">action</span><span class="sxs-lookup"><span data-stu-id="0e9cd-279">action</span></span>     |  <span data-ttu-id="0e9cd-280">Действие, выполняемое при запросе hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-280">Action taken on hello request.</span></span> <span data-ttu-id="0e9cd-281">Возможные значения: Blocked и Allowed.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="0e9cd-282">site</span><span class="sxs-lookup"><span data-stu-id="0e9cd-282">site</span></span>     | <span data-ttu-id="0e9cd-283">Сайт, для которого hello журнала была создана.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-283">Site for which hello log was generated.</span></span> <span data-ttu-id="0e9cd-284">В нашем случае возможно только значение Global, так как применяются глобальные правила.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="0e9cd-285">сведения</span><span class="sxs-lookup"><span data-stu-id="0e9cd-285">details</span></span>     | <span data-ttu-id="0e9cd-286">Сведения об активации события hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-286">Details of hello triggering event.</span></span>        |
|<span data-ttu-id="0e9cd-287">details.message</span><span class="sxs-lookup"><span data-stu-id="0e9cd-287">details.message</span></span>     | <span data-ttu-id="0e9cd-288">Описание правила hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-288">Description of hello rule.</span></span>        |
|<span data-ttu-id="0e9cd-289">details.data</span><span class="sxs-lookup"><span data-stu-id="0e9cd-289">details.data</span></span>     | <span data-ttu-id="0e9cd-290">В запросе данных найдены правила соответствия hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-290">Specific data found in request that matched hello rule.</span></span>         |
|<span data-ttu-id="0e9cd-291">details.file</span><span class="sxs-lookup"><span data-stu-id="0e9cd-291">details.file</span></span>     | <span data-ttu-id="0e9cd-292">Файл конфигурации, содержащий правило hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-292">Configuration file that contained hello rule.</span></span>        |
|<span data-ttu-id="0e9cd-293">details.line</span><span class="sxs-lookup"><span data-stu-id="0e9cd-293">details.line</span></span>     | <span data-ttu-id="0e9cd-294">Номер строки в файле конфигурации hello, вызвавшей событие hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-294">Line number in hello configuration file that triggered hello event.</span></span>       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a><span data-ttu-id="0e9cd-295">Просмотр и анализ журнала активности hello</span><span class="sxs-lookup"><span data-stu-id="0e9cd-295">View and analyze hello activity log</span></span>

<span data-ttu-id="0e9cd-296">Можно просматривать и анализировать данные журнала действий с помощью любого из следующих методов hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-296">You can view and analyze activity log data by using any of hello following methods:</span></span>

* <span data-ttu-id="0e9cd-297">**Инструменты Azure**: получать сведения из журнала активности hello через Azure PowerShell, hello Azure CLI, hello Azure REST API или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-297">**Azure tools**: Retrieve information from hello activity log through Azure PowerShell, hello Azure CLI, hello Azure REST API, or hello Azure portal.</span></span> <span data-ttu-id="0e9cd-298">Пошаговые инструкции для каждого метода описаны в hello [действия операции с помощью диспетчера ресурсов](../azure-resource-manager/resource-group-audit.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-298">Step-by-step instructions for each method are detailed in hello [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="0e9cd-299">**Power BI.** Если у вас еще нет учетной записи [Power BI](https://powerbi.microsoft.com/pricing), вы можете использовать бесплатную пробную версию.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="0e9cd-300">С помощью hello [журналы действий Azure пакет содержимого для Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), можно анализировать данные с помощью предварительно настроенных панелей мониторинга, которые можно использовать как есть или настроить.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-300">By using hello [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a><span data-ttu-id="0e9cd-301">Просмотр и анализ hello доступ, производительность и журналы брандмауэра</span><span class="sxs-lookup"><span data-stu-id="0e9cd-301">View and analyze hello access, performance, and firewall logs</span></span>

<span data-ttu-id="0e9cd-302">Azure [анализа журналов](../log-analytics/log-analytics-azure-networking-analytics.md) можно собирать hello счетчика и событие файлы журнала из вашей учетной записи хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect hello counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="0e9cd-303">Он включает визуализации и возможности tooanalyze мощное средство поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-303">It includes visualizations and powerful search capabilities tooanalyze your logs.</span></span>

<span data-ttu-id="0e9cd-304">Можно также подключиться tooyour учетной записи хранения и получения записей журнала hello JSON для доступа и производительности журналов.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-304">You can also connect tooyour storage account and retrieve hello JSON log entries for access and performance logs.</span></span> <span data-ttu-id="0e9cd-305">После загрузки файлов hello JSON можно преобразовать tooCSV и просматривать их в Excel, Power BI или любом другом средстве визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-305">After you download hello JSON files, you can convert them tooCSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="0e9cd-306">Если вы знакомы с Visual Studio и основные понятия, связанные изменения значений константы и переменные в C#, можно использовать hello [входа преобразователь средства](https://github.com/Azure-Samples/networking-dotnet-log-converter) GitHub доступны.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="0e9cd-307">Метрики</span><span class="sxs-lookup"><span data-stu-id="0e9cd-307">Metrics</span></span>

<span data-ttu-id="0e9cd-308">Метрики поддерживаются только для определенных ресурсов Azure, где можно просмотреть счетчики производительности в портале hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-308">Metrics are a feature for certain Azure resources where you can view performance counters in hello portal.</span></span> <span data-ttu-id="0e9cd-309">Сейчас для шлюза приложений доступна одна метрика.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="0e9cd-310">Эта метрика пропускной способности, и вы увидите это на портале hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-310">This metric is throughput, and you can see it in hello portal.</span></span> <span data-ttu-id="0e9cd-311">Обзор шлюза tooan приложения и нажмите кнопку **метрики**.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-311">Browse tooan application gateway and click **Metrics**.</span></span> <span data-ttu-id="0e9cd-312">значения tooview hello, выберите пропускную способность в hello **доступные метрики** раздела.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-312">tooview hello values, select throughput in hello **Available metrics** section.</span></span> <span data-ttu-id="0e9cd-313">Hello после изображения вы увидите пример с фильтрами hello, toodisplay hello данных можно использовать в различных временных интервалов.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-313">In hello following image, you can see an example with hello filters that you can use toodisplay hello data in different time ranges.</span></span>

![Представление метрик с фильтрами][5]

<span data-ttu-id="0e9cd-315">toosee текущий список метрик, в разделе [поддерживаемых метрик с помощью монитора Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0e9cd-315">toosee a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="0e9cd-316">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="0e9cd-316">Alert rules</span></span>

<span data-ttu-id="0e9cd-317">Вы можете запустить правила генерации оповещений на основе метрик для ресурса.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="0e9cd-318">Например предупреждение можно вызвать веб-перехватчик или электронной почты администратора, если пропускная способность шлюза приложения hello hello выше, ниже или в порогового значения за указанный период.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-318">For example, an alert can call a webhook or email an administrator if hello throughput of hello application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="0e9cd-319">Следующий пример Hello описывается создание правила оповещения, отправляющий администратор tooan электронной почты после нарушений пропускной способности a пороговое значение:</span><span class="sxs-lookup"><span data-stu-id="0e9cd-319">hello following example walks you through creating an alert rule that sends an email tooan administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="0e9cd-320">Нажмите кнопку **добавить оповещение метрики** tooopen hello **добавить правило** колонку.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-320">Click **Add metric alert** tooopen hello **Add rule** blade.</span></span> <span data-ttu-id="0e9cd-321">Можно также получить доступ из колонки метрики hello эту колонку.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-321">You can also reach this blade from hello metrics blade.</span></span>

   ![Кнопка "Добавить оповещение метрики"][6]

2. <span data-ttu-id="0e9cd-323">На hello **добавить правило** колонки, введите имя hello, условие и уведомить разделы и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-323">On hello **Add rule** blade, fill out hello name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="0e9cd-324">В hello **условие** селектора, выберите одно из значений hello четырех: **больше**, **больше или равно**, **меньше, чем**, или  **Меньше или равно**.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-324">In hello **Condition** selector, select one of hello four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="0e9cd-325">В hello **период** селектора, выберите период в 5 минут too6 часов.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-325">In hello **Period** selector, select a period from 5 minutes too6 hours.</span></span>

   * <span data-ttu-id="0e9cd-326">При выборе **электронной почты, владельцы, участники и читатели**, hello электронной почты может быть динамическим основании hello пользователям, имеющим доступ toothat ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-326">If you select **Email owners, contributors, and readers**, hello email can be dynamic based on hello users who have access toothat resource.</span></span> <span data-ttu-id="0e9cd-327">В противном случае можно указать список разделенных запятыми пользователей в hello **email(s) дополнительного администратора** поле.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-327">Otherwise, you can provide a comma-separated list of users in hello **Additional administrator email(s)** box.</span></span>

   ![Колонка "Добавление правила"][7]

<span data-ttu-id="0e9cd-329">Если пороговое значение hello, нарушена, прибывает сообщение электронной почты, аналогичные toohello один в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="0e9cd-329">If hello threshold is breached, an email that's similar toohello one in hello following image arrives:</span></span>

![Сообщение электронной почты о нарушении порога][8]

<span data-ttu-id="0e9cd-331">После создания оповещения метрики появится список оповещений.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="0e9cd-332">Он предоставляет общие сведения о всех правил генерации оповещений hello.</span><span class="sxs-lookup"><span data-stu-id="0e9cd-332">It provides an overview of all hello alert rules.</span></span>

![Список оповещений и правил][9]

<span data-ttu-id="0e9cd-334">. в разделе toolearn более уведомлений об предупреждениях, [получать уведомления об оповещениях](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0e9cd-334">toolearn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="0e9cd-335">Посетите toounderstand Дополнительные сведения о веб-привязок и их использовании с оповещениями, [настроить веб-перехватчика на оповещение Azure метрики](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="0e9cd-335">toounderstand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e9cd-336">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0e9cd-336">Next steps</span></span>

* <span data-ttu-id="0e9cd-337">См. сведения о визуализации журналов счетчиков и событий с помощью [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="0e9cd-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="0e9cd-338">Прочтите запись блога [Visualize your Azure Activity Log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Визуализация журналов действий Azure с помощью Power BI).</span><span class="sxs-lookup"><span data-stu-id="0e9cd-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="0e9cd-339">Прочтите запись блога [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Просмотр и анализ журналов аудита Azure с помощью Power BI и других средств).</span><span class="sxs-lookup"><span data-stu-id="0e9cd-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
