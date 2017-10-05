---
title: "Запуск и остановка виртуальных машин: графические модули | Документация Майкрософт"
description: "Версия сценария службы автоматизации Azure с рабочим процессом PowerShell включает модули Runbook для запуска и остановки классических виртуальных машин."
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
redirect_document_id: FALSE
ms.openlocfilehash: 338d5712239356e13cbf480d9655ca3ca499701d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Сценарий для службы автоматизации Azure: запуск и остановка виртуальных машин
В этот сценарий для службы автоматизации Azure входят модули Runbook для запуска и остановки классических виртуальных машин.  С этим сценарием вы можете:  

* использовать модули Runbook без внесения изменений в свою рабочую среду;
* реализовать дополнительные функциональные возможности посредством изменения модулей Runbook;  
* вызывать модули Runbook из другого модуля Runbook в рамках общего решения;
* использовать модули Runbook в качестве учебников для ознакомления с основными концепциями создания таких модулей.

> [!div class="op_single_selector"]
> * [Графический](automation-solution-startstopvm-graphical.md)
> * [Рабочий процесс PowerShell](automation-solution-startstopvm-psworkflow.md)
>
>

Это версия сценария с графическим модулем Runbook. Доступно также решение с использованием [модулей Runbook рабочего процесса PowerShell](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-the-scenario"></a>Получение сценария
Этот сценарий состоит из двух графических модулей Runbook, которые можно скачать по следующим ссылкам.  Ссылки на модули Runnbook рабочего процесса PowerShell см. в [версии этого сценария для рабочих процессов PowerShell](automation-solution-startstopvm-psworkflow.md).

| Модуль Runbook | Ссылка | Тип | Описание |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Запуск графического модуля Runbook классической виртуальной машины Azure](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Графический |Запуск всех классических виртуальных машин в подписке Azure или всех виртуальных машин с определенным именем службы. |
| StopAzureClassicVM |[Остановка графического модуля Runbook классической виртуальной машины Azure](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Графический |Остановка всех классических виртуальных машин в учетной записи службы автоматизации или всех виртуальных машин с определенным именем службы. |

## <a name="installing-and-configuring-the-scenario"></a>Установка и настройка сценария
### <a name="1-install-the-runbooks"></a>1. Установка модулей Runbook
После загрузки модулей Runbook вы можете импортировать их с помощью процедуры, описанной в статье [Процедуры графических модулей Runbook](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-the-description-and-requirements"></a>2. Просмотр описания и требований
Модуль Runbook включает действие с именем **Read Me** , содержащее описание и необходимые ресурсы.  Чтобы просмотреть эти сведения, выберите действие **Read Me**, а затем параметр **Скрипт рабочего процесса**.  Аналогичную информацию можно получить из этой статьи.

### <a name="3-configure-assets"></a>3. Настройка ресурсов
Модулям Runbook требуются следующие ресурсы, которые необходимо создать и заполнить соответствующими значениями.  Имена присваиваются по умолчанию.  Чтобы использовать ресурсы с другими, при запуске модуля Runbook укажите эти имена во [входных параметрах](#using-the-runbooks) .

| Тип ресурса | Имя по умолчанию | Описание |
|:--- |:--- |:--- |:--- |
| [Учетные данные](automation-credentials.md) |AzureCredential |Содержит учетные данные для учетной записи, имеющей полномочия для запуска и остановки виртуальных машин в подписке Azure. |
| [Переменная](automation-variables.md) |AzureSubscriptionId |Содержит идентификатор вашей подписки Azure. |

## <a name="using-the-scenario"></a>Использование сценария
### <a name="parameters"></a>Параметры
Модули Runbooks имеют следующие [входные параметры](automation-starting-a-runbook.md#runbook-parameters).  Вам потребуется указать значения всех обязательных параметров и, при необходимости, указать значения дополнительных параметров.

| Параметр | Тип | Обязательно | Описание |
|:--- |:--- |:--- |:--- |
| ServiceName |string |Нет |Если значение указано, запускаются или останавливаются все виртуальные машины с таким именем службы.  Если значение не указано, запускаются или останавливаются все классические виртуальные машины в подписке Azure. |
| AzureSubscriptionIdAssetName |string |Нет |Содержит имя [ресурса переменной](#installing-and-configuring-the-scenario) , в котором указан идентификатор вашей подписки Azure.  Если значение не указано, используется значение *AzureSubscriptionId* . |
| AzureCredentialAssetName |string |Нет |Содержит имя [ресурса учетных данных](#installing-and-configuring-the-scenario) , в котором указаны учетные данные используемого модуля Runbook.  Если не указать это значение, будет использоваться значение *AzureCredential* . |

### <a name="starting-the-runbooks"></a>Запуск модулей Runbook
Для запуска упомянутых в этой статье модулей Runbook можно использовать любой из методов, описанных в статье [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md) .

Приведенные ниже команды использует Windows PowerShell для запуска модуля **StartAzureClassicVM** , который запускает все виртуальные машины с именем службы *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Выходные данные
При выполнении модулей выводятся [сообщения](automation-runbook-output-and-messages.md) для каждой виртуальной машины. Из них можно узнать о результатах инструкций запуска или остановки.  Чтобы определить результат выполнения каждого модуля Runbook, найдите в выходных данных соответствующую строку.  В следующей таблице перечислены возможные варианты выходных данных.

| Модуль Runbook | Условие | Сообщение |
|:--- |:--- |:--- |
| StartAzureClassicVM |Виртуальная машина уже запущена |MyVM is already running |
| StartAzureClassicVM |Запрос запуска виртуальной машины успешно отправлен |MyVM запущена |
| StartAzureClassicVM |Не удалось выполнить запрос запуска виртуальной машины |Не удалось запустить MyVM |
| StopAzureClassicVM |Виртуальная машина уже запущена |MyVM уже остановлена |
| StopAzureClassicVM |Запрос запуска виртуальной машины успешно отправлен |MyVM запущена |
| StopAzureClassicVM |Не удалось выполнить запрос запуска виртуальной машины |Не удалось запустить MyVM |

Ниже показано использование **StartAzureClassicVM** в качестве [дочернего модуля Runbook](automation-child-runbooks.md) в образце графического модуля Runbook.  При этом используются условное ссылки, приведенные в следующей таблице.

| Ссылка | Критерии |
|:--- |:--- |
| Рабочая ссылка |$ActivityOutput['StartAzureClassicVM'] -like "\* запущена" |
| Ошибочная ссылка |$ActivityOutput['StartAzureClassicVM'] -notlike "\* запущена" |

![Пример дочернего модуля Runbook](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Подробный разбор
Ниже приведен подробный разбор модулей Runbook из этого сценария.  Вы можете использовать эти сведения для настройки модулей Runbook или просто для их изучения с целью создания собственных сценариев автоматизации.

### <a name="authentication"></a>Аутентификация
![Аутентификация](media/automation-solution-startstopvm/graphical-authentication.png)

После запуска модуль Runbook выполняет действия, устанавливающие [учетные данные](automation-credentials.md) и подписку Azure, которые будут использоваться в остальной части модуля Runbook.

Первые два действия, **Get Subscription Id** (Получить идентификатор подписки) и **Get Azure Credential** (Получить учетные данные Azure), получают [ресурсы-контейнеры](#installing-the-runbook), которые используются следующими двумя действиями.  Эти действия могут определять ресурсы напрямую, но для этого им нужны имена ресурсов.  Поскольку мы позволяем пользователю указать эти имена во [входных параметрах](#using-the-runbooks), нужно сделать так, чтобы эти ресурсы извлекали ресурсы с именем, определенным входным параметром.

**Add-AzureAccount** определяет, какие учетные данные будут использоваться в остальной части модуля Runbook.  Ресурс учетных данных, извлекаемый из модуля **Get Azure Credential** (Получить учетные данные Azure), должен иметь доступ для запуска и остановки виртуальных машин в подписке Azure.  Используемая подписка выбирается действием **Select-AzureSubscription**, которое использует идентификатор подписки из действия **Get Subscription Id** (Получить идентификатор подписки).

### <a name="get-virtual-machines"></a>Получение виртуальных машин
![Получение виртуальных машин](media/automation-solution-startstopvm/graphical-getvms.png)

Модуль Runbook должен определить, с какими виртуальными машинами он будет работать, а также запущены они или остановлены (в зависимости от модуля Runbook).   Одно из двух действий извлечет виртуальные машины.  **Get VMs in Service** (Получить ВМ в службе) будет выполняться, если входной параметр *ServiceName* для модуля Runbook содержит значение.  **Get All VMs** (Получить ВМ в службе) будет выполняться, если входной параметр *ServiceName* для модуля Runbook не содержит значение.  Эта логика выполняется с помощью условных связей, предшествующих каждому действию.

Оба действия используют командлет **Get-AzureVM** .  Действие **Get All VMs** (Получить все виртуальные машины) использует набор параметров **ListAllVMs** для возврата всех виртуальных машин.  В действии **Get VMs in Service** (Получить виртуальные машины в службе) используется набор параметров **GetVMByServiceAndVMName** и предоставляется входной параметр **ServiceName** для параметра **ServiceName**.  

### <a name="merge-vms"></a>Объединение виртуальных машин
![Объединение виртуальных машин](media/automation-solution-startstopvm/graphical-mergevms.png)

Действие **Merge VMs** (Объединить виртуальные машины) должно обеспечивать входные данные для действия **Start-AzureVM**, для запуска которого требуются имена виртуальной машины (или машин) и службы.  Входные данные могут быть получены из действия **Get All VMs** (Получить все виртуальные машины) или **Get VMs in Service** (Получить виртуальные машины в службе), но **Start-AzureVM** позволяет указать в качестве входных данных только одно из этих действий.   

Сценарий заключается в создании действия **Merge VMs** (Объединить виртуальные машины), которое выполняет командлет **Write-Output**.  Параметром **InputObject** для этого командлета является выражение PowerShell, объединяющее выходные параметры двух предыдущих действий.  Только одно из этих действий будет выполнено, так что результатом станет только один набор выходных файлов.  **Start-AzureVM** может использовать его как входные параметры.

### <a name="startstop-virtual-machines"></a>Запуск и остановка виртуальных машин
![Запуск виртуальных машин](media/automation-solution-startstopvm/graphical-startvm.png) ![Остановка виртуальных машин](media/automation-solution-startstopvm/graphical-stopvm.png)

Дальнейшие действия попытаются запустить или остановить модуль Runbook с помощью командлета **Start-AzureVM** или **Stop-AzureVM** в зависимости от типа этого модуля.  Поскольку действию предшествует конвейерная связь, оно будет выполнено по одному разу для каждого объекта, полученного из метода **Merge VMs**(Объединить ВМ).  Эта связь условна, так что действие будет выполняться только в том случае, если параметр *RunningState* (Состояние выполнения) виртуальной машины имеет значение *Stopped* (Остановлена) для командлета **Start-AzureVM** или *Started* (Запущена) для командлета **Stop-AzureVM**. Если это условие не соблюдено, то выполняется действие **Notify Already Started** (Сообщить, что уже запущена) или **Notify Already Stopped** (Сообщить, что уже остановлена), отправляющее сообщение с помощью команды **Write-Output** (Записать выходные данные).

### <a name="send-output"></a>Передача выходных данных
![Сообщение о запуске ВМ](media/automation-solution-startstopvm/graphical-notifystart.png) ![Сообщение об остановке ВМ](media/automation-solution-startstopvm/graphical-notifystop.png)

Последний шаг в модуле — это передача выходных данных об успешности выполнения запроса о запуске или остановке каждой виртуальной машины. Для каждой машины создается отдельное действие **Write-Output** (Записать выходные данные) и определяется, какая из них будет запущена с условными связями.  Действие **Notify VM Started** (Сообщить о запуске виртуальной машины) или **Notify VM Stopped** (Сообщить об остановке виртуальной машины) выполняется, если параметр *OperationStatus* (Состояние операции) имеет значение *Succeeded* (Успешно).  Если параметр *OperationStatus* (Состояние операции) имеет другое значение, то выполняется действие **Notify Failed To Start** (Сообщить о сбое запуска) или **Notify Failed to Stop** (Сообщить о сбое остановки).

## <a name="next-steps"></a>Дальнейшие действия
* [Графическая разработка в службе автоматизации Azure](automation-graphical-authoring-intro.md)
* [Дочерние модули Runbook в службе автоматизации Azure](automation-child-runbooks.md)
* [Выходные данные и сообщения Runbook в службе автоматизации Azure](automation-runbook-output-and-messages.md)
