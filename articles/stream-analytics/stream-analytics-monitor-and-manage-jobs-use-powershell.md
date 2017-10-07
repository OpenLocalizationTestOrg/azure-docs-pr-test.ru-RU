---
title: "aaaMonitor и управление заданиями Stream Analytics с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как командлеты Azure PowerShell и toomonitor toouse заданий Stream Analytics и управление ими."
keywords: "azure powershell, командлеты azure powershell, команда powershell, сценарии powershell"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a>Отслеживание заданий Stream Analytics и управление ими с помощью командлетов Azure PowerShell
Узнайте, как toomonitor и управление ресурсами Stream Analytics с помощью командлетов Azure PowerShell и сценариев powershell, выполнять основные задачи Stream Analytics.

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a>Необходимые условия для запуска командлетов Azure PowerShell службы Stream Analytics
* Создайте группу ресурсов Azure в своей подписке. Hello ниже приведен пример сценария Azure PowerShell. Дополнительную информацию об Azure PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).  

Azure PowerShell 0.9.8:  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

Azure PowerShell 1.0.  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> Отслеживание заданий Stream Analytics, созданных программным путем, по умолчанию отключено.  Вы можете вручную включить наблюдение в hello портал Azure, перейдя на страницу toohello задания монитора и щелкнув кнопку Enable hello, или это можно сделать программным образом, выполнив следующие шаги hello, расположенный в [Azure Stream Analytics — поток монитора Аналитика программным путем задания](stream-analytics-monitor-jobs.md).
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a>Командлеты Azure PowerShell для службы Stream Analytics
Hello следующие командлеты Azure PowerShell можно использовать toomonitor и управление заданиями Azure Stream Analytics. Обратите внимание, что Azure PowerShell имеет различные версии. 
**В примерах hello, первая команда перечисленных hello предназначен для Azure PowerShell 0.9.8 вторая команда hello является для Azure PowerShell 1.0.** команды Hello Azure PowerShell 1.0 всегда будет содержать «AzureRM» в команде hello.

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a>Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob
Перечисляет все задания Stream Analytics, определенные в hello подписки Azure или группа ресурсов или получает задание сведений о конкретном задании в группе ресурсов.

**Пример 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsJob

Эта команда PowerShell возвращает сведения обо всех заданиях Stream Analytics hello в hello подписки Azure.

**Пример 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Эта команда PowerShell возвращает сведения обо всех заданиях hello Stream Analytics в группе ресурсов hello StreamAnalytics по умолчанию-Центральная часть США.

**Пример 3**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Эта команда PowerShell возвращает сведения о задании Stream Analytics hello StreamingJob в группе ресурсов hello StreamAnalytics по умолчанию-Центральная часть США.

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a>Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput
Перечисляет все hello входных данных, которые определены в указанное задание Stream Analytics, или возвращает сведения об определенных входных данных.

**Пример 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Эта команда PowerShell возвращает сведения о всех входных данных hello, определенные в задании hello StreamingJob.

**Пример 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Эта команда PowerShell возвращает сведения о hello входных данных с именем EntryStream, определенные в задании hello StreamingJob.

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a>Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput
Перечисляет все hello выходных данных, которые определены в указанное задание Stream Analytics, или возвращает сведения о конкретных выходных данных.

**Пример 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Эта команда PowerShell возвращает сведения о определены в задании hello StreamingJob hello выходов.

**Пример 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Эта команда PowerShell возвращает сведения о hello выходных данных с именем выходные данные, определенные в задании hello StreamingJob.

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a>Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota
Получает сведения о квоте hello единицы в указанном регионе потоковой передачи.

**Пример 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

Эту команду PowerShell возвращает сведения о квоте hello и использования единиц потоковой передачи в регионе hello центральной части США.

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a>Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation
Возвращает сведения о конкретном преобразовании, определенном в задании Stream Analytics.

**Пример 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Эта команда PowerShell возвращает сведения о преобразовании «hello», называется StreamingJob в задании hello StreamingJob.

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a>New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput
Создает новые или обновляет существующие входные данные в задании Stream Analytics.

Hello Привет вводимых данных может быть указано имя в hello JSON-файл или в командной строке hello. Если указаны оба имени hello hello в командной строке необходимо hello то же, что один hello в файле hello.

Если указать входной, уже существует и не указывайте hello — параметр Force, командлет hello запрашивает ли tooreplace hello существующий вход.

Если нужно задать hello — параметр Force и существующий ввода имени, hello входные данные будут заменены без подтверждения.

