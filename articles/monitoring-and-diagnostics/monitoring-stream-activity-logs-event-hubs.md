---
title: "Потоковая передача журнала действий Azure в концентраторы событий | Документация Майкрософт"
description: "Узнайте, как настроить потоковую передачу журнала действий Azure в концентраторы событий."
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
ms.openlocfilehash: 88c5701279f370914fac68872d67b02a7571748a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="stream-the-azure-activity-log-to-event-hubs"></a><span data-ttu-id="1627d-103">Потоковая передача журнала действий Azure в концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="1627d-103">Stream the Azure Activity Log to Event Hubs</span></span>
<span data-ttu-id="1627d-104">[**Журнал действий Azure**](monitoring-overview-activity-logs.md) можно передавать в близком к реальному времени в любое приложение. Для этого следует настроить стандартный параметр "Экспорт" на портале или включить идентификатор правила служебной шины в профиле журнала с помощью командлетов Azure PowerShell или интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="1627d-104">The [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time to any application using the built-in “Export” option in the portal, or by enabling the Service Bus Rule Id in a Log Profile via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-the-activity-log-and-event-hubs"></a><span data-ttu-id="1627d-105">Что можно делать с журналом действий и концентраторами событий</span><span class="sxs-lookup"><span data-stu-id="1627d-105">What you can do with the Activity Log and Event Hubs</span></span>
<span data-ttu-id="1627d-106">Мы приведем лишь несколько примеров использования потоковой передачи журнала действий.</span><span class="sxs-lookup"><span data-stu-id="1627d-106">Here are just a few ways you might use the streaming capability for the Activity Log:</span></span>

* <span data-ttu-id="1627d-107">**Потоковая передача в сторонние системы ведения журналов и сбора телеметрии.** Через некоторое время концентраторы событий будут использоваться для передачи журнала действий в сторонние решения SIEM и решения для анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="1627d-107">**Stream to third-party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="1627d-108">**Создание пользовательской платформы для телеметрии и ведения журнала.** Если у вас уже есть пользовательская платформа для телеметрии и ведения журнала или вы только планируете ее создать, высокая масштабируемость публикации и подписки концентраторов событий позволит вам гибко настраивать прием журнала действий.</span><span class="sxs-lookup"><span data-stu-id="1627d-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest the activity log.</span></span> [<span data-ttu-id="1627d-109">Ознакомьтесь с руководством Дэна Росановы (Dan Rosanova) по использованию концентраторов событий для глобальной платформы телеметрии.</span><span class="sxs-lookup"><span data-stu-id="1627d-109">See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-the-activity-log"></a><span data-ttu-id="1627d-110">Включение потоковой передачи журнала действий</span><span class="sxs-lookup"><span data-stu-id="1627d-110">Enable streaming of the Activity Log</span></span>
<span data-ttu-id="1627d-111">Потоковую передачу журнала действий можно включить программно или с помощью портала.</span><span class="sxs-lookup"><span data-stu-id="1627d-111">You can enable streaming of the Activity Log either programmatically or via the portal.</span></span> <span data-ttu-id="1627d-112">В любом случае необходимо выбрать пространство имен служебной шины и политику общего доступа для него, после чего при возникновении нового события журнала действий в этом пространстве имен создается концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="1627d-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when the first new Activity Log event occurs.</span></span> <span data-ttu-id="1627d-113">Если у вас нет пространства имен служебной шины, необходимо сначала создать его.</span><span class="sxs-lookup"><span data-stu-id="1627d-113">If you do not have a Service Bus Namespace, you first need to create one.</span></span> <span data-ttu-id="1627d-114">Если потоковая передача событий журнала действий уже выполнялась в это пространство имен служебной шины, созданный ранее концентратор событий будет использован повторно.</span><span class="sxs-lookup"><span data-stu-id="1627d-114">If you have previously streamed Activity Log events to this Service Bus Namespace, the Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="1627d-115">Политика общего доступа определяет разрешения, предоставленные для механизма потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="1627d-115">The shared access policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="1627d-116">В настоящее время для потоковой передачи журналов в концентраторы событий нужны разрешения **Управление**, **Отправка** и **Прослушивание**.</span><span class="sxs-lookup"><span data-stu-id="1627d-116">Today, streaming to an Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="1627d-117">Политики общего доступа для пространства имен служебной шины можно создать или изменить на классическом портале на вкладке "Настройка" для пространства имен служебной шины.</span><span class="sxs-lookup"><span data-stu-id="1627d-117">You can create or modify Service Bus Namespace shared access policies in the classic portal under the “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="1627d-118">Чтобы изменить профиль журнала действий и разрешить потоковую передачу, пользователь, который вносит изменение, должен иметь разрешение ListKey для правила авторизации служебной шины.</span><span class="sxs-lookup"><span data-stu-id="1627d-118">To update the Activity Log log profile to include streaming, the user making the change must have the ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="1627d-119">Служебная шина или пространство имен концентратора событий не обязательно должны находиться в той самой подписке, в которой создаются журналы, если у пользователя, настраивающего параметр, имеется соответствующий доступ RBAC к обеим подпискам.</span><span class="sxs-lookup"><span data-stu-id="1627d-119">The service bus or event hub namespace does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="1627d-120">С помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="1627d-120">Via Azure portal</span></span>
1. <span data-ttu-id="1627d-121">Перейдите к колонке **Журнал действий** с помощью меню в левой части портала.</span><span class="sxs-lookup"><span data-stu-id="1627d-121">Navigate to the **Activity Log** blade using the menu on the left side of the portal.</span></span>
   
    ![Переход к журналу действий на портале](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="1627d-123">Нажмите кнопку **Экспорт** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="1627d-123">Click the **Export** button at the top of the blade.</span></span>
   
    ![Кнопка экспорта на портале](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="1627d-125">Откроется колонка, в которой вы можете выбрать регионы, для которых нужно выполнять передачу событий, и пространство имен служебной шины, в котором вы хотите создать концентратор событий для потоковой передачи этих событий.</span><span class="sxs-lookup"><span data-stu-id="1627d-125">In the blade that appears, you can select the regions for which you would like to stream events and the Service Bus Namespace in which you would like an Event Hub to be created for streaming these events.</span></span>
   
    ![Колонка экспорта журнала действий](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="1627d-127">Нажмите кнопку **Сохранить** , чтобы сохранить эти параметры.</span><span class="sxs-lookup"><span data-stu-id="1627d-127">Click **Save** to save these settings.</span></span> <span data-ttu-id="1627d-128">Параметры будут немедленно применены к подписке</span><span class="sxs-lookup"><span data-stu-id="1627d-128">The settings are immediately be applied to your subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="1627d-129">С помощью командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="1627d-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="1627d-130">Если профиль журнала уже существует, следует сначала удалить этот профиль.</span><span class="sxs-lookup"><span data-stu-id="1627d-130">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="1627d-131">Используйте `Get-AzureRmLogProfile` , чтобы проверить, существует ли профиль журнала.</span><span class="sxs-lookup"><span data-stu-id="1627d-131">Use `Get-AzureRmLogProfile` to identify if a log profile exists</span></span>
2. <span data-ttu-id="1627d-132">Если он есть, используйте `Remove-AzureRmLogProfile` , чтобы удалить его.</span><span class="sxs-lookup"><span data-stu-id="1627d-132">If so, use `Remove-AzureRmLogProfile` to remove it.</span></span>
3. <span data-ttu-id="1627d-133">Используйте `Set-AzureRmLogProfile`, чтобы создать профиль:</span><span class="sxs-lookup"><span data-stu-id="1627d-133">Use `Set-AzureRmLogProfile` to create a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="1627d-134">ServiceBusRuleID — это строка в таком формате: {идентификатор_ресурса_служебной_шины} /authorizationrules/{имя_ключа}. Например:</span><span class="sxs-lookup"><span data-stu-id="1627d-134">The Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="1627d-135">С помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="1627d-135">Via Azure CLI</span></span>
<span data-ttu-id="1627d-136">Если профиль журнала уже существует, следует сначала удалить этот профиль.</span><span class="sxs-lookup"><span data-stu-id="1627d-136">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="1627d-137">Используйте `azure insights logprofile list` , чтобы проверить, существует ли профиль журнала.</span><span class="sxs-lookup"><span data-stu-id="1627d-137">Use `azure insights logprofile list` to identify if a log profile exists</span></span>
2. <span data-ttu-id="1627d-138">Если он есть, используйте `azure insights logprofile delete` , чтобы удалить его.</span><span class="sxs-lookup"><span data-stu-id="1627d-138">If so, use `azure insights logprofile delete` to remove it.</span></span>
3. <span data-ttu-id="1627d-139">Используйте `azure insights logprofile add` , чтобы создать профиль:</span><span class="sxs-lookup"><span data-stu-id="1627d-139">Use `azure insights logprofile add` to create a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="1627d-140">ServiceBusRuleID — это строка в таком формате: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="1627d-140">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="1627d-141">Как используются данные журнала из концентраторов событий?</span><span class="sxs-lookup"><span data-stu-id="1627d-141">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="1627d-142">Схема для журнала действий доступна [здесь](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="1627d-142">[The schema for the Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="1627d-143">Каждое событие сохраняется в массиве больших двоичных объектов JSON, которые называются "записями".</span><span class="sxs-lookup"><span data-stu-id="1627d-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="1627d-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1627d-144">Next Steps</span></span>
* [<span data-ttu-id="1627d-145">Архивация журнала действий Azure</span><span class="sxs-lookup"><span data-stu-id="1627d-145">Archive the Activity Log to a storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="1627d-146">Общие сведения о журнале действий Azure</span><span class="sxs-lookup"><span data-stu-id="1627d-146">Read the overview of the Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="1627d-147">Настройка объекта webhook для оповещений журнала действий Azure</span><span class="sxs-lookup"><span data-stu-id="1627d-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

