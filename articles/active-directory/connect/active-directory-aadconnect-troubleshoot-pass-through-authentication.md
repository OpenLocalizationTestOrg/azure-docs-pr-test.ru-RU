---
title: "Azure AD Connect: устранение неполадок в работе сквозной аутентификации | Документация Майкрософт"
description: "В этой статье описывается как tootroubleshoot сквозная проверка подлинности Azure Active Directory (Azure AD)."
services: active-directory
keywords: "Устранение неполадок в работе сквозной аутентификации Azure AD Connect, установка Active Directory, необходимые компоненты для Azure AD, единый вход"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a>Устранение неполадок в работе сквозной аутентификации Azure Active Directory

В этой статье вы найдете информацию по устранению распространенных неполадок в работе сквозной аутентификации Azure AD.

>[!IMPORTANT]
>Если вы столкнулись с необходимостью вход проблемы у пользователей со сквозной проверки подлинности, не отключения функции hello или удаления агентов сквозной проверки подлинности без необходимости снова только для облака toofall учетная запись глобального администратора. См. дополнительные сведения о [добавлении облачной учетной записи глобального администратора](../active-directory-users-create-azure-portal.md). Этот шаг очень важен для того, чтобы не потерять доступ к клиенту.

## <a name="general-issues"></a>Общие проблемы

### <a name="check-status-of-hello-feature-and-authentication-agents"></a>Проверьте состояние функции hello и агенты проверки подлинности

Убедитесь, этот компонент hello сквозная проверка подлинности по-прежнему **включено** относительно состояния агентов проверки подлинности клиента и hello показывает **Active**и не **неактивно**. Можно проверить состояние, будет toohello **Azure AD Connect** колонка на hello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com/).

![Центр администрирования Active Directory Azure — колонка "Azure AD Connect"](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Центр администрирования Active Directory Azure — колонка "Сквозная проверка подлинности"](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a>Сообщения об ошибках при входе пользователей

Если пользователь hello не удается toosign в с помощью сквозной проверки подлинности, они видят один hello следующие ошибки пользовательского интерфейса на экране входа hello Azure AD: 

|Ошибка|Description (Описание)|Способы устранения:
| --- | --- | ---
|AADSTS80001|Не удается tooconnect tooActive каталога|Убедитесь, что агент серверы члены леса hello же AD как hello пользователи, чьи пароли должны проверить toobe, которые могут tooconnect tooActive каталога.  
|AADSTS8002|Истекло время ожидания подключения tooActive каталога|Проверьте tooensure наличие Active Directory и отвечает toorequests от агентов hello.
|AADSTS80004|Недопустимый Hello имя пользователя, переданное toohello агента|Убедитесь, что пользователь hello пытается toosign вход с помощью hello верное имя пользователя.
|AADSTS80005|При проверке было обнаружено непредсказуемое исключение WebException|Это временная проблема. Повторите запрос hello. Если он по-прежнему toofail, обратитесь в службу поддержки Майкрософт.
|AADSTS80007|Произошла ошибка при взаимодействии с Active Directory|Журналы агента hello Дополнительные сведения и убедитесь, что Active Directory работает должным образом.

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Причины сбоя входа на Центр администрирования Azure Active Directory hello

Запуск устранения неполадок проблем входа пользователя, просмотрев hello [действия при входе отчетов](../active-directory-reporting-activity-sign-ins.md) на hello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com/).

![Центр администрирования Azure Active Directory — отчет о действиях входа](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

Перейдите в слишком**Azure Active Directory** -> **входа в систему** на hello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com/) и нажмите кнопку действия при входе определенного пользователя. Найдите hello **входа в код ошибки** поля. Сопоставьте значение hello, причина сбоя tooa поля и разрешение, с помощью hello в следующей таблице:

