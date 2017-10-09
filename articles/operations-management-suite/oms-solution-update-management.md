---
title: "aaaUpdate решение управления в OMS | Документы Microsoft"
description: "Эта статья является предполагаемым toohelp понять способ toouse это решение toomanage обновления для компьютеров Windows и Linux."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: e33ce6f9-d9b0-4a03-b94e-8ddedcc595d2
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 2dd321913bf049ab1996fd60a2f74b8417084dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-management-solution-in-oms"></a>Решение для управления обновлениями в OMS

![Символ управления обновлениями](./media/oms-solution-update-management/update-management-symbol.png)

Hello решение управления обновлениями в OMS позволяет toomanage обновления для системы безопасности операционной системы для компьютеров Windows и Linux, развернутых в Azure, локальной среды или других поставщиков облачных услуг.  Можно быстро оценить состояние hello доступных обновлений на всех компьютерах агента и управлять hello процесс установки необходимых обновлений для серверов.


## <a name="solution-overview"></a>Обзор решения
Компьютеры, управляемые OMS используйте hello ниже для выполнения развертывания и оценки обновления:

* агент OMS для Windows или Linux;
* служба настройки требуемого состояния PowerShell;
* гибридные рабочие роли Runbook службы автоматизации;
* службы центра обновления Майкрософт или Windows Server Update Services для компьютеров с Windows.

Hello следующие схемы показывает, что подключены концептуальное представление hello поведение и потоки данных с как решение hello оценивает и применяет tooall обновлений безопасности Windows Server и Linux компьютеров в рабочей области.    

#### <a name="windows-server"></a>Windows Server
![Процесс управления обновлением Windows Server](media/oms-solution-update-management/update-mgmt-windows-updateworkflow.png)

#### <a name="linux"></a>Linux
![Процесс управления обновлением Linux](media/oms-solution-update-management/update-mgmt-linux-updateworkflow.png)

После hello компьютер выполняет проверку на соответствие обновлений требованиям, hello агента OMS передает hello в tooOMS массового. На компьютере окно проверки соответствия hello выполняется каждые 12 часов по умолчанию.  В дополнение к этому расписанию проверки toohello hello проверки соответствия требованиям обновления инициируется в течение 15 минут, если tooupdate перезагрузки, предыдущие установки hello агента наблюдения Майкрософт (MMA), а после установки обновления.  Компьютер Linux будет выполнена проверка соответствия hello каждые 3 часа по умолчанию и проверки соответствия инициируется в течение 15 минут при перезапуске агента MMA hello.  

Hello сведения о соответствии затем обрабатываются и представленные на панелях мониторинга hello, включенных в решение hello или для поиска с помощью пользовательских или pre-определяемых запросов.  Hello решения сообщает порядок обновления hello зависит какие источника, настроенных toosynchronize с компьютера.  Если компьютер Windows hello настроенных tooreport tooWSUS, в зависимости от того, когда последняя синхронизация WSUS с центром обновления Майкрософт, hello результаты могут отличаться от показывает обновлений Майкрософт.  Hello одинаковыми для компьютеров Linux, настроить локальный репозиторий tooreport tooa сравнение открытого репозитория.   

Можно развернуть и установить обновления программного обеспечения на компьютерах, требующих обновления hello путем создания запланированного развертывания.  Обновления, которые классифицируются как *необязательно* не включаются в область hello развертывания для компьютеров Windows только обязательные обновления.  Hello запланированного развертывания определяет список целевых компьютеров получит hello применимых обновлений, либо явно указать компьютеров, или с помощью команды [группы компьютеров](../log-analytics/log-analytics-computer-groups.md) , на основе этих запросов поиска журналов для определенной группы на компьютерах.  Также укажите tooapprove расписание и указать период времени, если допускается toobe установлены в рамках обновления.  Обновления устанавливаются с помощью Runbook в службе автоматизации Azure.  Эти модули Runbook нельзя просмотреть, и они не требуют настройки.  При создании развертывания, обновления, он создает расписание начинается обновление главного модуля runbook при hello указанного времени для компьютеров, включенных hello.  Этот Runbook запускает для каждого агента дочерний Runbook, который выполняет установку необходимых обновлений.       

В hello дату и время, указанное в развертывании обновлений hello hello целевых компьютерах параллельно выполняет hello развертывания.  Проверки является первого обновления hello выполнено tooverify по-прежнему необходимы и устанавливает их.  Очень важно, что не удастся toonote для клиентских компьютеров WSUS, если обновления hello не утверждены в WSUS hello развертывания обновлений.  результаты Hello hello применения обновлений пересылаются toobe tooOMS обрабатываются и представленные на панелях мониторинга hello или поиске событий hello hello.     

