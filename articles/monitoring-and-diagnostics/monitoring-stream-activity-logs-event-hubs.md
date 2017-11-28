---
title: "aaaStream hello журнал действий Azure tooEvent концентраторов | Документы Microsoft"
description: "Узнайте, как toostream hello tooEvent журнал действий Azure концентраторов."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a><span data-ttu-id="25e18-103">Поток tooEvent журнал действий Azure hello концентраторы</span><span class="sxs-lookup"><span data-stu-id="25e18-103">Stream hello Azure Activity Log tooEvent Hubs</span></span>
<span data-ttu-id="25e18-104">Hello [ **журнал действий Azure** ](monitoring-overview-activity-logs.md) может передаваться в соседние приложения tooany реального времени с помощью hello встроенный параметр «Экспорт» в портале hello, или путем включения hello ИД правила шины службы в профиле журнала через hello Командлеты Azure PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="25e18-104">hello [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time tooany application using hello built-in “Export” option in hello portal, or by enabling hello Service Bus Rule Id in a Log Profile via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a><span data-ttu-id="25e18-105">Что делать с журналом hello и концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="25e18-105">What you can do with hello Activity Log and Event Hubs</span></span>
<span data-ttu-id="25e18-106">Ниже приведены лишь несколько способов, которые можно использовать hello потоковой передачи возможность для hello журнал действий:</span><span class="sxs-lookup"><span data-stu-id="25e18-106">Here are just a few ways you might use hello streaming capability for hello Activity Log:</span></span>

* <span data-ttu-id="25e18-107">**Поток систем ведения журнала и данных телеметрии производителей toothird** — со временем концентраторов событий потоковая передача будет toopipe механизм hello ваш журнал действий в сторонних систем Siem и журнала аналитические решения.</span><span class="sxs-lookup"><span data-stu-id="25e18-107">**Stream toothird-party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="25e18-108">**Построение пользовательского телеметрии и платформ ведения журнала** – Если уже имеется платформы пользовательские телеметрии или являются мысли о построении один hello высокомасштабируемых публикации подписки характер концентраторов событий позволяет tooflexibly приема hello журнал действий.</span><span class="sxs-lookup"><span data-stu-id="25e18-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest hello activity log.</span></span> [<span data-ttu-id="25e18-109">В разделе руководства Dan Rosanova toousing концентраторов событий в платформу телеметрии масштабе.</span><span class="sxs-lookup"><span data-stu-id="25e18-109">See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a><span data-ttu-id="25e18-110">Включение потоковой передачи hello журнал действий</span><span class="sxs-lookup"><span data-stu-id="25e18-110">Enable streaming of hello Activity Log</span></span>
<span data-ttu-id="25e18-111">Вы можете включить потоковую передачу hello журнал действий программно или с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="25e18-111">You can enable streaming of hello Activity Log either programmatically or via hello portal.</span></span> <span data-ttu-id="25e18-112">В любом случае вы выберете пространство имен служебной шины и политики общего доступа для этого пространства имен и концентратор событий создается в этом пространстве имен hello первый новый журнал действий событием.</span><span class="sxs-lookup"><span data-stu-id="25e18-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when hello first new Activity Log event occurs.</span></span> <span data-ttu-id="25e18-113">Если у вас пространство имен служебной шины, необходимо сначала toocreate один.</span><span class="sxs-lookup"><span data-stu-id="25e18-113">If you do not have a Service Bus Namespace, you first need toocreate one.</span></span> <span data-ttu-id="25e18-114">Если ранее потоковой журналом событий toothis пространство имен служебной шины будет повторно hello концентратора событий, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="25e18-114">If you have previously streamed Activity Log events toothis Service Bus Namespace, hello Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="25e18-115">Hello общей политики доступа определяет hello разрешения, которые имеет механизм потоковой передачи hello.</span><span class="sxs-lookup"><span data-stu-id="25e18-115">hello shared access policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="25e18-116">В настоящее время потоковой передачи концентраторов событий tooan требуется **управление**, **отправки**, и **прослушивания** разрешения.</span><span class="sxs-lookup"><span data-stu-id="25e18-116">Today, streaming tooan Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="25e18-117">Можно создать или изменения политик доступа общего пространства имен Service Bus hello классического портала на вкладке «Настройка» hello пространства имен Service Bus.</span><span class="sxs-lookup"><span data-stu-id="25e18-117">You can create or modify Service Bus Namespace shared access policies in hello classic portal under hello “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="25e18-118">tooupdate Здравствуйте потоковой передачи журнала активности журнала профиль tooinclude, пользователь hello, изменения hello должен иметь разрешение ListKey hello в этом правиле авторизации шины службы.</span><span class="sxs-lookup"><span data-stu-id="25e18-118">tooupdate hello Activity Log log profile tooinclude streaming, hello user making hello change must have hello ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="25e18-119">Hello шины или события концентратора пространства имен службы не имеет toobe в hello той же подписке, hello подписки выпуска журналы при условии, что hello пользователь, настраивающий приветствия имеет соответствующий RBAC доступа tooboth подписок.</span><span class="sxs-lookup"><span data-stu-id="25e18-119">hello service bus or event hub namespace does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="25e18-120">С помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="25e18-120">Via Azure portal</span></span>
1. <span data-ttu-id="25e18-121">Перейдите toohello **журнал действий** колонки, с помощью меню hello на hello левая сторона hello портала.</span><span class="sxs-lookup"><span data-stu-id="25e18-121">Navigate toohello **Activity Log** blade using hello menu on hello left side of hello portal.</span></span>
   
    ![Перейдите tooActivity журнала на портале](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="25e18-123">Нажмите кнопку hello **Экспорт** кнопку hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="25e18-123">Click hello **Export** button at hello top of hello blade.</span></span>
   
    ![Кнопка экспорта на портале](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="25e18-125">В колонке hello, которое отображается можно выбрать hello областей, для которых вы хотите toostream события и hello пространства имен шины обслуживания в которой вы хотите toobe концентратора событий, созданные для потоковой передачи этих событий.</span><span class="sxs-lookup"><span data-stu-id="25e18-125">In hello blade that appears, you can select hello regions for which you would like toostream events and hello Service Bus Namespace in which you would like an Event Hub toobe created for streaming these events.</span></span>
   
    ![Колонка экспорта журнала действий](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="25e18-127">Нажмите кнопку **Сохранить** toosave эти параметры.</span><span class="sxs-lookup"><span data-stu-id="25e18-127">Click **Save** toosave these settings.</span></span> <span data-ttu-id="25e18-128">Параметры Hello немедленно быть применен tooyour подписки.</span><span class="sxs-lookup"><span data-stu-id="25e18-128">hello settings are immediately be applied tooyour subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="25e18-129">С помощью командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="25e18-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="25e18-130">Если профиль журнала уже существует, необходимо сначала tooremove этого профиля.</span><span class="sxs-lookup"><span data-stu-id="25e18-130">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="25e18-131">Используйте `Get-AzureRmLogProfile` tooidentify, если существует профиль журнала</span><span class="sxs-lookup"><span data-stu-id="25e18-131">Use `Get-AzureRmLogProfile` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="25e18-132">В этом случае используйте `Remove-AzureRmLogProfile` tooremove его.</span><span class="sxs-lookup"><span data-stu-id="25e18-132">If so, use `Remove-AzureRmLogProfile` tooremove it.</span></span>
3. <span data-ttu-id="25e18-133">Используйте `Set-AzureRmLogProfile` toocreate профиля:</span><span class="sxs-lookup"><span data-stu-id="25e18-133">Use `Set-AzureRmLogProfile` toocreate a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="25e18-134">Hello ИД правила Service Bus представляет собой строку следующего формата: {службы шины ИД ресурса} /authorizationrules/ {имя ключа}, например</span><span class="sxs-lookup"><span data-stu-id="25e18-134">hello Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="25e18-135">С помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="25e18-135">Via Azure CLI</span></span>
<span data-ttu-id="25e18-136">Если профиль журнала уже существует, необходимо сначала tooremove этого профиля.</span><span class="sxs-lookup"><span data-stu-id="25e18-136">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="25e18-137">Используйте `azure insights logprofile list` tooidentify, если существует профиль журнала</span><span class="sxs-lookup"><span data-stu-id="25e18-137">Use `azure insights logprofile list` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="25e18-138">В этом случае используйте `azure insights logprofile delete` tooremove его.</span><span class="sxs-lookup"><span data-stu-id="25e18-138">If so, use `azure insights logprofile delete` tooremove it.</span></span>
3. <span data-ttu-id="25e18-139">Используйте `azure insights logprofile add` toocreate профиля:</span><span class="sxs-lookup"><span data-stu-id="25e18-139">Use `azure insights logprofile add` toocreate a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="25e18-140">Hello ИД правила Service Bus представляет собой строку следующего формата: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="25e18-140">hello Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="25e18-141">Как использовать данные журнала hello из концентраторов событий?</span><span class="sxs-lookup"><span data-stu-id="25e18-141">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="25e18-142">[Схема Hello для hello журнал действий доступен здесь](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="25e18-142">[hello schema for hello Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="25e18-143">Каждое событие сохраняется в массиве больших двоичных объектов JSON, которые называются "записями".</span><span class="sxs-lookup"><span data-stu-id="25e18-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="25e18-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="25e18-144">Next Steps</span></span>
* [<span data-ttu-id="25e18-145">Архив hello учетной записи хранилища tooa журнал действий</span><span class="sxs-lookup"><span data-stu-id="25e18-145">Archive hello Activity Log tooa storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="25e18-146">Обзор hello hello журнал действий Azure</span><span class="sxs-lookup"><span data-stu-id="25e18-146">Read hello overview of hello Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="25e18-147">Настройка объекта webhook для оповещений журнала действий Azure</span><span class="sxs-lookup"><span data-stu-id="25e18-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

