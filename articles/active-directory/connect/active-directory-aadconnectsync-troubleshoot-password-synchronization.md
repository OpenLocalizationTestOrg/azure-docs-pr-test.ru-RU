---
title: "Устранение неполадок синхронизации паролей с помощью службы синхронизации Azure AD Connect | Документация Майкрософт"
description: "Эта статья содержит сведения по устранению неполадок синхронизации паролей."
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 0bf07e80e575309fe7fa44661776c23da5db6dce
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a>Устранение неполадок синхронизации паролей с помощью службы синхронизации Azure AD Connect
В этой статье приводятся пошаговые инструкции для устранения неполадок, связанных с синхронизацией паролей. Неполадки синхронизации паролей могут возникать либо в подмножестве пользователей, либо у всех.

Чтобы устранить неполадки синхронизации паролей в развертывании Azure Active Directory (Azure AD) Connect 1.1.614.0 или более поздней версии, используйте задачу устранения неполадок в мастере.

* Если пароли не синхронизируются, перейдите к разделу [Пароли не синхронизируются: устранение неполадок с помощью задачи устранения неполадок](#no-passwords-are-synchronized-troubleshoot-by-using-the-troubleshooting-task).

* Если возникла проблема с отдельными объектами, перейдите к разделу [Пароли не синхронизируются одним объектом: устранение неполадок с помощью задачи устранения неполадок](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-troubleshooting-task).

Для развертываний версии 1.1.524.0 и выше мы создали командлет диагностики, который вы можете использовать для устранения неполадок с синхронизацией паролей.

* Если пароли не синхронизируются, перейдите к разделу [Пароли не синхронизируются: устранение неполадок с помощью командлета диагностики](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet).

* Если возникла проблема с отдельными объектами, перейдите к разделу [Пароли не синхронизируются одним объектом: устранение неполадок с помощью командлета диагностики](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet).

Для ранних версий развертывания Azure AD Connect:

* Если пароли не синхронизируются, перейдите к разделу [Пароли не синхронизируются: шаги по устранению неполадок вручную](#no-passwords-are-synchronized-manual-troubleshooting-steps).

* Если возникла проблема с отдельными объектами, перейдите к разделу [Пароли не синхронизируются одним объектом: шаги по устранению неполадок вручную](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps).



## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-troubleshooting-task"></a>Пароли не синхронизируются: устранение неполадок с помощью задачи устранения неполадок
Вы можете использовать задачу устранения неполадок, чтобы выяснить, почему пароли не синхронизируются.

> [!NOTE]
> Эта задача доступна только для Azure AD Connect версии 1.1.614.0 и выше.

### <a name="run-the-troubleshooting-task"></a>Запуск задачи устранения неполадок
Чтобы устранить неполадки, связанные с синхронизацией паролей, сделайте следующее:

1. Откройте новый сеанс Windows PowerShell на сервере Azure AD Connect с помощью параметра **Запуск от имени администратора**.

2. Запустите `Set-ExecutionPolicy RemoteSigned` или `Set-ExecutionPolicy Unrestricted`.

3. Откройте мастер Azure AD Connect.

4. Перейдите к странице **Дополнительные задачи**, выберите **Устранение неполадок** и щелкните **Далее**.

5. На странице "Устранение неполадок" щелкните **Запуск**, чтобы открыть меню устранения неполадок в PowerShell.

6. В главном меню выберите **Устранение неполадок с синхронизацией паролей**.

7. В открывшемся подменю выберите **Синхронизация паролей не выполняется**.

### <a name="understand-the-results-of-the-troubleshooting-task"></a>Изучение результатов задачи устранения неполадок
Задача устранения неполадок выполняет следующие проверки.

* Проверяет, чтобы для вашего клиента Azure AD была включена функция синхронизации паролей.

* Проверяет, чтобы сервер Azure AD Connect не находился в промежуточном режиме.

* Для каждого существующего локального соединителя Active Directory (который соответствует существующему лесу Active Directory):

   * Проверяет, чтобы была включена функция синхронизации паролей.
   
   * Ищет события пульса синхронизации паролей в журнале событий приложений Windows.

   * Для каждого домена Active Directory в локальном соединителе Active Directory:

      * Проверяет, чтобы из сервера Azure AD Connect можно было получить доступ к домену.

      * Проверяет, чтобы учетные записи доменных служб Active Directory (AD DS), используемые локальным соединителем Active Directory, имели правильные имя пользователя, пароль и разрешения, необходимые для синхронизации паролей.

На схеме ниже отображаются результаты командлета для локальной топологии Active Directory с одним доменом:

![Диагностические выходные данные для синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

В оставшейся части этого раздела описаны возможные результаты, возвращаемые задачей, и соответствующие неполадки.

#### <a name="password-synchronization-feature-isnt-enabled"></a>Отключена функция синхронизации паролей
Если вы не включили синхронизацию паролей с помощью мастера Azure AD Connect, возвращается следующая ошибка:

![Отключена функция синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a>Сервер Azure AD Connect находится в промежуточном режиме
Если сервер Azure AD Connect находится в промежуточном режиме, синхронизация паролей временно отключена и возвращается следующая ошибка:

![Сервер Azure AD Connect находится в промежуточном режиме](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a>Отсутствуют события пульса синхронизации паролей
У каждого локального соединителя Active Directory есть свой собственный канал синхронизации паролей. Если установлен канал синхронизации паролей и нет необходимости синхронизировать какие-либо изменения пароля, в журнале событий приложений Windows каждые 30 минут создается событие пульса (EventId 654). Для каждого локального соединителя Active Directory командлет ищет соответствующие события пульса за последние три часа. Если событие пульса не найдено, возвращается следующая ошибка:

![Отсутствует событие пульса синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a>Учетная запись AD DS не имеет необходимых разрешений
Если учетная запись AD DS, используемая локальным соединителем Active Directory для синхронизации хэшей паролей, не содержит соответствующих разрешений, возвращается следующая ошибка:

![Неверные учетные данные](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a>Неправильный пароль или имя пользователя учетной записи AD DS
Если учетная запись AD DS, используемая локальным соединителем Active Directory для синхронизации хэшей паролей, содержит неправильный пароль или имя пользователя, возвращается следующая ошибка:

![Неверные учетные данные](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)



## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-troubleshooting-task"></a>Пароли не синхронизируются одним объектом: устранение неполадок с помощью задачи устранения неполадок

Вы можете использовать задачу устранения неполадок, чтобы определить, почему определенный объект не синхронизирует пароли.

> [!NOTE]
> Эта задача доступна только для Azure AD Connect версии 1.1.614.0 и выше.

### <a name="run-the-diagnostics-cmdlet"></a>Запуск командлета диагностики
Чтобы устранить неполадки для определенного объекта пользователя, сделайте следующее:

1. Откройте новый сеанс Windows PowerShell на сервере Azure AD Connect с помощью параметра **Запуск от имени администратора**.

2. Запустите `Set-ExecutionPolicy RemoteSigned` или `Set-ExecutionPolicy Unrestricted`.

3. Откройте мастер Azure AD Connect.

4. Перейдите к странице **Дополнительные задачи**, выберите **Устранение неполадок** и щелкните **Далее**.

5. На странице "Устранение неполадок" щелкните **Запуск**, чтобы открыть меню устранения неполадок в PowerShell.

6. В главном меню выберите **Устранение неполадок с синхронизацией паролей**.

7. Выберите в подменю **Пароль не синхронизируется для определенной учетной записи пользователя**.

### <a name="understand-the-results-of-the-troubleshooting-task"></a>Изучение результатов задачи устранения неполадок
Задача устранения неполадок выполняет следующие проверки.

* Проверяет состояние объекта Active Directory в пространстве соединителя Active Directory, метавселенной и пространстве соединителя Azure AD.

* Проверяет, чтобы с синхронизацией паролей были включены правила синхронизации, и чтобы они были применены к объекту Active Directory.

* Пытается извлечь и отобразить результаты последней попытки синхронизации паролей для объекта.

На схеме ниже отображаются результаты командлета при устранении неполадок синхронизации паролей для одного объекта:

![Диагностические выходные данные для синхронизации паролей для одного объекта](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

В оставшейся части этого раздела описываются определенные результаты, возвращенные командлетом, и соответствующие неполадки.

#### <a name="the-active-directory-object-isnt-exported-to-azure-ad"></a>Невозможно экспортировать в Azure AD объект Active Directory
Синхронизация паролей для этой локальной учетной записи Active Directory завершается сбоем, так как в клиенте Azure AD отсутствует соответствующий объект. Возвращается следующая ошибка:

![Отсутствует объект Azure AD](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a>У пользователя временный пароль
В настоящее время Azure AD Connect не поддерживает синхронизацию временных паролей с Azure AD. Пароль может рассматриваться как временный, если для локального пользователя Active Directory установлен параметр **смены пароля при следующем входе в систему**. Возвращается следующая ошибка:

![Временный пароль не экспортируется](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-to-synchronize-password-arent-available"></a>Результаты последней попытки синхронизации пароля недоступны
По умолчанию Azure AD Connect хранит результаты синхронизации паролей семь дней. Если для выбранного объекта Active Directory результаты недоступны, возвращается следующее предупреждение:

![Диагностические выходные данные для одного объекта: отсутствует история синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)



## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet"></a>Пароли не синхронизируются: устранение неполадок с помощью командлета диагностики
Вы можете использовать командлет `Invoke-ADSyncDiagnostics`, чтобы выяснить, почему не происходит синхронизация паролей.

> [!NOTE]
> Командлет `Invoke-ADSyncDiagnostics` доступен только для Azure AD Connect версии 1.1.524.0 или более поздней.

### <a name="run-the-diagnostics-cmdlet"></a>Запуск командлета диагностики
Чтобы устранить неполадки, связанные с синхронизацией паролей, сделайте следующее:

1. Откройте новый сеанс Windows PowerShell на сервере Azure AD Connect с помощью параметра **Запуск от имени администратора**.

2. Запустите `Set-ExecutionPolicy RemoteSigned` или `Set-ExecutionPolicy Unrestricted`.

3. Запустите `Import-Module ADSyncDiagnostics`.

4. Запустите `Invoke-ADSyncDiagnostics -PasswordSync`.



## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet"></a>Пароли не синхронизируются одним объектом: устранение неполадок с помощью командлета диагностики
Вы можете использовать командлет `Invoke-ADSyncDiagnostics`, чтобы определить, почему пароли не синхронизируются одним объектом.

> [!NOTE]
> Командлет `Invoke-ADSyncDiagnostics` доступен только для Azure AD Connect версии 1.1.524.0 или более поздней.

### <a name="run-the-diagnostics-cmdlet"></a>Запуск командлета диагностики
Чтобы устранить неполадки с синхронизацией паролей определенного пользователя, сделайте следующее:

1. Откройте новый сеанс Windows PowerShell на сервере Azure AD Connect с помощью параметра **Запуск от имени администратора**.

2. Запустите `Set-ExecutionPolicy RemoteSigned` или `Set-ExecutionPolicy Unrestricted`.

3. Запустите `Import-Module ADSyncDiagnostics`.

4. Выполните следующий командлет:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   Например: 
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```



## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a>Пароли не синхронизируются: шаги по устранению неполадок вручную
Чтобы выяснить, почему не происходит синхронизация паролей, выполните следующие действия:

1. Переведен ли сервер Connect в [промежуточный режим](active-directory-aadconnectsync-operations.md#staging-mode)? Сервер, находящийся в промежуточном режиме, не синхронизирует пароли.

2. Выполните сценарий, приведенный в разделе [Получение состояния параметров синхронизации паролей](#get-the-status-of-password-sync-settings). В этом разделе рассматривается конфигурация синхронизации паролей.  

    ![Выходные данные сценария PowerShell из параметров синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. Если в Azure AD не включена функция синхронизации паролей или не добавлено состояние канала синхронизации, запустите мастер установки Azure AD Connect. Выберите **Настроить параметры синхронизации** и снимите флажок синхронизации паролей. Это позволит временно отключить функцию. Затем снова запустите мастер установки и включите синхронизацию паролей. Запустите скрипт снова и проверьте правильность конфигурации.

4. Проверьте журнал событий на наличие ошибок. Найдите следующие события, которые могут указывать на проблему:
    * Источник: "Directory synchronization" ID: 0, 611, 652, 655. Если вы видите эти события, то это свидетельствует о проблеме с подключением. Сообщение в журнале событий содержит сведения о лесе, в котором возникла проблема. Дополнительные сведения см. в разделе о [проблеме с подключением](#connectivity problem).

5. Если нет пульса или не сработали другие методы, то [запустите полную синхронизацию всех паролей](#trigger-a-full-sync-of-all-passwords). Этот сценарий необходимо выполнить только один раз.

6. Ознакомьтесь с разделом [Пароли не синхронизируются одним объектом](#one-object-is-not-synchronizing-passwords).

### <a name="connectivity-problems"></a>Проблемы с подключением

Проверьте, есть ли подключение к Azure AD.

Имеет ли учетная запись необходимые разрешения для чтения хэшей паролей во всех доменах? Если при установке Connect вы использовали стандартные параметры, то у вас уже должны быть необходимые разрешения. 

Если вы использовали выборочную установку, задайте разрешения вручную следующим образом:
    
1. Чтобы найти учетную запись, используемую соединителем Active Directory, запустите **Synchronization Service Manager**. 
 
2. Перейдите в раздел **Connectors** (Соединители), а затем найдите локальный лес Active Directory, в котором устраняются неполадки. 
 
3. Выберите соединитель и щелкните **Properties** (Свойства). 
 
4. Выберите **Подключиться к лесу Active Directory**.  
    
    ![Учетная запись, используемая соединителем Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    Запишите имя пользователя и домен, в котором размещена учетная запись.
    
5. Запустите **Пользователи и компьютеры Active Directory** и проверьте, чтобы для учетной записи, найденной на предыдущем шаге, в корне всех доменов в лесу были заданы следующие разрешения:
    * Репликация изменений каталога
    * Репликация всех изменений каталога

6. Доступны ли контроллеры домена для Azure AD Connect? Если серверу Connect не удается подключиться ко всем контроллерам домена, настройте параметр **Only use preferred domain controller** (Использовать только предпочтительные контроллеры домена).  
    
    ![Контроллер домена, используемый соединителем Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. Вернитесь в меню **Synchronization Service Manager** и выберите **Configure Directory Partitions** (Настройка разделов каталога). 
 
8. В списке **Select directory partitions** (Выбор разделов каталога) выберите свой домен, установите флажок **Only use preferred domain controllers** (Использовать только предпочтительные контроллеры домена), а затем щелкните **Configure** (Настроить). 

9. В списке введите контроллеры домена, которые будет использовать Connect для синхронизации паролей. Этот же список используется для импорта и экспорта. Выполните эти действия для всех доменов.

10. Если в сценарии отображается отсутствие пульса, тогда запустите сценарий, приведенный в разделе [Запуск полной синхронизации всех паролей](#trigger-a-full-sync-of-all-passwords).

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a>Пароли не синхронизируются одним объектом: шаги по устранению неполадок вручную
Проблемы, связанные с синхронизацией паролей, можно легко устранить, просмотрев состояние объекта.

1. В средстве **Пользователи и компьютеры Active Directory** найдите пользователя, а затем убедитесь в отсутствии флажка для параметра **Требовать смены пароля при следующем входе в систему**.  

    ![Повышение производительности в Active Directory с помощью синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    Если флажок установлен, пользователь должен войти в систему и сменить пароль. Временные пароли не синхронизируются с Azure AD.

2. Если с паролем в Active Directory все в порядке, отследите пользователя в модуле синхронизации. Отследив пользователя от локального Active Directory до Azure AD, вы сможете убедиться в отсутствии ошибок в объекте.

    a. Запустите [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).

    Б. Щелкните **Соединители**.

    c. Выберите **соединитель Active Directory**, к которому относится пользователь.

    d. Выберите **Search Connector Space**(Поиск пространства соединителя).

    д. В поле **Scope** (Область) выберите **DN or Anchor** (Различающееся имя или привязка), а затем введите полное различающееся имя пользователя, для которого требуется устранить неполадки.

    ![Поиск пользователя в пространстве соединителя с различающимся именем](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    f. Найдите нужного пользователя и нажмите кнопку **Properties** (Свойства), чтобы просмотреть все атрибуты. Если в результатах поиска нет нужного пользователя, то проверьте [правила фильтрации](active-directory-aadconnectsync-configure-filtering.md) и выполните действия, описанные в разделе [Примените и проверьте изменения](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes). После этого пользователь должен отобразиться в Connect.

    ж. Чтобы просмотреть сведения о синхронизации паролей объекта за прошедшую неделю, щелкните **Log** (Журнал).  

    ![Сведения журнала для объекта](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    Если журнал объекта пуст, то Azure AD Connect не сможет считать хэш паролей из Active Directory. Перейдите к устранению неполадок, описанных в разделе [Проблема подключения](#connectivity-errors). Если состояние имеет значение, отличное от **успешного**, то воспользуйтесь таблицей в разделе [Журнал синхронизации паролей](#password-sync-log).

    h. Выберите вкладку **Lineage** (Журнал обращений и преобразований) и убедитесь, что по крайней мере для одного правила синхронизации в колонке **PasswordSync** задано значение **True**. В конфигурации по умолчанию правило синхронизации имеет имя **In from AD - User AccountEnabled**.  

    ![Сведения о пользователе в журнале обращений и преобразований](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    i. Щелкните **Metaverse Object Properties** (Свойства объекта метавселенной), чтобы показать список атрибутов пользователя.  

    ![Сведения метавселенной](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    Атрибут **cloudFiltered** должен отсутствовать. Убедитесь, что атрибуты домена (domainFQDN и domainNetBios) имеют ожидаемые значения.

    j. Щелкните вкладку **Connectors** (Соединители). Вы должны увидеть соединители для локального Active Directory и Azure AD.

    ![Сведения метавселенной](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    k. Выберите строку, которая представляет Azure AD, щелкните **Properties** (Свойства), а затем щелкните вкладку **Lineage** (Журнал обращений и преобразований). Объект пространства соединителя должен содержать правило исходящих подключений в колонке **синхронизации паролей** с заданным значением **True**. В конфигурации по умолчанию это будет правило синхронизации с именем **Out to AAD - User Join**.  

    ![Диалоговое окно свойств объекта пространства соединителя](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a>Журнал синхронизации паролей
В столбце "Состояние" могут содержаться перечисленные ниже значения.

| Status | ОПИСАНИЕ |
| --- | --- |
| Успешно |Пароль успешно синхронизирован |
| FilteredByTarget |Для пароля установлено значение **Пользователь должен изменить пароль при следующем входе**. Пароль не синхронизирован. |
| NoTargetConnection |Объект отсутствует в метавселенной или в пространстве соединителя Azure AD. |
| SourceConnectorNotPresent |Объект не найден в локальном пространстве соединителя Active Directory. |
| TargetNotExportedToDirectory |Объект в пространстве соединителя Azure AD еще не экспортирован. |
| MigratedCheckDetailsForMoreInfo |Запись журнала создана до выхода версии 1.0.9125.0 и отображается в исходном состоянии. |
| Ошибка |Служба вернула неизвестную ошибку. |
| Unknown |Произошла ошибка при попытке обработать пакет хэшей паролей.  |
| MissingAttribute |Недоступны определенные атрибуты (например, хэш Kerberos), необходимые доменным службам Azure AD. |
| RetryRequestedByTarget |Ранее были недоступны определенные атрибуты (например, хэш Kerberos), необходимые доменным службам Azure AD. Предпринята попытка повторно синхронизировать хэш пароля пользователя. |

## <a name="scripts-to-help-troubleshooting"></a>Сценарии, помогающие при устранении неполадок

### <a name="get-the-status-of-password-sync-settings"></a>Получение состояния параметров синхронизации паролей
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update the script to use the appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a>Запуск полной синхронизации всех паролей
> [!NOTE]
> Запустите этот сценарий только один раз. Если одного раза мало, то это значит, что проблема в чем-то другом. Для устранения этой проблемы обратитесь в службу поддержки Майкрософт.

Полную синхронизацию всех паролей можно активировать с помощью следующего сценария:

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a>Дополнительная информация
* [Реализация синхронизации паролей с помощью службы Azure AD Connect Sync](active-directory-aadconnectsync-implement-password-synchronization.md)
* [Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка](active-directory-aadconnectsync-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
