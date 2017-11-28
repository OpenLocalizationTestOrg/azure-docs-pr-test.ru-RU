---
title: "aaaAzure Active Directory подтверждения концепции репертуара введение | Документы Microsoft"
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
ms.openlocfilehash: 655524e9692de46e831fc68e1636e6c20d41958f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="b340c-104">Сборник тренировочных заданий по подтверждению концепции для Azure Active Directory: введение</span><span class="sxs-lookup"><span data-stu-id="b340c-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="b340c-105">Эта статья содержит рекомендации по возможности tooexplore другой Azure AD в экспериментальную (проверки концепции).</span><span class="sxs-lookup"><span data-stu-id="b340c-105">This article provides guidelines tooexplore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="b340c-106">аудитория данного документа — удостоверение архитекторов, ИТ-специалистов и системным интеграторам нужной Hello</span><span class="sxs-lookup"><span data-stu-id="b340c-106">hello intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-toouse-this-playbook"></a><span data-ttu-id="b340c-107">Как toouse этот репертуара</span><span class="sxs-lookup"><span data-stu-id="b340c-107">How toouse this Playbook</span></span>

1. <span data-ttu-id="b340c-108">Используйте hello [темы](active-directory-playbook-ingredients.md#theme) раздела и выбрать фона hello интерес в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="b340c-108">Use hello [Theme](active-directory-playbook-ingredients.md#theme) section and pick hello area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="b340c-109">Область hello подтверждения концепции, выбрав hello сценарии, которые соответствуют бизнес-целей.</span><span class="sxs-lookup"><span data-stu-id="b340c-109">Scope hello PoC by choosing hello scenarios that align with your business goals.</span></span> <span data-ttu-id="b340c-110">Hello короткий hello лучше.</span><span class="sxs-lookup"><span data-stu-id="b340c-110">hello shorter hello better.</span></span> <span data-ttu-id="b340c-111">Мы рекомендуем делать его как короткий и наглядной значение hello возможных tooconvey toohello заинтересованных лиц, сводя к минимуму hello сложности toorealize его.</span><span class="sxs-lookup"><span data-stu-id="b340c-111">We recommend doing it as short and concise as possible tooconvey hello value toohello stakeholders while minimizing hello complexity toorealize it.</span></span>  
3. <span data-ttu-id="b340c-112">Используйте hello [реализацию](active-directory-playbook-implementation.md) раздел toounderstand hello сценарии и что они будут означают для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="b340c-112">Use hello [Implementation](active-directory-playbook-implementation.md) section toounderstand hello scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="b340c-113">В каждом сценарии описывается как tooset его (называемый [стандартные блоки](active-directory-playbook-building-blocks.md)), и как toonavigate hello сценариев.</span><span class="sxs-lookup"><span data-stu-id="b340c-113">In each scenario, we describe how tooset it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how toonavigate hello scenarios.</span></span> 
4. <span data-ttu-id="b340c-114">Каждый стандартный блок описывается hello предварительных требований, а также примерное время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b340c-114">Each building block explains hello pre-requisites needed, as well as an approximate time toocomplete.</span></span> <span data-ttu-id="b340c-115">Это поможет вам во время процесса планирования hello.</span><span class="sxs-lookup"><span data-stu-id="b340c-115">This can help you during hello planning process.</span></span> 
5. <span data-ttu-id="b340c-116">На основе 1-3 выше, определяют hello [среды](active-directory-playbook-ingredients.md#environment) в какой tooexecute.</span><span class="sxs-lookup"><span data-stu-id="b340c-116">Based on 1-3 Above, define hello [Environment](active-directory-playbook-ingredients.md#environment) in which tooexecute.</span></span> <span data-ttu-id="b340c-117">Мы рекомендуем toostrive для рабочей среды tooget хорошо вида hello качества для пользователей.</span><span class="sxs-lookup"><span data-stu-id="b340c-117">We encourage toostrive for a production environment tooget a good feel of hello experience for your users.</span></span> 
6. <span data-ttu-id="b340c-118">Если какие-то требования противоречат друг другу, то воспользуйтесь следующими принципами:</span><span class="sxs-lookup"><span data-stu-id="b340c-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="b340c-119">отображение значения ориентировано на тему;</span><span class="sxs-lookup"><span data-stu-id="b340c-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="b340c-120">Сценарии гладкости tooprepare tooset вверх и tooexecute hello</span><span class="sxs-lookup"><span data-stu-id="b340c-120">Smoothness tooprepare, tooset up, and tooexecute hello scenarios</span></span> 
   * <span data-ttu-id="b340c-121">Минимальное время tooexecute hello целевые сценарии</span><span class="sxs-lookup"><span data-stu-id="b340c-121">Minimal time tooexecute hello target scenarios</span></span> 
   * <span data-ttu-id="b340c-122">Как закрыть tooproduction как можно в рамках вашей ограничений</span><span class="sxs-lookup"><span data-stu-id="b340c-122">As close tooproduction as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="b340c-123">В данной статьей упоминаются некоторые приложения и продукты сторонних разработчиков, которые проводятся в качестве примеров для удобства.</span><span class="sxs-lookup"><span data-stu-id="b340c-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="b340c-124">Azure AD поддерживает тысячи приложений из нашей [коллекции приложений](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps), которые вы можете использовать с учетом среды и имеющихся потребностей.</span><span class="sxs-lookup"><span data-stu-id="b340c-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]