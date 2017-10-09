---
title: "Примеры быстрого запуска монитора PowerShell aaaAzure. | Документация Майкрософт"
description: "С помощью PowerShell tooaccess монитора Azure функции, такие как Автомасштабирование, предупреждения, веб-перехватчиков и поиска журналы действий."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a>Примеры для быстрого запуска Azure Monitor с помощью PowerShell
Это статье показывает пример toohelp команд PowerShell, можно получить доступ к возможности Azure монитора. Монитор Azure позволяет tooAutoScale облачных служб, виртуальных машин и веб-приложений и toosend уведомлений или вызов веб-адреса на основе значений данных телеметрии, настроенных.

> [!NOTE]
> Монитор Azure — новое имя hello что был вызван «Azure Insights» до 25 сентября 2016 года. Однако hello пространств имен и, следовательно, hello, следующие команды по-прежнему содержать аналитики «hello».
> 
> 

## <a name="set-up-powershell"></a>Настройка PowerShell
Если это еще не сделано, установите toorun PowerShell на компьютере. Дополнительные сведения см. в разделе [как tooInstall и настроить PowerShell](/powershell/azure/overview).

## <a name="examples-in-this-article"></a>Примеры в этой статье
Hello в статье hello примерах об использовании командлетов Azure монитора. Можно также просмотреть hello весь список командлетов Azure PowerShell монитора на [командлеты Azure монитора (аналитика)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).

## <a name="sign-in-and-use-subscriptions"></a>Вход в систему и использование подписок
Во-первых войдите в tooyour подписки Azure.

```PowerShell
Login-AzureRmAccount
```

Для этого в toosign. После этого вы увидите свою учетную запись, идентификатор клиента и идентификатор подписки по умолчанию. Все hello Azure командлеты работают в контексте hello подписки по умолчанию. tooview hello список подписок, доступ к, используйте следующую команду hello.

```PowerShell
Get-AzureRmSubscription
```

toochange рабочий контекст tooa другой подпиской, hello используйте следующую команду.

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a>Получение журнала действий для подписки
Используйте hello `Get-AzureRmLog` командлета.  Hello ниже приведены некоторые примеры.

Получение записей журнала из этого toopresent даты и времени:

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

Получение записей журнала в пределах диапазона дат и времени.

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Получение записей журнала для определенной группы ресурсов.

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

Получение записей журнала от конкретного поставщика ресурсов в пределах диапазона даты и времени.

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Получение всех записей журнала для конкретной вызывающей стороны.

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

Следующая команда извлекает Hello hello последних 1000 событий из журнала активности hello:

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

`Get-AzureRmLog` поддерживает много других параметров. В разделе hello `Get-AzureRmLog` ссылку для получения дополнительной информации.

