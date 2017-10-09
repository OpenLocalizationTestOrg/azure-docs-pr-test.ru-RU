---
title: "Azure AD Connect: простой единый вход — быстрый запуск| Документы Майкрософт"
description: "В этой статье описывается, как tooget работу с Azure Active Directory прозрачную единого входа."
services: active-directory
keywords: "что такое Azure AD Connect, установка Active Directory, необходимые компоненты для Azure AD, единый вход"
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
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Простой единый вход Azure Active Directory — быстрый запуск

## <a name="how-toodeploy-seamless-sso"></a>Как toodeploy прозрачную единого входа

Azure Active Directory прозрачную единого входа (Azure AD, эффективная SSO) автоматически подписывает пользователей они находятся в своей корпоративной сети подключенных tooyour рабочих станций в организации. Он предоставляет удобного доступа пользователей tooyour облачные приложения без необходимости какие-либо дополнительные локальные компоненты.

>[!IMPORTANT]
>компонент Hello прозрачную единого входа в настоящий момент в режиме предварительного просмотра.

toodeploy прозрачную единого входа требуется toofollow следующие действия:

## <a name="step-1-check-prerequisites"></a>Шаг 1. Проверка предварительных требований

Убедитесь, что hello следующие необходимые компоненты будут на месте:

1. Настройка сервера Azure AD Connect. Если в качестве метода входа вы используете [сквозную проверку подлинности](active-directory-aadconnect-pass-through-authentication.md), никакие дополнительные действия не требуются. Если в качестве метода входа вы используете [синхронизацию хэша паролей](active-directory-aadconnectsync-implement-password-synchronization.md) и между Azure AD Connect и Azure AD существует брандмауэр, убедитесь, что:
- Вы используете версию 1.1.484.0 или более позднюю версию Azure AD Connect.
- Azure AD Connect может взаимодействовать с URL-адресами `*.msappproxy.net` и через порт 443. Это предварительное условие применимо только в том случае, если включена функция hello, а не для входа в систему пользователя.
- Azure AD Connect можно сделать toohello подключения прямых IP [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/details.aspx?id=41653). Опять же это предварительное условие применимо только в том случае, если включена функция hello.
2. Необходимо иметь учетные данные администратора домена для каждого леса AD синхронизации tooAzure AD (с помощью Azure AD Connect) и для пользователей, для которого требуется tooenable прозрачную единого входа.

## <a name="step-2-enable-hello-feature"></a>Шаг 2: Включение функции hello

Простой единый вход можно включить с помощью [Azure AD Connect](active-directory-aadconnect.md).

При выполнении новой установки Azure AD Connect выберите hello [пользовательский путь установки](active-directory-aadconnect-get-started-custom.md). На странице «Вход пользователей» hello установите флажок «Включить единый вход» hello.

![Azure AD Connect: страница "Вход пользователя"](./media/active-directory-aadconnect-sso/sso8.png)

Если уже имеется установленный экземпляр Azure AD Connect, выберите страницу "Смена имени пользователя для входа" в Azure AD Connect и нажмите кнопку "Далее". Затем установите флажок «Включить единый вход» hello.

![Azure AD Connect: страница "Смена имени пользователя для входа"](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Продолжайте работу приветствия мастера, пока не будет получен toohello страницы «Включить единый вход». Учетные данные администратора домена для каждого леса AD синхронизации tooAzure AD (с помощью Azure AD Connect) и для пользователей, для которого требуется tooenable прозрачную единого входа. 

После завершения работы мастера hello прозрачную единого входа включена для клиента.

>[!NOTE]
> учетные данные администратора домена Hello не хранятся в Azure AD Connect или в Azure AD, но являются только используемые tooenable функции hello.

Выполните эти инструкции tooverify, правильно включено прямое единого входа.

1. Войдите в toohello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) с hello учетные данные глобального администратора для вашего клиента.
2. Выберите **Azure Active Directory** на левой навигационной hello.
3. Выберите **Azure AD Connect**.
4. Убедитесь, что hello **прозрачную Single Sign-On** показано, как функция **включено**.

