---
title: "образцы aaaAzure 1.0 CLI монитор быстрого запуска. | Документация Майкрософт"
description: "Примеры команд интерфейса командной строки 1.0 для функций Azure Monitor. Монитор Azure — это служба Microsoft Azure, позволяющий toosend уведомления о предупреждениях, вызов URL-адресов на основе значений данных телеметрии настроенное и автоматического масштабирования облачных служб, виртуальных машин и веб-приложений."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="acd1a-105">Примеры команд для кроссплатформенного интерфейса командной строки 1.0 в Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="acd1a-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="acd1a-106">Это статье показывает образец доступ возможностях монитора Azure toohelp команды командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="acd1a-106">This article shows you sample command-line interface (CLI) commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="acd1a-107">Монитор Azure позволяет tooAutoScale облачных служб, виртуальных машин и веб-приложений и toosend уведомлений или вызов веб-адреса на основе значений данных телеметрии, настроенных.</span><span class="sxs-lookup"><span data-stu-id="acd1a-107">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="acd1a-108">Монитор Azure — новое имя hello что был вызван «Azure Insights» до 25 сентября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="acd1a-108">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="acd1a-109">Однако hello пространств имен и поэтому приведенную ниже команду hello по-прежнему содержать аналитики «hello».</span><span class="sxs-lookup"><span data-stu-id="acd1a-109">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="acd1a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="acd1a-110">Prerequisites</span></span>
<span data-ttu-id="acd1a-111">Если вы еще не установили hello Azure CLI, см. раздел [Install hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="acd1a-111">If you haven't already installed hello Azure CLI, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="acd1a-112">Если вы знакомы с Azure CLI, вы можете прочитать больше о нем в [используйте hello Azure CLI для Mac, Linux и Windows с помощью диспетчера ресурсов Azure](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="acd1a-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="acd1a-113">В Windows, необходимо установить npm с hello [Node.js веб-сайт](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="acd1a-113">In Windows, install npm from hello [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="acd1a-114">После завершения установки hello, с помощью CMD.exe с правами на запуск от имени администратора, выполните следующие hello из hello папку для установки npm:</span><span class="sxs-lookup"><span data-stu-id="acd1a-114">After you complete hello installation, using CMD.exe with Run As Administrator privileges, execute hello following from hello folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="acd1a-115">Далее перейдите tooany/расположение папки нужно и введите в hello командной строки:</span><span class="sxs-lookup"><span data-stu-id="acd1a-115">Next, navigate tooany folder/location you want and type at hello command-line:</span></span>

```console
azure help
```

## <a name="log-in-tooazure"></a><span data-ttu-id="acd1a-116">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="acd1a-116">Log in tooAzure</span></span>
<span data-ttu-id="acd1a-117">Hello первым шагом является toologin tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="acd1a-117">hello first step is toologin tooyour Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="acd1a-118">После выполнения этой команды, у вас toosign в через hello инструкциям на экране приветствия.</span><span class="sxs-lookup"><span data-stu-id="acd1a-118">After running this command, you have toosign in via hello instructions on hello screen.</span></span> <span data-ttu-id="acd1a-119">После этого вы увидите учетную запись, идентификатор клиента и идентификатор подписки по умолчанию. Все команды работают в контексте hello подписки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="acd1a-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in hello context of your default subscription.</span></span>

<span data-ttu-id="acd1a-120">hello toolist подробные сведения о вашей текущей подписки hello используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="acd1a-120">toolist hello details of your current subscription, use hello following command.</span></span>

```console
azure account show
```

<span data-ttu-id="acd1a-121">toochange рабочий контекст tooa другую подписку, hello используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="acd1a-121">toochange working context tooa different subscription, use hello following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="acd1a-122">toouse диспетчер ресурсов Azure и Azure монитора команд, требуется toobe в режим диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="acd1a-122">toouse Azure Resource Manager and Azure Monitor commands, you need toobe in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="acd1a-123">tooview список всех поддерживаемых команд монитора Azure, выполните следующие hello.</span><span class="sxs-lookup"><span data-stu-id="acd1a-123">tooview a list of all supported Azure Monitor commands, perform hello following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="acd1a-124">Просмотр журнала действий для подписки</span><span class="sxs-lookup"><span data-stu-id="acd1a-124">View activity log for a subscription</span></span>
<span data-ttu-id="acd1a-125">tooview список событий журнала действий, выполните следующие hello.</span><span class="sxs-lookup"><span data-stu-id="acd1a-125">tooview a list of activity log events, perform hello following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="acd1a-126">Попробуйте следующие tooview hello все доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="acd1a-126">Try hello following tooview all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="acd1a-127">Ниже приведен пример toolist журналы в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="acd1a-127">Here is an example toolist logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="acd1a-128">Пример toolist журналы вызывающим объектом</span><span class="sxs-lookup"><span data-stu-id="acd1a-128">Example toolist logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="acd1a-129">Пример toolist журналы вызывающим на тип ресурса в дату начала и окончания</span><span class="sxs-lookup"><span data-stu-id="acd1a-129">Example toolist logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="acd1a-130">Работа с оповещениями</span><span class="sxs-lookup"><span data-stu-id="acd1a-130">Work with alerts</span></span>
<span data-ttu-id="acd1a-131">Можно использовать сведения hello в toowork разделе hello с предупреждениями.</span><span class="sxs-lookup"><span data-stu-id="acd1a-131">You can use hello information in hello section toowork with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="acd1a-132">Получение правил генерации оповещений в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="acd1a-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="acd1a-133">Создание правила генерации оповещения для метрики</span><span class="sxs-lookup"><span data-stu-id="acd1a-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="acd1a-134">Создание правила генерации оповещения для веб-теста</span><span class="sxs-lookup"><span data-stu-id="acd1a-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="acd1a-135">Удаление правила генерации оповещения</span><span class="sxs-lookup"><span data-stu-id="acd1a-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="acd1a-136">Профили журнала</span><span class="sxs-lookup"><span data-stu-id="acd1a-136">Log profiles</span></span>
<span data-ttu-id="acd1a-137">Используйте hello информацию из этого раздела toowork с профилями журнала.</span><span class="sxs-lookup"><span data-stu-id="acd1a-137">Use hello information in this section toowork with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="acd1a-138">Получение профиля журнала</span><span class="sxs-lookup"><span data-stu-id="acd1a-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="acd1a-139">Добавление профиля журнала без хранения</span><span class="sxs-lookup"><span data-stu-id="acd1a-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="acd1a-140">Удаление профиля журнала</span><span class="sxs-lookup"><span data-stu-id="acd1a-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="acd1a-141">Добавление профиля журнала с хранением</span><span class="sxs-lookup"><span data-stu-id="acd1a-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="acd1a-142">Добавление профиля журнала с хранением и концентратором событий</span><span class="sxs-lookup"><span data-stu-id="acd1a-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="acd1a-143">Диагностика</span><span class="sxs-lookup"><span data-stu-id="acd1a-143">Diagnostics</span></span>
<span data-ttu-id="acd1a-144">Используйте hello информацию из этого раздела toowork с параметров диагностики.</span><span class="sxs-lookup"><span data-stu-id="acd1a-144">Use hello information in this section toowork with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="acd1a-145">Получение параметра диагностики</span><span class="sxs-lookup"><span data-stu-id="acd1a-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="acd1a-146">Отключение параметра диагностики</span><span class="sxs-lookup"><span data-stu-id="acd1a-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="acd1a-147">Включение параметра диагностики без хранения</span><span class="sxs-lookup"><span data-stu-id="acd1a-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="acd1a-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="acd1a-148">Autoscale</span></span>
<span data-ttu-id="acd1a-149">Используйте hello информацию из этого раздела toowork с параметрами автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="acd1a-149">Use hello information in this section toowork with autoscale settings.</span></span> <span data-ttu-id="acd1a-150">Необходимо toomodify этих примеров.</span><span class="sxs-lookup"><span data-stu-id="acd1a-150">You need toomodify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="acd1a-151">Получение параметров автомасштабирования для группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="acd1a-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="acd1a-152">Получение параметров автомасштабирования по имени в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="acd1a-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="acd1a-153">Установка параметров автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="acd1a-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
