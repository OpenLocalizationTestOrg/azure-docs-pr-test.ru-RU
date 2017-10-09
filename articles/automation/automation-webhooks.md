---
title: "runbook службы автоматизации Azure с веб-перехватчика aaaStarting | Документы Microsoft"
description: "Веб-перехватчика, позволяющую toostart клиента runbook в автоматизации Azure вызова HTTP.  В этой статье описывается как toocreate веб-перехватчика и как один toostart toocall runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a>Запуск Runbook службы автоматизации Azure с помощью объекта webhook
Объект *веб-перехватчика* позволяет toostart конкретного модуля runbook в автоматизации Azure через один HTTP-запроса. Это позволяет внешней службы, такие как Visual Studio Team Services, GitHub, аналитика журналов пакета управления Operations Microsoft или пользовательских приложений toostart модулей Runbook без реализации полного решения с использованием hello API автоматизации Azure.  
![Обзор веб-перехватчиков](media/automation-webhooks/webhook-overview-image.png)

Вы можете сравнить веб-перехватчиков tooother способов запуска модуля runbook [запуск runbook в автоматизации Azure](automation-starting-a-runbook.md)

## <a name="details-of-a-webhook"></a>Подробные сведения о Webhook
Hello следующей таблице описаны свойства hello, необходимо настроить для веб-перехватчик.

| Свойство | Описание |
|:--- |:--- |
| Имя |Вы можете указать любое имя, которое требуется для веб-перехватчика, так как это не предоставляется toohello клиента.  Оно используется только для вас tooidentify hello runbook в автоматизации Azure. <br>  Рекомендуется следует предоставить веб-перехватчика hello имя связанных toohello клиента, который будет его использовать. |
| URL-адрес |Hello URL-адрес веб-перехватчика hello: hello уникальный адрес, что клиент вызывает с runbook hello HTTP POST toostart связанные toohello веб-перехватчика.  Он создается автоматически при создании веб-перехватчика hello.  Нельзя указать другой URL-адрес. <br> <br>  Hello URL-адрес содержит маркер безопасности, позволяющий hello toobe runbook, вызываемые сторонняя система без дальнейшей проверки подлинности. По этой причине он должен рассматриваться как пароль.  По соображениям безопасности можно только hello представление создается URL-адрес в Azure портал на веб-перехватчика hello время hello hello. Следует отметить hello URL-адрес в безопасном месте для будущего использования. |
| Срок действия |Как и сертификат, каждый объект Webhook имеет срок действия, после которого он больше не используется.  Эта дата истечения срока действия можно изменить после создания веб-перехватчика hello. |
| Включено |При создании объекта Webhook он по умолчанию включается.  Если задать tooDisabled, то клиент не будет возможности toouse его.  Можно задать hello **включено** создается свойство при создании веб-перехватчика hello, или в любое время один раз. |

### <a name="parameters"></a>Параметры
Веб-перехватчика можно определить значения для параметров runbook, которые используются при запуске hello runbook, что веб-перехватчика. веб-перехватчика Hello должна содержать значения для всех обязательных параметров hello runbook и могут включать значения для необязательных параметров. Веб-перехватчика tooa настроить значение параметра можно изменить даже после создания hello webhoook. Несколько связанных веб-перехватчиков tooa отдельного модуля runbook можно использовать различные значения параметра.

При запуске модуля runbook с помощью веб-перехватчика клиента, он не может переопределить hello значения параметров, определенные в веб-перехватчика hello.  tooreceive данные от клиента hello, hello runbook может принимать один параметр с именем **$WebhookData** тип [object], который будет содержать данные этого клиента hello включает в себя в запросе POST hello.

![Свойства Webhookdata](media/automation-webhooks/webhook-data-properties.png)

Hello **$WebhookData** объект будет иметь hello следующие свойства:

