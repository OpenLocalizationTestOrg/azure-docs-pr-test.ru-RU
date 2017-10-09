---
title: "риск безопасности отчетов на портале Azure Active Directory hello с отметкой aaaUsers | Документы Microsoft"
description: "Дополнительные сведения о пользователях hello, помеченных для риск безопасности отчетов на портале Azure Active Directory hello"
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
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="653be-103">Пользователи с отметкой риск безопасности отчетов на портале Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="653be-103">Users flagged for risk security report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="653be-104">Hello безопасности отчетов в hello Azure Active Directory (Azure AD) позволяет получить подробные сведения о вероятности hello скомпрометированных учетных записей пользователей в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="653be-104">With hello security reports in hello Azure Active Directory (Azure AD), you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="653be-105">Azure Active Directory обнаруживает подозрительные действия, которые являются связанные tooyour учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="653be-105">Azure Active Directory detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="653be-106">Для каждого обнаруженного действия создается запись, которая называется *событием риска*.</span><span class="sxs-lookup"><span data-stu-id="653be-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="653be-107">Дополнительные сведения см. в статье [События риска Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="653be-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="653be-108">Hello обнаружил, что риск события, используемые toocalculate:</span><span class="sxs-lookup"><span data-stu-id="653be-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="653be-109">**Рискованные входы** -рискованным вход является показателем для попытки входа, возможно, выполнены с тем, кто не hello законный владельцем учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="653be-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="653be-110">Дополнительные сведения см. в разделе [Вход, представляющий риск](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="653be-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="653be-111">**Пользователи, находящиеся в группе риска**. Такая пометка означает, что конфиденциальность учетной записи пользователя, возможно, нарушена.</span><span class="sxs-lookup"><span data-stu-id="653be-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="653be-112">Дополнительные сведения см. в разделе [Пользователи, помеченные для события риска](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="653be-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="653be-113">В hello портал Azure, можно найти hello безопасности сообщает о hello **Azure Active Directory** колонки в hello **безопасности** раздела.</span><span class="sxs-lookup"><span data-stu-id="653be-113">In hello Azure portal, you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span>  

![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="653be-115">Какая лицензия Azure AD необходимо tooaccess безопасности отчета?</span><span class="sxs-lookup"><span data-stu-id="653be-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="653be-116">Все выпуски Azure Active Directory предоставляют отчеты о пользователях, находящихся в группе риска.</span><span class="sxs-lookup"><span data-stu-id="653be-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="653be-117">Однако hello уровень детализации отчета может различаться между выпусками hello:</span><span class="sxs-lookup"><span data-stu-id="653be-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="653be-118">В hello **выпуски Azure Active Directory Free и Basic**, вы уже получить список пользователей, помеченных для риска.</span><span class="sxs-lookup"><span data-stu-id="653be-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="653be-119">Hello **Azure Active Directory Premium 1** edition расширяет возможности этой модели, также позволяя tooexamine некоторых hello базового события рисков, которые были обнаружены для каждого отчета.</span><span class="sxs-lookup"><span data-stu-id="653be-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="653be-120">Hello **Azure Active Directory Premium 2** выпуск предлагает вам hello наиболее подробные сведения обо всех событиях риска, базовый и позволяет tooconfigure политик безопасности, которые автоматически реагировать tooconfigured риска уровни.</span><span class="sxs-lookup"><span data-stu-id="653be-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="653be-121">Выпуски "Бесплатный" и "Базовый" Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="653be-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="653be-122">Hello пользователей, помеченных для риска отчета в свободной и основные выпуски hello Azure Active Directory предоставляет список учетных записей пользователей, которые могли быть скомпрометированы.</span><span class="sxs-lookup"><span data-stu-id="653be-122">hello users flagged for risk report in hello Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="653be-124">При выборе пользователя открывает колонку данные соответствующих пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="653be-124">Selecting a user opens hello related user data blade.</span></span>
<span data-ttu-id="653be-125">Для пользователей, которые находятся под угрозой можно просмотреть журнал вход пользователя hello и сбросить пароль hello, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="653be-125">For users that are at risk, you can review hello user’s sign-in history and reset hello password if necessary.</span></span>

![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="653be-127">Это диалоговое окно предоставляет следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="653be-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="653be-128">Загрузить отчет hello</span><span class="sxs-lookup"><span data-stu-id="653be-128">Download hello report</span></span>

- <span data-ttu-id="653be-129">Поиск пользователей</span><span class="sxs-lookup"><span data-stu-id="653be-129">Search users</span></span>

![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="653be-131">Выпуски Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="653be-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="653be-132">Hello пользователей, помеченных для отчета риска в выпуски premium hello Azure Active Directory обеспечивает:</span><span class="sxs-lookup"><span data-stu-id="653be-132">hello users flagged for risk report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="653be-133">[Список учетных записей пользователей](active-directory-identityprotection.md#users-flagged-for-risk), которые, возможно, были скомпрометированы.</span><span class="sxs-lookup"><span data-stu-id="653be-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="653be-134">Статистической информации о hello [типы событий риска](active-directory-identity-protection-risk-events.md) , обнаружены</span><span class="sxs-lookup"><span data-stu-id="653be-134">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="653be-135">Параметр toodownload hello отчета</span><span class="sxs-lookup"><span data-stu-id="653be-135">An option toodownload hello report</span></span>

- <span data-ttu-id="653be-136">Параметр tooconfigure [политика исправления риск пользователя](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="653be-136">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="653be-138">При выборе пользователя отображается подробное представление отчета об этом пользователе, предоставляющее перечисленные ниже возможности.</span><span class="sxs-lookup"><span data-stu-id="653be-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="653be-139">Просмотреть все входы откройте hello</span><span class="sxs-lookup"><span data-stu-id="653be-139">Open hello All sign-ins view</span></span>

- <span data-ttu-id="653be-140">Сброс пароля пользователя hello</span><span class="sxs-lookup"><span data-stu-id="653be-140">Reset hello user's password</span></span>

- <span data-ttu-id="653be-141">Отклонение всех событий.</span><span class="sxs-lookup"><span data-stu-id="653be-141">Dismiss all events</span></span>

- <span data-ttu-id="653be-142">Проанализируйте обнаруженную риск события для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="653be-142">Investigate reported risk events for hello user.</span></span> 


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="653be-144">tooinvestigate события риска, выберите один из hello tooopen список hello **сведения** колонку для этого события риска.</span><span class="sxs-lookup"><span data-stu-id="653be-144">tooinvestigate a risk event, select one from hello list tooopen hello **Details** blade for this risk event.</span></span> <span data-ttu-id="653be-145">На hello **сведения** колонки, у вас есть параметр tooeither hello [вручную закрыть события риска](active-directory-identityprotection.md#closing-risk-events-manually) или повторно активировать событие вручную закрытого риска.</span><span class="sxs-lookup"><span data-stu-id="653be-145">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="653be-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="653be-147">Next steps</span></span>

- <span data-ttu-id="653be-148">Дополнительные сведения о защите идентификации Azure см. в статье [Защита идентификации Azure Active Directory](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="653be-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

