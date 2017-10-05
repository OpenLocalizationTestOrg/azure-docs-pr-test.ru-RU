---
title: "Отчеты Azure Active Directory | Документация Майкрософт"
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
ms.openlocfilehash: 738c8f4a56586b87f03973ec258b0a3023affa60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="b99c7-103">Отчеты Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b99c7-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="b99c7-104">С отчетами Azure Active Directory можно получить важные сведения о том, как работает ваша среда.</span><span class="sxs-lookup"><span data-stu-id="b99c7-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="b99c7-105">Полученные данные позволят вам выполнять следующее:</span><span class="sxs-lookup"><span data-stu-id="b99c7-105">The provided data enables you to:</span></span>

- <span data-ttu-id="b99c7-106">определять, как приложения и службы используются пользователями;</span><span class="sxs-lookup"><span data-stu-id="b99c7-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="b99c7-107">обнаружить потенциальные риски, которые могут повлиять на работоспособность среды;</span><span class="sxs-lookup"><span data-stu-id="b99c7-107">Detect potential risks affecting the health of your environment</span></span>
- <span data-ttu-id="b99c7-108">устранить неполадки, влияющие на работу пользователей.</span><span class="sxs-lookup"><span data-stu-id="b99c7-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="b99c7-109">Архитектура отчета основана на двух главных компонентах:</span><span class="sxs-lookup"><span data-stu-id="b99c7-109">The reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="b99c7-110">Отчеты о безопасности</span><span class="sxs-lookup"><span data-stu-id="b99c7-110">Security reports</span></span>
- <span data-ttu-id="b99c7-111">Отчеты об активности</span><span class="sxs-lookup"><span data-stu-id="b99c7-111">Activity reports</span></span>

