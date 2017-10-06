---
title: "Azure AD Connect: устранение неполадок с простым единым входом | Документы Майкрософт"
description: "В этом разделе описывается способ tootroubleshoot Azure Active Directory прозрачную единого входа (Azure AD, эффективная SSO)."
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
ms.openlocfilehash: f1c1c11522f22d5bc742c126fff483c5b06e1f06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a>Устранение неполадок с простым единым входом Azure Active Directory

Эта статья поможет вам найти информацию по вопросам относительно устранения неполадок с простым единым входом Azure AD.

## <a name="known-issues"></a>Известные проблемы

- При синхронизации 30 лесов AD и более простой единый вход через Azure AD Connect включить невозможно. Чтобы избежать этого, вы можете [вручную включить](#manual-reset-of-azure-ad-seamless-sso) функции hello на клиенте.
- Добавление Azure AD службы URL-адреса (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) toohello «Надежные узлы» зоны вместо зону «Местная интрасеть» hello **блокирует пользователям входить в**.
- Простой единый вход не работает в конфиденциальном режиме просмотра в Firefox и Edge, а также в Internet Explorer при включенном режиме повышенной защиты.

>[!IMPORTANT]
>Мы недавно откат поддержка Edge tooinvestigate устранения проблем клиента.

## <a name="check-status-of-hello-feature"></a>Проверьте состояние функции hello

Убедитесь, этот компонент hello прозрачную единого входа по-прежнему **включено** на клиенте. Можно проверить состояние, будет toohello **Azure AD Connect** колонка на hello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com/).

![Центр администрирования Active Directory Azure — колонка "Azure AD Connect"](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Причины сбоя входа на Центр администрирования Azure Active Directory hello

Хорошая toostart, устранения неполадок пользователя войти с помощью комплексной единого входа является toolook на hello [действия при входе отчетов](../active-directory-reporting-activity-sign-ins.md) на hello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com/).

![Центр администрирования Azure Active Directory — отчет о действиях входа](./media/active-directory-aadconnect-sso/sso9.png)

Перейдите в слишком**Azure Active Directory** -> **входа в систему** на hello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com/) и нажмите кнопку действия при входе определенного пользователя. Найдите hello **входа в код ошибки** поля. Сопоставьте значение hello, причина сбоя tooa поля и разрешение, с помощью hello в следующей таблице:

