---
title: "aaaView действий Azure записывает ресурсы toomonitor | Документы Microsoft"
description: "Используйте hello действий журналы tooreview пользователя и ошибок. Отображаются портал Azure, PowerShell, интерфейс командной строки Azure и REST."
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
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a><span data-ttu-id="f6966-104">Просмотр активности регистрирует действия tooaudit ресурсов</span><span class="sxs-lookup"><span data-stu-id="f6966-104">View activity logs tooaudit actions on resources</span></span>
<span data-ttu-id="f6966-105">С помощью журналов действий можно определить:</span><span class="sxs-lookup"><span data-stu-id="f6966-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="f6966-106">операций, которые были выполнены на hello ресурсам в подписке</span><span class="sxs-lookup"><span data-stu-id="f6966-106">what operations were taken on hello resources in your subscription</span></span>
* <span data-ttu-id="f6966-107">кто инициировал операцию hello (несмотря на то, что операции, инициированные с помощью серверной службы не возвращают пользователя как hello вызывающего объекта)</span><span class="sxs-lookup"><span data-stu-id="f6966-107">who initiated hello operation (although operations initiated by a backend service do not return a user as hello caller)</span></span>
* <span data-ttu-id="f6966-108">Если произошла операция hello</span><span class="sxs-lookup"><span data-stu-id="f6966-108">when hello operation occurred</span></span>
* <span data-ttu-id="f6966-109">Hello состояние операции hello</span><span class="sxs-lookup"><span data-stu-id="f6966-109">hello status of hello operation</span></span>
* <span data-ttu-id="f6966-110">Hello значений других свойств, которые могут помочь вам исследовать операции hello</span><span class="sxs-lookup"><span data-stu-id="f6966-110">hello values of other properties that might help you research hello operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="f6966-111">Можно получать сведения из журналы действий hello через портал hello, PowerShell, Azure CLI, API-интерфейса REST аналитики или [библиотеки .NET аналитики](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="f6966-111">You can retrieve information from hello activity logs through hello portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="f6966-112">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f6966-112">Portal</span></span>
1. <span data-ttu-id="f6966-113">Выберите журналы действий hello tooview через портал hello **монитора**.</span><span class="sxs-lookup"><span data-stu-id="f6966-113">tooview hello activity logs through hello portal, select **Monitor**.</span></span>
   
    ![просмотр журналов действий](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="f6966-115">Или, в журнал действий hello tooautomatically фильтра для определенного ресурса или ресурса группы выберите **журнал действий** из этой колонки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f6966-115">Or, tooautomatically filter hello activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="f6966-116">Обратите внимание, что этот журнал активности hello автоматически фильтруется по hello выбранных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f6966-116">Notice that hello activity log is automatically filtered by hello selected resource.</span></span>
   
    ![фильтрация по ресурсам](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="f6966-118">В hello **журнал действий** колонке просмотреть сводку последних операций.</span><span class="sxs-lookup"><span data-stu-id="f6966-118">In hello **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![отображение действий](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="f6966-120">Количество операций, отображенных, hello toorestrict выберите различных условий.</span><span class="sxs-lookup"><span data-stu-id="f6966-120">toorestrict hello number of operations displayed, select different conditions.</span></span> <span data-ttu-id="f6966-121">Hello следующем рисунке показано, hello **Timespan** и **инициировано событие** поля изменить tooview hello действия, предпринимаемые конкретного пользователя или приложения hello прошлый месяц.</span><span class="sxs-lookup"><span data-stu-id="f6966-121">For example, hello following image shows hello **Timespan** and **Event initiated by** fields changed tooview hello actions taken by a particular user or application for hello past month.</span></span> <span data-ttu-id="f6966-122">Выберите **применить** tooview hello результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="f6966-122">Select **Apply** tooview hello results of your query.</span></span>
   
    ![установка параметров фильтра](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="f6966-124">Если требуется запрос toorun hello позже выбрать **Сохранить** и присвойте имя запроса hello.</span><span class="sxs-lookup"><span data-stu-id="f6966-124">If you need toorun hello query again later, select **Save** and give hello query a name.</span></span>
   
    ![сохранение запроса](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="f6966-126">tooquickly при выполнении запроса, можно выбрать один из встроенных запросов hello, например неудачными развертываниями.</span><span class="sxs-lookup"><span data-stu-id="f6966-126">tooquickly run a query, you can select one of hello built-in queries, such as failed deployments.</span></span>

    ![Выбор запроса](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="f6966-128">Выбранный запрос Hello автоматически задает hello необходимые значения фильтра.</span><span class="sxs-lookup"><span data-stu-id="f6966-128">hello selected query automatically sets hello required filter values.</span></span>

    ![Просмотр ошибок развертывания](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="f6966-130">Выберите одну из операций hello toosee сводку событий hello.</span><span class="sxs-lookup"><span data-stu-id="f6966-130">Select one of hello operations toosee a summary of hello event.</span></span>

    ![Просмотр операции](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="f6966-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6966-132">PowerShell</span></span>
1. <span data-ttu-id="f6966-133">tooretrieve, записи журнала выполнения hello **Get AzureRmLog** команды.</span><span class="sxs-lookup"><span data-stu-id="f6966-133">tooretrieve log entries, run hello **Get-AzureRmLog** command.</span></span> <span data-ttu-id="f6966-134">Задаются Дополнительные параметры toofilter hello список записей.</span><span class="sxs-lookup"><span data-stu-id="f6966-134">You provide additional parameters toofilter hello list of entries.</span></span> <span data-ttu-id="f6966-135">Если время начала и окончания не указан, возвращаются записи для hello последний час.</span><span class="sxs-lookup"><span data-stu-id="f6966-135">If you do not specify a start and end time, entries for hello last hour are returned.</span></span> <span data-ttu-id="f6966-136">Например tooretrieve hello операции для группы ресурсов во время hello последний час запуска:</span><span class="sxs-lookup"><span data-stu-id="f6966-136">For example, tooretrieve hello operations for a resource group during hello past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="f6966-137">Hello в следующем примере показано, как действие hello toouse входа tooresearch операций, выполненных во время указанного времени.</span><span class="sxs-lookup"><span data-stu-id="f6966-137">hello following example shows how toouse hello activity log tooresearch operations taken during a specified time.</span></span> <span data-ttu-id="f6966-138">Hello даты начала и окончания указаны в формате даты.</span><span class="sxs-lookup"><span data-stu-id="f6966-138">hello start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="f6966-139">Или можно использовать функции toospecify hello дату диапазона дат, например hello последние 14 дней.</span><span class="sxs-lookup"><span data-stu-id="f6966-139">Or, you can use date functions toospecify hello date range, such as hello last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="f6966-140">В зависимости от времени запуска hello, указываемые hello предыдущих команд может возвращать длинный список операций для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="f6966-140">Depending on hello start time you specify, hello previous commands can return a long list of operations for hello resource group.</span></span> <span data-ttu-id="f6966-141">Можно фильтровать результаты hello для то, что вы ищете, предоставляя условия поиска.</span><span class="sxs-lookup"><span data-stu-id="f6966-141">You can filter hello results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="f6966-142">Например если вы пытаетесь tooresearch как веб-приложения было остановлено, можно выполнить hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f6966-142">For example, if you are trying tooresearch how a web app was stopped, you could run hello following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="f6966-143">В нашем примере вы видите, что веб-приложение было остановлено пользователем someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f6966-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

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

3. <span data-ttu-id="f6966-144">Можно выполнять поиск hello действия, производимые конкретного пользователя, даже для группы ресурсов, которые больше не существует.</span><span class="sxs-lookup"><span data-stu-id="f6966-144">You can look up hello actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="f6966-145">Можно применить фильтр для невыполненных операций.</span><span class="sxs-lookup"><span data-stu-id="f6966-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="f6966-146">Просмотрев hello сообщение о состоянии для этой записи, можно сосредоточиться на одну ошибку.</span><span class="sxs-lookup"><span data-stu-id="f6966-146">You can focus on one error by looking at hello status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="f6966-147">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="f6966-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="f6966-148">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="f6966-148">Azure CLI</span></span>
* <span data-ttu-id="f6966-149">записи журнала tooretrieve, запустите hello **Показать журнал группу azure** команды.</span><span class="sxs-lookup"><span data-stu-id="f6966-149">tooretrieve log entries, you run hello **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="f6966-150">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="f6966-150">REST API</span></span>
<span data-ttu-id="f6966-151">Hello операции REST для работы с журналом hello являются частью hello [API-интерфейса REST аналитики](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6966-151">hello REST operations for working with hello activity log are part of hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="f6966-152">tooretrieve активности журнала событий, в разделе [список событий управления hello в подписке](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6966-152">tooretrieve activity log events, see [List hello management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6966-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f6966-153">Next steps</span></span>
* <span data-ttu-id="f6966-154">Журналы Azure действие может использоваться с Power BI toogain лучшее представление о действиях hello в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="f6966-154">Azure Activity logs can be used with Power BI toogain greater insights about hello actions in your subscription.</span></span> <span data-ttu-id="f6966-155">Дополнительные сведения см. в записи блога [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Журналы аудита Azure в Power BI: просмотр, анализ и другие возможности).</span><span class="sxs-lookup"><span data-stu-id="f6966-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="f6966-156">toolearn о настройке политик безопасности в разделе [управления доступом на основе ролей Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f6966-156">toolearn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="f6966-157">toolearn о командах hello Просмотр операций развертывания. в разделе [просмотреть операции развертывания](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="f6966-157">toolearn about hello commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="f6966-158">tooprevent удаления ресурса для всех пользователей. в статье toolearn [блокировку ресурсов с помощью диспетчера ресурсов Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f6966-158">toolearn how tooprevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