## <a name="prerequisites"></a>Предварительные требования
* решение Hello поддерживает выполнение оценки обновления для Windows Server 2008 и более поздних версий и развертывания для Windows Server 2008 R2 SP1 и более поздних версий обновлений.  Параметры установки Server Core и Nano Server не поддерживаются.

    > [!NOTE]
    > Поддержка развертывания обновлений tooWindows Server 2008 R2 SP1 требуется .NET Framework 4.5 и WMF 5.0 или более поздней версии.
    >  
* Операционные системы клиента Windows не поддерживаются.  
* Агентов Windows должны быть toocommunicate, настроенных на сервере Windows Server Update Services (WSUS) или иметь доступ tooMicrosoft обновления.  

    > [!NOTE]
    > Агент Windows Hello не может управляться одновременно System Center Configuration Manager.  
    >
* CentOS 6 (x86 или x64) и 7 (x64)  
* Red Hat Enterprise 6 (x86 или x64) и 7 (x64)  
* SUSE Linux Enterprise Server 11 (x86 или x64) и 12 (x64)  
* Ubuntu 12.04 LTS и более поздняя версия x86 или x64   
    > [!NOTE]  
    > tooavoid обновления применяются только во время обслуживания в Ubuntu, перенастройте автоматическая установка обновления пакета toodisable автоматического обновления. Сведения о том, как tooconfigure, см. в разделе [автоматическое обновление раздела hello руководства Ubuntu Server](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).

* Агенты Linux, должны иметь доступ tooan обновления репозитория.  

    > [!NOTE]
    > Агент OMS для Linux настроить рабочих областей OMS toomultiple tooreport не поддерживается с этим решением.  
    >

