---
title: "aaaAzure Active Directory отчетов | Документы Microsoft"
description: "Общий обзор отчетов Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="92c36-103">Отчеты Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92c36-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="92c36-104">С отчетами Azure Active Directory можно получить важные сведения о том, как работает ваша среда.</span><span class="sxs-lookup"><span data-stu-id="92c36-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="92c36-105">Hello предоставленных данных позволяет делать следующее:</span><span class="sxs-lookup"><span data-stu-id="92c36-105">hello provided data enables you to:</span></span>

- <span data-ttu-id="92c36-106">определять, как приложения и службы используются пользователями;</span><span class="sxs-lookup"><span data-stu-id="92c36-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="92c36-107">Определить потенциальные угрозы влияющих на работоспособность hello среды</span><span class="sxs-lookup"><span data-stu-id="92c36-107">Detect potential risks affecting hello health of your environment</span></span>
- <span data-ttu-id="92c36-108">устранить неполадки, влияющие на работу пользователей.</span><span class="sxs-lookup"><span data-stu-id="92c36-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="92c36-109">Архитектура подготовки отчетов Hello основывается на двух основных основы:</span><span class="sxs-lookup"><span data-stu-id="92c36-109">hello reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="92c36-110">Отчеты о безопасности</span><span class="sxs-lookup"><span data-stu-id="92c36-110">Security reports</span></span>
- <span data-ttu-id="92c36-111">Отчеты об активности</span><span class="sxs-lookup"><span data-stu-id="92c36-111">Activity reports</span></span>