|Код ошибки входа|Причина ошибки входа|Способы устранения:
| --- | --- | ---
| 50144 | Истек срок действия пароля пользователя Active Directory. | Сброс пароля пользователя hello в локальной службе Active Directory.
| 80001 | Агент аутентификации недоступен. | Установите и зарегистрируйте агент аутентификации.
| 80002 | Истекло время ожидания запроса на проверку пароля агента аутентификации. | Проверьте, доступен с hello агент проверки подлинности Active Directory.
| 80003 | Агент аутентификации получил недопустимый ответ. | Если проблема hello постоянно между несколькими пользователями, проверьте конфигурацию Active Directory.
| 80004 | В запросе на вход использовано неправильное имя участника-пользователя (UPN). | Попросите hello toosign пользователя с помощью hello правильное имя пользователя.
| 80005 | Агент аутентификации: произошла ошибка. | Это временная проблема. Повторите попытку позже.
| 80007 | Не удается tooconnect tooActive агент проверки подлинности каталога. | Проверьте, доступен с hello агент проверки подлинности Active Directory.
| 80010 | Пароль не удается toodecrypt агент проверки подлинности. | Если проблема hello постоянно, установить и зарегистрировать новый агент проверки подлинности. А затем удалите hello текущего. 
| 80011 | Ключ расшифровки не удается tooretrieve агент проверки подлинности. | Если проблема hello постоянно, установить и зарегистрировать новый агент проверки подлинности. А затем удалите hello текущего.

## <a name="authentication-agent-installation-issues"></a>Проблемы с установкой агента аутентификации

### <a name="an-unexpected-error-occurred"></a>Произошла непредвиденная ошибка

