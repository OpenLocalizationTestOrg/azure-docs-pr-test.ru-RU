---
title: "Управление доступом на основе ролей (RBAC) toocontrol aaaAzure toocreate права доступа к и управление запросами поддержки | Документы Microsoft"
description: "Azure toocontrol управления доступом на основе ролей (RBAC) toocreate права доступа и управления ими запросов на получение поддержки"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a><span data-ttu-id="f073c-103">Azure toocontrol управления доступом на основе ролей (RBAC) toocreate права доступа и управления ими запросов на получение поддержки</span><span class="sxs-lookup"><span data-stu-id="f073c-103">Azure Role-Based Access Control (RBAC) toocontrol access rights toocreate and manage support requests</span></span>

<span data-ttu-id="f073c-104">[Управление доступом на основе ролей (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) обеспечивает точный контроль доступа в Azure.</span><span class="sxs-lookup"><span data-stu-id="f073c-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="f073c-105">Поддерживает создание запроса в hello портал Azure [portal.azure.com](https://portal.azure.com), использует toodefine модели RBAC в Azure, можно создавать и управлять запросов поддержки.</span><span class="sxs-lookup"><span data-stu-id="f073c-105">Support request creation in hello Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model toodefine who can create and manage support requests.</span></span>
<span data-ttu-id="f073c-106">Доступ предоставляется путем назначения hello соответствующие RBAC роли toousers, группы и приложения в определенной области, который может быть подписки, группы ресурсов или ресурс.</span><span class="sxs-lookup"><span data-stu-id="f073c-106">Access is granted by assigning hello appropriate RBAC role toousers, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="f073c-107">Рассмотрим пример: как владелец группы ресурсов с разрешениями на чтение в области видимости hello подписки, можно управлять ресурсами hello в группе ресурсов hello, таких как веб-сайты, виртуальные машины и подсети.</span><span class="sxs-lookup"><span data-stu-id="f073c-107">Let’s take an example: As a resource group owner with read permissions at hello subscription scope, you can manage all hello resources under hello resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="f073c-108">Тем не менее при попытке toocreate запрос на техническую поддержку для ресурса виртуальной машины hello, возникнет следующая ошибка hello</span><span class="sxs-lookup"><span data-stu-id="f073c-108">However, when you try toocreate a support request against hello virtual machine resource, you encounter hello following error</span></span>

![Ошибка подписки](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="f073c-110">В управлении запрос поддержки необходимо разрешение на запись или роли, имеющей hello поддерживает действие Microsoft.Support/* на возможности toocreate toobe область hello подписки и управление запросами на поддержку.</span><span class="sxs-lookup"><span data-stu-id="f073c-110">In support request management, you need write permission or a role that has hello Support action Microsoft.Support/* at hello Subscription scope toobe able toocreate and manage support requests.</span></span>

<span data-ttu-id="f073c-111">Hello следующей статьей объясняется, как можно использовать пользовательские toocreate управление доступом на основе ролей (RBAC) в Azure и управлять запросов поддержки в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f073c-111">hello following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) toocreate and manage support requests in hello Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f073c-112">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="f073c-112">Getting Started</span></span>

<span data-ttu-id="f073c-113">С помощью приведенном выше примере hello, будет может toocreate запрос на техническую поддержку для ресурса, если были назначены пользовательской роли RBAC в подписке hello владельцем подписки hello.</span><span class="sxs-lookup"><span data-stu-id="f073c-113">Using hello example above, you would be able toocreate a support request for your resource if you were assigned a custom RBAC role on hello subscription by hello subscription owner.</span></span>
<span data-ttu-id="f073c-114">[Пользовательские роли RBAC](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) могут создаваться с помощью Azure PowerShell, Azure интерфейс командной строки (CLI) и hello REST API.</span><span class="sxs-lookup"><span data-stu-id="f073c-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and hello REST API.</span></span>

<span data-ttu-id="f073c-115">Свойство действия Hello пользовательские роли указывает, что hello Azure операций toowhich hello роль предоставляет доступ.</span><span class="sxs-lookup"><span data-stu-id="f073c-115">hello actions property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span>
<span data-ttu-id="f073c-116">toocreate пользовательской роли для поддержки управления запроса hello роль должна иметь действие hello Microsoft.Support/*</span><span class="sxs-lookup"><span data-stu-id="f073c-116">toocreate a custom role for support request management, hello role must have hello action Microsoft.Support/*</span></span>

<span data-ttu-id="f073c-117">Ниже приведен пример пользовательской роли, вы можете использовать toocreate и управлять поддерживает запросы.</span><span class="sxs-lookup"><span data-stu-id="f073c-117">Here’s an example of a custom role you can use toocreate and manage support requests.</span></span>
<span data-ttu-id="f073c-118">Мы назвали этой роли «Участник запросов поддержки» и, как мы называем toohello настраиваемой роли в этой статье.</span><span class="sxs-lookup"><span data-stu-id="f073c-118">We’ve named this role “Support Request Contributor” and that’s how we refer toohello custom role in this article.</span></span>

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

<span data-ttu-id="f073c-119">Выполните hello действия, описанные в [в этом видеоролике](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn как toocreate пользовательской роли для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="f073c-119">Follow hello steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn how toocreate a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a><span data-ttu-id="f073c-120">Создание и управление ими запросов поддержки в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f073c-120">Create and manage support requests in hello Azure portal</span></span>

<span data-ttu-id="f073c-121">Рассмотрим пример — вы являетесь владельцем hello подписки «Visual Studio подписки MSDN.»</span><span class="sxs-lookup"><span data-stu-id="f073c-121">Let’s take an example – you are hello owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="f073c-122">Сергей является вашей однорангового узла, являющийся toosome владельца ресурса hello групп ресурсов в этой подписке и имеет подписки toohello разрешение "чтение".</span><span class="sxs-lookup"><span data-stu-id="f073c-122">Joe is your peer who is a resource owner toosome of hello resource groups in this subscription and has read permission toohello subscription.</span></span>
<span data-ttu-id="f073c-123">Правильно toogive доступа tooyour однорангового узла, Joe, toocreate возможность hello и управление запросами в службу поддержки для hello ресурсов в данной подписке.</span><span class="sxs-lookup"><span data-stu-id="f073c-123">You wish toogive access tooyour peer, Joe, hello ability toocreate and manage support tickets for hello resources under this subscription.</span></span>

1. <span data-ttu-id="f073c-124">Первый шаг Hello — toogo toohello подписки и в поле «Параметры» появится список пользователей.</span><span class="sxs-lookup"><span data-stu-id="f073c-124">hello first step is toogo toohello subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="f073c-125">Выберите пользователя hello Joe, кто имеет доступ для чтения на hello подписки и позволяет назначить новый toohim пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="f073c-125">Click hello user Joe who has reader access on hello Subscription and let’s assign a new custom role toohim.</span></span>

    ![Добавление роли](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="f073c-127">В колонке «Пользователи» hello, щелкните «Добавить».</span><span class="sxs-lookup"><span data-stu-id="f073c-127">Click "Add" under hello "Users" blade.</span></span> <span data-ttu-id="f073c-128">Выберите hello пользовательской роли «Участник запросов поддержки» из списка hello ролей</span><span class="sxs-lookup"><span data-stu-id="f073c-128">Select hello custom role "Support Request Contributor" from hello list of roles</span></span>

    ![Добавление роли участника с доступом к службе поддержки](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="f073c-130">После выбора имени роли hello, нажмите «Добавить пользователей» и введите учетные данные электронной почты hello Джо.</span><span class="sxs-lookup"><span data-stu-id="f073c-130">After selecting hello role name, click "Add users" and enter hello Joe's email credentials.</span></span> <span data-ttu-id="f073c-131">Нажмите "Выбрать".</span><span class="sxs-lookup"><span data-stu-id="f073c-131">Click "Select"</span></span>

    ![Добавление пользователей](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="f073c-133">Нажмите кнопку «ОК» tooproceed</span><span class="sxs-lookup"><span data-stu-id="f073c-133">Click "Ok" tooproceed</span></span>

    ![Предоставление доступа](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="f073c-135">Вы увидите hello пользователя с вновь добавленный hello пользовательской роли «Поддержка запроса участник» в подписке hello, для которого вы являетесь владельцем hello</span><span class="sxs-lookup"><span data-stu-id="f073c-135">Now you see hello user with hello newly added custom role "Support Request Contributor" under hello Subscription for which you are hello owner</span></span>

    ![Добавлен пользователь](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="f073c-137">При входе в портал hello Joe он видит toowhich подписки hello, когда он был добавлен.</span><span class="sxs-lookup"><span data-stu-id="f073c-137">When Joe logs in hello portal, he sees hello subscription toowhich he was added.</span></span>

7. <span data-ttu-id="f073c-138">Сергей нажимает кнопку «Нового запроса на обслуживание» из колонки «Справка и поддержка» hello и можно создать запросы на поддержку для «Visual Studio Ultimate с MSDN»</span><span class="sxs-lookup"><span data-stu-id="f073c-138">Joe clicks "New Support request" from hello "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Новый запрос на техническую поддержку](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="f073c-140">Нажав кнопку «Все поддерживают запросы» Joe можно просмотреть список запросов поддержки, созданному для этой подписки hello ![случае представление сведений](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="f073c-140">Clicking "All support requests" Joe can see hello list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-hello-azure-portal"></a><span data-ttu-id="f073c-141">Удаление поддержки запрашивать доступ в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f073c-141">Remove support request access in hello Azure portal</span></span>

<span data-ttu-id="f073c-142">Так же, как она возможных toogrant доступа tooa пользователя toocreate и управление запросами на поддержку это возможных tooremove доступ также пользователю hello.</span><span class="sxs-lookup"><span data-stu-id="f073c-142">Just as it is possible toogrant access tooa user toocreate and manage support requests, it's possible tooremove access for hello user as well.</span></span>
<span data-ttu-id="f073c-143">tooremove hello toocreate возможность управлять запросов поддержки, перейдите toohello подписки, нажмите кнопку «Параметры» и нажмите кнопку hello пользователя (в данном случае Joe).</span><span class="sxs-lookup"><span data-stu-id="f073c-143">tooremove hello ability toocreate and manage support requests, go toohello Subscription, click "Settings" and click hello user (in this case, Joe).</span></span>
<span data-ttu-id="f073c-144">Щелкните правой кнопкой мыши имя роли hello, «Участник запросов поддержки» и нажмите кнопку «Удалить»</span><span class="sxs-lookup"><span data-stu-id="f073c-144">Right-click hello role name, "Support Request Contributor" and click "Remove"</span></span>

![Отзыв доступа для создания запросов на поддержку](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="f073c-146">Если Сергей журналы портала toohello и пытается установить toocreate запрос на техническую поддержку, он обнаруживает hello следующая ошибка</span><span class="sxs-lookup"><span data-stu-id="f073c-146">When Joe logs in toohello portal and tries toocreate a support request, he encounters hello following error</span></span>

![Ошибка подписки 2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="f073c-148">Дмитрий не сможет просмотреть запросы на поддержку, щелкнув "Все запросы на поддержку".</span><span class="sxs-lookup"><span data-stu-id="f073c-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![Представление сведений об обращении 2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
