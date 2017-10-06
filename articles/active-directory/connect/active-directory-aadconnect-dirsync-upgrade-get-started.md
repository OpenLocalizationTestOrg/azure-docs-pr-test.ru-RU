---
title: "Azure AD Connect. Обновление службы DirSync | Документация Майкрософт"
description: "Узнайте, как tooupgrade из DirSync tooAzure AD Connect. Статьях описывается hello шаги обновления от DirSync tooAzure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: baf52da7-76a8-44c9-8e72-33245790001c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 05572af410698deaa1392c8837bfcb749efc69e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a>Azure AD Connect: обновление DirSync
Azure AD Connect — tooDirSync последователь hello. Можно найти способы hello в этом разделе можно обновить DirSync. Следующие действия не подходят для обновления другого выпуска Azure AD Connect или Azure AD Sync.

Прежде чем начать установку Azure AD Connect, убедитесь, что слишком[скачать Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) и завершения hello предварительные шаги в [Azure AD Connect: оборудование и компоненты](active-directory-aadconnect-prerequisites.md). В частности при необходимости tooread о hello следующую команду, так как эти области отличаются от DirSync:

* Hello требуемая версия .net и PowerShell. Новые версии становятся необходимые toobe сервера hello, чем требуется DirSync.
* Hello конфигурацию прокси-сервера. При использовании прокси-сервера сервера tooreach Здравствуйте Интернета, этот параметр должен быть настроен перед обновлением. DirSync всегда используется hello прокси-сервера, настроенного для пользователя hello, установив его, но использует Azure AD Connect параметры компьютера вместо него.
* требуется toobe Hello URL-адреса, откройте в hello прокси-сервера. Для основных сценариев, эти сценарии, также поддерживаются DirSync, hello требования — это же hello. Можно при необходимости toouse hello новых возможностей, включенных в Azure AD Connect, необходимо открыть некоторые новые URL-адреса.

> [!NOTE]
> После включения ваш новый Azure AD Connect server toostart синхронизации изменений tooAzure AD, вы должны не откат toousing DirSync или Azure AD Sync. Понижения версии с Azure AD Connect toolegacy клиентов, включая DirSync и Azure AD Sync не поддерживается и может привести tooissues, такие как потеря данных в Azure AD.

