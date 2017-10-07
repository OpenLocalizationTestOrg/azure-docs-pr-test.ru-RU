---
title: "Синхронизация Azure AD Connect: планировщик | Документация Майкрософт"
description: "В этом разделе описывается функция встроенного планировщика hello в Azure AD Connect sync."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a>Синхронизация Azure AD Connect: планировщик
В этом разделе описывается hello Планировщик синхронизации Azure AD Connect (так) (модуль синхронизации).

Эта функция появилась в сборке 1.1.105.0 (выпущенной в феврале 2016 года).

## <a name="overview"></a>Обзор
Служба синхронизации Azure AD Connect синхронизирует изменения в вашем локальном каталоге, используя планировщик. Планировщики выполняют два процесса — один для синхронизации паролей, другой для синхронизации объектов или атрибутов и задач технического обслуживания. В этом разделе рассматриваются последний hello.

В более ранних выпусках hello планировщика для объектов и атрибутов был toohello внешний модуль синхронизации. Он используется планировщик заданий Windows или отдельный процесс синхронизации tootrigger службы Windows hello. Планировщик Hello — с hello 1.1 подсистема синхронизации toohello Встроенные выпуски и позволяют выполнять некоторые настройки. Hello новой частоты синхронизации по умолчанию — 30 минут.

Планировщик Hello отвечает за две задачи:

* **Цикл синхронизации**. Hello tooimport процесс синхронизации изменения и экспорта.
* **Задачи обслуживания**. Обновление ключей и сертификатов для сброса паролей и службы регистрации устройств (DRS). Удалять старые записи в журнале операций hello.

Планировщик Hello сам всегда работает, но настроенных tooonly выполнить одно или ни один из этих задач может быть. Например если вам требуется toohave процесс цикла синхронизации, можно отключить этой задачи в планировщике hello, но по-прежнему выполнения hello задачи обслуживания.

## <a name="scheduler-configuration"></a>Конфигурация планировщика
toosee текущие настройки конфигурации перейдите tooPowerShell и запустите `Get-ADSyncScheduler`. Отобразятся данные примерно следующего вида:

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

Если вы видите **hello синхронизации команды или командлета недоступен** при выполнении этого командлета, затем hello PowerShell модуль не был загружен. Эта проблема может произойти, если запуск Azure AD Connect на контроллере домена или на сервере с более высоких уровнях PowerShell ограниченного использования программ, чем параметры по умолчанию hello. Если вы видите эту ошибку, запустите `Import-Module ADSync` toomake hello командлет доступно.