![Отчеты](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="92c36-113">Отчеты о безопасности</span><span class="sxs-lookup"><span data-stu-id="92c36-113">Security reports</span></span>

<span data-ttu-id="92c36-114">отчеты о безопасности Hello в Azure Active Directory помогают вам tooprotect удостоверения организации.</span><span class="sxs-lookup"><span data-stu-id="92c36-114">hello security reports in Azure Active Directory help you tooprotect your organization's identities.</span></span>  
<span data-ttu-id="92c36-115">В Azure Active Directory существует два типа отчетов безопасности:</span><span class="sxs-lookup"><span data-stu-id="92c36-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="92c36-116">**Пользователи с отметкой риск** — hello [пользователей с отметкой риск безопасности отчета](active-directory-reporting-security-user-at-risk.md), получить обзор учетных записей пользователей, которые могут быть скомпрометированы.</span><span class="sxs-lookup"><span data-stu-id="92c36-116">**Users flagged for risk** - From hello [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="92c36-117">**Рискованные входы** — используя hello [рискованным безопасности отчетов](active-directory-reporting-security-risky-sign-ins.md), отображается индикатор попыток входа, которые может быть выполнено с тем, кто является не hello законный владелец учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="92c36-117">**Risky sign-ins** - With hello [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 

<span data-ttu-id="92c36-118">**Какая лицензия Azure AD необходимо tooaccess безопасности отчета?**</span><span class="sxs-lookup"><span data-stu-id="92c36-118">**What Azure AD license do you need tooaccess a security report?**</span></span>  
<span data-ttu-id="92c36-119">Все выпуски Azure Active Directory предоставляют оба типа отчетов безопасности.</span><span class="sxs-lookup"><span data-stu-id="92c36-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="92c36-120">Однако hello уровень детализации отчета может различаться между выпусками hello:</span><span class="sxs-lookup"><span data-stu-id="92c36-120">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="92c36-121">В hello **выпуски Azure Active Directory Free и Basic**, вы уже получить список пользователей, помеченных для риска и рискованно входа в систему.</span><span class="sxs-lookup"><span data-stu-id="92c36-121">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="92c36-122">Hello **Azure Active Directory Premium 1** edition расширяет возможности этой модели, также позволяя tooexamine некоторых hello базового события рисков, которые были обнаружены для каждого отчета.</span><span class="sxs-lookup"><span data-stu-id="92c36-122">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="92c36-123">Hello **Azure Active Directory Premium 2** edition предоставляет вам hello наиболее подробные сведения о hello базового события рисков и позволяет также tooconfigure политики безопасности, которые автоматически отвечать tooconfigured уровней риска.</span><span class="sxs-lookup"><span data-stu-id="92c36-123">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about hello underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="92c36-124">Отчеты об активности</span><span class="sxs-lookup"><span data-stu-id="92c36-124">Activity reports</span></span>

<span data-ttu-id="92c36-125">В Azure Active Directory существует два типа отчетов об активности:</span><span class="sxs-lookup"><span data-stu-id="92c36-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="92c36-126">**Журналы аудита** - hello [журналы аудита, отчет о действиях](active-directory-reporting-activity-audit-logs.md) предоставляет доступ к истории toohello из каждой задачей, выполняемой в клиенте.</span><span class="sxs-lookup"><span data-stu-id="92c36-126">**Audit logs** - hello [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access toohello history of every task performed in your tenant.</span></span>

- <span data-ttu-id="92c36-127">**Входа в систему** — используя hello [входа в систему отчета об активности](active-directory-reporting-activity-sign-ins.md), можно определить, кто выполнил задачи hello, сообщаемые отчета журналов аудита hello.</span><span class="sxs-lookup"><span data-stu-id="92c36-127">**Sign-ins** -  With hello [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed hello tasks reported by hello audit logs report.</span></span>



<span data-ttu-id="92c36-128">Hello **отчет о журналах аудита** предоставляет записей действий системы для соответствия.</span><span class="sxs-lookup"><span data-stu-id="92c36-128">hello **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="92c36-129">Помимо прочего hello при условии, что данных можно tooaddress распространенные сценарии такие как:</span><span class="sxs-lookup"><span data-stu-id="92c36-129">Amongst others, hello provided data enables you tooaddress common scenarios such as:</span></span>

- <span data-ttu-id="92c36-130">Кто-то в клиент получил доступ tooan административной группы.</span><span class="sxs-lookup"><span data-stu-id="92c36-130">Someone in my tenant got access tooan admin group.</span></span> <span data-ttu-id="92c36-131">Кто предоставил этот доступ?</span><span class="sxs-lookup"><span data-stu-id="92c36-131">Who gave them access?</span></span> 

- <span data-ttu-id="92c36-132">Требуется список hello tooknow пользователи, входящие в определенное приложение с момента я недавно выставленных hello приложения и требуется tooknow, если он также выполняет</span><span class="sxs-lookup"><span data-stu-id="92c36-132">I want tooknow hello list of users signing into a specific app since I recently onboarded hello app and want tooknow if it’s doing well</span></span>

- <span data-ttu-id="92c36-133">Я хочу tooknow сколько пароль сбрасывает отключены в моей клиента</span><span class="sxs-lookup"><span data-stu-id="92c36-133">I want tooknow how many password resets are happening in my tenant</span></span>


<span data-ttu-id="92c36-134">**Какая лицензия Azure AD необходимо отчета журналов аудита hello tooaccess?**</span><span class="sxs-lookup"><span data-stu-id="92c36-134">**What Azure AD license do you need tooaccess hello audit logs report?**</span></span>  
<span data-ttu-id="92c36-135">отчет журналы аудита Hello доступен для компонентов, для которых имеются лицензии.</span><span class="sxs-lookup"><span data-stu-id="92c36-135">hello audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="92c36-136">При наличии лицензии для определенного компонента также имеется доступ toohello данные журнала для него аудита.</span><span class="sxs-lookup"><span data-stu-id="92c36-136">If you have a license for a specific feature, you also have access toohello audit log information for it.</span></span>

<span data-ttu-id="92c36-137">Дополнительные сведения см. в разделе **сравнение общедоступной возможности выпусков Free, Basic и Premium hello** в [средства Azure Active Directory и возможности](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="92c36-137">For more details, see **Comparing generally available features of hello Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="92c36-138">Hello **входа в систему отчета об активности** tootoofind включает отвечает tooquestions, такие как:</span><span class="sxs-lookup"><span data-stu-id="92c36-138">hello **sign-ins activity report** enables tootoofind answers tooquestions such as:</span></span>

- <span data-ttu-id="92c36-139">Что такое hello вход шаблон пользователя?</span><span class="sxs-lookup"><span data-stu-id="92c36-139">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="92c36-140">Сколько пользователей входили в течение недели?</span><span class="sxs-lookup"><span data-stu-id="92c36-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="92c36-141">Что такое состояние hello эти входа в систему?</span><span class="sxs-lookup"><span data-stu-id="92c36-141">What’s hello status of these sign-ins?</span></span>


<span data-ttu-id="92c36-142">**Какая лицензия Azure AD вы должны tooaccess hello отчета об активности входа в систему?**</span><span class="sxs-lookup"><span data-stu-id="92c36-142">**What Azure AD license do you need tooaccess hello sign-ins activity report?**</span></span>  
<span data-ttu-id="92c36-143">tooaccess Здравствуйте отчета об активности входа в систему, клиент должен иметь лицензию Azure AD Premium, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="92c36-143">tooaccess hello sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="92c36-144">Программный доступ</span><span class="sxs-lookup"><span data-stu-id="92c36-144">Programmatic access</span></span>

<span data-ttu-id="92c36-145">В пользовательском интерфейсе добавления toohello отчетов Azure Active Directory также предоставляет [программный доступ](active-directory-reporting-api-getting-started-azure-portal.md) toohello данных отчетов.</span><span class="sxs-lookup"><span data-stu-id="92c36-145">In addition toohello user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) toohello reporting data.</span></span> <span data-ttu-id="92c36-146">Hello данные этих отчетов могут быть очень полезным tooyour приложения, такие как системы SIEM, аудита и средства бизнес-аналитики.</span><span class="sxs-lookup"><span data-stu-id="92c36-146">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="92c36-147">Hello Azure AD сообщивший об API обеспечивают программный доступ к данным toohello через набор API на основе REST.</span><span class="sxs-lookup"><span data-stu-id="92c36-147">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="92c36-148">Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.</span><span class="sxs-lookup"><span data-stu-id="92c36-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="92c36-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="92c36-149">Next steps</span></span>

<span data-ttu-id="92c36-150">Если Дополнительные сведения о hello tooknow различных типов отчетов в Azure Active Directory, см.:</span><span class="sxs-lookup"><span data-stu-id="92c36-150">If you want tooknow more about hello various report types in Azure Active Directory, see:</span></span>

- <span data-ttu-id="92c36-151">[отчетом о пользователях, находящихся в группе риска](active-directory-reporting-security-user-at-risk.md);</span><span class="sxs-lookup"><span data-stu-id="92c36-151">[Users flagged for risk report](active-directory-reporting-security-user-at-risk.md)</span></span>
- <span data-ttu-id="92c36-152">[отчетом о входах, представляющих риск](active-directory-reporting-security-risky-sign-ins.md);</span><span class="sxs-lookup"><span data-stu-id="92c36-152">[Risky sign-ins report](active-directory-reporting-security-risky-sign-ins.md)</span></span>
- <span data-ttu-id="92c36-153">[отчетом о журналах аудита](active-directory-reporting-activity-audit-logs.md);</span><span class="sxs-lookup"><span data-stu-id="92c36-153">[Audit logs report](active-directory-reporting-activity-audit-logs.md)</span></span>
- <span data-ttu-id="92c36-154">[отчетом о журналах входа](active-directory-reporting-activity-sign-ins.md).</span><span class="sxs-lookup"><span data-stu-id="92c36-154">[Sign-ins logs report](active-directory-reporting-activity-sign-ins.md)</span></span>

<span data-ttu-id="92c36-155">Если tooknow больше о доступе к hello hello hello reporting API с помощью данных отчетов, см.:</span><span class="sxs-lookup"><span data-stu-id="92c36-155">If you want tooknow more about accessing hello hello reporting data using hello reporting API, see:</span></span> 

- [<span data-ttu-id="92c36-156">Приступая к работе с API отчетов Azure Active Directory "hello"</span><span class="sxs-lookup"><span data-stu-id="92c36-156">Getting started with hello Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png