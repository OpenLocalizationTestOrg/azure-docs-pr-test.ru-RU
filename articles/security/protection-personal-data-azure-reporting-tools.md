---
title: "aaaDocument защиты личных данных с помощью средства создания отчетов Azure | Документы Microsoft"
description: "как toouse Azure reporting services и технологии toohelp защитить конфиденциальность личных данных."
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a>Защита личных данных документа с помощью средств создания отчетов Azure

В этой статье обсуждается, как toouse Azure reporting services и технологии toohelp защиты конфиденциальности личных данных.

## <a name="scenario"></a>Сценарий

Компании больших прогулка по, рядом с офисом в Соединенных Штатах Америки hello, развернут расписаниям toooffer его операций в морская hello, Adriatic и Балтийский компании seas, а также Британские острова hello. toohelp эти действия, он получил несколько небольших строк прогулка по в Италии, Германии, Дания и hello Великобритания

Hello организация использует Microsoft Azure для обработки и хранения корпоративных данных. Сюда входят персональные данные, позволяющие установить личность, например имена, адреса, номера телефонов и данные кредитной карты в глобальной клиентской базе. Он также включает традиционные информацию о персонале, например адреса, номера телефонов, идентификационные номера налога и медицинские сведения о сотрудниках компании во всех расположениях. Строка Hello прогулка по также хранится большой базы данных вознаграждения и постоянных элементов программы, содержат персональные данные tootrack связи с клиентами, текущие и прошлые.

Сотрудники предприятий сети hello доступ из удаленных офисов и путешествий hello компании расположены по всему Здравствуй, мир! имеют доступ к ресурсам компании toosome.

## <a name="problem-statement"></a>Проблема

Hello компании должны защищать hello конфиденциальность личных данных сотрудников и клиентов через стратегию многоуровневый безопасности, которая использует Azure управления и безопасности функции tooimpose строго контролировать обработку tooand доступ к личным сведениям и должен быть может toodemonstrate его защитных мер toointernal и внешних аудиторов.

## <a name="company-goal"></a>Цель компании

Как часть его стратегии глубокой обороны безопасности он является tootrack цель компании вся обработка tooand доступ к персональным данным и убедитесь, что документация достаточно конфиденциальности защиты личных сведений и работе.

## <a name="solutions"></a>Решения

Microsoft Azure предоставляет комплексное наблюдения, ведения журнала и toohelp средства диагностики, отслеживать и записывать действия и события, связанные с функциями доступа и обработки личных данных, географические потока данных и данных toopersonal доступа сторонних разработчиков. Поскольку безопасность личных данных в облаке hello общей ответственности, Майкрософт также предоставляет пользователям:

- подробные сведения о собственной обработке данных клиентов;

- меры безопасности под управлением Майкрософт;

- необходимые расположения и способы отправки данных клиентов;

- подробности о рассмотрении Майкрософт сведений о конфиденциальности.

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) — это мультитенантный облачный каталог и служба управления удостоверениями Майкрософт. Hello входа в службы, а также возможности аудита предоставляются подробные входа и действия сведения об использовании приложения toohelp, отслеживать и обеспечить toocustomers права доступа и сотрудников персональные данные.

Существуют два типа отчетов об активности:

- Hello [действия отчеты и журналы аудита](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) предоставляют подробные записи системных действий и задач

- Hello [входа в систему отчетов и журнал действий](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) рассказывается о том, кто выполнил каждого действия, перечисленные в отчет об аудите hello

Совместное использование двух hello, можно отслеживать журнал hello каждой задачей, выполняемой и кто выполнил каждого. Эти типы отчетов можно настраивать и фильтровать.

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a>Как открывать hello аудита и безопасности журналы?

Hello журналы аудита и безопасности может осуществляться из Active Directory портала hello тремя разными способами: через hello **действия** раздел (либо выберите **журналы аудита** или **входавсистему**), или из **пользователей и групп** или **корпоративных приложений** под **управление** в Active Directory. Отчеты можно получить через hello Azure Active Directory reporting API. 

1. В hello портал Azure, выберите **Azure Active Directory.**

2. В hello **действия** выберите **журналы аудита.**

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. Настроить представление списка hello, щелкнув **столбцы** инструментов hello.

4.  Выберите элемент в представление toosee hello список всех доступных сведений о нем.

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

Отчеты Azure Active Directory также включают два типа отчетов безопасности — **пользователи в группе риска** и **события входа, представляющие риск**. С помощью этих отчетов можно отследить потенциальные риски в среде Azure.

Дополнительные сведения о hello reporting service в разделе [отчетов Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)

