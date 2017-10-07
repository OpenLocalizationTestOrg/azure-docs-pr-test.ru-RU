---
title: "Вопросы проектирования identity гибридных Active Directory aaaAzure - определить требования многофакторной проверки подлинности"
description: "С помощью элемента управления условного доступа Azure Active Directory проверяет hello определенных условий, выбранное при проверке подлинности пользователя hello и перед предоставлением доступа toohello приложения. Если эти условия выполнены, hello пользователя с проверкой подлинности и доступа toohello приложение, которому разрешен."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="3efc9-104">Определение требований к многофакторной проверке подлинности для решения гибридной идентификации</span><span class="sxs-lookup"><span data-stu-id="3efc9-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="3efc9-105">В мире мобильных пользователей, обращающихся к данным и приложениям в облаке hello и с любого устройства обеспечение безопасности этой информации становится первостепенное значение.</span><span class="sxs-lookup"><span data-stu-id="3efc9-105">In this world of mobility, with users accessing data and applications in hello cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="3efc9-106">Каждый день мы видим новости о взломе систем безопасности.</span><span class="sxs-lookup"><span data-stu-id="3efc9-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="3efc9-107">Хотя нет никакой гарантии для такой нарушений, многофакторной проверки подлинности обеспечивает дополнительный уровень безопасности toohelp предотвращения этих угроз.</span><span class="sxs-lookup"><span data-stu-id="3efc9-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security toohelp prevent these breaches.</span></span>
<span data-ttu-id="3efc9-108">Запустите по оценке требований организации hello многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3efc9-108">Start by evaluating hello organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="3efc9-109">То есть возможности идет toosecure hello организации.</span><span class="sxs-lookup"><span data-stu-id="3efc9-109">That is, what is hello organization trying toosecure.</span></span>  <span data-ttu-id="3efc9-110">Это вычисление является важные toodefine hello технические требования для установки и позволяет организациям hello многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3efc9-110">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="3efc9-111">Если вы не знакомы с многофакторной проверки Подлинности и действие, настоятельно рекомендуется прочитать статью hello [возможности многофакторной проверки подлинности Azure?](../multi-factor-authentication/multi-factor-authentication.md) предыдущих toocontinue прочтением этого раздела.</span><span class="sxs-lookup"><span data-stu-id="3efc9-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read hello article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior toocontinue reading this section.</span></span>
> 
> 

<span data-ttu-id="3efc9-112">Убедитесь, что tooanswer hello следующие:</span><span class="sxs-lookup"><span data-stu-id="3efc9-112">Make sure tooanswer hello following:</span></span>

* <span data-ttu-id="3efc9-113">Ваша компания пытается toosecure приложения Майкрософт?</span><span class="sxs-lookup"><span data-stu-id="3efc9-113">Is your company trying toosecure Microsoft apps?</span></span> 
* <span data-ttu-id="3efc9-114">Как публикуются эти приложения?</span><span class="sxs-lookup"><span data-stu-id="3efc9-114">How these apps are published?</span></span>
* <span data-ttu-id="3efc9-115">Ваша компания предоставляет ли удаленного доступа tooallow сотрудников tooaccess локальных приложений?</span><span class="sxs-lookup"><span data-stu-id="3efc9-115">Does your company provide remote access tooallow employees tooaccess on-premises apps?</span></span>

<span data-ttu-id="3efc9-116">Если Да, какой тип удаленного доступа? Необходимо также tooevaluate, где будут размещены hello пользователи, осуществляющие доступ к этим приложениям.</span><span class="sxs-lookup"><span data-stu-id="3efc9-116">If yes, what type of remote access?You also need tooevaluate where hello users who are accessing these applications will be located.</span></span> <span data-ttu-id="3efc9-117">Эта оценка — это другой важный шаг toodefine hello правильную многофакторной проверки подлинности стратегия.</span><span class="sxs-lookup"><span data-stu-id="3efc9-117">This evaluation is another important step toodefine hello proper multi-factor authentication strategy.</span></span> <span data-ttu-id="3efc9-118">Убедитесь, что hello tooanswer следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="3efc9-118">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="3efc9-119">Где находятся пользователи hello будет toobe?</span><span class="sxs-lookup"><span data-stu-id="3efc9-119">Where are hello users going toobe located?</span></span>
* <span data-ttu-id="3efc9-120">Могут ли они быть расположены где угодно?</span><span class="sxs-lookup"><span data-stu-id="3efc9-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="3efc9-121">Компания будет расположение toohello пользователя в соответствии с ограничениями tooestablish?</span><span class="sxs-lookup"><span data-stu-id="3efc9-121">Does your company want tooestablish restrictions according toohello user’s location?</span></span>

