---
title: "Мониторинг журналов доступа, журналов производительности, работоспособности серверной части и метрик для шлюза приложений | Документация Майкрософт"
description: "Узнайте, как включить журналы доступа и производительности для шлюза приложений и управлять ими."
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
ms.openlocfilehash: 12c252340b82aba5ee69b12db83353750782e7c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="0225b-103">Работоспособность серверной части, журналы диагностики и метрики для шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="0225b-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="0225b-104">С помощью шлюза приложений Azure можно отслеживать ресурсы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0225b-104">By using Azure Application Gateway, you can monitor resources in the following ways:</span></span>

* <span data-ttu-id="0225b-105">[Работоспособность серверной части.](#back-end-health) Шлюз приложений позволяет отслеживать работоспособность серверов во внутренних пулах с помощью портала Azure и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0225b-105">[Back-end health](#back-end-health): Application Gateway provides the capability to monitor the health of the servers in the back-end pools through the Azure portal and through PowerShell.</span></span> <span data-ttu-id="0225b-106">Состояние работоспособности внутренних пулов можно также узнать из журналов диагностики производительности.</span><span class="sxs-lookup"><span data-stu-id="0225b-106">You can also find the health of the back-end pools through the performance diagnostic logs.</span></span>

* <span data-ttu-id="0225b-107">[Журналы.](#diagnostic-logs) Можно сохранять или использовать данные производительности, доступа и другие данные, относящиеся к ресурсу, чтобы отслеживать его состояние.</span><span class="sxs-lookup"><span data-stu-id="0225b-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data to be saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="0225b-108">[Метрики.](#metrics) Сейчас в шлюзе приложений используется одна метрика.</span><span class="sxs-lookup"><span data-stu-id="0225b-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="0225b-109">Она позволяет измерить пропускную способность шлюза приложений в байтах в секунду.</span><span class="sxs-lookup"><span data-stu-id="0225b-109">This metric measures the throughput of the application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="0225b-110">Работоспособность серверной части</span><span class="sxs-lookup"><span data-stu-id="0225b-110">Back-end health</span></span>

<span data-ttu-id="0225b-111">Шлюз приложений позволяет отслеживать работоспособность отдельных участников внутренних пулов с помощью портала, PowerShell и интерфейса командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="0225b-111">Application Gateway provides the capability to monitor the health of individual members of the back-end pools through the portal, PowerShell, and the command-line interface (CLI).</span></span> <span data-ttu-id="0225b-112">Сводные данные работоспособности внутренних пулов можно также найти в журналах диагностики производительности.</span><span class="sxs-lookup"><span data-stu-id="0225b-112">You can also find an aggregated health summary of back-end pools through the performance diagnostic logs.</span></span> 

<span data-ttu-id="0225b-113">В отчете о работоспособности серверной части представлены результаты пробы работоспособности, выполняемой шлюзом приложений в отношении серверных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="0225b-113">The back-end health report reflects the output of the Application Gateway health probe to the back-end instances.</span></span> <span data-ttu-id="0225b-114">Если проба прошла успешно и серверная часть может получать трафик, она считается работоспособной.</span><span class="sxs-lookup"><span data-stu-id="0225b-114">When probing is successful and the back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="0225b-115">В противном случае серверная часть считается неработоспособной.</span><span class="sxs-lookup"><span data-stu-id="0225b-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0225b-116">Если в подсети шлюза приложений есть группа безопасности сети (NSG), то в этой подсети необходимо открыть диапазон портов 65503–65534 для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="0225b-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on the Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="0225b-117">Эти порты требуются для работы API работоспособности серверной части.</span><span class="sxs-lookup"><span data-stu-id="0225b-117">These ports are required for the back-end health API to work.</span></span>


### <a name="view-back-end-health-through-the-portal"></a><span data-ttu-id="0225b-118">Просмотр данных о работоспособности серверной части на портале</span><span class="sxs-lookup"><span data-stu-id="0225b-118">View back-end health through the portal</span></span>

<span data-ttu-id="0225b-119">На портале данные о работоспособности серверной части предоставляются автоматически.</span><span class="sxs-lookup"><span data-stu-id="0225b-119">In the portal, back-end health is provided automatically.</span></span> <span data-ttu-id="0225b-120">В существующем шлюзе приложений выберите **Мониторинг** > **Оценка работоспособности серверной части**.</span><span class="sxs-lookup"><span data-stu-id="0225b-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="0225b-121">На этой странице отображается каждый участник внутреннего пула (сетевой адаптер, IP-адрес или полное доменное имя).</span><span class="sxs-lookup"><span data-stu-id="0225b-121">Each member in the back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="0225b-122">На ней показаны имя внутреннего пула, порт, параметры HTTP внутреннего пула и его состояние работоспособности.</span><span class="sxs-lookup"><span data-stu-id="0225b-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="0225b-123">Допустимые значения состояния работоспособности: **Работоспособен**, **Неработоспособен** и **Неизвестно**.</span><span class="sxs-lookup"><span data-stu-id="0225b-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="0225b-124">Если отображается состояние работоспособности серверной части **Неизвестно**, убедитесь, что доступ к серверной части не заблокирован правилом NSG, маршрутом, определенным пользователем или пользовательской службой DNS в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0225b-124">If you see a back-end health status of **Unknown**, ensure that access to the back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in the virtual network.</span></span>

![Работоспособность серверной части][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="0225b-126">Просмотр данных о работоспособности серверной части с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0225b-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="0225b-127">В приведенном ниже коде PowerShell показано, как просмотреть данные о работоспособности серверной части с помощью командлета `Get-AzureRmApplicationGatewayBackendHealth`.</span><span class="sxs-lookup"><span data-stu-id="0225b-127">The following PowerShell code shows how to view back-end health by using the `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="0225b-128">Просмотр данных о работоспособности серверной части с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0225b-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="0225b-129">Результаты</span><span class="sxs-lookup"><span data-stu-id="0225b-129">Results</span></span>

<span data-ttu-id="0225b-130">В следующем фрагменте кода приведен пример отклика:</span><span class="sxs-lookup"><span data-stu-id="0225b-130">The following snippet shows an example of the response:</span></span>

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

## <span data-ttu-id="0225b-131"><a name="diagnostic-logging"></a>Журналы диагностики</span><span class="sxs-lookup"><span data-stu-id="0225b-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="0225b-132">В Azure можно использовать различные виды журналов для управления шлюзами приложений и устранения возникающих в них неполадок.</span><span class="sxs-lookup"><span data-stu-id="0225b-132">You can use different types of logs in Azure to manage and troubleshoot application gateways.</span></span> <span data-ttu-id="0225b-133">Доступ к некоторым из этих журналов можно получить через портал.</span><span class="sxs-lookup"><span data-stu-id="0225b-133">You can access some of these logs through the portal.</span></span> <span data-ttu-id="0225b-134">Также можно извлечь все журналы из хранилища BLOB-объектов Azure и просматривать их с помощью таких средств, как [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel и Power BI.</span><span class="sxs-lookup"><span data-stu-id="0225b-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="0225b-135">В списке ниже приведены дополнительные сведения о разных типах журналов.</span><span class="sxs-lookup"><span data-stu-id="0225b-135">You can learn more about the different types of logs from the following list:</span></span>

* <span data-ttu-id="0225b-136">**Журнал действий.** В [журналах действий Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (прежнее название — операционные журналы и журналы аудита) можно просматривать все операции, отправляемые в вашу подписку Azure, и состояние этих операций.</span><span class="sxs-lookup"><span data-stu-id="0225b-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) to view all operations that are submitted to your Azure subscription, and their status.</span></span> <span data-ttu-id="0225b-137">Записи этого журнала собираются по умолчанию, и их можно просмотреть на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0225b-137">Activity log entries are collected by default, and you can view them in the Azure portal.</span></span>
* <span data-ttu-id="0225b-138">**Журнал доступа.** С помощью этого журнала можно просматривать шаблоны доступа шлюза приложений и анализировать важную информацию, включая IP-адрес вызывающей стороны, запрошенный URL-адрес, сведения о задержке отклика, возвращаемом коде и переданных и полученных байтах. Данные для журнала доступа собираются каждые 300 секунд.</span><span class="sxs-lookup"><span data-stu-id="0225b-138">**Access log**: You can use this log to view Application Gateway access patterns and analyze important information, including the caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="0225b-139">Этот журнал содержит одну запись для каждого экземпляра шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="0225b-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="0225b-140">Экземпляр шлюза приложений определяется свойством instanceId.</span><span class="sxs-lookup"><span data-stu-id="0225b-140">The Application Gateway instance can be identified by the instanceId property.</span></span>
* <span data-ttu-id="0225b-141">**Журнал производительности.** С помощью этого журнала можно просматривать, как работают экземпляры шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="0225b-141">**Performance log**: You can use this log to view how Application Gateway instances are performing.</span></span> <span data-ttu-id="0225b-142">В этот журнал записываются сведения о производительности каждого экземпляра, включая общее число обработанных запросов, пропускную способность в байтах, число неудачных запросов, а также число работоспособных и неработоспособных серверных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="0225b-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="0225b-143">Данные для журнала производительности собираются каждые 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="0225b-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="0225b-144">**Журнал брандмауэра.** Этот журнал можно использовать для просмотра запросов, которые были зарегистрированы в режиме обнаружения или предотвращения в шлюзе приложений, в котором настроен брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0225b-144">**Firewall log**: You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with the web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="0225b-145">Журналы доступны только для ресурсов, развернутых в модели развертывания с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0225b-145">Logs are available only for resources deployed in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="0225b-146">Журналы нельзя использовать для ресурсов в классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="0225b-146">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="0225b-147">Чтобы получить более полное представление об этих двух моделях, см. статью [Развертывание с помощью Azure Resource Manager и классическое развертывание: сведения о моделях развертывания и состоянии ресурсов](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0225b-147">For a better understanding of the two models, see the [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="0225b-148">Существует три способа хранения журналов:</span><span class="sxs-lookup"><span data-stu-id="0225b-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="0225b-149">**Учетная запись хранения** лучше всего подходит для длительного хранения журналов и их просмотра по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="0225b-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="0225b-150">**Концентраторы событий** — это отличный вариант для интеграции с другими инструментами управления событиями и сведениями о безопасности (SEIM), позволяющий получать оповещения о ваших ресурсах.</span><span class="sxs-lookup"><span data-stu-id="0225b-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools to get alerts on your resources.</span></span>
* <span data-ttu-id="0225b-151">**Log Analytics** лучше всего подходит для общего мониторинга приложения в реальном времени и изучения тенденций.</span><span class="sxs-lookup"><span data-stu-id="0225b-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="0225b-152">Включение ведения журнала с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0225b-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="0225b-153">Ведение журнала действий автоматически включается для каждого ресурса Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0225b-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="0225b-154">Нужно включить ведение журналов доступа и производительности, чтобы начать сбор связанных данных.</span><span class="sxs-lookup"><span data-stu-id="0225b-154">You must enable access and performance logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="0225b-155">Вот как можно включить ведение журнала:</span><span class="sxs-lookup"><span data-stu-id="0225b-155">To enable logging, use the following steps:</span></span>

1. <span data-ttu-id="0225b-156">Запишите или запомните ИД ресурса учетной записи хранения, где хранятся данные журнала,</span><span class="sxs-lookup"><span data-stu-id="0225b-156">Note your storage account's resource ID, where the log data is stored.</span></span> <span data-ttu-id="0225b-157">в формате: /subscriptions/\<идентификатор_подписки\>/resourceGroups/\<имя_группы_ресурсов\>/providers/Microsoft.Storage/storageAccounts/\<имя_учетной_записи_хранения\>.</span><span class="sxs-lookup"><span data-stu-id="0225b-157">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="0225b-158">Можно использовать любую учетную запись хранения в подписке.</span><span class="sxs-lookup"><span data-stu-id="0225b-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="0225b-159">Получить эти сведения можно на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0225b-159">You can use the Azure portal to find this information.</span></span>

    ![ИД ресурса для учетной записи хранения на портале](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="0225b-161">Запишите или запомните идентификатор ресурса шлюза приложений, для которого нужно включить ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="0225b-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="0225b-162">в формате: /subscriptions/\<идентификатор_подписки\>/resourceGroups/\<имя_группы_ресурсов\>/providers/Microsoft.Network/applicationGateways/\<имя_шлюза_приложений\>.</span><span class="sxs-lookup"><span data-stu-id="0225b-162">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="0225b-163">Получить эти сведения можно на портале.</span><span class="sxs-lookup"><span data-stu-id="0225b-163">You can use the portal to find this information.</span></span>

    ![ИД ресурса для шлюза приложений на портале](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="0225b-165">Включите ведение журнала диагностики с помощью следующего командлета PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0225b-165">Enable diagnostic logging by using the following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="0225b-166">Для журналов действий отдельная учетная запись хранения не требуется.</span><span class="sxs-lookup"><span data-stu-id="0225b-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="0225b-167">За использование хранилища для журналов доступа и производительности взимается плата.</span><span class="sxs-lookup"><span data-stu-id="0225b-167">The use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-the-azure-portal"></a><span data-ttu-id="0225b-168">Включение ведения журнала на портале Azure</span><span class="sxs-lookup"><span data-stu-id="0225b-168">Enable logging through the Azure portal</span></span>

1. <span data-ttu-id="0225b-169">На портале Azure найдите нужный ресурс и щелкните **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="0225b-169">In the Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="0225b-170">Для шлюза приложений доступны три журнала:</span><span class="sxs-lookup"><span data-stu-id="0225b-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="0225b-171">журнал доступа;</span><span class="sxs-lookup"><span data-stu-id="0225b-171">Access log</span></span>
   * <span data-ttu-id="0225b-172">журнал производительности;</span><span class="sxs-lookup"><span data-stu-id="0225b-172">Performance log</span></span>
   * <span data-ttu-id="0225b-173">журнал брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="0225b-173">Firewall log</span></span>

2. <span data-ttu-id="0225b-174">Щелкните **Включить диагностику**, чтобы начать сбор данных.</span><span class="sxs-lookup"><span data-stu-id="0225b-174">To start collecting data, click **Turn on diagnostics**.</span></span>

   ![Включение диагностики][1]

3. <span data-ttu-id="0225b-176">В колонке **Параметры диагностики** представлены параметры журналов диагностики.</span><span class="sxs-lookup"><span data-stu-id="0225b-176">The **Diagnostics settings** blade provides the settings for the diagnostic logs.</span></span> <span data-ttu-id="0225b-177">В этом примере для хранения журналов используется Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0225b-177">In this example, Log Analytics stores the logs.</span></span> <span data-ttu-id="0225b-178">Щелкните **Настройка** в разделе **Log Analytics**, чтобы настроить рабочую область.</span><span class="sxs-lookup"><span data-stu-id="0225b-178">Click **Configure** under **Log Analytics** to configure your workspace.</span></span> <span data-ttu-id="0225b-179">Для хранения журналов диагностики можно также использовать концентраторы событий и учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="0225b-179">You can also use event hubs and a storage account to save the diagnostic logs.</span></span>

   ![Начало процесса настройки][2]

4. <span data-ttu-id="0225b-181">Выберите существующую рабочую область Operations Management Suite (OMS) или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="0225b-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="0225b-182">В этом примере используется существующая рабочая область.</span><span class="sxs-lookup"><span data-stu-id="0225b-182">This example uses an existing one.</span></span>

   ![Параметры для рабочих областей OMS][3]

5. <span data-ttu-id="0225b-184">Проверьте параметры и щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0225b-184">Confirm the settings and click **Save**.</span></span>

   ![Колонка "Параметры диагностики" с выбранными значениями][4]

### <a name="activity-log"></a><span data-ttu-id="0225b-186">Журнал действий</span><span class="sxs-lookup"><span data-stu-id="0225b-186">Activity log</span></span>

<span data-ttu-id="0225b-187">На портале Azure журнал действий создается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0225b-187">Azure generates the activity log by default.</span></span> <span data-ttu-id="0225b-188">Журналы хранятся в течение 90 дней в хранилище журналов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="0225b-188">The logs are preserved for 90 days in the Azure event logs store.</span></span> <span data-ttu-id="0225b-189">Дополнительные сведения об этих журналах см. в статье [Просмотр журналов действий для аудита действий с ресурсами](../monitoring-and-diagnostics/insights-debugging-with-events.md).</span><span class="sxs-lookup"><span data-stu-id="0225b-189">Learn more about these logs by reading the [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="0225b-190">журнал доступа;</span><span class="sxs-lookup"><span data-stu-id="0225b-190">Access log</span></span>

<span data-ttu-id="0225b-191">Журнал доступа создается, только если он включен для каждого экземпляра шлюза приложений, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="0225b-191">The access log is generated only if you've enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="0225b-192">Данные хранятся в учетной записи хранения, указанной при включении ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="0225b-192">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="0225b-193">Каждая операция доступа шлюза приложений регистрируется в журнале в формате JSON, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="0225b-193">Each access of Application Gateway is logged in JSON format, as shown in the following example:</span></span>


|<span data-ttu-id="0225b-194">Значение</span><span class="sxs-lookup"><span data-stu-id="0225b-194">Value</span></span>  |<span data-ttu-id="0225b-195">Описание</span><span class="sxs-lookup"><span data-stu-id="0225b-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="0225b-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="0225b-196">instanceId</span></span>     | <span data-ttu-id="0225b-197">Экземпляр шлюза приложений, который обрабатывает запрос.</span><span class="sxs-lookup"><span data-stu-id="0225b-197">Application Gateway instance that served the request.</span></span>        |
|<span data-ttu-id="0225b-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="0225b-198">clientIP</span></span>     | <span data-ttu-id="0225b-199">IP-адрес источника запроса.</span><span class="sxs-lookup"><span data-stu-id="0225b-199">Originating IP for the request.</span></span>        |
|<span data-ttu-id="0225b-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="0225b-200">clientPort</span></span>     | <span data-ttu-id="0225b-201">Порт источника запроса.</span><span class="sxs-lookup"><span data-stu-id="0225b-201">Originating port for the request.</span></span>       |
|<span data-ttu-id="0225b-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="0225b-202">httpMethod</span></span>     | <span data-ttu-id="0225b-203">Метод HTTP, используемый для запроса.</span><span class="sxs-lookup"><span data-stu-id="0225b-203">HTTP method used by the request.</span></span>       |
|<span data-ttu-id="0225b-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="0225b-204">requestUri</span></span>     | <span data-ttu-id="0225b-205">URI полученного запроса.</span><span class="sxs-lookup"><span data-stu-id="0225b-205">URI of the received request.</span></span>        |
|<span data-ttu-id="0225b-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="0225b-206">RequestQuery</span></span>     | <span data-ttu-id="0225b-207">**Server-Routed** — экземпляр внутреннего пула, из которого отправлен запрос.</span><span class="sxs-lookup"><span data-stu-id="0225b-207">**Server-Routed**: Back-end pool instance that was sent the request.</span></span> </br> <span data-ttu-id="0225b-208">**X-AzureApplicationGateway-LOG-ID** — идентификатор корреляции, используемый для запроса.</span><span class="sxs-lookup"><span data-stu-id="0225b-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for the request.</span></span> <span data-ttu-id="0225b-209">Он может использоваться для устранения неполадок с трафиком на внутренних серверах.</span><span class="sxs-lookup"><span data-stu-id="0225b-209">It can be used to troubleshoot traffic issues on the back-end servers.</span></span> </br><span data-ttu-id="0225b-210">**SERVER-STATUS** — код отклика HTTP, полученный шлюзом приложений из серверной части.</span><span class="sxs-lookup"><span data-stu-id="0225b-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from the back end.</span></span>       |
|<span data-ttu-id="0225b-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="0225b-211">UserAgent</span></span>     | <span data-ttu-id="0225b-212">Агент пользователя из заголовка HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="0225b-212">User agent from the HTTP request header.</span></span>        |
|<span data-ttu-id="0225b-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="0225b-213">httpStatus</span></span>     | <span data-ttu-id="0225b-214">Код состояния HTTP, возвращаемый клиенту из шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="0225b-214">HTTP status code returned to the client from Application Gateway.</span></span>       |
|<span data-ttu-id="0225b-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="0225b-215">httpVersion</span></span>     | <span data-ttu-id="0225b-216">Версия HTTP для запроса.</span><span class="sxs-lookup"><span data-stu-id="0225b-216">HTTP version of the request.</span></span>        |
|<span data-ttu-id="0225b-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="0225b-217">receivedBytes</span></span>     | <span data-ttu-id="0225b-218">Размер полученного пакета (в байтах).</span><span class="sxs-lookup"><span data-stu-id="0225b-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="0225b-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="0225b-219">sentBytes</span></span>| <span data-ttu-id="0225b-220">Размер отправленного пакета (в байтах).</span><span class="sxs-lookup"><span data-stu-id="0225b-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="0225b-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="0225b-221">timeTaken</span></span>| <span data-ttu-id="0225b-222">Время (в миллисекундах), необходимое для обработки запроса и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="0225b-222">Length of time (in milliseconds) that it takes for a request to be processed and its response to be sent.</span></span> <span data-ttu-id="0225b-223">Вычисляется как промежуток времени от момента, когда шлюз приложений получает первый байт HTTP-запроса, до завершения отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="0225b-223">This is calculated as the interval from the time when Application Gateway receives the first byte of an HTTP request to the time when the response send operation finishes.</span></span> <span data-ttu-id="0225b-224">Важно отметить, что в поле Time-Taken обычно указывается время передачи пакетов запросов и ответов по сети.</span><span class="sxs-lookup"><span data-stu-id="0225b-224">It's important to note that the Time-Taken field usually includes the time that the request and response packets are traveling over the network.</span></span> |
|<span data-ttu-id="0225b-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="0225b-225">sslEnabled</span></span>| <span data-ttu-id="0225b-226">Определяет, используется ли SSL для обмена данными с внутренними пулами.</span><span class="sxs-lookup"><span data-stu-id="0225b-226">Whether communication to the back-end pools used SSL.</span></span> <span data-ttu-id="0225b-227">Допустимые значения: on и off.</span><span class="sxs-lookup"><span data-stu-id="0225b-227">Valid values are on and off.</span></span>|
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

### <a name="performance-log"></a><span data-ttu-id="0225b-228">журнал производительности;</span><span class="sxs-lookup"><span data-stu-id="0225b-228">Performance log</span></span>

<span data-ttu-id="0225b-229">Журнал производительности создается, только если он включен для каждого экземпляра шлюза приложений, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="0225b-229">The performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="0225b-230">Данные хранятся в учетной записи хранения, указанной при включении ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="0225b-230">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="0225b-231">Данные журнала производительности формируются с интервалом в 1 минуту.</span><span class="sxs-lookup"><span data-stu-id="0225b-231">The performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="0225b-232">В журнал записываются следующие данные:</span><span class="sxs-lookup"><span data-stu-id="0225b-232">The following data is logged:</span></span>


|<span data-ttu-id="0225b-233">Значение</span><span class="sxs-lookup"><span data-stu-id="0225b-233">Value</span></span>  |<span data-ttu-id="0225b-234">Описание</span><span class="sxs-lookup"><span data-stu-id="0225b-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="0225b-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="0225b-235">instanceId</span></span>     |  <span data-ttu-id="0225b-236">Экземпляр шлюза приложений, для которого формируются данные о производительности.</span><span class="sxs-lookup"><span data-stu-id="0225b-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="0225b-237">Если экземпляров шлюза приложений несколько, каждому экземпляру будет соответствовать определенная строка.</span><span class="sxs-lookup"><span data-stu-id="0225b-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="0225b-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="0225b-238">healthyHostCount</span></span>     | <span data-ttu-id="0225b-239">Число работоспособных узлов во внутреннем пуле.</span><span class="sxs-lookup"><span data-stu-id="0225b-239">Number of healthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="0225b-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="0225b-240">unHealthyHostCount</span></span>     | <span data-ttu-id="0225b-241">Число неработоспособных узлов во внутреннем пуле.</span><span class="sxs-lookup"><span data-stu-id="0225b-241">Number of unhealthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="0225b-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="0225b-242">requestCount</span></span>     | <span data-ttu-id="0225b-243">Число обрабатываемых запросов.</span><span class="sxs-lookup"><span data-stu-id="0225b-243">Number of requests served.</span></span>        |
|<span data-ttu-id="0225b-244">latency</span><span class="sxs-lookup"><span data-stu-id="0225b-244">latency</span></span> | <span data-ttu-id="0225b-245">Задержка (в миллисекундах) запросов от экземпляра к серверной части, обрабатывающей запросы.</span><span class="sxs-lookup"><span data-stu-id="0225b-245">Latency (in milliseconds) of requests from the instance to the back end that serves the requests.</span></span> |
|<span data-ttu-id="0225b-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="0225b-246">failedRequestCount</span></span>| <span data-ttu-id="0225b-247">Количество невыполненных запросов.</span><span class="sxs-lookup"><span data-stu-id="0225b-247">Number of failed requests.</span></span>|
|<span data-ttu-id="0225b-248">throughput</span><span class="sxs-lookup"><span data-stu-id="0225b-248">throughput</span></span>| <span data-ttu-id="0225b-249">Средняя пропускная способность (в байтах в секунду) с момента создания последнего журнала.</span><span class="sxs-lookup"><span data-stu-id="0225b-249">Average throughput since the last log, measured in bytes per second.</span></span>|

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
> <span data-ttu-id="0225b-250">Задержка вычисляется от момента получения первого байта HTTP-запроса до момента отправки последнего байта HTTP-отклика.</span><span class="sxs-lookup"><span data-stu-id="0225b-250">Latency is calculated from the time when the first byte of the HTTP request is received to the time when the last byte of the HTTP response is sent.</span></span> <span data-ttu-id="0225b-251">Это сумма времени обработки шлюза приложений, времени передачи по сети к серверной части, а также времени, необходимого для обработки запроса в серверной части.</span><span class="sxs-lookup"><span data-stu-id="0225b-251">It's the sum of the Application Gateway processing time plus the network cost to the back end, plus the time that the back end takes to process the request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="0225b-252">журнал брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="0225b-252">Firewall log</span></span>

<span data-ttu-id="0225b-253">Этот журнал создается, только если он включен для каждого шлюза приложений, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="0225b-253">The firewall log is generated only if you have enabled it for each application gateway, as detailed in the preceding steps.</span></span> <span data-ttu-id="0225b-254">Кроме того, в шлюзе приложений должен быть настроен брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0225b-254">This log also requires that the web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="0225b-255">Данные хранятся в учетной записи хранения, указанной при включении ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="0225b-255">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="0225b-256">В журнал записываются следующие данные:</span><span class="sxs-lookup"><span data-stu-id="0225b-256">The following data is logged:</span></span>


|<span data-ttu-id="0225b-257">Значение</span><span class="sxs-lookup"><span data-stu-id="0225b-257">Value</span></span>  |<span data-ttu-id="0225b-258">Описание</span><span class="sxs-lookup"><span data-stu-id="0225b-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="0225b-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="0225b-259">instanceId</span></span>     | <span data-ttu-id="0225b-260">Экземпляр шлюза приложений, для которого формируются данные о брандмауэре.</span><span class="sxs-lookup"><span data-stu-id="0225b-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="0225b-261">Если экземпляров шлюза приложений несколько, каждому экземпляру будет соответствовать определенная строка.</span><span class="sxs-lookup"><span data-stu-id="0225b-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="0225b-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="0225b-262">clientIp</span></span>     |   <span data-ttu-id="0225b-263">IP-адрес источника запроса.</span><span class="sxs-lookup"><span data-stu-id="0225b-263">Originating IP for the request.</span></span>      |
|<span data-ttu-id="0225b-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="0225b-264">clientPort</span></span>     |  <span data-ttu-id="0225b-265">Порт источника запроса.</span><span class="sxs-lookup"><span data-stu-id="0225b-265">Originating port for the request.</span></span>       |
|<span data-ttu-id="0225b-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="0225b-266">requestUri</span></span>     | <span data-ttu-id="0225b-267">URL-адрес полученного запроса.</span><span class="sxs-lookup"><span data-stu-id="0225b-267">URL of the received request.</span></span>       |
|<span data-ttu-id="0225b-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="0225b-268">ruleSetType</span></span>     | <span data-ttu-id="0225b-269">Тип набора правил.</span><span class="sxs-lookup"><span data-stu-id="0225b-269">Rule set type.</span></span> <span data-ttu-id="0225b-270">Доступное значение — OWASP.</span><span class="sxs-lookup"><span data-stu-id="0225b-270">The available value is OWASP.</span></span>        |
|<span data-ttu-id="0225b-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="0225b-271">ruleSetVersion</span></span>     | <span data-ttu-id="0225b-272">Используемая версия набора правил.</span><span class="sxs-lookup"><span data-stu-id="0225b-272">Rule set version used.</span></span> <span data-ttu-id="0225b-273">Возможные значения: 2.2.9 и 3.0.</span><span class="sxs-lookup"><span data-stu-id="0225b-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="0225b-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="0225b-274">ruleId</span></span>     | <span data-ttu-id="0225b-275">Идентификатор правила события-триггера.</span><span class="sxs-lookup"><span data-stu-id="0225b-275">Rule ID of the triggering event.</span></span>        |
|<span data-ttu-id="0225b-276">Message</span><span class="sxs-lookup"><span data-stu-id="0225b-276">message</span></span>     | <span data-ttu-id="0225b-277">Понятное сообщение для события-триггера.</span><span class="sxs-lookup"><span data-stu-id="0225b-277">User-friendly message for the triggering event.</span></span> <span data-ttu-id="0225b-278">Дополнительные сведения приведены в разделе details.</span><span class="sxs-lookup"><span data-stu-id="0225b-278">More details are provided in the details section.</span></span>        |
|<span data-ttu-id="0225b-279">action</span><span class="sxs-lookup"><span data-stu-id="0225b-279">action</span></span>     |  <span data-ttu-id="0225b-280">Действие, выполняемое с запросом.</span><span class="sxs-lookup"><span data-stu-id="0225b-280">Action taken on the request.</span></span> <span data-ttu-id="0225b-281">Возможные значения: Blocked и Allowed.</span><span class="sxs-lookup"><span data-stu-id="0225b-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="0225b-282">site</span><span class="sxs-lookup"><span data-stu-id="0225b-282">site</span></span>     | <span data-ttu-id="0225b-283">Сайт, для которого создан журнал.</span><span class="sxs-lookup"><span data-stu-id="0225b-283">Site for which the log was generated.</span></span> <span data-ttu-id="0225b-284">В нашем случае возможно только значение Global, так как применяются глобальные правила.</span><span class="sxs-lookup"><span data-stu-id="0225b-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="0225b-285">сведения</span><span class="sxs-lookup"><span data-stu-id="0225b-285">details</span></span>     | <span data-ttu-id="0225b-286">Сведения о событии-триггере.</span><span class="sxs-lookup"><span data-stu-id="0225b-286">Details of the triggering event.</span></span>        |
|<span data-ttu-id="0225b-287">details.message</span><span class="sxs-lookup"><span data-stu-id="0225b-287">details.message</span></span>     | <span data-ttu-id="0225b-288">Описание правила.</span><span class="sxs-lookup"><span data-stu-id="0225b-288">Description of the rule.</span></span>        |
|<span data-ttu-id="0225b-289">details.data</span><span class="sxs-lookup"><span data-stu-id="0225b-289">details.data</span></span>     | <span data-ttu-id="0225b-290">Определенные данные из запроса, которые соответствуют правилу.</span><span class="sxs-lookup"><span data-stu-id="0225b-290">Specific data found in request that matched the rule.</span></span>         |
|<span data-ttu-id="0225b-291">details.file</span><span class="sxs-lookup"><span data-stu-id="0225b-291">details.file</span></span>     | <span data-ttu-id="0225b-292">Файл конфигурации, содержащий правило.</span><span class="sxs-lookup"><span data-stu-id="0225b-292">Configuration file that contained the rule.</span></span>        |
|<span data-ttu-id="0225b-293">details.line</span><span class="sxs-lookup"><span data-stu-id="0225b-293">details.line</span></span>     | <span data-ttu-id="0225b-294">Номер строки в файле конфигурации, активировавшей событие.</span><span class="sxs-lookup"><span data-stu-id="0225b-294">Line number in the configuration file that triggered the event.</span></span>       |

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

### <a name="view-and-analyze-the-activity-log"></a><span data-ttu-id="0225b-295">Просмотр и анализ журнала действий</span><span class="sxs-lookup"><span data-stu-id="0225b-295">View and analyze the activity log</span></span>

<span data-ttu-id="0225b-296">Данные журнала действий можно просматривать и анализировать с помощью любого из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="0225b-296">You can view and analyze activity log data by using any of the following methods:</span></span>

* <span data-ttu-id="0225b-297">**Средства Azure.** Информацию из журналов действий можно получать с помощью Azure PowerShell, Azure CLI, REST API Azure или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="0225b-297">**Azure tools**: Retrieve information from the activity log through Azure PowerShell, the Azure CLI, the Azure REST API, or the Azure portal.</span></span> <span data-ttu-id="0225b-298">Пошаговые инструкции для каждого метода подробно описаны в статье [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) (Выполнение операций в журналах действий с помощью Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="0225b-298">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="0225b-299">**Power BI.** Если у вас еще нет учетной записи [Power BI](https://powerbi.microsoft.com/pricing), вы можете использовать бесплатную пробную версию.</span><span class="sxs-lookup"><span data-stu-id="0225b-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="0225b-300">Используя [пакет содержимого журналов действий Azure для Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), можно анализировать данные с помощью предварительно настроенных панелей мониторинга, которые можно использовать "как есть" или дополнительно настроить.</span><span class="sxs-lookup"><span data-stu-id="0225b-300">By using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-the-access-performance-and-firewall-logs"></a><span data-ttu-id="0225b-301">Просмотр и анализ журналов доступа, производительности и брандмауэра</span><span class="sxs-lookup"><span data-stu-id="0225b-301">View and analyze the access, performance, and firewall logs</span></span>

<span data-ttu-id="0225b-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) может собирать файлы журналов счетчиков и событий из вашей учетной записи хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="0225b-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect the counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="0225b-303">Эта служба предоставляет средства визуализации и эффективные возможности поиска для анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="0225b-303">It includes visualizations and powerful search capabilities to analyze your logs.</span></span>

<span data-ttu-id="0225b-304">Вы также можете подключиться к учетной записи хранения и извлечь записи журнала JSON для журналов доступа и производительности.</span><span class="sxs-lookup"><span data-stu-id="0225b-304">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span></span> <span data-ttu-id="0225b-305">После скачивания JSON-файлов их можно преобразовать в формат CSV и просматривать в Excel, Power BI или другом средстве визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="0225b-305">After you download the JSON files, you can convert them to CSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="0225b-306">Если вы знакомы с Visual Studio и основными понятиями изменения значений констант и переменных в C#, можно использовать [инструменты преобразования журналов](https://github.com/Azure-Samples/networking-dotnet-log-converter), доступные на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="0225b-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="0225b-307">Метрики</span><span class="sxs-lookup"><span data-stu-id="0225b-307">Metrics</span></span>

<span data-ttu-id="0225b-308">Метрики — это функция определенных ресурсов Azure, позволяющая просматривать данные счетчиков производительности на портале.</span><span class="sxs-lookup"><span data-stu-id="0225b-308">Metrics are a feature for certain Azure resources where you can view performance counters in the portal.</span></span> <span data-ttu-id="0225b-309">Сейчас для шлюза приложений доступна одна метрика.</span><span class="sxs-lookup"><span data-stu-id="0225b-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="0225b-310">Эта метрика измеряет пропускную способность, и ее можно просмотреть на портале.</span><span class="sxs-lookup"><span data-stu-id="0225b-310">This metric is throughput, and you can see it in the portal.</span></span> <span data-ttu-id="0225b-311">Перейдите к шлюзу приложений и щелкните **Метрики**.</span><span class="sxs-lookup"><span data-stu-id="0225b-311">Browse to an application gateway and click **Metrics**.</span></span> <span data-ttu-id="0225b-312">Выберите "Throughput" (Пропускная способность) в разделе **Available metrics** (Доступные метрики), чтобы просмотреть значения.</span><span class="sxs-lookup"><span data-stu-id="0225b-312">To view the values, select throughput in the **Available metrics** section.</span></span> <span data-ttu-id="0225b-313">На следующем рисунке приведен пример с фильтрами, которые можно использовать для отображения данных за различные периоды времени.</span><span class="sxs-lookup"><span data-stu-id="0225b-313">In the following image, you can see an example with the filters that you can use to display the data in different time ranges.</span></span>

![Представление метрик с фильтрами][5]

<span data-ttu-id="0225b-315">Текущий список метрик доступен на странице [Метрики, поддерживаемые Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0225b-315">To see a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="0225b-316">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="0225b-316">Alert rules</span></span>

<span data-ttu-id="0225b-317">Вы можете запустить правила генерации оповещений на основе метрик для ресурса.</span><span class="sxs-lookup"><span data-stu-id="0225b-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="0225b-318">Например, оповещение может вызвать веб-перехватчик или отправить электронное сообщение администратору, если пропускная способность шлюза приложений будет больше или меньше порогового значения в указанный период времени либо равной этому значению.</span><span class="sxs-lookup"><span data-stu-id="0225b-318">For example, an alert can call a webhook or email an administrator if the throughput of the application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="0225b-319">Приведенный ниже пример поможет вам создать правило генерации оповещений, согласно которому администратору отправляется электронное сообщение в случае нарушения порога пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="0225b-319">The following example walks you through creating an alert rule that sends an email to an administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="0225b-320">Нажмите кнопку **Добавить оповещение метрики**, чтобы открыть колонку **Добавление правила**.</span><span class="sxs-lookup"><span data-stu-id="0225b-320">Click **Add metric alert** to open the **Add rule** blade.</span></span> <span data-ttu-id="0225b-321">Эту колонку можно также открыть из колонки метрик.</span><span class="sxs-lookup"><span data-stu-id="0225b-321">You can also reach this blade from the metrics blade.</span></span>

   ![Кнопка "Добавить оповещение метрики"][6]

2. <span data-ttu-id="0225b-323">В колонке **Добавление правила** заполните разделы для имени, условия и уведомления. После этого нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0225b-323">On the **Add rule** blade, fill out the name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="0225b-324">С помощью селектора **Условие** выберите одно из четырех значений: **Больше**, **Больше или равно**, **Меньше** или **Меньше или равно**.</span><span class="sxs-lookup"><span data-stu-id="0225b-324">In the **Condition** selector, select one of the four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="0225b-325">С помощью селектора **Период** выберите интервал от 5 минут до 6 часов.</span><span class="sxs-lookup"><span data-stu-id="0225b-325">In the **Period** selector, select a period from 5 minutes to 6 hours.</span></span>

   * <span data-ttu-id="0225b-326">Если установить флажок **Участники, читатели и владельцы электронной почты**, можно будет отправлять электронные сообщения в динамическом режиме пользователям, у которых есть доступ к этому ресурсу.</span><span class="sxs-lookup"><span data-stu-id="0225b-326">If you select **Email owners, contributors, and readers**, the email can be dynamic based on the users who have access to that resource.</span></span> <span data-ttu-id="0225b-327">В противном случае можно указать список пользователей с разделителями-запятыми в текстовом поле **Дополнительные адреса электронной почты администратора**.</span><span class="sxs-lookup"><span data-stu-id="0225b-327">Otherwise, you can provide a comma-separated list of users in the **Additional administrator email(s)** box.</span></span>

   ![Колонка "Добавление правила"][7]

<span data-ttu-id="0225b-329">При нарушении порога вы получите примерно такое электронное сообщение:</span><span class="sxs-lookup"><span data-stu-id="0225b-329">If the threshold is breached, an email that's similar to the one in the following image arrives:</span></span>

![Сообщение электронной почты о нарушении порога][8]

<span data-ttu-id="0225b-331">После создания оповещения метрики появится список оповещений.</span><span class="sxs-lookup"><span data-stu-id="0225b-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="0225b-332">В нем содержатся все правила генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="0225b-332">It provides an overview of all the alert rules.</span></span>

![Список оповещений и правил][9]

<span data-ttu-id="0225b-334">Дополнительные сведения об уведомлениях для оповещений см. в статье [Что такое оповещения в Microsoft Azure?](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="0225b-334">To learn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="0225b-335">Чтобы лучше понять, как действуют веб-перехватчики и как их использовать с оповещениями, см. статью [Настройка веб-перехватчиков для оповещений на основе метрик Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="0225b-335">To understand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0225b-336">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0225b-336">Next steps</span></span>

* <span data-ttu-id="0225b-337">См. сведения о визуализации журналов счетчиков и событий с помощью [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="0225b-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="0225b-338">Прочтите запись блога [Visualize your Azure Activity Log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Визуализация журналов действий Azure с помощью Power BI).</span><span class="sxs-lookup"><span data-stu-id="0225b-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="0225b-339">Прочтите запись блога [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Просмотр и анализ журналов аудита Azure с помощью Power BI и других средств).</span><span class="sxs-lookup"><span data-stu-id="0225b-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

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