|Код ошибки входа|Причина ошибки входа|Способы устранения:
| --- | --- | ---
| 81001 | Билет Kerberos пользователя слишком большой. | Сократите список членства пользователя в группах и повторите попытку.
| 81002 | Не удается toovalidate пользователя билета Kerberos. | См. [Контрольный список по устранению неполадок](#troubleshooting-checklist).
| 81003 | Не удается toovalidate пользователя билета Kerberos. | См. [Контрольный список по устранению неполадок](#troubleshooting-checklist).
| 81004 | Проверка подлинности Kerberos завершилась сбоем. | См. [Контрольный список по устранению неполадок](#troubleshooting-checklist).
| 81008 | Не удается toovalidate пользователя билета Kerberos. | См. [Контрольный список по устранению неполадок](#troubleshooting-checklist).
| 81009 | «Не удается toovalidate пользователя билета Kerberos. | См. [Контрольный список по устранению неполадок](#troubleshooting-checklist).
| 81010 | Эффективная единого входа не удалось, поскольку пользователь hello билета Kerberos истек или является недопустимым. | Пользователь должен toosign в из устройств, присоединенных к домену, в корпоративной сети.
| 81011 | Не удается toofind объект пользователя, на основе информации из билета Kerberos пользователя hello. | Используйте Azure AD Connect toosynchronize пользовательские данные в Azure AD.
| 81012 | Hello пользователя, пытающегося toosign в tooAzure AD отличается от пользователя hello вход hello устройство. | Войдите с другого устройства.
| 81013 | Не удается toofind объект пользователя, на основе информации из билета Kerberos пользователя hello. |Используйте Azure AD Connect toosynchronize пользовательские данные в Azure AD. 

## <a name="troubleshooting-checklist"></a>Контрольный список по устранению неполадок

Используйте hello следующих ситуаций прозрачную SSO tootroubleshoot контрольный список:

- Проверьте, включена ли возможность эффективной SSO hello в Azure AD Connect. Если не удается включить функцию hello (например, из-за tooa заблокирован порт), проверьте наличие всех hello [предварительным](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) на месте.
- Проверьте, если оба эти Azure AD URL-адреса (https://autologon.microsoftazuread-sso.com и https://aadg.windows.net.nsatc.net) являются частью настроек зоны hello пользователя.
- Убедитесь, что домен toohello присоединены к домену AD hello корпоративных устройств.
- Убедитесь, что hello в любом toohello устройства, с помощью учетной записи домена AD.
- Убедитесь, что учетная запись пользователя hello из леса AD, где было прозрачную единого входа.
- Убедитесь, что устройство hello подключено hello корпоративной сети.
- Убедитесь, что время на устройстве hello синхронизируется с временем hello Active Directory и контроллеров домена hello и находится в пределах пяти минут.
- Список существующих билеты Kerberos на устройстве hello, с помощью hello **klist** команду из командной строки. Проверьте билеты уведомления в случае hello `AZUREADSSOACCT` присутствуют учетной записи компьютера. Билеты Kerberos пользователей обычно действительны в течение 12 часов. В вашем каталоге Active Directory могут быть заданы другие параметры.
- Очистить существующие билеты Kerberos с помощью hello устройства hello **Очистка klist** команды и повторите попытку.
- toodetermine при наличии вопросов, связанных с JavaScript, просмотрите журналы консоли hello hello браузера (в разделе «средства разработчика»).
- Просмотрите hello [контроллер домена регистрирует](#domain-controller-logs) также.

### <a name="domain-controller-logs"></a>Журналы контроллеров домена

Если аудит успешных попыток включен на контроллере домена, затем каждый раз, пользователь выполняет вход с использованием SSO прозрачную запись безопасности записывается в журнал событий hello. Можно найти эти события безопасности с помощью приветствия при следующем запросе (Найдите событие **4769** связанные с учетной записью компьютера hello **AzureADSSOAcc$**):

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-hello-feature"></a>Ручного сброса функции hello

Если разрешение не помогла, можно вручную сбросить функции hello в клиенте. Выполните следующие действия hello на локальном сервере, на котором выполняется Azure AD Connect.

### <a name="step-1-import-hello-seamless-sso-powershell-module"></a>Шаг 1: Импортируйте модуль hello прозрачную PowerShell для единого входа

1. Во-первых, загрузка и установка hello [Microsoft Online Services помощник по входу](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Затем загрузите и установите hello [64-разрядного модуля Azure Active Directory для Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Перейдите toohello `%programfiles%\Microsoft Azure Active Directory Connect` папки.
4. Импорт hello прозрачную PowerShell единого входа модуля с помощью этой команды: `Import-Module .\AzureADSSO.psd1`.

### <a name="step-2-get-hello-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a>Шаг 2: Получение списка hello лесов AD, для которых включен прозрачную единого входа

1. Запустите PowerShell от имени администратора. В PowerShell вызовите `New-AzureADSSOAuthenticationContext`. При запросе введите свои учетные данные глобального администратора клиента.
2. Вызовите `Get-AzureADSSOStatus`. Эта команда предоставляет Здравствуйте списке лесов AD (см. список доменов «hello»), на которых включена эта функция.

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a>Шаг 3. Отключите простой единый вход для каждого леса AD, где он был настроен

1. Вызовите `$creds = Get-Credential`. При появлении запроса введите учетные данные администратора домена hello hello предназначен леса AD.
2. Вызовите `Disable-AzureADSSOForest -OnPremCredentials $creds`. Эта команда удаляет hello `AZUREADSSOACCT` учетную запись компьютера в hello локального контроллера домена для данного конкретного леса AD.
3. Повторите предыдущих шагах для каждого леса AD, вы настроили функции hello на hello.

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a>Шаг 4. Включение простого единого входа для каждого леса AD

1. Вызовите `Enable-AzureADSSOForest`. При появлении запроса введите учетные данные администратора домена hello hello предназначен леса AD.
2. Повторите hello предыдущих шагах для каждого леса AD нужного tooset копирование функции hello.

### <a name="step-5-enable-hello-feature-on-your-tenant"></a>Шаг 5. Включить функцию hello на клиенте

Вызовите `Enable-AzureADSSO` и введите «true» в hello `Enable: ` prompt tooturn функцию hello в клиенте.
