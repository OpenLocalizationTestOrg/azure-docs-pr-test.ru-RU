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
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="90ad3-103">Справочник по API отчета о действиях при входе Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90ad3-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="90ad3-104">Этот раздел является частью коллекции разделов, посвященных hello Azure Active Directory reporting API.</span><span class="sxs-lookup"><span data-stu-id="90ad3-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="90ad3-105">Отчетами Azure AD предоставляет API, который позволяет tooaccess данных отчета на действия при входе с помощью кода или связанные средства.</span><span class="sxs-lookup"><span data-stu-id="90ad3-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="90ad3-106">Hello в этом разделе относится tooprovide вам справочные сведения о hello **входа в API действия отчета**.</span><span class="sxs-lookup"><span data-stu-id="90ad3-106">hello scope of this topic is tooprovide you with reference information about hello **sign-in activity report API**.</span></span>

<span data-ttu-id="90ad3-107">См.:</span><span class="sxs-lookup"><span data-stu-id="90ad3-107">See:</span></span>

* <span data-ttu-id="90ad3-108">Основные сведения см. в разделе [Действия при входе](active-directory-reporting-azure-portal.md#activity-reports).</span><span class="sxs-lookup"><span data-stu-id="90ad3-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="90ad3-109">[Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) Дополнительные сведения о hello reporting API.</span><span class="sxs-lookup"><span data-stu-id="90ad3-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="who-can-access-hello-api-data"></a><span data-ttu-id="90ad3-110">Кто имеет доступ к данным API hello?</span><span class="sxs-lookup"><span data-stu-id="90ad3-110">Who can access hello API data?</span></span>
* <span data-ttu-id="90ad3-111">Пользователи и участники службы роли администратора безопасности или безопасность чтения hello</span><span class="sxs-lookup"><span data-stu-id="90ad3-111">Users and Service Principals in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="90ad3-112">Глобальные администраторы</span><span class="sxs-lookup"><span data-stu-id="90ad3-112">Global Admins</span></span>
* <span data-ttu-id="90ad3-113">Любое приложение, которое имеет авторизации tooaccess hello API (авторизации приложения может быть установки, только на основе разрешения глобального администратора)</span><span class="sxs-lookup"><span data-stu-id="90ad3-113">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="90ad3-114">доступ к tooconfigure для tooaccess безопасности приложения API-интерфейсы таких как события входа hello используйте следующие приложения hello tooadd PowerShell участника-службы в роль безопасности чтения hello</span><span class="sxs-lookup"><span data-stu-id="90ad3-114">tooconfigure access for an application tooaccess security APIs such as signin events, use hello following PowerShell tooadd hello applications Service Principal into hello Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="90ad3-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="90ad3-115">Prerequisites</span></span>
<span data-ttu-id="90ad3-116">Это подчиненности tooaccess hello отчетов API, должен иметь:</span><span class="sxs-lookup"><span data-stu-id="90ad3-116">tooaccess this report through hello reporting API, you must have:</span></span>

* <span data-ttu-id="90ad3-117">установить [Azure Active Directory Premium P1 или P2](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="90ad3-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="90ad3-118">Завершенная hello [API отчетов hello Azure AD tooaccess необходимых компонентов](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="90ad3-118">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="90ad3-119">Доступ к hello API</span><span class="sxs-lookup"><span data-stu-id="90ad3-119">Accessing hello API</span></span>
<span data-ttu-id="90ad3-120">Этот API можно получить либо через hello [Graph Explorer](https://graphexplorer2.cloudapp.net) или программно, используя, например, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90ad3-120">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="90ad3-121">В порядке для PowerShell toocorrectly интерпретировать синтаксис фильтра OData hello, используемых при вызове AAD Graph REST необходимо использовать обратный апостроф hello (также называемого: апостроф) символ слишком «escape» символа "$" hello.</span><span class="sxs-lookup"><span data-stu-id="90ad3-121">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="90ad3-122">служит Hello апострофа [escape-символа PowerShell](https://technet.microsoft.com/library/hh847755.aspx), позволяя PowerShell toodo литерала интерпретацию символа $ hello и не путать его как имя переменной PowerShell (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="90ad3-122">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="90ad3-123">Hello в этом разделе нацелено на hello Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="90ad3-123">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="90ad3-124">Пример PowerShell см. в этом [сценарии PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="90ad3-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="90ad3-125">Конечная точка API</span><span class="sxs-lookup"><span data-stu-id="90ad3-125">API Endpoint</span></span>
<span data-ttu-id="90ad3-126">Вы можете использовать этот API, с помощью hello следующий базовый URI:</span><span class="sxs-lookup"><span data-stu-id="90ad3-126">You can access this API using hello following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="90ad3-127">Этот API из-за toohello объем данных ограничен миллиона возвращенных записей.</span><span class="sxs-lookup"><span data-stu-id="90ad3-127">Due toohello volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="90ad3-128">Этот вызов возвращается hello данных в пакетах.</span><span class="sxs-lookup"><span data-stu-id="90ad3-128">This call returns hello data in batches.</span></span> <span data-ttu-id="90ad3-129">В каждом пакете содержится не более 1000 записей.</span><span class="sxs-lookup"><span data-stu-id="90ad3-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="90ad3-130">tooget hello следующего пакета записей, используйте hello следующей ссылки.</span><span class="sxs-lookup"><span data-stu-id="90ad3-130">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="90ad3-131">Получить hello [токен skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) сведения из первого набора hello возвращенных записей.</span><span class="sxs-lookup"><span data-stu-id="90ad3-131">Get hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from hello first set of returned records.</span></span> <span data-ttu-id="90ad3-132">в конце hello hello результирующий набор будет токен пропуска Hello.</span><span class="sxs-lookup"><span data-stu-id="90ad3-132">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="90ad3-133">Поддерживаемые фильтры</span><span class="sxs-lookup"><span data-stu-id="90ad3-133">Supported filters</span></span>
<span data-ttu-id="90ad3-134">Можно сузить hello число записей, возвращаемых API вызова в форме фильтра.</span><span class="sxs-lookup"><span data-stu-id="90ad3-134">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="90ad3-135">Для входа в API поддерживаются связанные данные hello следующие фильтры:</span><span class="sxs-lookup"><span data-stu-id="90ad3-135">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="90ad3-136">**$top =\<возвращается число записей toobe\>**  -toolimit hello количество возвращаемых записей.</span><span class="sxs-lookup"><span data-stu-id="90ad3-136">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="90ad3-137">Это дорогостоящая операция.</span><span class="sxs-lookup"><span data-stu-id="90ad3-137">This is an expensive operation.</span></span> <span data-ttu-id="90ad3-138">Этот фильтр не следует использовать, если требуется, чтобы tooreturn тысяч объектов.</span><span class="sxs-lookup"><span data-stu-id="90ad3-138">You should not use this filter if you want tooreturn thousands of objects.</span></span>  
* <span data-ttu-id="90ad3-139">**$filter =\<инструкцию фильтра\>**  -toospecify на основе hello поддерживаемый фильтр поля, типа hello записей, важные для вас</span><span class="sxs-lookup"><span data-stu-id="90ad3-139">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="90ad3-140">Поддерживаемый поля и операторы фильтров</span><span class="sxs-lookup"><span data-stu-id="90ad3-140">Supported filter fields and operators</span></span>
<span data-ttu-id="90ad3-141">Тип hello toospecify записей, которые вас интересуют, можно построить инструкцию фильтра, который может содержать один или сочетание hello следующие поля фильтра:</span><span class="sxs-lookup"><span data-stu-id="90ad3-141">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="90ad3-142">[signinDateTime](#signindatetime) определяет дату или диапазон дат;</span><span class="sxs-lookup"><span data-stu-id="90ad3-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="90ad3-143">[userId](#userid) -определяет идентификатор пользователя hello на основе определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="90ad3-143">[userId](#userid) - defines a specific user based hello user's ID.</span></span>
* <span data-ttu-id="90ad3-144">[userPrincipalName](#userprincipalname) -определяет пользователя hello конкретного пользователя на основе имя участника-пользователя (UPN)</span><span class="sxs-lookup"><span data-stu-id="90ad3-144">[userPrincipalName](#userprincipalname) - defines a specific user based hello user's user principal name (UPN)</span></span>
* <span data-ttu-id="90ad3-145">[appId](#appid) -определяет идентификатор приложения hello конкретного приложения на основе</span><span class="sxs-lookup"><span data-stu-id="90ad3-145">[appId](#appid) - defines a specific app based hello app's ID</span></span>
* <span data-ttu-id="90ad3-146">[appDisplayName](#appdisplayname) -определяет приложение hello конкретного приложения на основе отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="90ad3-146">[appDisplayName](#appdisplayname) - defines a specific app based hello app's display name</span></span>
* <span data-ttu-id="90ad3-147">[loginStatus](#loginStatus) -определяет состояние hello приветствия имен входа (успех или сбой)</span><span class="sxs-lookup"><span data-stu-id="90ad3-147">[loginStatus](#loginStatus) - defines hello status of hello logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="90ad3-148">При использовании Graph Explorer, вы hello должны toouse hello правильный вариант для каждой буквы является полей фильтра.</span><span class="sxs-lookup"><span data-stu-id="90ad3-148">When using Graph Explorer, you hello need toouse hello correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="90ad3-149">toonarrow вниз область hello hello вернул данные, можно создать сочетание hello поддерживается фильтры и поля фильтра.</span><span class="sxs-lookup"><span data-stu-id="90ad3-149">toonarrow down hello scope of hello returned data, you can build combinations of hello supported filters and filter fields.</span></span> <span data-ttu-id="90ad3-150">Например, hello следующая инструкция возвращает hello top 10 записей между 1 июля 2016 г. и 6 июля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="90ad3-150">For example, hello following statement returns hello top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="90ad3-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="90ad3-151">signinDateTime</span></span>
<span data-ttu-id="90ad3-152">**Поддерживаемые операторы**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="90ad3-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="90ad3-153">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="90ad3-153">**Example**:</span></span>

<span data-ttu-id="90ad3-154">Использование определенной даты</span><span class="sxs-lookup"><span data-stu-id="90ad3-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="90ad3-155">Использование диапазона дат</span><span class="sxs-lookup"><span data-stu-id="90ad3-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="90ad3-156">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="90ad3-156">**Notes**:</span></span>

<span data-ttu-id="90ad3-157">параметр Hello datetime должен быть в формате UTC hello</span><span class="sxs-lookup"><span data-stu-id="90ad3-157">hello datetime parameter should be in hello UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="90ad3-158">userId</span><span class="sxs-lookup"><span data-stu-id="90ad3-158">userId</span></span>
<span data-ttu-id="90ad3-159">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="90ad3-159">**Supported operators**: eq</span></span>

<span data-ttu-id="90ad3-160">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="90ad3-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="90ad3-161">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="90ad3-161">**Notes**:</span></span>

<span data-ttu-id="90ad3-162">значение userId Hello является строковым значением</span><span class="sxs-lookup"><span data-stu-id="90ad3-162">hello value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="90ad3-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="90ad3-163">userPrincipalName</span></span>
<span data-ttu-id="90ad3-164">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="90ad3-164">**Supported operators**: eq</span></span>

<span data-ttu-id="90ad3-165">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="90ad3-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="90ad3-166">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="90ad3-166">**Notes**:</span></span>

<span data-ttu-id="90ad3-167">значение Hello userPrincipalName является строковым значением</span><span class="sxs-lookup"><span data-stu-id="90ad3-167">hello value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="90ad3-168">appId</span><span class="sxs-lookup"><span data-stu-id="90ad3-168">appId</span></span>
<span data-ttu-id="90ad3-169">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="90ad3-169">**Supported operators**: eq</span></span>

<span data-ttu-id="90ad3-170">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="90ad3-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="90ad3-171">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="90ad3-171">**Notes**:</span></span>

<span data-ttu-id="90ad3-172">Hello appId значение строковое значение</span><span class="sxs-lookup"><span data-stu-id="90ad3-172">hello value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="90ad3-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="90ad3-173">appDisplayName</span></span>
<span data-ttu-id="90ad3-174">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="90ad3-174">**Supported operators**: eq</span></span>

<span data-ttu-id="90ad3-175">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="90ad3-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="90ad3-176">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="90ad3-176">**Notes**:</span></span>

<span data-ttu-id="90ad3-177">значение Hello appDisplayName является строковым значением</span><span class="sxs-lookup"><span data-stu-id="90ad3-177">hello value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="90ad3-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="90ad3-178">loginStatus</span></span>
<span data-ttu-id="90ad3-179">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="90ad3-179">**Supported operators**: eq</span></span>

<span data-ttu-id="90ad3-180">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="90ad3-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="90ad3-181">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="90ad3-181">**Notes**:</span></span>

<span data-ttu-id="90ad3-182">Существует два варианта hello loginStatus: 0 — успех, 1 — сбой</span><span class="sxs-lookup"><span data-stu-id="90ad3-182">There are two options for hello loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="90ad3-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="90ad3-183">Next steps</span></span>
* <span data-ttu-id="90ad3-184">Действительно toosee примеры отфильтрованные действия?</span><span class="sxs-lookup"><span data-stu-id="90ad3-184">Do you want toosee examples for filtered sign-in activities?</span></span> <span data-ttu-id="90ad3-185">Извлечение hello [образцы отчетов API действия при входе в Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="90ad3-185">Check out hello [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="90ad3-186">Вы хотите, чтобы tooknow Дополнительные сведения об API отчетов hello Azure AD?</span><span class="sxs-lookup"><span data-stu-id="90ad3-186">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="90ad3-187">В разделе [Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="90ad3-187">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

