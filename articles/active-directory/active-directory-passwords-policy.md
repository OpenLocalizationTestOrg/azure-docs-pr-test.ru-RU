---
title: "Политика: Azure AD SSPR | Документация Майкрософт"
description: "Параметры политики самостоятельного сброса пароля в Azure AD"
services: active-directory
keywords: "Управление паролями Active Directory, управление паролями, самостоятельный сброс пароля Azure AD"
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
ms.openlocfilehash: af7cb13794bf3a9fee91d355f788aa5c2246e57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a>Политики и ограничения для паролей в Azure Active Directory

В этой статье описываются политики паролей hello и требования к сложности, связанные с учетными записями пользователей, хранящимися в клиенте Azure AD.

## <a name="administrator-password-policy-differences"></a>Различия политики паролей администратора

Корпорация Майкрософт применяет строгую **двухступенчатую** политику сброса паролей по умолчанию для любой роли администратора Azure (например, роли глобального администратора, администратора службы технической поддержки, администратора паролей и т. д.).

Это отключит администраторов с помощью контрольных вопросов и обеспечивает выполнение следующих hello.

Два шлюза политики, требующие два блока данных проверки подлинности (адрес электронной почты **и** номер телефона), применяется в следующих обстоятельствах hello

* Все роли администратора в Azure
  * Администратор службы технической поддержки
  * Администратор службы поддержки
  * администратора выставления счетов; 
  * Служба поддержка партнеров уровня 1
  * Служба поддержка партнеров уровня 2
  * Администратор службы Exchange
  * Администратор службы Lync
  * Администратор учетных записей
  * Создатели каталогов
  * Глобальный или корпоративный администратор
  * Администратор службы SharePoint
  * Администратор соответствия требованиям
  * Администратор приложений
  * Администратор безопасности
  * Администратор привилегированных ролей
  * Администратор службы Intune
  * Администратор прокси-сервера приложений
  * Администратор службы CRM
  * Администратор службы Power BI
  
* 30 **дней** с момента установки пробной версии истекло;
* **при** наличии личного домена;
* Azure AD Connect выполняет синхронизацию удостоверений из вашего локального каталога.

### <a name="exceptions"></a>Исключения
Одна политика вентиля, требующие один фрагмент данных проверки подлинности (адрес электронной почты **или** номер телефона), применяется в следующих обстоятельствах hello

* первые 30 **дней** пробной версии;
* отсутствие личного домена (*.onmicrosoft.com) **и** если в Azure AD Connect не выполняется синхронизация удостоверений.


## <a name="userprincipalname-policies-that-apply-tooall-user-accounts"></a>Политики UserPrincipalName, которые применяются tooall учетных записей пользователей

Каждой учетной записи пользователя, который должен toosign в tooAzure AD должен иметь значение атрибута имя участника (UPN) пользователя, связанный с учетной записью. Таблица Hello под структуры hello политик, применить tooboth локальной синхронизированную облака toohello и toocloud только для учетных записей пользователей Active Directory.

| Свойство | Требования UserPrincipalName |
| --- | --- |
| Допустимые символы |<ul> <li>A–Z</li> <li>a–z</li><li>0–9</li> <li> . - \_ ! \# ^ \~</li></ul> |
| Недопустимые символы |<ul> <li>Любой "@" символ, который не является отделение hello имя пользователя из домена hello.</li> <li>Не может содержать символ точки "." ближайший предшествующий hello ' @' символ</li></ul> |
| Ограничения длины |<ul> <li>Общая длина не должна превышать 113 знаков</li><li>64 знака до hello ' @' символ</li><li>48 знаков после hello ' @' символ</li></ul> |

## <a name="password-policies-that-apply-only-toocloud-user-accounts"></a>Политики паролей, которые применяются только учетные записи пользователей toocloud

Привет, в следующей таблице описываются hello доступные параметры политики паролей, может быть применен toouser учетные записи, которые создаются и управляются в Azure AD.

| Свойство | Требования |
| --- | --- |
| Допустимые символы |<ul><li>A–Z</li><li>a–z</li><li>0–9</li> <li>@ # $ % ^ & * - _ ! + = [ ] { } &#124; \ : ‘ , . ? / ` ~ “ ( ) ;</li></ul> |
| Недопустимые символы |<ul><li>Символы Юникода</li><li>Пробелы</li><li> **Только надежные пароли**: не может содержать символ точки "." ближайший предшествующий hello ' @' символ</li></ul> |
| Ограничения для пароля |<ul><li>Минимум 8 символов, максимум 16 символов</li><li>**Только надежные пароли**: требуется 3 из 4 hello следующее:<ul><li>Строчные буквы</li><li>Прописные буквы</li><li>Числа (0–9)</li><li>Символы (см. ограничения для пароля выше)</li></ul></li></ul> |
| Длительность срока действия пароля |<ul><li>Значение по умолчанию: **90** дней </li><li>Значение задается с помощью командлета Set-MsolPasswordPolicy hello из hello Azure Active Directory модуля для Windows PowerShell.</li></ul> |
| Уведомление об окончании срока действия пароля |<ul><li>Значение по умолчанию: **14** дней (до истечения срока действия пароля)</li><li>Значение задается с помощью командлета Set-MsolPasswordPolicy hello.</li></ul> |
| Окончание срока действия пароля |<ul><li>Значение по умолчанию: **false** дней (означает, что включен срок действия пароля) </li><li>Значение можно настроить для отдельных учетных записей пользователей с помощью командлета Set-MsolUser hello. </li></ul> |
| Журнал **изменения** пароля |Последний пароль **невозможно** использовать повторно при **изменении** пароля. |
| Журнал **сброса** пароля | Последний пароль **можно** использовать повторно при **сбросе** забытого пароля. |
| Блокировка учетной записи |После 10 неудачной попытки входа в (неверный пароль) hello пользователя будет заблокирована на одну минуту. Дополнительно неправильные попытки входа блокировка пользователя hello для увеличения длительности. |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a>Установка политик срока действия пароля в Azure Active Directory

