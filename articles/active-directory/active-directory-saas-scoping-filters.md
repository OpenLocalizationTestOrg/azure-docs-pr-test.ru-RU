---
title: "aaaProvisioning приложений с использованием фильтров области | Документы Microsoft"
description: "Узнайте, как области toouse фильтрует объекты tooprevent в приложениях, поддерживающих Автоматическая подготовка пользователей из фактически идет подготовка, если объект не удовлетворяет необходимым требованиям бизнеса."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="7976c-103">Подготовка приложений на основе атрибутов с использованием фильтров области</span><span class="sxs-lookup"><span data-stu-id="7976c-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="7976c-104">Цель этого раздела Hello — как toouse области фильтров toodefine основанное на атрибутах правила, определяющие, какие пользователи имеют tooexplain подготовить toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="7976c-104">hello objective of this section is tooexplain how toouse scoping filters toodefine attribute-based rules that determine which users are provisioned toohello application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="7976c-105">Предложения и группы областей</span><span class="sxs-lookup"><span data-stu-id="7976c-105">Clauses and Scope Groups</span></span>
![Фильтр области действия][1] 

<span data-ttu-id="7976c-107">Фильтры области действия определяются одной или несколькими **группами областей**, каждая из которых содержит одно или несколько **предложений**.</span><span class="sxs-lookup"><span data-stu-id="7976c-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="7976c-108">toosee hello предложения для определенной группы областей, разверните ее, щелкнув hello стрелка влево toohello имя_группы hello.</span><span class="sxs-lookup"><span data-stu-id="7976c-108">toosee hello clauses for a particular scope group, expand it by clicking hello arrow toohello left of hello group name.</span></span>

<span data-ttu-id="7976c-109">Объект **предложение** определяет, какие пользователи имеют право toopass через hello фильтр области, оценивая атрибуты каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="7976c-109">A **clause** determines which users are allowed toopass through hello scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="7976c-110">Например может потребоваться одно предложение, требующее, пользователя «состояние» атрибута равно Нью-Йорке, поэтому только пользователи из Московской подготавливаются в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="7976c-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into hello application.</span></span>

![Имя группы областей][2] 

<span data-ttu-id="7976c-112">Каждый **группы областей** начинается с одного обязательно **предложение**, как показано на снимке экрана приветствия выше.</span><span class="sxs-lookup"><span data-stu-id="7976c-112">Each **scope group** starts with one mandatory **clause**, as shown in hello screenshot above.</span></span> <span data-ttu-id="7976c-113">Это предложение просто указывает, что этот пользователь hello необходимо назначить toohello приложения до его оценки по фильтрам области.</span><span class="sxs-lookup"><span data-stu-id="7976c-113">This clause simply states that hello user must first be assigned toohello application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="7976c-114">Это предложение нельзя удалить или изменить.</span><span class="sxs-lookup"><span data-stu-id="7976c-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="7976c-115">Можно добавить новые предложения или группы областей, нажав соответствующую кнопку "hello".</span><span class="sxs-lookup"><span data-stu-id="7976c-115">You can add new clauses or new scope groups by pressing hello appropriate button.</span></span> <span data-ttu-id="7976c-116">Каждой группе областей можно присвоить имя, изменив ее свойство **Имя группы областей** .</span><span class="sxs-lookup"><span data-stu-id="7976c-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="7976c-117">Оценка по фильтрам области</span><span class="sxs-lookup"><span data-stu-id="7976c-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="7976c-118">Во время инициализации, мы тестируем каждого назначенного пользователя по вашей области toodetermine фильтры, если этот пользователь заслуживает toohello приложения access.</span><span class="sxs-lookup"><span data-stu-id="7976c-118">During provisioning, we test every assigned user against your scoping filters toodetermine if that user deserves access toohello application.</span></span> <span data-ttu-id="7976c-119">Можно рассматривать как тест, который должен быть передан в порядке для hello пользователя tooavoid был отфильтрован каждого предложения.</span><span class="sxs-lookup"><span data-stu-id="7976c-119">You can think of each clause as being a test that must be passed in order for hello user tooavoid getting filtered out.</span></span> 

<span data-ttu-id="7976c-120">Если имеется несколько групп областей, каждый пользователь должен попасть по крайней мере один из них tooaccess приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7976c-120">If you have multiple scope groups defined, each user must pass at least one of them tooaccess hello application.</span></span> <span data-ttu-id="7976c-121">Внутри каждой группы областей, тем не менее, hello пользователь должен передать toopass каждого предложения эту группу областей.</span><span class="sxs-lookup"><span data-stu-id="7976c-121">Within each scope group, however, hello user must pass every clause toopass that specific scope group.</span></span> 

<span data-ttu-id="7976c-122">Другими словами, можно представить группы областей как логическая или можно представить hello предложения в них, как и логическая.</span><span class="sxs-lookup"><span data-stu-id="7976c-122">In other words, you can think of scope groups as being OR’d together, and you can think of hello clauses within them as being AND’d together.</span></span> <span data-ttu-id="7976c-123">Например рассмотрим hello фильтр ниже области.</span><span class="sxs-lookup"><span data-stu-id="7976c-123">For example, consider hello scoping filter below:</span></span>

![Имя группы областей][3]  

<span data-ttu-id="7976c-125">В соответствии с toothis фильтр области, пользователи должны удовлетворять hello следующие критерии, toobe подготовки:</span><span class="sxs-lookup"><span data-stu-id="7976c-125">According toothis scoping filter, users must satisfy hello following criteria, toobe provisioned:</span></span>

1. <span data-ttu-id="7976c-126">Должны быть назначены toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="7976c-126">They must be assigned toohello application.</span></span>
2. <span data-ttu-id="7976c-127">Они должны работать в отдел разработок hello</span><span class="sxs-lookup"><span data-stu-id="7976c-127">They must work in hello Engineering department</span></span>
3. <span data-ttu-id="7976c-128">они должны работать в Сан-Франциско или в Канаде.</span><span class="sxs-lookup"><span data-stu-id="7976c-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="7976c-129">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="7976c-129">Related Articles</span></span>
* [<span data-ttu-id="7976c-130">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7976c-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="7976c-131">Автоматизировать подготовку пользователей и их отзыва tooSaaS приложений</span><span class="sxs-lookup"><span data-stu-id="7976c-131">Automate User Provisioning and Deprovisioning tooSaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="7976c-132">Настройка сопоставления атрибутов для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="7976c-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="7976c-133">Запись выражений для сопоставления атрибутов</span><span class="sxs-lookup"><span data-stu-id="7976c-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="7976c-134">Уведомления о подготовке учетных записей</span><span class="sxs-lookup"><span data-stu-id="7976c-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="7976c-135">С помощью SCIM tooenable автоматическую подготовку пользователей и групп из Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="7976c-135">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="7976c-136">Список учебников по tooIntegrate приложений SaaS</span><span class="sxs-lookup"><span data-stu-id="7976c-136">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
