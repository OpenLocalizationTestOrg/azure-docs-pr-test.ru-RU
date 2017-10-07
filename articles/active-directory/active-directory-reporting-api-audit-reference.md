---
title: "Аудит Active Directory aaaAzure Справочник по API | Документы Microsoft"
description: "Как tooget работу с hello API аудита Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a>Справочник по API аудита Azure Active Directory
Этот раздел является частью коллекции разделов, посвященных hello Azure Active Directory reporting API.  
Отчетами Azure AD предоставляет API, который позволяет tooaccess данные аудита, с помощью кода или связанные средства.
Hello в этом разделе относится tooprovide вам справочные сведения о hello **audit API**.

См.:

* Основные сведения см. в разделе [Журналы аудита](active-directory-reporting-azure-portal.md#activity-reports).

* [Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) Дополнительные сведения о hello reporting API.


Сведения:

- Ответы на вопросы см. в разделе [Часто задаваемые вопросы](active-directory-reporting-faq.md). 

- При возникновении проблем [создайте запрос в службу поддержки](active-directory-troubleshooting-support-howto.md). 


## <a name="who-can-access-hello-data"></a>Кто имеет доступ к данным hello?
* Пользователи с ролью администратора безопасности или безопасность чтения hello
* Глобальные администраторы
* Любое приложение, которое имеет авторизации tooaccess hello API (авторизации приложения может быть установки, только на основе разрешения глобального администратора)

## <a name="prerequisites"></a>Предварительные требования
В порядке tooaccess это подчиненности hello Reporting API, должен иметь:

* установить [Azure Active Directory Free или более поздней версии](active-directory-editions.md)
* Завершенная hello [API отчетов hello Azure AD tooaccess необходимых компонентов](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Доступ к hello API
Этот API можно получить либо через hello [Graph Explorer](https://graphexplorer2.cloudapp.net) или программно, используя, например, PowerShell. В порядке для PowerShell toocorrectly интерпретировать синтаксис фильтра OData hello, используемых при вызове AAD Graph REST необходимо использовать обратный апостроф hello (также называемого: апостроф) символ слишком «escape» символа "$" hello. служит Hello апострофа [escape-символа PowerShell](https://technet.microsoft.com/library/hh847755.aspx), позволяя PowerShell toodo литерала интерпретацию символа $ hello и не путать его как имя переменной PowerShell (ie: $filter).

Hello в этом разделе нацелено на hello Graph Explorer. Пример PowerShell см. в этом [сценарии PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).

## <a name="api-endpoint"></a>Конечная точка API
Вы можете использовать этот API, с помощью hello, следующий URI:  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

Нет ограничений на hello число записей, возвращаемых API аудита hello Azure AD (с помощью OData разбиение на страницы).
Сведения о периоде удержания данных отчетов приведены в статье [Политики периода удержания отчетов](active-directory-reporting-retention.md).

Этот вызов возвращается hello данных в пакетах. В каждом пакете содержится не более 1000 записей.  
tooget hello следующего пакета записей, используйте hello следующей ссылки. Получение сведений токен skiptoken hello из первого набора hello возвращенных записей. в конце hello hello результирующий набор будет токен пропуска Hello.  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a>Поддерживаемые фильтры
Можно сузить hello число записей, возвращаемых API вызова в форме фильтра.  
Для входа в API поддерживаются связанные данные hello следующие фильтры:

* **$top =\<возвращается число записей toobe\>**  -toolimit hello количество возвращаемых записей. Это дорогостоящая операция. Этот фильтр не следует использовать, если требуется, чтобы tooreturn тысяч объектов.     
* **$filter =\<инструкцию фильтра\>**  -toospecify на основе hello поддерживаемый фильтр поля, типа hello записей, важные для вас

## <a name="supported-filter-fields-and-operators"></a>Поддерживаемый поля и операторы фильтров
Тип hello toospecify записей, которые вас интересуют, можно построить инструкцию фильтра, который может содержать один или сочетание hello следующие поля фильтра:

* [activityDate](#activitydate) определяет дату или диапазон дат;
* [Категория](#category) — определяет категорию hello требуются toofilter.
* [activityStatus](#activitystatus) -определяет hello состояние действия
* [Тип действия](#activitytype) -определяет тип hello действия
* [Действие](#activity) -определяет действие hello в виде строки  
* [в имя субъекта](#actorname) -определяет субъект hello в форме имени субъекта hello
* [Субъект/objectid](#actorobjectid) -определяет субъект hello в виде идентификатора субъекта hello   
* [субъект или имя участника-пользователя](#actorupn) -определяет субъект hello в форме hello субъекта имя участника-пользователя (UPN) 
* [Имяцелевого/](#targetname) -определяет целевой hello в форме имени субъекта hello
* [целевой/objectid](#targetobjectid) -определяет цель hello в виде идентификатора целевого hello  
* [целевой/upn](#targetupn) -определяет субъект hello в форме hello субъекта имя участника-пользователя (UPN)   

- - -
### <a name="activitydate"></a>activityDate
**Поддерживаемые операторы**: eq, ge, le, gt, lt

**Пример**:

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

**Примечания**

Время и дата указываются в формате UTC.

- - -
### <a name="category"></a>category

**Поддерживаемые значения**:

| Категория                         | Значение     |
| :--                              | ---       |
| "Core Directory" (Основной каталог);                   | Каталог |
| "Self-service Password Management" (Самостоятельное управление паролями); | SSPR      |
| "Self-service Group Management" (Самостоятельное управление группами);    | SSGM      |
| "Account Provisioning" (Подготовка учетных записей).             | Sync      |
| "Automated Password Rollover" (Автоматическая смена пароля)      | "Automated Password Rollover" (Автоматическая смена пароля) |
| Защита идентификации              | IdentityProtection |
| Invited Users (Приглашаемые пользователи)                    | Invited Users (Приглашаемые пользователи) |
| MIM Service (Служба MIM)                      | MIM Service (Служба MIM) |



**Поддерживаемые операторы**: eq

**Пример**:

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a>activityStatus

**Поддерживаемые значения**:

| Состояние действия | Значение |
| :--             | ---   |
| Успешно         | 0     |
| Сбой         | - 1   |

**Поддерживаемые операторы**: eq

**Пример**:

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a>activityType
**Поддерживаемые операторы**: eq

**Пример**:

    $filter=activityType eq 'User'    

**Примечания**

Учитывает регистр.

- - -
### <a name="activity"></a>activity
**Поддерживаемые операторы**: eq, contains, startsWith

**Пример**:

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

**Примечания**

Учитывает регистр.

- - -
### <a name="actorname"></a>actor/name
**Поддерживаемые операторы**: eq, contains, startsWith

**Пример**:

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

**Примечания**

Не учитывает регистр.

- - -
### <a name="actorobjectid"></a>actor/objectid
**Поддерживаемые операторы**: eq

**Пример**:

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a>target/name
**Поддерживаемые операторы**: eq, contains, startsWith

**Пример**:

    $filter=targets/any(t: t/name eq 'some name')    

**Примечания**

Не учитывает регистр.

- - -
### <a name="targetupn"></a>target/upn
**Поддерживаемые операторы**: eq, startsWith

**Пример**:

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

**Примечания**

* Не учитывает регистр.
* Требуется полное пространство имен hello tooadd при запросе Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity

- - -
### <a name="targetobjectid"></a>target/objectid
**Поддерживаемые операторы**: eq

**Пример**:

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a>actor/upn
**Поддерживаемые операторы**: eq, startsWith

**Пример**:

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

**Примечания**

* Не учитывает регистр. 
* Требуется полное пространство имен hello tooadd при запросе Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity

- - -
## <a name="next-steps"></a>Дальнейшие действия
* Вы хотите toosee примеры для отфильтрованных системных действий? Извлечение hello [примеры аудита API Azure Active Directory](active-directory-reporting-api-audit-samples.md).
* Вы хотите, чтобы tooknow Дополнительные сведения об API отчетов hello Azure AD? В разделе [Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).

