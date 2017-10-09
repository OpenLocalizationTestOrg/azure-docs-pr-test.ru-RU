---
title: "aaaGet работы с ролями, разрешения и безопасности с помощью монитора Azure | Документы Microsoft"
description: "Узнайте, как встроенные роли и разрешения toorestrict монитора toouse Azure доступ к ресурсам toomonitoring."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a>Приступая к работе с ролями, разрешениями и системой безопасности с помощью Azure Monitor
Многие команды требуется toostrictly регулировать доступ toomonitoring данные и параметры. Например, если участники команды, работающие только на наблюдение за (инженеры службы поддержки, специалисты devops) или если используется поставщик управляемых услуг, вы можете toogrant им доступа tooonly наблюдение за данными, ограничивая их возможности toocreate при, изменить, или Удаление ресурсов. В этой статье показано, как tooquickly применяются встроенные мониторинга RBAC роли tooa пользователя в Azure или построить пользовательские роли для пользователя, которому ограниченные разрешения для мониторинга. Он затем рассматриваются вопросы безопасности для ресурсов, связанных с монитором Azure и как можно ограничить доступ к данным toohello они содержат.

## <a name="built-in-monitoring-roles"></a>Встроенные роли мониторинга
Встроенные роли Azure монитор отвечают спроектированный toohelp ограничение доступа tooresources в подписке, то же время позволяя те, для мониторинга инфраструктуры tooobtain и настройте hello данные, которые им необходимы. Azure Monitor предоставляет две готовые роли: Monitoring Reader и Monitoring Contributor.

### <a name="monitoring-reader"></a>Роль Monitoring Reader
Назначить роль чтения мониторинга hello людей можно просматривать все данные наблюдения в подписке, но нельзя изменить любой ресурс или изменить какие-либо параметры toomonitoring связанные ресурсы. Эту роль подходит для пользователей в организации, например операций или поддержки инженеров, которым требуется возможность toobe:

