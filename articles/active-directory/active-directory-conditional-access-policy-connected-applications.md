---
title: "политики условного доступа на основе устройств Azure Active Directory aaaConfigure | Документы Microsoft"
description: "Узнайте, как политики tooconfigure Azure Active Directory на основе устройств условного доступа."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="403a0-103">Настройка политик условного доступа на основе устройств для Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="403a0-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="403a0-104">Благодаря [условному доступу Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md) можно настроить доступ авторизованных пользователей к вашим ресурсам.</span><span class="sxs-lookup"><span data-stu-id="403a0-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="403a0-105">Например вы ограничиваете hello доступа toocertain ресурсов tootrusted устройств.</span><span class="sxs-lookup"><span data-stu-id="403a0-105">For example, you limit hello access toocertain resources tootrusted devices.</span></span> <span data-ttu-id="403a0-106">Политика условного доступа, требующая доверенного устройства, также называется политикой условного доступа на основе устройств.</span><span class="sxs-lookup"><span data-stu-id="403a0-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="403a0-107">Этот раздел предоставляет сведения в как условное устройства под управлением tooconfigure политик доступа для приложения Azure AD подключен.</span><span class="sxs-lookup"><span data-stu-id="403a0-107">This topic provides you with information on how tooconfigure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="403a0-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="403a0-108">Before you begin</span></span>

<span data-ttu-id="403a0-109">Условный доступ на основе устройств объединяет **условный доступ Azure AD** и **управление устройствами Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="403a0-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="403a0-110">Если вы еще не знакомы с одной из этих областей, следует прочитать следующие разделы, сначала hello:</span><span class="sxs-lookup"><span data-stu-id="403a0-110">If you are not familiar with one of these areas yet, you should read hello following topics, first:</span></span>

- <span data-ttu-id="403a0-111">**[Условный доступ в Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  -в этом разделе содержится с концептуальный обзор условного доступа и hello связанной терминологии.</span><span class="sxs-lookup"><span data-stu-id="403a0-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and hello related terminology.</span></span>

- <span data-ttu-id="403a0-112">**[Управление toodevice введение в Azure Active Directory](device-management-introduction.md)**  -в этом разделе дается обзор hello различных параметров у вас есть tooconnect устройствами с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="403a0-112">**[Introduction toodevice management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of hello various options you have tooconnect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="403a0-113">Доверенные устройства</span><span class="sxs-lookup"><span data-stu-id="403a0-113">Trusted devices</span></span>

<span data-ttu-id="403a0-114">В мире mobile сначала, облачный Azure Active Directory позволяет-toodevices приложений и служб из любого места.</span><span class="sxs-lookup"><span data-stu-id="403a0-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="403a0-115">Для некоторых ресурсов в вашей среде, предоставление доступа toohello пользователи не вполне достаточно.</span><span class="sxs-lookup"><span data-stu-id="403a0-115">For certain resources in your environment, granting access toohello right users might not be good enough.</span></span> <span data-ttu-id="403a0-116">В дополнение к этому toohello пользователи, вы может также потребоваться toobe доверенного устройства используемых tooaccess ресурса.</span><span class="sxs-lookup"><span data-stu-id="403a0-116">In addition toohello right users, you might also require a trusted device toobe used tooaccess a resource.</span></span> <span data-ttu-id="403a0-117">В вашей среде, можно определить, какие доверенное устройство, основываясь на hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="403a0-117">In your environment, you can define what a trusted device is based on hello following components:</span></span>

- <span data-ttu-id="403a0-118">Hello [платформ устройств](active-directory-conditional-access-azure-portal.md#device-platforms) на устройстве</span><span class="sxs-lookup"><span data-stu-id="403a0-118">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="403a0-119">Является ли устройство совместимым.</span><span class="sxs-lookup"><span data-stu-id="403a0-119">Whether a device is compliant</span></span>
- <span data-ttu-id="403a0-120">Подключено ли устройство к домену.</span><span class="sxs-lookup"><span data-stu-id="403a0-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="403a0-121">Hello [платформ устройств](active-directory-conditional-access-azure-portal.md#device-platforms) характеризуется hello операционной системы, на котором работает на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="403a0-121">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by hello operating system that is running on your device.</span></span> <span data-ttu-id="403a0-122">В политике условного доступа на основе устройств можно ограничить доступ toocertain ресурсов toospecific платформах.</span><span class="sxs-lookup"><span data-stu-id="403a0-122">In your device-based conditional access policy, you can limit access toocertain resources toospecific device platforms.</span></span>



<span data-ttu-id="403a0-123">В политике условного доступа на основе устройств может потребоваться toobe доверенных устройств, помеченные как соответствующие требованиям.</span><span class="sxs-lookup"><span data-stu-id="403a0-123">In a device-based conditional access policy, you can require trusted devices toobe marked as compliant.</span></span>

![Облачные приложения](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="403a0-125">Устройства могут быть помечены как совместимые в каталоге hello по:</span><span class="sxs-lookup"><span data-stu-id="403a0-125">Devices can be marked as compliant in hello directory by:</span></span>

- <span data-ttu-id="403a0-126">Intune</span><span class="sxs-lookup"><span data-stu-id="403a0-126">Intune</span></span> 
- <span data-ttu-id="403a0-127">Сторонней системы управления мобильными устройствами, интегрируемой с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="403a0-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="403a0-128">Только устройства, подключенного tooAzure AD может быть помечен как соответствующий.</span><span class="sxs-lookup"><span data-stu-id="403a0-128">Only devices that are connected tooAzure AD can be marked as compliant.</span></span> <span data-ttu-id="403a0-129">tooconnect устройства tooAzure Active Directory, у вас есть hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="403a0-129">tooconnect a device tooAzure Active Directory, you have hello following options:</span></span> 

- <span data-ttu-id="403a0-130">регистрация в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="403a0-130">Azure AD registered</span></span>
- <span data-ttu-id="403a0-131">присоединение к Azure AD;</span><span class="sxs-lookup"><span data-stu-id="403a0-131">Azure AD joined</span></span>
- <span data-ttu-id="403a0-132">присоединение к Azure AD (гибридные устройства).</span><span class="sxs-lookup"><span data-stu-id="403a0-132">Hybrid Azure AD joined</span></span>

    ![Облачные приложения](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="403a0-134">Если у вас есть локально занимаемое место Active Directory (AD), может потребоваться устройства, не подключенного tooAzure AD, но доверенных toobe tooyour присоединены к домену AD.</span><span class="sxs-lookup"><span data-stu-id="403a0-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected tooAzure AD but joined tooyour AD toobe trusted.</span></span>

![Облачные приложения](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="403a0-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="403a0-136">Next steps</span></span>

<span data-ttu-id="403a0-137">Перед настройкой политики условного доступа на основе устройств в вашей среде, следует рассмотреть hello [советы и рекомендации для условного доступа в Azure Active Directory](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="403a0-137">Before configuring a device-based conditional access policy in your environment, you should take a look at hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

