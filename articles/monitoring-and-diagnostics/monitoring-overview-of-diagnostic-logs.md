---
title: "aaaOverview журналов диагностики Azure | Документы Microsoft"
description: "Что такое Azure журналы диагностики и способы их toounderstand событиями, происходящими в ресурс Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>Сбор и использование данных журнала из ресурсов Azure

## <a name="what-are-azure-resource-diagnostic-logs"></a>Что такое журналы диагностики ресурсов Azure
**Журналы диагностики Azure уровня ресурсов** создаваемых ресурса с журнала предоставляет широкие возможности, часто данные об операции hello этого ресурса. Hello содержимое этих журналов зависит от типа ресурса. Например, счетчики правила группы безопасности сети и аудит Key Vault представляют две категории журналов ресурсов.

Журналы диагностики уровня ресурсов отличаются от hello [журнал действий](monitoring-overview-activity-logs.md). Hello журнал действий позволяет контролировать hello операций, которые были выполнены на ресурсы в подписке с помощью диспетчера ресурсов, например, для создания виртуальной машины или удаление приложения логики. Hello журнал действий — это журнал уровня подписки. Журналы диагностики уровня ресурса дают представление об операциях, которые были выполнены в рамках этого ресурса, например о получении секрета из Key Vault.

Журналы диагностики уровня ресурса также отличаются от журналов диагностики уровня гостевой ОС. Журналы диагностики гостевой ОС собирает агент, работающий на виртуальной машине или поддерживаемом ресурсе другого типа. Журналы диагностики уровня ресурсов требуется данные определенных ресурсов агента и записи между hello платформы Azure, когда журналы диагностики гостевой ОС уровень сбора данных из hello операционной системы и приложений, выполняющихся на виртуальной машине.

Не все ресурсы поддержки нового типа ресурса журналов диагностики, описанные здесь hello. В этой статье перечислены раздел типы ресурсов поддержки новых журналов диагностики hello уровня ресурсов.

