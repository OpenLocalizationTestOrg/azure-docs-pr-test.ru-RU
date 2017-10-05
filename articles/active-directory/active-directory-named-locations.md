---
title: "Именованные расположения в Azure Active Directory | Документация Майкрософт"
description: "Настроив именованные расположения, вы предотвратите ситуацию, когда IP-адреса вашей организации вызывают ложное срабатывание для типа события риска \"Невозможно переместиться в нетипичные расположения\"."
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
ms.openlocfilehash: ff31ded1d9d60e47e0ae5f01119de78cd7f2df38
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="ffdb2-103">Именованные расположения в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffdb2-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="ffdb2-104">Функция "Именованные расположения" в Azure Active Directory позволяет пометить диапазоны доверенных IP-адресов в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-104">With the named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="ffdb2-105">В своей среде именованные расположения можно использовать в контексте обнаружения [событий риска](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="ffdb2-105">In your environment, you can use named locations in the context of the detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="ffdb2-106">Эта функция позволяет сократить количество сообщаемых ложных срабатываний для типа событий риска *Невозможно переместиться в нетипичные расположения*.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-106">The feature helps reduce the number of reported false positives for the *Impossible travel to atypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="ffdb2-107">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="ffdb2-107">Configuration</span></span>

<span data-ttu-id="ffdb2-108">Чтобы настроить именованное расположение, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-108">To configure a named location:</span></span>

1. <span data-ttu-id="ffdb2-109">Войдите на [портал Azure](https://portal.azure.com) как глобальный администратор.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-109">Sign in to the [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="ffdb2-110">В левой панели щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-110">In the left pane, click **Azure Active Directory**.</span></span>

    ![Ссылка на Azure Active Directory на левой панели](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="ffdb2-112">В колонке **Azure Active Directory** в разделе **Безопасность** щелкните **Условный доступ**.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-112">On the **Azure Active Directory** blade, in the **Security** section, click **Conditional access**.</span></span>

    ![Команда "Условный доступ"](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="ffdb2-114">В колонке **Условный доступ** в разделе **Управление** щелкните **Именованные расположения**.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-114">On the **Conditional Access** blade, in the **Manage** section, click **Named locations**.</span></span>

    ![Команда "Именованные расположения"](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="ffdb2-116">В колонке **Именованные расположения** щелкните **Создать расположение**.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-116">On the **Named locations** blade, click **New location**.</span></span>

    ![Команда "Создать расположение"](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="ffdb2-118">В колонке **Создать** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ffdb2-118">On the **New** blade, do the following:</span></span>

    ![Колонка "Создать"](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="ffdb2-120">а.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-120">a.</span></span> <span data-ttu-id="ffdb2-121">В поле **Имя** введите имя именованного расположения.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-121">In the **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="ffdb2-122">b.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-122">b.</span></span> <span data-ttu-id="ffdb2-123">В поле **Диапазоны IP-адресов** введите диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-123">In the **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="ffdb2-124">Диапазон IP-адресов должен иметь формат *бесклассовой междоменной маршрутизации* (CIDR).</span><span class="sxs-lookup"><span data-stu-id="ffdb2-124">The IP range needs to be in the *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="ffdb2-125">c.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-125">c.</span></span> <span data-ttu-id="ffdb2-126">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="ffdb2-127">Необходимая информация</span><span class="sxs-lookup"><span data-stu-id="ffdb2-127">What you should know</span></span>

<span data-ttu-id="ffdb2-128">**Bulk updates** (Массовые обновления). При создании или обновлении именованных расположений для массовых обновлений можно передать или скачать CSV-файл с диапазонами IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with the IP ranges.</span></span> <span data-ttu-id="ffdb2-129">С помощью этого действия диапазоны IP-адресов из файла добавляются в список, и их не нужно переписывать.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-129">An upload adds the IP ranges in the file to the list instead of overwriting the list.</span></span>

![Ссылки для передачи и скачивания](./media/active-directory-named-locations/09.png)


<span data-ttu-id="ffdb2-131">**Ограничения.** Вы можете определить не более 60 именованных расположений, каждому из которых назначен один диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned to each of them.</span></span> <span data-ttu-id="ffdb2-132">Если у вас есть только одно настроенное именованное расположение, для него можно определить до 500 диапазонов IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ffdb2-132">If you have just one named location configured, you can define up to 500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ffdb2-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ffdb2-133">Next steps</span></span>

<span data-ttu-id="ffdb2-134">Дополнительные сведения о событиях риска см. в статье [События риска Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="ffdb2-134">To learn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

