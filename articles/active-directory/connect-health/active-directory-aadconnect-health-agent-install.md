---
title: "Установка агента работоспособности подключения aaaAzure AD | Документы Microsoft"
description: "Это страница hello Azure AD Connect Health, описывающий hello установки агента AD FS и синхронизации."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9019628ec1d4c477496e08910cfd668ed1933a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a>Установка агента Azure AD Connect Health
В этом документе рассматривается процесс установки и настройки агенты hello Azure AD Connect Health. Вы можете загрузить агенты hello из [здесь](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent).

## <a name="requirements"></a>Требования
Привет, в следующей таблице приведен список предварительных требований для использования Azure AD Connect Health.

| Требование | Описание |
| --- | --- |
| Azure AD Premium |Служба Azure AD Connect Health относится к Azure AD Premium и требует наличия выпуска Azure AD Premium. </br></br>Дополнительные сведения см. в статье [Приступая к работе с Azure Active Directory Premium](../active-directory-get-started-premium.md). </br>. в разделе toostart пробной 30-дневной [запустить пробную версию.](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Должен быть глобальный администратор вашей tooget Azure AD, работы с Azure AD Connect Health |По умолчанию только глобальные Администраторы hello можно установить и настроить hello работоспособности агентов tooget запущена, доступ hello портала и выполнять любые операции в Azure AD Connect Health. Дополнительные сведения см. в статье [Администрирование каталога Azure AD](../active-directory-administer.md). <br><br> С помощью управления доступом на основе ролей можно разрешить доступ пользователей tooother tooAzure AD Connect Health в вашей организации. Дополнительные сведения см. в разделе [Управление доступом с помощью контроля доступа на основе ролей](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control). </br></br>**Важно:** hello учетная запись, используемая при установке агентов hello должно быть рабочей или учебной учетной записи. Учетную запись Майкрософт для этого использовать нельзя. Дополнительные сведения см. в статье [Подпишитесь на Azure как организация](../sign-up-organization.md). |
| Агент Azure AD Connect Health следует установить на всех целевых серверах | Azure AD Connect Health требует toobe агенты работоспособности hello установлен и настроен на целевых серверах tooreceive hello данных и предоставляют возможности наблюдения и аналитика hello </br></br>Например данные tooget из инфраструктуры AD FS hello агент должен устанавливаться на hello AD FS и серверами прокси веб-приложения. Аналогичным образом, tooget данные на локальном инфраструктур AD DS, должен быть установлен агент hello на контроллерах домена hello. </br></br> |
| Конечные точки службы Azure toohello исходящие подключения | Во время установки и выполнения агента hello требуется конечных точек службы подключения к tooAzure AD Connect Health. Исходящие подключения заблокирован с помощью брандмауэров, убедитесь, что hello следующие конечные точки добавляются toohello списка разрешенных: </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.servicebus.windows.net, порт 5671; </li><li>&#42;.adhybridhealth.azure.com/;</li><li>https://management.azure.com </li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
|Исходящие подключения на основе IP-адресов | Для IP-адресов на основе фильтрации на брандмауэрах, см. toohello [диапазоны IP-адресов Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).|
| Проверка SSL для исходящего трафика отфильтрована или отключена | Hello агента регистрации шаг или данных операций отправки может завершиться ошибкой, если проверку SSL или завершения для исходящего трафика на сетевом уровне hello. |
| Порты брандмауэра на сервере hello агентом hello. |агент Hello требует hello, следующие порты брандмауэра toobe чтобы toocommunicate агента hello hello Azure AD Health конечными точками.</br></br><li>TCP-порт 443</li><li>TCP-порт 5671</li> |
| Разрешить следующие веб-сайты, если включена политика усиленной безопасности IE hello |Если включена политика усиленной безопасности IE, затем hello следующих веб-сайтов должен быть разрешен на сервере hello, установлен агент hello toohave постоянной.</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>Hello сервер федерации для вашей организации, доверенным для Azure Active Directory. (Например, https://sts.contoso.com.)</li> |
|Отключение FIPS|FIPS не поддерживается агентами Azure Active Directory Connect Health.|

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-fs"></a>Установка агента Azure AD Connect Health для AD FS hello
toostart Здравствуйте установки агента, дважды щелкните загруженный файл .exe hello. На первом экране приветствия нажмите кнопку "установить".

![Проверка Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install1.png)

После завершения установки hello, нажмите кнопку настроить.

![Проверка Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install2.png)

Это запускает процесс PowerShell hello tooinitiate окно агента регистрации. При появлении соответствующего запроса войдите под учетной записью Azure AD, имеющий доступ tooperform агента регистрации. По умолчанию hello учетная запись глобального администратора есть доступ.

![Проверка Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install3.png)

После входа PowerShell продолжит выполнять команду. По завершении его можно закрыть PowerShell и hello Настройка завершена.

На этом этапе hello службы необходимо запустить агент автоматически разрешает hello агент передачи hello необходимых данных toohello облачной службы в безопасном режиме.

Если не выполнены все необходимые компоненты hello подробно описаны в предыдущем разделе hello, предупреждения отображаются в окне PowerShell hello. Быть убедиться, что hello toocomplete [требования](active-directory-aadconnect-health-agent-install.md#requirements) до установки агента hello. Следующий снимок экрана приветствия приведен пример этих ошибок.

![Проверка Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install4.png)

установлен агент tooverify hello, найдите следующие службы на сервере hello hello. Если вы выполнили hello конфигурации, они уже должен быть запущен. В противном случае они были остановлены, пока не будет завершена настройка hello.

* Служба диагностики AD FS Azure AD Connect Health
* Служба AD FS получения ценной информации из данных о работоспособности Azure AD Connect
* Служба наблюдения AD FS Azure AD Connect Health

![Проверка Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>Установка агента на серверах Windows Server 2008 R2
Для серверов Windows Server 2008 R2 сделайте следующее:

1. Убедитесь, что на этом сервере hello работает с пакетом обновления 1 или более поздней версии.
2. Отключите IE ESC для установки агента.
3. Установите Windows PowerShell 4.0 на каждом из серверов hello перед установкой агента AD Health hello. tooinstall Windows PowerShell 4.0:
   * Установка [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779) с помощью hello следующая ссылка toodownload hello автономный установщик.
   * Установите интегрированную среду сценариев PowerShell (из компонентов Windows).
   * Установка hello [Windows Management Framework 4.0.](https://www.microsoft.com/download/details.aspx?id=40855)
   * Установить браузер Internet Explorer версии 10 или более поздней версии на сервере hello. (Требуется для службы работоспособности tooauthenticate hello, используя свои учетные данные администратора Azure).
4. Дополнительные сведения об установке Windows PowerShell 4.0 на Windows Server 2008 R2 см. в разделе вики-статье hello [здесь](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx).

### <a name="enable-auditing-for-ad-fs"></a>Включение аудита для AD FS
> [!NOTE]
> Этот раздел относится только к серверам tooAD федерации Active Directory. У вас toofollow следующие действия на веб-приложения hello прокси-серверах.
>

Чтобы hello аналитические данные об использовании компонентов toogather и анализ данных hello агента Azure AD Connect Health должен hello сведения в журналах аудита hello AD FS. По умолчанию эти журналы не включены. Hello используйте следующие процедуры tooenable AD FS аудита toolocate hello AD FS аудит и журналы на серверах AD FS.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2008-r2"></a>tooenable аудита для AD FS в Windows Server 2008 R2
1. Нажмите кнопку **запустить**, слишком точки**программы**, слишком точки**Администрирование**и нажмите кнопку **Локальная политика безопасности**.
2. Перейдите toohello **безопасности безопасности\Локальные Политики\назначение прав** папки, а затем дважды щелкните Создание аудитов безопасности.
3. На hello **параметр локальной безопасности** убедитесь, что указана учетная запись службы hello AD FS 2.0. Если он отсутствует, нажмите кнопку **добавить пользователя или группу** и добавить его в список toohello и нажмите кнопку **ОК**.
4. Аудит tooenable, откройте командную строку с повышенными привилегиями и выполните следующую команду hello:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. Закройте локальную политику безопасности, а затем откройте оснастку управления hello. hello tooopen оснастки управления, нажмите кнопку **запустить**, точки слишком**программы**, точки слишком**Администрирование**и нажмите кнопку AD FS 2.0 управления.
6. В области действия hello щелкните Изменить свойства службы федерации.
7. В hello **свойства службы федерации** диалоговое окно, нажмите кнопку hello **события** вкладки.
8. Выберите hello **успешные события аудита** и **неудачные события аудита** флажки.
9. Нажмите кнопку **ОК**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>tooenable аудита для AD FS в Windows Server 2012 R2
1. Откройте **Локальная политика безопасности** , открыв **диспетчера сервера** на начальном экране hello, или диспетчер сервера на приветствия задач на рабочем столе hello, нажмите кнопку **средства/Локальная политика безопасности**.
2. Перейдите toohello **безопасности безопасности\Локальные Политики\назначение прав** папку и дважды щелкните **Создание аудитов безопасности**.
3. На hello **параметр локальной безопасности** убедитесь, что указана учетная запись службы федерации Active Directory hello AD. Если он отсутствует, нажмите кнопку **добавить пользователя или группу** и добавить его в список toohello и нажмите кнопку **ОК**.
4. tooenable аудита, откройте командную строку с повышенными привилегиями и запустите следующую команду hello: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```.
5. Закрыть **Локальная политика безопасности**, а затем откройте hello **управления AD FS** оснастки (в диспетчере серверов выберите в меню Сервис и выберите управления AD FS).
6. В области действия hello, щелкните **изменить свойства службы федерации**.
7. В диалоговом окне Свойства службы федерации hello, щелкните hello **события** вкладки.
8. Выберите hello **аудит успехов и аудит отказов** флажки и нажмите кнопку **ОК**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2016"></a>tooenable аудита для AD FS в Windows Server 2016
1. Откройте **Локальная политика безопасности** , открыв **диспетчера сервера** на начальном экране hello, или диспетчер сервера на приветствия задач на рабочем столе hello, нажмите кнопку **средства/Локальная политика безопасности**.
2. Перейдите toohello **безопасности безопасности\Локальные Политики\назначение прав** папку и дважды щелкните **Создание аудитов безопасности**.
3. На hello **параметр локальной безопасности** убедитесь, что указана учетная запись службы федерации Active Directory hello AD. Если он отсутствует, нажмите кнопку **добавить пользователя или группу** и добавление hello AD FS службы учетной записи toohello списка и нажмите кнопку **ОК**.
4. Аудит tooenable, откройте командную строку с повышенными привилегиями и выполните следующую команду hello:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. Закрыть **Локальная политика безопасности**, а затем откройте hello **управления AD FS** оснастки (в диспетчере серверов выберите в меню Сервис и выберите управления AD FS).
6. В области действия hello, щелкните **изменить свойства службы федерации**.
7. В диалоговом окне Свойства службы федерации hello, щелкните hello **события** вкладки.
8. Выберите hello **аудит успехов и аудит отказов** флажки и нажмите кнопку **ОК**. Этот параметр должен быть включен по умолчанию.
9. Откройте окно PowerShell и выполните следующую команду hello: ```Set-AdfsProperties -AuditLevel Verbose```.

Обратите внимание, что по умолчанию включен "базовый" уровень аудита. Дополнительные сведения о hello [улучшения аудита AD FS в Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)


#### <a name="toolocate-hello-ad-fs-audit-logs"></a>журналы аудита toolocate hello AD FS
1. Откройте **Средство просмотра событий**.
2. Журналы tooWindows перейдите и выберите **безопасности**.
3. Щелкните правой hello, **фильтр текущих журналов**.
4. В разделе «Источник события» выберите **Аудит AD FS**.

![Журналы аудита AD FS](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> Групповая политика может отключить аудит AD FS. Если аудит AD FS отключен, аналитика по использованию в отношении действий входа недоступна. Убедитесь, что групповая политика, которая может отключить аудит AD FS, отсутствует.>
>


## <a name="installing-hello-azure-ad-connect-health-agent-for-sync"></a>Установка агента hello Azure AD Connect Health для синхронизации
агент Hello Azure AD Connect Health для синхронизации автоматически устанавливается в последнюю сборку hello Azure AD Connect. toouse Azure AD Connect для синхронизации, то требуется toodownload hello последнюю версию Azure AD Connect и установить его. Можно загрузить последнюю версию hello [здесь](http://www.microsoft.com/download/details.aspx?id=47594).

установлен агент tooverify hello, найдите следующие службы на сервере hello hello. Если вы выполнили hello конфигурации, они уже должен быть запущен. В противном случае они были остановлены, пока не будет завершена настройка hello.

* Служба Sync Insights Azure AD Connect Health
* Служба Sync Monitoring Azure AD Connect Health

![Проверка Azure AD Connect Health для синхронизации](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> Помните, что для использования службы Azure AD Connect Health требуется Azure AD Premium. Если у вас Azure AD Premium, вы несете конфигурации не удается toocomplete hello в hello портал Azure. Дополнительные сведения см. в разделе hello [странице требований](active-directory-aadconnect-health-agent-install.md#requirements).
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>Регистрация агента Azure AD Connect Health для синхронизации вручную
Если hello Azure AD Connect Health для синхронизации агента регистрации завершается ошибкой после успешной установки Azure AD Connect, можно использовать следующую команду PowerShell toomanually зарегистрировать агент hello hello.

> [!IMPORTANT]
> С помощью этой команды PowerShell является только требуется, если происходит ошибка регистрации агента hello после установки Azure AD Connect.
>
>

Hello команда следующие команды PowerShell требуется только регистрация агента работоспособности hello сбоем даже после успешной установки и настройки Azure AD Connect. службы Azure AD Connect Health Hello начнется после успешной регистрации агента hello.

Можно вручную зарегистрировать агент hello Azure AD Connect Health для синхронизации с помощью hello следующую команду PowerShell:

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

Команда Hello принимает следующие параметры:

* AttributeFiltering: значение $true (по умолчанию) — Если Azure AD Connect не выполняет синхронизацию набор атрибутов по умолчанию hello и было toouse настраиваемого атрибута фильтра. В противном случае используется значение $false.
* StagingMode: $false (по умолчанию) — Если hello Azure AD Connect сервер находится в промежуточном режиме, $true, если сервер hello не настроена toobe в промежуточный режим.

При запросе проверки подлинности следует использовать учетную запись глобального администратора hello (такие как admin@domain.onmicrosoft.com), использованный для настройки Azure AD Connect.

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-ds"></a>Установка агента Azure AD Connect Health для AD DS hello
toostart Здравствуйте установки агента, дважды щелкните загруженный файл .exe hello. На первом экране приветствия нажмите кнопку "установить".

![Проверка Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

После завершения установки hello, нажмите кнопку настроить.

![Проверка Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

Это приведет к запуску командной строки и оболочки PowerShell, которая выполнит команду Register-AzureADConnectHealthADDSAgent. Когда запрос toosign в tooAzure, действуйте и выполните вход.

![Проверка Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

После входа PowerShell продолжит выполнять команду. По завершении его можно закрыть PowerShell и hello Настройка завершена.

На этом этапе hello службы должны запускаться автоматически, позволяя toomonitor агента hello и сбора данных. Если не выполнены все необходимые компоненты hello подробно описаны в предыдущем разделе hello, предупреждения отображаются в окне PowerShell hello. Быть убедиться, что hello toocomplete [требования](active-directory-aadconnect-health-agent-install.md#requirements) до установки агента hello. Следующий снимок экрана приветствия приведен пример этих ошибок.

![Проверка Azure AD Connect Health для AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

установлен агент tooverify hello, найдите следующие службы на контроллере домена hello hello.

* служба AD DS для Azure AD Connect Health;
* служба наблюдения AD DS Azure AD Connect Health.

Если вы выполнили конфигурации hello, эти службы должна быть запущена. В противном случае они были остановлены, пока не будет завершена настройка hello.

![Проверка Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a>Регистрация агента с помощью PowerShell
После установки setup.exe hello соответствующего агента, можно выполнить шаг регистрации агента hello, используя следующие команды PowerShell в зависимости от роли hello hello. Откройте окно PowerShell и выполните соответствующую команду hello:

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

Эти команды принять» учетные данные «как параметр toocomplete hello в неинтерактивном режиме или на компьютере Server Core.
* в переменной PowerShell, которая передается в качестве параметра могут захватываться Hello учетных данных.
* Можно указать любой идентификации Azure AD с агентами hello tooregister доступ, не поддерживает многофакторную проверку Подлинности включена.
* По умолчанию глобальные Администраторы имеют доступ tooperform агента регистрации. Можно также разрешить другие менее привилегированных удостоверений tooperform этот шаг. Дополнительные сведения см. в статье [Контроль доступа на основе ролей в Azure](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control).

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-toouse-http-proxy"></a>Настройка toouse агенты Azure AD Connect работоспособности прокси-сервера HTTP
Агенты Azure AD Connect работоспособности toowork можно настроить с помощью HTTP-прокси.

> [!NOTE]
> * С помощью «Netsh WinHttp set ProxyServerAddress» не поддерживается, поскольку агент hello использует веб-запросов System.Net toomake вместо службы Microsoft Windows HTTP.
> * Hello настроенный адрес прокси-сервера Http — используется toopass через зашифрованные сообщения Https.
> * Прокси-серверы с проверкой подлинности (с помощью HTTPBasic) не поддерживаются.
>
>

### <a name="change-health-agent-proxy-configuration"></a>Изменение конфигурации прокси-сервера агента работоспособности
У вас есть следующие параметры tooconfigure Azure AD Connect Health Agent toouse прокси-сервер HTTP hello.

> [!NOTE]
> Необходимо перезапустить все службы Azure AD Connect Health Agent, чтобы обновить параметры toobe с прокси-сервера hello. Выполните следующую команду hello.<br>
> Restart-Service AdHealth*
>
>

#### <a name="import-existing-proxy-settings"></a>Импорт имеющихся параметров прокси-сервера
##### <a name="import-from-internet-explorer"></a>Импорт из Internet Explorer
Можно импортировать параметры прокси-сервера Internet Explorer HTTP и toobe используется hello агенты Azure AD Connect работоспособности. На каждом сервере hello агентом работоспособности hello выполните следующую команду PowerShell hello:

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>Импорт из WinHTTP
Можно импортировать параметры прокси-сервера WinHTTP и toobe используется hello агенты Azure AD Connect работоспособности. На каждом сервере hello агентом работоспособности hello выполните следующую команду PowerShell hello:

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>Задание адресов прокси-сервера вручную
Можно вручную указать прокси-сервера на каждом из серверов hello запущен агент работоспособности hello, выполнив следующую команду PowerShell hello:

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

Пример: *Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress myproxyserver:443*.

* Значение "address" может быть именем сервера, разрешимым в DNS, или адресом IPv4.
* Значение "port" можно опустить. Если это значение не указано, в качестве порта по умолчанию используется 443.

#### <a name="clear-existing-proxy-configuration"></a>Очистка существующей конфигурации прокси-сервера
Можно снять hello существующую конфигурацию прокси-сервера, выполнив следующую команду hello:

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>Считывание текущих параметров прокси-сервера
Можно прочитать hello в настоящее время настроены параметры прокси-сервера, выполнив следующую команду hello.

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-tooazure-ad-connect-health-service"></a>Тестирование подключения tooAzure AD подключение службы работоспособности
Это возможно, что могут возникнуть проблемы с приводит hello Azure AD Connect Health agent toolose связи со службой hello Azure AD Connect Health. К ним относятся проблемы с сетью, с правами доступа и другие причины.

Если агент hello службы toohello Azure AD Connect Health не удается toosend данных более двух часов, он обозначается hello следующие оповещения в портале hello: «данные службы работоспособности не копирование toodate.» Вы можете подтвердить агента Azure AD Connect Health hello затронутых является может tooupload данных toohello Azure AD Connect Health службы, выполнив следующую команду PowerShell hello:

    Test-AzureADConnectHealthConnectivity -Role ADFS

параметр роли Hello в настоящее время имеет hello следующие значения:

* ADFS
* Sync
* ADDS

Можно использовать флаг - ShowResults hello в tooview команда hello подробные журналы. Используйте следующий пример hello.

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> Средство подключения к toouse hello, сначала необходимо первой регистрации агента завершения hello. При отсутствии возможности toocomplete hello агента регистрации, убедитесь в том, что выполнены все hello [требования](active-directory-aadconnect-health-agent-install.md#requirements) для Azure AD Connect Health. Эта проверка подключения выполняется по умолчанию во время регистрации агента.
>
>

## <a name="related-links"></a>Связанные ссылки
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Операции Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Использование Azure AD Connect Health с AD FS](active-directory-aadconnect-health-adfs.md)
* [Использование Azure AD Connect Health для синхронизации](active-directory-aadconnect-health-sync.md)
* [Using Azure AD Connect Health with AD DS (Использование Azure AD Connect Health с AD DS)](active-directory-aadconnect-health-adds.md)
* [Часто задаваемые вопросы об Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health: история версий](active-directory-aadconnect-health-version-history.md)
