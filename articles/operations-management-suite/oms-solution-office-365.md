---
title: "aaaOffice 365 решения в Operations Management Suite (OMS) | Документы Microsoft"
description: "Эта статья содержит сведения по настройке и использовании hello Office 365 решения в OMS.  Он содержит подробное описание записи hello Office 365, созданных в службе анализа журналов."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: a1507745251ff015abb785bae8352fea7cea0734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-solution-in-operations-management-suite-oms"></a>Решение Office 365 в Operations Management Suite (OMS)

![Логотип Office 365](media/oms-solution-office-365/icon.png)

Hello решение Office 365 Operations Management Suite (OMS) позволяет toomonitor среде Office 365 в службе анализа журналов.  

- Мониторинг действий пользователей на использование шаблонов tooanalyze учетные записи Office 365, а также тенденциями изменения поведения. Например можно извлечь конкретных сценариев использования, такие как файлы, которые являются общими за пределами вашей организации или hello наиболее популярных сайтов SharePoint.
- Отслеживать изменения конфигурации tootrack действий администратора или операций с высоким уровнем привилегий.
- Выявлять и анализировать нежелательное поведение пользователей, которое можно настраивать, исходя из потребностей организации.
- Выполнять аудит и проверку соответствия. Например можно отслеживать операции доступа к файлу на конфиденциальные файлы, которые могут помочь с процессом hello соответствия и аудита.
- Оперативно устранять неполадки с помощью поиска OMS на основе данных о действиях Office 365 в вашей организации.

## <a name="prerequisites"></a>Предварительные требования
Hello Приведем решения требуется предыдущих toothis ли установлены и настроены.

