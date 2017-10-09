---
title: "Azure AD Connect: простой единый вход — часто задаваемые вопросы | Документы Майкрософт"
description: "Ответы toofrequently вопросы и ответы о Azure Active Directory прозрачную единого входа."
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Часто задаваемые вопросы о простом едином входе Azure Active Directory

В этой статье представлены часто задаваемые вопросы о простом едином входе Azure Active Directory. Следите за новым содержимым.

>[!IMPORTANT]
>компонент Hello прозрачную единого входа в настоящий момент в режиме предварительного просмотра.

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>С какими методами входа работает простой единый вход?

Эффективная единого входа может сочетаться с либо hello [синхронизация хэшей паролей](active-directory-aadconnectsync-implement-password-synchronization.md) или [сквозная проверка подлинности](active-directory-aadconnect-pass-through-authentication.md) входа в методы. Однако эту функцию нельзя использовать со службами федерации Active Directory (AD FS).

## <a name="is-seamless-sso-a-free-feature"></a>Простой единый вход — это бесплатная функция?

Эффективная ЕДИНЫЙ — это бесплатная функция и не нужны все платных выпусков toouse Azure AD его. Он остается свободного после выхода общедоступной функции hello.

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>Какие приложения используют возможность параметра `domain_hint` или `login_hint` простого единого входа?

Не в процессе компиляции hello список приложений, которые отправляют эти параметры и hello те, которые не hello. Если у вас есть приложения, которых интересует, свяжитесь с нами в разделе комментариев hello.

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Поддерживает прямое SSO `Alternate ID` как hello имя пользователя, а не `userPrincipalName`?

Да. Поддерживает прозрачную SSO `Alternate ID` как hello имя пользователя при настройке в Azure AD Connect, как показано [здесь](active-directory-aadconnect-get-started-custom.md). Не все приложения Office 365 поддерживают `Alternate ID`. См. в документации toohello конкретного приложения для поддержки инструкции hello.

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>Я хочу tooregister устройств Windows 10 с Azure AD, без использования AD FS. Можно вместо этого использовать простой единый вход?

Да, этот сценарий требуется версия 2.1 или более поздней hello [клиента к рабочему месту](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a>Как можно меня, наведите курсор на ключ расшифровки Kerberos hello hello `AZUREADSSOACCT` учетной записи компьютера?

Очень важно toofrequently, наведите курсор на ключ расшифровки Kerberos hello hello `AZUREADSSOACCT` учетная запись компьютера (представляющий Azure AD) в локальном лесу AD.

>[!IMPORTANT]
>Корпорация Майкрософт рекомендует, вы, наведите курсор на ключ расшифровки Kerberos hello каждые 30 дней.

Выполните следующие действия hello на локальном сервере, на котором выполняется Azure AD Connect.

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Шаг 1. Получение списка лесов AD, где включен простой единый вход

1. Во-первых, загрузка и установка hello [Microsoft Online Services помощник по входу](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Затем загрузите и установите hello [64-разрядного модуля Azure Active Directory для Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Перейдите toohello `%programfiles%\Microsoft Azure Active Directory Connect` папки.
4. Импорт hello прозрачную PowerShell единого входа модуля с помощью этой команды: `Import-Module .\AzureADSSO.psd1`.
5. Откройте PowerShell от имени администратора. В PowerShell вызовите `New-AzureADSSOAuthenticationContext`. Эта команда позволяет tooenter всплывающее окно учетные данные глобального администратора вашего клиента.
6. Вызовите `Get-AzureADSSOStatus`. Эта команда предоставляет Здравствуйте списке лесов AD (см. список доменов «hello»), на которых включена эта функция.

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>Шаг 2. Обновить ключ расшифровки Kerberos hello в каждом лесу, он был установлен на

1. Вызовите `$creds = Get-Credential`. При появлении запроса введите учетные данные администратора домена hello hello предназначен леса AD.
2. Вызовите `Update-AzureADSSOForest -OnPremCredentials $creds`. Эта команда обновления hello ключ расшифровки Kerberos для hello `AZUREADSSOACCT` учетной записи компьютера в этом леса AD и обновляет его в Azure AD.
3. Повторите предыдущих шагах для каждого леса AD, вы настроили функции hello на hello.

>[!IMPORTANT]
>Убедитесь, которую _не_ запуска hello `Update-AzureADSSOForest` команды несколько раз. В противном случае функция hello прекращает работать до времени hello билеты Kerberos пользователей срок действия и переиздать с вашей локальной Active Directory.

## <a name="how-can-i-disable-seamless-sso"></a>Как отключить простой единый вход?

Простой единый вход можно отключить с помощью Azure AD Connect.

Запустите Azure AD Connect, выберите "Смена имени пользователя для входа" и щелкните "Далее". Затем снимите флажок «Включить единый вход» hello. Продолжайте работу мастера hello. После завершения работы мастера hello прозрачную единого входа отключена на клиенте.

Тем не менее вы увидите на экране следующее сообщение:

«Единый вход отключен, но существуют дополнительные действия вручную tooperform в порядке toocomplete очистки. Подробнее".

toocomplete Здравствуйте процесса, выполните следующие вручную действия hello на локальном сервере, в котором выполняется Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Шаг 1. Получение списка лесов AD, где включен простой единый вход

1. Во-первых, загрузка и установка hello [Microsoft Online Services помощник по входу](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Затем загрузите и установите hello [64-разрядного модуля Azure Active Directory для Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Перейдите toohello `%programfiles%\Microsoft Azure Active Directory Connect` папки.
4. Импорт hello прозрачную PowerShell единого входа модуля с помощью этой команды: `Import-Module .\AzureADSSO.psd1`.
5. Откройте PowerShell от имени администратора. В PowerShell вызовите `New-AzureADSSOAuthenticationContext`. Эта команда позволяет tooenter всплывающее окно учетные данные глобального администратора вашего клиента.
6. Вызовите `Get-AzureADSSOStatus`. Эта команда предоставляет Здравствуйте списке лесов AD (см. список доменов «hello»), на которых включена эта функция.

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>Шаг 2. Вручную удалите hello `AZUREADSSOACCT` учетную запись компьютера в каждом лесу, которое будет отображаться в списке.

## <a name="next-steps"></a>Дальнейшие действия

- [**Краткое руководство**](active-directory-aadconnect-sso-quick-start.md). Настройка и подготовка к работе простого единого входа Azure AD.
- [**Техническое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-sso-how-it-works.md). Сведения о том, как работает эта функция.
- [**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-sso.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.
