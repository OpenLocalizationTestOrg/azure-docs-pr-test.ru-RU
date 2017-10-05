---
title: "Отчет системы безопасности о пользователях под угрозой на портале Azure Active Directory | Документация Майкрософт"
description: "Описание отчета системы безопасности о пользователях под угрозой на портале Azure Active Directory"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 04f15384a7cd0fa03300acdf159d371569ecf9fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="users-flagged-for-risk-security-report-in-the-azure-active-directory-portal"></a><span data-ttu-id="3fba2-103">Описание отчета системы безопасности о пользователях под угрозой на портале Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3fba2-103">Users flagged for risk security report in the Azure Active Directory portal</span></span>

<span data-ttu-id="3fba2-104">С помощью отчетов о безопасности в Azure Active Directory (Azure AD) можно получить ценную информацию о наличии скомпрометированных учетных записей пользователей в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="3fba2-104">With the security reports in the Azure Active Directory (Azure AD), you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="3fba2-105">Azure Active Directory обнаруживает подозрительные действия, связанные с учетными записями пользователей.</span><span class="sxs-lookup"><span data-stu-id="3fba2-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="3fba2-106">Для каждого обнаруженного действия создается запись, которая называется *событием риска*.</span><span class="sxs-lookup"><span data-stu-id="3fba2-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="3fba2-107">Дополнительные сведения см. в статье [События риска Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="3fba2-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="3fba2-108">Обнаруженные события риска используются для вычисления следующих параметров.</span><span class="sxs-lookup"><span data-stu-id="3fba2-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="3fba2-109">**Входы, представляющие риск**. Вход, представляющий риск, означает, что в систему пытался войти пользователь, который не является законным владельцем учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3fba2-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="3fba2-110">Дополнительные сведения см. в разделе [Вход, представляющий риск](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="3fba2-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="3fba2-111">**Пользователи, находящиеся в группе риска**. Такая пометка означает, что конфиденциальность учетной записи пользователя, возможно, нарушена.</span><span class="sxs-lookup"><span data-stu-id="3fba2-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="3fba2-112">Дополнительные сведения см. в разделе [Пользователи, помеченные для события риска](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="3fba2-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="3fba2-113">На портале Azure отчеты о безопасности можно найти в колонке **Azure Active Directory** в разделе **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="3fba2-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span>  

![события входа, представляющие риск.](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a><span data-ttu-id="3fba2-115">Какая лицензия Azure AD требуется для доступа к отчету безопасности?</span><span class="sxs-lookup"><span data-stu-id="3fba2-115">What Azure AD license do you need to access a security report?</span></span>  

<span data-ttu-id="3fba2-116">Все выпуски Azure Active Directory предоставляют отчеты о пользователях, находящихся в группе риска.</span><span class="sxs-lookup"><span data-stu-id="3fba2-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="3fba2-117">Однако уровень детализации отчета может для выпусков отличаться.</span><span class="sxs-lookup"><span data-stu-id="3fba2-117">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="3fba2-118">В **бесплатном и базовом выпусках Azure Active Directory** у вас будет список пользователей, находящихся в группе риска.</span><span class="sxs-lookup"><span data-stu-id="3fba2-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="3fba2-119">Выпуск **Azure Active Directory Premium 1** расширяет эту модель, также позволяя вам изучать некоторые базовые события риска, обнаруженные для каждого отчета.</span><span class="sxs-lookup"><span data-stu-id="3fba2-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="3fba2-120">Выпуск **Azure Active Directory Premium 2** предоставляет наиболее полные сведения о базовых событиях риска, а также позволяет настроить политики безопасности, автоматически реагирующие на настроенные уровни риска.</span><span class="sxs-lookup"><span data-stu-id="3fba2-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and enables you to configure security policies that automatically respond to configured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="3fba2-121">Выпуски "Бесплатный" и "Базовый" Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3fba2-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="3fba2-122">В выпусках "Бесплатный" и "Базовый" Azure Active Directory доступен список учетных записей пользователей, конфиденциальность которых могла быть нарушена.</span><span class="sxs-lookup"><span data-stu-id="3fba2-122">The users flagged for risk report in the Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="3fba2-124">Если выбрать пользователя, откроется колонка его данных.</span><span class="sxs-lookup"><span data-stu-id="3fba2-124">Selecting a user opens the related user data blade.</span></span>
<span data-ttu-id="3fba2-125">Вы можете просмотреть журнал входов пользователя под угрозой и сбросить пароль, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="3fba2-125">For users that are at risk, you can review the user’s sign-in history and reset the password if necessary.</span></span>

![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="3fba2-127">Это диалоговое окно предоставляет следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="3fba2-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="3fba2-128">Загрузка отчета</span><span class="sxs-lookup"><span data-stu-id="3fba2-128">Download the report</span></span>

- <span data-ttu-id="3fba2-129">Поиск пользователей</span><span class="sxs-lookup"><span data-stu-id="3fba2-129">Search users</span></span>

![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="3fba2-131">Выпуски Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="3fba2-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="3fba2-132">Отчет о пользователях под угрозой в выпусках Azure Active Directory Premium предоставляет следующее:</span><span class="sxs-lookup"><span data-stu-id="3fba2-132">The users flagged for risk report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="3fba2-133">[Список учетных записей пользователей](active-directory-identityprotection.md#users-flagged-for-risk), которые, возможно, были скомпрометированы.</span><span class="sxs-lookup"><span data-stu-id="3fba2-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="3fba2-134">Сводная информация о [типах обнаруженных событий риска](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="3fba2-134">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="3fba2-135">Возможность скачать отчет.</span><span class="sxs-lookup"><span data-stu-id="3fba2-135">An option to download the report</span></span>

- <span data-ttu-id="3fba2-136">Настройка [политики устранения рисков пользователей](active-directory-identityprotection.md#user-risk-security-policy).</span><span class="sxs-lookup"><span data-stu-id="3fba2-136">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="3fba2-138">При выборе пользователя отображается подробное представление отчета об этом пользователе, предоставляющее перечисленные ниже возможности.</span><span class="sxs-lookup"><span data-stu-id="3fba2-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="3fba2-139">Отображение представления всех событий входа.</span><span class="sxs-lookup"><span data-stu-id="3fba2-139">Open the All sign-ins view</span></span>

- <span data-ttu-id="3fba2-140">Сброс пароля пользователя</span><span class="sxs-lookup"><span data-stu-id="3fba2-140">Reset the user's password</span></span>

- <span data-ttu-id="3fba2-141">Отклонение всех событий.</span><span class="sxs-lookup"><span data-stu-id="3fba2-141">Dismiss all events</span></span>

- <span data-ttu-id="3fba2-142">Изучение обнаруженных событий риска для пользователя.</span><span class="sxs-lookup"><span data-stu-id="3fba2-142">Investigate reported risk events for the user.</span></span> 


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="3fba2-144">Чтобы изучить событие риска, выберите его из списка. Откроется колонка **Сведения** для этого события риска.</span><span class="sxs-lookup"><span data-stu-id="3fba2-144">To investigate a risk event, select one from the list to open the **Details** blade for this risk event.</span></span> <span data-ttu-id="3fba2-145">В колонке **Сведения** вы можете либо [вручную закрыть событие риска](active-directory-identityprotection.md#closing-risk-events-manually), либо повторно активировать событие риска, закрытое вручную.</span><span class="sxs-lookup"><span data-stu-id="3fba2-145">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="3fba2-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3fba2-147">Next steps</span></span>

- <span data-ttu-id="3fba2-148">Дополнительные сведения о защите идентификации Azure см. в статье [Защита идентификации Azure Active Directory](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="3fba2-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

