---
title: "Предупреждения виртуальной Машины Windows Azure с Runbook автоматизации исправлять AAA» | Документы Microsoft»"
description: "В этой статье показано, как предупреждения toointegrate виртуальной машине Azure с Runbook автоматизации Azure и автоматически устранить проблемы"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a>Сценарий службы автоматизации Azure: обработка оповещений виртуальной машины Azure
Новая функция позволяет Runbook автоматизации toorun предупреждения виртуальной машины (VM) tooconfigure выпустили Azure Automation и виртуальных машинах Azure. Эта новая возможность позволяет tooautomatically выполнение стандартных исправления в оповещениях tooVM ответа, как и перезапуска или остановки hello виртуальной Машины.

Ранее, при создании правила оповещения виртуальной Машины можно было слишком[укажите перехватчик службы автоматизации](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook в runbook hello порядок toorun всякий раз, когда создано оповещение hello. Тем не менее это вам требовалось рабочих hello toodo создания hello, создания hello веб-перехватчика для hello runbook и скопировав и вставив веб-перехватчика hello во время создания правила оповещения. С этот новый выпуск hello процесс намного проще, так как напрямую, можно выбрать из списка runbook во время создания правила оповещения и выбрана учетная запись автоматизации, которая будет выполнять hello runbook или легко создать учетную запись.

В этой статье будут показано, как просто можно tooset копирование оповещение виртуальной Машины Azure и настроены toorun runbook автоматизации всякий раз, когда предупреждение hello триггеров. Примеры сценариев включают перезапуск виртуальной Машины, если использование памяти hello превышает некоторое пороговое значение из-за tooan приложение hello виртуальной Машины с утечкой памяти или остановка виртуальной Машины, когда находятся ниже 1% последний час hello ЦП в пользовательском режиме, а не используется. Вы также узнаете, как hello автоматизировать создание субъекта-службы автоматической учетной записи упрощает использование hello модулей Runbook в Azure предупреждения исправления.

## <a name="create-an-alert-on-a-vm"></a>Создание оповещения на виртуальной машине
Выполните hello при порогом выполнены следующие шаги tooconfigure предупреждения toolaunch runbook.

> [!NOTE]
> В этом выпуске поддерживаются только виртуальные машины V2. Поддержка классических виртуальных машин будет добавлена в ближайшее время.  
> 
> 

1. Войдите в портал Azure toohello и нажмите кнопку **виртуальные машины**.  
2. Выберите одну из виртуальных машин.  Hello колонке панели мониторинга виртуальной машины будет отображаться и hello **параметры** колонке tooits справа.  
3. Из hello **параметры** колонки в списке выберите раздел мониторинг hello **правила предупреждения**.
4. На hello **предупреждения правила** колонка, щелкните **добавить оповещение**.

Это открывает hello **Добавление правила оповещения** колонки, где можно настроить условия hello для оповещения hello и выбрать одно или все из этих параметров: Отправка toosomeone электронной почты, использование системы предупреждений tooanother hello tooforward веб-перехватчика, и (или) Запустите runbook автоматизации в выпуске hello tooremediate попытки ответа.

## <a name="configure-a-runbook"></a>Настройка модуля Runbook
tooconfigure toorun runbook, по достижении порога оповещения hello виртуальной Машины, выберите **Runbook службы автоматизации**. В hello **Настройка runbook** колонки, можно выбрать hello runbook toorun и runbook hello toorun учетной записи службы автоматизации hello в.

![Настройка модуля Runbook службы автоматизации и создание учетной записи службы автоматизации](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> В этой версии можно выбирать из трех Runbook, которые предоставляет службу hello — перезапуск виртуальной Машины, остановить виртуальную Машину или удалить виртуальную Машину (Удалить).  Здравствуйте возможность tooselect другие модули Runbook или один из собственных модулей Runbook будут доступны в будущих выпусках.
> 
> 

![Модули Runbook toochoose из](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

Здравствуйте, выбрав один из трех hello, доступные модули Runbook, **учетной записи автоматизации** появляется в раскрывающемся списке, и можно будет выбрать автоматизации runbook hello учетной записи будет выполняться как. Модули Runbook должны toorun в контексте hello [учетной записи автоматизации](automation-security-overview.md) , находящегося в вашей подписке Azure. Можно выбрать уже созданную учетную запись службы автоматизации или создать новую учетную запись.

Hello Runbook, которые предоставляются проверки подлинности tooAzure с помощью субъекта-службы. Если в одной из существующих учетных записей автоматизации toorun hello runbook, мы будет автоматически создавать hello службы участника. При выборе новой учетной записи автоматизации toocreate затем будут автоматически созданы hello учетной записи и hello участника-службы. В обоих случаях два средства также будет создан в учетной записи автоматизации — ресурс сертификата с именем hello **AzureRunAsCertificate** и средств подключения, с именем **AzureRunAsConnection**. будет использовать модули Runbook Hello **AzureRunAsConnection** tooauthenticate с Azure в действие управления tooperform hello порядке по отношению к hello виртуальной Машины.

> [!NOTE]
> Hello участника-службы в область hello подписки создается и назначается роль участника hello. Эта роль необходима для hello учетной записи toohave разрешение toorun автоматизации модулей Runbook toomanage виртуальных машинах Azure.  Создание Hello машин учетной записи и/или субъекта-службы — однократного события. После их создания, можно использовать модули Runbook toorun этой учетной записи для других оповещений на виртуальной Машине Azure.
> 
> 

При нажатии кнопки **ОК** настроено оповещение hello и если вы выбрали параметр hello toocreate учетную запись автоматизации, он будет создан вместе с hello участника-службы.  Это может занять несколько секунд toocomplete.  

![Настройка модуля Runbook](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

После завершения настройки hello вы увидите имя hello hello runbook отображаются в hello **Добавление правила оповещения** колонку.

![Модуль Runbook настроен](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

Нажмите кнопку **ОК** в hello **Добавление правила оповещения** колонки и hello правило оповещения будут создаваться и активировать, если hello виртуальная машина находится в состоянии выполнения.

### <a name="enable-or-disable-a-runbook"></a>Включение и отключение модуля Runbook
Если у вас есть runbook, настроенных для оповещения, его можно отключить без удаления конфигурации runbook hello. Это дает предупреждение hello tookeep под управлением и возможно тестировании некоторых правил оповещения hello и затем повторно включать hello runbook.

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a>Создание модуля Runbook, который работает с оповещениями Azure
При выборе модуля в рамках Azure правила генерации оповещений hello модуль должен логики toohave toomanage hello данных предупреждений, передаваемое tooit.  Создается при настройке модуля в правиле оповещения веб-перехватчика для hello runbook; Этот веб-перехватчика является, то используется toostart hello runbook каждого предупреждения триггеры hello времени.  toostart hello Hello реальный вызов runbook является URL-адрес HTTP POST веб-перехватчика запроса toohello. текст Hello hello POST-запрос содержит неверный формат JSON объект, который содержит связанные toohello оповещение полезных свойств.  Как можно увидеть ниже, предупреждения данных hello содержит сведения, такие как идентификатор подписки, resourceGroupName, resourceName и типа ресурса.

### <a name="example-of-alert-data"></a>Пример данных оповещения
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

Получив hello веб-перехватчика службы автоматизации hello HTTP POST он извлекает данные предупреждения hello и передает его toohello runbook в hello WebhookData runbook входного параметра.  Ниже приведен пример модуля runbook, показывающий, как toouse hello параметр WebhookData и извлечения данных о предупреждениях hello и использовать его hello toomanage ресурсов Azure, вызвавшей предупреждение hello.

### <a name="example-runbook"></a>Пример модуля Runbook
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a>Сводка
При настройке оповещение на Виртуальной машине Azure, теперь у вас есть tooeasily возможность hello настройки автоматизации runbook tooautomatically действий исправления при hello предупреждение запускает. Для этого выпуска можно выбрать из модулей Runbook toorestart, остановить или удаление виртуальной Машины, в зависимости от вашего сценария предупреждения. Это просто hello начало Включение сценариев, где вы управляете действия hello (уведомление, устранение неполадок, исправления), которые будут выполнены автоматически, когда инициирует предупреждение.

## <a name="next-steps"></a>Дальнейшие действия
* tooget к работе с графический Runbook в разделе [Мой первый графический runbook](automation-first-runbook-graphical.md)
* tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)
* в разделе toolearn Дополнительные сведения о типах runbook, их преимущества и ограничения, [типов runbook службы автоматизации Azure](automation-runbook-types.md)