<span data-ttu-id="3efc9-122">После ознакомления с этим требованиям, очень важно tooalso оценки требований к hello пользователя для многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3efc9-122">Once you understand these requirements, it is important tooalso evaluate hello user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="3efc9-123">Это вычисление важно, так как он будет определять hello требования для развертывания многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3efc9-123">This evaluation is important because it will define hello requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="3efc9-124">Убедитесь, что hello tooanswer следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="3efc9-124">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="3efc9-125">Hello пользователи знакомы с многофакторной проверкой подлинности?</span><span class="sxs-lookup"><span data-stu-id="3efc9-125">Are hello users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="3efc9-126">Некоторые варианты будут tooprovide требуется дополнительная проверка подлинности?</span><span class="sxs-lookup"><span data-stu-id="3efc9-126">Will some uses be required tooprovide additional authentication?</span></span>  
  * <span data-ttu-id="3efc9-127">Если Да, все hello время, если он поступает из внешних сетей, или доступ к конкретным приложениям или при других условиях?</span><span class="sxs-lookup"><span data-stu-id="3efc9-127">If yes, all hello time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="3efc9-128">Hello пользователям потребуется обучения о том, как toosetup и реализуйте многофакторной проверки подлинности?</span><span class="sxs-lookup"><span data-stu-id="3efc9-128">Will hello users require training on how toosetup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="3efc9-129">Каковы основные сценарии hello, что ваша компания хочет tooenable многофакторной проверки подлинности для пользователей?</span><span class="sxs-lookup"><span data-stu-id="3efc9-129">What are hello key scenarios that your company wants tooenable multi-factor authentication for their users?</span></span>

<span data-ttu-id="3efc9-130">После ответа на предыдущие вопросы hello, будет может toounderstand при наличии многофакторной проверки подлинности уже реализован в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="3efc9-130">After answering hello previous questions, you will be able toounderstand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="3efc9-131">Это вычисление является важные toodefine hello технические требования для установки и позволяет организациям hello многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3efc9-131">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span> <span data-ttu-id="3efc9-132">Убедитесь, что hello tooanswer следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="3efc9-132">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="3efc9-133">Требуется ли вашей компании tooprotect привилегированные учетные записи с многофакторной проверки Подлинности?</span><span class="sxs-lookup"><span data-stu-id="3efc9-133">Does your company need tooprotect privileged accounts with MFA?</span></span>
* <span data-ttu-id="3efc9-134">Нужна ли вашей компании tooenable многофакторной проверки Подлинности для определенных приложений в целях соответствия требованиям?</span><span class="sxs-lookup"><span data-stu-id="3efc9-134">Does your company need tooenable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="3efc9-135">Требуется ли вашей компании tooenable многофакторной проверки Подлинности для всех подходящих пользователей из этих приложений или только администраторы?</span><span class="sxs-lookup"><span data-stu-id="3efc9-135">Does your company need tooenable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="3efc9-136">Требуется у вас всегда включена многофакторной проверки Подлинности и только тогда, когда пользователи hello регистрируются за пределами корпоративной сети?</span><span class="sxs-lookup"><span data-stu-id="3efc9-136">Do you need have MFA always enabled or only when hello users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="3efc9-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3efc9-137">Next steps</span></span>
[<span data-ttu-id="3efc9-138">Определение стратегии внедрения гибридной идентификации</span><span class="sxs-lookup"><span data-stu-id="3efc9-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="3efc9-139">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="3efc9-139">See also</span></span>
[<span data-ttu-id="3efc9-140">Обзор рекомендаций по проектированию</span><span class="sxs-lookup"><span data-stu-id="3efc9-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