![Портал Azure — колонка Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a>Шаг 3: Развертывание функции hello

tooroll hello функция tooyour пользователей необходимо tooadd два Azure AD URL-адреса (https://autologon.microsoftazuread-sso.com и https://aadg.windows.net.nsatc.net) toousers настроек зоны посредством групповой политики в Active Directory.

>[!NOTE]
> Здравствуйте, следующие инструкции работают, только для Internet Explorer и Google Chrome в Windows (если он использует набор URL-адресов в список надежных узлов с Internet Explorer). Чтение hello следующего раздела приведены инструкции tooset Mozilla Firefox и Google Chrome на Mac.

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a>Зачем нужен настроек зоны toomodify пользователей?

По умолчанию hello браузер автоматически вычисляет hello правой зоны (Интернет или интрасеть) с URL-адреса. Например http://contoso/ является сопоставленных toohello интрасеть, тогда как http://intranet.contoso.com/ находится сопоставленных toohello зоны Интернета (hello URL-адрес содержит точку). Браузеры не отправлять конечную точку облака билеты Kerberos с tooa - как hello двух Azure AD URL - Если явно добавлен зоны интрасети toohello браузера его URL-адрес.

### <a name="detailed-steps"></a>Подробные инструкции

1. Откройте средство управления групповой политикой hello.
2. Измените hello групповой политики, примененные toosome или всех пользователей. В этом примере мы используем hello **политика домена по умолчанию**.
3. Перейдите в слишком**пользователя Конфигурация компьютера\Административные шаблоны\Компоненты Components\Internet пользователи управления Panel\Security страницы** и выберите **сайта tooZone список назначений**.
![Единый вход](./media/active-directory-aadconnect-sso/sso6.png)  
4. Включить политику hello и введите следующие значения (Azure AD URL-адреса, которые пересылаются билеты Kerberos) hello и данные (*1* указывает интрасеть) в диалоговое окно «hello».

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> Toodisallow некоторые пользователи из с использованием прозрачную SSO - например, если эти пользователи входят на общей киосках - задайте hello, предшествующий значения слишком*4*. Это действие добавляет toohello URL-адреса Azure AD hello ограниченной зоны и происходит сбой прозрачную единый вход постоянно hello.

5. Нажмите кнопку **ОК**, затем нажмите кнопку **ОК** еще раз.

![Единый вход](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>Рекомендации для браузера

#### <a name="mozilla-firefox"></a>Mozilla Firefox

Mozilla Firefox автоматически не выполняет проверку подлинности Kerberos. Каждый пользователь имеет toomanually добавить hello Azure AD URL-адреса tootheir Firefox параметры с помощью hello следующие шаги:
1. Запустите Firefox и введите `about:config` в адресную строку hello. Проигнорируйте все отображаемые уведомления.
2. Поиск hello **network.negotiate auth.trusted идентификаторы URI** предпочтения. Этот параметр выводит список доверенных сайтов в Firefox для проверки подлинности Kerberos.
3. Щелкните правой кнопкой мыши и выберите "Изменить".
4. Введите «https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net» в поле hello.
5. Нажмите кнопку «ОК» и снова откройте браузер hello.

#### <a name="safari-on-mac-os"></a>Safari в Mac OS

Убедитесь, что этого hello компьютера под управлением Mac OS tooAD присоединены к домену. См. инструкции о том, как toodo, [здесь](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).

#### <a name="google-chrome-on-mac-os"></a>Google Chrome в Mac OS

Google Chrome в Mac OS и других платформах, отличных от Windows, см. в разделе слишком[в этой статье](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) сведения о как toowhitelist hello URL-адреса Azure AD для проверки подлинности.

С помощью групповой политики Active Directory сторонних расширений tooroll tooFirefox hello URL-адреса Azure AD и Google Chrome на пользователям Mac не рассматривается в этой статье.

#### <a name="known-limitations"></a>Известные ограничения

Простой единый вход не работает в конфиденциальном режиме просмотра в браузерах Firefox и Edge, Он также не работает в Internet Explorer, если браузер hello работает в режиме усиленной защиты.

>[!IMPORTANT]
>Мы недавно откат поддержка Edge tooinvestigate устранения проблем клиента.

## <a name="step-4-test-hello-feature"></a>Шаг 4: Тестирование функции hello

функция hello tootest для конкретного пользователя, убедитесь, что _все_ предусмотрены hello следующие условия:
  - вход пользователя Hello на корпоративных устройств.
  - Hello устройства был ранее объединенные tooyour домена Active Directory (AD).
  - Hello устройство имеет прямое подключение tooyour контроллеру домена (DC), hello корпоративной проводной или беспроводной сети или посредством подключения удаленного доступа, таких как VPN-подключения.
  - У вас есть [распространен функции hello](##step-3-roll-out-the-feature) toothis пользователя, с помощью групповой политики.

сценарий tootest hello, где hello пользователь вводит только имя пользователя hello, но не hello пароль.
- Войдите на *https://myapps.microsoft.com/* в новом частном сеансе браузера.

сценарий tootest hello, где hello пользователь не имеет пароля имя пользователя или hello hello tooenter. 
- Войдите на *https://myapps.microsoft.com/contoso.onmicrosoft.com* в новом частном сеансе браузера. Введите вместо "*contoso*" имя своего клиента.
- Или войдите на *https://myapps.microsoft.com/contoso.com* в новом частном сеансе браузера. Введите вместо "*contoso.com*" проверенный домен (не федеративный домен) в клиенте.

## <a name="step-5-roll-over-keys"></a>Шаг 5. Смена ключей

На шаге 2 Azure AD Connect создает учетные записи компьютеров (представляющий Azure AD) во всех лесах hello AD, для которых была включена прозрачную единого входа. Дополнительные сведения см. [здесь](active-directory-aadconnect-sso-how-it-works.md). В целях повышения безопасности рекомендуется, можно часто, наведите курсор на ключи расшифровки Kerberos hello этих учетных записей компьютеров.

>[!IMPORTANT]
>Этот шаг не требуется по toodo _немедленно_ после включения функции hello. Наведите курсор на ключи расшифровки Kerberos hello каждые 30 дней.

## <a name="next-steps"></a>Дальнейшие действия

- [**Техническое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-sso-how-it-works.md). Сведения о том, как работает эта функция.
- [**Часто задаваемые вопросы** ](active-directory-aadconnect-sso-faq.md) -ответы на вопросы и ответы toofrequently.
- [**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-sso.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.
