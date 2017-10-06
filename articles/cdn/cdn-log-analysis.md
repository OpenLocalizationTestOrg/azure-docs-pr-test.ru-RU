---
title: "Анализ aaaLog для Azure CDN | Документы Microsoft"
description: "Клиент может включить анализ журналов для Azure CDN."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="ed1d9-103">Журналы диагностики для Azure CDN</span><span class="sxs-lookup"><span data-stu-id="ed1d9-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="ed1d9-104">После включения CDN для вашего приложения, будет скорее всего требуется использование CDN toomonitor hello, проверьте работоспособность вашей доставки hello и устранения возможных проблем.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-104">After enabling CDN for your application, you will likely want toomonitor hello CDN usage, check hello health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="ed1d9-105">Azure CDN предоставляет эти возможности с помощью [CDN Core Analytics](cdn-analyze-usage-patterns.md) и [журналов диагностики](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="ed1d9-106">CDN Core Analytics</span><span class="sxs-lookup"><span data-stu-id="ed1d9-106">CDN Core Analytics</span></span>
<span data-ttu-id="ed1d9-107">Именем текущего пользователя сети доставки Содержимого Azure Verizon standard или premium профиля уже analytics основные возможности tooview hello дополнительный портал через параметр «Управление» hello из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able tooview core analytics in hello supplemental portal accessible via hello "Manage" option from hello Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="ed1d9-108">Журналы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="ed1d9-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="ed1d9-109">Эта новая функция Azure позволяет просматривать основную аналитику и сохранять ее в одно или несколько целевых расположений:</span><span class="sxs-lookup"><span data-stu-id="ed1d9-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="ed1d9-110">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="ed1d9-110">Azure Storage account</span></span>
 - <span data-ttu-id="ed1d9-111">Концентраторы событий Azure</span><span class="sxs-lookup"><span data-stu-id="ed1d9-111">Azure Event Hubs</span></span>
 - <span data-ttu-id="ed1d9-112">[репозиторий OMS Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-112">[OMS Log Analytics repository](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)</span></span>
 
 <span data-ttu-id="ed1d9-113">Эта функция доступна для всех конечных точек CDN, принадлежащий tooVerizon (Standard и Premium) и профили CDN Akamai (стандартный).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-113">This feature is available for all CDN endpoints belonging tooVerizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="ed1d9-114">Журналы диагностики разрешить показателей tooexport базовые способы использования вашей CDN конечную точку tooa различных источников, что позволяет обрабатывать настраиваемым способом.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-114">Diagnostics logs allow you tooexport basic usage metrics from your CDN endpoint tooa variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="ed1d9-115">Например, можно сделать hello следующие типы данных экспорта:</span><span class="sxs-lookup"><span data-stu-id="ed1d9-115">For example, you can do hello following types of data export:</span></span>

- <span data-ttu-id="ed1d9-116">Экспорт данных tooblob хранилища, экспорт tooCSV и создание диаграмм в excel.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-116">Export data tooblob storage, export tooCSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="ed1d9-117">Экспорт данных tooevent концентраторов и согласования с данными из других служб azure.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-117">Export data tooevent hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="ed1d9-118">Экспорт данных toolog аналитики и просмотра данных в собственных рабочей области OMS</span><span class="sxs-lookup"><span data-stu-id="ed1d9-118">Export data toolog analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="ed1d9-119">Hello на этом рисунке показано типичное представление Analytics CDN основных данных.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-119">hello following figure shows a typical CDN Core Analytics view into data.</span></span>

![Портал — журналы диагностики](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="ed1d9-121">*Рисунок 1. Представление CDN Core Analytics*</span><span class="sxs-lookup"><span data-stu-id="ed1d9-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="ed1d9-122">Пошаговое руководство Hello проходит через hello схемы данных аналитики core hello, шаги, необходимые для включения функции hello и их доставку toovarious назначения из указанных целей.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-122">hello following walkthrough goes through hello schema of hello core analytics data, steps involved in enabling hello feature and delivering them toovarious destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="ed1d9-123">Включение ведения журнала с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="ed1d9-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="ed1d9-124">Hello журналы диагностики включены **off** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-124">hello diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="ed1d9-125">Выполните действия hello ниже tooenable ведения журнала с помощью CDN Core аналитики.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-125">Follow hello steps below tooenable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="ed1d9-126">Войдите в toohello [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-126">Sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="ed1d9-127">Если в вашем рабочем процессе еще не включена служба CDN, [включите Azure CDN](cdn-create-new-endpoint.md), прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="ed1d9-128">На портале hello перейдите слишком**профиля CDN**.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-128">In hello portal, navigate too**CDN profile**.</span></span>
2. <span data-ttu-id="ed1d9-129">Выберите профиль CDN, а затем hello конечной точки CDN, которые должны tooenable **журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-129">Select a CDN profile, then select hello CDN endpoint that you want tooenable **Diagnostics Logs**.</span></span>

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="ed1d9-131">Go слишком**журналы диагностики** колонке под **мониторинг** , а затем изменить состояние hello слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-131">Go too**Diagnostics Logs** blade Under **Monitoring** section, then change hello status too**On**.</span></span>

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="ed1d9-133">Включение ведения журнала с помощью службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ed1d9-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="ed1d9-134">журналы hello toostore toouse хранилища Azure, выберите **архивировать учетной записи хранилища tooa**выберите количество дней хранения и нажмите кнопку **CoreAnalytics** под **журнала**.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-134">toouse Azure Storage toostore hello logs, select **Archive tooa storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![Портал — журналы диагностики](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="ed1d9-136">*Рисунок 2. Ведение журнала с помощью службы хранилища Azure*</span><span class="sxs-lookup"><span data-stu-id="ed1d9-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="ed1d9-137">Ведение журнала с помощью OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ed1d9-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="ed1d9-138">журналы hello toostore toouse анализа журналов OMS, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-138">toouse OMS Log Analytics toostore hello logs, follow these steps:</span></span>

1. <span data-ttu-id="ed1d9-139">Из hello **журналы диагностики** колонке под **мониторинг**выберите **отправки tooLog Analytics** из</span><span class="sxs-lookup"><span data-stu-id="ed1d9-139">From hello **Diagnostics Logs** blade Under **Monitoring**, select **Send tooLog Analytics** from</span></span> 

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="ed1d9-141">Настройка ведения журнала для анализа журналов hello, щелкнув на настройки.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-141">Configure hello Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="ed1d9-142">Откроется диалоговое окно tooa, где можно выбрать предыдущей рабочей областью или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-142">This takes you tooa dialog where you can select a previous workspace or create a new one.</span></span>

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="ed1d9-144">Щелкните **Create New Workspace** (Создание рабочей области).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-144">Click **Create New Workspace**.</span></span>

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="ed1d9-146">Далее необходимо выбрать имя новой рабочей области, имеющуюся подписку, группу ресурсов (новую или имеющуюся), расположение и ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="ed1d9-147">Предусмотрена возможность hello закрепление этой панели мониторинга tooyour конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-147">You have hello option of pinning this configuration tooyour dashboard.</span></span> <span data-ttu-id="ed1d9-148">Нажмите кнопку ОК toocomplete hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-148">Click OK toocomplete hello configuration.</span></span>

    <span data-ttu-id="ed1d9-149">Далее для рабочей области отобразятся имена рабочей области OMS и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="ed1d9-150">Имена должны быть уникальными. В них могут использоваться только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="ed1d9-151">Запрещено использовать пробелы и знаки подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-151">Spaces and underscores are not allowed.</span></span> 

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="ed1d9-153">Далее вы получаете короткое сообщение о том, что рабочей области будет создана и возвращаются tooyour окно конфигурации ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-153">You next get a short message saying that your workspace has been created and you are returned tooyour logging configuration screen.</span></span> <span data-ttu-id="ed1d9-154">Чтобы проверить hello имя рабочей области аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-154">You can confirm hello name of your Log Analytics workspace.</span></span>

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="ed1d9-156">После настройки конфигурации службы анализа журналов hello убедитесь, что вы также установите флажок CoreAnalytics hello CDN ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-156">Once you have set up hello Log Analytics configuration, make sure you also check hello CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="ed1d9-157">Если все tooyour оформлением, щелкните hello **Сохранить** кнопку hello верхней части диалогового окна настройки hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-157">If everything is tooyour liking, click hello **Save** button at hello top of hello configuration dialog.</span></span>

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="ed1d9-159">Hello **Сохранить** кнопка больше не активно и что hello на/кнопки теперь является ON, но синего цвета вместо сиреневый.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-159">hello **Save** button is no longer active and that hello ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="ed1d9-160">Следует toosee новой рабочей областью OMS перейдите tooyour портал Azure панели мониторинга, щелкните имя hello рабочей области аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-160">If you want toosee your new OMS workspace, go tooyour Azure portal Dashboard, click hello name of your Log Analytics workspace.</span></span> <span data-ttu-id="ed1d9-161">Далее вы увидите рабочей области (Убедитесь, что рабочая область OMS выделяется слева hello).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on hello left).</span></span> <span data-ttu-id="ed1d9-162">Щелкните рабочую область в репозиторий OMS hello toosee плитки приветствия портал OMS.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-162">Click on hello OMS Portal tile toosee your workspace in hello OMS repository.</span></span> 

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="ed1d9-164">Репозиторий OMS получаются данные готовы toolog.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-164">Your OMS repository is now ready toolog data.</span></span> <span data-ttu-id="ed1d9-165">Чтобы tooconsume эти данные, необходимо использовать [решений OMS](#consuming-oms-log-analytics-data), охватываемого далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-165">In order tooconsume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="ed1d9-166">Дополнительные сведения о задержках данных журнала см. [здесь](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="ed1d9-167">Включение ведения журнала с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed1d9-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="ed1d9-168">Ниже приведен пример на как tooenable и get журналы диагностики через hello командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-168">Below is an example on how tooenable and get Diagnostic Logs via hello Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="ed1d9-169">Включение журналов диагностики в учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="ed1d9-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="ed1d9-170">Сначала войдите в систему и выберите подписку:</span><span class="sxs-lookup"><span data-stu-id="ed1d9-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="ed1d9-171">tooEnable в журналах диагностики в учетную запись хранилища, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ed1d9-171">tooEnable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="ed1d9-172">tooEnable журналов диагностики в рабочей области OMS, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ed1d9-172">tooEnable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="ed1d9-173">Использование журналов диагностики из службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ed1d9-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="ed1d9-174">В этом разделе описываются схемы hello hello CDN core аналитики, как они организованы в учетную запись хранилища Azure и предоставляет образец кода toodownload hello входит в tooa CSV-файла.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-174">This section describes hello schema of hello CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code toodownload hello logs in tooa CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="ed1d9-175">Использование обозревателя хранилищ Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ed1d9-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="ed1d9-176">Перед обращением к hello core аналитические данные из hello учетной записи хранилища Azure, необходимо сначала hello содержимое средство tooaccess учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-176">Before you can access hello core analytics data from hello Azure Storage Account, you first need a tool tooaccess hello contents in a storage account.</span></span> <span data-ttu-id="ed1d9-177">Хотя существует несколько средств на рынке hello, hello, рекомендуется — hello обозреватель хранилищ Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-177">While there are several tools available in hello market, hello one that we recommend is hello Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="ed1d9-178">Можно загрузить средство hello из [здесь](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-178">You can download hello tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="ed1d9-179">После загрузки и установки программного обеспечения hello, настройте его toouse hello одной учетной записи хранилища Azure, был настроен в качестве назначения toohello CDN журналы диагностики.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-179">After downloading and installing hello software, configure it toouse hello same Azure Storage Account that was configured as a destination toohello CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="ed1d9-180">Откройте **обозреватель хранилищ Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="ed1d9-181">Найдите учетную запись хранилища hello</span><span class="sxs-lookup"><span data-stu-id="ed1d9-181">Locate hello storage account</span></span>
3.  <span data-ttu-id="ed1d9-182">Go toohello **«Контейнеров больших двоичных объектов»** узел в группе хранения учетной записи, а затем раскройте узел hello</span><span class="sxs-lookup"><span data-stu-id="ed1d9-182">Go toohello **“Blob Containers”** node under this storage account and expand hello node</span></span>
4.  <span data-ttu-id="ed1d9-183">Выберите hello контейнер с именем **«аналитика журналов coreanalytics»** и дважды щелкните его</span><span class="sxs-lookup"><span data-stu-id="ed1d9-183">Select hello container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="ed1d9-184">Результаты Показать вверх на hello правой панели начиная с hello уровня, который выглядит как **«resourceId =»**.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-184">Results show up on hello right-hand pane starting with hello first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="ed1d9-185">Продолжайте нажимать кнопку все hello способом, пока не появится файл hello **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-185">Continue clicking all hello way until you see hello file **PT1H.json**.</span></span> <span data-ttu-id="ed1d9-186">См. следующее примечание объяснение пути hello hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-186">See hello following note for explanation of hello path.</span></span>
6.  <span data-ttu-id="ed1d9-187">Каждый BLOB-объект **PT1H.json** представляет hello журналы аналитики один час для конкретной конечной точки CDN или его пользовательский домен.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-187">Each blob **PT1H.json** represents hello analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="ed1d9-188">Схема Hello hello содержимое этого файла JSON описан в разделе hello схемы из hello журналы аналитики Core</span><span class="sxs-lookup"><span data-stu-id="ed1d9-188">hello schema of hello contents of this JSON file is described in hello section Schema of hello Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="ed1d9-189">**Формат пути к BLOB-объекту**</span><span class="sxs-lookup"><span data-stu-id="ed1d9-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="ed1d9-190">Журналы основной аналитики создаются каждый час.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="ed1d9-191">Все данные за час собираются и сохраняются в одном большом двоичном объекте Azure в виде полезных данных JSON.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="ed1d9-192">toothis Hello пути больших двоичных объектов Azure отображается, как если бы — это иерархическая структура.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-192">hello path toothis Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="ed1d9-193">Это так, как средства обозревателя хранилищ hello интерпретирует «/» в качестве разделителя каталогов, показана иерархия hello для удобства.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-193">This is because hello Storage explorer tool interprets '/' as a directory separator and shows hello hierarchy for convenience.</span></span> <span data-ttu-id="ed1d9-194">На самом деле полный путь hello лишь представляет hello имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-194">Actually, hello whole path just represents hello blob name.</span></span> <span data-ttu-id="ed1d9-195">Это имя BLOB-объектов hello следует hello следующее соглашение об именовании</span><span class="sxs-lookup"><span data-stu-id="ed1d9-195">This name of hello blob follows hello following naming convention</span></span> 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="ed1d9-196">**Описание полей**</span><span class="sxs-lookup"><span data-stu-id="ed1d9-196">**Description of fields:**</span></span>

|<span data-ttu-id="ed1d9-197">value</span><span class="sxs-lookup"><span data-stu-id="ed1d9-197">value</span></span>|<span data-ttu-id="ed1d9-198">description</span><span class="sxs-lookup"><span data-stu-id="ed1d9-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="ed1d9-199">Идентификатор подписки</span><span class="sxs-lookup"><span data-stu-id="ed1d9-199">Subscription ID</span></span>    |<span data-ttu-id="ed1d9-200">Идентификатор подписки Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-200">ID of hello Azure Subscription.</span></span> <span data-ttu-id="ed1d9-201">Это формат Guid hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-201">This is in hello Guid format.</span></span>|
|<span data-ttu-id="ed1d9-202">Ресурс</span><span class="sxs-lookup"><span data-stu-id="ed1d9-202">Resource</span></span> |<span data-ttu-id="ed1d9-203">Имя группы ресурсов hello ресурсов группы toowhich hello CDN принадлежат.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-203">Group Name   Name of hello resource group toowhich hello CDN resources belong.</span></span>|
|<span data-ttu-id="ed1d9-204">Имя профиля</span><span class="sxs-lookup"><span data-stu-id="ed1d9-204">Profile Name</span></span> |<span data-ttu-id="ed1d9-205">Имя профиля CDN hello</span><span class="sxs-lookup"><span data-stu-id="ed1d9-205">Name of hello CDN Profile</span></span>|
|<span data-ttu-id="ed1d9-206">Имя конечной точки</span><span class="sxs-lookup"><span data-stu-id="ed1d9-206">Endpoint Name</span></span> |<span data-ttu-id="ed1d9-207">Имя конечной точки CDN hello</span><span class="sxs-lookup"><span data-stu-id="ed1d9-207">Name of hello CDN Endpoint</span></span>|
|<span data-ttu-id="ed1d9-208">Год</span><span class="sxs-lookup"><span data-stu-id="ed1d9-208">Year</span></span>|  <span data-ttu-id="ed1d9-209">представление 4-значный номер года hello 2017 г. Например,</span><span class="sxs-lookup"><span data-stu-id="ed1d9-209">4-digit representation of hello year for example, 2017</span></span>|
|<span data-ttu-id="ed1d9-210">Месяц</span><span class="sxs-lookup"><span data-stu-id="ed1d9-210">Month</span></span>| <span data-ttu-id="ed1d9-211">2-разрядное представление числа месяца hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-211">2-digit representation of hello month number.</span></span> <span data-ttu-id="ed1d9-212">01 — январь, 12 — декабрь.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="ed1d9-213">День</span><span class="sxs-lookup"><span data-stu-id="ed1d9-213">Day</span></span>|   <span data-ttu-id="ed1d9-214">представление 2 цифры hello день месяца hello</span><span class="sxs-lookup"><span data-stu-id="ed1d9-214">2 digit representation of hello day of hello month</span></span>|
|<span data-ttu-id="ed1d9-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="ed1d9-215">PT1H.json</span></span>| <span data-ttu-id="ed1d9-216">Фактический файл JSON, где хранятся данные аналитики hello</span><span class="sxs-lookup"><span data-stu-id="ed1d9-216">Actual JSON file where hello analytics data is stored</span></span>|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a><span data-ttu-id="ed1d9-217">Экспорт tooa hello Core аналитические данные CSV-файла</span><span class="sxs-lookup"><span data-stu-id="ed1d9-217">Exporting hello Core Analytics Data tooa CSV File</span></span>

<span data-ttu-id="ed1d9-218">toomake ИТ легко tooaccess hello Core Analytics мы предоставляем образец кода для средства, которое пользователи могут загрузить файлы hello JSON в формат плоской CSV-файл, который можно использовать tooeasily создания диаграмм или других агрегатов.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-218">toomake it easy tooaccess hello Core Analytics, we provide a sample code for a tool, which allows downloading hello JSON files into a flat comma-separated file format, which can be used tooeasily create charts or other aggregations.</span></span>

<span data-ttu-id="ed1d9-219">Вот, как можно использовать средство hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-219">Here is how you can use hello tool:</span></span>

1.  <span data-ttu-id="ed1d9-220">Посетите ссылки hello github: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="ed1d9-220">Visit hello github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="ed1d9-221">Загрузка кода hello</span><span class="sxs-lookup"><span data-stu-id="ed1d9-221">Download hello code</span></span>
3.  <span data-ttu-id="ed1d9-222">Следуйте инструкциям toocompile и настройка</span><span class="sxs-lookup"><span data-stu-id="ed1d9-222">Follow instructions toocompile and configure</span></span>
4.  <span data-ttu-id="ed1d9-223">Запустите средство hello</span><span class="sxs-lookup"><span data-stu-id="ed1d9-223">Run hello tool</span></span>
5.  <span data-ttu-id="ed1d9-224">Полученный CSV-файл отображает данные hello analytics в простых Плоская иерархия.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-224">Resulting CSV file shows hello analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="ed1d9-225">Использование журналов диагностики из репозитория OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ed1d9-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="ed1d9-226">Аналитика журналов представляет собой службу в Operations Management Suite (OMS), отслеживающий вашего облака и локальных сред toomaintain их доступности и производительности.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments toomaintain their availability and performance.</span></span> <span data-ttu-id="ed1d9-227">Он собирает данные, созданные ресурсы в облачных и локальных сред и других мониторинга анализа tooprovide средства в нескольких источниках.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools tooprovide analysis across multiple sources.</span></span> 

<span data-ttu-id="ed1d9-228">toouse аналитики журналов должна [включить ведение журнала](#enable-logging-with-azure-storage) toohello анализа журналов OMS Azure репозитория, описанная ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-228">toouse Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) toohello Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-hello-oms-repository"></a><span data-ttu-id="ed1d9-229">С помощью hello репозиторий OMS</span><span class="sxs-lookup"><span data-stu-id="ed1d9-229">Using hello OMS Repository</span></span>

 <span data-ttu-id="ed1d9-230">Hello, следующая диаграмма показывает архитектура hello hello входов и выходов hello репозитория:</span><span class="sxs-lookup"><span data-stu-id="ed1d9-230">hello following diagram shows hello architecture of hello inputs and outputs of hello repository:</span></span>

![Репозиторий OMS Log Analytics](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="ed1d9-232">*Рисунок 3. Репозиторий OMS Log Analytics*.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="ed1d9-233">Можно отобразить hello данных различными способами с помощью решения для управления.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-233">You can display hello data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="ed1d9-234">Решения для управления можно получить из hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-234">You can obtain Management Solutions from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="ed1d9-235">Решения для управления можно установить из Azure marketplace, щелкнув hello **компания** ссылку внизу hello каждого решения.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-235">You can install management solutions from Azure marketplace by clicking hello **Get it now** link at hello bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="ed1d9-236">Добавление решения по управлению OMS CDN</span><span class="sxs-lookup"><span data-stu-id="ed1d9-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="ed1d9-237">Выполните эти шаги tooadd решением по управлению.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-237">Follow these steps tooadd a Management Solution:</span></span>

1.   <span data-ttu-id="ed1d9-238">Если это еще не сделано, вход toohello портал Azure с помощью вашей подписки Azure и перейдите tooyour панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-238">If you haven't already done so, sign in toohello Azure portal using your Azure subscription and go tooyour Dashboard.</span></span>
    <span data-ttu-id="ed1d9-239">![Панель мониторинга Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="ed1d9-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="ed1d9-240">В hello **New** колонке под **Marketplace**выберите **мониторинг + управления**.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-240">In hello **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="ed1d9-242">В hello **мониторинг + управления** колонка, щелкните **все**.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-242">In hello **Monitoring + management** blade, click **See all**.</span></span>

    ![Смотреть все](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="ed1d9-244">Поиск CDN в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-244">Search for CDN in hello search box.</span></span>

    ![Смотреть все](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="ed1d9-246">Выберите **Azure CDN Core Analytics**.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Смотреть все](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="ed1d9-248">После нажатия кнопки **создать**, появится запрос toocreate новую рабочую область OMS или используйте существующую.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-248">After clicking **Create**, you will be asked toocreate a new OMS workspace or use an existing one.</span></span> 

    ![Смотреть все](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="ed1d9-250">Выберите рабочую область hello создается до.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-250">Select hello workspace you created before.</span></span> <span data-ttu-id="ed1d9-251">Необходимо tooadd учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-251">You then need tooadd an automation account.</span></span>

    ![Смотреть все](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="ed1d9-253">Hello следующий экран показывает форму hello автоматизации учетной записи, которую необходимо заполнить.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-253">hello following screen shows hello automation account form you must fill out.</span></span> 

    ![Смотреть все](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="ed1d9-255">После создания учетной записи автоматизации hello вы являетесь готов tooadd решения.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-255">Once you have created hello automation account, you are ready tooadd your solution.</span></span> <span data-ttu-id="ed1d9-256">Нажмите кнопку hello **создать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-256">Click hello **Create** button.</span></span>

    ![Смотреть все](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="ed1d9-258">Решение теперь добавлено tooyour рабочей области.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-258">Your solution has now been added tooyour workspace.</span></span> <span data-ttu-id="ed1d9-259">Вы можете вернуться tooyour портал Azure панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-259">Go back tooyour Azure portal Dashboard.</span></span>

    ![Смотреть все](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="ed1d9-261">Щелкните рабочую область службы анализа журналов hello, вы создали toogo tooyour область.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-261">Click hello Log Analytics workspace you created toogo tooyour workspace.</span></span> 

11. <span data-ttu-id="ed1d9-262">Нажмите кнопку hello **портал OMS** плитки toosee нового решения на портале OMS hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-262">Click hello **OMS Portal** tile toosee your new solution in hello OMS portal.</span></span>

    ![Смотреть все](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="ed1d9-264">На портале OMS теперь должен выглядеть после экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="ed1d9-264">Your OMS portal should now look like hello following screen:</span></span>

    ![Смотреть все](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="ed1d9-266">Выберите один из toosee плитки приветствия несколько представлений данных.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-266">Click one of hello tiles toosee several views into your data.</span></span>

    ![Смотреть все](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="ed1d9-268">Таблицу можно прокрутить влево или вправо toosee дальнейшей плитки, представляющих отдельных представлений данных hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-268">You can scroll left or right toosee further tiles representing individual views into hello data.</span></span> 

    <span data-ttu-id="ed1d9-269">Выбрав одну из плиток hello содержатся дополнительные сведения о данных.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-269">Clicking one of hello tiles gives you more details about your data.</span></span>

     ![Смотреть все](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="ed1d9-271">Предложения и ценовые категории</span><span class="sxs-lookup"><span data-stu-id="ed1d9-271">Offers and pricing tiers</span></span>

<span data-ttu-id="ed1d9-272">Предложения и ценовые категории для решений по управлению OMS см. [здесь](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="ed1d9-273">Настройка представлений</span><span class="sxs-lookup"><span data-stu-id="ed1d9-273">Customizing views</span></span>

<span data-ttu-id="ed1d9-274">Можно настроить hello представление о ваших данных с помощью hello **конструктор представлений**.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-274">You can customize hello view into your data by using hello **View Designer**.</span></span> <span data-ttu-id="ed1d9-275">Перейдите в рабочую область OMS tooyour и начинает разрабатывать, щелкнув hello **конструктор представлений** плитки.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-275">Go tooyour OMS workspace and begin designing by clicking hello **View Designer** tile.</span></span>

![«Просмотреть конструктор»](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="ed1d9-277">Можно перетаскивать и удалять типы диаграмм слева hello и заполните сведения о данных hello требуется tooanalyze на hello слева.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-277">You can drag and drop types of charts from hello left and fill in hello data details you want tooanalyze on hello left.</span></span>

![«Просмотреть конструктор»](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="ed1d9-279">Задержка данных журнала</span><span class="sxs-lookup"><span data-stu-id="ed1d9-279">Log data delays</span></span>

<span data-ttu-id="ed1d9-280">Задержка данных журнала Verizon</span><span class="sxs-lookup"><span data-stu-id="ed1d9-280">Verizon log data delays</span></span> | <span data-ttu-id="ed1d9-281">Задержка данных журнала Akamai</span><span class="sxs-lookup"><span data-stu-id="ed1d9-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="ed1d9-282">Данные журнала Verizon откладывается 1 час и занимают toostart too2 часы, появляющиеся после завершения распространения конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-282">Verizon log data is 1 hour delayed, and take up too2 hours toostart appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="ed1d9-283">Данные журнала Akamai отложенной 24 часа и занимает toostart too2 часы, появляется ли она создана более 24 часов назад.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-283">Akamai log data is 24 hours delayed, and takes up too2 hours toostart appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="ed1d9-284">Если он был создан недавно, может занять too25 часов для появления toostart журналы hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-284">If it was recently created, it can take up too25 hours for hello logs toostart appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="ed1d9-285">Типы журналов диагностики для CDN Core Analytics</span><span class="sxs-lookup"><span data-stu-id="ed1d9-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="ed1d9-286">В настоящее время мы предлагаем только журналы аналитики основных компонентов, которые содержат метрики, показывающий статистику ответа HTTP и исходящих отображающееся hello CDN извлекает и линии.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from hello CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="ed1d9-287">Сведения о метриках основной аналитики</span><span class="sxs-lookup"><span data-stu-id="ed1d9-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="ed1d9-288">Hello в следующей таблице содержится перечень метрики недоступны в журналы аналитики Core hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-288">hello following table shows a list of metrics available in hello Core Analytics logs.</span></span> <span data-ttu-id="ed1d9-289">Не все метрики доступны у всех поставщиков, хотя различия минимальны.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="ed1d9-290">в следующей таблице также Hello указывает данная метрика доступно у поставщика.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-290">hello following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="ed1d9-291">Обратите внимание на то, что hello метрики доступны для только конечные точки CDN на которых установлена трафика.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-291">Please note that hello metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="ed1d9-292">Метрика</span><span class="sxs-lookup"><span data-stu-id="ed1d9-292">Metric</span></span>                     | <span data-ttu-id="ed1d9-293">Описание</span><span class="sxs-lookup"><span data-stu-id="ed1d9-293">Description</span></span>   | <span data-ttu-id="ed1d9-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="ed1d9-294">Verizon</span></span>  | <span data-ttu-id="ed1d9-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="ed1d9-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="ed1d9-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="ed1d9-296">RequestCountTotal</span></span>         |<span data-ttu-id="ed1d9-297">Общее количество запросов за этот период.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-297">Total number of request hits during this period</span></span>| <span data-ttu-id="ed1d9-298">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-298">Yes</span></span>  |<span data-ttu-id="ed1d9-299">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-299">Yes</span></span>   |
| <span data-ttu-id="ed1d9-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="ed1d9-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="ed1d9-301">Количество всех запросов, в результате которых вернулся код HTTP 2xx (например, 200, 202).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="ed1d9-302">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-302">Yes</span></span>  |<span data-ttu-id="ed1d9-303">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-303">Yes</span></span>   |
| <span data-ttu-id="ed1d9-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="ed1d9-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="ed1d9-305">Количество всех запросов, в результате которых вернулся код HTTP 3xx (например, 300, 302).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="ed1d9-306">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-306">Yes</span></span>  |<span data-ttu-id="ed1d9-307">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-307">Yes</span></span>   |
| <span data-ttu-id="ed1d9-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="ed1d9-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="ed1d9-309">Количество всех запросов, в результате которых вернулся код HTTP 4xx (например, 400, 404).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="ed1d9-310">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-310">Yes</span></span>   |<span data-ttu-id="ed1d9-311">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-311">Yes</span></span>   |
| <span data-ttu-id="ed1d9-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="ed1d9-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="ed1d9-313">Количество всех запросов, в результате которых вернулся код HTTP 5xx (например, 500, 504).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="ed1d9-314">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-314">Yes</span></span>  |<span data-ttu-id="ed1d9-315">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-315">Yes</span></span>   |
| <span data-ttu-id="ed1d9-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="ed1d9-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="ed1d9-317">Количество всех остальных кодов HTTP (кроме 2xx–5xx).</span><span class="sxs-lookup"><span data-stu-id="ed1d9-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="ed1d9-318">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-318">Yes</span></span>  |<span data-ttu-id="ed1d9-319">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-319">Yes</span></span>   |
| <span data-ttu-id="ed1d9-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="ed1d9-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="ed1d9-321">Количество всех запросов, в результате которых вернулся код HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="ed1d9-322">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-322">No</span></span>   |<span data-ttu-id="ed1d9-323">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-323">Yes</span></span>   |
| <span data-ttu-id="ed1d9-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="ed1d9-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="ed1d9-325">Количество всех запросов, в результате которых вернулся код HTTP 206.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="ed1d9-326">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-326">No</span></span>   |<span data-ttu-id="ed1d9-327">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-327">Yes</span></span>   |
| <span data-ttu-id="ed1d9-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="ed1d9-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="ed1d9-329">Количество всех запросов, в результате которых вернулся код HTTP 302.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="ed1d9-330">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-330">No</span></span>   |<span data-ttu-id="ed1d9-331">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-331">Yes</span></span>   |
| <span data-ttu-id="ed1d9-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="ed1d9-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="ed1d9-333">Количество всех запросов, в результате которых вернулся код HTTP 304.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="ed1d9-334">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-334">No</span></span>   |<span data-ttu-id="ed1d9-335">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-335">Yes</span></span>   |
| <span data-ttu-id="ed1d9-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="ed1d9-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="ed1d9-337">Количество всех запросов, в результате которых вернулся код HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="ed1d9-338">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-338">No</span></span>   |<span data-ttu-id="ed1d9-339">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-339">Yes</span></span>   |
| <span data-ttu-id="ed1d9-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="ed1d9-340">RequestCountCacheHit</span></span> |<span data-ttu-id="ed1d9-341">Количество всех запросов, в результате которых произошло попадание в кэш.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="ed1d9-342">Это означает, что был обработан активов hello непосредственно из toohello POP hello клиента.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-342">This means hello asset was served directly from hello POP toohello Client.</span></span>               | <span data-ttu-id="ed1d9-343">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-343">Yes</span></span>  |<span data-ttu-id="ed1d9-344">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-344">No</span></span>   |
| <span data-ttu-id="ed1d9-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="ed1d9-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="ed1d9-346">Количество всех запросов, в результате которых произошел промах кэша.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="ed1d9-347">Это означает, что активов hello не найден на клиенте toohello ближайший POP hello и поэтому был извлечен из hello источника.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-347">This means hello asset was not found on hello POP closest toohello client, and therefore was retrieved from hello Origin.</span></span>              |<span data-ttu-id="ed1d9-348">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-348">Yes</span></span>   | <span data-ttu-id="ed1d9-349">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-349">No</span></span>  |
| <span data-ttu-id="ed1d9-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="ed1d9-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="ed1d9-351">Количество всех запросов tooan активов, препятствующая кэшируемого из-за конфигурации пользователя tooa на границе hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-351">Count of all requests tooan asset that are prevented from being cached due tooa user configuration on hello edge.</span></span>              |<span data-ttu-id="ed1d9-352">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-352">Yes</span></span>   | <span data-ttu-id="ed1d9-353">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-353">No</span></span>  |
| <span data-ttu-id="ed1d9-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="ed1d9-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="ed1d9-355">Количество всех запросов tooassets, препятствующая кэширования hello активов Cache-Control и истечения срока действия заголовки, которые указывают, что его не следует кэшировать POP или клиентом hello HTTP</span><span class="sxs-lookup"><span data-stu-id="ed1d9-355">Count of all requests tooassets that are prevented from being cached by hello asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                |<span data-ttu-id="ed1d9-356">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-356">Yes</span></span>   |<span data-ttu-id="ed1d9-357">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-357">No</span></span>   |
| <span data-ttu-id="ed1d9-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="ed1d9-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="ed1d9-359">Количество всех запросов с состоянием кэша, не указанным выше.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="ed1d9-360">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-360">Yes</span></span>   | <span data-ttu-id="ed1d9-361">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-361">No</span></span>  |
| <span data-ttu-id="ed1d9-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="ed1d9-362">EgressTotal</span></span> | <span data-ttu-id="ed1d9-363">Объем передачи исходящих данных в ГБ.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="ed1d9-364">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-364">Yes</span></span>   |<span data-ttu-id="ed1d9-365">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-365">Yes</span></span>   |
| <span data-ttu-id="ed1d9-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="ed1d9-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="ed1d9-367">Объем передачи исходящих данных* для ответов с кодами состояния HTTP 2xx в ГБ.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="ed1d9-368">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-368">Yes</span></span>   |<span data-ttu-id="ed1d9-369">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-369">No</span></span>   |
| <span data-ttu-id="ed1d9-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="ed1d9-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="ed1d9-371">Объем передачи исходящих данных для ответов с кодами состояния HTTP 3xx в ГБ.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="ed1d9-372">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-372">Yes</span></span>   |<span data-ttu-id="ed1d9-373">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-373">No</span></span>   |
| <span data-ttu-id="ed1d9-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="ed1d9-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="ed1d9-375">Объем передачи исходящих данных для ответов с кодами состояния HTTP 4xx в ГБ.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="ed1d9-376">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-376">Yes</span></span>   | <span data-ttu-id="ed1d9-377">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-377">No</span></span>  |
| <span data-ttu-id="ed1d9-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="ed1d9-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="ed1d9-379">Объем передачи исходящих данных для ответов с кодами состояния HTTP 5xx в ГБ.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="ed1d9-380">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-380">Yes</span></span>   |  <span data-ttu-id="ed1d9-381">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-381">No</span></span> |
| <span data-ttu-id="ed1d9-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="ed1d9-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="ed1d9-383">Объем передачи исходящих данных для ответов с другими кодами состояния HTTP в ГБ.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="ed1d9-384">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-384">Yes</span></span>   |<span data-ttu-id="ed1d9-385">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-385">No</span></span>   |
| <span data-ttu-id="ed1d9-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="ed1d9-386">EgressCacheHit</span></span> |  <span data-ttu-id="ed1d9-387">Исходящие передачи данных для ответов, которые были доставлены непосредственно из кэша CDN hello на hello CDN извлекает и линии</span><span class="sxs-lookup"><span data-stu-id="ed1d9-387">Outbound data transfer for responses that were delivered directly from hello CDN cache on hello CDN POPs/Edges</span></span>  |<span data-ttu-id="ed1d9-388">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-388">Yes</span></span>   |  <span data-ttu-id="ed1d9-389">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-389">No</span></span> |
| <span data-ttu-id="ed1d9-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="ed1d9-390">EgressCacheMiss</span></span> | <span data-ttu-id="ed1d9-391">Передача исходящих данных для ответов, не найден на hello ближайшего POP-сервер и полученные от исходного сервера hello</span><span class="sxs-lookup"><span data-stu-id="ed1d9-391">Outbound data transfer for responses that were not found on hello nearest POP server, and retrieved from hello origin server</span></span>              |<span data-ttu-id="ed1d9-392">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-392">Yes</span></span>   |  <span data-ttu-id="ed1d9-393">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-393">No</span></span> |
| <span data-ttu-id="ed1d9-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="ed1d9-394">EgressCacheNoCache</span></span> | <span data-ttu-id="ed1d9-395">Для средств, которые предотвращаются кэширования из-за конфигурации пользователя tooa на границе hello передачи исходящих данных.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-395">Outbound data transfer for assets that are prevented from being cached due tooa user configuration on hello edge.</span></span>                |<span data-ttu-id="ed1d9-396">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-396">Yes</span></span>   |<span data-ttu-id="ed1d9-397">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-397">No</span></span>   |
| <span data-ttu-id="ed1d9-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="ed1d9-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="ed1d9-399">Передача исходящих данных для средств, которые запрещено кэш Cache-Control и Expires заголовки, которые указывают, что его не следует кэшировать POP или клиентом hello HTTP hello активов</span><span class="sxs-lookup"><span data-stu-id="ed1d9-399">Outbound data transfer for assets that are prevented from being cached by hello asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                    |<span data-ttu-id="ed1d9-400">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-400">Yes</span></span>   | <span data-ttu-id="ed1d9-401">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-401">No</span></span>  |
| <span data-ttu-id="ed1d9-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="ed1d9-402">EgressCacheOthers</span></span> |  <span data-ttu-id="ed1d9-403">Объем передачи исходящих данных для других сценариев с использованием кэша.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="ed1d9-404">Да</span><span class="sxs-lookup"><span data-stu-id="ed1d9-404">Yes</span></span>   | <span data-ttu-id="ed1d9-405">Нет</span><span class="sxs-lookup"><span data-stu-id="ed1d9-405">No</span></span>  |

<span data-ttu-id="ed1d9-406">* Исходящие данные передачи ссылается tootraffic доставлен из CDN POP серверов toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-406">*Outbound data transfer refers tootraffic delivered from CDN POP servers toohello client.</span></span>


### <a name="schema-of-hello-core-analytics-logs"></a><span data-ttu-id="ed1d9-407">Схема Core журналы аналитики hello</span><span class="sxs-lookup"><span data-stu-id="ed1d9-407">Schema of hello Core Analytics Logs</span></span> 

<span data-ttu-id="ed1d9-408">Все журналы хранятся в формате JSON, и каждая запись содержит строковые поля после hello ниже схемой:</span><span class="sxs-lookup"><span data-stu-id="ed1d9-408">All logs are stored in JSON format and each entry has string fields following hello below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="ed1d9-409">Где hello «время» представляет время начала hello границы час hello, для которой сообщается hello статистики.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-409">Where hello ‘time’ represents hello start time of hello hour boundary for which hello statistics is reported.</span></span> <span data-ttu-id="ed1d9-410">Если метрика не поддерживается поставщиком CDN, вместо значения типа double или целого числа используется значение NULL.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="ed1d9-411">Нулевое значение указывает отсутствие hello метрики, и оно отличается от значения 0.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-411">This null value indicates hello absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="ed1d9-412">Также Обратите внимание, что будет один набор показателей в домене, настроенный на конечной hello.</span><span class="sxs-lookup"><span data-stu-id="ed1d9-412">Also note that there will be one set of these metrics per domain configured on hello endpoint.</span></span>

<span data-ttu-id="ed1d9-413">Примеры свойств приведены ниже</span><span class="sxs-lookup"><span data-stu-id="ed1d9-413">Example properties below:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="ed1d9-414">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ed1d9-414">Additional resources</span></span>

* [<span data-ttu-id="ed1d9-415">Сбор и использование диагностических данных из ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="ed1d9-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="ed1d9-416">Анализ вариантов использования CDN Azure</span><span class="sxs-lookup"><span data-stu-id="ed1d9-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="ed1d9-417">Что такое Log Analytics?</span><span class="sxs-lookup"><span data-stu-id="ed1d9-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* <span data-ttu-id="ed1d9-418">[Log Analytics REST API Reference](https://docs.microsoft.com/en-us/rest/api/loganalytics) (Справочник по REST API Log Analytics)</span><span class="sxs-lookup"><span data-stu-id="ed1d9-418">[Azure Log Analytics REST API](https://docs.microsoft.com/en-us/rest/api/loganalytics)</span></span>







