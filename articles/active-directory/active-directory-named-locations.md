---
title: "aaaNamed расположения в Azure Active Directory | Документы Microsoft"
description: "Настроив с именем расположения, можно избежать необходимости IP адресов, которые принадлежат вашей организации к созданию ложных положительных результатов для hello невозможно местоположений tooatypical тип событий риска."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="f00bc-103">Именованные расположения в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f00bc-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="f00bc-104">С hello с именем расположения функция Azure Active Directory можно пометить доверенные диапазоны IP-адресов в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="f00bc-104">With hello named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="f00bc-105">В вашей среде, можно использовать именованные папки в контексте hello обнаружение hello [риск события](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="f00bc-105">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="f00bc-106">функция Hello помогает снизить количество hello обнаруженную ложных положительных результатов для hello *tooatypical невозможно местоположений* тип событий риска.</span><span class="sxs-lookup"><span data-stu-id="f00bc-106">hello feature helps reduce hello number of reported false positives for hello *Impossible travel tooatypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="f00bc-107">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="f00bc-107">Configuration</span></span>

<span data-ttu-id="f00bc-108">tooconfigure именованное расположение:</span><span class="sxs-lookup"><span data-stu-id="f00bc-108">tooconfigure a named location:</span></span>

1. <span data-ttu-id="f00bc-109">Войдите в toohello [портал Azure](https://portal.azure.com) роли глобального администратора.</span><span class="sxs-lookup"><span data-stu-id="f00bc-109">Sign in toohello [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="f00bc-110">Hello левой панели щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f00bc-110">In hello left pane, click **Azure Active Directory**.</span></span>

    ![Hello Azure Active Directory ссылку в левой области hello](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="f00bc-112">На hello **Azure Active Directory** колонки в hello **безопасности** щелкните **условного доступа**.</span><span class="sxs-lookup"><span data-stu-id="f00bc-112">On hello **Azure Active Directory** blade, in hello **Security** section, click **Conditional access**.</span></span>

    ![Hello условным доступом команды](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="f00bc-114">На hello **условного доступа** колонки в hello **управление** щелкните **расположения с именем**.</span><span class="sxs-lookup"><span data-stu-id="f00bc-114">On hello **Conditional Access** blade, in hello **Manage** section, click **Named locations**.</span></span>

    ![Команда расположения именованных Hello](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="f00bc-116">На hello **с именем расположения** колонка, щелкните **новое расположение**.</span><span class="sxs-lookup"><span data-stu-id="f00bc-116">On hello **Named locations** blade, click **New location**.</span></span>

    ![Новая команда расположение Hello](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="f00bc-118">На hello **New** колонке hello следующие:</span><span class="sxs-lookup"><span data-stu-id="f00bc-118">On hello **New** blade, do hello following:</span></span>

    ![Новая колонка Hello](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="f00bc-120">а.</span><span class="sxs-lookup"><span data-stu-id="f00bc-120">a.</span></span> <span data-ttu-id="f00bc-121">В hello **имя** введите имя для данного именованного местоположения.</span><span class="sxs-lookup"><span data-stu-id="f00bc-121">In hello **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="f00bc-122">b.</span><span class="sxs-lookup"><span data-stu-id="f00bc-122">b.</span></span> <span data-ttu-id="f00bc-123">В hello **диапазоны IP-адресов** введите диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="f00bc-123">In hello **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="f00bc-124">диапазон IP-адресов Hello должен toobe в hello *бесклассовой междоменной маршрутизации* формате (CIDR).</span><span class="sxs-lookup"><span data-stu-id="f00bc-124">hello IP range needs toobe in hello *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="f00bc-125">c.</span><span class="sxs-lookup"><span data-stu-id="f00bc-125">c.</span></span> <span data-ttu-id="f00bc-126">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f00bc-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="f00bc-127">Необходимая информация</span><span class="sxs-lookup"><span data-stu-id="f00bc-127">What you should know</span></span>

<span data-ttu-id="f00bc-128">**Массового обновления**: при создании или обновлении именованных расположений для массового обновления, можно передать или загрузить CSV-файл с hello IP-диапазонов.</span><span class="sxs-lookup"><span data-stu-id="f00bc-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with hello IP ranges.</span></span> <span data-ttu-id="f00bc-129">Передача добавляет hello IP-диапазонов в списке toohello hello файла вместо перезаписи список hello.</span><span class="sxs-lookup"><span data-stu-id="f00bc-129">An upload adds hello IP ranges in hello file toohello list instead of overwriting hello list.</span></span>

![Привет, отправка и загрузка ссылок](./media/active-directory-named-locations/09.png)


<span data-ttu-id="f00bc-131">**Ограничения**: можно определить один tooeach диапазона, назначенного IP из них не более 60 именованных расположений.</span><span class="sxs-lookup"><span data-stu-id="f00bc-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned tooeach of them.</span></span> <span data-ttu-id="f00bc-132">Если имеется только один именованный расположения, настроенного для него можно определить too500 диапазоны IP.</span><span class="sxs-lookup"><span data-stu-id="f00bc-132">If you have just one named location configured, you can define up too500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f00bc-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f00bc-133">Next steps</span></span>

<span data-ttu-id="f00bc-134">toolearn Дополнительные сведения о событиях риска в разделе [событий риска Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="f00bc-134">toolearn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