Дополнительные сведения о предоставлении tooinstall hello агента OMS для Linux и загрузить последнюю версию hello ссылаться слишком[агент Operations Management Suite для Linux](https://github.com/microsoft/oms-agent-for-linux).  Сведения о том, как tooinstall hello Windows для агента OMS, просмотрите [Operations Management Suite агент для Windows](../log-analytics/log-analytics-windows-agents.md).  

### <a name="permissions"></a>Разрешения
В порядке toocreate развертыванием обновлений, необходимо toobe предоставлена роль участника hello в учетной записи службы автоматизации и рабочей областью аналитики журналов.  

## <a name="solution-components"></a>Компоненты решения
Это решение состоит из следующих ресурсов, которые добавляются в учетную запись автоматизации tooyour и непосредственно подключенные агенты или Operations Manager подключенной группы управления hello.

### <a name="management-packs"></a>Пакеты управления
Если группе управления System Center Operations Manager подключенной tooan рабочей области OMS, hello следующие пакеты управления в Operations Manager установлено.  После добавления этого решения пакеты управления также будут установлены на компьютерах с Windows, подключенных напрямую. Нет ничего tooconfigure или управляемые с помощью этих пакетов управления.

* Пакет аналитики оценки обновления Microsoft System Center Advisor (Microsoft.IntelligencePacks.UpdateAssessment);
* Microsoft.IntelligencePack.UpdateAssessment.Configuration (Microsoft.IntelligencePack.UpdateAssessment.Configuration);
* пакет управления развертыванием обновлений.

Дополнительные сведения об обновлении пакетов управления решения см. в разделе [tooLog подключение Operations Manager Analytics](../log-analytics/log-analytics-om-agents.md).

### <a name="hybrid-worker-groups"></a>Группы гибридных рабочих ролей
После включения этого решения любого компьютера Windows непосредственно подключенные tooyour рабочей области OMS автоматически настроена как модули hello toosupport гибридную рабочую роль Runbook, включенные в это решение.  Для каждого компьютера Windows, под управлением решения hello, оно будет указано в колонке гибридного Runbook рабочих групп hello hello учетной записи автоматизации следующее соглашение об именовании hello *Hostname FQDN_GUID*.  Вы не можете выбрать эти группы с помощью модулей Runbook в своей учетной записи, так как произойдет сбой. Эти группы предоставляют только нужные toosupport hello решение по управлению.   

Однако вы можете hello Windows компьютеров tooa гибридной рабочей ролью Runbook на добавить группу к toosupport учетной записи автоматизации Runbook автоматизации при условии, что вы используете учетную запись для решения hello и членство в группе гибридной рабочей ролью Runbook hello.  Эта функция будет добавлен tooversion 7.2.12024.0 из hello гибридной рабочей ролью Runbook.  

## <a name="configuration"></a>Конфигурация
Выполните следующие шаги tooadd hello управления обновлениями решения tooyour рабочей области OMS hello и убедитесь, что агенты отчетности. Рабочая область уже установлено tooyour агентов Windows будут автоматически добавлены без дополнительной настройки.

Вы можете развернуть решения hello, с помощью hello следующие методы:

* Из Azure Marketplace в hello портал Azure, выбрав hello элемента управления и автоматизации предложения или решение для управления обновлениями
* Из hello Коллекция решений OMS в рабочей области OMS

Если уже имеется учетная запись службы автоматизации и связанной рабочей области OMS в hello вместе одну группу ресурсов и региона, при выборе элемента управления и автоматизации будет проверить конфигурацию только установки hello решения и настроить его на обе службы.  Выбор решения управления обновлениями hello из Azure Marketplace обеспечивает hello такое же поведение.  Если у вас либо служб, развернутых в подписке, выполните действия hello в hello **Создание нового решения** колонки и подтверждения tooinstall hello других предварительно выбраны рекомендуемые решения.  При необходимости можно добавить решения tooyour hello управления обновлениями, рабочую область OMS hello шагов описанной в [решения OMS, добавьте](../log-analytics/log-analytics-add-solutions.md) из hello коллекции решений.  

### <a name="confirm-oms-agents-and-operations-manager-management-group-connected-toooms"></a>Подтвердите агенты OMS и tooOMS подключено групп управления Operations Manager

tooconfirm прямое подключение агента OMS для Linux и Windows, обмениваются данными с OMS, через несколько минут вы можете запустить hello, выполнив поиск журналов:

* Для Linux — `Type=Heartbeat OSType=Linux | top 500000 | dedup SourceComputerId | Sort Computer | display Table`.  

* Для Windows — `Type=Heartbeat OSType=Windows | top 500000 | dedup SourceComputerId | Sort Computer | display Table`.

На компьютере Windows вы можете просмотреть следующие tooverify соединение агента с OMS hello:

1.  Откройте Microsoft Monitoring Agent на панели управления, а также на hello **анализа журналов Azure (OMS)** вкладки, hello агента отображается сообщение, указывающее: **hello Microsoft Monitoring Agent успешно подключен toohello Microsoft Служба Operations Management Suite**.   
2.  Откройте журнал событий Windows hello, перейдите в каталог слишком**приложения и службы Logs\Operations** и выполните поиск 3000 идентификатор события и 5002 из источника соединитель служб.  Эти события указывают hello компьютер был зарегистрирован с рабочей областью OMS hello и получает конфигурации.  

Если агент hello не может toocommunicate с hello службой OMS и настроенный toocommunicate с hello Интернет через брандмауэр или прокси-сервер, подтвердите hello брандмауэра или прокси-сервер настроен правильно, просмотрев [сети Конфигурация для агента Windows](../log-analytics/log-analytics-windows-agents.md#network) или [конфигурацию сети для агента Linux](../log-analytics/log-analytics-agent-linux.md#network).

> [!NOTE]
> Если системы Linux, настроенные toocommunicate с прокси-сервер или шлюз OMS и адаптации этого решения, обновите hello *proxy.conf* разрешений toogrant hello omiuser группа разрешение на чтение для файла hello, выполнение hello, следующие команды:  
> `sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf`  
> `sudo chmod 644 /etc/opt/microsoft/omsagent/proxy.conf`


Добавленные агенты Linux отобразят статус **обновления** после оценки.  Этот процесс может занять too6 часов.

tooconfirm Operations Manager группы управления взаимодействует с OMS см [Проверка интеграции Operations Manager с OMS](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-oms).

## <a name="data-collection"></a>Сбор данных
### <a name="supported-agents"></a>Поддерживаемые агенты
Привет, в следующей таблице описываются hello подключенных источников, которые поддерживаются в этом решении.

| Подключенный источник | Поддерживаются | Описание |
| --- | --- | --- |
| Агенты Windows |Да |решение Hello собирает сведения о системных обновлений от агентов Windows и инициирует установки необходимых обновлений. |
| Агенты Linux |Да |решение Hello собирает сведения о системных обновлений из агенты Linux и начинает установку необходимых обновлений на поддерживаемые дистрибутивы. |
| Группа управления Operations Manager |Да |решение Hello собирает сведения о системных обновлений от агентов в подключенной группе управления.<br>Прямое подключение от tooLog агента Operations Manager hello Analytics не требуется. Данные будут отправлены из репозитория OMS toohello группы управления hello. |
| Учетная запись хранения Azure. |Нет |В хранилище Azure не хранятся сведения о системных обновлениях. |

### <a name="collection-frequency"></a>Частота сбора
Дважды в день выполняется проверка каждого управляемого компьютера Windows. Каждые 15 минут hello Windows API называется tooquery для hello последнего обновления времени toodetermine при изменении состояния, и в этом случае инициируется проверки соответствия.  Каждые три часа выполняется проверка всех управляемых компьютеров Linux.

Он может занять от 30 минут too6 часов для hello мониторинга toodisplay обновить данные с управляемых компьютеров.   

## <a name="using-hello-solution"></a>С помощью решения hello
При добавлении рабочая область OMS tooyour решения управления обновлениями hello hello **управления обновлениями** плитки будут добавлены tooyour мониторинга OMS. Эта Плитка отображается число и графическое представление hello количество компьютеров в вашей среде и их соответствие обновлений.<br><br>
![Плитка сводки "Управление обновлениями"](media/oms-solution-update-management/update-management-summary-tile.png)  


## <a name="viewing-update-assessments"></a>Просмотр оценки обновлений
Щелкните hello **управления обновлениями** плитки приветствия tooopen **управления обновлениями** панели мониторинга.<br><br> ![Панель мониторинга со сводкой "Управление обновлениями"](./media/oms-solution-update-management/update-management-dashboard.png)<br>

На этой панели мониторинга представлена подробная разбивка по состоянию обновлений, которая разделяется по типам операционной системы и классификации обновлений — важные, обновления безопасности и другие (например, обновления определения). Hello результаты каждой плитки на этой панели мониторинга отражают только обновления, утвержденные для развертывания, который основан на основе источника синхронизации компьютеров hello.   Hello **развертываний обновлений** плитки при выборе, вы будете перенаправлены toohello развертываний обновлений страницы, где можно просматривать расписания, развертываний, выполняющихся, завершенных развертываний или запланировать новое развертывание.  

Можно выполнить поиск журнала, который возвращает все записи, нажав кнопку в определенной плитке hello или toorun запроса определенной категории и предварительно определенные условия, выберите его из списка hello, доступных в группе hello **общие запросы на обновление** столбца.    

## <a name="installing-updates"></a>Установка обновлений
После обновления были оценки для всех hello Linux и компьютерах Windows в вашей рабочей области, вы могут установлены необходимые обновления путем создания *обновление развертывания*.  Развертывание обновлений — это запланированная установка требуемых обновлений для одного или нескольких компьютеров.  Следует указать hello даты и времени для развертывания hello Кроме tooa компьютера или группы компьютеров, которые должны быть включены в области развертывания hello.  toolearn Дополнительные сведения о группах компьютеров. в разделе [групп компьютеров в службе анализа журналов](../log-analytics/log-analytics-computer-groups.md).  При включении группы компьютеров в вашем развертывании обновления группы memnbership вычисляется только один раз во время hello создания расписания.  Группа tooa последующие изменения не отражаются.  toowork возникновения этой проблемы, удалите hello запланированное обновление развертывания и создайте его заново.

> [!NOTE]
> Windows виртуальных машин, развернутых из Azure Marketplace по умолчанию задаются tooreceive автоматического обновления из службы Центра обновления Windows hello.  Это поведение остается неизменным после добавления этого решения или рабочей tooyour виртуальные машины Windows.  В противном случае не активно управляемых обновлений с помощью этого решения hello поведение по умолчанию (автоматически применять обновления) применяются.  

Для виртуальных машин, созданных из hello по требованию Red Hat Enterprise Linux (RHEL) образов, доступных в Azure Marketplace, они являются hello зарегистрированных tooaccess [Red Hat обновления инфраструктуры (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md) развертывания в Azure.  Любой другой дистрибутив Linux должны обновляться из hello дистрибутивы файлов в сети репозитория после их поддерживаемых методов.  

### <a name="viewing-update-deployments"></a>Просмотр развертываний обновлений
Нажмите кнопку hello **развертывания обновлений** плитки tooview hello список существующих развертываний обновлений.  Они группируются по состоянию — **Запланировано**, **Выполняется** и **Завершено**.<br><br> ![Страница расписания развертываний обновлений](./media/oms-solution-update-management/update-updatedeployment-schedule-page.png)<br>  

в hello в следующей таблице описаны свойства Hello, отображаются для каждого развертывания обновлений.

| Свойство | Описание |
| --- | --- |
| Имя |Имя hello развертывания обновлений. |
| Расписание |Тип расписания.  Доступные параметры: *Один раз*, *Повторяется еженедельно*, *Повторяется ежемесячно*. |
| Время начала |Дата и время, которые hello развертывания обновлений — запланированных toostart. |
| Duration |Число минут hello развертывания обновлений может toorun.  Здравствуйте, все обновления не установлены в течение этого интервала времени, то hello оставшихся обновлений необходимо дождаться следующего развертывания обновлений. |
| Серверы |Количество компьютеров для развертывания обновлений hello.  |
| Состояние |Текущее состояние hello развертывания обновлений.<br><br>Возможные значения:<br>— "Не запущено";<br>- Выполнение<br>— "Готово". |

Выберите завершенного развертывания обновлений tooview hello экран сведений включает столбцы hello в hello в следующей таблице.  Эти столбцы будут быть заполнен, если не имеет hello развертывания обновлений еще не запущен.<br><br> ![Обзор результатов развертывания обновлений](./media/oms-solution-update-management/update-management-deploymentresults-dashboard.png)

| столбец | Описание |
| --- | --- |
| **Компьютеры** | |
| Компьютеры с Windows |Список hello количество компьютеров Windows в hello развертывания обновлений по состоянию.  Щелкните toorun состояние возврат с определенным состоянием для hello развертывания обновления все обновления записей поиска журнала. |
| Компьютеры с Linux |Список hello количество компьютеров Linux в hello развертывания обновлений по состоянию.  Щелкните toorun состояние возврат с определенным состоянием для hello развертывания обновления все обновления записей поиска журнала. |
| Состояние установки компьютера |Список hello компьютеров, участвующих в hello развертывания обновлений и процент hello обновлений, для которых было успешно установлено. Выберите одну из записей toorun hello поиска журналов, возвращая все отсутствующие и критические обновления. |
| **Обновления** | |
| Установка обновлений Windows |Список обновлений Windows, включенных в hello развертывания обновления и состоянием их установки на каждое обновление.  Выберите обновление toorun поиска журналов, возвращение все обновления записей для конкретного обновления, или щелкнуть toorun состояние hello возврат всех обновления записей для развертывания hello поиска журнала. |
| Обновления Linux |Список обновлений Linux, включенных в hello развертывания обновления и состоянием их установки на каждое обновление.  Выберите обновление toorun поиска журналов, возвращение все обновления записей для конкретного обновления, или щелкнуть toorun состояние hello возврат всех обновления записей для развертывания hello поиска журнала. |

### <a name="creating-an-update-deployment"></a>Создание развертывания обновлений
Создайте новое развертывание обновления, щелкнув hello **добавить** кнопку вверху hello hello tooopen экрана приветствия **новое развертывание обновления** страницы.  Необходимо указать значения для свойств hello в hello в следующей таблице.

| Свойство | Описание |
| --- | --- |
| Имя |Развертывание обновления hello tooidentify уникальное имя. |
| Часовой пояс |Toouse часовой пояс для времени начала hello. |
| Тип расписания | Тип расписания.  Доступные параметры: *Один раз*, *Повторяется еженедельно*, *Повторяется ежемесячно*.  
| Время начала |Дата и время toostart hello развертывания обновлений. **Примечание:** hello раньше всего развертывания можно запустить составляет 30 минут от текущего времени, если вам требуется toodeploy немедленно. |
| Duration |Число минут hello развертывания обновлений может toorun.  Здравствуйте, все обновления не установлены в течение этого интервала времени, то hello оставшихся обновлений необходимо дождаться следующего развертывания обновлений. |
| Компьютеры |Имена компьютеров или групп tooinclude компьютера и целевого объекта в hello развертывания обновлений.  Выберите одну или несколько записей из hello раскрывающегося списка. |

<br><br> ![Страница New Update Deployment (Новое развертывание обновлений)](./media/oms-solution-update-management/update-newupdaterun-page.png)

### <a name="time-range"></a>Диапазон времени
По умолчанию hello проанализирован в hello решение для управления обновлением данных hello относится от всех подключенных групп управления создается внутри hello 1 последний день.

Выберите диапазон времени hello toochange данных hello **данные на основе** hello верхней части панели мониторинга hello. Можно выбрать записи создан или обновлен в рамках hello последние 7 дней, 6 часов или 1 день. Или можно выбрать **Custom** (Пользовательский) и указать диапазон дат.

## <a name="log-analytics-records"></a>Записи Log Analytics
решение для управления обновлениями Hello создает два типа записей в репозиторий OMS hello.

### <a name="update-records"></a>Записи обновлений
Запись типа **Обновление** создается для каждого обновления, которое установлено или необходимо установить на каждом компьютере. Обновить записи имеют свойства hello в hello в следующей таблице.

| Свойство | Описание |
| --- | --- |
| Тип |*Обновление*. |
| SourceSystem |Источник Hello утвержденных установки обновления hello.<br>Возможные значения:<br>— Microsoft Update;<br>— Центр обновления Windows;<br>— SCCM;<br>— Linux Servers (серверы с Linux, данные которых получены из диспетчеров пакетов). |
| Approved |Указывает, является ли hello обновление было утверждено для установки.<br> Для серверов с Linux сейчас это необязательное свойство, так как OMS не осуществляет управление исправлениями. |
| Классификация для Windows |Классификация обновления hello.<br>Возможные значения:<br>— приложения;<br>— Critical Updates (Критические обновления);<br>— "Обновления определений";<br>— Feature Packs (Пакеты дополнительных компонентов);<br>— Security Updates (Обновления для системы безопасности);<br>— Service Packs (Пакеты обновления);<br>— Update Rollups (Накопительные пакеты обновления);<br>— "Обновления". |
| Классификация для Linux |Cassification обновления hello.<br>Возможные значения:<br>— Critical Updates (Критические обновления);<br>— Security Updates (Обновления для системы безопасности);<br>— Other Updates (Другие обновления). |
| Компьютер |Имя компьютера hello. |
| InstallTimeAvailable |Указывает время установки hello доступен из других ли агенты, которые установлены hello же обновления. |
| InstallTimePredictionSeconds |Примерное время установки в секундах, на основе других агенты, которые установлены hello того же обновления. |
| KBID |Идентификатор hello КБ статья с описанием обновления hello. |
| ManagementGroupName |Имя группы управления hello агентов SCOM.  Для других агентов это AOI-<workspace ID>. |
| MSRCBulletinID |Идентификатор бюллетеня по безопасности Microsoft hello описанием hello обновления. |
| MSRCSeverity |Серьезность hello бюллетене по безопасности.<br>Возможные значения:<br>— Critical;<br>— Important;<br>— Moderate. |
| Необязательно |Указывает, является ли обновление hello необязательно. |
| Продукт |Функция обновления продукта hello hello называется для.  Нажмите кнопку **представление** tooopen статье hello в браузере. |
| PackageSeverity |Серьезность Hello уязвимость hello, исправленные в этом обновлении, сообщаемых поставщиков дистрибутив Linux hello. |
| PublishDate |Дата и время hello обновления был установлен. |
| RebootBehavior |Указывает, если обновление hello принудительно перезагрузить компьютер.<br>Возможные значения:<br>— canrequestreboot;<br>— neverreboots. |
| RevisionNumber |Номер редакции hello обновления. |
| SourceComputerId |Идентификатор GUID toouniquely идентификации компьютера hello. |
| TimeGenerated |Дата и время hello записи последнего обновления. |
| Название |Название обновления hello. |
| UpdateID |Идентификатор GUID toouniquely идентификации hello обновления. |
| UpdateState |Указывает, установлено ли обновление hello на этом компьютере.<br>Возможные значения:<br>-Установить - hello обновление установлено на этом компьютере.<br>-Необходимо - hello обновления не установлен и – на этом компьютере. |

При выполнении любой поиск журнала, который возвращает записи с типом **обновление** можно выбрать hello **обновления** представления, отображающий набор плиток суммирования возвращенных hello поиска обновлений hello. Можно щелкнуть hello записей в hello **отсутствует и примененные обновления** и **обязательные и необязательные обновления** плитки tooscope представление hello toothat набор обновлений. Выберите hello **списка** или **таблицы** просмотра tooreturn hello отдельных записей.<br>

![Представление обновлений с поиском по журналам, где отображаются записи типа обновления](./media/oms-solution-update-management/update-la-view-updates.png)  

В hello **таблицы** представления, можно щелкнуть hello **KBID** для любой записи tooopen обозревателя со статьей hello КБ. Это позволяет tooquickly можно прочитать о деталях hello hello определенное обновление.<br>

![Представление таблицы с поиском по журналам, где отображаются плитки и записями типа обновления](./media/oms-solution-update-management/update-la-view-table.png)

В hello **списка** представление, щелкните hello **представление** ссылку Далее toohello KBID tooopen hello КБ статьи.<br>

![Представление списка с поиском по журналам, где отображаются плитки с записями типа обновления](./media/oms-solution-update-management/update-la-view-list.png)

### <a name="updatesummary-records"></a>Записи UpdateSummary
Запись типа **UpdateSummary** создается для каждого компьютера агента Windows. Эта запись обновляется каждый раз hello компьютере выполняется сканирование на наличие обновлений. **UpdateSummary** записи содержат свойства hello в hello в следующей таблице.

| Свойство | Описание |
| --- | --- |
| Тип |UpdateSummary |
| SourceSystem |OpsManager |
| Компьютер |Имя компьютера hello. |
| CriticalUpdatesMissing |Количество критических обновлений, отсутствует на компьютере hello. |
| ManagementGroupName |Имя группы управления hello агентов SCOM. Для других агентов это AOI-<workspace ID>. |
| NETRuntimeVersion |Версия среды выполнения .NET hello, установленных на компьютере hello. |
| OldestMissingSecurityUpdateBucket |Контейнер toocategorize hello время с момента публикации hello старые отсутствует обновление для системы безопасности на этом компьютере.<br>Возможные значения:<br>— Older;<br>— 180 дней назад;<br>— 150 days ago;<br>— 120 дней назад;<br>— 90 days ago;<br>— 60 days ago;<br>— 30 дней назад;<br>— недавно. |
| OldestMissingSecurityUpdateInDays |Число дней с момента публикации hello старые отсутствует обновление для системы безопасности на этом компьютере. |
| OsVersion |Версия hello операционной системы, установленной на компьютере hello. |
| OtherUpdatesMissing |Число другие обновления, отсутствующие на компьютере hello. |
| SecurityUpdatesMissing |Количество обновлений безопасности отсутствует на компьютере hello. |
| SourceComputerId |Идентификатор GUID toouniquely идентификации компьютера hello. |
| TimeGenerated |Дата и время hello записи последнего обновления. |
| TotalUpdatesMissing |Общее число обновлений, отсутствует на компьютере hello. |
| WindowsUpdateAgentVersion |Номер версии агента Центра обновления Windows hello на компьютере hello. |
| WindowsUpdateSetting |Значение параметра как hello на компьютере будет установлена важные обновления.<br>Возможные значения:<br>— Disabled;<br>— Notify before installation;<br>— Scheduled installation. |
| WSUSServer |URL-адрес служб WSUS Если компьютер hello серверы toouse один. |

## <a name="sample-log-searches"></a>Пример поисков журналов
Hello в следующей таблице предоставляет образец поиска журналов для обновления записей, собранные этого решения.

| Запрос | Описание |
| --- | --- |
| Type:Update OSType!=Linux UpdateState=Needed Optional=false Approved!=false &#124; measure count() by Computer |Компьютеры с сервером на основе Windows, которые необходимо обновить |
| Type:Update OSType=Linux UpdateState!="Not needed" &#124; measure count() by Computer |Серверы Linux, которые необходимо обновить | 
| Type=Update UpdateState=Needed Optional=false &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Все компьютеры с недостающими обновлениями |
| Type=Update UpdateState=Needed Optional=false Computer="COMPUTER01.contoso.com" &#124; select Computer,Title,KBID,Product,UpdateSeverity,PublishedDate |Отсутствующие обновления для определенного компьютера (замените значение именем своего компьютера)|
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") |Все компьютеры с недостающими критическими обновлениями или обновлениями для системы безопасности | 
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual &#124; Distinct Computer} &#124; Distinct KBID |Критические обновления или обновления для системы безопасности, необходимые компьютерам, на которых обновления применяются вручную |
| Type=Event EventLevelName=error Computer IN {Type=Update (Classification="Security Updates" OR Classification="Critical Updates") UpdateState=Needed Optional=false &#124; Distinct Computer} |События ошибок для компьютеров, на которых отсутствовали обязательные критические обновления или обновления для системы безопасности |
| Type=Update Optional=false Classification="Update Rollups" UpdateState=Needed &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Все компьютеры с недостающими накопительными пакетами обновления | 
| Type=Update UpdateState=Needed Optional=false &#124; Distinct Title |Отдельные недостающие обновления на всех компьютерах | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Title, UpdateRunName |Компьютер с сервером на основе Windows с обновлениями, завершившимися сбоем при выполнении | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Product, UpdateRunName |Сервер Linux с обновлениями, завершившимися сбоем при выполнении | 
| Type=UpdateSummary &#124; measure count() by WSUSServer |Членство компьютеров WSUS | 
| Type=UpdateSummary &#124; measure count() by WindowsUpdateSetting |Настройка автоматического обновления | 
| Type=UpdateSummary WindowsUpdateSetting=Manual |Компьютеры, на которых отключено автоматическое обновление | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" &#124; measure count() by Computer |Список всех машин Linux hello, имеющих доступно обновление пакета | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") &#124; measure count() by Computer |Список всех машин Linux hello, имеющих доступно обновление пакета, который устраняет уязвимость критическим или безопасности | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" |List of all packages that have an update available (Список всех пакетов, для которых доступно обновление) | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") |List of all packages that have an update available which addresses Critical or Security vulnerability (Список всех пакетов с доступными обновлениями, позволяющими устранить критическую уязвимость или уязвимость системы безопасности) | 
| Type:UpdateRunProgress &#124; measure Count() by UpdateRunName |Список измененных развертываний обновлений | 
| Type:UpdateRunProgress UpdateRunName="DeploymentName" &#124; measure Count() by Computer |Компьютеры, обновленные при этом запуске обновления (замените значение именем развертывания обновлений) | 
| Type=Update and OSType=Linux and OSName = Ubuntu &#124; measure count() by Computer |Список всех машин «Ubuntu» hello с доступно обновление | 

## <a name="troubleshooting"></a>Устранение неполадок

Этот раздел содержит сведения, toohelp неполадок, связанных с hello решения для управления обновлениями.  

### <a name="how-do-i-troubleshoot-onboarding-issues"></a>Как устранить проблемы подключения?
Если возникли проблемы при попытке tooonboard hello решения или виртуальной машины, проверьте hello **приложения и службы Logs\Operations** журнала событий для событий с событий 4502 идентификатор и событий сообщение, содержащее **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**.  Hello в следующей таблице выделены отдельные сообщения об ошибках и возможное решение для каждого.  

| Сообщение | Причина | Решение |   
|----------|----------|----------|  
| Не удается tooRegister машины для работы с исправлениями<br>Сбой регистрации с исключением<br>System.InvalidOperationException: {"Message":"Machine is already<br>зарегистрированные tooa отдельную учетную запись. "} ("Message": "Компьютер уже зарегистрирован для другой учетной записи") | Компьютер уже подключенным рабочей tooanother для управления обновлениями | Выполнить очистку старого артефактов, [удаление группы runbook гибридных hello](../automation/automation-hybrid-runbook-worker.md#remove-hybrid-worker-groups)|  
| Не удается слишком зарегистрировать компьютер для работы с исправлениями<br>Сбой регистрации с исключением<br>System.Net.Http.HttpRequestException: Произошла ошибка при отправке запроса hello. ---><br>System.Net.WebException: Базовое соединение hello<br>закрыто. Непредвиденная ошибка<br>при приеме. ---> System.ComponentModel.Win32Exception:<br>не удается связаться Hello клиента и сервера<br>т. к. у них разный алгоритм работы. | Связь блокируется прокси-сервером, шлюзом или брандмауэром | [Ознакомьтесь с требованиями к сети](../automation/automation-offering-get-started.md#network-planning)|  
| Не удается tooRegister машины для работы с исправлениями<br>Сбой регистрации с исключением<br>Newtonsoft.Json.JsonReaderException: ошибка при анализе положительного значения бесконечности. | Связь блокируется прокси-сервером, шлюзом или брандмауэром | [Ознакомьтесь с требованиями к сети](../automation/automation-offering-get-started.md#network-planning)| 
| Hello сертификата, предоставленного службой hello <wsid>. oms.opinsights.azure.com<br>не был выдан центром сертификации<br>для служб Майкрософт. Чтобы узнать,<br>toosee администратор вашей сети, если они работают под управлением прокси, который перехватывает<br>обратитесь к администратору сети. |Связь блокируется прокси-сервером, шлюзом или брандмауэром | [Ознакомьтесь с требованиями к сети](../automation/automation-offering-get-started.md#network-planning)|  
| Не удается tooRegister машины для работы с исправлениями<br>Сбой регистрации с исключением<br>AgentService.HybridRegistration.<br>PowerShell.Certificates.CertificateCreationException:<br>Не удалось выполнить toocreate самозаверяющий сертификат. ---><br>System.UnauthorizedAccessException: в доступе отказано. | Сбой создания самозаверяющего сертификата | У системной учетной записи должен быть<br>toofolder доступ для чтения:<br>**C:\ProgramData\Microsoft\**<br>**Crypto\RSA**|  

### <a name="how-do-i-troubleshoot-update-deployments"></a>Как устранить неполадки, связанные с развертыванием обновлений?
Можно просмотреть результаты hello hello runbook отвечать за развертывание hello обновления, включенные в hello запланированного развертывания из колонки заданий hello вашей учетной записи автоматизации, связанный с рабочей областью OMS hello, поддержка этого решения.  Здравствуйте, runbook **MicrosoftOMSComputer исправление** является дочерний модуль runbook, который обращается конкретный управляемый компьютер и просмотрев hello verbose Stream появятся подробные сведения для этого развертывания.  Вывод Hello будет отображения которой требуемые обновления применимы, загрузить состояние, состояние установки и Дополнительные сведения.<br><br> ![Состояние задания развертывания обновлений](media/oms-solution-update-management/update-la-patchrunbook-outputstream.png)<br>

Дополнительные сведения см. в статье [Выходные данные и сообщения Runbook в службе автоматизации Azure](../automation/automation-runbook-output-and-messages.md).   

## <a name="next-steps"></a>Дальнейшие действия
* Использование поиска журналов в [анализа журналов](../log-analytics/log-analytics-log-searches.md) tooview подробные данные обновления.
* [Создавайте свои панели мониторинга](../log-analytics/log-analytics-dashboards.md), где будут отображаться данные о соответствии обновлений для управляемых компьютеров.
* [Создавайте оповещения](../log-analytics/log-analytics-alerts.md) об обнаружении важных критических обновлений, отсутствующих на компьютерах, или отключении автоматических обновлений на компьютере.  