Посетите [отчеты о действиях Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) более конкретные сведения о hello отчеты, доступные в Azure Active Directory. Этот сайт содержит дополнительные сведения о том, как tooaccess и использовать [журналы аудита, отчеты о действиях](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) и [действия при входе отчеты](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) hello портала. Вы можете также ознакомиться с отчетами безопасности о [пользователях в группе риска](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) и [событиях входа, представляющих риск](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins).

Посетите hello [аудита Azure Active Directory Справочник по API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) более подробные сведения о том, как tooconnect tooAzure каталог отчетов программным способом.

### <a name="log-analytics"></a>Служба Log Analytics

[Аналитика журналов](https://azure.microsoft.com/services/log-analytics/) можно [сбора данных из монитора Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate его с другими данными и обеспечивают дополнительный анализ. Azure Monitor собирает и анализирует данные мониторинга для вашей среды Azure. 

Средства анализа в Log Analytics, такие как поиск по журналам, представления и решения, обрабатывают все собранные данные, предоставляя централизованный анализ всей среды. Служба аналитики журналов можно объединять и анализировать журналы событий Windows, журналы IIS и сообщения, который может помочь в обнаружении потенциальных угроз личных данных, предоставляемых пользователям toounauthorized персональные данные.

#### <a name="how-do-i-use-log-analytics"></a>Как использовать Log Analytics?

Служба аналитики журналов доступны через портал OMS hello или hello портал Azure, из любого браузера. Служба аналитики журналов включает извлечь tooquickly языка запросов и консолидировать данные в репозиторий hello. Можно создать и сохранить toodirectly запросов поиска журналов анализа данных в портале hello.

toocreate рабочей области аналитики журналов в hello портал Azure hello следующие:

1. Выберите **анализа журналов** из списка hello служб в hello Marketplace.

2. Выберите **Create,** укажите имя рабочей области OMS hello, выберите вашей подписки, группы ресурсов, расположение и ценовой категории.

3. Нажмите кнопку **ОК** toodisplay список рабочих областей.

4. Выберите сведения о нем toosee рабочей области.

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

Посетите hello [документации для аналитика журналов](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn Дополнительные сведения о службе hello.

Посетите hello [приступить к работе с рабочей областью аналитики журналов](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) учебника toocreate рабочую область вычислений и узнайте, как toouse hello службы основы hello.

Посетите следующие веб-страниц более подробные сведения на способ использует toouse tooconnect анализа журналов с hello для входа hello описанные выше:

[Источники данных для журнала событий Windows в Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[Журналы IIS в службе Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[Источники данных системного журнала в Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a>Журнал действий Azure и Azure Monitor 

[Azure Monitor](https://azure.microsoft.com/services/monitor/) предоставляет метрики инфраструктуры базового уровня, а также журналы для большинства служб Microsoft Azure.
Отслеживание может помочь toogain полное представление о приложения Azure. Монитор Azure использует hello расширения службы диагностики Azure (Windows или Linux) для сбора большинство метрик уровня приложения и журналы. [Журнал действий Azure Hello](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) — один из ресурсов hello, можно просмотреть с помощью монитора Azure. Он отслеживает все вызовы API и предоставляет подробные сведения о действиях в [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).
Hello журнал действий (прежнее название — рабочее или журналы аудита) можно найти сведения о ресурсе в hello инфраструктуры Azure. 

Несмотря на то, что большая часть hello сведения записываются в действие hello журнала относится tooperformance и служба работоспособности, также сведения, связанные tooprotection данных. С помощью hello журнал действий, можно определить hello», кто и когда» для любой записи (PUT, POST, DELETE) на hello ресурсы в подписке Azure.

Например он содержит запись, когда администратор удаляет группу безопасности сети, что может повлиять на hello защиты личных данных. Записи журнала действий хранятся в Azure Monitor в течение 90 дней.

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a>Как использовать hello данные, собранные монитором Azure?

Существует ряд способов toouse hello данные в журнал действий hello и другим ресурсам Azure монитора.

- Можно осуществлять потоковую передачу hello расположения tooother данных в реальном строки.

- Данные можно хранить hello дольше времени от значений по умолчанию hello, с помощью [учетной записи хранилища Azure](https://docs.microsoft.com/azure/storage/common/storage-introduction) и задание политики хранения.

- Вы можете visual hello данных в графики и диаграммы, с помощью hello [портал Azure](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), или средства стороннего визуализации.

- Вы можете запрашивать данные hello, с помощью hello Azure REST API-Интерфейс монитора, команд CLI [PowerShell](https://docs.microsoft.com/powershell/) командлетов, или hello .NET SDK.

Выберите tooget работу с монитором Azure **более служб** в hello портал Azure.

1. Прокрутите список вниз слишком**монитор** в hello **наблюдения и управления** раздела.

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  Монитор открывается в hello **журнал действий** представления.

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

Можно создать и сохранить запросы для общие фильтры, а затем ПИН-кода hello наиболее важных запросов tooa панели мониторинга портала, поэтому вы всегда будете знать, если произошли события, которые соответствуют указанным критериям.

1. Вы можете фильтровать представление hello, группа ресурсов, timespan и категории событий.

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. Вы можете Закрепить панели мониторинга портала tooa запросы, щелкнув hello **ПИН-код** кнопки. Это поможет вам создать единый источник информации о рабочих данных в службах. Имя запроса Hello и количество результатов отображается на панели мониторинга hello.

Можно также использовать метрики tooview hello монитор для всех ресурсов Azure, настройки параметров диагностики и оповещений и найти в журнале hello. Дополнительные сведения о статье toouse hello Azure монитора и журнал действий [начать работу с монитором Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).

### <a name="azure-diagnostics"></a>Диагностика Azure 

функции диагностики Hello Azure включает сбор данных из нескольких источников. журналы событий Windows Hello, которые включают hello журнал безопасности, может быть особенно полезна при отслеживании и документирование защиты личных данных. журнал безопасности Hello отслеживает Успех и отказ событий входа в систему, а также изменения разрешений, обнаружения шаблонов, указывающее, определенные виды атак, изменения политики безопасности, изменения членства в группе безопасности и многое другое.

Например 4695 идентификатор события оповещения вы toohello попытка unprotection для защищенных данных. Это относится toohello API защиты данных (DPAPI), которая помогает tooprotect данные, такие как закрытые ключи, сохраненные учетные данные и другие конфиденциальные данные.

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a>Как включить расширение диагностики hello для виртуальных машин Windows?

PowerShell tooenable hello диагностического расширения для ВМ Windows, можно использовать так, чтобы данные журнала toocollect. Hello для таким образом определяется на какую модель развертывания используется (диспетчера ресурсов или Классическая версия). расширение диагностики tooenable hello в существующей виртуальной Машины, которая была создана с помощью модели развертывания диспетчера ресурсов hello, можно использовать hello [командлета PowerShell Set-AzureRMVMDiagnosticsExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

*\$diagnosticsconfig_path* hello путь toohello файл, содержащий конфигурацию диагностики hello в формате XML. Более подробные инструкции о включении диагностики Azure на виртуальной Машине см. в разделе [tooenable с помощью PowerShell диагностики Azure в виртуальной машине под управлением Windows.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)

Hello расширения службы диагностики Azure переносить учетной записи хранилища Azure hello собранных данных tooan и отправлять их tooservices, например Application Insights. Hello данные затем можно использовать для аудита.

#### <a name="how-do-i-store-and-view-diagnostic-data"></a>Как хранить и просматривать диагностические данные?

Это важные tooremember, диагностических данных не хранится постоянно, если не передать его toohello хранилища эмулятора или tooAzure службе хранилища Microsoft Azure. toostore и просмотр диагностических данных в хранилище Azure, выполните следующие действия.

1. Укажите учетную запись хранилища в файле ServiceConfiguration.cscfg hello. Система диагностики Azure можно использовать службы BLOB-объектов hello или hello службы таблиц, в зависимости от типа данных hello. Журналы событий Windows хранятся в формате таблицы.

2. Передача данных hello. Tootransfer hello диагностические данные можно запросить через файл конфигурации hello. Для пакета SDK 2.4 и предыдущим можно также выполнять запрос hello программными средствами.

3. Просмотр данных с помощью hello [обозреватель хранилищ Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer), [обозревателя серверов](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) в Visual Studio или [Azure Diagnostics Manager](https://www.cerebrata.com/products/azure-diagnostics-manager) в среде Management Studio Azure.

Дополнительные сведения о том, как tooperform каждого из этих шагов см [хранение и просмотр диагностических данных в хранилище Azure.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)

### <a name="azure-storage-analytics"></a>Аналитика службы хранилища Azure 

Аналитика хранилища заносит в журнал подробные сведения о службе хранилища tooa успешных и неудачных запросах. Эти сведения можно использовать toomonitor отдельные запросы, которые могут помочь в Документирование доступа к данным toopersonal хранятся в службе hello. Тем не менее ведение журнала решения "Аналитики Службы хранилища" по умолчанию для учетной записи хранения не предусмотрено. Его можно включить в hello портал Azure.

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a>Как настроить мониторинг учетной записи хранения?

Здравствуйте tooconfigure наблюдение за учетной записью хранения, следующие:

1. Выберите **учетные записи хранения** в hello портал Azure, затем выберите имя hello hello счета toomonitor.

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. В hello **мониторинг** выберите **диагностики.**

3.  Выберите hello **тип** данных метрик требуется toomonitor для каждой службы (больших двоичных объектов, таблиц, файл). журналы диагностики toosave tooinstruct хранилища Azure для чтения, записи и запросов на удаление для hello большого двоичного объекта, таблицы и очереди службы, выберите **больших двоичных объектов журналы, таблицы журналов** и **очередь журналов.**

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. С помощью ползунка hello внизу hello, установить hello **хранения** политики дней (значение 1 — 365). Семь дней — по умолчанию hello.

5. Выберите **Сохранить** параметры конфигурации tooapply hello.

Записи журнала хранилища содержат следующие сведения об отдельных запросах hello:

- Сведения о времени, например время запуска, совокупное время задержки и время задержки сервера.

- Сведения об операции хранения hello, такие как тип операции hello hello ключ клиента hello объекта хранилища hello имеет доступ к, успех или сбой и toohello клиента возвращается код состояния HTTP hello.

- Сведения о проверке подлинности, такие как hello типа проверки подлинности клиента hello.

- Сведения о параллелизме, например значение ETag hello и отметка времени последнего изменения.

- размеры Hello hello сообщения запроса и ответа.

Более подробные инструкции о том, как tooenable аналитики хранилища ведения журнала, в разделе [отслеживание учетной записи хранилища в hello портал Azure.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)

### <a name="azure-security-center"></a>Центр безопасности Azure 

[Центр безопасности Azure](https://azure.microsoft.com/services/security-center/) мониторы hello состояния безопасности ресурсам Azure в порядке tooprevent обнаружения угроз и содержатся рекомендации по отвечать на запросы. Он предоставляет несколько способов toohelp документа мер защиты, защищающих hello конфиденциальность личных данных.

Отслеживание работоспособности системы безопасности необходимо для обеспечения соответствия политикам безопасности. Мониторинг безопасности — стратегии упреждающего аудит систем tooidentify ресурсы, которые не соответствуют стандартам организации или рекомендации. Можно отслеживать состояние безопасности hello hello следующие ресурсы:

- вычислений (виртуальные машины и облачные службы);

- сетей (виртуальные сети);

- хранилища и данных (аудит базы данных и сервера и обнаружение угроз, прозрачное шифрование данных, шифрование хранилища);

- приложений (потенциальные проблемы безопасности).

Проблемы безопасности в любом из этих категорий может представлять угрозу конфиденциальность toohello персональные данные.

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a>Как просмотреть состояние безопасности hello Мои ресурсы Azure?

Центр обеспечения безопасности периодически анализирует состояние безопасности hello ресурсам Azure. Какие-либо потенциальной уязвимости, оно определяет, можно просмотреть в hello **Предотвращение** hello панели мониторинга.

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. В hello **Предотвращение** раздел, выберите hello **вычислений** плитки. Вы увидите здесь **Обзор,** вместе с hello **виртуальные машины** перечень всех виртуальных машин и их состояния безопасности и hello **облачные службы** список рабочих и веб-ролей ведет наблюдение за центра обеспечения безопасности.

2. На hello **Обзор** вкладки, вторую tooview рекомендация Дополнительные сведения.

3. На hello **виртуальные машины** выберите виртуальной Машины tooview дополнительных сведений.

При включении сбора данных в центр безопасности Azure hello Microsoft Monitoring Agent инициализируется автоматически на все существующие и новые любой поддерживаемый виртуальных машин, развернутых. Данные, собранные из этого агента, сохраняются в существующей рабочей области [Log Analytics](https://azure.microsoft.com/services/log-analytics/), связанной с подпиской Azure, или в новой рабочей области.

[Отчеты об исследовании угроз](https://docs.microsoft.com/azure/security-center/security-center-threat-report) предоставляет центр безопасности. Эти получения полезной информации, toohelp распознавания удостоверение, цели, текущие и прошлые атаки кампаний и тактики, инструменты и процедуры, используемые hello злоумышленника. В них также содержатся сведения по устранению рисков.

основной целью Hello эти отчеты угроз является toohelp toorespond вы эффективно toohello немедленно Предотвращение угроз и справки take впоследствии измеряет toomitigate hello проблему. Hello сведения в отчетах hello, также можно использовать при документировании к реагированию на события для создания отчетов и удобной организации аудита.

Отчеты аналитики угроз Hello представлены в. Формат PDF, доступ к ней через ссылку в hello **отчеты** поле hello **подозрительные процессу, выполняемому** колонку для каждого оповещения системы безопасности в центр безопасности Azure.

Дополнительные сведения о hello как tooview и использование отчетов аналитики угроз в разделе [отчет аналитики угроз центра безопасности Azure.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

## <a name="next-steps"></a>Дальнейшие действия

[Приступая к работе с API отчетов Azure Active Directory "hello"](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[Что такое Log Analytics?](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[Обзор мониторинга в Microsoft Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[Введение toohello журнал действий Azure (видео)](https://azure.microsoft.com/resources/videos/intro-activity-log/)
