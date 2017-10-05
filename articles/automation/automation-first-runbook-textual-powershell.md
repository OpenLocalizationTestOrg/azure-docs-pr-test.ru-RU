---
title: "Мой первый модуль Runbook PowerShell в службе автоматизации Azure | Документация Майкрософт"
description: "Учебник, в котором описывается создание, тестирование и публикация простого модуля Runbook PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "Azure PowerShell, руководство по скриптам PowerShell, инструменты автоматизации PowerShell"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;sngun
ms.openlocfilehash: 4b32011b72acc647d4af44bb5ccbcaab408fb4d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="my-first-powershell-runbook"></a>Мой первый модуль Runbook PowerShell

> [!div class="op_single_selector"]
> * [Графический](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Рабочий процесс PowerShell](automation-first-runbook-textual.md)
> 
> 

В этом руководстве описана процедура создания [модуля Runbook PowerShell](automation-runbook-types.md#powershell-runbooks) в службе автоматизации Azure. Для начала мы протестируем и опубликуем простой модуль runbook и расскажем, как отслеживать состояние его заданий. Затем мы изменим модуль runbook, настроив его на фактическое управление ресурсами Azure (в нашем примере это запуск виртуальной машины Azure). И наконец, мы сделаем этот модуль runbook еще надежнее, добавив параметры.

## <a name="prerequisites"></a>Предварительные требования
Для работы с этим учебником требуется:

* Подписка Azure. Если у вас ее нет, [активируйте преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или <a href="/pricing/free-account/" target="_blank">[зарегистрируйте бесплатную учетную запись](https://azure.microsoft.com/free/).
* [Учетная запись службы автоматизации](automation-sec-configure-azure-runas-account.md) , чтобы хранить модуль Runbook и выполнять проверку подлинности ресурсов Azure.  Эта учетная запись должна иметь разрешение на запуск и остановку виртуальной машины.
* Виртуальная машина Azure. Это не должна быть рабочая виртуальная машина, так как в процессе изучения этого руководства ее нужно будет остановить и запустить заново.

## <a name="step-1---create-new-runbook"></a>Шаг 1. Создание нового модуля Runbook
Для начала мы создадим простой модуль Runbook, выводящий на экран текст *Привет, мир!*

1. На портале Azure выберите свою учетную запись службы автоматизации.  
   Страница учетной записи в службе автоматизации позволяет быстро получить представление о ресурсах, доступных в этой учетной записи. Некоторые ресурсы уже должны быть доступны. Большинство из них — это модули, которые добавляются в каждую новую учетную запись в службе автоматизации по умолчанию. Кроме того, вам потребуется ресурс учетных данных, упомянутый в [предварительных требованиях](#prerequisites).
2. Щелкните элемент **Модули Runbook** , чтобы открыть список модулей Runbook.<br><br> ![Управление модулями Runbook](media/automation-first-runbook-textual-powershell/runbooks-control-tiles.png)  
3. Создайте новый модуль runbook. Для этого нажмите кнопку **Добавить Runbook**, а затем выберите **Создать новый Runbook**.
4. Присвойте модулю Runbook имя *MyFirstRunbook-PowerShell*.
5. В данном случае мы создадим [модуль Runbook PowerShell](automation-runbook-types.md#powershell-runbooks), поэтому для параметра **Тип Runbook** выберите значение **Powershell**.<br><br> ![Runbook Type](media/automation-first-runbook-textual-powershell/automation-runbook-type.png)  
6. Щелкните **Создать** , чтобы создать модуль Runbook и открыть текстовый редактор.

## <a name="step-2---add-code-to-the-runbook"></a>Шаг 2. Добавление кода в Runbook
Можно либо напрямую ввести код в модуль Runbook, либо выбрать командлеты, модули Runbook и ресурсы из элемента управления "Библиотека" и добавить их к модулю Runbook с любыми связанными параметрами. В этом пошаговом руководстве мы введем код напрямую в модуль runbook.

1. Сейчас модуль Runbook пуст, поэтому введите *Write-Output "Hello World."*.<br><br> ![Привет, мир!](media/automation-first-runbook-textual-powershell/automation-helloworld.png)  
2. Сохраните модуль Runbook, щелкнув **Сохранить**.<br><br> ![Кнопка "Сохранить"](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-save.png)  

## <a name="step-3---test-the-runbook"></a>Шаг 3. Тестирование модуля Runbook
Прежде чем опубликовать модуль Runbook и, таким образом, сделать его доступным для рабочей среды, необходимо проверить, нормально ли он работает. Чтобы протестировать модуль Runbook, нужно запустить его **черновую** версию и проверить его работу в интерактивном режиме.

1. Щелкните **Область тестирования**.<br><br> ![Test Pane](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-test.png)  
2. Щелкните **Пуск** , чтобы начать тестирование. Активным должен быть только этот параметр.
3. При этом создается [задание Runbook](automation-runbook-execution.md) и отображается его состояние.  
   Сначала задание получает состояние *В очереди*, которое означает, что задание ожидает доступа к рабочей роли runbook в облаке. Как только рабочая роль затребует задание, оно получит состояние *Запущено*, а с началом фактического выполнения модуля Runbook — состояние *Выполняется*.  
4. Когда задание модуля Runbook будет выполнено, на экране появится результат. В нашем случае это должен быть текст *Привет, мир!*.<br><br> ![Вывод области тестирования](media/automation-first-runbook-textual-powershell/automation-testpane-output.png)  
5. Закройте область тестирования, чтобы вернуться на холст.

## <a name="step-4---publish-and-start-the-runbook"></a>Шаг 4. Публикация и запуск модуля Runbook
Модуль runbook, который мы только что создали, все еще находится в режиме черновика. Прежде чем запустить модуль в рабочей среде, его нужно опубликовать.  При публикации модуля Runbook существующая опубликованная версия перезаписывается черновой версией.  В нашем случае опубликованной версии не существует, поскольку Runbook был создан только что.

1. Щелкните **Опубликовать**, чтобы опубликовать модуль Runbook, а затем нажмите кнопку **Да** в появившемся запросе.<br><br> ![Кнопка "Опубликовать"](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-publish.png)  
2. Прокрутив экран влево до области **Модули Runbook**, вы увидите, что в поле **Состояние авторизации** для данного модуля Runbook появилось значение **Опубликован**.
3. Прокрутите экран вправо до области **MyFirstRunbook-PowerShell**.  
   Параметры в верхней части экрана позволяют запускать и просматривать модуль runbook, назначать его запуск в определенное время в будущем, а также создавать вызовы [webhook](automation-webhooks.md), чтобы запускать модуль с помощью HTTP-вызова.
4. Нам нужно запустить модуль runbook, поэтому щелкните **Запустить**, а затем, когда откроется колонка "Запуск Runbook", нажмите кнопку **ОК**.<br><br> ![Кнопка "Запуск"](media/automation-first-runbook-textual-powershell/automation-runbook-controls-start.png)<br>    
5. Откроется область заданий с созданным заданием runbook. Эту область можно закрыть, но сейчас оставим ее открытой, чтобы следить за ходом выполнения задания.
6. Состояние задания отображается в поле **Сводка по заданию** и отражает состояния, которые мы наблюдали при тестировании модуля Runbook.<br><br> ![Сводные данные задания](media/automation-first-runbook-textual-powershell/job-pane-status-blade-jobsummary.png)<br>  
7. Как только состояние модуля Runbook изменится на *Выполнено*, щелкните **Выходные данные**. Откроется область "Выходные данные" с текстом *Hello World*.<br><br> ![Выходные данные задания](media/automation-first-runbook-textual-powershell/job-pane-status-blade-outputtile.png)<br> 
8. Закройте область выходных данных.
9. Щелкните **Все журналы** , чтобы открыть область "Потоки" для задания Runbook. В потоке выходных данных должен отображаться только текст *Hello World* , но могут присутствовать и другие потоки заданий Runbook, например "Подробные сведения" и "Ошибка", если Runbook записывает в них какие-то данные.<br><br> ![Все журналы](media/automation-first-runbook-textual-powershell/job-pane-status-blade-alllogstile.png)<br>   
10. Закройте области "Потоки" и "Задания", чтобы вернуться в область MyFirstRunbook-PowerShell.
11. Щелкните **Задания** , чтобы открыть область "Задания" для этого Runbook. Откроется список всех заданий, созданных этим модулем Runbook. В нем должно быть только одно задание, так как мы запускали задание только один раз.<br><br> ![Список заданий](media/automation-first-runbook-textual-powershell/runbook-control-job-tile.png)  
12. Если щелкнуть это задание, откроется та же область заданий, которую мы видели при запуске модуля runbook. С ее помощью можно вернуться назад и просмотреть сведения о любом задании, созданном для конкретного модуля Runbook.

## <a name="step-5---add-authentication-to-manage-azure-resources"></a>Шаг 5. Добавление проверки подлинности для управления ресурсами Azure
Мы протестировали и опубликовали свой модуль Runbook, но пока он не выполняет никаких полезных действий. Нам нужно, чтобы он управлял ресурсами Azure. Runbook не сможет делать это, пока не пройдет проверку подлинности с использованием учетных данных, упомянутых в [предварительных требованиях](#prerequisites). Для этого используется командлет **Add-AzureRmAccount** .

1. Откройте текстовый редактор, щелкнув **Изменить** в области MyFirstRunbook-PowerShell.<br><br> ![Изменение модуля Runbook](media/automation-first-runbook-textual-powershell/automation-runbook-controls-edit.png)<br>   
2. Нам больше не потребуется использовать строку **Write-Output** , поэтому удалите ее.
3. Введите или скопируйте и вставьте следующий код, который выполнит проверку подлинности с помощью учетной записи запуска от имени службы автоматизации:
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
   <br>
4. Щелкните **область тестирования** , чтобы проверить модуль Runbook.
5. Щелкните **Пуск** , чтобы начать тестирование. После его завершения на экране должны отобразиться приблизительно такие основные сведения из вашей учетной записи. Это подтверждает допустимость учетных данных.<br><br> ![Проверка подлинности](media/automation-first-runbook-textual-powershell/runbook-auth-output.png)

## <a name="step-6---add-code-to-start-a-virtual-machine"></a>Шаг 6. Добавление кода запуска виртуальной машины
Теперь, когда модуль Runbook прошел проверку подлинности в нашей подписке Azure, можно управлять ресурсами. Мы добавим команду для запуска виртуальной машины. Вы можете выбрать любую виртуальную машину в своей подписке Azure. Имя этой машины будет прописано в модуле runbook.

1. После команды *Add-AzureRmAccount* введите команду *Start-AzureRmVM -Name 'имя_ВМ' -ResourceGroupName 'имя_группы_ресурсов'*, указав имя виртуальной машины, которую нужно запустить, и имя ее группы ресурсов.  
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   ```
   <br>
2. Сохраните модуль Runbook, после чего щелкните **область тестирования** для выполнения проверок.
3. Щелкните **Пуск** , чтобы начать тестирование. После завершения теста проверьте, запущена ли виртуальная машина.

## <a name="step-7---add-an-input-parameter-to-the-runbook"></a>Шаг 7. Добавление входного параметра в модуль Runbook
Созданный модуль runbook сейчас запускает виртуальную машину, указанную в коде модуля runbook, но лучше указать виртуальную машину при запуске runbook. Для этого добавим в модуль Runbook входные параметры.

1. Добавьте значения для параметров *VMName* (Имя ВМ) и *ResourceGroupName* (Имя группы ресурсов) в модуль Runbook и используйте эти переменные в командлете **Start-AzureRmVM**, как показано в примере ниже.  
   
   ```
   Param(
    [string]$VMName,
    [string]$ResourceGroupName
   )
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   ```
   <br>
2. Сохраните модуль Runbook и откройте область тестирования. Теперь можно указать значения двух входных переменных, которые будут использоваться в тесте.
3. Закройте область тестирования.
4. Щелкните **Опубликовать** , чтобы опубликовать новую версию модуля Runbook.
5. Остановите виртуальную машину, запущенную на предыдущем этапе.
6. Щелкните **Пуск** , чтобы запустить модуль Runbook. Введите значения **VMName** и **ResourceGroupName** для виртуальной машины, которую нужно запустить.<br><br> ![Передача параметра](media/automation-first-runbook-textual-powershell/automation-pass-params.png)<br>  
7. Когда модуль Runbook будет выполнен, проверьте, запустилась ли виртуальная машина.

## <a name="differences-from-powershell-workflow"></a>Отличия от рабочего процесса PowerShell
Модули runbook PowerShell имеют тот же жизненный цикл, возможности и средства управления, что и модули runbook рабочих процессов PowerShell, но существуют некоторые различия и ограничения.

1. Модули Runbook PowerShell выполняются быстрее (по сравнению с модулями Runbook рабочих процессов PowerShell), так как они не имеют этапа компиляции.
2. Модули Runbook PowerShell поддерживают контрольные точки, с помощью которых их выполнение можно возобновить с любого момента, тогда как модули Runbook рабочих процессов PowerShell можно возобновить только с начала.
3. Модули Runbook PowerShell поддерживают параллельное и последовательное выполнение, тогда как модули Runbook рабочих процессов PowerShell могут выполнять команды только последовательно.
4. В модуле runbook рабочего процесса PowerShell действие, команда или блок скрипта могут иметь свои собственные пространства выполнения, тогда как в модуле runbook PowerShell все содержимое скрипта выполняется в одном пространстве выполнения. Кроме того, существуют некоторые [синтаксические различия](https://technet.microsoft.com/magazine/dn151046.aspx) между собственным модулем Runbook PowerShell и модулем Runbook рабочих процессов PowerShell.

## <a name="next-steps"></a>Дальнейшие действия
* Чтобы начать работу с графическими модулями Runbook, см. инструкции в статье [Первый графический Runbook](automation-first-runbook-graphical.md).
* Чтобы приступить к работе с модулями Runbook рабочих процессов PowerShell, обратитесь к статье [Мой первый модуль Runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)
* Чтобы получить дополнительные сведения о типах модулей Runbook, их преимуществах и ограничениях, обратитесь к статье [Типы модулей Runbook в службе автоматизации Azure](automation-runbook-types.md)
* Дополнительные сведения о функции поддержки скриптов PowerShell см. в статье [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Встроенная поддержка скриптов PowerShell в службе автоматизации Azure).