Если вам не нужно обновлять DirSync, см. другие сценарии в [документации](#related-documentation).

## <a name="upgrade-from-dirsync"></a>Обновление из DirSync
В зависимости от текущего развертывания DirSync имеются различные параметры для обновления hello. Если hello время обновления — меньше трех часов, затем hello рекомендуется toodo обновление на месте. Если hello ожидается обновления времени более трех часов, затем hello рекомендуется toodo параллельное развертывание на другом сервере. Предполагается, что при наличии более 50 000 объектов требуется более чем через три часа toodo hello обновления.

| Сценарий |
| --- | --- |
| [Обновление «на месте»](#in-place-upgrade) |
| [Параллельное развертывание](#parallel-deployment) |

> [!NOTE]
> При планировании tooupgrade из DirSync tooAzure AD Connect, не удаляйте DirSync самостоятельно перед обновлением hello. Azure AD Connect чтения и перенос hello конфигурации из DirSync и удалить после проверки сервера hello.

**Обновление «на месте»**  
Hello ожидается, что обновление hello toocomplete время отображается мастером hello. Оценка основана на предположении hello, что требуется три часа toocomplete обновления для базы данных с 50 000 объектов (пользователей, контактов и групп). Если hello число объектов в базе данных является менее 50 000, Azure AD Connect рекомендует обновление на месте. Если вы решите toocontinue, параметры автоматически применяются во время обновления и сервер автоматически возобновляется синхронизация active.

Если toodo миграции конфигурации а выполните параллельное развертывание, можно переопределить рекомендации по обновлению на месте hello. Например, может потребоваться toorefresh hello hello возможности оборудования и операционной системы. Дополнительные сведения см. в разделе hello [параллельное развертывание](#parallel-deployment) раздела.

**Параллельное развертывание**  
Параллельное развертывание рекомендуется использовать при наличии более 50 000 объектов. Это развертывание позволит избежать задержек в работе пользователей. Hello установки Azure AD Connect пытается tooestimate hello простоя для hello обновления, но при обновлении DirSync в прошлом hello собственных возможностей является наиболее руководства скорее всего toobe hello.

### <a name="supported-dirsync-configurations-toobe-upgraded"></a>Поддерживаемые конфигурации toobe DirSync, которые обновлены
После изменения конфигурации Hello поддерживаются с помощью обновленного DirSync:

* Фильтрация домена и подразделения
* Альтернативный идентификатор (UPN)
* Гибридные параметры синхронизации паролей и Exchange
* Параметры вашего леса или домена и Azure AD
* Фильтрация на основе атрибутов пользователя

не удается обновить Hello после изменения. При наличии этой конфигурации hello обновление заблокировано:

* Неподдерживаемые изменения DirSync, например удаленные атрибуты и использование пользовательского расширения DLL.

![Обновление заблокировано](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

В таких случаях hello рекомендуется tooinstall нового сервера Azure AD Connect [промежуточный режим](active-directory-aadconnectsync-operations.md#staging-mode) и проверьте hello DirSync старой и новой конфигурации Azure AD Connect. Повторно примените изменения с помощью пользовательской конфигурации, как описано в разделе [Пользовательская конфигурация службы синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md).

Hello пароли, используемые DirSync для учетных записей служб hello не удается получить и не переносятся. Эти пароли сбрасываются во время обновления hello.

### <a name="high-level-steps-for-upgrading-from-dirsync-tooazure-ad-connect"></a>Общие инструкции по обновлению из DirSync tooAzure AD Connect
1. Добро пожаловать tooAzure AD Connect
2. Анализ текущей конфигурации DirSync
3. Получение пароля глобального администратора Azure AD.
4. Сбор учетных данных для учетной записи администратора предприятия (используется только во время установки hello Azure AD Connect)
5. Установка Azure AD Connect
   * Удаление (или временное отключение) DirSync
   * Установка Azure AD Connect
   * Запуск синхронизации (при необходимости).

Дополнительные действия необходимы, если:

* в настоящее время вы используете полную версию SQL Server, локальную или удаленную;
* в области синхронизации более 50 000 объектов.

## <a name="in-place-upgrade"></a>Обновление «на месте»
1. Запуск hello Azure AD Connect установщика (MSI).
2. Читайте и принимайте условия toolicense и уведомление о конфиденциальности.  
   ![Вас приветствует tooAzure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. Нажмите кнопку Далее toobegin анализа существующей установки DirSync.  
   ![Анализ существующей установки службы синхронизации каталогов](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. После завершения анализа hello, вы видите hello рекомендации о том, как tooproceed.  
   * Если экспресс-выпуск SQL Server и иметь не более 50 000 объектов, отображается следующий экран приветствия:  
     ![Анализ завершен готов tooupgrade от DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * При использовании полной версии SQL Server для DirSync вы увидите такую страницу:  
     ![Анализ завершен готов tooupgrade от DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)  
     отображается Hello сведения, касающиеся hello существующей базы данных SQL server, используемого DirSync. При необходимости внесите соответствующие изменения. Нажмите кнопку **Далее** toocontinue hello установки.
   * При наличии более 50 000 объектов отобразится следующий экран:  
     ![Анализ завершен готов tooupgrade от DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)  
     следующее сообщение toothis hello флажок, нажмите кнопку tooproceed при обновлении на месте: **продолжить обновление DirSync на этом компьютере.**
     toodo [параллельное развертывание](#parallel-deployment) вместо этого экспортировать параметры конфигурации DirSync hello и переместить hello конфигурации toohello новый сервер.
5. Пароль учетной записи hello, используемой в настоящее время tooconnect tooAzure AD hello. Это должен быть hello учетной записи, используемой в настоящий момент DirSync.  
   ![Введите учетные данные Azure AD.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)  
   Если вы получаете сообщение об ошибке и испытываете проблемы с подключением, см. статью [Устранение неполадок подключения в Azure AD Connect](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Укажите учетную запись администратора предприятия для Active Directory.  
   ![Введите учетные данные ADDS.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. Теперь вы готовы tooconfigure. Нажмите кнопку **Обновить**, чтобы удалить DirSync и начать настройку и синхронизацию Azure AD Connect.  
   ![Все готово tooconfigure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)
8. После завершения установки hello, выйдите из системы и войдите снова tooWindows, прежде чем использовать диспетчер служб синхронизации, редактор правил синхронизации, или попробуйте toomake изменения конфигурации.

## <a name="parallel-deployment"></a>Параллельное развертывание
### <a name="export-hello-dirsync-configuration"></a>Экспорт конфигурации DirSync hello
**Параллельное развертывание — более 50 000 объектов**

Если вы более 50 000 объектов, затем hello установки Azure AD Connect рекомендует параллельное развертывание.

Экран аналогичные toohello систему отображается следующая информация:  
![Анализ завершен.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

Если вы хотите tooproceed с параллельное развертывание, необходимо hello tooperform следующие шаги:

* Нажмите кнопку hello **экспорт параметров** кнопки. При установке Azure AD Connect на отдельном сервере, эти параметры переносятся из текущей tooyour DirSync новой установки Azure AD Connect.

После настройки были успешно экспортированы, можно выйти из мастера hello Azure AD Connect на сервере DirSync hello. Продолжить выполнение следующего шага hello слишком[установить Azure AD Connect на отдельном сервере](#installation-of-azure-ad-connect-on-separate-server)

**Параллельное развертывание — менее 50 000 объектов**

Если использовать менее 50 000 объектов, но по-прежнему требуется toodo параллельное развертывание, затем hello следующие:

1. Запустите установщик hello Azure AD Connect (MSI).
2. При появлении hello **приветствия tooAzure AD Connect** экране мастера установки hello выход, щелкнув hello «X» в верхнем правом углу hello окна hello.
3. Откройте окно командной строки.
4. Hello установить расположение Azure AD Connect (по умолчанию: C:\Program Files\Microsoft Azure Active Directory Connect) выполните следующую команду hello: `AzureADConnect.exe /ForceExport`.
5. Нажмите кнопку hello **экспорт параметров** кнопки. При установке Azure AD Connect на отдельном сервере, эти параметры переносятся из текущей tooyour DirSync новой установки Azure AD Connect.

![Анализ завершен.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

После настройки были успешно экспортированы, можно выйти из мастера hello Azure AD Connect на сервере DirSync hello. Продолжить выполнение следующего шага hello слишком[установить Azure AD Connect на отдельном сервере](#installation-of-azure-ad-connect-on-separate-server).

### <a name="install-azure-ad-connect-on-separate-server"></a>Установка Azure AD Connect на отдельном сервере
При установке Azure AD Connect на новом сервере hello подразумевается, что требуется tooperform чистой установки Azure AD Connect. Поскольку требуется конфигурации DirSync hello toouse существует tootake некоторые дополнительные действия:

1. Запустите установщик hello Azure AD Connect (MSI).
2. При появлении hello **приветствия tooAzure AD Connect** экране мастера установки hello выход, щелкнув hello «X» в верхнем правом углу hello окна hello.
3. Откройте окно командной строки.
4. Hello установить расположение Azure AD Connect (по умолчанию: C:\Program Files\Microsoft Azure Active Directory Connect) выполните следующую команду hello: `AzureADConnect.exe /migrate`.
   Мастер установки Hello Azure AD Connect начинается и предоставляет следующий экран приветствия.  
   ![Введите учетные данные Azure AD.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)
5. Выберите файл параметров hello, экспортированный из установки DirSync.
6. Настройте любые дополнительные параметры, в том числе:
   * пользовательский путь установки Azure AD Connect;
   * существующий экземпляр SQL Server (по умолчанию Azure AD Connect устанавливает SQL Server 2012 Express). Не используйте hello же экземпляр базы данных, что и сервер DirSync.
   * Учетная запись службы используется tooconnect tooSQL сервера (базы данных SQL Server является удаленным, то эта учетная запись должна быть учетной записью службы домена).
     Следующие параметры можно увидеть на этом экране:   
     ![Введите учетные данные Azure AD.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)
7. Щелкните **Далее**.
8. На hello **готовности tooconfigure** оставьте hello **запуск процесса синхронизации hello сразу же после завершения настройки hello** проверяется. Hello server находится в [промежуточный режим](active-directory-aadconnectsync-operations.md#staging-mode) таким образом, изменения не будут экспортированного tooAzure AD.
9. Щелкните **Install**(Установить).
10. После завершения установки hello, выйдите из системы и войдите снова tooWindows, прежде чем использовать диспетчер служб синхронизации, редактор правил синхронизации, или попробуйте toomake изменения конфигурации.

> [!NOTE]
> Начинается синхронизация между Windows Server Active Directory и Azure Active Directory, но не вносить изменения экспортированных tooAzure AD. В каждый момент времени активно экспортировать изменения может только одно средство синхронизации. Это состояние называется [промежуточным режимом](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-that-azure-ad-connect-is-ready-toobegin-synchronization"></a>Убедитесь, что готовы toobegin синхронизации Azure AD Connect
tooverify, Azure AD Connect готов tootake через от DirSync, нужно tooopen **Synchronization Service Manager** в группе hello **Azure AD Connect** из меню "Пуск" hello.

В приложении hello go toohello **операции** вкладки. На этой вкладке убедитесь, что hello следующие операции выполнены:

* Импортируйте на hello соединителя AD
* Импортируйте на hello соединителя Azure AD
* Полная синхронизация по hello соединителя AD
* Полная синхронизация по hello соединителя Azure AD

![Импорт и синхронизация завершены](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

Просмотрите результат hello из этих операций и убедитесь, что нет ошибок.

Toosee и проверять hello изменения, которые будут экспортированы toobe tooAzure AD, считываются как tooverify hello конфигурации в разделе [промежуточный режим](active-directory-aadconnectsync-operations.md#staging-mode). Внесите необходимые изменения конфигурации, пока не увидите что-нибудь непредвиденное.

Все готово tooswitch из tooAzure DirSync AD выполнены эти действия при довольны результатами hello.

### <a name="uninstall-dirsync-old-server"></a>Удаление DirSync (старый сервер)
* В разделе **Программы и компоненты** найдите **Microsoft Azure Active Directory Sync Tool**.
* Удалите **Microsoft Azure Active Directory Sync Tool**
* Удаление Hello может занимать toocomplete too15 минут.

При желании позже toouninstall DirSync можно также временно завершить работу сервера hello или отключить службу hello. Если что-то пойдет не так, этот метод позволяет включить toore его. Однако он не ожидается следующем действии hello будут выполнены, поэтому это не требуется.

С помощью DirSync, удален или отключен нет ни одного активного сервера, экспорт tooAzure AD. Далее tooenable шаг Hello Azure AD Connect должны быть завершены до любые изменения в локальной службе Active Directory будут синхронизированы toobe tooAzure AD.

### <a name="enable-azure-ad-connect-new-server"></a>Включение Azure AD Connect (новый сервер)
После установки Azure AD повторное открытие подключения будет позволяют toomake дополнительные изменения конфигурации. Запуск **Azure AD Connect** из меню "Пуск" hello или hello ярлык на рабочем столе hello. Убедитесь, что не предпринимайте toorun hello установку MSI.

Вы должны увидеть следующие hello.  
![Дополнительные задачи](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* Выберите **Настроить промежуточный режим**.
* Отключить промежуточного хранения, сняв флажок hello **промежуточный режим включен** флажок.

![Введите учетные данные Azure AD.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* Нажмите кнопку hello **Далее** кнопки
* На странице подтверждения hello, щелкните hello **установить** кнопки.

Azure AD Connect теперь является активного сервера и не переключитесь задней toousing существующего сервера DirSync.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, после установки Azure AD Connect можно [проверка установки hello и назначить лицензии](active-directory-aadconnect-whats-next.md).

Дополнительные сведения об этих новых функций, которые были включены с установкой hello: [автоматическое обновление](active-directory-aadconnect-feature-automatic-upgrade.md), [избежать случайного удаления](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), и [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Дополнительные сведения об этих основных разделов: [планировщик и как синхронизировать tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
