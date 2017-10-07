---
title: "aaaStarting и остановки виртуальных машин - Graph | Документы Microsoft"
description: "Версия рабочего процесса PowerShell сценарий автоматизации Azure, включая модули Runbook toostart и остановить классических виртуальных машин."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 62d93170-ca3d-42ef-ac1d-6d50b61ac87d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 5add8d8cf35ea2e89a570744755ac7db0a6feb07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Сценарий для службы автоматизации Azure: запуск и остановка виртуальных машин
Этот сценарий автоматизации Azure включает модули Runbook toostart и остановить классических виртуальных машин.  Этот сценарий можно использовать для следующих hello:  

* Модули Runbook hello без каких-либо используйте в собственной среде.
* Измените функциональность tooperform пользовательские модули Runbook hello.  
* Вызывает hello модулей Runbook из другого модуля runbook как часть общего решения.
* Используйте модули Runbook hello как разработка основные понятия runbook toolearn учебники.

> [!div class="op_single_selector"]
> * [Графический](automation-solution-startstopvm-graphical.md)
> * [Рабочий процесс PowerShell](automation-solution-startstopvm-psworkflow.md)
>
>

Это версия графический runbook hello этого сценария. Доступно также решение с использованием [модулей Runbook рабочего процесса PowerShell](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-hello-scenario"></a>Начало сценария hello
Этот сценарий состоит из двух hello два графических модулей Runbook, которые можно загрузить из следующих ссылок.  В разделе hello [версии рабочего процесса PowerShell](automation-solution-startstopvm-psworkflow.md) этого сценария для ссылки toohello модулях Runbook рабочего процесса PowerShell.

| Модуль Runbook | Ссылка | Тип | Описание |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Запуск графического модуля Runbook классической виртуальной машины Azure](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Графический |Запуск всех классических виртуальных машин в подписке Azure или всех виртуальных машин с определенным именем службы. |
| StopAzureClassicVM |[Остановка графического модуля Runbook классической виртуальной машины Azure](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Графический |Остановка всех классических виртуальных машин в учетной записи службы автоматизации или всех виртуальных машин с определенным именем службы. |

## <a name="installing-and-configuring-hello-scenario"></a>Установка и настройка сценария hello
### <a name="1-install-hello-runbooks"></a>1. Установка модулей Runbook hello
После загрузки модулей Runbook hello, их можно импортировать с помощью процедуры hello в [процедуры графический runbook](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-hello-description-and-requirements"></a>2. Просмотрите описание hello и требования
модули Runbook Hello включать действие с именем **сведения об установке** , содержится описание и необходимые активы.  Эти сведения можно просмотреть, выбрав hello **сведения об установке** действия, а затем hello **скрипта рабочего процесса** параметра.  Можно также получить hello же сведения из этой статьи.

### <a name="3-configure-assets"></a>3. Настройка ресурсов
Hello Runbook требуют hello следующие ресурсы, которые необходимо создать и заполнить с соответствующими значениями.  Привет, называются по умолчанию.  Ресурсы можно использовать с разными именами, при указании этих имен в hello [входных параметров](#using-the-runbooks) при запуске hello runbook.

| Тип ресурса | Имя по умолчанию | Описание |
|:--- |:--- |:--- |:--- |
| [Учетные данные](automation-credentials.md) |AzureCredential |Содержит учетные данные учетной записи, которая имеет полномочия toostart и остановки виртуальных машин в hello подписки Azure. |
| [Variable](automation-variables.md) |AzureSubscriptionId |Содержит идентификатор подписки hello подписки Azure. |

## <a name="using-hello-scenario"></a>С помощью сценария hello
### <a name="parameters"></a>Параметры
Hello Runbook каждый имеют следующие hello [входных параметров](automation-starting-a-runbook.md#runbook-parameters).  Вам потребуется указать значения всех обязательных параметров и, при необходимости, указать значения дополнительных параметров.

| Параметр | Тип | Обязательно | Описание |
|:--- |:--- |:--- |:--- |
| ServiceName |string |Нет |Если значение указано, запускаются или останавливаются все виртуальные машины с таким именем службы.  Если значение не указано, затем классических виртуальных машин в hello подписки Azure запуска или остановки. |
| AzureSubscriptionIdAssetName |string |Нет |Содержит имя hello hello [переменной активов](#installing-and-configuring-the-scenario) , содержащее идентификатор подписки hello подписки Azure.  Если значение не указано, используется значение *AzureSubscriptionId* . |
| AzureCredentialAssetName |string |Нет |Содержит имя hello hello [актива учетных данных](#installing-and-configuring-the-scenario) , содержащий hello учетные данные для hello runbook toouse.  Если не указать это значение, будет использоваться значение *AzureCredential* . |

### <a name="starting-hello-runbooks"></a>Запуск модулей Runbook hello
Можно использовать любой из методов hello в [запуск runbook в автоматизации Azure](automation-starting-a-runbook.md) toostart либо hello Runbook в этой статье.

Следующие примеры команд Hello использует Windows PowerShell toorun **StartAzureClassicVM** toostart все виртуальные машины с именем службы hello *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Выходные данные
модули Runbook Hello будет [выводить сообщение](automation-runbook-output-and-messages.md) для каждой виртуальной машины, указывающее, ли hello Пуск или инструкция stop успешно отправлен.  Можно найти конкретную строку в результате hello toodetermine hello выходные данные для каждого модуля runbook.  в hello в следующей таблице перечислены строки возможного выхода Hello.

| Модуль Runbook | Условие | Сообщение |
|:--- |:--- |:--- |
| StartAzureClassicVM |Виртуальная машина уже запущена |MyVM is already running |
| StartAzureClassicVM |Запрос запуска виртуальной машины успешно отправлен |MyVM запущена |
| StartAzureClassicVM |Не удалось выполнить запрос запуска виртуальной машины |Не удалось выполнить MyVM toostart |
| StopAzureClassicVM |Виртуальная машина уже запущена |MyVM уже остановлена |
| StopAzureClassicVM |Запрос запуска виртуальной машины успешно отправлен |MyVM запущена |
| StopAzureClassicVM |Не удалось выполнить запрос запуска виртуальной машины |Не удалось выполнить MyVM toostart |

Ниже приведен образ с помощью hello **StartAzureClassicVM** как [дочернего модуля](automation-child-runbooks.md) в образце графического модуля runbook.  В следующей таблице hello используется hello условные связи.

| Ссылка | Критерии |
|:--- |:--- |
| Рабочая ссылка |$ActivityOutput['StartAzureClassicVM'] -like "\* запущена" |
| Ошибочная ссылка |$ActivityOutput['StartAzureClassicVM'] -notlike "\* запущена" |

![Пример дочернего модуля Runbook](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Подробный разбор
Ниже приведен подробный разбор Runbook hello в этом сценарии.  Эти сведения можно использовать tooeither Настройка модулей Runbook hello или просто toolearn из них для создания собственных сценариев автоматизации.

### <a name="authentication"></a>Аутентификация
![Аутентификация](media/automation-solution-startstopvm/graphical-authentication.png)

Hello runbook начинается с действия hello tooset [учетные данные](automation-credentials.md) и подписку Azure, которая будет использоваться для оставшихся hello hello runbook.

Здравствуйте, первые два действия **получить идентификатор подписки** и **получить учетные данные Azure**, получить hello [активы](#installing-the-runbook) , которые используются в следующих двух действий hello.  Эти действия может напрямую указывать hello активы, но они должны иметь имена активов hello.  Поскольку мы разрешили toospecify hello пользователя эти имена в hello [входных параметров](#using-the-runbooks), нам нужно активы hello tooretrieve эти действия с именем, указанным входным параметром.

**-AzureAccount** наборов hello учетные данные, которые будут использоваться для оставшихся hello hello runbook.  Hello учетных данных ресурса, который извлекает из **получить учетные данные Azure** должны иметь доступ toostart и остановить виртуальные машины в hello подписки Azure.  Hello, используемый выбрана подписка **Select-AzureSubscription** с использованием идентификатора подписки hello из **получить идентификатор подписки**.

### <a name="get-virtual-machines"></a>Получение виртуальных машин
![Получение виртуальных машин](media/automation-solution-startstopvm/graphical-getvms.png)

модуль Hello должен toodetermine, какие виртуальные машины он будет работать и ли они уже запуска или остановки (в зависимости от hello runbook).   Одно из двух действий приведет к получению виртуальных машин hello.  **Получить виртуальные машины в службе** будет выполняться, если hello *ServiceName* входной параметр для hello runbook содержит значение.  **Получить все виртуальные машины** будет выполняться, если hello *ServiceName* входного параметра для hello runbook не содержит значение.  Эта логика выполняется путем hello условные связи перед каждым действием.

Оба действия используют hello **Get-AzureVM** командлета.  **Получить все виртуальные машины** hello использует **ListAllVMs** параметру tooreturn все виртуальные машины.  **Получить виртуальные машины в службе** hello использует **GetVMByServiceAndVMName** параметр набора и предоставляющая hello **ServiceName** входного параметра для hello **ServiceName**параметра.  

### <a name="merge-vms"></a>Объединение виртуальных машин
![Объединение виртуальных машин](media/automation-solution-startstopvm/graphical-mergevms.png)

Hello **слияния виртуальные машины** действие является обязательным tooprovide ввода слишком**Start-AzureVM** какие требуют hello имя и имя службы toostart hello виртуальные машины.  Входные данные могут быть получены из действия **Get All VMs** (Получить все виртуальные машины) или **Get VMs in Service** (Получить виртуальные машины в службе), но **Start-AzureVM** позволяет указать в качестве входных данных только одно из этих действий.   

сценарий Hello — toocreate **слияния виртуальные машины** выполняемая hello **Write-Output** командлета.  Hello **InputObject** параметр для этого командлета является выражение PowerShell, которое объединяет ввода hello hello предыдущих двух действий.  Только одно из этих действий будет выполнено, так что результатом станет только один набор выходных файлов.  **Start-AzureVM** может использовать его как входные параметры.

### <a name="startstop-virtual-machines"></a>Запуск и остановка виртуальных машин
![Запуск виртуальных машин](media/automation-solution-startstopvm/graphical-startvm.png) ![Остановка виртуальных машин](media/automation-solution-startstopvm/graphical-stopvm.png)

В зависимости от hello runbook hello последующих действий, попробуйте toostart или остановить hello runbook с помощью **Start-AzureVM** или **Stop-AzureVM**.  Поскольку действие hello предшествует связи с конвейером, то запускается один раз для каждого объекта, возвращенные **слияния виртуальные машины**.  Hello ссылка является условной что hello действие будет выполняться только в том случае, если hello *RunningState* hello виртуальной машины — *остановлена* для **Start-AzureVM** и  *Запущен* для **Stop-AzureVM**. Если это условие не выполняется, затем **уведомления уже запущен** или **уведомления уже остановлен** работает toosend сообщения с помощью **Write-Output**.

### <a name="send-output"></a>Передача выходных данных
![Сообщение о запуске ВМ](media/automation-solution-startstopvm/graphical-notifystart.png) ![Сообщение об остановке ВМ](media/automation-solution-startstopvm/graphical-notifystop.png)

Заключительным шагом Hello hello runbook является выходной toosend ли hello Пуск или запроса на остановку для каждой виртуальной машины успешно отправлен. Отдельного **Write-Output** действия для каждой из них, и мы можем определить, какие один toorun с условными связями.  Действие **Notify VM Started** (Сообщить о запуске виртуальной машины) или **Notify VM Stopped** (Сообщить об остановке виртуальной машины) выполняется, если параметр *OperationStatus* (Состояние операции) имеет значение *Succeeded* (Успешно).  Если *OperationStatus* задано любое другое значение, затем **не удалось уведомить tooStart** или **tooStop не удалось уведомить** выполняется.

## <a name="next-steps"></a>Дальнейшие действия
* [Графическая разработка в службе автоматизации Azure](automation-graphical-authoring-intro.md)
* [Дочерние модули Runbook в службе автоматизации Azure](automation-child-runbooks.md)
* [Выходные данные и сообщения Runbook в службе автоматизации Azure](automation-runbook-output-and-messages.md)
