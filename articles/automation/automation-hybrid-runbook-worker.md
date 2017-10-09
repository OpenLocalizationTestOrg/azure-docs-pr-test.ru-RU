---
title: "Гибридные рабочие роли Runbook автоматизации aaaAzure | Документы Microsoft"
description: "Это статье содержатся сведения об установке и использовании гибридной рабочей роли Runbook, который входит в состав службы автоматизации Azure, позволяющий toorun модулей Runbook на компьютерах в локальном центре обработки данных или поставщика облачных служб."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: ccee35e8324149a79ff692a867e5ce7801299bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resources-in-your-data-center-or-cloud-with-hybrid-runbook-worker"></a>Автоматизация ресурсов в центре обработки данных или облаке с помощью гибридной рабочей роли Runbook
Runbook в автоматизации Azure не может обращаться к ресурсам в других облаках, или в локальной среде, так как они выполняются в облаке Azure hello.  Hello гибридной рабочей ролью Runbook автоматизации Azure позволяет toorun runbooks непосредственно на компьютере hello с ролью hello и к ресурсам в среде toomanage hello этих локальных ресурсов. Модули Runbook хранятся и управляются в автоматизации Azure и затем доставляются tooone или более компьютеров, назначенный.  

Эта функциональность проиллюстрирован в hello после изображения:<br>  