Глобальный администратор для облачной службы Майкрософт можно использовать tooset Microsoft Azure Active Directory модуля для Windows PowerShell hello бессрочных паролей не tooexpire. Также можно использовать Windows PowerShell, командлеты tooremove hello Бессрочные конфигурации или toosee tooexpire не настроены какие пароли пользователей. Это руководство применяется tooother поставщиков, например Microsoft Intune и Office 365, которые также основаны на Microsoft Azure Active Directory для службы удостоверений и каталогов.

> [!NOTE]
> Только пароли для учетных записей пользователей, которые не синхронизируются с помощью синхронизации службы каталогов можно настроить toonot срока действия. Дополнительные сведения о синхронизации каталогов см. в статье [Приступая к работе с Azure AD Connect с использованием стандартных параметров](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).
>
>

## <a name="set-or-check-password-policies-using-powershell"></a>Задание и проверка политик пароля с помощью PowerShell

tooget работы, необходимо слишком[Загрузите и установите модуль Azure AD PowerShell hello](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0). После его установки, можно выполнить действия hello ниже tooconfigure каждого поля.

### <a name="how-toocheck-expiration-policy-for-a-password"></a>Как toocheck политику истечения срока действия пароля
1. Подключите tooWindows PowerShell с использованием учетных данных администратора.
2. Выполните одну из следующих команд hello.

   * toosee ли пароль отдельного пользователя имеет значение toonever срока действия, запустите следующий командлет с помощью hello имя участника-пользователя (UPN) hello (например, aprilr@contoso.onmicrosoft.com) или идентификатор пользователя hello hello пользователя требуется toocheck:`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`
   * toosee hello параметр «Срок действия пароля не ограничен» для всех пользователей, запустите следующий командлет hello:`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`

### <a name="set-a-password-tooexpire"></a>Задать tooexpire пароль

1. Подключите tooWindows PowerShell с использованием учетных данных администратора.
2. Выполните одну из следующих команд hello.

   * tooset hello пароль одного пользователя, чтобы hello действия пароля истек, выполните следующий командлет с помощью hello имя участника-пользователя (UPN) hello или hello идентификатор пользователя hello:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`
   * tooset hello паролей всех пользователей в организации hello, чтобы их срока действия использовать hello, выполнив командлет:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`

### <a name="set-a-password-toonever-expire"></a>Срок действия набора toonever пароль

1. Подключите tooWindows PowerShell с использованием учетных данных администратора.
2. Выполните одну из следующих команд hello.

   * пароль hello tooset toonever одного пользователя истекает, запустите следующий командлет с помощью hello имя участника-пользователя (UPN) hello или hello идентификатор hello пользователя:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`
   * tooset hello пароли всех пользователей hello в toonever организации имеют срок действия, запустите следующий командлет hello:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`

## <a name="next-steps"></a>Дальнейшие действия

Привет, следующие ссылки предоставляют дополнительную информацию об пароль с помощью Azure AD

* [**Быстрое начало работы с самостоятельным сбросом пароля в Azure AD**](active-directory-passwords-getting-started.md). Запуск и выполнение службы самостоятельного управления паролями Azure AD. 
* [**Licensing requirements for Azure AD self-service password reset**](active-directory-passwords-licensing.md) (Требования к лицензированию самостоятельного сброса пароля в Azure AD). Сведения о настройке лицензирования Azure AD.
* [**Данные** ](active-directory-passwords-data.md) — понять hello данные, которые не требуется и как она используется для управления паролями
* [**Развертывание** ](active-directory-passwords-best-practices.md) -планирование и развертывание SSPR tooyour пользователей с помощью hello рекомендации по следующему адресу
* [**Настройка** ](active-directory-passwords-customize.md) -настроить hello внешний вид и поведение hello SSPR взаимодействие с вашей компании.
* [**Reporting options for Azure AD password management**](active-directory-passwords-reporting.md) (Параметры отчетов для управления паролями Azure AD). Определяйте, кто и когда использовал функцию SSPR.
* [**Технические глубокое погружение** ](active-directory-passwords-how-it-works.md) -перейдите за занавесом toounderstand hello принцип работы
* [**Вопросы и ответы об управлении паролями**](active-directory-passwords-faq.md). Как? Почему? Что? Где? Кто? Когда? -Ответы tooquestions требуется, чтобы tooask
* [**Устранение неполадок** ](active-directory-passwords-troubleshoot.md) -Узнайте, как tooresolve распространенные проблемы, мы увидим с SSPR