- Подписка Office 365 организации.
- Учетные данные для учетной записи пользователя с правами глобального администратора.
- данные аудита tooreceive, сначала необходимо [настройки аудита](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&rs=en-US&ad=US#PickTab=Before_you_begin) в вашей подписке Office 365.  Обратите внимание, что [аудит почтовых ящиков](https://technet.microsoft.com/library/dn879651.aspx) настраивается отдельно.  По-прежнему можно установить решение hello и сбор других данных, если аудит не настроен.
 


## <a name="management-packs"></a>Пакеты управления
В этом решении не предусматривается установка пакетов управления в подключенных группах управления.
  

## <a name="configuration"></a>Конфигурация
После запуска [добавить подписку tooyour решения Office 365 hello](../log-analytics/log-analytics-add-solutions.md), у вас есть tooconnect его tooyour подписки Office 365.

1. Добавить tooyour решение управления оповещениями hello, рабочую область OMS hello процесс описывается в [добавить решения](../log-analytics/log-analytics-add-solutions.md).
2. Go слишком**параметры** на портале OMS hello.
3. В разделе **Подключенные источники** выберите **Office 365**.
4. Щелкните **Подключить Office 365**.<br>![Подключить Office 365](media/oms-solution-office-365/configure.png)
5. Войдите в tooOffice 365 под учетной записью, является глобальным администратором для вашей подписки. 
6. Hello подписки отображаются с hello рабочих нагрузок, которые будет отслеживать hello решения.<br>![Подключить Office 365](media/oms-solution-office-365/connected.png) 


## <a name="data-collection"></a>Сбор данных
### <a name="supported-agents"></a>Поддерживаемые агенты
Hello решение Office 365 не извлечения данных из любого hello [агенты OMS](../log-analytics/log-analytics-data-sources.md).  Оно извлекает данные непосредственно из Office 365.

### <a name="collection-frequency"></a>Частота сбора
Office 365 отправляет [веб-перехватчика уведомлений](https://msdn.microsoft.com/office-365/office-365-management-activity-api-reference#receiving-notifications) с tooLog подробные данные Analytics каждый раз создается запись.

## <a name="using-hello-solution"></a>С помощью решения hello
При добавлении рабочая область OMS tooyour решения Office 365 hello hello **Office 365** плитки будут добавлены tooyour мониторинга OMS. Эта Плитка отображается число и графическое представление hello количество компьютеров в вашей среде и их соответствие обновлений.<br><br>
![Элемент сводки Office 365](media/oms-solution-office-365/tile.png)  

Щелкните hello **Office 365** плитки приветствия tooopen **Office 365** панели мониторинга.

![Панель мониторинга Office 365](media/oms-solution-office-365/dashboard.png)  

панель мониторинга Hello, включает столбцы hello hello в следующей таблице. Каждый столбец список hello top десять предупреждений, сопоставляя число указан, критерий столбца hello области и временной диапазон. Можно выполнить поиск журнала, который предоставляет hello весь список, щелкнув см. в разделе все внизу hello hello столбца или, щелкнув заголовок столбца hello.

| столбец | Описание |
|:--|:--|
| Операции | Сведения о hello активных пользователей из всех отслеживаемых подписок Office 365. Можно также может toosee hello число действий, которые происходят во времени.
| Exchange | Показывает распределение hello действия Exchange Server, такие как Add-почтовому ящику или Set-Mailbox. |
| SharePoint | Показывает hello верхнего действия выполнять документов SharePoint. При выполнении детализации из этой плитки, страница поиска hello отображает подробные сведения hello этих действий, таких как hello целевого документа и расположение hello этого действия. Например, для события доступа к файлу, можно будет toosee hello документа, к которому имеет доступ, соответствующая учетная запись имени и IP-адрес. |
| Azure Active Directory | Включает в себя основные действия пользователей, такие как сброс пароля пользователя и попытка входа в систему. При выполнении детализации можно может toosee hello сведения из этих действий, как hello состояние результата. Это наиболее полезно, если вы хотите toomonitor подозрительных действий на Azure Active Directory. |




## <a name="log-analytics-records"></a>Записи Log Analytics

Все записи, созданные в рабочей области аналитики журналов hello решением Office 365 hello иметь **тип** из **OfficeActivity**.  Hello **OfficeWorkload** свойство определяет, какие записи Office 365 службы hello указывает слишком Exchange, azureactivedirectory возникла ошибка, SharePoint или OneDrive.  Hello **RecordType** свойство задает тип операции hello.  свойства Hello будут различаться для каждого типа операции и показано в приведенных ниже таблицах hello.

### <a name="common-properties"></a>Общие свойства
Привет, следующие свойства, распространенные записи tooall Office 365.

| Свойство | Описание |
|:--- |:--- |
| Тип | *OfficeActivity* |
| ClientIP | IP-адрес Hello hello устройство, которое было использовано, когда действие hello зафиксировано. Hello IP-адрес отображается в формате адреса IPv4 или IPv6. |
| OfficeWorkload | Служба Office 365, запись hello относится.<br><br>AzureActiveDirectory<br>Exchange<br>SharePoint|
| Операция | Имя Hello hello активность пользователя или администратора.  |
| OrganizationId | Hello GUID для клиента Office 365 организации. Это значение будет всегда быть hello одинаково для вашей организации, независимо от того, служба hello Office 365, в котором он выполняется. |
| RecordType | Тип выполняемой операции. |
| ResultStatus | Указывает, успешно ли действие hello (указанный в hello свойство операции). Возможные значения: Succeeded (Успешно), PartiallySucceded (Выполнено частично) и Failed (Сбой). Для действия администратора Exchange, hello значением является либо True или False. |
| UserId | Hello UPN (имя участника-пользователя) hello пользователя, выполнившего действие hello, которая привела к появлению hello записи; например my_name@my_domain_name. Обратите внимание, что сюда также включаются записи для действий, выполняемых системными учетными записями (такими как SHAREPOINT\system или NTAUTHORITY\SYSTEM). | 
| UserKey | Альтернативным Идентификатором для hello пользователю, указанному в hello свойства UserId.  Например это свойство заполняется с уникальным ИД hello паспорта (PUID) для события, выполняемые пользователями в SharePoint, OneDrive для бизнеса и Exchange. Это свойство также может указать hello совпадает со значением свойства UserID для события, происходящие в других службах и мероприятиях hello выполняемые системные учетные записи|
| UserType | Тип пользователя, выполнившего операцию hello Hello.<br><br>Администратор<br>Приложение<br>DcAdmin<br>Регулярное, <br>Reserved<br>ServicePrincipal<br>системный; |


### <a name="azure-active-directory-base"></a>Основа Azure Active Directory
Привет, следующие свойства являются общие записи tooall Azure Active Directory.

| Свойство | Описание |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AzureActiveDirectory_EventType | Тип Hello события Azure AD. |
| ExtendedProperties | Hello расширенные свойства события hello Azure AD. |


### <a name="azure-active-directory-account-logon"></a>Вход в учетную запись Azure Active Directory
Эти записи создаются при toolog попыток пользователя Active Directory.

| Свойство | Описание |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectoryAccountLogon |
| Приложение | приложение Hello, которое запускает событие входа учетной записи hello, такие как Office 15. |
| Клиент | Сведения о клиенте hello устройства, операционной системе устройства и браузер устройства, который был использован для hello hello учетной записи входа события. |
| LoginStatus | Это свойство получается непосредственно из параметра OrgIdLogon.LoginStatus. сопоставление Hello различных интересные ошибок входа в систему может выполнить системой предупреждений алгоритмы. |
| UserDomain | Hello сведения удостоверение клиента (TII). | 


### <a name="azure-active-directory"></a>Azure Active Directory
Эти записи создаются при внесении объектов Active Directory tooAzure изменения или дополнения.

| Свойство | Описание |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AADTarget | Hello пользователя, которое было выполнено действие hello (определяется hello свойство операции). |
| Субъект | Hello пользователя или участника-службы, выполнившего действие hello. |
| ActorContextId | принадлежит Hello GUID организации hello, hello субъекта. |
| ActorIpAddress | Здравствуйте, IP-адрес субъекта в формате адреса IPV4 или IPV6. |
| InterSystemsId | Здравствуйте, идентификатор GUID, который отслеживает действия hello между компонентами в службе hello Office 365. |
| IntraSystemId |   Здравствуйте, GUID, созданный действие hello tootrack Azure Active Directory. |
| SupportTicketId | Клиент Hello поддержка действие hello в ситуациях «act на behalf-of» ИД билета. |
| TargetContextId | Hello GUID организации hello, hello целевой пользователь принадлежит. |


### <a name="data-center-security"></a>Безопасность центра обработки данных
Эти записи создаются на основе данных аудита безопасности центра обработки данных.  

| Свойство | Описание |
|:--- |:--- |
| EffectiveOrganization | Имя Hello hello клиента, которому hello повышение прав или командлета, предназначены для. |
| ElevationApprovedTime | Hello отметка времени при повышение hello было утверждено. |
| ElevationApprover | Имя диспетчера Microsoft Hello. |
| ElevationDuration | Длительность Hello, для какой hello повышение был активен. |
| ElevationRequestId |  Уникальный идентификатор для запроса на повышение прав hello. |
| ElevationRole | Повышение hello роли Hello запрошен для. |
| ElevationTime | время повышения прав hello начала Hello. |
| Start_Time | время выполнения командлета hello начала Hello. |


### <a name="exchange-admin"></a>Администратор Exchange
Эти записи создаются при изменении конфигурации tooExchange.

| Свойство | Описание |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeAdmin |
| ExternalAccess |  Указывает, выполнялась ли командлет hello пользователем в вашей организации в центре обработки данных корпорации Майкрософт или учетной записи службы центра обработки данных, или полномочного администратора. Hello значение False указывает, что этот командлет hello был выполнен кем-то в вашей организации. Hello значение True указывает, что этот командлет hello был выполнен по персоналу центра обработки данных, учетной записи службы центра обработки данных или полномочного администратора. |
| ModifiedObjectResolvedName |  Это понятное имя пользователя hello hello объекта, который был изменен с помощью командлета hello. Данное событие регистрируется только в том случае, если hello изменяет hello объекта. |
| OrganizationName | Имя Hello hello клиента. |
| OriginatingServer | Имя сервера hello, из которого hello был выполнен командлет Hello. |
| Параметры | Hello имя и значение для всех параметров, которые использовались с командлетом hello, определяемое в hello свойство операций. |


### <a name="exchange-mailbox"></a>Почтовый ящик Exchange
Эти записи создаются при внесении почтовые ящики tooExchange изменения или дополнения.

| Свойство | Описание |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| ClientInfoString | Сведения о почтовом клиенте hello, операции используется tooperform hello, например, версия браузера, версия Outlook и сведения о мобильных устройствах. |
| Client_IPAddress | IP-адрес Hello hello устройства, который был использован при регистрации hello операции. Hello IP-адрес отображается в формате адреса IPv4 или IPv6. |
| ClientMachineName | Hello имя компьютера, на котором находится клиент Outlook hello. |
| ClientProcessName | Hello клиент электронной почты, который был почтового ящика используется tooaccess hello. |
| ClientVersion | версия клиента электронной почты hello Hello. |
| InternalLogonType | Зарезервировано для внутреннего использования. |
| Logon_Type | Указывает тип пользователя, доступ к hello почтового ящика и выполнить операцию hello, которое было записано hello. |
| LogonUserDisplayName |    Понятное имя Hello hello пользователя, выполнившего операцию hello. |
| LogonUserSid | Здравствуйте, SID hello пользователя, выполнившего операцию hello. |
| MailboxGuid | Hello Exchange GUID почтового ящика hello, которое было открыто. |
| MailboxOwnerMasterAccountSid | ИД безопасности главной учетной записи для учетной записи владельца почтового ящика. |
| MailboxOwnerSid | Здравствуйте, идентификатор безопасности владельца hello. |
| MailboxOwnerUPN | адрес электронной почты Hello hello лица, ответственного за hello почтовых ящиков, которое было открыто. |


### <a name="exchange-mailbox-audit"></a>Аудит почтового ящика Exchange
Эти записи создаются при создании записей аудита почтового ящика.

| Свойство | Описание |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| Элемент | Представляет элемент hello, после которого hello операции | 
| SendAsUserMailboxGuid | Hello GUID Exchange hello почтового ящика, который был доступ к электронной почте toosend от имени. |
| SendAsUserSmtp | SMTP-адрес пользователя hello, олицетворяется. |
| SendonBehalfOfUserMailboxGuid | Hello GUID Exchange hello почтового ящика, который был доступ к toosend почту от имени. |
| SendOnBehalfOfUserSmtp | SMTP-адрес hello пользователя, от лица которого hello электронной почты будет отправлено. |


### <a name="exchange-mailbox-audit-group"></a>Группа аудита почтового ящика Exchange
Эти записи создаются при внесении tooExchange группы изменения или дополнения.

| Свойство | Описание |
|:--- |:--- |
| OfficeWorkload | Exchange |
| OfficeWorkload | ExchangeItemGroup |
| AffectedItems | Сведения о каждом элементе в группе hello. |
| CrossMailboxOperations | Указывает, если операции hello используются более чем один почтовый ящик. |
| DestMailboxId | Установите только в том случае, если параметр CrossMailboxOperations hello имеет значение True. Указывает hello целевой GUID почтового ящика. |
| DestMailboxOwnerMasterAccountSid | Установите только в том случае, если параметр CrossMailboxOperations hello имеет значение True. Указывает hello SID для hello основной ИД безопасности учетной записи владельца целевой hello. |
| DestMailboxOwnerSid | Установите только в том случае, если параметр CrossMailboxOperations hello имеет значение True. Указывает hello SID hello целевой почтовый ящик. |
| DestMailboxOwnerUPN | Установите только в том случае, если параметр CrossMailboxOperations hello имеет значение True. Указывает имя участника-пользователя владельца hello hello целевой hello. |
| DestFolder | Hello конечной папки для операций, таких как Move. |
| Папка | Hello каталог, содержащий группу элементов. |
| Папки |     Сведения о папках источника hello, задействованные в операции; Например, если выбраны папки и затем удаляется. |


### <a name="sharepoint-base"></a>Основа SharePoint
Эти свойства определяются общие записи tooall SharePoint.

| Свойство | Описание |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| EventSource | Указывает, что событие произошло в SharePoint. Возможные значения: SharePoint или ObjectModel. |
| ItemType | Тип Hello объекта, который был доступ к или изменен. В разделе таблица ItemType hello сведения о hello типов объектов. |
| MachineDomainInfo | Сведения об операциях синхронизации устройств. Эта информация передается только в том случае, если он присутствует в запросе hello. |
| MachineId |   Сведения об операциях синхронизации устройств. Эта информация передается только в том случае, если он присутствует в запросе hello. |
| Site_ | Здравствуйте, GUID hello сайта, где находится hello файла или папки, пользователь hello. |
| Source_Name | Hello объекта, запустившего hello аудите операции. Возможные значения: SharePoint или ObjectModel. |
| UserAgent | Сведения о клиенте или в браузере пользователя hello. Эти сведения предоставляются hello клиент или браузер. |


### <a name="sharepoint-schema"></a>Схема SharePoint
Эти записи создаются при внесении изменений конфигурации tooSharePoint.

| Свойство | Описание |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| CustomEvent | Необязательная строка для пользовательских событий. |
| Event_Data |  Необязательные полезные данные для пользовательских событий. |
| ModifiedProperties | Свойство Hello включается для события административного канала, например добавление пользователя в составе сайта или группы узлов коллекции администратора. Свойство Hello включает имя hello свойства hello, который был изменен (например, группа администраторов узла hello) hello, новое значение hello свойства (такие hello пользователя, добавленная в качестве администратора сайта), и изменения hello предыдущее значение hello объекта. |


### <a name="sharepoint-file-operations"></a>Операции с файлами SharePoint
Эти записи создаются в операциях toofile ответа в SharePoint.

| Свойство | Описание |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePointFileOperation |
| DestinationFileExtension | Hello расширение файла, в который копируется или перемещается. Это свойство отображается только для событий FileCopied и FileMoved. |
| DestinationFileName | Hello имя файла "hello", копируется или перемещается. Это свойство отображается только для событий FileCopied и FileMoved. |
| DestinationRelativeUrl | URL-адрес Hello hello целевой папке, где файл копируется или перемещается. сочетание Hello hello значения для параметров SiteURL DestinationRelativeURL и DestinationFileName hello то же, что значение hello hello ObjectID свойство, являющееся hello полное имя пути для файла hello, который был скопирован. Это свойство отображается только для событий FileCopied и FileMoved. |
| SharingType | Тип разрешения, которые были назначены toohello пользователя, который был предоставлен hello ресурсов для управления доступом Hello. Этот пользователь идентифицируется параметром UserSharedWith hello. |
| Site_Url | Hello URL-адрес сайта hello, где находится hello файла или папки, пользователь hello. |
| SourceFileExtension | Hello расширение файла hello, которое было открыто пользователем hello. Это свойство является пустым, если папка является hello объект, который был доступен. |
| SourceFileName |  Имя Hello hello файла или папки, пользователь hello. |
| SourceRelativeUrl | URL-адрес Hello hello папку, содержащую файл hello пользователь hello. сочетание Hello hello значения для параметров SiteURL SourceRelativeURL и Имя_файла_исходного_кода hello hello то же, что значение hello hello ObjectID свойство, являющееся hello полное имя пути для файла hello пользователь hello. |
| UserSharedWith |  Hello пользователь, который был предоставлен ресурса. |




## <a name="sample-log-searches"></a>Пример поисков журналов
Hello в следующей таблице предоставляет образец поиска журналов для обновления записей, собранные этого решения.

| Запрос | Описание |
| --- | --- |
|Количество всех hello операций по подписке Office 365 |`Type = OfficeActivity | measure count() by Operation` |
|Использование сайтов SharePoint|`Type=OfficeActivity OfficeWorkload=sharepoint | measure count() as Count by SiteUrl | sort Count asc`|
|Операции доступа к файлам по типу пользователя|`Type=OfficeActivity OfficeWorkload=sharepoint Operation=FileAccessed | measure count() by UserType`|
|Поиск по определенному ключевому слову|`Type=OfficeActivity OfficeWorkload=azureactivedirectory "MyTest"`|
|Мониторинг внешних действий в отношении Exchange|`Type=OfficeActivity OfficeWorkload=exchange ExternalAccess = true`|



## <a name="troubleshooting"></a>Устранение неполадок

Если решение Office 365 не собирает данные, как ожидалось, проверьте его состояние на портале OMS hello в **параметры** -> **подключенные источники** -> **Office 365** . Привет, в следующей таблице описываются каждого состояния.

| Состояние | Описание |
|:--|:--|
| Активна | активен Hello подписки Office 365 и hello рабочей нагрузки является рабочей областью OMS tooyour успешно выполнено подключение. |
| Ожидает | активен Hello подписки Office 365, но рабочей нагрузки hello еще не успешное подключение tooyour рабочей области OMS. Hello первом подключении подписки Office 365 hello всех рабочих нагрузок hello будет в это состояние до успешного подключения. Подождите 24 часа для всех tooActive tooswitch рабочих нагрузок hello. |
| Неактивно | Hello подписки Office 365 находится в неактивном состоянии. Дополнительные сведения смотрите на странице администрирования Office 365. После активации подписки Office 365, отмените его связь с вашей рабочей области OMS и связать его снова toostart получение данных. |



## <a name="next-steps"></a>Дальнейшие действия
* Использование поиска журналов в [анализа журналов](../log-analytics/log-analytics-log-searches.md) tooview подробные данные обновления.
* [Создание собственных панелей мониторинга](../log-analytics/log-analytics-dashboards.md) toodisplay избранных запросов поиска Office 365.
* [Создание оповещений](../log-analytics/log-analytics-alerts.md) toobe заранее уведомления о важных событиях Office 365.  
