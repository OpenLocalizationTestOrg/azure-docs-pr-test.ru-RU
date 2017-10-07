---
title: "отчет о действиях aaaAzure входа в Active Directory Справочник по API | Документы Microsoft"
description: "Ссылка для отчета об активности hello входа в Azure Active Directory API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a>Справочник по API отчета о действиях при входе Azure Active Directory
Этот раздел является частью коллекции разделов, посвященных hello Azure Active Directory reporting API.  
Отчетами Azure AD предоставляет API, который позволяет tooaccess данных отчета на действия при входе с помощью кода или связанные средства.
Hello в этом разделе относится tooprovide вам справочные сведения о hello **входа в API действия отчета**.

См.:

* Основные сведения см. в разделе [Действия при входе](active-directory-reporting-azure-portal.md#activity-reports).
* [Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) Дополнительные сведения о hello reporting API.


## <a name="who-can-access-hello-api-data"></a>Кто имеет доступ к данным API hello?
* Пользователи и участники службы роли администратора безопасности или безопасность чтения hello
* Глобальные администраторы
* Любое приложение, которое имеет авторизации tooaccess hello API (авторизации приложения может быть установки, только на основе разрешения глобального администратора)

доступ к tooconfigure для tooaccess безопасности приложения API-интерфейсы таких как события входа hello используйте следующие приложения hello tooadd PowerShell участника-службы в роль безопасности чтения hello

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a>Предварительные требования
Это подчиненности tooaccess hello отчетов API, должен иметь:

* установить [Azure Active Directory Premium P1 или P2](active-directory-editions.md)
* Завершенная hello [API отчетов hello Azure AD tooaccess необходимых компонентов](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Доступ к hello API
Этот API можно получить либо через hello [Graph Explorer](https://graphexplorer2.cloudapp.net) или программно, используя, например, PowerShell. В порядке для PowerShell toocorrectly интерпретировать синтаксис фильтра OData hello, используемых при вызове AAD Graph REST необходимо использовать обратный апостроф hello (также называемого: апостроф) символ слишком «escape» символа "$" hello. служит Hello апострофа [escape-символа PowerShell](https://technet.microsoft.com/library/hh847755.aspx), позволяя PowerShell toodo литерала интерпретацию символа $ hello и не путать его как имя переменной PowerShell (ie: $filter).

Hello в этом разделе нацелено на hello Graph Explorer. Пример PowerShell см. в этом [сценарии PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).

## <a name="api-endpoint"></a>Конечная точка API
Вы можете использовать этот API, с помощью hello следующий базовый URI:  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



Этот API из-за toohello объем данных ограничен миллиона возвращенных записей. 

Этот вызов возвращается hello данных в пакетах. В каждом пакете содержится не более 1000 записей.  
tooget hello следующего пакета записей, используйте hello следующей ссылки. Получить hello [токен skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) сведения из первого набора hello возвращенных записей. в конце hello hello результирующий набор будет токен пропуска Hello.  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a>Поддерживаемые фильтры
Можно сузить hello число записей, возвращаемых API вызова в форме фильтра.  
Для входа в API поддерживаются связанные данные hello следующие фильтры:

* **$top =\<возвращается число записей toobe\>**  -toolimit hello количество возвращаемых записей. Это дорогостоящая операция. Этот фильтр не следует использовать, если требуется, чтобы tooreturn тысяч объектов.  
* **$filter =\<инструкцию фильтра\>**  -toospecify на основе hello поддерживаемый фильтр поля, типа hello записей, важные для вас

## <a name="supported-filter-fields-and-operators"></a>Поддерживаемый поля и операторы фильтров
Тип hello toospecify записей, которые вас интересуют, можно построить инструкцию фильтра, который может содержать один или сочетание hello следующие поля фильтра:

* [signinDateTime](#signindatetime) определяет дату или диапазон дат;
* [userId](#userid) -определяет идентификатор пользователя hello на основе определенного пользователя.
* [userPrincipalName](#userprincipalname) -определяет пользователя hello конкретного пользователя на основе имя участника-пользователя (UPN)
* [appId](#appid) -определяет идентификатор приложения hello конкретного приложения на основе
* [appDisplayName](#appdisplayname) -определяет приложение hello конкретного приложения на основе отображаемое имя
* [loginStatus](#loginStatus) -определяет состояние hello приветствия имен входа (успех или сбой)

> [!NOTE]
> При использовании Graph Explorer, вы hello должны toouse hello правильный вариант для каждой буквы является полей фильтра.
> 
> 

toonarrow вниз область hello hello вернул данные, можно создать сочетание hello поддерживается фильтры и поля фильтра. Например, hello следующая инструкция возвращает hello top 10 записей между 1 июля 2016 г. и 6 июля 2016 г.

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a>signinDateTime
**Поддерживаемые операторы**: eq, ge, le, gt, lt

**Пример**:

Использование определенной даты

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



Использование диапазона дат    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


**Примечания**

параметр Hello datetime должен быть в формате UTC hello 

- - -
### <a name="userid"></a>userId
**Поддерживаемые операторы**: eq

**Пример**:

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

**Примечания**

значение userId Hello является строковым значением

- - -
### <a name="userprincipalname"></a>userPrincipalName
**Поддерживаемые операторы**: eq

**Пример**:

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


**Примечания**

значение Hello userPrincipalName является строковым значением

- - -
### <a name="appid"></a>appId
**Поддерживаемые операторы**: eq

**Пример**:

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



**Примечания**

Hello appId значение строковое значение

- - -
### <a name="appdisplayname"></a>appDisplayName
**Поддерживаемые операторы**: eq

**Пример**:

    $filter=appDisplayName+eq+'Azure+Portal' 


**Примечания**

значение Hello appDisplayName является строковым значением

- - -
### <a name="loginstatus"></a>loginStatus
**Поддерживаемые операторы**: eq

**Пример**:

    $filter=loginStatus+eq+'1'  


**Примечания**

Существует два варианта hello loginStatus: 0 — успех, 1 — сбой

- - -
## <a name="next-steps"></a>Дальнейшие действия
* Действительно toosee примеры отфильтрованные действия? Извлечение hello [образцы отчетов API действия при входе в Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).
* Вы хотите, чтобы tooknow Дополнительные сведения об API отчетов hello Azure AD? В разделе [Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).

