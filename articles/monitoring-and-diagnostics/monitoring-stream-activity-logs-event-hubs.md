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
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a>Поток tooEvent журнал действий Azure hello концентраторы
Hello [ **журнал действий Azure** ](monitoring-overview-activity-logs.md) может передаваться в соседние приложения tooany реального времени с помощью hello встроенный параметр «Экспорт» в портале hello, или путем включения hello ИД правила шины службы в профиле журнала через hello Командлеты Azure PowerShell или Azure CLI.

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a>Что делать с журналом hello и концентраторов событий
Ниже приведены лишь несколько способов, которые можно использовать hello потоковой передачи возможность для hello журнал действий:

* **Поток систем ведения журнала и данных телеметрии производителей toothird** — со временем концентраторов событий потоковая передача будет toopipe механизм hello ваш журнал действий в сторонних систем Siem и журнала аналитические решения.
* **Построение пользовательского телеметрии и платформ ведения журнала** – Если уже имеется платформы пользовательские телеметрии или являются мысли о построении один hello высокомасштабируемых публикации подписки характер концентраторов событий позволяет tooflexibly приема hello журнал действий. [В разделе руководства Dan Rosanova toousing концентраторов событий в платформу телеметрии масштабе.](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a>Включение потоковой передачи hello журнал действий
Вы можете включить потоковую передачу hello журнал действий программно или с помощью портала hello. В любом случае вы выберете пространство имен служебной шины и политики общего доступа для этого пространства имен и концентратор событий создается в этом пространстве имен hello первый новый журнал действий событием. Если у вас пространство имен служебной шины, необходимо сначала toocreate один. Если ранее потоковой журналом событий toothis пространство имен служебной шины будет повторно hello концентратора событий, который был создан ранее. Hello общей политики доступа определяет hello разрешения, которые имеет механизм потоковой передачи hello. В настоящее время потоковой передачи концентраторов событий tooan требуется **управление**, **отправки**, и **прослушивания** разрешения. Можно создать или изменения политик доступа общего пространства имен Service Bus hello классического портала на вкладке «Настройка» hello пространства имен Service Bus. tooupdate Здравствуйте потоковой передачи журнала активности журнала профиль tooinclude, пользователь hello, изменения hello должен иметь разрешение ListKey hello в этом правиле авторизации шины службы.

Hello шины или события концентратора пространства имен службы не имеет toobe в hello той же подписке, hello подписки выпуска журналы при условии, что hello пользователь, настраивающий приветствия имеет соответствующий RBAC доступа tooboth подписок.

### <a name="via-azure-portal"></a>С помощью портала Azure
1. Перейдите toohello **журнал действий** колонки, с помощью меню hello на hello левая сторона hello портала.
   
    ![Перейдите tooActivity журнала на портале](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Нажмите кнопку hello **Экспорт** кнопку hello верхней части колонки hello.
   
    ![Кнопка экспорта на портале](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. В колонке hello, которое отображается можно выбрать hello областей, для которых вы хотите toostream события и hello пространства имен шины обслуживания в которой вы хотите toobe концентратора событий, созданные для потоковой передачи этих событий.
   
    ![Колонка экспорта журнала действий](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Нажмите кнопку **Сохранить** toosave эти параметры. Параметры Hello немедленно быть применен tooyour подписки.

### <a name="via-powershell-cmdlets"></a>С помощью командлетов PowerShell
Если профиль журнала уже существует, необходимо сначала tooremove этого профиля.

1. Используйте `Get-AzureRmLogProfile` tooidentify, если существует профиль журнала
2. В этом случае используйте `Remove-AzureRmLogProfile` tooremove его.
3. Используйте `Set-AzureRmLogProfile` toocreate профиля:

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

Hello ИД правила Service Bus представляет собой строку следующего формата: {службы шины ИД ресурса} /authorizationrules/ {имя ключа}, например 

### <a name="via-azure-cli"></a>С помощью интерфейса командной строки Azure
Если профиль журнала уже существует, необходимо сначала tooremove этого профиля.

1. Используйте `azure insights logprofile list` tooidentify, если существует профиль журнала
2. В этом случае используйте `azure insights logprofile delete` tooremove его.
3. Используйте `azure insights logprofile add` toocreate профиля:

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

Hello ИД правила Service Bus представляет собой строку следующего формата: `{service bus resource ID}/authorizationrules/{key name}`.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Как использовать данные журнала hello из концентраторов событий?
[Схема Hello для hello журнал действий доступен здесь](monitoring-overview-activity-logs.md). Каждое событие сохраняется в массиве больших двоичных объектов JSON, которые называются "записями".

## <a name="next-steps"></a>Дальнейшие действия
* [Архив hello учетной записи хранилища tooa журнал действий](monitoring-archive-activity-log.md)
* [Обзор hello hello журнал действий Azure](monitoring-overview-activity-logs.md)
* [Настройка объекта webhook для оповещений журнала действий Azure](insights-auditlog-to-webhook-email.md)

