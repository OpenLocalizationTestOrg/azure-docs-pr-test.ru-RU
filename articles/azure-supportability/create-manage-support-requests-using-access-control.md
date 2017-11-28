---
title: "Контроль прав доступа для создания запросов в службу поддержки и управления ими с помощью управления доступом на основе ролей (RBAC) Azure | Документация Майкрософт"
description: "Контроль прав доступа для создания запросов в службу поддержки и управления ими с помощью управления доступом на основе ролей (RBAC) Azure"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: 20ebd324cbf379980b43d255d468673de2b6d950
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-based-access-control-rbac-to-control-access-rights-to-create-and-manage-support-requests"></a><span data-ttu-id="39322-103">Контроль прав доступа для создания запросов в службу поддержки и управления ими с помощью управления доступом на основе ролей (RBAC) Azure</span><span class="sxs-lookup"><span data-stu-id="39322-103">Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests</span></span>

<span data-ttu-id="39322-104">[Управление доступом на основе ролей (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) обеспечивает точный контроль доступа в Azure.</span><span class="sxs-lookup"><span data-stu-id="39322-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="39322-105">Модель RBAC Azure используется при создании запросов на поддержку на портале Azure ([portal.azure.com](https://portal.azure.com)) для предоставления прав на создание таких запросов и управление ими.</span><span class="sxs-lookup"><span data-stu-id="39322-105">Support request creation in the Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model to define who can create and manage support requests.</span></span>
<span data-ttu-id="39322-106">Доступ предоставляется путем назначения соответствующей роли RBAC пользователям, группам и приложениям в определенной области. Это может быть подписка, группа ресурсов или ресурс.</span><span class="sxs-lookup"><span data-stu-id="39322-106">Access is granted by assigning the appropriate RBAC role to users, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="39322-107">Рассмотрим такой пример: владелец группы ресурсов с разрешениями на чтение в области действия подписки может управлять всеми ресурсами в этой группе, в том числе веб-сайтами, виртуальными машинами и подсетями.</span><span class="sxs-lookup"><span data-stu-id="39322-107">Let’s take an example: As a resource group owner with read permissions at the subscription scope, you can manage all the resources under the resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="39322-108">Тем не менее при попытке создать запрос на техническую поддержку для ресурса виртуальной машины произойдет следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="39322-108">However, when you try to create a support request against the virtual machine resource, you encounter the following error</span></span>

![Ошибка подписки](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="39322-110">Для управления запросами на поддержку необходимо разрешение на запись или роль, для которой в области действия подписки задано действие поддержки Microsoft.Support/*, которое дает возможность создавать запросы на поддержку и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="39322-110">In support request management, you need write permission or a role that has the Support action Microsoft.Support/* at the Subscription scope to be able to create and manage support requests.</span></span>

<span data-ttu-id="39322-111">В следующей статье объясняется, как можно использовать управление доступом на основе ролей (RBAC) для создания запросов на поддержку на портале Azure и управления ими.</span><span class="sxs-lookup"><span data-stu-id="39322-111">The following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) to create and manage support requests in the Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="39322-112">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="39322-112">Getting Started</span></span>

<span data-ttu-id="39322-113">Если возникла такая ситуация, как в описанном выше примере, вы можете создать запрос на поддержку для ресурса, если владелец подписки назначил вам пользовательские роли RBAC.</span><span class="sxs-lookup"><span data-stu-id="39322-113">Using the example above, you would be able to create a support request for your resource if you were assigned a custom RBAC role on the subscription by the subscription owner.</span></span>
<span data-ttu-id="39322-114">[Настраиваемые роли RBAC](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) можно создавать с помощью Azure PowerShell, интерфейса командной строки (CLI) Azure и интерфейса REST API.</span><span class="sxs-lookup"><span data-stu-id="39322-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and the REST API.</span></span>

<span data-ttu-id="39322-115">Свойство Actions пользовательской роли определяет операции Azure, к которым эта роль предоставляет доступ.</span><span class="sxs-lookup"><span data-stu-id="39322-115">The actions property of a custom role specifies the Azure operations to which the role grants access.</span></span>
<span data-ttu-id="39322-116">Чтобы создать пользовательскую роль для управления запросами на поддержку, для нее потребуется действие Microsoft.Support/*.</span><span class="sxs-lookup"><span data-stu-id="39322-116">To create a custom role for support request management, the role must have the action Microsoft.Support/*</span></span>

<span data-ttu-id="39322-117">Ниже приведен пример пользовательской роли, которую можно использовать для создания запросов на поддержку и управления ими.</span><span class="sxs-lookup"><span data-stu-id="39322-117">Here’s an example of a custom role you can use to create and manage support requests.</span></span>
<span data-ttu-id="39322-118">Мы назвали ее "Участник с правом создавать запросы на поддержку" и будем использовать это название в данной статье.</span><span class="sxs-lookup"><span data-stu-id="39322-118">We’ve named this role “Support Request Contributor” and that’s how we refer to the custom role in this article.</span></span>

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

<span data-ttu-id="39322-119">Выполните шаги, описанные [в этом видео](https://www.youtube.com/watch?v=-PaBaDmfwKI), чтобы научиться создавать пользовательские роли для подписки.</span><span class="sxs-lookup"><span data-stu-id="39322-119">Follow the steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) to learn how to create a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-the-azure-portal"></a><span data-ttu-id="39322-120">Создание запросов на поддержку и управление ими на портале Azure</span><span class="sxs-lookup"><span data-stu-id="39322-120">Create and manage support requests in the Azure portal</span></span>

<span data-ttu-id="39322-121">Рассмотрим такой пример: предположим, вы являетесь владельцем подписки "Подписка MSDN для Visual Studio".</span><span class="sxs-lookup"><span data-stu-id="39322-121">Let’s take an example – you are the owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="39322-122">Ваш коллега Дмитрий — владелец ресурсов в нескольких группах ресурсов этой подписки, у которого есть для нее разрешение на чтение.</span><span class="sxs-lookup"><span data-stu-id="39322-122">Joe is your peer who is a resource owner to some of the resource groups in this subscription and has read permission to the subscription.</span></span>
<span data-ttu-id="39322-123">Вы хотите предоставить ему возможность создавать запросы в службу поддержки и управлять ими для ресурсов в рамках данной подписки.</span><span class="sxs-lookup"><span data-stu-id="39322-123">You wish to give access to your peer, Joe, the ability to create and manage support tickets for the resources under this subscription.</span></span>

1. <span data-ttu-id="39322-124">Первым делом следует перейти к подписке. В поле "Параметры" отобразится список пользователей.</span><span class="sxs-lookup"><span data-stu-id="39322-124">The first step is to go to the subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="39322-125">Выберите пользователя по имени Дмитрий, у которого есть доступ для чтения в рамках этой подписки, и назначьте ему новую пользовательскую роль.</span><span class="sxs-lookup"><span data-stu-id="39322-125">Click the user Joe who has reader access on the Subscription and let’s assign a new custom role to him.</span></span>

    ![Добавление роли](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="39322-127">В колонке "Пользователи" щелкните "Добавить".</span><span class="sxs-lookup"><span data-stu-id="39322-127">Click "Add" under the "Users" blade.</span></span> <span data-ttu-id="39322-128">Выберите в списке ролей пользовательскую роль "Участник с правом создавать запросы на поддержку".</span><span class="sxs-lookup"><span data-stu-id="39322-128">Select the custom role "Support Request Contributor" from the list of roles</span></span>

    ![Добавление роли участника с доступом к службе поддержки](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="39322-130">Выбрав имя роли, щелкните "Добавить пользователей" и введите учетные данные электронной почты Дмитрия.</span><span class="sxs-lookup"><span data-stu-id="39322-130">After selecting the role name, click "Add users" and enter the Joe's email credentials.</span></span> <span data-ttu-id="39322-131">Нажмите "Выбрать".</span><span class="sxs-lookup"><span data-stu-id="39322-131">Click "Select"</span></span>

    ![Добавление пользователей](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="39322-133">Нажмите кнопку "ОК", чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="39322-133">Click "Ok" to proceed</span></span>

    ![Предоставление доступа](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="39322-135">Вы увидите пользователя с добавленной для него новой пользовательской ролью "Участник с правом создавать запросы на поддержку" в рамках подписки, владельцем которой вы являетесь.</span><span class="sxs-lookup"><span data-stu-id="39322-135">Now you see the user with the newly added custom role "Support Request Contributor" under the Subscription for which you are the owner</span></span>

    ![Добавлен пользователь](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="39322-137">Когда Дмитрий войдет на портал, он увидит подписку, в которую он был добавлен.</span><span class="sxs-lookup"><span data-stu-id="39322-137">When Joe logs in the portal, he sees the subscription to which he was added.</span></span>

7. <span data-ttu-id="39322-138">Если он нажмет "Новый запрос в службу поддержки" в колонке "Справка и поддержка", то сможет создать запросы на поддержку для Visual Studio Ultimate с подпиской MSDN.</span><span class="sxs-lookup"><span data-stu-id="39322-138">Joe clicks "New Support request" from the "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Новый запрос на техническую поддержку](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="39322-140">Нажав кнопку «Все поддерживают запросы» Joe можно просмотреть список запросов поддержки, созданному для этой подписки ![случае представление сведений](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="39322-140">Clicking "All support requests" Joe can see the list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-the-azure-portal"></a><span data-ttu-id="39322-141">Отзыв прав доступа для создания запросов на поддержку на портале Azure</span><span class="sxs-lookup"><span data-stu-id="39322-141">Remove support request access in the Azure portal</span></span>

<span data-ttu-id="39322-142">Пользователю можно не только предоставить доступ для создания запросов на поддержку и управление ими, но и отозвать право на такой доступ.</span><span class="sxs-lookup"><span data-stu-id="39322-142">Just as it is possible to grant access to a user to create and manage support requests, it's possible to remove access for the user as well.</span></span>
<span data-ttu-id="39322-143">Чтобы запретить создание запросов на поддержку и управление ими, перейдите к подписке, щелкните "Параметры" и выберите пользователя (в данном случае это Дмитрий).</span><span class="sxs-lookup"><span data-stu-id="39322-143">To remove the ability to create and manage support requests, go to the Subscription, click "Settings" and click the user (in this case, Joe).</span></span>
<span data-ttu-id="39322-144">Щелкните правой кнопкой мыши имя роли "Участник с правом создавать запросы на поддержку" и выберите "Удалить".</span><span class="sxs-lookup"><span data-stu-id="39322-144">Right-click the role name, "Support Request Contributor" and click "Remove"</span></span>

![Отзыв доступа для создания запросов на поддержку](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="39322-146">Когда Дмитрий войдет на портал и попытается создать запрос на поддержку, произойдет следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="39322-146">When Joe logs in to the portal and tries to create a support request, he encounters the following error</span></span>

![Ошибка подписки 2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="39322-148">Дмитрий не сможет просмотреть запросы на поддержку, щелкнув "Все запросы на поддержку".</span><span class="sxs-lookup"><span data-stu-id="39322-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![Представление сведений об обращении 2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