| Свойство | Описание |
|:--- |:--- |
| WebhookName |Имя веб-перехватчика hello Hello. |
| RequestHeader |Хэш-таблица с заголовками hello hello входящего запроса POST. |
| RequestBody |текст Hello hello входящего запроса POST.  Это сохранит все форматирование, такое как строка, JSON, XML или данные, закодированные в форме. Hello runbook должно быть написано toowork с форматом данных hello, которая ожидается. |

Нет конфигураций hello необходимые toosupport веб-перехватчика hello **$WebhookData** параметра, и hello runbook не требуется tooaccept его.  Если hello runbook не определяет параметр hello, все сведения о запросе hello, отправляемых с клиента hello учитывается.

Если указать значение для $WebhookData при создании веб-перехватчика hello, что значение будет переопределенное в начале веб-перехватчика hello hello runbook hello данными из hello клиентский запрос POST, даже если клиент hello не включать данные в текст запроса hello.  При запуске модуля runbook, который имеет $WebhookData с помощью метода, отличного от веб-перехватчик может предоставить значение для $Webhookdata, будут распознаваться hello runbook.  Это значение должно быть объектом с hello же [свойства](#details-of-a-webhook) как $Webhookdata, этого модуля hello должным образом можно работать с ними, как если бы он работал фактическое WebhookData, переданных веб-перехватчик.

Например если вы начинаете hello следующую runbook из портала Azure hello и toopass WebhookData некоторые образцы для тестирования, так как WebhookData — это объект, он должен передаваться как JSON в hello пользовательского интерфейса.

![Параметр WebhookData из пользовательского интерфейса](media/automation-webhooks/WebhookData-parameter-from-UI.png)

Для hello выше runbook, если у вас есть следующие свойства для параметра WebhookData hello hello:

1. WebhookName: *MyWebhook*
2. RequestHeader: *From=Test User*
3. RequestBody: *[“VM1”, “VM2”]*

Затем можно передать следующие значения JSON в hello пользовательского интерфейса для параметра WebhookData hello hello:  

* {"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}

![Запуск параметра WebhookData из пользовательского интерфейса](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> с заданием runbook hello регистрируются Hello значения всех входных параметров.  Это означает, что любой входных данных, предоставленных клиентом hello в запрос веб-перехватчика hello будет tooanyone регистрируются и доступны с помощью задания автоматизации toohello доступа.  По этой причине необходимо соблюдать осторожность при указании критических данных в вызовах Webhook.
>

## <a name="security"></a>Безопасность
безопасность веб-перехватчика Hello зависит от hello конфиденциальность его URL-адрес, который содержит маркер безопасности, позволяющий ему toobe вызывается. Службы автоматизации Azure не будет выполнять проверку подлинности hello запроса до тех пор, пока он станет toohello правильный URL-адрес. По этой причине веб-привязок не должен использоваться для модулей Runbook, которые выполняют конфиденциальными функции без использования альтернативный способ проверки запроса hello.

Можно включить логику в toodetermine runbook hello, что она была вызвана веб-перехватчика, проверив hello **WebhookName** свойства параметра hello $WebhookData. Hello runbook может выполнять последующие проверки путем поиска определенной информации в hello **RequestHeader** или **RequestBody** свойства.

Другая стратегия — toohave hello runbook выполнить некоторые проверки внешнего условия при получении запроса на веб-перехватчика.  Например рассмотрим книгу выполнения, вызывается GitHub всякий раз, когда новый репозиторий GitHub tooa фиксации.  Hello runbook может подключиться toovalidate tooGitHub, новые фиксации просто возникла перед продолжением.

## <a name="creating-a-webhook"></a>Создание объекта Webhook
Используйте следующие процедуры toocreate новый модуль runbook связан с веб-перехватчика tooa в hello портал Azure hello.

1. Из hello **Runbooks колонки** hello портал Azure, щелкните runbook hello, hello веб-перехватчика начнет tooview колонке детализации.
2. Нажмите кнопку **веб-перехватчика** вверху hello hello колонке tooopen hello **добавить веб-перехватчика** колонку. <br>
   ![Кнопка Webhook](media/automation-webhooks/webhooks-button.png)
3. Нажмите кнопку **создать новый веб-перехватчика** tooopen hello **создать веб-перехватчика колонке**.
4. Укажите **имя**, **Дата окончания срока действия** для веб-перехватчика hello и является ли он должен быть включен. Подробные сведения об этих свойствах см. в разделе [Details of a webhook](#details-of-a-webhook) (Сведения об объекте webhook).
5. Щелкните значок копирования hello и нажмите Ctrl + C toocopy hello URL-адрес веб-перехватчика hello.  Сохраните URL-адрес в безопасном месте.  **После создания веб-перехватчика hello hello URL-адрес не удается получить еще раз.** <br>
   ![URL-адрес объекта webhook](media/automation-webhooks/copy-webhook-url.png)
6. Нажмите кнопку **параметры** tooprovide значения для параметров runbook hello.  Если hello runbook обязательные параметры, затем нельзя веб-перехватчик может toocreate hello, если не предоставлены значения.
7. Нажмите кнопку **создать** веб-перехватчика toocreate hello.

## <a name="using-a-webhook"></a>Использование объекта Webhook
toouse веб-перехватчика после его создания клиентского приложения должен выдать HTTP POST с hello URL-адрес для веб-перехватчика hello.  синтаксис Hello веб-перехватчика hello будут в кодировке hello.

    http://<Webhook Server>/token?=<Token Value>

Hello клиент получит следующие коды возврата из запроса POST hello hello.  

| Код | текст | Описание |
|:--- |:--- |:--- |
| 202 |Принято |Hello запрос принят и hello runbook был успешно помещен в очередь. |
| 400 |Ошибка запроса |Hello запрос не был принят для одной из следующих причин hello. <ul> <li>веб-перехватчика Hello истек.</li> <li>Hello веб-перехватчик отключен.</li> <li>Недопустимый токен Hello в URL-АДРЕСЕ hello.</li>  </ul> |
| 404 |Не найдено |Hello запрос не был принят для одной из следующих причин hello. <ul> <li>веб-перехватчика Hello не найден.</li> <li>Hello runbook не найдено.</li> <li>Hello учетная запись не найдена.</li>  </ul> |
| 500 |Внутренняя ошибка сервера |Hello URL-адрес является допустимым, но произошла ошибка.  Повторно отправьте запрос hello. |

Предположим, что hello запрос выполнен успешно, hello веб-перехватчика ответ содержит идентификатор задания hello в формате JSON следующим образом. Он будет содержать идентификатор одним заданием, но позволяет hello формат JSON для возможных будущих улучшений.

    {"JobIds":["<JobId>"]}  

Hello клиент не может определить при завершении задания runbook hello или его состояние завершения с веб-перехватчика hello.  Он определяет эти сведения, такие как с помощью идентификатора задания hello одного метода другим [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) или hello [API автоматизации Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).

### <a name="example"></a>Пример
Следующий пример Hello использует Windows PowerShell toostart runbook с веб-перехватчик.  Обратите внимание, что в любом языке, способном выполнить HTTP-запрос, можно использовать объект Webhook; Windows PowerShell используется здесь просто для примера.

Hello runbook ожидает список виртуальных машин, в формате JSON в тексте hello hello запроса в формате. Сведения о, выполняется запуск hello runbook и hello даты и времени, она запущена в заголовке hello hello запроса также предоставляются вместе.      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


Hello на рисунке показаны сведения о заголовке hello (с помощью [Fiddler](http://www.telerik.com/fiddler) трассировки) из этого запроса. Сюда входят стандартные заголовки HTTP-запроса на добавление toohello настраиваемые дата и из заголовков, которые мы добавили.  Каждое из этих значений является доступной toohello runbook в hello **RequestHeaders** свойство **WebhookData**.

![Кнопка Webhook](media/automation-webhooks/webhook-request-headers.png)

Hello на рисунке показаны hello тексте hello запроса (с помощью [Fiddler](http://www.telerik.com/fiddler) трассировки), доступные toohello runbook в hello **RequestBody** свойство **WebhookData**. Это в формате JSON за hello формат, который был включен в тексте hello hello запроса.     

![Кнопка Webhook](media/automation-webhooks/webhook-request-body.png)

Hello следующем рисунке показан запрос hello, отправляемых из Windows PowerShell, а также получаемые ответы hello.  Идентификатор задания Hello извлекается из ответа hello и tooa преобразованной строки.

![Кнопка Webhook](media/automation-webhooks/webhook-request-response.png)

Hello следующий пример модуля runbook принимает hello предыдущего примера запрос и запускает hello виртуальных машин, указанный в тексте запроса hello.

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a>Запуск модулей Runbook в ответ tooAzure оповещения
Модули Runbook с поддержкой веб-перехватчика также может быть используется tooreact[оповещения Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Ресурсы в Azure можно отслеживать путем сбора статистики hello как производительности, доступности и использования с помощью hello оповещения Azure. Вы можете получать оповещения на основе отслеживания метрик или событий в ресурсах Azure, сейчас учетные записи автоматизации поддерживают только метрики. Если значение hello указанной метрики превышает hello установленный порог, заданный или, если настроена hello события затем toohello администратора или соадминистраторам tooresolve hello предупреждение службы, Дополнительные сведения о показателях отправляется уведомление о и событий можно найти слишком[ Оповещения Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

Помимо использования оповещения Azure как система уведомлений, можно также начнем Runbook в tooalerts ответа. Служба автоматизации Azure обеспечивает hello возможность toorun включен веб-перехватчика Runbook с оповещения Azure. При превышении показателем hello настроен пороговое значение, то hello правило оповещения становится активным и триггеры hello веб-перехватчика автоматизации, который в свою очередь выполняет hello runbook.

![Объекты Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a>Контекст оповещения
ЦП этой машины является одним из hello метрики производительности, учитывайте ресурс Azure, такие как виртуальной машины. Если hello ЦП — 100% или превышает определенное длительного периода времени, может потребоваться toorestart hello виртуальной машины toofix hello проблему. Это может быть решена Настройка виртуальной машины toohello правила оповещения и это правило имеет процент использования ЦП в качестве его метрик. Здесь процент использования ЦП берется только в качестве примера, но существует множество метрик, которые можно настроить tooyour Azure ресурсов и перезапуск hello виртуальной машины — это действие, будет предпринято toofix эту проблему, hello runbook tootake можно настроить другие действия.

После этого правила оповещения hello становится активным и триггеры hello runbook с поддержкой веб-перехватчика, он отправляет runbook toohello hello контекст предупреждения. [Контекст предупреждения](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) содержит сведения, включая **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** и **Timestamp** , необходимые для hello runbook tooidentify hello ресурса, на котором он будет предпринимать действия. Предупреждения, контекст внедрен в часть текста hello hello **WebhookData** объекта отправленных toohello runbook, и можно осуществить с помощью **Webhook.RequestBody** свойство

### <a name="example"></a>Пример
Создание виртуальной машины Azure в подписку и связывание [предупреждения toomonitor ЦП в процентах метрика](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). При создании предупреждения hello убедитесь, что необходимо заполнить поле веб-перехватчика hello hello URL-адрес веб-перехватчика hello, который был создан при создании веб-перехватчика hello.

Hello следующий пример модуля runbook инициируется при hello правило оповещения становится активным и собирает параметры hello контекст предупреждения, которые требуются для hello tooidentify runbook hello ресурса, на котором он будет предпринимать действия.

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о различных способов toostart runbook см. в разделе [запуск Runbook](automation-starting-a-runbook.md).
* Сведения о hello Просмотр состояния задания Runbook, см. в разделе слишком[выполнение модуля Runbook в автоматизации Azure](automation-runbook-execution.md).
* toouse действия tootake автоматизации Azure в Azure Alerts. в статье toolearn [устранения предупреждения виртуальной Машины Azure с Runbook автоматизации](automation-azure-vm-alert-integration.md).