* Просмотр информационных панелей мониторинга портала hello и создать свои собственные закрытый информационных панелей мониторинга.
* Запрос для метрик с помощью hello [API REST Azure монитор](https://msdn.microsoft.com/library/azure/dn931930.aspx), [командлеты PowerShell](insights-powershell-samples.md), или [CLI кросс платформенных](insights-cli-samples.md).
* Запрос hello журнал действий с помощью портала hello, API REST Azure монитор, командлеты PowerShell или кросс платформенных CLI.
* Представление hello [параметров диагностики](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) для ресурса.
* Представление hello [входа профиль](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) для подписки.
* Просмотр параметров автомасштабирования.
* Просмотр действий и параметров оповещений.
* Доступ к данным Application Insights и просмотр данных в Application Insights Analytics.
* Поиск данных рабочей области анализа журналов (OMS), включая данные об использовании для hello рабочей области.
* Просмотр групп управления Log Analytics (OMS).
* Получить схему поиска hello аналитика журналов (OMS).
* Вывод списка пакетов интеллектуализации Log Analytics (OMS).
* Извлечение и выполнение сохраненных поисков Log Analytics (OMS).
* Получить конфигурацию хранилища hello аналитика журналов (OMS).

> [!NOTE]
> Эта роль не позволяет получить данные toolog доступ для чтения потоковых tooan концентратора событий или хранятся в учетной записи хранилища. [См. ниже](#security-considerations-for-monitoring-data) сведения о настройке доступа к ресурсам toothese.
> 
> 

### <a name="monitoring-contributor"></a>Monitoring Contributor
Сотрудникам hello мониторинга участника роли могут просматривать все данные мониторинга для подписки и создать или изменить параметры наблюдения, но также могут изменять другие ресурсы. Эта роль является надмножеством роль чтения мониторинга hello и подходит для членов группы мониторинга и управляемые поставщики служб, кроме разрешения toohello выше, также должны toobe возможность организации:

* Публикация панелей мониторинга для совместного использования.
* Настройка [параметров диагностики](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) для ресурса.*
* Набор hello [входа профиль](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) для subscription.*
* Настройка действий и параметров оповещений.
* Создание веб-тестов и компонентов Application Insights.
* Вывод списка общих ключей рабочей области Log Analytics (OMS).
* Включение или отключение пакетов интеллектуализации Log Analytics (OMS).
* Создание и удаление сохраненных поисков Log Analytics (OMS).
* Создание и удаление конфигурации хранилища hello аналитика журналов (OMS).

* пользователя отдельно также должно быть предоставлено разрешение ListKeys hello целевого ресурса (хранилища учетной записи или событие пространство имен концентратора) tooset профиля журнала или параметра диагностики.

> [!NOTE]
> Эта роль не позволяет получить данные toolog доступ для чтения потоковых tooan концентратора событий или хранятся в учетной записи хранилища. [См. ниже](#security-considerations-for-monitoring-data) сведения о настройке доступа к ресурсам toothese.
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a>Разрешения мониторинга и настраиваемые роли RBAC
Если hello выше встроенных ролей не отвечают hello потребностей вашей команды, вы можете [Создание пользовательской роли RBAC](../active-directory/role-based-access-control-custom-roles.md) с более детализированные разрешения. Ниже приведены hello общих операций Azure монитор RBAC с описаниями.

| Операция | Описание |
| --- | --- |
| Microsoft.Insights/AlertRules/[Read, Write, Delete] |Чтение, запись и удаление правила генерации оповещений. |
| Microsoft.Insights/AlertRules/Incidents/Read |Список инцидентов (журнал запустилась правило генерации оповещений hello) для правил оповещения. Это относится только toohello портала. |
| Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete] |Чтение, запись и удаление параметров автомасштабирования. |
| Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete] |Чтение, запись и удаление параметров диагностики. |
| Microsoft.Insights/eventtypes/digestevents/Read |Это разрешение необходимо для пользователей, которым требуется доступ к журналам tooActivity через портал hello. |
| Microsoft.Insights/eventtypes/values/Read |Вывод списка событий журнала действий (событий управления) в подписке. Это разрешение — программный и портала доступ применимо tooboth toohello журнал действий. |
| Microsoft.Insights/LogDefinitions/Read |Это разрешение необходимо для пользователей, которым требуется доступ к журналам tooActivity через портал hello. |
| Microsoft.Insights/MetricDefinitions/Read |Чтение определений метрик (вывод списка доступных типов метрик для ресурса). |
| Microsoft.Insights/Metrics/Read |Чтение метрик для ресурса. |

> [!NOTE]
> Tooalerts доступ, параметры диагностики и метрики для ресурса требуется этот hello пользователь имеет доступ на чтение toohello ресурса типа и области действия ресурса. Создание («написать отзыв») диагностики параметр журнала профиль или что архивы tooa хранилища учетной записи или в потоки tooevent концентраторов требует tooalso пользователя hello разрешение ListKeys на hello целевого ресурса.
> 
> 

Например с помощью hello над таблицей удалось создать пользовательской роли RBAC «действие чтения журнала» следующим образом:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a>Вопросы безопасности данных мониторинга
Данные мониторинга, в особенности файлы журналов, могут содержать конфиденциальные сведения, такие как IP-адреса или имена пользователей. Данные мониторинга поступают из Azure в трех основных формах:

1. Здравствуйте, журнал действий, который описывает все действия плоскости управления в своей подписке Azure.
2. журналы диагностики, выдаваемые ресурсом;
3. метрики, выдаваемые ресурсами.

Все три из этих типов данных может храниться в учетной записи хранилища, или передавать их потоком tooEvent концентратора, которые являются общего назначения ресурсов Azure. Так как это универсальные ресурсы, то их создание, удаление и доступ к ним являются привилегированными операциями, которые обычно зарезервированы для администратора. Мы рекомендуем использовать методы неправильное использование ресурсов, связанных с мониторингом tooprevent hello:

* Используйте отдельную учетную запись хранения для данных мониторинга. Если вам требуется tooseparate данных мониторинга на несколько учетных записей хранилища, никогда не используют использование учетной записи хранилища между мониторинга и данные, отличных от наблюдения, что случайно дать тех, кто только требуется доступ к данным toomonitoring (например) сторонние SIEM) доступ к данным мониторинга toonon.
* Используйте единый, выделенных имен Service Bus или концентратор событий во всех параметров диагностики для hello же причинам, как описано выше.
* Ограничения, сохраняя их в отдельной группе ресурсов, учетные записи хранения, связанные с toomonitoring доступа или концентраторов событий и [использовать область](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) на ролях мониторинга toolimit получить доступ к tooonly данной группы ресурсов.
* Предоставьте разрешение ListKeys hello учетным записям хранения или концентраторов событий в области видимости подписки никогда не в том случае, когда пользователю требуется только доступ к данным toomonitoring. Вместо этого предоставьте пользователя toohello эти разрешения на ресурс или группа ресурсов (если имеется отдельная группа ресурсов мониторинга) области.

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a>Ограничение учетных записей хранения, связанные с toomonitoring доступа
Когда пользователь или приложение должно получить доступ к toomonitoring данные в учетной записи хранилища, следует [создать SAS для учетной записи](https://msdn.microsoft.com/library/azure/mt584140.aspx) в учетной записи хранения hello, содержащий данные наблюдения с хранилищем tooblob доступа только для чтения на уровне службы. В PowerShell это может выглядеть следующим образом.

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

После этого можно предоставить hello маркера toohello сущность, которая должна tooread из этой учетной записи хранилища, и его можно перечислить и считывать все большие двоичные объекты в этой учетной записи хранения.

Кроме того при необходимости это разрешение с помощью RBAC toocontrol можно предоставить этой сущности hello Microsoft.Storage/storageAccounts/listkeys/action разрешение для этой учетной записи. Это необходимо для пользователей, которым нужно будет tooset toobe диагностики параметр или журнала профиль tooarchive tooa учетной записи хранилища. Например можно создать следующие пользовательские RBAC роль для пользователя или приложения, нужно только tooread из одну учетную запись хранения hello:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> Hello разрешение ListKeys позволяет hello пользователя toolist hello первичные и вторичные ключи учетной записи. Эти ключи предоставьте hello все подписанные разрешения (чтение, запись, создание больших двоичных объектов, удалите BLOB-объектов, т. д.) по всем подпись службы (больших двоичных объектов, очередей, таблицы, файла) в этой учетной записи хранения. Рекомендуется при возможности использовать SAS учетной записи, как описано выше.
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a>Ограничение доступа концентраторы событий, связанных с toomonitoring
Той же модели, которые можно выполнять с концентраторами событий, но сначала необходимо toocreate выделенное правила авторизации прослушивания. Если требуется toogrant доступ tooan приложение, которое нужно только концентраторов событий, связанных с toomonitoring toolisten hello следующие:

1. Создайте политики общего доступа на hello концентраторы событий, созданные для мониторинга данных с помощью только прослушивания утверждения. Это можно сделать на портале hello. Например, можно назвать ее monitoringReadOnly. Если это возможно требуется toogive, непосредственно ключа toohello потребителя и пропустить следующий шаг hello.
2. Если потребитель hello должен toobe может tooget hello ключа компьютер компьютер, предоставьте hello hello ListKeys для действия пользователя этот концентратор событий. Это также необходимо для пользователей, которым требуется доступ tooset toobe параметра диагностики или журнала концентраторов tooevent toostream профиля. Например, можно создать правило RBAC, как показано ниже.
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a>Дальнейшие действия
* [Прочитайте о RBAC и разрешениях в Resource Manager](../active-directory/role-based-access-control-what-is.md)
* [Обзор hello мониторинга в Azure](monitoring-overview.md)

