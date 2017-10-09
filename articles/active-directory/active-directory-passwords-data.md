---
title: "Требования к данным для самостоятельного сброса пароля Azure AD | Документация Майкрософт"
description: "Сброс данных требования для самостоятельного пароля Azure AD и как toosatisfy их"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>Развертывание сброса пароля без регистрации пользователя

Развертывание самостоятельного сброса пароля (SSPR) требуется наличие toobe данных проверки подлинности. В некоторых организациях есть их пользователям вводить свои данные проверки подлинности самостоятельно, но многие организации предпочитают toosynchronize с существующие данные в Active Directory. Если имеются правильно отформатированные данные в ваш локальный каталог и настроить [Azure AD Connect, используя стандартные параметры](./connect/active-directory-aadconnect-get-started-express.md), что данных становится доступной tooAzure AD и SSPR, без необходимости участия пользователя.

Все телефонные номера должен быть в формате hello + CountryCode PhoneNumber пример: 4255551234 + 1 toowork должным образом.

> [!NOTE]
> Функция сброса пароля не поддерживает добавочные номера. Даже в формате 12345 hello 4255551234 + 1 X расширения будут удалены перед установкой hello.

## <a name="fields-populated"></a>Заполненные поля

Сопоставление производится, если используются параметры по умолчанию hello в Azure AD Connect hello следующие.

| Локальная служба AD | Azure AD | Контактные данные проверки подлинности Azure AD |
| --- | --- | --- |
| TelephoneNumber | Рабочий телефон | Дополнительный телефон |
| mobile | Мобильный телефон | Номер телефона |


## <a name="security-questions-and-answers"></a>Контрольные вопросы и ответы на них

Вопросы и ответы, надежно сохранены в клиенте Azure AD и являются только доступный toousers через hello [портал регистрации SSPR](https://aka.ms/ssprsetup). Администраторы не может просматривать или изменять содержимое hello другим пользователям вопросов и ответов.

### <a name="what-happens-when-a-user-registers"></a>Что происходит, когда пользователь проходит регистрацию?

Когда пользователь регистрирует, страница регистрации hello задает hello следующие поля:

* Телефон для проверки подлинности
* Адрес электронной почты для проверки подлинности
* Контрольные вопросы и ответы на них

При указании значения для **мобильный телефон** или **запасной адрес электронной почты**, пользователи могут сразу же использовать эти значения tooreset свои пароли, даже если они еще не зарегистрированы для службы hello. Кроме того пользователи см. Эти значения при регистрации для hello впервые и при желании измените их. После успешной регистрации, эти значения будут сохраняться в hello **телефон для аутентификации** и **электронной почты для проверки подлинности** соответственно.

## <a name="set-and-read-authentication-data-using-powershell"></a>Установка и считывание данных аутентификации с помощью PowerShell

Hello следующие поля можно задать с помощью PowerShell

* Запасной адрес электронной почты
* Мобильный телефон
* Рабочий телефон — его можно указать, только если это значение не синхронизируется с локальным каталогом

### <a name="using-powershell-v1"></a>Использование PowerShell V1

tooget работы, необходимо слишком[Загрузите и установите модуль Azure AD PowerShell hello](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule). После его установки, вы можете использовать hello описанных ниже tooconfigure каждого поля.

#### <a name="set-authentication-data-with-powershell-v1"></a>Настройка данных аутентификации с помощью PowerShell V1

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a>Чтение данных аутентификации с помощью PowerShell V1

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a>Телефон для аутентификации и электронной почты для проверки подлинности могут быть прочитаны только с помощью Powershell V1 hello с помощью команды ниже

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>Использование PowerShell V2

tooget работы, необходимо слишком[загрузить и установить модуль PowerShell Azure AD V2 hello](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md). После его установки, вы можете использовать hello описанных ниже tooconfigure каждого поля.

tooinstall быстро из последних версий PowerShell, поддерживающие Install-Module, выполняемых команд (первая строка hello просто проверяет toosee Если уже установлена):

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a>Настройка данных аутентификации с помощью PowerShell V2

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a>Чтение данных аутентификации с помощью PowerShell V2

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a>Дальнейшие действия

Привет, следующие ссылки предоставляют дополнительную информацию об пароль с помощью Azure AD

* [**Быстрое начало работы с самостоятельным сбросом пароля в Azure AD**](active-directory-passwords-getting-started.md). Запуск и выполнение службы самостоятельного управления паролями Azure AD. 
* [**Licensing requirements for Azure AD self-service password reset**](active-directory-passwords-licensing.md) (Требования к лицензированию самостоятельного сброса пароля в Azure AD). Сведения о настройке лицензирования Azure AD.
* [**Развертывание** ](active-directory-passwords-best-practices.md) -планирование и развертывание SSPR tooyour пользователей с помощью hello рекомендации по следующему адресу
* [**Настройка** ](active-directory-passwords-customize.md) -настроить hello внешний вид и поведение hello SSPR взаимодействие с вашей компании.
* [**Политики и ограничения для паролей в Azure Active Directory**](active-directory-passwords-policy.md). Общие сведения и информация об установке политик паролей Azure AD.
* [**Reporting options for Azure AD password management**](active-directory-passwords-reporting.md) (Параметры отчетов для управления паролями Azure AD). Определяйте, кто и когда использовал функцию SSPR.
* [**Технические глубокое погружение** ](active-directory-passwords-how-it-works.md) -перейдите за занавесом toounderstand hello принцип работы
* [**Вопросы и ответы об управлении паролями**](active-directory-passwords-faq.md). Как? Почему? Что? Где? Кто? Когда? -Ответы tooquestions требуется, чтобы tooask
* [**Устранение неполадок** ](active-directory-passwords-troubleshoot.md) -Узнайте, как tooresolve распространенные проблемы, мы увидим с SSPR