> [!NOTE]
> `Get-AzureRmLog` предоставляет данные журнала только за 15 дней. С помощью hello **- MaxEvents** параметр позволяет tooquery hello последние N событий, за 15 дней. события tooaccess старее 15 дней используйте hello API-интерфейса REST или пакета SDK (пример на C# с помощью пакета SDK для hello). Если не включать **StartTime**, то значение по умолчанию hello **EndTime** минус один час. Если не включать **EndTime**, то значение по умолчанию hello текущее время. Все значения времени указаны в формате UTC.
> 
> 

## <a name="retrieve-alerts-history"></a>Извлечение журнала оповещений
все предупреждения событий, вы можете запросить tooview hello журналы диспетчера ресурсов Azure, используя следующие примеры hello.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

правило tooview hello журнала для указанного предупреждения, можно использовать hello `Get-AzureRmAlertHistory` командлета, передавая идентификатор ресурса hello hello правило оповещения.

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

Hello `Get-AzureRmAlertHistory` командлет поддерживает различные параметры. Дополнительные сведения см. в документации командлета [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).

## <a name="retrieve-information-on-alert-rules"></a>Извлечение информации о правилах генерации оповещений
Все следующие команды hello, влияют на группу ресурсов с именем «montest».

Просмотрите все свойства hello hello правило генерации оповещений:

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

Извлечение всех оповещений о группе ресурсов.

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

Извлечение всех правил генерации оповещений для целевого ресурса. Например, можно извлечь все правила генерации оповещений, установленные для виртуальной машины.

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

`Get-AzureRmAlertRule` поддерживает и другие параметры. Дополнительную информацию см. в документации [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx).

## <a name="create-metric-alerts"></a>Создание оповещений о метриках
Можно использовать hello `Add-AlertRule` toocreate командлета, обновление или отключение правила оповещения.

С помощью `New-AzureRmAlertRuleEmail` и `New-AzureRmAlertRuleWebhook` можно создать свойства электронного адреса и веб-перехватчика, соответственно. В командлете правило генерации оповещений hello, назначьте их в качестве действия toohello **действия** свойство hello правило оповещения.

Hello в следующей таблице описаны параметры hello и значения используется toocreate оповещение с использованием показателя.

| Параметр | value |
| --- | --- |
| Имя |simpletestdiskwrite |
| Расположение этого правила генерации оповещений |Восток США |
| ResourceGroup |montest |
| TargetResourceId |/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig |
| MetricName hello предупреждения, которая создается |\PhysicalDisk (_Total) \Disk операции записи в секунду. В разделе hello `Get-MetricDefinitions` по командлетам как tooretrieve hello точные имена метрик |
| operator |GreaterThan |
| Пороговое значение (число/с для этой метрики) |1 |
| WindowSize (в формате чч:мм:сс) |00:05:00 |
| средство инвентаризации (статистики hello метрики, которые используются в этом случае среднее количество) |Средняя |
| пользовательские сообщения электронной почты (строковый массив) |'foo@example.com','bar@example.com' |
| Отправить по электронной почте tooowners, участники и Читатели |-SendToServiceOwners |

Создание действия электронного сообщения

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

Создание действия веб-перехватчика

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

Создание правила оповещения hello на метрику % ЦП hello в классической виртуальной Машины

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

Получить правило генерации оповещений hello

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

Hello добавить оповещения также обновляет правило hello Если правило генерации оповещений для заданного свойства hello уже существует. toodisable правило генерации оповещений, включите параметр hello **- DisableRule**.

## <a name="get-a-list-of-available-metrics-for-alerts"></a>Получение списка доступных метрик для оповещений
Можно использовать hello `Get-AzureRmMetricDefinition` командлет tooview hello список все метрики для конкретного ресурса.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

Hello следующий пример создает таблицу с метрикой hello имя и hello единицы для него.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Полный список доступных параметров для `Get-AzureRmMetricDefinition` представлен в разделе [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).

## <a name="create-and-manage-autoscale-settings"></a>Создание параметров автомасштабирования и управление ими
Для ресурса, например веб-приложения, виртуальной машины, облачной службы или масштабируемого набора виртуальных машин, можно настроить только один параметр автомасштабирования.
Однако у каждого параметра автомасштабирования может быть несколько профилей. Например, один профиль для масштабирования на основе производительности, а второй — на основе расписания. Для каждого профиля можно настроить несколько правил. Дополнительные сведения о автомасштабирования см. в разделе [как tooAutoscale приложения](../cloud-services/cloud-services-how-to-scale.md).

Ниже приведены шаги hello, которые будут использоваться.

1. Создадим правила.
2. Создайте профили правила сопоставления hello, созданный ранее toohello профилей.
3. (Необязательно.) Создадим уведомления для автомасштабирования, настроив свойства веб-перехватчика и электронного адреса.
4. Создание параметров автоматического масштабирования с именем hello целевого ресурса путем сопоставления профилей hello и уведомления, созданные в предыдущих шагах hello.

Hello следующих примерах показано, как создать параметров автоматического масштабирования для набора масштабирования виртуальных машин для операционной системы Windows, с помощью приложения hello ЦП метрики использования.

Сначала создайте правило tooscale выход, с увеличением числа экземпляра.

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

Создайте правило tooscale в с уменьшение числа экземпляра.

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

Затем создайте профиль для правил hello.

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

Создайте действие веб-перехватчика.

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

Создайте свойство hello уведомления для параметра автоматического масштабирования hello, включая сообщения электронной почты и hello веб-перехватчика, созданной ранее.

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

Наконец создайте hello автомасштабирования параметр tooadd hello профиль, созданный выше.

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

Дополнительные сведения об управлении параметрами автомасштабирования см. в документации [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).

## <a name="autoscale-history"></a>Журнал автомасштабирования
Hello следующем примере показано, как можно просмотреть последние события автоматического масштабирования и предупреждение. Используйте hello поиска журнала действий tooview историю автомасштабирования hello.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

Можно использовать hello `Get-AzureRmAutoScaleHistory` tooretrieve командлет историю автомасштабирования.

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

Дополнительные сведения см. в документации [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).

### <a name="view-details-for-an-autoscale-setting"></a>Просмотр сведений о параметре автомасштабирования
Можно использовать hello `Get-Autoscalesetting` tooretrieve командлет Дополнительные сведения о настройке автомасштабирования hello.

Hello пример сведения обо всех параметрах автоматического масштабирования в группе ресурсов hello «myrg1».

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

Hello следующий пример показывает сведения обо всех параметрах автоматического масштабирования в группе ресурсов hello «myrg1» и в частности hello с именем «MyScaleVMSSSetting» параметр автомасштабирования.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a>Удаление параметра автомасштабирования
Можно использовать hello `Remove-Autoscalesetting` toodelete командлет параметров автоматического масштабирования.

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a>Управление профилями журнала действий
Можно создать *входа профиль* и экспорт данных из вашей учетной записи действия журнала tooa хранения и можно настроить хранение данных для него. При необходимости можно осуществлять потоковую tooyour hello данных концентратора событий. Обратите внимание, что в настоящее время доступна предварительная версия этой функции и можно создать только один профиль журнала на подписку. Можно использовать следующие командлеты с вашей текущей подписки toocreate hello и управления профилями журнала. Вы также можете выбрать другую подписку. Несмотря на то, что PowerShell значения по умолчанию для текущей подписки toohello всегда можно изменить, используя `Set-AzureRmContext`. Можно настроить учетную запись хранения tooany данных в tooroute журнала действий или концентратор событий в пределах этой подписки. Данные записываются как файлы больших двоичных объектов в формате JSON.

### <a name="get-a-log-profile"></a>Получение профиля журнала
toofetch существующие профили журнала, используйте hello `Get-AzureRmLogProfile` командлета.

### <a name="add-a-log-profile-without-data-retention"></a>Добавление профиля журнала без хранения данных
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Удаление профиля журнала
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a>Добавление профиля журнала с хранением данных
Можно указать hello **- RetentionInDays** свойство с hello количество дней, в виде положительного целого числа, где хранятся данные hello.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a>Добавление профиля журнала с периодом удержания и концентратором событий
В дополнение toorouting toostorage учетной записи данных, вы также осуществляет потоковую передачу его tooan концентратора событий. Обратите внимание, что в этой предварительной версии выпуска и hello конфигурацию учетной записи хранения является обязательным, но конфигурация концентратора событий не является обязательной.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a>Настройка журналов диагностики
Многие службы Azure предоставляют дополнительные журналы и данные телеметрии, может быть toosave настроенных данных в вашей учетной записи хранилища Azure, отправить tooEvent концентраторов и/или отправлено рабочей области аналитики журналов OMS tooan. Эта операция может выполняться только на уровне ресурсов и хранилища hello учетной записи или события концентратора должны присутствовать в hello же регионе, где целевой ресурс hello где hello диагностики настраивается.

### <a name="get-diagnostic-setting"></a>Получение параметра диагностики
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

Отключение параметра диагностики

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

Включение параметра диагностики без периода удержания

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

Включение параметра диагностики с периодом удержания

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Включение параметра диагностики с периодом удержания для определенной категории журналов

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Включение параметра диагностики для концентратора событий

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

Включение параметра диагностики для OMS

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
