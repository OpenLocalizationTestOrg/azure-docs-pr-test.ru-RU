---
title: "службы aaaOffering стека Azure | Документы Microsoft"
description: "Оператор облака могут предлагать пользователям tooyour служб."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: 47cff8bfb202527ae4c930c7d1b9eb3998bee85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-offering-services-in-azure-stack"></a><span data-ttu-id="0a6c0-103">Обзор предложения службы в стек Azure</span><span class="sxs-lookup"><span data-stu-id="0a6c0-103">Overview of offering services in Azure Stack</span></span>

<span data-ttu-id="0a6c0-104">Стек Microsoft Azure — гибридного облачная платформа, которая позволяет вам предоставлять службы из центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-104">Microsoft Azure Stack is a hybrid cloud platform that lets you deliver services from your datacenter.</span></span> <span data-ttu-id="0a6c0-105">Как поставщик услуг можно предложить клиентам tooyour служб.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-105">As a service provider, you can offer services tooyour tenants.</span></span> <span data-ttu-id="0a6c0-106">В рамках бизнес- или государственным учреждением можно предложить сотрудников tooyour локальной службы.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-106">Within a business or government agency, you can offer on-premises services tooyour employees.</span></span> <span data-ttu-id="0a6c0-107">Hello услуги можно со включают, но не ограничиваются:</span><span class="sxs-lookup"><span data-stu-id="0a6c0-107">hello services that you can deliver include, but are not limited to:</span></span>

- <span data-ttu-id="0a6c0-108">Службы приложений, мобильные приложения, приложения API, API-функций, SQL, MySQL, например платформы как услуги (PaaS).</span><span class="sxs-lookup"><span data-stu-id="0a6c0-108">Platform as a Service (PaaS) services like App Services, Mobile Apps, API Apps, API Functions, SQL, MySQL.</span></span>
- <span data-ttu-id="0a6c0-109">Программное обеспечение как услуга (SaaS) служб, как Sharepoint.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-109">Software as a Service (SaaS) services like Sharepoint.</span></span>

<span data-ttu-id="0a6c0-110">Можно даже объединять toointegrate службы и создания сложных решений для различных пользователей.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-110">You can even combine services toointegrate and build complex solutions for different users.</span></span>

<span data-ttu-id="0a6c0-111">toodeliver tooyour пользователей этих служб, необходимо создать [планы, предложений и квоты](azure-stack-plan-offer-quota-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a6c0-111">toodeliver these services tooyour users, you must create [plans, offers, and quotas](azure-stack-plan-offer-quota-overview.md).</span></span> <span data-ttu-id="0a6c0-112">Пользователи затем могут подписаться toouse hello tooyour предложения службы.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-112">Your users can then subscribe tooyour offers toouse hello services.</span></span>

## <a name="plan-your-service-offers"></a><span data-ttu-id="0a6c0-113">Планирование предложения по обслуживанию</span><span class="sxs-lookup"><span data-stu-id="0a6c0-113">Plan your service offers</span></span>

<span data-ttu-id="0a6c0-114">При планировании вашего предложения, поддержания hello следующих соображений:</span><span class="sxs-lookup"><span data-stu-id="0a6c0-114">When you’re planning your offers, keep hello following points in mind:</span></span>

<span data-ttu-id="0a6c0-115">**Пробных версиях**: можно использовать пробных версиях tooattract новых пользователей, которые затем можно обновить tooadditional служб.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-115">**Trial offers**: You can use trial offers tooattract new users, who can then upgrade tooadditional services.</span></span> <span data-ttu-id="0a6c0-116">toocreate пробной версии, создать небольшое [базового плана](azure-stack-plan-offer-quota-overview.md#base-plan) с необязательным план более высокого надстройку.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-116">toocreate a trial offer, create a small [base plan](azure-stack-plan-offer-quota-overview.md#base-plan) with an optional larger add-on plan.</span></span>

<span data-ttu-id="0a6c0-117">**Планирование мощности**: может возникнуть вопрос о пользователях, достаточно большое количество ресурсов и переполнения hello системы для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-117">**Capacity planning**: You might be concerned about users grabbing large amounts of resources and clogging hello system for all users.</span></span> <span data-ttu-id="0a6c0-118">производительность toohelp, вы можете [настроить планы с квотами](azure-stack-plan-offer-quota-overview.md#plans) toocap использования.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-118">toohelp performance, you can [configure your plans with quotas](azure-stack-plan-offer-quota-overview.md#plans) toocap usage.</span></span>

<span data-ttu-id="0a6c0-119">**Делегировать поставщики**: можно предоставлять другим hello возможность toocreate предложения в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-119">**Delegated providers**: You can grant others hello ability toocreate offers in your environment.</span></span> <span data-ttu-id="0a6c0-120">Например, если вы являетесь поставщиком услуг, вы можете [делегировать](azure-stack-delegated-provider.md) торговые посредники tooyour этой возможности.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-120">For example, if you’re a service provider, you can [delegate](azure-stack-delegated-provider.md) this ability tooyour resellers.</span></span> <span data-ttu-id="0a6c0-121">Или, если вы организации, вы можете делегировать tooother подразделений и филиалов.</span><span class="sxs-lookup"><span data-stu-id="0a6c0-121">Or, if you’re an organization, you can delegate tooother divisions/subsidiaries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a6c0-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a6c0-122">Next steps</span></span>
[<span data-ttu-id="0a6c0-123">Дополнительные сведения о предложениях, планы, квоты и подписок</span><span class="sxs-lookup"><span data-stu-id="0a6c0-123">Learn more about offers, plans, quotas, and subscriptions</span></span>](azure-stack-plan-offer-quota-overview.md)

