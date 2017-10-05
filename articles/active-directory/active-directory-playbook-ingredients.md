---
title: "Сборник тренировочных заданий по PoC для Azure Active Directory: ингредиенты | Документация Майкрософт"
description: "Ознакомление со сценариями управления удостоверениями и доступом, а также их реализация."
services: active-directory
keywords: "azure active directory, сборник тренировочных заданий, подтверждение концепции, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: d2a0fe280f143d390f5e4ba40e0ebe92d8a4a837
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="63483-104">Сборник тренировочных заданий по подтверждению концепции для Azure Active Directory: ингредиенты</span><span class="sxs-lookup"><span data-stu-id="63483-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="63483-105">Тема</span><span class="sxs-lookup"><span data-stu-id="63483-105">Theme</span></span>
<span data-ttu-id="63483-106">Azure AD предоставляет решения для управления удостоверениями и доступом по нескольким областям предприятия.</span><span class="sxs-lookup"><span data-stu-id="63483-106">Azure AD provides identity and access solutions across multiple areas in the enterprise.</span></span> <span data-ttu-id="63483-107">Мы классифицируем сценарии по следующим областям:</span><span class="sxs-lookup"><span data-stu-id="63483-107">We classify the scenarios in the following areas:</span></span> 

* [<span data-ttu-id="63483-108">Большое количество приложений, одно удостоверение</span><span class="sxs-lookup"><span data-stu-id="63483-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="63483-109">Повышение уровня безопасности</span><span class="sxs-lookup"><span data-stu-id="63483-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="63483-110">Самостоятельное масштабирование</span><span class="sxs-lookup"><span data-stu-id="63483-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="63483-111">Определение темы для PoC помогает сконцентрировать усилия, что перекликается с бизнес-целями, которые зачастую являются главными триггерами интереса к подтверждению концепции.</span><span class="sxs-lookup"><span data-stu-id="63483-111">Defining a theme to frame the PoC helps to focus the efforts that resonates with business goals, which oftentimes are the triggers of the interest in a proof of concept in the first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="63483-112">Среда</span><span class="sxs-lookup"><span data-stu-id="63483-112">Environment</span></span>

<span data-ttu-id="63483-113">Важно детально определить среду, в которой будет реализовываться подтверждение концепции.</span><span class="sxs-lookup"><span data-stu-id="63483-113">It is important to determine the details of the environment where you will deliver the PoC.</span></span> <span data-ttu-id="63483-114">В идеале на ее основе можно будет продолжить работу после выполнения PoC.</span><span class="sxs-lookup"><span data-stu-id="63483-114">Ideally you can build upon it after the PoC is completed.</span></span> <span data-ttu-id="63483-115">Целевая среда является критически важной, поэтому необходимо найти правильный баланс между ее максимальной реалистичностью и необходимостью учитывать различные ограничения и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="63483-115">The target environment is crucial and you should find the right balance between making it as real as possible and the overhead of constraints or extra considerations.</span></span> <span data-ttu-id="63483-116">Ниже описаны типичные среды для PoC.</span><span class="sxs-lookup"><span data-stu-id="63483-116">The typical environments for PoCs are:</span></span>
* <span data-ttu-id="63483-117">**Рабочая среда.** Сценарии будут реализованы в динамической среде с использованием уже развернутых облачных служб Майкрософт (рабочая среда AD, Office 365, клиент Azure AD или решение единого входа).</span><span class="sxs-lookup"><span data-stu-id="63483-117">**Production:** The scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="63483-118">**Пользовательский тест приемки (UAT) или среда разработки.** Вам предоставляется инфраструктура тестирования (параллельная среда AD и потенциальный клиент Azure AD или решение единого входа) с тестовыми данными, напоминающими рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="63483-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="63483-119">Как правило, тестовая среда совместно используется несколькими проектами на предприятии.</span><span class="sxs-lookup"><span data-stu-id="63483-119">Typically, the test environment is shared across multiple projects in the enterprise.</span></span>

<span data-ttu-id="63483-120">Большинство сценариев в этом руководстве аддитивно по своей природе.</span><span class="sxs-lookup"><span data-stu-id="63483-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="63483-121">Поэтому их можно развернуть в рабочем клиенте без влияния на работу пользователей за пределами PoC.</span><span class="sxs-lookup"><span data-stu-id="63483-121">As a result, they can be deployed in the production tenant without affecting users outside the PoC.</span></span> <span data-ttu-id="63483-122">В этом документе мы будем отмечать, какие сценарии могут оказывать влияние на работу клиента.</span><span class="sxs-lookup"><span data-stu-id="63483-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="63483-123">Для таких случаев вы можете использовать другую (не рабочую) среду.</span><span class="sxs-lookup"><span data-stu-id="63483-123">In those cases, you might want to consider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="63483-124">Целевые пользователи</span><span class="sxs-lookup"><span data-stu-id="63483-124">Target Users</span></span>

<span data-ttu-id="63483-125">Важно определить целевой набор пользователей, которые будут испытывать эти сценарии, в частности, когда среда является рабочей или тестовой.</span><span class="sxs-lookup"><span data-stu-id="63483-125">It is important to determine the target set of users that will exercise the scenarios, especially when the environment is production or test.</span></span> <span data-ttu-id="63483-126">Ниже описаны категории целевых пользователей для PoC:</span><span class="sxs-lookup"><span data-stu-id="63483-126">The categories of target users for PoC are:</span></span>
* <span data-ttu-id="63483-127">**Пилотные пользователи.** Реальные пользователи в среде, которые будут использовать решение с учетной записью, применяемой для ежедневных рабочих заданий.</span><span class="sxs-lookup"><span data-stu-id="63483-127">**Pilot Users:** Real users in the environment that will be using the solution with the account they use for their day to day job functions</span></span>
* <span data-ttu-id="63483-128">**Тестовые пользователи.** Тестовые учетные записи, созданные в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="63483-128">**Test Users:** Test accounts created in the environment</span></span> 

<span data-ttu-id="63483-129">Большинство сценариев в этом руководстве может быть выполнено пилотными пользователями.</span><span class="sxs-lookup"><span data-stu-id="63483-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="63483-130">В этом документе мы будем при необходимости отмечать целевых пользователей, в отношении которых есть особые рекомендации.</span><span class="sxs-lookup"><span data-stu-id="63483-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]