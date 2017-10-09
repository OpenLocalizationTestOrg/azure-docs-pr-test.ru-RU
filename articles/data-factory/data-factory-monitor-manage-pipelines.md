---
title: "aaaMonitor и управлять конвейеров с помощью PowerShell и hello портал Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure и Azure PowerShell toomonitor и управлять фабриками данных Azure hello и конвейеры, созданных."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a>Мониторинг и управление ими конвейеров фабрики данных Azure с помощью портала Azure hello и PowerShell
> [!div class="op_single_selector"]
> * [Использование портала Azure или Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Использование приложения для мониторинга и управления](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> Управление и мониторинг приложения Hello предоставляет улучшенную поддержку мониторинг и управление конвейеры данных и устранение проблем. Дополнительные сведения об использовании приложения hello см. в разделе [мониторинг и управление ими конвейеров фабрики данных с помощью приложения hello мониторинг и управление](data-factory-monitor-manage-app.md). 


В этой статье описывается toomonitor, управлять и отлаживать конвейеров с помощью портала Azure и PowerShell. Hello и содержатся рекомендации о предоставлении toocreate предупреждения и получить уведомление о сбоях.

## <a name="understand-pipelines-and-activity-states"></a>Состояния конвейеров и действий
С помощью hello портал Azure, вы можете:

* представлять фабрику данных в виде схемы;
* просматривать действия в конвейере;
* просматривать входные и выходные наборы данных.

В этом разделе также описываются переходы среза набора данных из одного состояния tooanother состояния.   

### <a name="navigate-tooyour-data-factory"></a>Перейдите tooyour фабрики данных
1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Нажмите кнопку **фабрик данных** hello меню слева hello. Если вы не видите его, нажмите кнопку **дополнительные службы >**, а затем нажмите кнопку **фабрик данных** под hello **АНАЛИТИКИ + АНАЛИТИКА** категории.

   !["Просмотреть все" -> "Фабрики данных"](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. На hello **фабрик данных** колонки, выберите hello фабрики данных, который вас интересует.

    ![Выбор фабрики данных](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   Вы увидите домашнюю страницу приветствия для фабрики данных hello.

   ![Колонка "Фабрика данных"](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a>Представление фабрики данных в виде схемы
Hello **схема** представление фабрики данных предоставляет единое toomonitor стекла и управлять hello фабрики данных и ресурсы. toosee hello **схема** фабрики данных, щелкните **схема** на домашней странице приветствия для фабрики данных hello.

![Представление схемы](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

Можно увеличить масштаб, уменьшить масштаб toofit масштаба, % too100 масштаба, блокировка hello макет диаграммы hello и автоматическое расположение конвейеров и наборы данных. Можно также просмотреть информацию журнала обращений и преобразований данных hello (то есть, Показать восходящие и нисходящие элементы выбранных элементов).

### <a name="activities-inside-a-pipeline"></a>Действия в конвейере
1. Щелкните правой кнопкой мыши конвейера hello и нажмите кнопку **откройте конвейера** toosee конвейера все действия в hello, а также входные и выходные наборы данных для действия hello. Эта возможность полезна, конвейер содержит более одного действия, если необходимо toounderstand hello оперативной журнала обращений и преобразований из одного конвейера.

    ![Откройте меню конвейера](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. В следующем примере hello вы видите операции копирования в конвейере hello с входным и выходным. 

    ![Действия в конвейере](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. Можно перейти назад toohello Домашняя страница hello фабрики данных, щелкнув hello **фабрики данных** ссылку на навигатора hello в левом верхнем углу hello.

    ![Перейдите назад toodata фабрики](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a>Представление hello состояние каждого действия в конвейере
Hello текущее состояние действия можно отследить, просмотрев состояние hello какой-либо hello наборов данных, полученных с действия "hello".

Двойным щелчком hello **OutputBlobTable** в hello **схема**, вы увидите все срезы hello, созданные при выполнении различных действий в конвейере. Можно увидеть, что действие копирования hello успешно выполнен для hello последние восемь часов и полученных фрагментов hello в hello **готовности** состояния.  

![Состояние конвейера hello](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

Hello срезов набор данных в фабрике данных hello может иметь одно из следующих статусов hello:

<table>
<tr>
    <th align="left">Состояние</th><th align="left">Подсостояние</th><th align="left">Описание</th>
</tr>
<tr>
    <td rowspan="8">Waiting</td><td>ScheduleTime</td><td>время Hello не входят в toorun срез hello.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>Hello восходящие зависимости не готовы.</td>
</tr>
<tr>
<td>ComputeResources</td><td>Hello вычислительные ресурсы недоступны.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Все экземпляры действий hello заняты обработкой других срезов.</td>
</tr>
<tr>
<td>ActivityResume</td><td>Действие Hello приостановлено и не могут выполняться hello фрагментов до возобновления действия hello.</td>
</tr>
<tr>
<td>Retry</td><td>Действие выполняется повторно.</td>
</tr>
<tr>
<td>Проверка</td><td>Проверка еще не начата.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>Проверка выполняется повторная toobe ожидания.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Validating</td><td>Проверка выполняется.</td>
</tr>
<td>-</td>
<td>Hello срез обрабатывается.</td>
</tr>
<tr>
<td rowspan="4">Сбой</td><td>TimedOut</td><td>Выполнение действия Hello продолжалась дольше, чем допустимых с действия "hello".</td>
</tr>
<tr>
<td>Canceled</td><td>срез Hello была отменена пользователем.</td>
</tr>
<tr>
<td>Проверка</td><td>Сбой проверки.</td>
</tr>
<tr>
<td>-</td><td>срез Hello сбой toobe создан и (или) проверки.</td>
</tr>
<td>Ready</td><td>-</td><td>Hello срез будет готов к использованию.</td>
</tr>
<tr>
<td>Skipped</td><td>None</td><td>срез Hello не обрабатывается.</td>
</tr>
<tr>
<td>None</td><td>-</td><td>Срез используется tooexist в другом состоянии, но был сброшен.</td>
</tr>
</table>



Hello сведения о срез можно просмотреть, щелкнув запись среза на hello **недавно обновлен фрагменты** колонку.

![Сведения о срезе](./media/data-factory-monitor-manage-pipelines/slice-details.png)

Если срез hello выполнен несколько раз, можно увидеть несколько строки в hello **действие выполняется** списка. Для просмотра сведений о действии, запустить, щелкнув hello выполнить запись в hello **действие выполняется** списка. Hello список hello файлов журнала, а также сообщение об ошибке, если таковой имеется. Эта возможность очень полезна tooview и отладочный журналы без необходимости tooleave фабрики данных.

![СВЕДЕНИЯ О ВЫПОЛНЕННОМ ДЕЙСТВИИ](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

Если срез hello не hello **готовности** состояние, можно увидеть hello восходящие срезы, которые не готовы и блокируют hello текущего среза выполнения в hello **восходящие срезы, которые не готовы** списка. Эта возможность полезна, когда ваш среза находится в **ожидания** состояние и требуется ожидание восходящие зависимости hello toounderstand, которые hello среза.

![Неготовые восходящие срезы](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a>Схема состояний наборов данных
После развертывания фабрику данных и конвейеры hello имеют допустимые активного периода, набор данных hello срезы переход из одного состояния tooanother. В настоящее время состояние среза hello ниже hello, следующая схема состояний:

![Схема состояний](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

Hello поток переход состояния набора данных в фабрике данных необходимо hello в следующем: ожидание -> в ход выполнения и выполнение (проверка) -> готов или ошибка.

срез Hello начинается **ожидания** состояния, ожидая toobe предварительные условия выполнены, прежде чем он выполняется. Затем начала выполнения действия hello и срез hello переходит в **выполняющиеся** состояния. Выполнение действия Hello может завершаются успехом или сбоем. Hello среза помечается как **готовности** или **сбой**, основываясь на hello результат выполнения hello.

Можно сбросить toogo срез hello обратно из hello **готовности** или **сбой** toohello состояние **ожидания** состояния. Можно также пометить состояние среза hello слишком**пропустить**, позволяющая активности hello, выполнение и не обработки среза hello.

## <a name="pause-and-resume-pipelines"></a>Приостановка и возобновление работы конвейеров
Управлять конвейерами можно с помощью Azure Powershell. Например, вы можете приостановить и возобновить работу конвейеров, используя командлеты Azure PowerShell. 

> [!NOTE] 
> Приостановка и возобновление конвейеры Hello представление диаграммы не поддерживает. Если вы хотите toouse пользовательский интерфейс, используйте hello отслеживания и управления ими приложения. Дополнительные сведения об использовании приложения hello см. в разделе [мониторинг и управление ими конвейеров фабрики данных с помощью приложения hello мониторинг и управление](data-factory-monitor-manage-app.md) статьи. 

Можно приостановить или приостановить конвейеров с помощью hello **Suspend AzureRmDataFactoryPipeline** командлета PowerShell. Этот командлет полезен, если вы не хотите toorun конвейеры до исправления проблемы. 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Например:

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

После устранения проблемы hello с конвейером hello hello приостановки конвейера можно возобновить, запустив следующую команду PowerShell hello:

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Например:

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a>Отладка конвейеров
Фабрика данных Azure предоставляет богатые возможности для вас toodebug и устранение неполадок конвейеров с помощью hello портал Azure и Azure PowerShell.

> [! Обратите внимание}, что это намного проще tootroubleshot, hello ошибок с помощью мониторинга и приложение для управления. Дополнительные сведения об использовании приложения hello см. в разделе [мониторинг и управление ими конвейеров фабрики данных с помощью приложения hello мониторинг и управление](data-factory-monitor-manage-app.md) статьи. 

### <a name="find-errors-in-a-pipeline"></a>Поиск ошибок в конвейере
Сбой при выполнении действия hello в конвейере hello набора данных, созданного в конвейере hello находится в состоянии ошибки из-за сбоя hello. Отладка и устранение ошибок в фабрике данных Azure с помощью следующих методов hello.

#### <a name="use-hello-azure-portal-toodebug-an-error"></a>Использовать hello Azure портала toodebug ошибку
1. На hello **таблицы** колонка, щелкните срез hello проблемы с hello **состояние** значение слишком**сбой**.

   ![Колонка "Таблица" с проблемным срезом](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. На hello **срез данных** колонке нажмите кнопку, сбой при выполнении действия hello.

   ![Срез данных с ошибкой](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. На hello **сведения о выполнении действия** колонки, файлы можно загрузить hello, связанные с обработкой HDInsight hello. Нажмите кнопку **загрузки** для состояния и stderr toodownload hello файл журнала ошибок со сведениями об ошибке hello.

   ![Колонка "Сведения о циклах выполнения действия" с ошибкой](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a>Используйте PowerShell toodebug ошибку
1. Запустите **PowerShell**.
2. Запустите hello **Get AzureRmDataFactorySlice** команд toosee hello срезов и их состояния. Вы увидите срез с состоянием hello **сбой**.        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   Например:

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   Замените **StartDateTime** на время запуска конвейера. 
3. Теперь запустите hello **Get AzureRmDataFactoryRun** запустить командлет tooget сведения о действии hello hello среза.

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    Например:

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    Hello StartDateTime равен hello время начала среза hello ошибки или проблемы, записанными из предыдущего шага hello. Hello даты времени должна быть заключена в двойные кавычки.
4. Вы должны увидеть результаты с подробными сведениями об ошибке hello, аналогичные toohello следующее:

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. Можно запустить hello **сохранить AzureRmDataFactoryLog** со значением идентификатора см. в выходных данных hello и загрузите файлы журналов hello с помощью hello hello **- DownloadLogsoption** для командлета hello.

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a>Повторная обработка проблемных срезов в конвейере

> [!IMPORTANT]
> Это упрощает tootroubleshoot ошибки и повторного запуска невыполненных фрагментов с помощью hello мониторинг & приложение для управления. Дополнительные сведения об использовании приложения hello см. в разделе [мониторинг и управление ими конвейеров фабрики данных с помощью приложения hello мониторинг и управление](data-factory-monitor-manage-app.md). 

### <a name="use-hello-azure-portal"></a>Использовать hello портал Azure
После устранения неполадок и отладки сбоев в конвейере, можно повторно запустить сбоев путем перехода toohello ошибка среза и щелкнув hello **запуска** кнопки на панели команд hello.

![Повторная обработка среза](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

В случае hello срез не прошло проверку из-за сбоя политики (например, если данные не доступны), можно устранить ошибки hello и еще раз проверьте, выбрав hello **проверки** кнопку на панели команд hello.

![Исправление ошибок и проверка](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a>Использование Azure PowerShell
Ошибки можно перезапустить с помощью hello **AzureRmDataFactorySliceStatus набор** командлета. В разделе hello [AzureRmDataFactorySliceStatus набор](https://msdn.microsoft.com/library/mt603522.aspx) раздел о синтаксисе и другие сведения о командлете hello.

**Пример**

Hello следующий пример задает hello состояние всех фрагментов для hello таблицу «DAWikiAggregatedData» too'Waiting "в фабрике данных Azure hello «WikiADF».

Hello «Тип обновления» имеет значение too'UpstreamInPipeline, это означает, что состояния каждого среза для hello таблицы и всех таблиц (вышестоящего) hello для зависимых задаются too'Waiting. Hello другие возможные значения для этого параметра — это «Пользователь».

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a>Создание оповещений
Azure регистрирует пользовательские события, когда ресурс Azure (например, фабрика данных) создается, обновляется или удаляется. Вы можете создавать оповещения об этих событиях. Можно использовать различные метрики toocapture фабрики данных и создавать предупреждения для метрики. Мы советуем использовать события для наблюдения в режиме реального времени, а метрики — для статистических целей.

### <a name="alerts-on-events"></a>Оповещения о событиях
События Azure позволяют получить представление о том, что происходит в ресурсах Azure. При использовании фабрики данных Azure события создаются, когда:

* фабрика данных создается, обновляется или удаляется;
* запускается или завершается обработка данных (цикл выполнения);
* создается и удаляется кластер HDInsight по требованию.

Можно создавать предупреждения по этим событиям пользователя и их настройки уведомления toohello toosend электронной почты администратора и coadministrators hello подписки. Кроме того можно указать дополнительных адресов электронной почты пользователей, которым требуются уведомления по электронной почте tooreceive при выполнении условий hello. Эта возможность полезна, требуется tooget уведомления об ошибках, если не нужно toocontinuously монитор фабрики данных.

> [!NOTE]
> В настоящее время портал hello не отображать оповещения о событиях. Используйте hello [управление и мониторинг приложения](data-factory-monitor-manage-app.md) toosee все предупреждения.


#### <a name="specify-an-alert-definition"></a>Задание определения оповещения
toospecify определение предупреждения, создайте файл JSON, описывающий hello операций, которые вы хотите toobe оповещения на. В следующем примере hello предупреждение hello отправляет уведомление по электронной почте для hello RunFinished операции. toobe конкретного уведомления по электронной почте отправляется после завершения выполнения в фабрике данных hello и произошел сбой запуска hello (состояние = FailedExecution).

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

Можно удалить **подсостояния** из определения JSON, если вы не хотите toobe оповещения на конкретный сбой hello.

Этот пример устанавливает hello предупреждения для всех фабрик данных в вашей подписке. Если требуется, чтобы предупреждения toobe hello для фабрики данных, можно указать фабрики данных **resourceUri** в hello **dataSource**:

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

Hello следующей таблице приведен список hello доступные операции и состояния (и Дополнительные сведения).

| Имя операции | Состояние | Подсостояние |
| --- | --- | --- |
| RunStarted |Started |Starting |
| RunFinished |Failed / Succeeded |FailedResourceAllocation<br/><br/>Succeeded<br/><br/>FailedExecution<br/><br/>TimedOut<br/><br/><Canceled<br/><br/>FailedValidation<br/><br/>Abandoned |
| OnDemandClusterCreateStarted |Started | |
| OnDemandClusterCreateSuccessful |Успешно | |
| OnDemandClusterDeleted |Успешно | |

В разделе [создания правила оповещения](https://msdn.microsoft.com/library/azure/dn510366.aspx) подробные сведения об элементах hello JSON, которые используются в примере hello.

#### <a name="deploy-hello-alert"></a>Развертывание предупреждение hello
Предупреждение toodeploy hello, используйте командлет Azure PowerShell hello **New AzureRmResourceGroupDeployment**, как показано в следующий пример hello:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

После успешного завершения развертывания группы ресурсов hello отображаются hello следующие сообщения:

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> Можно использовать hello [создать правило оповещения о](https://msdn.microsoft.com/library/azure/dn510366.aspx) toocreate API-интерфейса REST правило оповещения. полезные данные JSON Hello — аналогичный пример toohello JSON.  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a>Получить список hello развертывания группы ресурсов Azure
Список hello tooretrieve развернутого развертывания группы ресурсов Azure, с помощью командлета hello **Get AzureRmResourceGroupDeployment**, как показано в следующий пример hello:

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a>Устранение неполадок пользовательских событий
1. Вы можете просмотреть все события hello, созданные после нажатия кнопки hello **метрики и операций** плитки.

    ![Элемент "Метрики и операции"](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. Нажмите кнопку hello **события** плитки toosee hello события.

    ![Плитки "События"](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. На hello **события** колонки, чтобы просмотреть сведения о событиях, отфильтрованных событий и т. д.

    ![Колонка "События"](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. Нажмите кнопку **операции** списка операций hello, приводит к ошибке.

    ![Выберите операцию](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. Нажмите кнопку **ошибка** событие toosee сведения об ошибке hello.

    ![Ошибка события](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

В разделе [анализ Azure командлеты](https://msdn.microsoft.com/library/mt282452.aspx) для командлетов PowerShell, которые можно использовать tooadd, получения и удаления оповещения. Вот несколько примеров использования hello **Get AlertRule** командлета:

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

Выполните следующие команды get-help toosee-подробные сведения и примеры для командлета Get-AlertRule hello hello.

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


Если на события создания оповещений hello hello портала колонки, но не получать уведомления по электронной почте, проверить, установлен ли указанный адрес электронной почты hello tooreceive сообщений электронной почты от внешних отправителей. предупреждения Hello сообщения электронной почты может были заблокированы параметры электронной почты.

### <a name="alerts-on-metrics"></a>Оповещения по метрикам
Фабрика данных позволяет собирать различные метрики и создавать по ним оповещения. Можно отслеживать и создавать предупреждения для следующих метрик для hello срезов в вашей фабрике данных hello:

* **циклы выполнения со сбоем**;
* **успешные циклы выполнения**.

Эти показатели полезны и помочь tooget запуска Обзор в целом, так и неуспешные в фабрике данных hello. Метрики создаются при каждом цикле выполнения действия со срезом. В начале hello hello час, эти показатели объединяются и помещается tooyour учетной записи хранилища. метрики tooenable Настройка учетной записи хранилища.

#### <a name="enable-metrics"></a>Включить метрики
tooenable метрик, щелкните следующую команду hello hello **фабрики данных** колонки:

**Мониторинг** > **Метрика** > **Параметры диагностики** > **Диагностика**

![Ссылка диагностики](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

На hello **диагностики** колонка, щелкните **на**, выберите учетную запись хранения hello и нажмите кнопку **Сохранить**.

![Выноска "Диагностика"](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

Он может занять час tooone для hello метрики toobe отображается на hello **мониторинг** колонки так как статистических показателей происходит каждый час.

### <a name="set-up-an-alert-on-metrics"></a>Настройка оповещений по метрикам
Нажмите кнопку hello **фабрики данных метрик** плитки:

![Элемент "Метрики фабрики данных"](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

На hello **метрика** колонка, щелкните **+ добавить оповещение** на панели инструментов hello.
![Колонка "Метрики фабрики данных", добавление оповещения](./media/data-factory-monitor-manage-pipelines/add-alert.png)

На hello **Добавление правила оповещения** , hello, выполнив действия и нажмите кнопку **ОК**.

* Введите имя для оповещения hello (пример: «предупреждение о сбое»).
* Введите описание для предупреждения hello (пример: «отправить сообщение электронной почты, когда происходит сбой»).
* Выберите метрику (неудачные и успешные выполнения).
* Укажите условие и пороговое значение.   
* Укажите период времени hello.
* Укажите, следует ли отправлять сообщение электронной почты, tooowners, участники и читатели.

![Колонка "Метрики фабрики данных", добавление правила оповещения](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

После успешно добавлено правило генерации оповещений hello, закрывает колонке hello и вы увидите новое предупреждение hello в hello **метрика** колонку.

![Колонка "Метрики фабрики данных", добавление нового оповещения](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

Вы также увидите hello число оповещений за hello **предупреждения правила** плитки. Нажмите кнопку hello **предупреждения правила** плитки.

![Колонка "Метрики фабрики данных", правила оповещения](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

На hello **правила оповещения** колонку, вы видите все имеющиеся оповещения. tooadd оповещения, щелкните **добавить оповещение** на панели инструментов hello.

![Колонка "Правила оповещения"](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a>Оповещения
После правила оповещения hello соответствует условию hello, вы должны получить сообщение электронной почты о том, что активации предупреждения hello. После устранения проблемы hello и больше не соответствует hello условие оповещения, вы получаете электронное сообщение о том, что предупреждение hello разрешается.

Такое поведение отличается от ситуации, когда уведомление отправляется по каждому сбою, соответствующему правилу оповещения.

### <a name="deploy-alerts-by-using-powershell"></a>Развертывание оповещений с помощью PowerShell
Вы можете развернуть предупреждения для метрики hello таким же образом, как для событий.

**Определение оповещения**

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

Замените *subscriptionId*, *resourceGroupName*, и *с именем dataFactoryName* в образце hello с соответствующими значениями.

*metricName* на данный момент поддерживает два значения:

* FailedRuns и
* SuccessfulRuns.

**Развертывание предупреждение hello**

Предупреждение toodeploy hello, используйте командлет Azure PowerShell hello **New AzureRmResourceGroupDeployment**, как показано в следующий пример hello:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

В случае успешного развертывания вы увидите следующее сообщение:

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

Можно также использовать hello **AlertRule добавить** toodeploy командлет правило оповещения. В разделе hello [AlertRule добавить](https://msdn.microsoft.com/library/mt282468.aspx) разделе Дополнительные сведения и примеры.  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a>Перемещение данных фабрики tooa другой группе ресурсов или подписки
Можно переместить данные фабрики tooa другой группе ресурсов или другую подписку с помощью hello **переместить** командной строке кнопки на главной странице hello фабрики данных.

![Перемещение фабрики данных](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

Также можно перемещать все связанные ресурсы (такие как предупреждения, связанные с фабрикой данных hello), вместе с hello фабрики данных.

![Диалоговое окно "Перемещение ресурсов"](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