* **AllowedSyncCycleInterval**. Hello короткий интервал времени между циклами синхронизации, предоставляемые Azure AD. Более частная синхронизация не поддерживается.
* **CurrentlyEffectiveSyncCycleInterval**. Hello расписание в данный момент в силу. Он имеет hello совпадает со значением в CustomizedSyncInterval (если задать) Если это не чаще, чем AllowedSyncInterval. При использовании сборки до версии 1.1.281 изменения параметра CustomizedSyncCycleInterval вступают в силу после следующего цикла синхронизации. При сборке 1.1.281 hello изменение вступает в силу немедленно.
* **CustomizedSyncCycleInterval**. Если вы хотите toorun планировщика hello любой частотой, чем по умолчанию hello 30 минут, затем этот параметр. На приведенном выше рисунке hello, hello планировщика был задан toorun каждый час вместо него. Если значение этого параметра tooa ниже, чем AllowedSyncInterval, используется последнее hello.
* **NextSyncCyclePolicyType**. Изменение или исходное значение. Определяет, если следующий запуск hello следует только незначительные изменения процесса, либо если hello следующего запуска полной импорта и синхронизации. последний Hello также будет повторно обработать все новые или измененные правила.
* **NextSyncCycleStartTimeInUTC**. При очередном hello запускается диспетчер hello следующего цикла синхронизации.
* **PurgeRunHistoryInterval**. Здравствуйте, журналы должны храниться время операции. Эти журналы могут быть просмотрены hello диспетчер службы синхронизации. Здравствуйте, по умолчанию является tookeep эти журналы в течение 7 дней.
* **SyncCycleEnabled**. Указывает, планировщика hello работает ли hello импорта, синхронизации и процессов экспорта как часть своей работы.
* **MaintenanceEnabled**. Показывает, включен ли процесс обслуживания hello. Обновляет hello сертификаты и ключи и очищает hello журнала операций.
* **StagingModeEnabled**. Показано, включен ли [промежуточный режим](active-directory-aadconnectsync-operations.md#staging-mode) . Если этот параметр включен, затем он отключает экспортов hello запуск, но по-прежнему запускать импорта и синхронизации.
* **SchedulerSuspended**. Задается соединение во время обновления tootemporarily блок hello планировщика запуск.

Некоторые из этих параметров можно изменить с помощью `Set-ADSyncScheduler`. можно изменить Hello следующие параметры:

* CustomizedSyncCycleInterval
* NextSyncCyclePolicyType
* PurgeRunHistoryInterval
* SyncCycleEnabled
* MaintenanceEnabled

В предыдущих сборках Azure AD Connect параметр **isStagingModeEnabled** предоставлялся в командлете Set-ADSyncScheduler. Это **неподдерживаемый** tooset это свойство. Здравствуйте, свойство **SchedulerSuspended** может изменяться только для Connect. Это **неподдерживаемый** tooset с PowerShell непосредственно.

Настройка планировщика Hello хранится в Azure AD. Если у вас есть тестовый сервер, любые изменения на сервере-источнике hello также влияет на hello тестового сервера (за исключением IsStagingModeEnabled).

### <a name="customizedsynccycleinterval"></a>CustomizedSyncCycleInterval
Синтаксис: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`  
d — дни, HH — часы, mm — минуты, ss — секунды.

Пример: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`  
Изменения hello планировщика toorun каждые 3 часа.

Пример: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`  
Изменения toorun планировщика hello ежедневно.

### <a name="disable-hello-scheduler"></a>Отключить hello планировщика  
При необходимости изменения конфигурации toomake вы хотите toodisable hello планировщика. Например, если вы [настроить фильтрацию](active-directory-aadconnectsync-configure-filtering.md) или [внести изменения правил toosynchronization](active-directory-aadconnectsync-change-the-configuration.md).

Планировщик hello toodisable, запустите `Set-ADSyncScheduler -SyncCycleEnabled $false`.

![Отключить hello планировщика](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

После внесения изменений, не забудьте планировщика hello tooenable с `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="start-hello-scheduler"></a>Запустить планировщик hello
Планировщик Hello — по умолчанию выполняются каждые 30 минут. В некоторых случаях может потребоваться toorun цикл синхронизации между hello запланированных циклов или toorun другого типа, необходимо установить.

**Цикл синхронизации изменений**  
Цикл синхронизации дельта включает hello следующие шаги:

* Импорт изменений во всех соединителях
* Синхронизация изменений во всех соединителях
* Экспорт во всех соединителях

Это может быть наличие срочных изменение, которое должна быть синхронизирована немедленно, поэтому необходимо toomanually выполнения цикла. Если вам требуется toomanually выполнения цикла, затем от выполнения PowerShell `Start-ADSyncSyncCycle -PolicyType Delta`.

**Цикл полной синхронизации**  
Внесены следующие изменения конфигурации hello, необходимости toorun циклом полной синхронизации (так) Цикл полной (первоначальной) синхронизации необходимо выполнять, если в конфигурацию внесено одно из следующих изменений:

* Добавлены дополнительные объекты или атрибуты toobe, импортированных из исходного каталога
* Внесенные изменения правила синхронизации toohello
* Изменение [фильтрации](active-directory-aadconnectsync-configure-filtering.md) , в результате которого изменяется число включаемых объектов.

Если были внесены одно из этих изменений, должны toorun цикла полной синхронизации, модуль синхронизации hello имеет пространств соединителей hello tooreconsolidate возможности hello. Цикла полной синхронизации включает hello следующие шаги:

* Полный импорт во всех соединителях
* Полная синхронизация во всех соединителях
* Экспорт во всех соединителях

Запустите tooinitiate циклом полной синхронизации `Start-ADSyncSyncCycle -PolicyType Initial` из командной строки PowerShell. Эта команда запускает цикл полной синхронизации.

## <a name="stop-hello-scheduler"></a>Остановить планировщик hello
Если планировщик hello в настоящее время выполняется цикл синхронизации, то может потребоваться toostop его. Например, если запустить мастер установки hello и этой ошибки:

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

Пока выполняется цикл синхронизации, вносить изменения в конфигурацию нельзя. Может дождаться завершения процесса hello hello планировщика, но также можно остановить его, и немедленно внести изменения. Остановка текущего цикла hello не является опасной и ожидающих изменений обрабатываются с помощью следующего запуска.

1. Начало путем указания его текущего планировщика toostop hello цикла с помощью командлета PowerShell hello `Stop-ADSyncSyncCycle`.
2. Если использовать сборку до 1.1.281, то Остановка планировщика hello не останавливает hello текущий соединитель от его текущей задачи. tooforce Здравствуйте toostop соединитель, принимают hello, следующие действия: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)
   * Запуск **служба синхронизации** из меню "Пуск" hello. Go слишком**соединители**, выделите hello соединителя с состоянием hello **под управлением**и выберите **остановить** из hello действия.

