---
title: "отчет aaaRisky входа в систему на портале Azure Active Directory hello | Документы Microsoft"
description: "Дополнительные сведения об отчете hello рискованным входа в систему на портале Azure Active Directory hello"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="21b29-103">Рискованные входы отчетов на портале Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="21b29-103">Risky sign-ins report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="21b29-104">Hello безопасности отчетов в Azure Active Directory (Azure AD) позволяет получить представление о вероятности hello скомпрометированных учетных записей в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="21b29-104">With hello security reports in Azure Active Directory (Azure AD) you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="21b29-105">Azure AD обнаруживает подозрительные действия, которые являются связанные tooyour учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="21b29-105">Azure AD detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="21b29-106">Для каждого обнаруженного действия создается запись, которая называется *событием риска*.</span><span class="sxs-lookup"><span data-stu-id="21b29-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="21b29-107">Дополнительные сведения см. в статье о [событиях риска в Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="21b29-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="21b29-108">Hello обнаружил, что риск события, используемые toocalculate:</span><span class="sxs-lookup"><span data-stu-id="21b29-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="21b29-109">**Рискованные входы** -рискованным вход является показателем для попытки входа, возможно, выполнены с тем, кто не hello законный владельцем учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="21b29-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="21b29-110">Дополнительные сведения см. в [этом разделе](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="21b29-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="21b29-111">**Пользователи, находящиеся в группе риска**. Такая пометка означает, что конфиденциальность учетной записи пользователя, возможно, нарушена.</span><span class="sxs-lookup"><span data-stu-id="21b29-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="21b29-112">Дополнительные сведения см. в разделе о [пользователях, находящихся в группе риска](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="21b29-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="21b29-113">В [hello портал Azure](https://portal.azure.com), можно найти hello безопасности сообщает о hello **Azure Active Directory** колонки в hello **безопасности** раздела.</span><span class="sxs-lookup"><span data-stu-id="21b29-113">In [hello Azure portal](https://portal.azure.com), you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span> 

![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="21b29-115">Какая лицензия Azure AD необходимо tooaccess безопасности отчета?</span><span class="sxs-lookup"><span data-stu-id="21b29-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="21b29-116">Все выпуски Azure Active Directory предоставляют отчеты о событиях входа, представляющих риск.</span><span class="sxs-lookup"><span data-stu-id="21b29-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="21b29-117">Однако hello уровень детализации отчета может различаться между выпусками hello:</span><span class="sxs-lookup"><span data-stu-id="21b29-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="21b29-118">В hello **выпуски Azure Active Directory Free и Basic**, появляется список рискованным входа в систему.</span><span class="sxs-lookup"><span data-stu-id="21b29-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="21b29-119">Hello **Azure Active Directory Premium 1** edition расширяет возможности этой модели, также позволяя tooexamine некоторых hello базового события рисков, которые были обнаружены для каждого отчета.</span><span class="sxs-lookup"><span data-stu-id="21b29-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="21b29-120">Hello **Azure Active Directory Premium 2** обеспечивает с hello наиболее подробные сведения обо всех событиях риска, базовый и позволяет также tooconfigure политики безопасности, которые автоматически отвечать tooconfigured уровней риска.</span><span class="sxs-lookup"><span data-stu-id="21b29-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="21b29-121">Выпуски "Бесплатный" и "Базовый" Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21b29-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="21b29-122">Hello Azure Active Directory free и basic Edition позволяют список рискованным входа в систему, обнаруженных для пользователей.</span><span class="sxs-lookup"><span data-stu-id="21b29-122">hello Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="21b29-123">В этом отчете указаны:</span><span class="sxs-lookup"><span data-stu-id="21b29-123">This report lists:</span></span>

- <span data-ttu-id="21b29-124">**Пользователь** - hello имя пользователя hello, который использовался во время операции входа hello</span><span class="sxs-lookup"><span data-stu-id="21b29-124">**User** - hello name of hello user that was used during hello sign-in operation</span></span>
- <span data-ttu-id="21b29-125">**IP** -hello IP-адрес устройства hello, используемые tooconnect tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21b29-125">**IP** - hello IP address of hello device that was used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="21b29-126">**Расположение** -использовать расположение hello tooconnect tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21b29-126">**Location** - hello location used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="21b29-127">**Время входа сохраняются** -hello время вход hello копии</span><span class="sxs-lookup"><span data-stu-id="21b29-127">**Sign-in time** - hello time when hello sign-in was performed</span></span>
- <span data-ttu-id="21b29-128">**Состояние** -hello состояние hello входа в систему</span><span class="sxs-lookup"><span data-stu-id="21b29-128">**Status** - hello status of hello sign-in</span></span>


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="21b29-130">На основании изучение hello рискованным вход, можно предоставить отзыв tooAzure Active Directory в форме hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="21b29-130">Based on your investigation of hello risky sign-in, you can provide feedback tooAzure Active Directory in form of hello following actions:</span></span>

- <span data-ttu-id="21b29-131">Разрешить</span><span class="sxs-lookup"><span data-stu-id="21b29-131">Resolve</span></span>
- <span data-ttu-id="21b29-132">Пометить как ложное срабатывание</span><span class="sxs-lookup"><span data-stu-id="21b29-132">Mark as false positive</span></span>
- <span data-ttu-id="21b29-133">Игнорировать</span><span class="sxs-lookup"><span data-stu-id="21b29-133">Ignore</span></span>
- <span data-ttu-id="21b29-134">Повторно активировать</span><span class="sxs-lookup"><span data-stu-id="21b29-134">Reactivate</span></span>

![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="21b29-136">Дополнительные сведения см. в разделе [Закрытие событий риска вручную](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="21b29-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="21b29-137">Этот отчет предоставляет следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="21b29-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="21b29-138">поиск ресурсов;</span><span class="sxs-lookup"><span data-stu-id="21b29-138">Searh resources</span></span>
- <span data-ttu-id="21b29-139">Загрузить данные отчета hello</span><span class="sxs-lookup"><span data-stu-id="21b29-139">Download hello report data</span></span>


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="21b29-141">Выпуски Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="21b29-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="21b29-142">отчет рискованным входы Hello в выпуски premium hello Azure Active Directory обеспечивает:</span><span class="sxs-lookup"><span data-stu-id="21b29-142">hello risky sign-ins report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="21b29-143">Статистической информации о hello [типы событий риска](active-directory-identity-protection-risk-events.md) , обнаружены</span><span class="sxs-lookup"><span data-stu-id="21b29-143">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="21b29-144">Параметр toodownload hello отчета</span><span class="sxs-lookup"><span data-stu-id="21b29-144">An option toodownload hello report</span></span>


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="21b29-146">При выборе события риска отображается подробное представление отчета об этом событии, предоставляющее перечисленные ниже возможности.</span><span class="sxs-lookup"><span data-stu-id="21b29-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="21b29-147">Параметр tooconfigure [политика исправления риск пользователя](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="21b29-147">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="21b29-148">Просмотрите hello обнаружения временная шкала событий риска hello</span><span class="sxs-lookup"><span data-stu-id="21b29-148">Review hello detection timeline for hello risk event</span></span>  

- <span data-ttu-id="21b29-149">Просмотр списка пользователей, для которых было обнаружено это событие риска.</span><span class="sxs-lookup"><span data-stu-id="21b29-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="21b29-150">[Ручное закрытие события риска](active-directory-identityprotection.md#closing-risk-events-manually) или повторная активация события риска, закрытого вручную.</span><span class="sxs-lookup"><span data-stu-id="21b29-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="21b29-152">При выборе пользователя отображается подробное представление отчета об этом пользователе, предоставляющее перечисленные ниже возможности.</span><span class="sxs-lookup"><span data-stu-id="21b29-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="21b29-153">Просмотреть все входы откройте hello</span><span class="sxs-lookup"><span data-stu-id="21b29-153">Open hello All sign-ins view</span></span>

- <span data-ttu-id="21b29-154">Сброс пароля пользователя hello</span><span class="sxs-lookup"><span data-stu-id="21b29-154">Reset hello user's password</span></span>

- <span data-ttu-id="21b29-155">Отклонение всех событий.</span><span class="sxs-lookup"><span data-stu-id="21b29-155">Dismiss all events</span></span>

- <span data-ttu-id="21b29-156">Проанализируйте обнаруженную риск события для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="21b29-156">Investigate reported risk events for hello user.</span></span> 


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="21b29-158">tooinvestigate события риска, выберите его из списка hello.</span><span class="sxs-lookup"><span data-stu-id="21b29-158">tooinvestigate a risk event, select one from hello list.</span></span>  
<span data-ttu-id="21b29-159">При этом откроется hello **сведения** колонку для этого события риска.</span><span class="sxs-lookup"><span data-stu-id="21b29-159">This opens hello **Details** blade for this risk event.</span></span> <span data-ttu-id="21b29-160">На hello **сведения** колонки, у вас есть параметр tooeither hello [вручную закрыть события риска](active-directory-identityprotection.md#closing-risk-events-manually) или повторно активировать событие вручную закрытого риска.</span><span class="sxs-lookup"><span data-stu-id="21b29-160">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="21b29-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="21b29-162">Next steps</span></span>

- <span data-ttu-id="21b29-163">Дополнительные сведения о защите идентификации Azure см. в статье [Защита идентификации Azure Active Directory](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="21b29-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