![Журналы диагностики ресурсов и другие типы журналов ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>Что можно делать с журналами диагностики уровня ресурса
Ниже приведены некоторые hello вещей, которые можно сделать с помощью журналов диагностики для ресурса.

![Логическое размещение журналов диагностики ресурсов](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* Сохранить их tooa [ **учетной записи хранилища** ](monitoring-archive-diagnostic-logs.md) проверка аудита или вручную. Можно указать с помощью времени (в днях) хранения hello **параметров диагностики для ресурса**.
* [Слишком потоковую передачу**концентраторов событий** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) продукты для использования службой сторонних или пользовательских analytics решение, например PowerBI.
* Анализ журналов с помощью [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)

Можно использовать учетную запись хранения или пространство имен концентраторов событий, не входящий в hello той же подписке, которые hello одного выпуска журналы. Hello пользователь, настраивающий приветствия должен иметь hello соответствующие RBAC доступа tooboth подписки.

## <a name="resource-diagnostic-settings"></a>Параметры диагностики ресурсов
Журналы диагностики для всех ресурсов, кроме вычислительных, настраиваются с помощью параметров диагностики ресурсов. **Параметры диагностики ресурсов** для управления ресурсами:

* Куда отправляются журналы диагностики ресурсов и метрики (учетная запись хранения, концентраторы событий и/или OMS Log Analytics).
* Какие категории журнала отправляются и следует ли отправлять данные метрики.
* Как долго должны храниться журналы каждой категории в учетной записи хранения.
    - Срок хранения 0 дней означает, что журналы хранятся неограниченно долго. В противном случае — значение hello может быть любое число дней от 1 до 2147483647.
    - Если заданы политики хранения, но сохранения журналов в учетной записи хранения отключена (например, если только выбраны параметры концентраторов событий или OMS), политики хранения hello не действуют.
    - Политики хранения, примененных в день, поэтому hello регистрирует конец дня (UTC), с датой hello, что теперь находится за пределами hello политику хранения, удаляются. Например если у вас есть политика хранения продолжительностью в один день, в начале hello сегодня день hello hello журналы из позавчерашнего дня hello, будет удален.

Эти параметры настраиваются легко hello параметров диагностики для ресурса в hello портал Azure, посредством команд Azure PowerShell и интерфейс командной строки или с помощью hello [API REST Azure монитор](https://msdn.microsoft.com/library/azure/dn931943.aspx).

> [!WARNING]
> Журналы диагностики и метрики для hello гостевой ОС уровня использования вычислительных ресурсов (например, виртуальные машины или Service Fabric) [отдельным механизмом для конфигурации и выбора выходов](../azure-diagnostics.md).
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a>Как tooenable сбора диагностических журналов ресурсов
Сбор журналов диагностики ресурсов можно включить [при создании ресурса шаблона диспетчера ресурсов](./monitoring-enable-diagnostic-logs-using-template.md) или после создания ресурса из этого ресурса страницу портала hello. Можно также включить коллекции в любой момент с помощью команд Azure PowerShell или интерфейс командной строки или с помощью API REST Azure монитор hello.

> [!TIP]
> Эти инструкции могут не относиться непосредственно tooevery ресурсов. Просмотрите ссылки схемы hello hello нижней части этой страницы toounderstand шаги, которые могут относиться toocertain типов ресурсов.
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a>Включить сбор журналов диагностики ресурсов на портале hello
Можно включить сбор журналов диагностики ресурсов в hello Azure портал после создания ресурса будет tooa конкретный ресурс или путем перемещения tooAzure монитора. tooenable это через монитор Azure:

1. В hello [портал Azure](http://portal.azure.com)tooAzure монитора перейдите и выберите команду **параметров диагностики**

    ![Раздел мониторинга Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. При необходимости фильтровать список hello по группе ресурсов или тип ресурса, а затем щелкните hello ресурсов, для которого вы хотите tooset параметра диагностики.

3. Если параметры не существует в hello ресурс, который вы выбрали, не запрошенные toocreate параметр. Щелкните Turn on diagnostics (Включить диагностику).

   ![Добавление параметра диагностики — имеющиеся параметры отсутствуют](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   Если имеются существующие параметры ресурсов hello, вы увидите список параметров, уже настроен на этом ресурсе. Нажмите Add diagnostic setting (Добавить параметр диагностики).

   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. Задайте имя параметра, флажки hello для каждого назначения toowhich бы как toosend данные и настройки ресурса, который используется для каждого назначения. При необходимости задайте количество дней tooretain эти журналы с помощью hello **хранения (в днях)** ползунки (только применимые toohello учетной записи местом назначения хранилища). Хранение 0 дней хранит журналы hello бесконечно.
   
   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Щелкните **Сохранить**.

Через несколько секунд hello новый параметр отображается в списке параметров для этого ресурса, а также журналы диагностики отправляются toohello указан назначения сразу созданы новые данные события.

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>Включение сбора журналов диагностики ресурсов с помощью PowerShell
Коллекция tooenable журналы диагностики ресурсов через Azure PowerShell, hello используйте следующие команды:

хранение tooenable в журналах диагностики в учетную запись хранилища, используйте следующую команду:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

Идентификатор учетной записи хранилища Hello hello идентификатор ресурса для журналов toowhich учетной записи хранилища hello, требуется toosend hello.

Потоковая передача tooenable концентратора событий tooan журналы диагностики, используйте следующую команду:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

ИД правила Hello service bus представляет собой строку следующего формата: `{Service Bus resource ID}/authorizationrules/{key name}`.

tooenable отправки журналов диагностики рабочей области аналитики журналов tooa, используйте следующую команду:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

Вы можете получить идентификатор ресурса hello рабочей области аналитики журналов с помощью hello следующую команду:

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

Эти параметры tooenable можно объединить несколько параметров вывода.

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a>Включение сбора журналов диагностики ресурсов с помощью интерфейса командной строки
Коллекция tooenable журналы диагностики ресурсов через hello Azure CLI, используйте hello, следующие команды:

хранение tooenable в журналах диагностики в учетную запись хранилища, используйте следующую команду:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

Идентификатор учетной записи хранилища Hello hello идентификатор ресурса для журналов toowhich учетной записи хранилища hello, требуется toosend hello.

Потоковая передача tooenable концентратора событий tooan журналы диагностики, используйте следующую команду:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

ИД правила Hello service bus представляет собой строку следующего формата: `{Service Bus resource ID}/authorizationrules/{key name}`.

tooenable отправки журналов диагностики рабочей области аналитики журналов tooa, используйте следующую команду:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

Эти параметры tooenable можно объединить несколько параметров вывода.

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>Включение сбора журналов диагностики ресурсов с помощью REST API
toochange параметров диагностики с помощью hello Azure REST API-Интерфейс монитора, в разделе [в этом документе](https://msdn.microsoft.com/library/azure/dn931931.aspx).

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a>Управление параметрами диагностических ресурсов в портале hello
Убедитесь, что все ресурсы настроены с помощью параметров диагностики. Перейдите в слишком**монитор** в hello портала и откройте **параметров диагностики**.

![Диагностические журналы колонке hello портала](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

Вы можете иметь tooclick раздел «Дополнительные службы» toofind hello монитора.

Здесь можно просмотреть и отфильтровать все ресурсы, поддерживающие toosee параметров диагностики, если они имеют включении диагностики. Можно также детализировать toosee, если несколько параметры настроены для ресурса и проверьте какой учетной записи хранилища, пространство имен концентраторов событий и рабочей области аналитики журналов, потоков данных.

![Журналы диагностики на портале](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

Добавление параметра диагностики появится представление параметров диагностики, где можно включить, отключить или изменить параметры диагностики для hello hello выбранных ресурсов.

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>Поддерживаемые службы, категории и схемы для журналов диагностики ресурсов
[См. в статье](monitoring-diagnostic-logs-schema.md) полный список поддерживаемых служб и категории журнала hello и схем, используемых этими службами.

## <a name="next-steps"></a>Дальнейшие действия

* [Поток ресурсов журналы диагностики слишком**концентраторов событий**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Изменение параметров диагностики ресурсов, с помощью API REST Azure монитор hello](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Сбор журналов и метрик для служб Azure для использования в Log Analytics](../log-analytics/log-analytics-azure-storage.md)