Планировщик Hello еще активен и снова запускается на первой возможности.

## <a name="custom-scheduler"></a>Настраиваемый планировщик
Hello командлеты, описанные в этом разделе доступны только в сборке [1.1.130.0](active-directory-aadconnect-version-history.md#111300) и более поздних версий.

Если планировщик hello не удовлетворяет необходимым требованиям, можно запланировать hello соединителей, с помощью PowerShell.

### <a name="invoke-adsyncrunprofile"></a>Invoke-ADSyncRunProfile
Запустить профиль для соединителя можно таким образом:

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

Hello toouse имена для [именами соединителей](active-directory-aadconnectsync-service-manager-ui-connectors.md) и [запуска профиля имена](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) можно найти в hello [пользовательского интерфейса диспетчера службы синхронизации](active-directory-aadconnectsync-service-manager-ui.md).

![Вызов профиля выполнения](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

Hello `Invoke-ADSyncRunProfile` командлета является синхронным, то есть, он не возвращает управление до hello соединителя завершения операции hello успешно или с ошибкой.

При планировании соединителях hello рекомендуется tooschedule их в hello следующий порядок:

1. (полная/изменения) импорт из локальных каталогов, например Active Directory;
2. (полная/изменения) импорт из Azure AD;
3. (полная/изменения) синхронизация из локальных каталогов, например Active Directory;
4. (полная/изменения) синхронизация из Azure AD;
5. Экспорт tooAzure AD
6. Экспорт tooon локальные каталоги, например Active Directory.

Этот порядок является выполнением соединители hello hello встроенного планировщика.

### <a name="get-adsyncconnectorrunstatus"></a>Get-ADSyncConnectorRunStatus
Также можно отслеживать toosee механизм синхронизации hello, если это занятости и неактивности. Этот командлет возвращает пустой результат, если подсистема синхронизации hello находится в состоянии простоя, но не запущена соединителя. Если запущен соединитель, он возвращает имя hello hello соединителя.

```
Get-ADSyncConnectorRunStatus
```

![Состояние выполнения соединителя](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
На приведенном выше рисунке hello первая строка hello — из состояния, где модуль синхронизации hello бездействует. Вторая строка Hello из при выполнении hello соединителя Azure AD.

## <a name="scheduler-and-installation-wizard"></a>Планировщик и мастер установки
При запуске мастера установки hello hello планировщика временно приостанавливается. Эта функция действует так, как предполагается внести изменения в конфигурацию и не может применяться эти параметры, если активно запущен обработчик синхронизации hello. По этой причине не закрывайте приветствия мастера установки, так как он перестает подсистема синхронизации hello выполнять любые действия синхронизации.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello [синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) конфигурации.

Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