![Отчеты](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="b99c7-113">Отчеты о безопасности</span><span class="sxs-lookup"><span data-stu-id="b99c7-113">Security reports</span></span>

<span data-ttu-id="b99c7-114">Отчеты безопасности в Azure Active Directory помогают защитить удостоверения организации.</span><span class="sxs-lookup"><span data-stu-id="b99c7-114">The security reports in Azure Active Directory help you to protect your organization's identities.</span></span>  
<span data-ttu-id="b99c7-115">В Azure Active Directory существует два типа отчетов безопасности:</span><span class="sxs-lookup"><span data-stu-id="b99c7-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="b99c7-116">**Пользователи, находящиеся в группе риска.** [С помощью отчетов безопасности о пользователях, находящихся в группе риска](active-directory-reporting-security-user-at-risk.md) вы получите сведения об учетных записях пользователей, которые могли быть скомпрометированы.</span><span class="sxs-lookup"><span data-stu-id="b99c7-116">**Users flagged for risk** - From the [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="b99c7-117">**Рискованные входы в систему.** [С помощью отчетов безопасности о рискованных входах в систему](active-directory-reporting-security-risky-sign-ins.md) вы получите сведения о попытках входа пользователями, которые не являются законными владельцами учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="b99c7-117">**Risky sign-ins** - With the [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 

<span data-ttu-id="b99c7-118">**Какая требуется лицензия Azure AD, чтобы получить доступ к отчету безопасности?**</span><span class="sxs-lookup"><span data-stu-id="b99c7-118">**What Azure AD license do you need to access a security report?**</span></span>  
<span data-ttu-id="b99c7-119">Все выпуски Azure Active Directory предоставляют оба типа отчетов безопасности.</span><span class="sxs-lookup"><span data-stu-id="b99c7-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="b99c7-120">Однако уровень детализации отчета может для выпусков отличаться.</span><span class="sxs-lookup"><span data-stu-id="b99c7-120">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="b99c7-121">В **бесплатном и базовом выпусках Azure Active Directory** у вас будет список пользователей, находящихся в группе риска и рискованных входов в систему.</span><span class="sxs-lookup"><span data-stu-id="b99c7-121">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="b99c7-122">Выпуск **Azure Active Directory Premium 1** расширяет эту модель, также позволяя вам изучать некоторые базовые события риска, обнаруженные для каждого отчета.</span><span class="sxs-lookup"><span data-stu-id="b99c7-122">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="b99c7-123">Выпуск **Azure Active Directory Premium 2** предоставляет наиболее полные сведения о базовых событиях риска, а также позволяет настроить политики безопасности, автоматически реагирующие на настроенные уровни риска.</span><span class="sxs-lookup"><span data-stu-id="b99c7-123">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about the underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="b99c7-124">Отчеты об активности</span><span class="sxs-lookup"><span data-stu-id="b99c7-124">Activity reports</span></span>

<span data-ttu-id="b99c7-125">В Azure Active Directory существует два типа отчетов об активности:</span><span class="sxs-lookup"><span data-stu-id="b99c7-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="b99c7-126">**Журналы аудита.** [Отчет об активности журналов аудита](active-directory-reporting-activity-audit-logs.md) обеспечивает доступ к журналу каждой задачи, выполняемой в клиенте.</span><span class="sxs-lookup"><span data-stu-id="b99c7-126">**Audit logs** - The [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access to the history of every task performed in your tenant.</span></span>

- <span data-ttu-id="b99c7-127">**События входа.** [С помощью отчета об активности событий входа](active-directory-reporting-activity-sign-ins.md) вы можете определить, кто выполнил задачи, отправленные отчетом о журналах аудита.</span><span class="sxs-lookup"><span data-stu-id="b99c7-127">**Sign-ins** -  With the [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed the tasks reported by the audit logs report.</span></span>



<span data-ttu-id="b99c7-128">**Отчет о журналах аудита** предоставляет записи системных операций для соответствия.</span><span class="sxs-lookup"><span data-stu-id="b99c7-128">The **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="b99c7-129">Помимо прочего, предоставленные данные позволят вам ознакомиться со следующими распространенными сценариями:</span><span class="sxs-lookup"><span data-stu-id="b99c7-129">Amongst others, the provided data enables you to address common scenarios such as:</span></span>

- <span data-ttu-id="b99c7-130">Кто-то в моем клиенте получил доступ к группе администраторов.</span><span class="sxs-lookup"><span data-stu-id="b99c7-130">Someone in my tenant got access to an admin group.</span></span> <span data-ttu-id="b99c7-131">Кто предоставил этот доступ?</span><span class="sxs-lookup"><span data-stu-id="b99c7-131">Who gave them access?</span></span> 

- <span data-ttu-id="b99c7-132">Я хочу знать список пользователей, выполнивших вход в определенное приложение, так как оно подключено недавно и я хочу убедиться, что оно работает соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="b99c7-132">I want to know the list of users signing into a specific app since I recently onboarded the app and want to know if it’s doing well</span></span>

- <span data-ttu-id="b99c7-133">Я хочу знать число сбросов пароля в клиенте.</span><span class="sxs-lookup"><span data-stu-id="b99c7-133">I want to know how many password resets are happening in my tenant</span></span>


<span data-ttu-id="b99c7-134">**Какая требуется лицензия Azure AD, чтобы получить доступ к отчету о журналах аудита?**</span><span class="sxs-lookup"><span data-stu-id="b99c7-134">**What Azure AD license do you need to access the audit logs report?**</span></span>  
<span data-ttu-id="b99c7-135">Отчет о журналах аудита доступен для функций, на которые у вас есть лицензии.</span><span class="sxs-lookup"><span data-stu-id="b99c7-135">The audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="b99c7-136">Если у вас есть лицензия для определенной функции, у вас также есть доступ к данным журнала аудита для этой функции.</span><span class="sxs-lookup"><span data-stu-id="b99c7-136">If you have a license for a specific feature, you also have access to the audit log information for it.</span></span>

<span data-ttu-id="b99c7-137">Дополнительные сведения см. в разделе **Сравнение общедоступных функций выпусков Free, Basic и Premium** на странице [Функции и возможности Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="b99c7-137">For more details, see **Comparing generally available features of the Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="b99c7-138">**Отчет об активности событий входа** позволяет ответить на следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="b99c7-138">The **sign-ins activity report** enables to to find answers to questions such as:</span></span>

- <span data-ttu-id="b99c7-139">Что такое шаблон входа пользователя?</span><span class="sxs-lookup"><span data-stu-id="b99c7-139">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="b99c7-140">Сколько пользователей входили в течение недели?</span><span class="sxs-lookup"><span data-stu-id="b99c7-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="b99c7-141">Каков статус их входа?</span><span class="sxs-lookup"><span data-stu-id="b99c7-141">What’s the status of these sign-ins?</span></span>


<span data-ttu-id="b99c7-142">**Какая требуется лицензия Azure AD, чтобы получить доступ к отчету об активности событий входа?**</span><span class="sxs-lookup"><span data-stu-id="b99c7-142">**What Azure AD license do you need to access the sign-ins activity report?**</span></span>  
<span data-ttu-id="b99c7-143">Чтобы получить доступ к отчету об активности событий входа, с клиентом должна быть связана лицензия Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="b99c7-143">To access the sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="b99c7-144">Программный доступ</span><span class="sxs-lookup"><span data-stu-id="b99c7-144">Programmatic access</span></span>

<span data-ttu-id="b99c7-145">Кроме пользовательского интерфейса отчеты Azure Active Directory также предоставляют [программный доступ](active-directory-reporting-api-getting-started-azure-portal.md) для данных отчетов.</span><span class="sxs-lookup"><span data-stu-id="b99c7-145">In addition to the user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) to the reporting data.</span></span> <span data-ttu-id="b99c7-146">Данные этих отчетов могут быть очень полезными для приложений, например систем SIEM, а также инструментов аудита и бизнес-аналитики.</span><span class="sxs-lookup"><span data-stu-id="b99c7-146">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="b99c7-147">Интерфейсы API отчетов Azure AD предоставляют программный доступ к данным с помощью набора интерфейсов API на базе REST.</span><span class="sxs-lookup"><span data-stu-id="b99c7-147">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="b99c7-148">Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.</span><span class="sxs-lookup"><span data-stu-id="b99c7-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="b99c7-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b99c7-149">Next steps</span></span>

<span data-ttu-id="b99c7-150">Если вы хотите получить дополнительные сведения о различных типах отчетов в Azure Active Directory, ознакомьтесь со следующими разделами:</span><span class="sxs-lookup"><span data-stu-id="b99c7-150">If you want to know more about the various report types in Azure Active Directory, see:</span></span>

- <span data-ttu-id="b99c7-151">[отчетом о пользователях, находящихся в группе риска](active-directory-reporting-security-user-at-risk.md);</span><span class="sxs-lookup"><span data-stu-id="b99c7-151">[Users flagged for risk report](active-directory-reporting-security-user-at-risk.md)</span></span>
- <span data-ttu-id="b99c7-152">[отчетом о входах, представляющих риск](active-directory-reporting-security-risky-sign-ins.md);</span><span class="sxs-lookup"><span data-stu-id="b99c7-152">[Risky sign-ins report](active-directory-reporting-security-risky-sign-ins.md)</span></span>
- <span data-ttu-id="b99c7-153">[отчетом о журналах аудита](active-directory-reporting-activity-audit-logs.md);</span><span class="sxs-lookup"><span data-stu-id="b99c7-153">[Audit logs report](active-directory-reporting-activity-audit-logs.md)</span></span>
- <span data-ttu-id="b99c7-154">[отчетом о журналах входа](active-directory-reporting-activity-sign-ins.md).</span><span class="sxs-lookup"><span data-stu-id="b99c7-154">[Sign-ins logs report](active-directory-reporting-activity-sign-ins.md)</span></span>

<span data-ttu-id="b99c7-155">Если вы хотите получить дополнительные сведения о доступе к данным отчетов с помощью API отчетов, ознакомьтесь со статьей</span><span class="sxs-lookup"><span data-stu-id="b99c7-155">If you want to know more about accessing the the reporting data using the reporting API, see:</span></span> 

- <span data-ttu-id="b99c7-156">[Getting started with the Azure Active Directory reporting API](active-directory-reporting-api-getting-started-azure-portal.md) (Приступая к работе с API отчетов Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="b99c7-156">[Getting started with the Azure Active Directory reporting API](active-directory-reporting-api-getting-started-azure-portal.md)</span></span>


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png