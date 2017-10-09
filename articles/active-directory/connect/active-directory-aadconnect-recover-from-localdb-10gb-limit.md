---
title: "Azure AD Connect: Как ограничить toorecover из 10 ГБ LocalDB проблема | Документы Microsoft"
description: "В этом разделе описывается, как toorecover синхронизация Azure AD Connect службы при обнаружении LocalDB 10 ГБ ограничить проблемы."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a>Azure AD Connect: Как toorecover из LocalDB 10 ГБ
Azure AD Connect требуется база данных SQL Server toostore удостоверений. Можно использовать значение по умолчанию hello установлен SQL Server 2012 Express LocalDB с Azure AD Connect или использовать полный SQL. SQL Server Express налагает ограничение в размере 10 ГБ. Если при использовании LocalDB достигнут этот предел, служба синхронизации Azure AD Connect больше не сможет запускаться или выполнять синхронизацию должным образом. Эта статья содержит инструкции по восстановлению hello.

## <a name="symptoms"></a>Симптомы
Существует два общих признака проблемы:

* Служба синхронизации подключения для Azure AD **выполняется** безуспешно toosynchronize с *«остановлено-базы данных диск full»* ошибки.

* Служба синхронизации подключения для Azure AD **— не удается toostart**. При попытке службы toostart hello, он завершается с события 6323 и сообщение об ошибке *«hello сервер обнаружил ошибку, так как SQL Server не хватает места на диске.»*

## <a name="short-term-recovery-steps"></a>Краткосрочные действия по восстановлению
Этот раздел содержит hello действия tooreclaim DB пространство, необходимое для операции tooresume служба синхронизации подключения для Azure AD. Hello шаги включают:
1. [Определить состояние службы синхронизации hello](#determine-the-synchronization-service-status)
2. [Сжатие базы данных hello](#shrink-the-database)
3. [Удалите данные журнала выполнения](#delete-run-history-data).
4. [Сократите срок хранения данных журнала выполнения](#shorten-retention-period-for-run-history-data).

### <a name="determine-hello-synchronization-service-status"></a>Определить состояние службы синхронизации hello
Сначала определите, по-прежнему выполняется ли служба синхронизации hello или нет:

1. Войдите в систему tooyour сервера Azure AD Connect как администратор.

2. Go слишком**диспетчера управления службами**.

3. Проверьте состояние hello **Microsoft Azure AD Sync**.


4. Если он выполняется, не остановить и перезапустить службу hello. Пропустить [жать базу данных hello](#shrink-the-database) шаг и перейти слишком[данные журнала выполнения Delete](#delete-run-history-data) шаг.

5. Если она не запущена, попробуйте toostart hello службы. Если hello служба была запущена успешно, пропустите [жать базу данных hello](#shrink-the-database) шаг и перейти слишком[данные журнала выполнения удаления](#delete-run-history-data) шаг. В противном случае продолжите [жать базу данных hello](#shrink-the-database) шаг.

### <a name="shrink-hello-database"></a>Сжатие базы данных hello
Используйте toofree операцию сжатия hello копирование достаточно hello toostart пространства БД службы синхронизации. Она освобождает место в базе данных, удаляя пробельные символы в базе данных hello. Этот наилучшее, но не всегда действующее решение. Эта статья toolearn Дополнительные сведения о операции сжатия [сжатие базы данных](https://msdn.microsoft.com/library/ms189035.aspx).

> [!IMPORTANT]
> Пропустите этот шаг, если вы можете получить toorun hello службы синхронизации. Не рекомендуется hello tooshrink баз данных SQL Server как может привести к появлению toopoor производительности из-за фрагментации tooincreased.

Название Hello hello базы данных, созданных для Azure AD Connect **ADSync**. tooperform операцию сжатия, необходимо войти как hello sysadmin или Владельцем базы данных hello. Во время установки Azure AD Connect hello следующие учетные записи предоставляются права системного администратора:
* локальные администраторы;
* Учетная запись пользователя Hello, установка используется toorun Azure AD Connect.
* Здравствуйте, учетной записи службы синхронизации, которая используется как hello операционной контексте службы подключения синхронизации Azure AD.
* Hello локальной группы ADSyncAdmins, который был создан во время установки.

1. Резервное копирование базы данных hello путем копирования **ADSync.mdf** и **ADSync_log.ldf** файлы, расположенные в группе `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa безопасном месте.

2. Запустите сеанс PowerShell.

3. Перейдите toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.

4. Запуск **sqlcmd** программы, выполнив команду hello `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, с помощью учетных данных hello роли sysadmin или hello базы данных DBO.

5. База данных hello tooshrink командной строки sqlcmd hello (1 >), введите `DBCC Shrinkdatabase(ADSync,1);`, за которым следует `GO` в следующую строку hello.

6. При успешном выполнении операции hello повторите toostart hello службы синхронизации. При запуске службы синхронизации hello go слишком[данные журнала выполнения Delete](#delete-run-history-data) шаг. В противном случае обратитесь в службу поддержки.

### <a name="delete-run-history-data"></a>Удаление данных журнала выполнения
По умолчанию Azure AD Connect сохраняет tooseven дней данных журнала выполнения. На этом шаге мы удалить hello пространство tooreclaim DB данных журнала выполнения, для возможности запуска попытку синхронизации службы синхронизации подключения для Azure AD.

1.  Запуск **диспетчер службы синхронизации** с переходом → tooSTART службы синхронизации.

2.  Go toohello **операции** вкладки.

3.  В разделе **Действия** выберите **Clear Runs** (Очистить выполнения).

4.  Можно выбрать параметр **Clear all runs** (Очистить все выполнения) или **Clear runs before…<date>** (Очистить выполнения до...). Рекомендуется начать с очистки тех данных журнала выполнения, которым больше двух дней. В случае продолжения toorun в проблема с размером базы данных выберите hello **очистить все фрагменты** параметр.

### <a name="shorten-retention-period-for-run-history-data"></a>Сокращение срока хранения данных журнала выполнения
Этот шаг является tooreduce hello вероятность того, что после нескольких циклов синхронизации выполняется в 10 ГБ проблема hello.

1. Запустите новый сеанс PowerShell.

2. Запустите `Get-ADSyncScheduler` и запомните hello PurgeRunHistoryInterval свойство, которое указывает текущий срок хранения hello.

3. Запустите `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` дней периода tootwo хранения tooset hello. Настройте срок хранения hello соответствующим образом.

## <a name="long-term-solution--migrate-toofull-sql"></a>Долгосрочное решение — toofull миграции SQL
Как правило, проблемы hello указывает, что размер 10 ГБ базы данных больше не достаточно для Azure AD Connect toosynchronize вашей локальной Active Directory tooAzure AD. Рекомендуется переключиться toousing hello полную версию SQL server. Нельзя напрямую заменить hello LocalDB существующего развертывания Azure AD Connect с базой данных hello hello полной версии SQL. Вместо этого необходимо развернуть новый сервер с hello полную версию SQL Azure AD Connect. Рекомендуется выполнить миграцию ходу где развертывании hello нового сервера Azure AD Connect (с баз данных SQL Server) в качестве промежуточного сервера Далее toohello существующего Azure AD Connect сервера (с LocalDB). 
* Инструкции по как tooconfigure удаленный SQL с Azure AD Connect см. tooarticle [выборочной установки из Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).
* Инструкции по ходу миграции для обновления Azure AD Connect, см. в разделе tooarticle [Azure AD Connect: обновление с предыдущей версии toohello последней](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
