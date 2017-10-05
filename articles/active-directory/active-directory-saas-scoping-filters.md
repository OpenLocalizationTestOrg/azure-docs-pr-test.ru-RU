---
title: "Подготовка приложений с использованием фильтров области | Документация Майкрософт"
description: "Узнайте, как использовать фильтры области, чтобы предотвратить подготовку объектов, которые поддерживают автоматическую подготовку пользователей, но не отвечают требованиям компании."
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
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="64a38-103">Подготовка приложений на основе атрибутов с использованием фильтров области</span><span class="sxs-lookup"><span data-stu-id="64a38-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="64a38-104">В этой статье объясняется, как использовать фильтры области, чтобы задать правила на основе атрибутов, которые определяют, какие пользователи подготовлены для работы с приложением.</span><span class="sxs-lookup"><span data-stu-id="64a38-104">The objective of this section is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to the application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="64a38-105">Предложения и группы областей</span><span class="sxs-lookup"><span data-stu-id="64a38-105">Clauses and Scope Groups</span></span>
![Фильтр области действия][1] 

<span data-ttu-id="64a38-107">Фильтры области действия определяются одной или несколькими **группами областей**, каждая из которых содержит одно или несколько **предложений**.</span><span class="sxs-lookup"><span data-stu-id="64a38-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="64a38-108">Чтобы просмотреть предложения для определенной группы областей, разверните ее, щелкнув стрелку слева от имени группы.</span><span class="sxs-lookup"><span data-stu-id="64a38-108">To see the clauses for a particular scope group, expand it by clicking the arrow to the left of the group name.</span></span>

<span data-ttu-id="64a38-109">**Предложение** определяет, какие пользователи могут проходить через фильтр области, оценивая атрибуты каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="64a38-109">A **clause** determines which users are allowed to pass through the scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="64a38-110">Например, у вас может быть одно предложение, требующее, чтобы атрибут пользователя "область" имел значение "Нью-Йорк". Тогда только пользователи из Нью-Йорка будут подготовлены для работы с приложением.</span><span class="sxs-lookup"><span data-stu-id="64a38-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into the application.</span></span>

![Имя группы областей][2] 

<span data-ttu-id="64a38-112">Каждая **группа областей** начинается с одного обязательного **предложения**, как показано на снимке экрана выше.</span><span class="sxs-lookup"><span data-stu-id="64a38-112">Each **scope group** starts with one mandatory **clause**, as shown in the screenshot above.</span></span> <span data-ttu-id="64a38-113">Это предложение просто указывает, что до оценки фильтрами области приложению нужно назначить пользователя.</span><span class="sxs-lookup"><span data-stu-id="64a38-113">This clause simply states that the user must first be assigned to the application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="64a38-114">Это предложение нельзя удалить или изменить.</span><span class="sxs-lookup"><span data-stu-id="64a38-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="64a38-115">Можно добавить новые предложения или группы областей, нажав соответствующую кнопку.</span><span class="sxs-lookup"><span data-stu-id="64a38-115">You can add new clauses or new scope groups by pressing the appropriate button.</span></span> <span data-ttu-id="64a38-116">Каждой группе областей можно присвоить имя, изменив ее свойство **Имя группы областей** .</span><span class="sxs-lookup"><span data-stu-id="64a38-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="64a38-117">Оценка по фильтрам области</span><span class="sxs-lookup"><span data-stu-id="64a38-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="64a38-118">Во время подготовки мы проверяем каждого назначенного пользователя по фильтрам области, чтобы определить, положен ли ему доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="64a38-118">During provisioning, we test every assigned user against your scoping filters to determine if that user deserves access to the application.</span></span> <span data-ttu-id="64a38-119">Каждое предложение можно рассматривать как тест, который необходимо пройти пользователю, чтобы не быть отфильтрованным.</span><span class="sxs-lookup"><span data-stu-id="64a38-119">You can think of each clause as being a test that must be passed in order for the user to avoid getting filtered out.</span></span> 

<span data-ttu-id="64a38-120">Если определено несколько групп областей, каждый пользователь должен пройти по крайней мере один из тестов, чтобы получить доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="64a38-120">If you have multiple scope groups defined, each user must pass at least one of them to access the application.</span></span> <span data-ttu-id="64a38-121">Но внутри каждой группы областей пользователь должен пройти каждое предложение, чтобы попасть в эту группу областей.</span><span class="sxs-lookup"><span data-stu-id="64a38-121">Within each scope group, however, the user must pass every clause to pass that specific scope group.</span></span> 

<span data-ttu-id="64a38-122">Другими словами, группы областей можно представить как объединенные по условию "ИЛИ", а предложения в них — по условию "И".</span><span class="sxs-lookup"><span data-stu-id="64a38-122">In other words, you can think of scope groups as being OR’d together, and you can think of the clauses within them as being AND’d together.</span></span> <span data-ttu-id="64a38-123">Например, рассмотрим фильтр области.</span><span class="sxs-lookup"><span data-stu-id="64a38-123">For example, consider the scoping filter below:</span></span>

![Имя группы областей][3]  

<span data-ttu-id="64a38-125">Согласно этому фильтру области подготовке подлежат только пользователи, которые отвечают следующим условиям:</span><span class="sxs-lookup"><span data-stu-id="64a38-125">According to this scoping filter, users must satisfy the following criteria, to be provisioned:</span></span>

1. <span data-ttu-id="64a38-126">они должны быть назначены для работы с приложением;</span><span class="sxs-lookup"><span data-stu-id="64a38-126">They must be assigned to the application.</span></span>
2. <span data-ttu-id="64a38-127">они должны работать в отделе разработки;</span><span class="sxs-lookup"><span data-stu-id="64a38-127">They must work in the Engineering department</span></span>
3. <span data-ttu-id="64a38-128">они должны работать в Сан-Франциско или в Канаде.</span><span class="sxs-lookup"><span data-stu-id="64a38-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="64a38-129">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="64a38-129">Related Articles</span></span>
* [<span data-ttu-id="64a38-130">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64a38-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="64a38-131">Автоматическая подготовка пользователей и ее отзыв для приложений SaaS</span><span class="sxs-lookup"><span data-stu-id="64a38-131">Automate User Provisioning and Deprovisioning to SaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="64a38-132">Настройка сопоставления атрибутов для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="64a38-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="64a38-133">Запись выражений для сопоставления атрибутов</span><span class="sxs-lookup"><span data-stu-id="64a38-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="64a38-134">Уведомления о подготовке учетных записей</span><span class="sxs-lookup"><span data-stu-id="64a38-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="64a38-135">Автоматическая подготовка пользователей и групп из Azure Active Directory в приложениях с использованием SCIM</span><span class="sxs-lookup"><span data-stu-id="64a38-135">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="64a38-136">Список учебников по интеграции приложений SaaS</span><span class="sxs-lookup"><span data-stu-id="64a38-136">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
