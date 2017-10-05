---
title: "Сборник тренировочных заданий по PoC для Azure Active Directory: введение | Документация Майкрософт"
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
ms.openlocfilehash: 567f3373594bc53435e8c0bd0a3445dd318af1cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="bdab0-104">Сборник тренировочных заданий по подтверждению концепции для Azure Active Directory: введение</span><span class="sxs-lookup"><span data-stu-id="bdab0-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="bdab0-105">Эта статья содержит рекомендации для ознакомления с различными возможностями Azure AD в области подтверждения концепции (PoC).</span><span class="sxs-lookup"><span data-stu-id="bdab0-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="bdab0-106">Целевой аудиторией данного документа являются архитекторы по идентификации, ИТ-специалисты и системные интеграторы.</span><span class="sxs-lookup"><span data-stu-id="bdab0-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-to-use-this-playbook"></a><span data-ttu-id="bdab0-107">Как использовать этот сборник тренировочных заданий</span><span class="sxs-lookup"><span data-stu-id="bdab0-107">How to use this Playbook</span></span>

1. <span data-ttu-id="bdab0-108">Используйте раздел [Тема](active-directory-playbook-ingredients.md#theme), чтобы выбрать интересующую вас область (или области), исходя из своих потребностей.</span><span class="sxs-lookup"><span data-stu-id="bdab0-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="bdab0-109">Ограничьте область подтверждения концепции, выбрав сценарии, соответствующие вашим бизнес-целям.</span><span class="sxs-lookup"><span data-stu-id="bdab0-109">Scope the PoC by choosing the scenarios that align with your business goals.</span></span> <span data-ttu-id="bdab0-110">Чем точнее, тем лучше.</span><span class="sxs-lookup"><span data-stu-id="bdab0-110">The shorter the better.</span></span> <span data-ttu-id="bdab0-111">Рекомендуется указать эти значения максимально коротко и четко, чтобы заинтересованные лица получили необходимые сведения, и при этом реализация была наименее сложной.</span><span class="sxs-lookup"><span data-stu-id="bdab0-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span></span>  
3. <span data-ttu-id="bdab0-112">Используйте раздел [Реализация](active-directory-playbook-implementation.md), чтобы разобраться в сценариях и их значении для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="bdab0-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="bdab0-113">В каждом сценарии мы описываем, как его настроить (то, что мы называем [стандартными блоками](active-directory-playbook-building-blocks.md)) и как перемещаться по сценариям.</span><span class="sxs-lookup"><span data-stu-id="bdab0-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span></span> 
4. <span data-ttu-id="bdab0-114">Для каждого стандартного блока указаны предварительные требования, а также примерное время выполнения.</span><span class="sxs-lookup"><span data-stu-id="bdab0-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span></span> <span data-ttu-id="bdab0-115">Эти сведения будут полезными в процессе планирования.</span><span class="sxs-lookup"><span data-stu-id="bdab0-115">This can help you during the planning process.</span></span> 
5. <span data-ttu-id="bdab0-116">В зависимости от значений, выбранных на шагах 1–3, определите [среду](active-directory-playbook-ingredients.md#environment) выполнения.</span><span class="sxs-lookup"><span data-stu-id="bdab0-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span></span> <span data-ttu-id="bdab0-117">По возможности следует использовать рабочую среду, чтобы получить лучшее представление о том, с чем сталкиваются ваши пользователи.</span><span class="sxs-lookup"><span data-stu-id="bdab0-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span></span> 
6. <span data-ttu-id="bdab0-118">Если какие-то требования противоречат друг другу, то воспользуйтесь следующими принципами:</span><span class="sxs-lookup"><span data-stu-id="bdab0-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="bdab0-119">отображение значения ориентировано на тему;</span><span class="sxs-lookup"><span data-stu-id="bdab0-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="bdab0-120">удобство подготовки, настройки и выполнения сценариев;</span><span class="sxs-lookup"><span data-stu-id="bdab0-120">Smoothness to prepare, to set up, and to execute the scenarios</span></span> 
   * <span data-ttu-id="bdab0-121">минимальная продолжительность выполнения целевых сценариев;</span><span class="sxs-lookup"><span data-stu-id="bdab0-121">Minimal time to execute the target scenarios</span></span> 
   * <span data-ttu-id="bdab0-122">максимальная приближенность к рабочей среде в рамках имеющихся ограничений.</span><span class="sxs-lookup"><span data-stu-id="bdab0-122">As close to production as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="bdab0-123">В данной статьей упоминаются некоторые приложения и продукты сторонних разработчиков, которые проводятся в качестве примеров для удобства.</span><span class="sxs-lookup"><span data-stu-id="bdab0-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="bdab0-124">Azure AD поддерживает тысячи приложений из нашей [коллекции приложений](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps), которые вы можете использовать с учетом среды и имеющихся потребностей.</span><span class="sxs-lookup"><span data-stu-id="bdab0-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]