Подробные сведения о структуре файла JSON hello и содержимое, см. в разделе toohello [создать входные данные (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input] раздел hello [API REST управления Stream Analytics Справочная библиотека][stream.analytics.rest.api.reference].

**Пример 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Эта команда PowerShell создает новые входные данные из файла hello Input.json. Если существующий вход с именем hello, указанной в файле ввода определения hello уже определено, hello командлет запросит ли tooreplace его.

**Пример 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Эта команда PowerShell создает новые входные данные в задании hello вызывается EntryStream. Если существующий вход с таким именем уже определено, hello командлет запросит ли tooreplace его.

**Пример 3**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Эта команда PowerShell заменяет определение hello hello существующий источник входных данных называется EntryStream с определением hello из файла hello.

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a>New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob
Создает новое задание Stream Analytics в Microsoft Azure или обновляет определение hello существующего указанного задания.

Имя задания hello Hello указываются в hello JSON-файл или в командной строке hello. Если указаны оба имени hello hello в командной строке необходимо hello то же, что один hello в файле hello.

Если указать имя задания, которое уже существует и не указывайте hello — параметр Force, командлет hello запрашивает ли tooreplace hello существующего задания.

Если нужно задать hello — параметр Force и задания имени существующего определения задания hello будут заменены без подтверждения.

Подробные сведения о структуре файла JSON hello и содержимое, см. в разделе toohello [создать задание Stream Analytics] [ msdn-rest-api-create-stream-analytics-job] раздел hello [Справочник API REST управления Stream Analytics Библиотека][stream.analytics.rest.api.reference].

**Пример 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Эта команда PowerShell создает новое задание из определения hello в JobDefinition.json. Если существующее задание с именем hello, указанной в файле определения задания hello уже определено, hello командлет запросит ли tooreplace его.

**Пример 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Эта команда PowerShell заменяет hello определения задания для StreamingJob.

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a>New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput
Создает новые или обновляет существующие выходные данные в задании Stream Analytics.  

можно указать имя Hello hello выходных данных, в hello JSON-файл или в командной строке hello. Если указаны оба имени hello hello в командной строке необходимо hello то же, что один hello в файле hello.

Если указано ключевое слово output, который уже существует и не указывайте hello — параметр Force, командлет hello запрашивает ли tooreplace hello существующего выхода.

При указании hello — параметр Force и укажите имя существующего выходного, hello выходные данные будут заменены без подтверждения.

Подробные сведения о структуре файла JSON hello и содержимое, см. в разделе toohello [создание выходных данных (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output] раздел hello [API REST управления Stream Analytics Справочная библиотека][stream.analytics.rest.api.reference].

**Пример 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Эта команда PowerShell создает новые выходные данные с именем «выход» в задании hello StreamingJob. Если существующий выходных данных с таким именем уже определено, hello командлет запросит ли tooreplace его.

**Пример 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Эта команда PowerShell заменяет определение «выход» в задании hello StreamingJob hello.

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a>New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation
Создает новое преобразование в задании Stream Analytics или обновляет существующий преобразования hello.

можно указать имя Hello преобразования «hello», в hello JSON-файл или в командной строке hello. Если указаны оба имени hello hello в командной строке необходимо hello то же, что один hello в файле hello.

Если указано преобразование, которое уже существует и не указывайте hello — параметр Force, командлет hello запрашивает ли tooreplace hello существующего преобразования.

При указании hello — параметр Force и укажите имя существующей преобразование, преобразование «hello» будут заменены без подтверждения.

Подробные сведения о структуре файла JSON hello и содержимое, см. в разделе toohello [Создание преобразования (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] раздел hello [управления Stream Analytics Справочная библиотека API REST][stream.analytics.rest.api.reference].

**Пример 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Эта команда PowerShell создает новое преобразование называется StreamingJobTransform в задании hello StreamingJob. Если преобразование существующих с таким именем уже определено, hello командлет запросит ли tooreplace его.

**Пример 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 Эта команда PowerShell заменяет определение StreamingJobTransform hello в задании hello StreamingJob.

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a>Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput
Асинхронно удаляет указанные входные данные из задания Stream Analytics в Microsoft Azure.  
При указании hello — параметр Force, hello ввода будет удален без подтверждения.

**Пример 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Azure PowerShell 1.0.  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Эту команду PowerShell, удаляет hello ввода EventStream в задании hello StreamingJob.  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a>Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob
Асинхронно удаляет указанное задание Stream Analytics в Microsoft Azure.  
При указании hello — параметр Force hello задание будет удален без подтверждения.

**Пример 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0.  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Эта команда PowerShell удаляет задание hello StreamingJob.  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a>Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput
Асинхронно удаляет указанные выходные данные из задания Stream Analytics в Microsoft Azure.  
При указании hello — параметр Force hello выходные данные будут удалены без подтверждения.

**Пример 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0.  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Выходные данные этого PowerShell команда удаляет hello выходные данные в задании hello StreamingJob.  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a>Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob
Асинхронно развертывает и запускает задание Stream Analytics в Microsoft Azure.

**Пример 1**

Azure PowerShell 0.9.8:  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Azure PowerShell 1.0.  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Эта команда PowerShell запускает hello задание StreamingJob с временем начала пользовательский вывод tooDecember 12, 2012 г., 12:12:12 UTC.

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a>Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob
Асинхронно останавливает задание Stream Analytics в Microsoft Azure и освобождает используемые ресурсы. Hello определение задания и метаданные останутся доступными в подписке через портал Azure hello и API управления, hello задания можно изменить и перезапустить. Вы не будете платить за задание в состоянии остановки hello.

**Пример 1**

Azure PowerShell 0.9.8:  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0.  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Эта команда PowerShell останавливает задание hello StreamingJob.  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a>Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput
Проверяет возможность hello tooa tooconnect Stream Analytics указано входных данных.

**Пример 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0.  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Это PowerShell команды тесты hello состояние соединения hello ввода EntryStream в StreamingJob.  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a>Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput
Возможность hello тесты tooa tooconnect Stream Analytics указаны выходные данные.

**Пример 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0.  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Выходные данные в StreamingJob вывода этого PowerShell команды тесты hello состояние соединения hello.  

## <a name="get-support"></a>Получение поддержки
За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics). 

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

