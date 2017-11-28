---
title: "Просмотр журналов действий Azure для наблюдения за ресурсами | Документация Майкрософт"
description: "Просмотр действий пользователя и ошибок с помощью журнала действий. Отображаются портал Azure, PowerShell, интерфейс командной строки Azure и REST."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 9f90bc80c146c6c2da04aacbc110f7d389c0baa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="view-activity-logs-to-audit-actions-on-resources"></a><span data-ttu-id="06db9-104">Просмотр журналов действий для аудита действий с ресурсами</span><span class="sxs-lookup"><span data-stu-id="06db9-104">View activity logs to audit actions on resources</span></span>
<span data-ttu-id="06db9-105">С помощью журналов действий можно определить:</span><span class="sxs-lookup"><span data-stu-id="06db9-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="06db9-106">какие операции выполнялись с ресурсами в вашей подписке;</span><span class="sxs-lookup"><span data-stu-id="06db9-106">what operations were taken on the resources in your subscription</span></span>
* <span data-ttu-id="06db9-107">кто инициировал операцию (при этом для операций, инициированных серверной службой, имя вызывающего пользователя не возвращается); </span><span class="sxs-lookup"><span data-stu-id="06db9-107">who initiated the operation (although operations initiated by a backend service do not return a user as the caller)</span></span>
* <span data-ttu-id="06db9-108">когда была выполнена операция;</span><span class="sxs-lookup"><span data-stu-id="06db9-108">when the operation occurred</span></span>
* <span data-ttu-id="06db9-109">состояние операции;</span><span class="sxs-lookup"><span data-stu-id="06db9-109">the status of the operation</span></span>
* <span data-ttu-id="06db9-110">значения других свойств, которые могут помочь в изучении операции.</span><span class="sxs-lookup"><span data-stu-id="06db9-110">the values of other properties that might help you research the operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="06db9-111">Сведения из журналов действий можно получить с помощью портала, PowerShell, интерфейса командной строки Azure, API REST Insights или с помощью [библиотеки .NET для Insights](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="06db9-111">You can retrieve information from the activity logs through the portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="06db9-112">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="06db9-112">Portal</span></span>
1. <span data-ttu-id="06db9-113">Чтобы просмотреть журналы действий на портале, выберите **Монитор**.</span><span class="sxs-lookup"><span data-stu-id="06db9-113">To view the activity logs through the portal, select **Monitor**.</span></span>
   
    ![просмотр журналов действий](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="06db9-115">Или, чтобы автоматически отфильтровать журнал действий по определенному ресурсу или группе ресурсов, выберите **Журнал действий** в колонке этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="06db9-115">Or, to automatically filter the activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="06db9-116">Обратите внимание, что журнал действий автоматически фильтруется по выбранному ресурсу.</span><span class="sxs-lookup"><span data-stu-id="06db9-116">Notice that the activity log is automatically filtered by the selected resource.</span></span>
   
    ![фильтрация по ресурсам](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="06db9-118">В колонке **Журнал действий** можно просмотреть сводку последних операций.</span><span class="sxs-lookup"><span data-stu-id="06db9-118">In the **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![отображение действий](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="06db9-120">Чтобы ограничить количество отображаемых операций, выберите различные условия.</span><span class="sxs-lookup"><span data-stu-id="06db9-120">To restrict the number of operations displayed, select different conditions.</span></span> <span data-ttu-id="06db9-121">Например, на следующем рисунке показано, как изменение полей **Временной диапазон** и **Кем инициировано событие** позволяет просмотреть действия конкретного пользователя или приложения за прошлый месяц.</span><span class="sxs-lookup"><span data-stu-id="06db9-121">For example, the following image shows the **Timespan** and **Event initiated by** fields changed to view the actions taken by a particular user or application for the past month.</span></span> <span data-ttu-id="06db9-122">Выберите **Применить** для просмотра результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="06db9-122">Select **Apply** to view the results of your query.</span></span>
   
    ![установка параметров фильтра](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="06db9-124">Если вы хотите повторить тот же запрос позже, выберите **Сохранить** и укажите имя запроса.</span><span class="sxs-lookup"><span data-stu-id="06db9-124">If you need to run the query again later, select **Save** and give the query a name.</span></span>
   
    ![сохранение запроса](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="06db9-126">Чтобы быстро выполнить запрос, можно выбрать один из встроенных запросов, например запрос невыполненных развертываний.</span><span class="sxs-lookup"><span data-stu-id="06db9-126">To quickly run a query, you can select one of the built-in queries, such as failed deployments.</span></span>

    ![Выбор запроса](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="06db9-128">Выбранный запрос автоматически задает необходимые значения фильтра.</span><span class="sxs-lookup"><span data-stu-id="06db9-128">The selected query automatically sets the required filter values.</span></span>

    ![Просмотр ошибок развертывания](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="06db9-130">Выберите одну из операций, чтобы просмотреть сводку по событию.</span><span class="sxs-lookup"><span data-stu-id="06db9-130">Select one of the operations to see a summary of the event.</span></span>

    ![Просмотр операции](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="06db9-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06db9-132">PowerShell</span></span>
1. <span data-ttu-id="06db9-133">Чтобы получить записи журнала, выполните команду **Get-AzureRmLog** .</span><span class="sxs-lookup"><span data-stu-id="06db9-133">To retrieve log entries, run the **Get-AzureRmLog** command.</span></span> <span data-ttu-id="06db9-134">Укажите дополнительные параметры, чтобы отфильтровать список записей.</span><span class="sxs-lookup"><span data-stu-id="06db9-134">You provide additional parameters to filter the list of entries.</span></span> <span data-ttu-id="06db9-135">Если не указать время начала и окончания, возвращаются записи за последний час.</span><span class="sxs-lookup"><span data-stu-id="06db9-135">If you do not specify a start and end time, entries for the last hour are returned.</span></span> <span data-ttu-id="06db9-136">Например, для получения операций для группы ресурсов за последний час выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="06db9-136">For example, to retrieve the operations for a resource group during the past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="06db9-137">В следующем примере показано, как использовать журнал действий для анализа действий, выполненных в течение указанного времени.</span><span class="sxs-lookup"><span data-stu-id="06db9-137">The following example shows how to use the activity log to research operations taken during a specified time.</span></span> <span data-ttu-id="06db9-138">Даты начала и окончания указывайте в формате даты.</span><span class="sxs-lookup"><span data-stu-id="06db9-138">The start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="06db9-139">Диапазон дат, например последние 14 дней, также можно указать с помощью функций даты.</span><span class="sxs-lookup"><span data-stu-id="06db9-139">Or, you can use date functions to specify the date range, such as the last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="06db9-140">В зависимости от указанного времени начала приведенные выше команды могут вернуть длинный список операций для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="06db9-140">Depending on the start time you specify, the previous commands can return a long list of operations for the resource group.</span></span> <span data-ttu-id="06db9-141">Чтобы найти в результатах нужную информацию, отфильтруйте их, используя условия поиска.</span><span class="sxs-lookup"><span data-stu-id="06db9-141">You can filter the results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="06db9-142">Например, чтобы проанализировать обстоятельства остановки веб-приложения, выполните приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="06db9-142">For example, if you are trying to research how a web app was stopped, you could run the following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="06db9-143">В нашем примере вы видите, что веб-приложение было остановлено пользователем someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="06db9-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. <span data-ttu-id="06db9-144">Можно найти действия, выполненные конкретным пользователем, даже для группы ресурсов, которой больше не существует.</span><span class="sxs-lookup"><span data-stu-id="06db9-144">You can look up the actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="06db9-145">Можно применить фильтр для невыполненных операций.</span><span class="sxs-lookup"><span data-stu-id="06db9-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="06db9-146">Можно получить сведения об одной ошибке, просмотрев сообщение о состоянии для ее записи.</span><span class="sxs-lookup"><span data-stu-id="06db9-146">You can focus on one error by looking at the status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="06db9-147">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="06db9-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="06db9-148">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="06db9-148">Azure CLI</span></span>
* <span data-ttu-id="06db9-149">Чтобы получить записи журнала, выполните команду **azure group log show** .</span><span class="sxs-lookup"><span data-stu-id="06db9-149">To retrieve log entries, you run the **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="06db9-150">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="06db9-150">REST API</span></span>
<span data-ttu-id="06db9-151">Операции REST для работы с журналом действий включены в интерфейс [REST API Insights](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="06db9-151">The REST operations for working with the activity log are part of the [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="06db9-152">Получение событий журнала действий описано в статье [Список событий управления в подписке](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="06db9-152">To retrieve activity log events, see [List the management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="06db9-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06db9-153">Next steps</span></span>
* <span data-ttu-id="06db9-154">Чтобы получить больше информации о действиях в вашей подписке, можно использовать журналы аудита Azure совместно с Power BI.</span><span class="sxs-lookup"><span data-stu-id="06db9-154">Azure Activity logs can be used with Power BI to gain greater insights about the actions in your subscription.</span></span> <span data-ttu-id="06db9-155">Дополнительные сведения см. в записи блога [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Журналы аудита Azure в Power BI: просмотр, анализ и другие возможности).</span><span class="sxs-lookup"><span data-stu-id="06db9-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="06db9-156">Дополнительные сведения о настройке политик безопасности см. в статье о [контроле доступа на основе ролей Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="06db9-156">To learn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="06db9-157">Чтобы узнать о командах для просмотра операций развертывания, ознакомьтесь с разделом [View deployment operations with Azure Resource Manager](resource-manager-deployment-operations.md) (Просмотр операций развертывания с помощью Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="06db9-157">To learn about the commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="06db9-158">Вы можете запретить всем пользователям операции удаления для определенного ресурса, как описано в статье [Блокировка ресурсов с помощью Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="06db9-158">To learn how to prevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

