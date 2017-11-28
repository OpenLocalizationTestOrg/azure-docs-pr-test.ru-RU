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
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="6454e-103">Справочник по API аудита Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6454e-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="6454e-104">Этот раздел является частью коллекции разделов, посвященных hello Azure Active Directory reporting API.</span><span class="sxs-lookup"><span data-stu-id="6454e-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="6454e-105">Отчетами Azure AD предоставляет API, который позволяет tooaccess данные аудита, с помощью кода или связанные средства.</span><span class="sxs-lookup"><span data-stu-id="6454e-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="6454e-106">Hello в этом разделе относится tooprovide вам справочные сведения о hello **audit API**.</span><span class="sxs-lookup"><span data-stu-id="6454e-106">hello scope of this topic is tooprovide you with reference information about hello **audit API**.</span></span>

<span data-ttu-id="6454e-107">См.:</span><span class="sxs-lookup"><span data-stu-id="6454e-107">See:</span></span>

* <span data-ttu-id="6454e-108">Основные сведения см. в разделе [Журналы аудита](active-directory-reporting-azure-portal.md#activity-reports).</span><span class="sxs-lookup"><span data-stu-id="6454e-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="6454e-109">[Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) Дополнительные сведения о hello reporting API.</span><span class="sxs-lookup"><span data-stu-id="6454e-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


<span data-ttu-id="6454e-110">Сведения:</span><span class="sxs-lookup"><span data-stu-id="6454e-110">For:</span></span>

- <span data-ttu-id="6454e-111">Ответы на вопросы см. в разделе [Часто задаваемые вопросы](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="6454e-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="6454e-112">При возникновении проблем [создайте запрос в службу поддержки](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="6454e-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-hello-data"></a><span data-ttu-id="6454e-113">Кто имеет доступ к данным hello?</span><span class="sxs-lookup"><span data-stu-id="6454e-113">Who can access hello data?</span></span>
* <span data-ttu-id="6454e-114">Пользователи с ролью администратора безопасности или безопасность чтения hello</span><span class="sxs-lookup"><span data-stu-id="6454e-114">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="6454e-115">Глобальные администраторы</span><span class="sxs-lookup"><span data-stu-id="6454e-115">Global Admins</span></span>
* <span data-ttu-id="6454e-116">Любое приложение, которое имеет авторизации tooaccess hello API (авторизации приложения может быть установки, только на основе разрешения глобального администратора)</span><span class="sxs-lookup"><span data-stu-id="6454e-116">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6454e-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6454e-117">Prerequisites</span></span>
<span data-ttu-id="6454e-118">В порядке tooaccess это подчиненности hello Reporting API, должен иметь:</span><span class="sxs-lookup"><span data-stu-id="6454e-118">In order tooaccess this report through hello Reporting API, you must have:</span></span>

* <span data-ttu-id="6454e-119">установить [Azure Active Directory Free или более поздней версии](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="6454e-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="6454e-120">Завершенная hello [API отчетов hello Azure AD tooaccess необходимых компонентов](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="6454e-120">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="6454e-121">Доступ к hello API</span><span class="sxs-lookup"><span data-stu-id="6454e-121">Accessing hello API</span></span>
<span data-ttu-id="6454e-122">Этот API можно получить либо через hello [Graph Explorer](https://graphexplorer2.cloudapp.net) или программно, используя, например, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6454e-122">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="6454e-123">В порядке для PowerShell toocorrectly интерпретировать синтаксис фильтра OData hello, используемых при вызове AAD Graph REST необходимо использовать обратный апостроф hello (также называемого: апостроф) символ слишком «escape» символа "$" hello.</span><span class="sxs-lookup"><span data-stu-id="6454e-123">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="6454e-124">служит Hello апострофа [escape-символа PowerShell](https://technet.microsoft.com/library/hh847755.aspx), позволяя PowerShell toodo литерала интерпретацию символа $ hello и не путать его как имя переменной PowerShell (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="6454e-124">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="6454e-125">Hello в этом разделе нацелено на hello Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="6454e-125">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="6454e-126">Пример PowerShell см. в этом [сценарии PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="6454e-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="6454e-127">Конечная точка API</span><span class="sxs-lookup"><span data-stu-id="6454e-127">API Endpoint</span></span>
<span data-ttu-id="6454e-128">Вы можете использовать этот API, с помощью hello, следующий URI:</span><span class="sxs-lookup"><span data-stu-id="6454e-128">You can access this API using hello following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="6454e-129">Нет ограничений на hello число записей, возвращаемых API аудита hello Azure AD (с помощью OData разбиение на страницы).</span><span class="sxs-lookup"><span data-stu-id="6454e-129">There is no limit on hello number of records returned by hello Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="6454e-130">Сведения о периоде удержания данных отчетов приведены в статье [Политики периода удержания отчетов](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="6454e-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="6454e-131">Этот вызов возвращается hello данных в пакетах.</span><span class="sxs-lookup"><span data-stu-id="6454e-131">This call returns hello data in batches.</span></span> <span data-ttu-id="6454e-132">В каждом пакете содержится не более 1000 записей.</span><span class="sxs-lookup"><span data-stu-id="6454e-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="6454e-133">tooget hello следующего пакета записей, используйте hello следующей ссылки.</span><span class="sxs-lookup"><span data-stu-id="6454e-133">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="6454e-134">Получение сведений токен skiptoken hello из первого набора hello возвращенных записей.</span><span class="sxs-lookup"><span data-stu-id="6454e-134">Get hello skiptoken information from hello first set of returned records.</span></span> <span data-ttu-id="6454e-135">в конце hello hello результирующий набор будет токен пропуска Hello.</span><span class="sxs-lookup"><span data-stu-id="6454e-135">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="6454e-136">Поддерживаемые фильтры</span><span class="sxs-lookup"><span data-stu-id="6454e-136">Supported filters</span></span>
<span data-ttu-id="6454e-137">Можно сузить hello число записей, возвращаемых API вызова в форме фильтра.</span><span class="sxs-lookup"><span data-stu-id="6454e-137">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="6454e-138">Для входа в API поддерживаются связанные данные hello следующие фильтры:</span><span class="sxs-lookup"><span data-stu-id="6454e-138">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="6454e-139">**$top =\<возвращается число записей toobe\>**  -toolimit hello количество возвращаемых записей.</span><span class="sxs-lookup"><span data-stu-id="6454e-139">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="6454e-140">Это дорогостоящая операция.</span><span class="sxs-lookup"><span data-stu-id="6454e-140">This is an expensive operation.</span></span> <span data-ttu-id="6454e-141">Этот фильтр не следует использовать, если требуется, чтобы tooreturn тысяч объектов.</span><span class="sxs-lookup"><span data-stu-id="6454e-141">You should not use this filter if you want tooreturn thousands of objects.</span></span>     
* <span data-ttu-id="6454e-142">**$filter =\<инструкцию фильтра\>**  -toospecify на основе hello поддерживаемый фильтр поля, типа hello записей, важные для вас</span><span class="sxs-lookup"><span data-stu-id="6454e-142">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="6454e-143">Поддерживаемый поля и операторы фильтров</span><span class="sxs-lookup"><span data-stu-id="6454e-143">Supported filter fields and operators</span></span>
<span data-ttu-id="6454e-144">Тип hello toospecify записей, которые вас интересуют, можно построить инструкцию фильтра, который может содержать один или сочетание hello следующие поля фильтра:</span><span class="sxs-lookup"><span data-stu-id="6454e-144">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="6454e-145">[activityDate](#activitydate) определяет дату или диапазон дат;</span><span class="sxs-lookup"><span data-stu-id="6454e-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="6454e-146">[Категория](#category) — определяет категорию hello требуются toofilter.</span><span class="sxs-lookup"><span data-stu-id="6454e-146">[category](#category) - defines hello category you want toofilter on.</span></span>
* <span data-ttu-id="6454e-147">[activityStatus](#activitystatus) -определяет hello состояние действия</span><span class="sxs-lookup"><span data-stu-id="6454e-147">[activityStatus](#activitystatus) - defines hello status of an activity</span></span>
* <span data-ttu-id="6454e-148">[Тип действия](#activitytype) -определяет тип hello действия</span><span class="sxs-lookup"><span data-stu-id="6454e-148">[activityType](#activitytype)  - defines hello type of an activity</span></span>
* <span data-ttu-id="6454e-149">[Действие](#activity) -определяет действие hello в виде строки</span><span class="sxs-lookup"><span data-stu-id="6454e-149">[activity](#activity) - defines hello activity as string</span></span>  
* <span data-ttu-id="6454e-150">[в имя субъекта](#actorname) -определяет субъект hello в форме имени субъекта hello</span><span class="sxs-lookup"><span data-stu-id="6454e-150">[actor/name](#actorname) -   defines hello actor in form of hello actor's name</span></span>
* <span data-ttu-id="6454e-151">[Субъект/objectid](#actorobjectid) -определяет субъект hello в виде идентификатора субъекта hello</span><span class="sxs-lookup"><span data-stu-id="6454e-151">[actor/objectid](#actorobjectid) - defines hello actor in form of hello actor's ID</span></span>   
* <span data-ttu-id="6454e-152">[субъект или имя участника-пользователя](#actorupn) -определяет субъект hello в форме hello субъекта имя участника-пользователя (UPN)</span><span class="sxs-lookup"><span data-stu-id="6454e-152">[actor/upn](#actorupn)  - defines hello actor in form of hello actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="6454e-153">[Имяцелевого/](#targetname) -определяет целевой hello в форме имени субъекта hello</span><span class="sxs-lookup"><span data-stu-id="6454e-153">[target/name](#targetname)  - defines hello target in form of hello actor's name</span></span>
* <span data-ttu-id="6454e-154">[целевой/objectid](#targetobjectid) -определяет цель hello в виде идентификатора целевого hello</span><span class="sxs-lookup"><span data-stu-id="6454e-154">[target/objectid](#targetobjectid) - defines hello target in form of hello target's ID</span></span>  
* <span data-ttu-id="6454e-155">[целевой/upn](#targetupn) -определяет субъект hello в форме hello субъекта имя участника-пользователя (UPN)</span><span class="sxs-lookup"><span data-stu-id="6454e-155">[target/upn](#targetupn) - defines hello actor in form of hello actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="6454e-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="6454e-156">activityDate</span></span>
<span data-ttu-id="6454e-157">**Поддерживаемые операторы**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="6454e-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="6454e-158">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6454e-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="6454e-159">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6454e-159">**Notes**:</span></span>

<span data-ttu-id="6454e-160">Время и дата указываются в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="6454e-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="6454e-161">category</span><span class="sxs-lookup"><span data-stu-id="6454e-161">category</span></span>

<span data-ttu-id="6454e-162">**Поддерживаемые значения**:</span><span class="sxs-lookup"><span data-stu-id="6454e-162">**Supported values**:</span></span>

| <span data-ttu-id="6454e-163">Категория</span><span class="sxs-lookup"><span data-stu-id="6454e-163">Category</span></span>                         | <span data-ttu-id="6454e-164">Значение</span><span class="sxs-lookup"><span data-stu-id="6454e-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="6454e-165">"Core Directory" (Основной каталог);</span><span class="sxs-lookup"><span data-stu-id="6454e-165">Core Directory</span></span>                   | <span data-ttu-id="6454e-166">Каталог</span><span class="sxs-lookup"><span data-stu-id="6454e-166">Directory</span></span> |
| <span data-ttu-id="6454e-167">"Self-service Password Management" (Самостоятельное управление паролями);</span><span class="sxs-lookup"><span data-stu-id="6454e-167">Self-service Password Management</span></span> | <span data-ttu-id="6454e-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="6454e-168">SSPR</span></span>      |
| <span data-ttu-id="6454e-169">"Self-service Group Management" (Самостоятельное управление группами);</span><span class="sxs-lookup"><span data-stu-id="6454e-169">Self-service Group Management</span></span>    | <span data-ttu-id="6454e-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="6454e-170">SSGM</span></span>      |
| <span data-ttu-id="6454e-171">"Account Provisioning" (Подготовка учетных записей).</span><span class="sxs-lookup"><span data-stu-id="6454e-171">Account Provisioning</span></span>             | <span data-ttu-id="6454e-172">Sync</span><span class="sxs-lookup"><span data-stu-id="6454e-172">Sync</span></span>      |
| <span data-ttu-id="6454e-173">"Automated Password Rollover" (Автоматическая смена пароля)</span><span class="sxs-lookup"><span data-stu-id="6454e-173">Automated Password Rollover</span></span>      | <span data-ttu-id="6454e-174">"Automated Password Rollover" (Автоматическая смена пароля)</span><span class="sxs-lookup"><span data-stu-id="6454e-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="6454e-175">Защита идентификации</span><span class="sxs-lookup"><span data-stu-id="6454e-175">Identity Protection</span></span>              | <span data-ttu-id="6454e-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="6454e-176">IdentityProtection</span></span> |
| <span data-ttu-id="6454e-177">Invited Users (Приглашаемые пользователи)</span><span class="sxs-lookup"><span data-stu-id="6454e-177">Invited Users</span></span>                    | <span data-ttu-id="6454e-178">Invited Users (Приглашаемые пользователи)</span><span class="sxs-lookup"><span data-stu-id="6454e-178">Invited Users</span></span> |
| <span data-ttu-id="6454e-179">MIM Service (Служба MIM)</span><span class="sxs-lookup"><span data-stu-id="6454e-179">MIM Service</span></span>                      | <span data-ttu-id="6454e-180">MIM Service (Служба MIM)</span><span class="sxs-lookup"><span data-stu-id="6454e-180">MIM Service</span></span> |



<span data-ttu-id="6454e-181">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="6454e-181">**Supported operators**: eq</span></span>

<span data-ttu-id="6454e-182">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6454e-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="6454e-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="6454e-183">activityStatus</span></span>

<span data-ttu-id="6454e-184">**Поддерживаемые значения**:</span><span class="sxs-lookup"><span data-stu-id="6454e-184">**Supported values**:</span></span>

| <span data-ttu-id="6454e-185">Состояние действия</span><span class="sxs-lookup"><span data-stu-id="6454e-185">Activity Status</span></span> | <span data-ttu-id="6454e-186">Значение</span><span class="sxs-lookup"><span data-stu-id="6454e-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="6454e-187">Успешно</span><span class="sxs-lookup"><span data-stu-id="6454e-187">Success</span></span>         | <span data-ttu-id="6454e-188">0</span><span class="sxs-lookup"><span data-stu-id="6454e-188">0</span></span>     |
| <span data-ttu-id="6454e-189">Сбой</span><span class="sxs-lookup"><span data-stu-id="6454e-189">Failure</span></span>         | <span data-ttu-id="6454e-190">- 1</span><span class="sxs-lookup"><span data-stu-id="6454e-190">- 1</span></span>   |

<span data-ttu-id="6454e-191">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="6454e-191">**Supported operators**: eq</span></span>

<span data-ttu-id="6454e-192">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6454e-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="6454e-193">activityType</span><span class="sxs-lookup"><span data-stu-id="6454e-193">activityType</span></span>
<span data-ttu-id="6454e-194">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="6454e-194">**Supported operators**: eq</span></span>

<span data-ttu-id="6454e-195">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6454e-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="6454e-196">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6454e-196">**Notes**:</span></span>

<span data-ttu-id="6454e-197">Учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="6454e-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="6454e-198">activity</span><span class="sxs-lookup"><span data-stu-id="6454e-198">activity</span></span>
<span data-ttu-id="6454e-199">**Поддерживаемые операторы**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="6454e-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="6454e-200">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6454e-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="6454e-201">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6454e-201">**Notes**:</span></span>

<span data-ttu-id="6454e-202">Учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="6454e-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="6454e-203">actor/name</span><span class="sxs-lookup"><span data-stu-id="6454e-203">actor/name</span></span>
<span data-ttu-id="6454e-204">**Поддерживаемые операторы**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="6454e-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="6454e-205">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6454e-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="6454e-206">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6454e-206">**Notes**:</span></span>

<span data-ttu-id="6454e-207">Не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="6454e-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="6454e-208">actor/objectid</span><span class="sxs-lookup"><span data-stu-id="6454e-208">actor/objectId</span></span>
<span data-ttu-id="6454e-209">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="6454e-209">**Supported operators**: eq</span></span>

<span data-ttu-id="6454e-210">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6454e-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="6454e-211">target/name</span><span class="sxs-lookup"><span data-stu-id="6454e-211">target/name</span></span>
<span data-ttu-id="6454e-212">**Поддерживаемые операторы**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="6454e-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="6454e-213">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6454e-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="6454e-214">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6454e-214">**Notes**:</span></span>

<span data-ttu-id="6454e-215">Не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="6454e-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="6454e-216">target/upn</span><span class="sxs-lookup"><span data-stu-id="6454e-216">target/upn</span></span>
<span data-ttu-id="6454e-217">**Поддерживаемые операторы**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="6454e-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="6454e-218">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6454e-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="6454e-219">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6454e-219">**Notes**:</span></span>

* <span data-ttu-id="6454e-220">Не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="6454e-220">Case-insensitive</span></span>
* <span data-ttu-id="6454e-221">Требуется полное пространство имен hello tooadd при запросе Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="6454e-221">You need tooadd hello full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="6454e-222">target/objectid</span><span class="sxs-lookup"><span data-stu-id="6454e-222">target/objectId</span></span>
<span data-ttu-id="6454e-223">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="6454e-223">**Supported operators**: eq</span></span>

<span data-ttu-id="6454e-224">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6454e-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="6454e-225">actor/upn</span><span class="sxs-lookup"><span data-stu-id="6454e-225">actor/upn</span></span>
<span data-ttu-id="6454e-226">**Поддерживаемые операторы**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="6454e-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="6454e-227">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6454e-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="6454e-228">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6454e-228">**Notes**:</span></span>

* <span data-ttu-id="6454e-229">Не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="6454e-229">Case-insensitive</span></span> 
* <span data-ttu-id="6454e-230">Требуется полное пространство имен hello tooadd при запросе Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="6454e-230">You need tooadd hello full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="6454e-231">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6454e-231">Next Steps</span></span>
* <span data-ttu-id="6454e-232">Вы хотите toosee примеры для отфильтрованных системных действий?</span><span class="sxs-lookup"><span data-stu-id="6454e-232">Do you want toosee examples for filtered system activities?</span></span> <span data-ttu-id="6454e-233">Извлечение hello [примеры аудита API Azure Active Directory](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6454e-233">Check out hello [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="6454e-234">Вы хотите, чтобы tooknow Дополнительные сведения об API отчетов hello Azure AD?</span><span class="sxs-lookup"><span data-stu-id="6454e-234">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="6454e-235">В разделе [Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6454e-235">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