![Обзор гибридного компонента Runbook Worker](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Технический обзор hello Runbook гибридной рабочей роли и вопросы развертывания см. в разделе [Обзор архитектуры автоматизации](automation-offering-get-started.md#automation-architecture-overview).    

## <a name="hybrid-runbook-worker-groups"></a>Группы гибридных компонентов Runbook Worker
Каждый гибридной рабочей ролью Runbook является членом группы гибридную рабочую роль Runbook, которая указывается при установке агента hello.  Группа может включать одного агента, но в нее можно установить несколько агентов для обеспечения высокого уровня доступности.

При запуске модуля runbook на гибридную рабочую роль Runbook необходимо указать группы hello, на котором работает.  Hello члены группы hello определяют, какой рабочий процесс служб hello запроса.  Указание конкретного компонента Worker для выполнения конкретной задачи не предусмотрено.

## <a name="relationship-tooservice-management-automation"></a>Связь tooService Management Automation
[Автоматизация управления службами (SMA)](https://technet.microsoft.com/library/dn469260.aspx) позволяет toorun hello же модулей Runbook, которые поддерживаются службой автоматизации Azure в вашем центре обработки локальных данных. Компонент SMA обычно развертывается вместе с Windows Azure Pack, так как Windows Azure Pack содержит графический интерфейс для управления SMA. В отличие от автоматизации Azure SMA требует локальной установки, включающий hello toohost серверы web API, в базе данных toocontain runbooks и SMA конфигурации и рабочих ролей Runbook tooexecute заданиях. Служба автоматизации Azure предоставляет аналогичные услуги в облаке hello и требуется только hello toomaintain гибридных рабочих ролей Runbook в локальной среде.

При наличии существующего пользователя SMA можно переместить ваш toobe автоматизации tooAzure модулей Runbook используется с гибридной рабочей ролью Runbook без изменений, при условии, что они выполняют свои собственные tooresources проверки подлинности, как описано в [запуска модулей Runbook в Runbook гибридных Рабочий](automation-hrw-run-runbooks.md).  Модули Runbook в SMA, выполняются в контексте учетной записи службы hello на hello рабочий сервер, который может предоставлять, проверку подлинности для модулей Runbook hello hello.

Можно использовать следующие критерии toodetermine ли более подходящий для требований к автоматизации Azure с гибридной рабочей ролью Runbook или Service Management Automation hello.

* SMA требуется локальная установка базовых компонентов, подключенных tooWindows Azure Pack, если требуется графический интерфейс. По сравнению со службой автоматизации Azure, для которой необходим только агент, установленный в локальных рабочих ролях Runbook, требуется больше локальных ресурсов и более высокие затраты на обслуживание. агенты Hello управляются Operations Management Suite дальнейшей уменьшение расходов на обслуживание.
* Служба автоматизации Azure хранит его модули Runbook в облаке hello и доставляет их tooon локальных гибридных рабочих ролей Runbook. Если ваша политика безопасности не допускает развертывания такой модели, тогда необходимо использовать SMA.
* Компонент SMA входит в состав System Center. Следовательно, для его использования требуется лицензия System Center 2012 R2. Служба автоматизации Azure основана на модели многоуровневой подписки.
* Служба автоматизации Azure обладает дополнительными функциями, такими как создание графических модулей Runbook, которые недоступны в SMA.

## <a name="installing-hello-windows-hybrid-runbook-worker"></a>Установка hello Windows гибридной рабочей роли Runbook 

tooinstall и настройка гибридной рабочей роли Runbook Windows, существует два способа.  Hello, рекомендуется использовать метод с помощью автоматизации runbook toocompletely автоматизировать процесс hello tooconfigure компьютера Windows.  Второй метод Hello следовать toomanually пошаговая процедура установки и настройте роль hello.  

> [!NOTE]
> конфигурации hello toomanage поддержки hello гибридной рабочей роли Runbook с требуемого состояния (DSC) серверов, необходимо tooadd их как узлы DSC.  Дополнительные сведения о развертывании этих узлов для управления с помощью DSC см. в статье [Подключение компьютеров для управления с помощью Azure Automation DSC](automation-dsc-onboarding.md).           
><br>
>При включении hello [решение для управления обновлениями](../operations-management-suite/oms-solution-update-management.md), tooyour рабочей области OMS автоматически настраивается как модули toosupport гибридную рабочую роль Runbook, включенные в это решение подключенных компьютерах под управлением Windows.  Но он не регистрируется в группах гибридных рабочих ролей, которые уже определены в вашей учетной записи службы автоматизации.  Hello компьютер можно добавить группу гибридных рабочих ролей Runbook tooa в ваш toosupport учетной записи автоматизации Runbook автоматизации при условии, что вы используете учетную запись для решения hello и членство в группе гибридной рабочей ролью Runbook hello.  Эта функция будет добавлен tooversion 7.2.12024.0 из hello гибридной рабочей ролью Runbook.  

Hello просмотрите следующие сведения, касающиеся hello [требования к оборудованию и программному обеспечению](automation-offering-get-started.md#hybrid-runbook-worker) и [сведения о подготовке сети](automation-offering-get-started.md#network-planning) перед началом развертывания гибридной рабочей роли Runbook.  После успешного развертывания runbook worker, просмотрите [запуска модулей Runbook на гибридную рабочую роль Runbook](automation-hrw-run-runbooks.md) toolearn tooconfigure tooautomate к модули Runbook обработка в центре обработки данных в локальной или другой облачной среде.  
 
### <a name="automated-deployment"></a>Автоматизированное развертывание

Hello следующих шагов tooautomate hello установки и настройки роли гибридной рабочей роли Windows hello.  

1. Загрузите hello *New OnPremiseHybridWorker.ps1* сценарий из hello [коллекции PowerShell](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/1.0/DisplayScript) непосредственно с компьютера hello hello гибридной рабочей роли Runbook или с другого компьютера в вашей среды и скопировать его toohello работника.  

    Hello *New OnPremiseHybridWorker.ps1* сценарий требует hello следующие параметры во время выполнения:

  * *AutomationAccountName* (обязательный) - hello имя вашей учетной записи автоматизации.  
  * *ResourceGroupName* (обязательный) - hello имя группы ресурсов hello, связанный с вашей учетной записи автоматизации.  
  * *HybridGroupName* (обязательный) - hello имени группы гибридную рабочую роль Runbook, укажите в качестве цели для поддержки этого сценария Runbook hello. 
  *  *SubscriptionID* (обязательный) - hello идентификатор подписки Azure, который используется для учетной записи автоматизации.
  *  *WorkspaceName* (необязательно) — hello OMS имя рабочей области.  Если у вас рабочей области OMS, hello скрипт создает и настраивает один.  

     > [!NOTE]
     > В настоящее время единственным автоматизации области hello поддерживается для интеграции с OMS — это - **Юго-Восточная Австралия**, **восточная часть США 2**, **Юго-Восточная Азия**, и **Западная Европа**.  Если ваша учетная запись автоматизации не в одном из этих областей, hello скрипт создает рабочую область OMS, но оно предупреждает, что его нельзя связать их друг с другом.
     > 
2. На компьютере, запустите **Windows PowerShell** из hello **запустить** экрана в режиме администратора.  
3. Hello оболочка командной строки PowerShell перейдите toohello папке, которая содержит скрипт hello загрузить и выполнить его изменение hello значения для параметров *- AutomationAccountName*, *- ResourceGroupName* , *- HybridGroupName*, *- SubscriptionId*, и *- WorkspaceName*.

     > [!NOTE] 
     > После выполнения сценария hello все запрашиваемые tooauthenticate с Azure.  Вы **должен** войти в учетную запись, которая является членом роли администраторов подписки hello и соадминистратором подписки hello.  
     >  
    
        .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> `
        -ResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
        -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfOMSWorkspace>

4. — Запрос tooagree tooinstall **NuGet** и имеют tooauthenticate запрашиваемые учетные данные Azure.<br><br> ![Выполнение сценария New-OnPremiseHybridWorker](media/automation-hybrid-runbook-worker/new-onpremisehybridworker-scriptoutput.png)

5. После завершения скрипта hello колонке hello гибридных рабочих групп будет отображаться новая группа hello и количество элементов или если существующую группу, увеличивается hello количество элементов.  Можно выбрать группу hello списке hello на hello **гибридных рабочих групп** колонки и select hello **гибридные рабочие роли** плитки.  На hello **гибридные рабочие роли** колонки, отображается каждый член группы hello в списке.  

### <a name="manual-deployment"></a>Развертывание вручную 
Один раз выполнить первые два шага hello для автоматизации среды, а затем повторите hello, оставшиеся шаги для каждого компьютера работника.

#### <a name="1-create-operations-management-suite-workspace"></a>1. Создайте рабочую область Operations Management Suite
Если у вас еще нет рабочей области Operations Management Suite, [создайте](../log-analytics/log-analytics-manage-access.md) ее. Если у вас уже есть рабочая область, вы можете использовать ее.

#### <a name="2-add-automation-solution-toooperations-management-suite-workspace"></a>2. Добавить решение автоматизации tooOperations рабочей области Management Suite
Решения расширяют функциональные возможности tooOperations Management Suite.  Hello решение автоматизации добавляет функциональные возможности для автоматизации Azure, включая поддержку гибридной рабочей ролью Runbook.  При добавлении рабочей tooyour hello решение автоматически помещает вниз компьютер агента toohello компоненты рабочего процесса, устанавливаемого в следующем шаге hello.

Следуйте инструкциям hello в [tooadd решения с использованием коллекции решений hello](../log-analytics/log-analytics-add-solutions.md) tooadd hello **автоматизации** рабочая область Operations Management Suite tooyour решения.

#### <a name="3-install-hello-microsoft-monitoring-agent"></a>3. Установка Microsoft Monitoring Agent hello
Microsoft Monitoring Agent Hello подключается компьютеров tooOperations Management Suite.  При установке агента hello на локальный компьютер и подключите его tooyour рабочей области, будут автоматически загружены hello компонентов, необходимых для гибридной рабочей ролью Runbook.

Следуйте инструкциям hello в [tooLog компьютеров Windows для подключения аналитики](../log-analytics/log-analytics-windows-agents.md) агента hello tooinstall hello на локальном компьютере.  Может повторить этот процесс для нескольких компьютеров tooadd среды tooyour несколько рабочих процессов.

Когда агент hello tooOperations Management Suite успешно подключен, он появится в списке на hello **подключенные источники** вкладка hello Operations Management Suite **параметры** панели.  Убедитесь, что агент hello правильно загрузила решение автоматизации hello после папку с именем **AzureAutomationFiles** в agent\agent C:\Program Files\Microsoft наблюдения.  версии hello tooconfirm hello гибридную рабочую роль Runbook, можно перейти hello tooC:\Program Files\Microsoft Agent\Agent\AzureAutomation\ мониторинг и обратите внимание, \\ *версии* вложенную папку.   

#### <a name="4-install-hello-runbook-environment-and-connect-tooazure-automation"></a>4. Установить среду runbook hello и подключить tooAzure автоматизации
При добавлении агента tooOperations Management Suite hello решение автоматизации поставляет hello **HybridRegistration** модуль PowerShell, который содержит hello **Add-HybridRunbookWorker** командлета.  Используйте этот командлет tooinstall hello runbook среды на компьютере hello и зарегистрируйте его в службе автоматизации Azure.

Откройте сеанс PowerShell с правами администратора и запустите следующие команды tooimport hello модуля hello.

    cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
    Import-Module HybridRegistration.psd1

Затем запустите hello **Add-HybridRunbookWorker** командлета с помощью hello, используя синтаксис:

    Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>

Можно получить hello сведения, необходимые для этого командлета из hello **управление ключами** колонки в hello портал Azure.  Откройте эту колонку, выбрав hello **ключей** параметр из hello **параметры** колонки в вашей учетной записи автоматизации.

![Обзор гибридного компонента Runbook Worker](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName** — имя hello hello группу гибридных рабочих ролей Runbook. Если эта группа уже существует в учетной записи автоматизации hello, hello текущего компьютера добавляется tooit.  Если она еще не существует, то выполняется ее добавление.
* **Конечная точка** — hello **URL-адрес** в hello **управление ключами** колонку.
* **Токен** — hello **первичный ключ доступа** в hello **управление ключами** колонку.  

Используйте hello **-Verbose** переключиться с **Add-HybridRunbookWorker** tooreceive подробные сведения об установке hello.

#### <a name="5-install-powershell-modules"></a>5. Установка модулей PowerShell
Модули Runbook можно использовать любой из действия hello и командлеты, определенные в модулях hello, установленных в среде автоматизации Azure.  Эти модули не будут автоматически развернутой tooon локальных компьютеров, поэтому его необходимо установить их вручную.  исключение Hello: hello модуль Azure, который устанавливается по умолчанию, предоставляя toocmdlets доступ для всех служб Azure и действий для автоматизации Azure.

Поскольку основной целью функции hello гибридной рабочей ролью Runbook hello toomanage локальных ресурсов, скорее всего, необходимо tooinstall hello модулей, которые поддерживают эти ресурсы.  Можно ссылаться слишком[Установка модулей](http://msdn.microsoft.com/library/dd878350.aspx) сведения об установке модули Windows PowerShell.  Установленных модулей должны находиться в расположении ссылается переменная среды PSModulePath, чтобы они автоматически импортируются hello гибридной рабочей роли.  Дополнительные сведения см. в разделе [hello изменение пути установки PSModulePath](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx). 

## <a name="removing-hybrid-runbook-worker"></a>Удаление гибридного компонента Runbook Worker 
Один или несколько Runbook гибридных рабочих ролей можно удалить из группы или удалении группы hello в зависимости от требований.  tooremove гибридную рабочую роль Runbook на локальном компьютере, выполните hello следующие шаги.

1. В hello портал Azure перейдите tooyour учетной записи автоматизации.  
2. Из hello **параметры** колонке выберите **ключей** и запишите hello значения для поля **URL-адрес** и **первичный ключ доступа**.  Эти сведения необходимы для следующего шага hello.
3. Откройте сеанс PowerShell с правами администратора и запустите следующую hello command - `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>`.  Используйте hello **-Verbose** перейти подробный журнал hello процесс удаления.

> [!NOTE]
> Это не удаляет hello Microsoft Monitoring Agent с компьютера hello, только функции hello и конфигурация роли hello гибридной рабочей ролью Runbook.  

## <a name="remove-hybrid-worker-groups"></a>Удаление групп гибридных рабочих ролей
tooremove группу, необходимо сначала tooremove hello гибридной рабочей роли Runbook с каждого компьютера, который является членом группы hello, с помощью приведенной выше процедуры hello и выполните следующие действия в группу tooremove hello hello.  

1. Откройте учетную запись автоматизации hello в hello портал Azure.
2. Выберите hello **гибридных рабочих групп** плитку и в hello **гибридных рабочих групп** колонку, вы хотите toodelete группы выберите hello.  После выбора конкретной группы hello, hello **группу гибридных рабочих ролей** свойства колонке отображается.<br> ![Колонка группы гибридных рабочих ролей Runbook](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
3. В колонке hello свойств для выбранной группы hello, нажмите кнопку **удалить**.  Появится сообщение, предлагающее tooconfirm вы это действие, выберите **Да** Если Вы действительно tooproceed.<br> ![Диалоговое окно подтверждения удаления группы](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> Этот процесс может занять несколько секунд toocomplete и можно отслеживать ход его выполнения в группе **уведомления** меню "hello".  

## <a name="troubleshooting"></a>Устранение неполадок 
Hello гибридной рабочей ролью Runbook зависит от hello toocommunicate Microsoft Monitoring Agent с вашей рабочей hello tooregister учетной записи автоматизации, получать заданий и отчет о состоянии. При сбое регистрации работника hello, Вот некоторые возможные причины ошибки hello.  

1. Гибридная рабочая роль Hello находится за прокси-сервера или брандмауэра.  
    Убедитесь, что компьютер hello имеет исходящий доступ too*.azure-automation.net через порт 443.  

2. Hello гибридной рабочей роли компьютера hello выполняется на меньше чем hello минимальные [требования](automation-offering-get-started.md#hybrid-runbook-worker).  
    Компьютеры под управлением hello гибридную рабочую роль Runbook, должен удовлетворять минимальным требованиям к оборудованию hello перед назначением его toohost эту функцию. В противном случае — в зависимости от использования ресурсов hello других фоновые процессы и конфликтах между модулями Runbook во время выполнения, hello компьютер становится более использованы будут и привести к задержкам задания runbook или истечение времени ожидания.
   Убедитесь, hello компьютеров, назначенных toorun hello гибридной рабочей ролью Runbook функция соответствует hello минимальным требованиям к оборудованию.  В этом случае отслеживать toodetermine использования ЦП и памяти корреляции между производительностью hello гибридного Runbook рабочих процессов и Windows.  Если объем памяти или нагрузка на ЦП, это может указывать tooupgrade необходимость hello или добавьте дополнительные процессоры или увеличение памяти tooaddress hello нехватки ресурсов и устранить ошибку hello. Можно также выберите ресурс различных вычислений, могут поддерживать минимальные требования hello и масштабирования, когда рабочих нагрузок указывают, что требуется увеличить.
    
3. Служба Microsoft Monitoring Agent Hello не выполняется.  
    Если служба Windows агента мониторинга Microsoft hello не выполняется, это предотвращает hello гибридной рабочей ролью Runbook связи в службе автоматизации Azure.  Проверьте, запущен агент hello, введя следующую команду в PowerShell hello: `get-service healthservice`.  Если hello служба остановлена, введите следующую команду в службе hello toostart PowerShell hello: `start-service healthservice`.  

4. В hello **приложения и службы Logs\Operations** журнал событий, появится событие 4502 и содержащий EventMessage **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**с hello после описания: *hello сертификата, предоставленного службой hello <wsid>. oms.opinsights.azure.com не был выдан центром сертификации, используемый для служб Microsoft. Обратитесь в службу toosee администратор вашей сети, если они работают под управлением прокси, который перехватывает связи протокол TLS/SSL. статья Hello KB3126513 имеет дополнительные диагностические сведения для проблем с подключением.*
    Это может быть вызвано вашего прокси-сервер или сетевой брандмауэр blockking связи tooMicrosoft Azure.  Убедитесь, что компьютер hello имеет исходящий доступ too*.azure-automation.net на портах 443.

Журналы сохраняются локально в каждом гибридном компоненте Worker по адресу C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Можно проверить, если есть любые предупреждения или ошибки события, записываемые toohello **приложения и службы Logs\Microsoft-SMA\Operations** и **приложения и службы Logs\Operations** , в журнале событий Указывает подключения или другие проблемы, которая затрагивает адаптации tooAzure роли hello автоматизации или проблемы во время выполнения обычных операций.  

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите [запуска модулей Runbook на гибридную рабочую роль Runbook](automation-hrw-run-runbooks.md) toolearn tooconfigure tooautomate к модули Runbook обработка в центре обработки данных в локальной или другой облачной среде.
