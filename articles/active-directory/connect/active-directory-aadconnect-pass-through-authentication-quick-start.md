---
title: "Краткое руководство по сквозной проверке подлинности Azure AD | Документация Майкрософт"
description: "В этой статье описывается, как tooget работу с сквозная проверка подлинности Azure Active Directory (Azure AD)."
services: active-directory
keywords: "сквозная проверка подлинности azure ad connect, установка active directory, необходимые компоненты для azure ad, единый вход"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: billmath
ms.openlocfilehash: d6d0f85fe144cf36cc94676f6592d37988b20647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a>Краткое руководство по сквозной проверке подлинности Azure Active Directory

## <a name="how-toodeploy-azure-ad-pass-through-authentication"></a>Как toodeploy Azure AD сквозная проверка подлинности

Сквозная проверка подлинности Azure Active Directory (Azure AD) позволяет вашей toosign пользователей tooboth на локальном компьютере и облачными приложениями с помощью hello одинаковые пароли. При входе пользователей в систему их пароли проверяются непосредственно в локальной службе Active Directory.

>[!IMPORTANT]
>Сквозная проверка подлинности Azure AD доступна в предварительной версии. Если вы использовали эту функцию через миниатюрные изображения, следует убедиться, обновлении бета-версии агентов hello проверки подлинности с помощью hello инструкциям [здесь](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md).

Необходимые toofollow эти инструкции toodeploy сквозной проверки подлинности.

## <a name="step-1-check-prerequisites"></a>Шаг 1. Проверка предварительных требований

Убедитесь, что hello следующие необходимые компоненты будут на месте:

### <a name="on-hello-azure-active-directory-admin-center"></a>В центре администрирования Azure Active Directory hello

1. Создайте облачную учетную запись глобального администратора в клиенте Azure AD. Таким образом, вы можете управлять hello конфигурации клиента должен локальных служб отказать или становятся недоступными. См. дополнительные сведения о [добавлении облачной учетной записи глобального администратора](../active-directory-users-create-azure-portal.md). После этого этапа — критический tooensure, вы не получите блокировки клиента.
2. Добавьте один или несколько [имена пользовательских доменов](../active-directory-add-domain.md) клиента tooyour Azure AD. Пользователи выполняют вход с помощью одного из этих доменных имен.

### <a name="in-your-on-premises-environment"></a>В локальной среде

