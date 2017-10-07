---
title: "Синхронизация паролей aaaTroubleshoot с Azure AD Connect sync | Документы Microsoft"
description: "Эта статья содержит сведения о том, как tootroubleshoot проблем с синхронизацией паролей."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a>Устранение неполадок синхронизации паролей с помощью службы синхронизации Azure AD Connect
В этом разделе шаги как tootroubleshoot проблемы с синхронизацией паролей. Неполадки синхронизации паролей могут возникать либо в подмножестве пользователей, либо у всех. Для Azure Active Directory (Azure AD) подключения развертывания к версии 1.1.524.0 или более поздней версии, теперь есть командлет диагностики, которые можно использовать tootroubleshoot проблем синхронизации паролей:

* Если имеется проблема, где нет пароли синхронизируются, см. toohello [не пароли синхронизируются: Устранение неполадок с помощью командлета диагностики hello](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) раздела.

* Если имеется проблема с отдельными объектами ссылаются toohello [одного объекта не выполняют синхронизацию паролей: Устранение неполадок с помощью командлета диагностики hello](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) раздела.

Для ранних версий развертывания Azure AD Connect:

* Если имеется проблема, где нет пароли синхронизируются, см. toohello [не пароли синхронизируются: вручную шаги по устранению неполадок](#no-passwords-are-synchronized-manual-troubleshooting-steps) раздела.

* Если имеется проблема с отдельными объектами ссылаются toohello [одного объекта не выполняют синхронизацию паролей: вручную шаги по устранению неполадок](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) раздела.

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Выполняется синхронизация паролей не: Устранение неполадок с помощью командлета диагностики hello
Можно использовать hello `Invoke-ADSyncDiagnostics` toofigure командлет out почему не пароли синхронизируются.

> [!NOTE]
> Hello `Invoke-ADSyncDiagnostics` командлет доступен только для Azure AD Connect версии 1.1.524.0 или более поздней версии.

### <a name="run-hello-diagnostics-cmdlet"></a>Запустите командлет диагностики hello
проблемы tootroubleshoot, где нет пароли синхронизируются:

1. Откройте новый сеанс Windows PowerShell на сервере Azure AD Connect с hello **Запуск от имени администратора** параметр.

2. Запустите `Set-ExecutionPolicy RemoteSigned` или `Set-ExecutionPolicy Unrestricted`.

3. Запустите `Import-Module ADSyncDiagnostics`.

4. Запустите `Invoke-ADSyncDiagnostics -PasswordSync`.

### <a name="understand-hello-results-of-hello-cmdlet"></a>Изучите результаты hello hello командлета
Hello диагностики командлет выполняет следующие проверки hello:

* Проверяет, hello включена функция синхронизации паролей для вашего клиента Azure AD.

* Проверяет, hello Azure AD Connect, сервер не находится в промежуточный режим.

* Для каждой существующей локальной Active Directory connector (которая соответствует tooan существующий лес Active Directory):

   * Проверяет, hello включена функция синхронизации паролей.
   
   * Выполняет поиск событий пульса синхронизации паролей в hello журналы событий приложений Windows.

   * Для каждого домена Active Directory под hello локальный Соединитель Active Directory:

      * Проверяет, hello домен доступен с сервера hello Azure AD Connect.

      * Проверяет наличие hello правильное имя пользователя, пароль и разрешения, необходимые для синхронизации паролей учетных записей доменных служб Active Directory (AD DS) hello, используемых hello локальный Соединитель Active Directory.

Привет, следующая схема иллюстрирует hello результаты командлета hello топологии одного домена в локальной среде Active Directory:

![Диагностические выходные данные для синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

Hello оставшейся части этого раздела описываются определенные результаты, возвращаемые командлетом hello и соответствующих проблем.

#### <a name="password-synchronization-feature-isnt-enabled"></a>Отключена функция синхронизации паролей
Если вы не включили синхронизации паролей с помощью мастера hello Azure AD Connect, возвращается hello следующая ошибка:

![Отключена функция синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a>Сервер Azure AD Connect находится в промежуточном режиме
В случае сервера Azure AD Connect hello в промежуточный режим синхронизации паролей временно отключена и hello будет возвращена следующая ошибка:

![Сервер Azure AD Connect находится в промежуточном режиме](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a>Отсутствуют события пульса синхронизации паролей
У каждого локального соединителя Active Directory есть свой собственный канал синхронизации паролей. Если не синхронизировать изменения toobe любой пароль система устанавливается канал синхронизации пароля hello, событие пульса (EventId 654) создается один раз каждые 30 минут в журнале событий приложений Windows hello. Для каждого локального соединителя Active Directory, hello командлет ищет соответствующие события пульса в hello последние три часа. Если событие пульса не найден, hello будет возвращена следующая ошибка:

![Отсутствует событие пульса синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a>Учетная запись AD DS не имеет необходимых разрешений
Если учетная запись hello AD DS, используемый hello в локальной среде хэши паролей toosynchronize Соединитель Active Directory не имеет соответствующих разрешений hello hello будет возвращена следующая ошибка:

![Неверные учетные данные](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a>Неправильный пароль или имя пользователя учетной записи AD DS
Если hello Доменных службах Active Directory учетная запись используется hello хэши паролей toosynchronize Соединитель Active Directory в локальной среде имеет неправильное имя пользователя или пароль, hello будет возвращена следующая ошибка:

![Неверные учетные данные](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Один объект не выполняют синхронизацию паролей: Устранение неполадок с помощью командлета диагностики hello
Можно использовать hello `Invoke-ADSyncDiagnostics` toodetermine командлета, почему один объект не выполняется синхронизация паролей.

> [!NOTE]
> Hello `Invoke-ADSyncDiagnostics` командлет доступен только для Azure AD Connect версии 1.1.524.0 или более поздней версии.

### <a name="run-hello-diagnostics-cmdlet"></a>Запустите командлет диагностики hello
проблемы tootroubleshoot, где нет пароли синхронизируются:

1. Откройте новый сеанс Windows PowerShell на сервере Azure AD Connect с hello **Запуск от имени администратора** параметр.

2. Запустите `Set-ExecutionPolicy RemoteSigned` или `Set-ExecutionPolicy Unrestricted`.

3. Запустите `Import-Module ADSyncDiagnostics`.

4. Выполните следующий командлет hello.
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   Например:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a>Изучите результаты hello hello командлета
Hello диагностики командлет выполняет следующие проверки hello:

* Проверяет состояние hello объекта Active Directory hello в пространство соединителя Active Directory hello, метавселенной и Azure AD пространством соединителя.

* Проверяет, что отсутствуют правила синхронизации с синхронизацией паролей включен и применяется toohello объекта Active Directory.

* Пытается tooretrieve и отображение результатов hello hello последней попытки toosynchronize hello пароля для hello объекта.

Привет, следующая схема иллюстрирует hello результаты командлета hello при устранении неполадок синхронизации паролей для одного объекта:

![Диагностические выходные данные для синхронизации паролей для одного объекта](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

Hello оставшейся части этого раздела описываются определенных результатов, возвращаемых командлетом hello и соответствующих проблем.

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a>объект Active Directory Hello не экспортированного tooAzure AD
Синхронизация паролей для этой учетной записи локальной службы каталогов Active Directory завершается ошибкой, так как отсутствует соответствующий объект в клиенте Azure AD hello. возвращается следующая ошибка Hello:

![Отсутствует объект Azure AD](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a>У пользователя временный пароль
В настоящее время Azure AD Connect не поддерживает синхронизацию временных паролей с Azure AD. Пароль считается toobe временные Если hello **смену пароля при следующем входе в систему** был установлен на hello локального пользователя Active Directory. возвращается следующая ошибка Hello:

![Временный пароль не экспортируется](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a>Результаты выполнения последней попытки toosynchronize пароль недоступны
По умолчанию Azure AD Connect сохраняются результаты hello попыток синхронизации паролей на семь дней. Если нет результатов для выбранного hello объекта Active Directory, возвращается hello следующие предупреждения:

![Диагностические выходные данные для одного объекта: отсутствует история синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a>Пароли не синхронизируются: шаги по устранению неполадок вручную
Выполните эти шаги toodetermine, почему не пароли синхронизируются.

1. — Сервер Connect hello в [промежуточный режим](active-directory-aadconnectsync-operations.md#staging-mode)? Сервер, находящийся в промежуточном режиме, не синхронизирует пароли.

2. Выполнение скрипта hello hello [получить состояние hello синхронизации паролей](#get-the-status-of-password-sync-settings) раздела. Он предоставляет общие сведения о конфигурации синхронизации пароля hello.  

    ![Выходные данные сценария PowerShell из параметров синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. Если функция hello не включена в Azure AD или состояние канала синхронизации hello не включена, запустите мастер установки Connect hello. Выберите **Настроить параметры синхронизации** и снимите флажок синхронизации паролей. Это изменение временно отключает функцию «hello». Затем снова запустите мастер hello и повторное включение синхронизации паролей. Запустите сценарий hello снова tooverify, hello конфигурации указано правильно.

4. Просмотрите журнал ошибок hello. Найдите следующие события, указывающие на проблему hello:
    * Источник: "Directory synchronization" ID: 0, 611, 652, 655. Если вы видите эти события, то это свидетельствует о проблеме с подключением. сообщения журнала событий Hello содержит сведения лесу, где возникла проблема. Дополнительные сведения см. в разделе о [проблеме с подключением](#connectivity problem).

5. Если нет пульса или не сработали другие методы, то [запустите полную синхронизацию всех паролей](#trigger-a-full-sync-of-all-passwords). Запустите сценарий hello только один раз.

6. В разделе hello [Устранение один объект, который не выполняют синхронизацию паролей](#one-object-is-not-synchronizing-passwords) раздела.

### <a name="connectivity-problems"></a>Проблемы с подключением

Проверьте, есть ли подключение к Azure AD.

Требуется хэши паролей hello tooread разрешения во всех доменах hello учетная запись? Если вы установили подключение с помощью экспресс-параметры, разрешения hello уже должен быть правильно. 

Если вы использовали выборочную установку, разрешения hello вручную, выполнив hello ниже:
    
1. hello toofind учетная запись, используемая службой соединителя Active Directory hello, start **диспетчер службы синхронизации**. 
 
2. Go слишком**соединители**и выполните поиск в лесу Active Directory локальной hello, устранении неполадок. 
 
3. Выберите соединитель hello и нажмите кнопку **свойства**. 
 
4. Go слишком**подключения леса tooActive**.  
    
    ![Учетная запись, используемая соединителем Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    Обратите внимание, hello имя пользователя и домен hello, где расположена учетная запись hello.
    
5. Запуск **Active Directory — пользователи и компьютеры**и убедитесь, что учетная запись hello, найденные ранее имеет разрешения выполните hello в корне hello всех доменов в лесу:
    * Репликация изменений каталога
    * Репликация всех изменений каталога

6. Являются hello контроллерами домена, которые доступны для Azure AD Connect? Если подключение сервера hello не может подключаться tooall контроллеров домена, настройте **использовать предпочтительный контроллер домена только**.  
    
    ![Контроллер домена, используемый соединителем Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. Возврат слишком**Synchronization Service Manager** и **Настройка раздела каталога**. 
 
8. Выберите домен в **выберите разделы каталога**выберите hello **использовать только контроллеры домена предпочтительный** флажок и нажмите кнопку **Настройка**. 

9. В списке hello введите hello контроллеры домена, подключение следует использовать для синхронизации паролей. Hello один список используется для импорта и экспорта также. Выполните эти действия для всех доменов.

10. Если hello сценарий показывает, что не пакетов пульса, выполните сценарий hello в [запуска полной синхронизации всех паролей](#trigger-a-full-sync-of-all-passwords).

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a>Пароли не синхронизируются одним объектом: шаги по устранению неполадок вручную
Можно легко устранения неполадок синхронизации паролей, проверив состояние hello объекта.

1. В **Active Directory — пользователи и компьютеры**, поиск пользователя hello и убедитесь, что hello **пользователь должен сменить пароль при следующем входе в систему** флажок снят.  

    ![Повышение производительности в Active Directory с помощью синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    Если установлен флажок "hello", попросите toosign пользователя hello в и смену пароля hello. Временные пароли не синхронизируются с Azure AD.

2. Если пароль hello верны в Active Directory, выполните пользователя hello в модуль синхронизации hello. Следующие hello пользователя из локальной Active Directory tooAzure AD вы увидите, имеются ли описательное сообщение об ошибке hello объекта.

    а. Запуск hello [диспетчер службы синхронизации](active-directory-aadconnectsync-service-manager-ui.md).

    b. Щелкните **Соединители**.

    c. Выберите hello **Соединитель Active Directory** где находится пользователь hello.

    d. Выберите **Search Connector Space**(Поиск пространства соединителя).

    д. В hello **область** выберите **DN или привязки**и введите полное имя DN hello пользователя hello, устранении неполадок.

    ![Поиск пользователя в пространстве соединителя с различающимся именем](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    f. Найдите hello пользователя ищете и нажмите кнопку **свойства** toosee все hello атрибуты. Если пользователь hello не hello результат поиска, проверьте вашей [правила фильтрации](active-directory-aadconnectsync-configure-filtering.md) и убедитесь, что запускается [применить и проверка изменений](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) для tooappear пользователя hello в соединение.

    ж. щелкните последнюю неделю toosee пароль hello синхронизации сведений hello объекта для hello **журнала**.  

    ![Сведения журнала для объекта](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    Если журнал hello объекта пуст, Azure AD Connect был хэш пароля невозможно tooread hello из Active Directory. Перейдите к устранению неполадок, описанных в разделе [Проблема подключения](#connectivity-errors). Если вы видите любое другое значение, чем **успех**, см. таблицу toohello в [журнал синхронизации паролей](#password-sync-log).

    h. Выберите hello **журнала обращений и преобразований** вкладку и убедитесь, что это правило синхронизации по крайней мере один в hello **PasswordSync** столбец **True**. В конфигурации по умолчанию hello hello правило синхронизации hello называется **в из AD — User AccountEnabled**.  

    ![Сведения о пользователе в журнале обращений и преобразований](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    i. Нажмите кнопку **свойства объекта метавселенной** toodisplay список атрибутов пользователей.  

    ![Сведения метавселенной](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    Атрибут **cloudFiltered** должен отсутствовать. Убедитесь, что атрибуты домена hello (domainFQDN и domainNetBios) hello ожидаемые значения.

    j. Нажмите кнопку hello **соединители** вкладки. Убедитесь, что вы видите tooboth соединители локальной Active Directory и Azure AD.

    ![Сведения метавселенной](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    k. Выберите hello строку, представляющую Azure AD щелкните **свойства**и нажмите кнопку hello **журнала обращений и преобразований** объект пространства соединителя hello вкладку должны иметь исходящего правила в hello **PasswordSync** столбец установлен слишком**True**. В конфигурации по умолчанию hello hello правило синхронизации hello называется **Out tooAAD - User Join**.  

    ![Диалоговое окно свойств объекта пространства соединителя](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a>Журнал синхронизации паролей
Hello Status может содержать hello следующие значения:

| Состояние | Description (Описание) |
| --- | --- |
| Успешно |Пароль успешно синхронизирован |
| FilteredByTarget |Задать пароль слишком**пользователь должен сменить пароль при следующем входе в систему**. Пароль не синхронизирован. |
| NoTargetConnection |Ни один из объектов в метавселенной hello или в пространство соединителя hello Azure AD. |
| SourceConnectorNotPresent |Объект не найден в пространство соединителя hello в локальной среде Active Directory. |
| TargetNotExportedToDirectory |Hello объекта в hello пространство соединителя Azure AD не экспортированы. |
| MigratedCheckDetailsForMoreInfo |Запись журнала создана до выхода версии 1.0.9125.0 и отображается в исходном состоянии. |
| Ошибка |Служба вернула неизвестную ошибку. |
| Unknown |Произошла ошибка при попытке tooprocess пакет хэши паролей.  |
| MissingAttribute |Недоступны определенные атрибуты (например, хэш Kerberos), необходимые доменным службам Azure AD. |
| RetryRequestedByTarget |Ранее были недоступны определенные атрибуты (например, хэш Kerberos), необходимые доменным службам Azure AD. Выполняется попытка tooresynchronize hello хэш пароля пользователя. |

## <a name="scripts-toohelp-troubleshooting"></a>Устранение неполадок toohelp сценариев

### <a name="get-hello-status-of-password-sync-settings"></a>Получить состояние hello синхронизации паролей
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
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
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
> Запустите этот сценарий только один раз. Если вам требуется toorun его несколько раз, либо является проблема hello. tootroubleshoot hello проблему, обратитесь в службу поддержки Майкрософт.

Полная синхронизация всех паролей можно запускать с помощью hello следующий скрипт:

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

## <a name="next-steps"></a>Дальнейшие действия
* [Реализация синхронизации паролей с помощью службы Azure AD Connect Sync](active-directory-aadconnectsync-implement-password-synchronization.md)
* [Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка](active-directory-aadconnectsync-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