[Собирать журналы агента](#collecting-pass-through-authentication-agent-logs) от сервера hello и обратитесь в службу поддержки Майкрософт по вашему вопросу.

## <a name="authentication-agent-registration-issues"></a>Проблемы с регистрацией агента аутентификации

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a>Не удалось зарегистрировать hello агент проверки подлинности из-за tooblocked порты

Убедитесь, hello сервера, на какие hello установлен агент проверки подлинности может обмениваться данными с URL-адреса и порты в списке службы [здесь](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a>Не удалось зарегистрировать hello агент проверки подлинности из-за ошибки авторизации tootoken или учетной записи

Вы должны использовать облачную учетную запись глобального администратора для установки и регистрации изолированного агента аутентификации или Azure AD Connect. Имеется известная проблема с поддержкой многофакторной проверки Подлинности глобального администратора учетных записей; Отключите многофакторную проверку Подлинности временно (только операции hello toocomplete) обойти эту проблему.

### <a name="an-unexpected-error-occurred"></a>Произошла непредвиденная ошибка

[Собирать журналы агента](#collecting-pass-through-authentication-agent-logs) от сервера hello и обратитесь в службу поддержки Майкрософт по вашему вопросу.

## <a name="authentication-agent-uninstallation-issues"></a>Проблемы с удалением агента аутентификации

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a>Предупреждение при удалении Azure AD Connect

При наличии сквозная проверка подлинности включена на клиенте, и повторите toouninstall Azure AD Connect, он показывает hello следующие предупреждающее сообщение: «пользователи не смогут использовать возможности toosign в tooAzure AD при отсутствии других агентов сквозная проверка подлинности установить на других серверах».

Убедитесь, что настройки [высокий доступных](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) перед удалением tooavoid Azure AD Connect, критические вход пользователя.

## <a name="issues-with-enabling-hello-feature"></a>Проблемы, связанные с Включение функции hello

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a>Не удалось включить функции hello, поскольку отсутствуют доступные агенты не проверки подлинности

Требуется toohave по крайней мере один активный агент проверки подлинности tooenable сквозной проверки подлинности для клиента. Можно установить агент аутентификации, установив либо Azure AD Connect, либо отдельный агент аутентификации.

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a>Включение функции hello сбой из-за tooblocked порты

Убедитесь, hello сервера, на котором установлен Azure AD Connect может обмениваться данными с URL-адреса и порты в списке службы [здесь](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a>Включение функции hello сбой из-за ошибки авторизации tootoken или учетной записи

Обязательно используйте только для облака учетной записи глобального администратора при включении функции hello. Известные проблемы с многофакторной проверкой подлинности (MFA) — включить глобальный администратор учетных записей; Отключите многофакторную проверку Подлинности временно (только операция hello toocomplete) обойти эту проблему.

## <a name="exchange-activesync-configuration-issues"></a>Проблемы с конфигурацией Exchange ActiveSync

Это hello распространенных проблем при настройке поддержки Exchange ActiveSync для сквозной проверки подлинности.

### <a name="exchange-powershell-issue"></a>Проблема Exchange PowerShell

Если вы видите hello»**не удается найти параметр, соответствующая имени параметра «PerTenantSwitchToESTSEnabled»\.**» Ошибка при выполнении hello `Set-OrganizationConfig` Exchange PowerShell команды, обратитесь в службу поддержки Майкрософт.

### <a name="exchange-activesync-not-working"></a>Exchange ActiveSync не работает

Конфигурация Hello принимает некоторый эффект tootake время - hello период времени зависит от среды. Если ситуации hello не удается устранить в течение долгого времени, обратитесь в службу поддержки Майкрософт.

## <a name="collecting-pass-through-authentication-agent-logs"></a>Сбор журналов агента сквозной аутентификации

В зависимости от типа проблемы, которые может иметь hello необходимо toolook в разных местах журналы агента сквозной проверки подлинности.

### <a name="authentication-agent-event-logs"></a>Журналы событий агента аутентификации

Для ошибок, связанных toohello агент проверки подлинности, откройте приложение просмотра событий на сервере hello hello и проверить в разделе **приложения и службы Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.

Для детального анализа включите журнал «Session» hello. Не запускайте hello агент проверки подлинности с этот журнал, включенным во время обычной работы; используется только для устранения неполадок. содержимое журнала Hello отображаются только после отключения hello журнала еще раз.

### <a name="detailed-trace-logs"></a>Подробные журналы трассировки

Найдите tootroubleshoot входа ошибки пользователей, журналы трассировки в **%programdata%\Microsoft\Azure AD Agent\Trace проверки подлинности подключения\\**. В этих журналах содержатся причины конкретного пользователя войти непрохождения с помощью функции hello сквозной проверки подлинности. Эти ошибки представляют собой также причины сбоя входа сопоставленных toohello, показано в предыдущем hello [таблицы](#sign-in-failure-reasons-on-the-Azure-portal). Ниже приведен пример записи в журнале.

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

Описательные сведения об ошибке hello ("1328 во" в предшествующих пример hello) можно получить, открыв командную строку hello и работающей hello следующую команду (Примечание: замените "1328 во" hello фактический номер ошибки, см в журналах):

`Net helpmsg 1328`

![Сквозная проверка подлинности](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a>Журналы контроллеров домена

Если включено ведение журнала аудита, Дополнительные сведения можно найти в журналах hello безопасности контроллеров домена. Простой способ tooquery входа запросы, отправленные агентами сквозной проверки подлинности выглядит следующим образом:

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a>Счетчики системного монитора

Другой способ toomonitor агенты проверки подлинности — счетчики монитора производительности отдельных tootrack на каждом сервере, где установлен агент проверки подлинности hello. Следующие глобальные счетчики hello используйте (**проверок подлинности # PTA**, **#PTA сбой проверки подлинности** и **#PTA успешных проверок подлинности**) и счетчиков ошибок (**Ошибки проверки подлинности # PTA**):

![Счетчики системного монитора для сквозной аутентификации](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
>Сквозная аутентификация обеспечивает высокий уровень доступности за счет нескольких агентов аутентификации, но _не_ предоставляет возможности балансировки нагрузки. В зависимости от вашей конфигурации _не_ все агенты аутентификации могут получать примерно _одинаковое_ число запросов. Возможно, какой-либо агент аутентификации вообще не получает трафик.
