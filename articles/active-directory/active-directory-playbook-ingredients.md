---
title: "aaaAzure компоненты репертуара подтверждения концепции Active Directory | Документы Microsoft"
description: "Ознакомление со сценариями управления удостоверениями и доступом и их реализация"
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
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="7b332-104">Сборник тренировочных заданий по подтверждению концепции для Azure Active Directory: ингредиенты</span><span class="sxs-lookup"><span data-stu-id="7b332-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="7b332-105">Тема</span><span class="sxs-lookup"><span data-stu-id="7b332-105">Theme</span></span>
<span data-ttu-id="7b332-106">Azure AD предоставляет решения, удостоверение и доступ через несколько областей в hello enterprise.</span><span class="sxs-lookup"><span data-stu-id="7b332-106">Azure AD provides identity and access solutions across multiple areas in hello enterprise.</span></span> <span data-ttu-id="7b332-107">Мы классифицировать сценариев hello в hello в следующих областях:</span><span class="sxs-lookup"><span data-stu-id="7b332-107">We classify hello scenarios in hello following areas:</span></span> 

* [<span data-ttu-id="7b332-108">Большое количество приложений, одно удостоверение</span><span class="sxs-lookup"><span data-stu-id="7b332-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="7b332-109">Повышение уровня безопасности</span><span class="sxs-lookup"><span data-stu-id="7b332-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="7b332-110">Самостоятельное масштабирование</span><span class="sxs-lookup"><span data-stu-id="7b332-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="7b332-111">Определение типа темы tooframe hello подтверждения концепции помогает toofocus hello усилия, нацелены с бизнес-целей, который зачастую и триггеры hello hello интересуют пробная версия на первом месте hello.</span><span class="sxs-lookup"><span data-stu-id="7b332-111">Defining a theme tooframe hello PoC helps toofocus hello efforts that resonates with business goals, which oftentimes are hello triggers of hello interest in a proof of concept in hello first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="7b332-112">Среда</span><span class="sxs-lookup"><span data-stu-id="7b332-112">Environment</span></span>

<span data-ttu-id="7b332-113">Это важные toodetermine сведения hello hello среды, где будет доставлять hello подтверждения концепции.</span><span class="sxs-lookup"><span data-stu-id="7b332-113">It is important toodetermine hello details of hello environment where you will deliver hello PoC.</span></span> <span data-ttu-id="7b332-114">В идеале можно создавать на нем после hello подтверждения концепции будет выполнено.</span><span class="sxs-lookup"><span data-stu-id="7b332-114">Ideally you can build upon it after hello PoC is completed.</span></span> <span data-ttu-id="7b332-115">Важно Hello целевая среда и необходимо найти баланс между что делает ее как реальные максимально и издержки hello ограничения или Дополнительные соображения hello.</span><span class="sxs-lookup"><span data-stu-id="7b332-115">hello target environment is crucial and you should find hello right balance between making it as real as possible and hello overhead of constraints or extra considerations.</span></span> <span data-ttu-id="7b332-116">Стандартные среды Hello для PoCs являются:</span><span class="sxs-lookup"><span data-stu-id="7b332-116">hello typical environments for PoCs are:</span></span>
* <span data-ttu-id="7b332-117">**Порождение:** hello сценарии будут реализованы в динамической среде и уже развернуты облачные службы Майкрософт (производство AD, Office 365, решение клиента и единого входа Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b332-117">**Production:** hello scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="7b332-118">**Пользовательский тест приемки (UAT) или среда разработки.** Вам предоставляется инфраструктура тестирования (параллельная среда AD и потенциальный клиент Azure AD или решение единого входа) с тестовыми данными, напоминающими рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="7b332-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="7b332-119">Как правило hello тестовой среде совместно используется несколькими проектами предприятии hello.</span><span class="sxs-lookup"><span data-stu-id="7b332-119">Typically, hello test environment is shared across multiple projects in hello enterprise.</span></span>

<span data-ttu-id="7b332-120">Большинство сценариев в этом руководстве аддитивно по своей природе.</span><span class="sxs-lookup"><span data-stu-id="7b332-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="7b332-121">В результате они могут развертываться в клиенте производственного hello без влияния на пользователей за пределами hello подтверждения концепции.</span><span class="sxs-lookup"><span data-stu-id="7b332-121">As a result, they can be deployed in hello production tenant without affecting users outside hello PoC.</span></span> <span data-ttu-id="7b332-122">В этом документе мы будем отмечать, какие сценарии могут оказывать влияние на работу клиента.</span><span class="sxs-lookup"><span data-stu-id="7b332-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="7b332-123">В таких случаях может потребоваться tooconsider нерабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7b332-123">In those cases, you might want tooconsider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="7b332-124">Целевые пользователи</span><span class="sxs-lookup"><span data-stu-id="7b332-124">Target Users</span></span>

<span data-ttu-id="7b332-125">Это важные toodetermine hello целевой набор пользователей, которым будет использоваться для сценариев hello, особенно в том случае, когда hello среды производственного или тестирования.</span><span class="sxs-lookup"><span data-stu-id="7b332-125">It is important toodetermine hello target set of users that will exercise hello scenarios, especially when hello environment is production or test.</span></span> <span data-ttu-id="7b332-126">перечислены категории Hello целевых пользователей для проверки концепции.</span><span class="sxs-lookup"><span data-stu-id="7b332-126">hello categories of target users for PoC are:</span></span>
* <span data-ttu-id="7b332-127">**Пилотных пользователей:** реальных пользователей в среде hello, которая будет использоваться с учетной записью hello, они будут использовать для их tooday день решение hello должностных обязанностей</span><span class="sxs-lookup"><span data-stu-id="7b332-127">**Pilot Users:** Real users in hello environment that will be using hello solution with hello account they use for their day tooday job functions</span></span>
* <span data-ttu-id="7b332-128">**Тестовых пользователей:** тестовые учетные записи, созданные в среде hello</span><span class="sxs-lookup"><span data-stu-id="7b332-128">**Test Users:** Test accounts created in hello environment</span></span> 

<span data-ttu-id="7b332-129">Большинство сценариев в этом руководстве может быть выполнено пилотными пользователями.</span><span class="sxs-lookup"><span data-stu-id="7b332-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="7b332-130">В этом документе мы будем при необходимости отмечать целевых пользователей, в отношении которых есть особые рекомендации.</span><span class="sxs-lookup"><span data-stu-id="7b332-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]