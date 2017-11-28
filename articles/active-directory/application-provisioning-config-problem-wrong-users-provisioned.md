---
title: "Подготовка неправильного набора пользователей для приложения в коллекции Azure AD | Документация Майкрософт"
description: "Узнайте, как выяснить, почему в приложении подготавливается не та группа пользователей, которую вы настроили"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 85b533584c8ec15a23be32e20db7de583fced6a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a><span data-ttu-id="054ee-103">Подготовка неправильного набора пользователей для приложения в коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="054ee-103">Wrong set of users are being provisioned to an Azure AD Gallery application</span></span>

<span data-ttu-id="054ee-104">Пользователи, подготавливаемые в приложении, в основном определяются пользователями и группами, **назначенными** для него.</span><span class="sxs-lookup"><span data-stu-id="054ee-104">Which users are provisioned to the app is primarily driven by which users and groups have been **assigned** to the application.</span></span>

<span data-ttu-id="054ee-105">Воспользуйтесь приведенными ниже ссылками, чтобы узнать, как определить пользователей и группы, назначенные приложению в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="054ee-105">Use the resources below to learn how to check which users and groups have been assigned to an application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="054ee-106">Назначение пользователей напрямую от имени администратора</span><span class="sxs-lookup"><span data-stu-id="054ee-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="054ee-107">Чтобы напрямую назначить одного или нескольких пользователей для приложения, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="054ee-107">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="054ee-108">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="054ee-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="054ee-109">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="054ee-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="054ee-110">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="054ee-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="054ee-111">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="054ee-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="054ee-112">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="054ee-112">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="054ee-113">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="054ee-113">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="054ee-114">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="054ee-114">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="054ee-115">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="054ee-115">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="054ee-116">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="054ee-116">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="054ee-117">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="054ee-117">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="054ee-118">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** пользователя, которого требуется назначить.</span><span class="sxs-lookup"><span data-stu-id="054ee-118">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="054ee-119">Наведите указатель мыши на **пользователя** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="054ee-119">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="054ee-120">Чтобы добавить пользователя в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="054ee-120">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="054ee-121">**Необязательно.** Если вы хотите **добавить более одного пользователя**, в поле **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** другого пользователя и установите флажок, чтобы добавить этого пользователя в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="054ee-121">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="054ee-122">Выбрав всех пользователей, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="054ee-122">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="054ee-123">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="054ee-123">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="054ee-124">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="054ee-124">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="054ee-125">Если подготовка настраивается и уже выполняется для приложения, новые пользователи будут подготовлены для приложения в течение 10 минут.</span><span class="sxs-lookup"><span data-stu-id="054ee-125">If provisioning is configured and already running for an app, new users should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="054ee-126">Проверьте **журналы аудита**, чтобы получить подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="054ee-126">Check the **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="054ee-127">Назначение группы для приложений напрямую от имени администратора</span><span class="sxs-lookup"><span data-stu-id="054ee-127">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="054ee-128">Чтобы напрямую назначить одну или несколько групп для приложения, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="054ee-128">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="054ee-129">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="054ee-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="054ee-130">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="054ee-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="054ee-131">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="054ee-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="054ee-132">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="054ee-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="054ee-133">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="054ee-133">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="054ee-134">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="054ee-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="054ee-135">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="054ee-135">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="054ee-136">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="054ee-136">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="054ee-137">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="054ee-137">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="054ee-138">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="054ee-138">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="054ee-139">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя группы**, которой требуется назначить приложение.</span><span class="sxs-lookup"><span data-stu-id="054ee-139">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="054ee-140">Наведите указатель мыши на **группу** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="054ee-140">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="054ee-141">Чтобы добавить группу в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этой группы.</span><span class="sxs-lookup"><span data-stu-id="054ee-141">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="054ee-142">**Необязательно.** Если вы хотите **добавить более одной группы**, в поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя группы** и установите флажок, чтобы добавить группу в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="054ee-142">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="054ee-143">Выбрав все группы, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="054ee-143">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="054ee-144">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным группам.</span><span class="sxs-lookup"><span data-stu-id="054ee-144">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="054ee-145">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным группам.</span><span class="sxs-lookup"><span data-stu-id="054ee-145">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="054ee-146">Если подготовка настраивается и уже выполняется для приложения, новые пользователи в группе будут подготовлены для приложения в течение 10 минут.</span><span class="sxs-lookup"><span data-stu-id="054ee-146">If provisioning is configured and already running for an app, new users contained within the group should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="054ee-147">Проверьте **журналы аудита**, чтобы получить подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="054ee-147">Check the **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="054ee-148">Подготовка имени группы и сведений о ней, помимо ее участников (если поддерживается для некоторых приложений).</span><span class="sxs-lookup"><span data-stu-id="054ee-148">Provisioning of the group name and group details, in addition to the members, if supported for some applications.</span></span> <span data-ttu-id="054ee-149">Вы можете включить или отключить эту возможность, включая или отключая **сопоставление** для объектов группы, отображающихся на вкладке **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="054ee-149">You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="054ee-150">Если подготовка групп включена, обязательно ознакомьтесь с атрибутами сопоставления, чтобы убедиться, что для соответствующего идентификатора используется соответствующее поле.</span><span class="sxs-lookup"><span data-stu-id="054ee-150">If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”.</span></span> <span data-ttu-id="054ee-151">Это может быть отображающееся имя или псевдоним электронной почты, так как группа и ее участники не будут подготовлены, если соответствующее свойство пустое или не заполнено для группы в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="054ee-151">This can be the display name or email alias, as the group and its members not be provisioned if the matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="054ee-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="054ee-152">Next steps</span></span>
[<span data-ttu-id="054ee-153">Автоматическая подготовка пользователей и ее отзыв для приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="054ee-153">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