1. Определите сервер под управлением Windows Server 2012 R2 или более поздней версии на какие toorun Azure AD Connect. Добавьте лес toohello же AD hello server как hello пользователи, чьи пароли должны проверить toobe.
2. Установка hello [последнюю версию Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) на сервер hello, определенный в предыдущем шаге. При наличии Azure AD Connect работает, убедитесь, что hello версия 1.1.557.0 или более поздней версии.
3. Определите дополнительный сервер под управлением Windows Server 2012 R2 или позже на какие toorun a изолированный агент проверки подлинности. версия агента проверки подлинности Hello должен toobe 1.5.193.0 или более поздней версии. Этот сервер является необходимые tooensure высокого уровня доступности запросов на вход. Добавьте лес toohello же AD hello server как hello пользователи, чьи пароли должны проверить toobe.
4. Если брандмауэр между серверами и Azure AD, необходимо tooconfigure hello следующих элементов:
   - Гарантии того, что агенты проверки подлинности можно **исходящих** запросы tooAzure AD через hello, следующие порты:
   
   | Номер порта | Как он используется |
   | --- | --- |
   | **80** | Загрузка отзыва сертификатов списки отзыва сертификатов при проверке сертификата SSL hello |
   | **443** | Весь исходящий трафик для нашей службы. |
   
   Если брандмауэр инициирует toooriginating пользователей в соответствии с правилами, откройте эти порты для трафика из служб Windows, работающих в качестве сетевой службы.
   - Если брандмауэр или прокси-сервер разрешает список утвержденных DNS, белый список подключений слишком**\*. msappproxy.net** и  **\*. servicebus.windows.net**. Если нет, разрешить доступ слишком[диапазоны IP-центра обработки данных Azure](https://www.microsoft.com/download/details.aspx?id=41653), которой обновляются раз в неделю.
   - Агенты проверки подлинности требуется доступ слишком**login.windows.net** и **login.microsoftonline.com** для первоначальной регистрации так откройте брандмауэр для этих URL-адресов также.
   - Для проверки сертификата разблокировать hello следующие URL-адреса: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** и  **www.Microsoft.com:80**. Эти URL-адреса используются для проверки сертификатов в других продуктах Майкрософт, поэтому они же могут быть разблокированы.

## <a name="step-2-enable-exchange-activesync-support-optional"></a>Шаг 2. Включение поддержки Exchange ActiveSync (необязательно)

Выполните эти инструкции tooenable поддержку Exchange ActiveSync.

1. Используйте [Exchange PowerShell](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) hello toorun следующую команду:
```
Get-OrganizationConfig | fl per*
```

2. Проверьте значение hello hello `PerTenantSwitchToESTSEnabled` параметр. Если значение hello **true**, клиент настроен правильно, — это обычно hello так, для большинства клиентов. Если значение hello **false**, запустите hello следующую команду:
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. Убедитесь, что значение hello объекта hello `PerTenantSwitchToESTSEnabled` теперь установлено слишком**true**. Подождите часа, после чего скользящего toohello следующий шаг.

Если на этом этапе возникли какие-либо проблемы, ознакомьтесь с нашим [руководством по устранению неполадок](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues) для получения дополнительной информации.

## <a name="step-3-enable-hello-feature"></a>Шаг 3: Включение функции hello

Сквозную проверку подлинности можно включить с помощью [Azure AD Connect](active-directory-aadconnect.md).

>[!IMPORTANT]
>Сквозная проверка подлинности можно включить на сервере первичного или промежуточную Connect hello Azure AD. Настоятельно рекомендуется включить его с сервера-источника hello.

Если вы устанавливаете Azure AD Connect для hello первый раз, выберите hello [пользовательский путь установки](active-directory-aadconnect-get-started-custom.md). В hello **вход пользователя** выберите **сквозная проверка подлинности** как hello входа в методе. При успешном завершении агента сквозной проверки подлинности устанавливается на hello же сервере, что Azure AD Connect. Кроме того функция hello сквозная проверка подлинности включена для клиента.

![Azure AD Connect: страница "Вход пользователя"](./media/active-directory-aadconnect-sso/sso3.png)

Если вы уже установили Azure AD Connect (с помощью hello [экспресс-установка](active-directory-aadconnect-get-started-express.md) или hello [выборочной установки](active-directory-aadconnect-get-started-custom.md) путь), выберите **изменение пользователя на странице входа** в Azure AD Подключение, нажмите кнопку **Далее**. Выберите **сквозная проверка подлинности** как hello входа в методе. При успешном завершении агента сквозной проверки подлинности устанавливается на hello же сервере, что компонент Azure AD Connect и hello включена на клиенте.

![Azure AD Connect: страница "Смена имени пользователя для входа"](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
>Сквозная проверка подлинности — это функция уровня клиента. Включение он влияет на вход для пользователей через _все_ hello управляемые домены в клиенте. При переключении из tooPass сквозной проверкой подлинности AD FS рекомендуется, подождите по крайней мере за 12 часов перед завершением работы инфраструктуры AD FS — это время ожидания равно tooensure, пользователи могут сохранять вход tooExchange ActiveSync во время перехода.

## <a name="step-4-test-hello-feature"></a>Шаг 4: Тестирование функции hello

Выполните эти инструкции, tooverify правильно включена сквозная проверка подлинности.

1. Войдите в toohello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) с hello учетные данные глобального администратора для вашего клиента.
2. Выберите **Azure Active Directory** на левой навигационной hello.
3. Выберите **Azure AD Connect**.
4. Убедитесь, что hello **сквозная проверка подлинности** показано, как функция **включено**.
5. Выберите **Сквозная проверка подлинности**. Эту колонку список серверов hello, где установлены агенты проверки подлинности.

![Центр администрирования Active Directory Azure — колонка "Azure AD Connect"](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Центр администрирования Active Directory Azure — колонка "Сквозная проверка подлинности"](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

На этом этапе пользователи из всех управляемых доменов клиента смогут выполнять вход с помощью сквозной аутентификации. Тем не менее пользователи из федеративных доменов и дальше toosign с помощью служб федерации Active Directory (AD FS) или другого поставщика федерации, который вы настроили ранее. При преобразовании toomanaged федеративный домен, все пользователи из этого домена автоматически запускает вход с использованием сквозной проверки подлинности. Сквозная проверка подлинности функцией hello не влияет на пользователей только для облака.

## <a name="step-5-ensure-high-availability"></a>Шаг 5. Обеспечение высокого уровня доступности

Если планируется toodeploy сквозной проверки подлинности в рабочей среде, необходимо установить отдельный агент проверки подлинности. Установите этот второй агент проверки подлинности на сервере _других_ чем hello один запуск Azure AD Connect и hello первый агент проверки подлинности. Эта настройка обеспечит высокий уровень доступности запросов на вход. Выполните эти инструкции toodeploy изолированный агент проверки подлинности.

1. **Загрузить последнюю версию hello hello агент проверки подлинности (версии 1.5.193.0 или более поздней версии)**: вход toohello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) с учетными данными глобального администратора вашего клиента.
2. Выберите **Azure Active Directory** на левой навигационной hello.
3. Выберите **Azure AD Connect**, а затем — **проверка подлинности**. Далее выберите **Скачать агент**.
4. Нажмите кнопку hello **принимаю условия & Загрузить** кнопки.
5. **Установить последнюю версию агента проверки подлинности hello hello**: hello запустить исполняемый файл, загруженный в hello предыдущих шага. По запросу введите учетные данные глобального администратора для арендатора.

![Центр администрирования Azure Active Directory — кнопка "Download Authentication Agent" (Скачать агент аутентификации)](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Центр администрирования Azure Active Directory — колонка "Скачивание агента"](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
>Можно также загрузить hello агент проверки подлинности из [здесь](https://aka.ms/getauthagent). Убедитесь, что просмотрите и примите агент проверки подлинности hello [условия предоставления услуг](https://aka.ms/authagenteula) _перед_ его установки.

## <a name="next-steps"></a>Дальнейшие действия
- [**Текущие ограничения**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) — эта функция в настоящее время находится на стадии предварительной версии. Узнайте, какие сценарии поддерживаются, а какие нет.
- [**Техническое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-pass-through-authentication-how-it-works.md). Сведения о том, как работает эта функция.
- [**Часто задаваемые вопросы** ](active-directory-aadconnect-pass-through-authentication-faq.md) -ответы на вопросы и ответы toofrequently.
- [**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.
- [**Простой единый вход Azure Active Directory**](active-directory-aadconnect-sso.md). Дополнительные сведения об этой дополнительной функции.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.
