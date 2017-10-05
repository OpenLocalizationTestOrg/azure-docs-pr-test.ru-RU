---
title: "Справочник по API аудита Azure Active Directory | Документация Майкрософт"
description: "Как начать работу с API аудита Azure Active Directory"
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
ms.openlocfilehash: 573e940c5390e7b990d889681eb37b73c5b253d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="ccb3d-103">Справочник по API аудита Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ccb3d-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="ccb3d-104">Эта статья входит в серию статей об API отчетов Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="ccb3d-105">Инструмент создания отчетов Azure AD предоставляет API, с помощью которого можно получить доступ к данным аудита, используя код или связанные инструменты.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span></span>
<span data-ttu-id="ccb3d-106">Цель этой статьи — предоставить справочные сведения об **API аудита**.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-106">The scope of this topic is to provide you with reference information about the **audit API**.</span></span>

<span data-ttu-id="ccb3d-107">См.:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-107">See:</span></span>

* <span data-ttu-id="ccb3d-108">Основные сведения см. в разделе [Журналы аудита](active-directory-reporting-azure-portal.md#activity-reports).</span><span class="sxs-lookup"><span data-stu-id="ccb3d-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="ccb3d-109">Дополнительные сведения об API отчетов см. в статье [Приступая к работе с API отчетов Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3d-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


<span data-ttu-id="ccb3d-110">Сведения:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-110">For:</span></span>

- <span data-ttu-id="ccb3d-111">Ответы на вопросы см. в разделе [Часто задаваемые вопросы](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3d-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="ccb3d-112">При возникновении проблем [создайте запрос в службу поддержки](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3d-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-the-data"></a><span data-ttu-id="ccb3d-113">Кто может получить доступ к данным?</span><span class="sxs-lookup"><span data-stu-id="ccb3d-113">Who can access the data?</span></span>
* <span data-ttu-id="ccb3d-114">Пользователи с ролью администратора безопасности или читателя безопасности</span><span class="sxs-lookup"><span data-stu-id="ccb3d-114">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="ccb3d-115">Глобальные администраторы</span><span class="sxs-lookup"><span data-stu-id="ccb3d-115">Global Admins</span></span>
* <span data-ttu-id="ccb3d-116">Любое приложение с разрешением на доступ к API (авторизацию приложения можно настроить только на основе разрешения глобального администратора)</span><span class="sxs-lookup"><span data-stu-id="ccb3d-116">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccb3d-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ccb3d-117">Prerequisites</span></span>
<span data-ttu-id="ccb3d-118">Для доступа к этому отчету с помощью API отчетов нужно:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-118">In order to access this report through the Reporting API, you must have:</span></span>

* <span data-ttu-id="ccb3d-119">установить [Azure Active Directory Free или более поздней версии](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="ccb3d-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="ccb3d-120">выполнить [предварительные требования для доступа к API отчетов Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3d-120">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="ccb3d-121">Получение доступа к API</span><span class="sxs-lookup"><span data-stu-id="ccb3d-121">Accessing the API</span></span>
<span data-ttu-id="ccb3d-122">Получить доступ к API можно с помощью [песочницы Graph](https://graphexplorer2.cloudapp.net) или программным путем, используя, например, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-122">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="ccb3d-123">Чтобы программа PowerShell правильно интерпретировала синтаксис фильтров OData, используемых в вызовах REST AAD Graph, необходимо использовать обратный апостроф и отделить знак $ escape-символами.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-123">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="ccb3d-124">Обратный апостроф выступает в качестве [escape-символа PowerShell](https://technet.microsoft.com/library/hh847755.aspx), позволяя PowerShell выполнить точную интерпретацию знака $ и не спутать его с именем переменной PowerShell (т. е. $filter).</span><span class="sxs-lookup"><span data-stu-id="ccb3d-124">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="ccb3d-125">В этой статье внимание уделяется Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-125">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="ccb3d-126">Пример PowerShell см. в этом [сценарии PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="ccb3d-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="ccb3d-127">Конечная точка API</span><span class="sxs-lookup"><span data-stu-id="ccb3d-127">API Endpoint</span></span>
<span data-ttu-id="ccb3d-128">Доступ к этому API можно получить, используя следующий URI:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-128">You can access this API using the following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="ccb3d-129">Количество записей, возвращаемых API аудита Azure AD (с помощью разбиения на страницы OData), не ограничено.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-129">There is no limit on the number of records returned by the Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="ccb3d-130">Сведения о периоде удержания данных отчетов приведены в статье [Политики периода удержания отчетов](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3d-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="ccb3d-131">Этот вызов возвращает данные в пакетах.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-131">This call returns the data in batches.</span></span> <span data-ttu-id="ccb3d-132">В каждом пакете содержится не более 1000 записей.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="ccb3d-133">Чтобы получить следующий пакет записей, используйте ссылку "Следующий".</span><span class="sxs-lookup"><span data-stu-id="ccb3d-133">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="ccb3d-134">Получите сведения о маркере пропуска из первого набора полученных записей.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-134">Get the skiptoken information from the first set of returned records.</span></span> <span data-ttu-id="ccb3d-135">Маркер пропуска можно найти в конце результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-135">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="ccb3d-136">Поддерживаемые фильтры</span><span class="sxs-lookup"><span data-stu-id="ccb3d-136">Supported filters</span></span>
<span data-ttu-id="ccb3d-137">Можно сократить число записей, возвращаемых после вызова API, в виде фильтра.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-137">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="ccb3d-138">Данные, связанные с API входа, поддерживают следующие фильтры:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-138">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="ccb3d-139">**$top=\<число возвращаемых записей\>** позволяет ограничить количество возвращаемых записей.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-139">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="ccb3d-140">Это дорогостоящая операция.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-140">This is an expensive operation.</span></span> <span data-ttu-id="ccb3d-141">Этот фильтр не следует использовать, если нужно возвратить большое количество объектов.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-141">You should not use this filter if you want to return thousands of objects.</span></span>     
* <span data-ttu-id="ccb3d-142">**$filter=\<оператор фильтра\>** позволяет указать тип требуемых записей на основе полей фильтра.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-142">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="ccb3d-143">Поддерживаемый поля и операторы фильтров</span><span class="sxs-lookup"><span data-stu-id="ccb3d-143">Supported filter fields and operators</span></span>
<span data-ttu-id="ccb3d-144">Чтобы указать тип требуемых записей, можно создать оператор фильтра, который может содержать одно или несколько из следующих полей фильтра:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-144">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="ccb3d-145">[activityDate](#activitydate) определяет дату или диапазон дат;</span><span class="sxs-lookup"><span data-stu-id="ccb3d-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="ccb3d-146">[category](#category) определяет категорию, по которой необходимо отфильтровать;</span><span class="sxs-lookup"><span data-stu-id="ccb3d-146">[category](#category) - defines the category you want to filter on.</span></span>
* <span data-ttu-id="ccb3d-147">[activityStatus](#activitystatus) определяет состояние действия;</span><span class="sxs-lookup"><span data-stu-id="ccb3d-147">[activityStatus](#activitystatus) - defines the status of an activity</span></span>
* <span data-ttu-id="ccb3d-148">[activityType](#activitytype) определяет тип действия;</span><span class="sxs-lookup"><span data-stu-id="ccb3d-148">[activityType](#activitytype)  - defines the type of an activity</span></span>
* <span data-ttu-id="ccb3d-149">[activity](#activity) определяет действие в виде строки;</span><span class="sxs-lookup"><span data-stu-id="ccb3d-149">[activity](#activity) - defines the activity as string</span></span>  
* <span data-ttu-id="ccb3d-150">[actor/name](#actorname) определяет субъект в виде имени субъекта;</span><span class="sxs-lookup"><span data-stu-id="ccb3d-150">[actor/name](#actorname) -   defines the actor in form of the actor's name</span></span>
* <span data-ttu-id="ccb3d-151">[actor/objectid](#actorobjectid) определяет субъект в виде идентификатора субъекта;</span><span class="sxs-lookup"><span data-stu-id="ccb3d-151">[actor/objectid](#actorobjectid) - defines the actor in form of the actor's ID</span></span>   
* <span data-ttu-id="ccb3d-152">[actor/upn](#actorupn) определяет субъект в виде имени участника-пользователя (UPN);</span><span class="sxs-lookup"><span data-stu-id="ccb3d-152">[actor/upn](#actorupn)  - defines the actor in form of the actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="ccb3d-153">[target/name](#targetname) определяет целевой объект в виде имени субъекта;</span><span class="sxs-lookup"><span data-stu-id="ccb3d-153">[target/name](#targetname)  - defines the target in form of the actor's name</span></span>
* <span data-ttu-id="ccb3d-154">[target/objectid](#targetobjectid) определяет целевой объект в виде идентификатора целевого объекта;</span><span class="sxs-lookup"><span data-stu-id="ccb3d-154">[target/objectid](#targetobjectid) - defines the target in form of the target's ID</span></span>  
* <span data-ttu-id="ccb3d-155">[target/upn](#targetupn) определяет целевой объект в виде основного имени пользователя (UPN) субъекта.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-155">[target/upn](#targetupn) - defines the actor in form of the actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="ccb3d-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="ccb3d-156">activityDate</span></span>
<span data-ttu-id="ccb3d-157">**Поддерживаемые операторы**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="ccb3d-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="ccb3d-158">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="ccb3d-159">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="ccb3d-159">**Notes**:</span></span>

<span data-ttu-id="ccb3d-160">Время и дата указываются в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="ccb3d-161">category</span><span class="sxs-lookup"><span data-stu-id="ccb3d-161">category</span></span>

<span data-ttu-id="ccb3d-162">**Поддерживаемые значения**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-162">**Supported values**:</span></span>

| <span data-ttu-id="ccb3d-163">Категория</span><span class="sxs-lookup"><span data-stu-id="ccb3d-163">Category</span></span>                         | <span data-ttu-id="ccb3d-164">Значение</span><span class="sxs-lookup"><span data-stu-id="ccb3d-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="ccb3d-165">"Core Directory" (Основной каталог);</span><span class="sxs-lookup"><span data-stu-id="ccb3d-165">Core Directory</span></span>                   | <span data-ttu-id="ccb3d-166">Каталог</span><span class="sxs-lookup"><span data-stu-id="ccb3d-166">Directory</span></span> |
| <span data-ttu-id="ccb3d-167">"Self-service Password Management" (Самостоятельное управление паролями);</span><span class="sxs-lookup"><span data-stu-id="ccb3d-167">Self-service Password Management</span></span> | <span data-ttu-id="ccb3d-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="ccb3d-168">SSPR</span></span>      |
| <span data-ttu-id="ccb3d-169">"Self-service Group Management" (Самостоятельное управление группами);</span><span class="sxs-lookup"><span data-stu-id="ccb3d-169">Self-service Group Management</span></span>    | <span data-ttu-id="ccb3d-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="ccb3d-170">SSGM</span></span>      |
| <span data-ttu-id="ccb3d-171">"Account Provisioning" (Подготовка учетных записей).</span><span class="sxs-lookup"><span data-stu-id="ccb3d-171">Account Provisioning</span></span>             | <span data-ttu-id="ccb3d-172">Sync</span><span class="sxs-lookup"><span data-stu-id="ccb3d-172">Sync</span></span>      |
| <span data-ttu-id="ccb3d-173">"Automated Password Rollover" (Автоматическая смена пароля)</span><span class="sxs-lookup"><span data-stu-id="ccb3d-173">Automated Password Rollover</span></span>      | <span data-ttu-id="ccb3d-174">"Automated Password Rollover" (Автоматическая смена пароля)</span><span class="sxs-lookup"><span data-stu-id="ccb3d-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="ccb3d-175">Защита идентификации</span><span class="sxs-lookup"><span data-stu-id="ccb3d-175">Identity Protection</span></span>              | <span data-ttu-id="ccb3d-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="ccb3d-176">IdentityProtection</span></span> |
| <span data-ttu-id="ccb3d-177">Invited Users (Приглашаемые пользователи)</span><span class="sxs-lookup"><span data-stu-id="ccb3d-177">Invited Users</span></span>                    | <span data-ttu-id="ccb3d-178">Invited Users (Приглашаемые пользователи)</span><span class="sxs-lookup"><span data-stu-id="ccb3d-178">Invited Users</span></span> |
| <span data-ttu-id="ccb3d-179">MIM Service (Служба MIM)</span><span class="sxs-lookup"><span data-stu-id="ccb3d-179">MIM Service</span></span>                      | <span data-ttu-id="ccb3d-180">MIM Service (Служба MIM)</span><span class="sxs-lookup"><span data-stu-id="ccb3d-180">MIM Service</span></span> |



<span data-ttu-id="ccb3d-181">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="ccb3d-181">**Supported operators**: eq</span></span>

<span data-ttu-id="ccb3d-182">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="ccb3d-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="ccb3d-183">activityStatus</span></span>

<span data-ttu-id="ccb3d-184">**Поддерживаемые значения**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-184">**Supported values**:</span></span>

| <span data-ttu-id="ccb3d-185">Состояние действия</span><span class="sxs-lookup"><span data-stu-id="ccb3d-185">Activity Status</span></span> | <span data-ttu-id="ccb3d-186">Значение</span><span class="sxs-lookup"><span data-stu-id="ccb3d-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="ccb3d-187">Успешно</span><span class="sxs-lookup"><span data-stu-id="ccb3d-187">Success</span></span>         | <span data-ttu-id="ccb3d-188">0</span><span class="sxs-lookup"><span data-stu-id="ccb3d-188">0</span></span>     |
| <span data-ttu-id="ccb3d-189">Сбой</span><span class="sxs-lookup"><span data-stu-id="ccb3d-189">Failure</span></span>         | <span data-ttu-id="ccb3d-190">- 1</span><span class="sxs-lookup"><span data-stu-id="ccb3d-190">- 1</span></span>   |

<span data-ttu-id="ccb3d-191">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="ccb3d-191">**Supported operators**: eq</span></span>

<span data-ttu-id="ccb3d-192">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="ccb3d-193">activityType</span><span class="sxs-lookup"><span data-stu-id="ccb3d-193">activityType</span></span>
<span data-ttu-id="ccb3d-194">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="ccb3d-194">**Supported operators**: eq</span></span>

<span data-ttu-id="ccb3d-195">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="ccb3d-196">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="ccb3d-196">**Notes**:</span></span>

<span data-ttu-id="ccb3d-197">Учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="ccb3d-198">activity</span><span class="sxs-lookup"><span data-stu-id="ccb3d-198">activity</span></span>
<span data-ttu-id="ccb3d-199">**Поддерживаемые операторы**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="ccb3d-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="ccb3d-200">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="ccb3d-201">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="ccb3d-201">**Notes**:</span></span>

<span data-ttu-id="ccb3d-202">Учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="ccb3d-203">actor/name</span><span class="sxs-lookup"><span data-stu-id="ccb3d-203">actor/name</span></span>
<span data-ttu-id="ccb3d-204">**Поддерживаемые операторы**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="ccb3d-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="ccb3d-205">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="ccb3d-206">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="ccb3d-206">**Notes**:</span></span>

<span data-ttu-id="ccb3d-207">Не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="ccb3d-208">actor/objectid</span><span class="sxs-lookup"><span data-stu-id="ccb3d-208">actor/objectId</span></span>
<span data-ttu-id="ccb3d-209">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="ccb3d-209">**Supported operators**: eq</span></span>

<span data-ttu-id="ccb3d-210">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="ccb3d-211">target/name</span><span class="sxs-lookup"><span data-stu-id="ccb3d-211">target/name</span></span>
<span data-ttu-id="ccb3d-212">**Поддерживаемые операторы**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="ccb3d-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="ccb3d-213">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="ccb3d-214">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="ccb3d-214">**Notes**:</span></span>

<span data-ttu-id="ccb3d-215">Не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="ccb3d-216">target/upn</span><span class="sxs-lookup"><span data-stu-id="ccb3d-216">target/upn</span></span>
<span data-ttu-id="ccb3d-217">**Поддерживаемые операторы**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="ccb3d-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="ccb3d-218">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="ccb3d-219">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="ccb3d-219">**Notes**:</span></span>

* <span data-ttu-id="ccb3d-220">Без учета регистра</span><span class="sxs-lookup"><span data-stu-id="ccb3d-220">Case-insensitive</span></span>
* <span data-ttu-id="ccb3d-221">При запросе Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity необходимо добавить полное пространство имен.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-221">You need to add the full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="ccb3d-222">target/objectid</span><span class="sxs-lookup"><span data-stu-id="ccb3d-222">target/objectId</span></span>
<span data-ttu-id="ccb3d-223">**Поддерживаемые операторы**: eq</span><span class="sxs-lookup"><span data-stu-id="ccb3d-223">**Supported operators**: eq</span></span>

<span data-ttu-id="ccb3d-224">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="ccb3d-225">actor/upn</span><span class="sxs-lookup"><span data-stu-id="ccb3d-225">actor/upn</span></span>
<span data-ttu-id="ccb3d-226">**Поддерживаемые операторы**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="ccb3d-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="ccb3d-227">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="ccb3d-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="ccb3d-228">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="ccb3d-228">**Notes**:</span></span>

* <span data-ttu-id="ccb3d-229">Не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-229">Case-insensitive</span></span> 
* <span data-ttu-id="ccb3d-230">При запросе Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity необходимо добавить полное пространство имен.</span><span class="sxs-lookup"><span data-stu-id="ccb3d-230">You need to add the full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="ccb3d-231">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ccb3d-231">Next Steps</span></span>
* <span data-ttu-id="ccb3d-232">Хотите увидеть примеры отфильтрованных системных операций?</span><span class="sxs-lookup"><span data-stu-id="ccb3d-232">Do you want to see examples for filtered system activities?</span></span> <span data-ttu-id="ccb3d-233">См. [примеры API аудита Azure Active Directory](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3d-233">Check out the [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="ccb3d-234">Хотите узнать больше об API отчетов Azure AD?</span><span class="sxs-lookup"><span data-stu-id="ccb3d-234">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="ccb3d-235">См. статью [Приступая к работе с API отчетов Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3d-235">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

