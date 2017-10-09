---
title: "aaaCreate удостоверение для приложения Azure в портале | Документы Microsoft"
description: "Описывает уровень доступа tooresources toocreate новое приложение Azure Active Directory и службы-участника, который может использоваться с элементом управления доступом на основе hello в toomanage диспетчера ресурсов Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="d5372-103">Использование портала toocreate приложения Azure Active Directory и участника-службы, могут обращаться к ресурсам</span><span class="sxs-lookup"><span data-stu-id="d5372-103">Use portal toocreate an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="d5372-104">Если у вас есть приложение, которое требуется tooaccess или изменить ресурсы, необходимо настроить приложение Azure Active Directory (AD) и назначить tooit hello необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="d5372-104">When you have an application that needs tooaccess or modify resources, you must set up an Azure Active Directory (AD) application and assign hello required permissions tooit.</span></span> <span data-ttu-id="d5372-105">Этот подход является более предпочтительным, чем toorunning приложение hello в своих собственных учетных данных, так как:</span><span class="sxs-lookup"><span data-stu-id="d5372-105">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="d5372-106">Можно назначить разрешения удостоверение приложения toohello, отличаются от собственных разрешений.</span><span class="sxs-lookup"><span data-stu-id="d5372-106">You can assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="d5372-107">Как правило эти разрешения являются ограниченными tooexactly какие hello приложению toodo.</span><span class="sxs-lookup"><span data-stu-id="d5372-107">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="d5372-108">У вас приложение hello toochange учетные данные при изменении ваши обязанности.</span><span class="sxs-lookup"><span data-stu-id="d5372-108">You do not have toochange hello app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="d5372-109">При выполнении сценария автоматической можно использовать проверку подлинности сертификата tooautomate.</span><span class="sxs-lookup"><span data-stu-id="d5372-109">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>

<span data-ttu-id="d5372-110">В этом разделе показано, как tooperform те проходит через портал hello.</span><span class="sxs-lookup"><span data-stu-id="d5372-110">This topic shows you how tooperform those steps through hello portal.</span></span> <span data-ttu-id="d5372-111">Этот раздел посвящен приложения одного клиента, где приложение hello предполагаемого toorun только одной организации.</span><span class="sxs-lookup"><span data-stu-id="d5372-111">It focuses on a single-tenant application where hello application is intended toorun within only one organization.</span></span> <span data-ttu-id="d5372-112">Обычно однотенантная архитектура используется для создания бизнес-приложений в рамках организации.</span><span class="sxs-lookup"><span data-stu-id="d5372-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="d5372-113">Необходимые разрешения</span><span class="sxs-lookup"><span data-stu-id="d5372-113">Required permissions</span></span>
<span data-ttu-id="d5372-114">toocomplete в этом разделе, необходимо иметь достаточные разрешения tooregister приложения с клиентом Azure AD и назначить роли tooa приложения hello в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="d5372-114">toocomplete this topic, you must have sufficient permissions tooregister an application with your Azure AD tenant, and assign hello application tooa role in your Azure subscription.</span></span> <span data-ttu-id="d5372-115">Давайте убедитесь, что имеется hello нужные разрешения tooperform эти действия.</span><span class="sxs-lookup"><span data-stu-id="d5372-115">Let's make sure you have hello right permissions tooperform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="d5372-116">Проверка разрешений в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5372-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="d5372-117">Войдите в tooyour учетную запись Azure через hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5372-117">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d5372-118">Выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5372-118">Select **Azure Active Directory**.</span></span>

     ![Выбор Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="d5372-120">В Azure Active Directory выберите **Параметры пользователя**.</span><span class="sxs-lookup"><span data-stu-id="d5372-120">In Azure Active Directory, select **User settings**.</span></span>

     ![Выбор параметров пользователя](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="d5372-122">Проверьте hello **регистрации приложения** параметр.</span><span class="sxs-lookup"><span data-stu-id="d5372-122">Check hello **App registrations** setting.</span></span> <span data-ttu-id="d5372-123">Если задать слишком**Да**, не являющихся администраторами пользователи могут регистрировать приложения AD.</span><span class="sxs-lookup"><span data-stu-id="d5372-123">If set too**Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="d5372-124">Этот параметр означает, что любой пользователь в клиенте Azure AD hello можно зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="d5372-124">This setting means any user in hello Azure AD tenant can register an app.</span></span> <span data-ttu-id="d5372-125">Можно продолжить слишком[прав доступа к подпискам Azure проверьте](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="d5372-125">You can proceed too[Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![Проверка регистрации приложений](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="d5372-127">Если параметр регистрации приложения hello задано слишком**нет**, только администраторы могут регистрировать приложения.</span><span class="sxs-lookup"><span data-stu-id="d5372-127">If hello app registrations setting is set too**No**, only admin users can register apps.</span></span> <span data-ttu-id="d5372-128">Необходимо toocheck ли ваша учетная запись имеет права администратора для клиента Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="d5372-128">You need toocheck whether your account is an admin for hello Azure AD tenant.</span></span> <span data-ttu-id="d5372-129">В разделе "Быстрые задачи" щелкните **Обзор**, а затем выберите **Найти пользователя**.</span><span class="sxs-lookup"><span data-stu-id="d5372-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Пункт "Найти пользователя"](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="d5372-131">Найдите свою учетную запись и выберите ее.</span><span class="sxs-lookup"><span data-stu-id="d5372-131">Search for your account, and select it when you find it.</span></span>

     ![Поиск пользователя](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="d5372-133">В разделе со сведениями об учетной записи щелкните **Роль каталога**.</span><span class="sxs-lookup"><span data-stu-id="d5372-133">For your account, select **Directory role**.</span></span> 

     ![Пункт "Роль каталога"](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="d5372-135">Просмотрите назначенную роль каталога в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5372-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="d5372-136">Если ваша учетная запись назначена роль пользователя toohello, но hello параметр регистрации приложения (из предыдущих шагах hello) является ограниченной tooadmin пользователей, попросите вашего администратора tooeither назначить вы tooan роль администратора или tooenable пользователей tooregister приложений.</span><span class="sxs-lookup"><span data-stu-id="d5372-136">If your account is assigned toohello User role, but hello app registration setting (from hello preceding steps) is limited tooadmin users, ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

     ![Просмотр роли](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="d5372-138">Проверка прав доступа к подпискам Azure</span><span class="sxs-lookup"><span data-stu-id="d5372-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="d5372-139">В подписке Azure учетной записи должно быть `Microsoft.Authorization/*/Write` доступ к tooassign tooa роль AD.</span><span class="sxs-lookup"><span data-stu-id="d5372-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access tooassign an AD app tooa role.</span></span> <span data-ttu-id="d5372-140">Это действие предоставляется посредством hello [владельца](../active-directory/role-based-access-built-in-roles.md#owner) роли или [администратор доступа пользователя](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) роли.</span><span class="sxs-lookup"><span data-stu-id="d5372-140">This action is granted through hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="d5372-141">Если ваша учетная запись назначается toohello **участника** роли, у вас достаточно разрешений.</span><span class="sxs-lookup"><span data-stu-id="d5372-141">If your account is assigned toohello **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="d5372-142">Вы получите ошибку при попытке роль участника tooa tooassign hello службы.</span><span class="sxs-lookup"><span data-stu-id="d5372-142">You will receive an error when attempting tooassign hello service principal tooa role.</span></span> 

<span data-ttu-id="d5372-143">toocheck разрешения по подписке:</span><span class="sxs-lookup"><span data-stu-id="d5372-143">toocheck your subscription permissions:</span></span>

1. <span data-ttu-id="d5372-144">Если вы не уже видите учетной записи Azure AD из предыдущих шагах hello, выберите **Azure Active Directory** hello левой панели.</span><span class="sxs-lookup"><span data-stu-id="d5372-144">If you are not already looking at your Azure AD account from hello preceding steps, select **Azure Active Directory** from hello left pane.</span></span>

2. <span data-ttu-id="d5372-145">Найдите свою учетную запись Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5372-145">Find your Azure AD account.</span></span> <span data-ttu-id="d5372-146">В разделе "Быстрые задачи" щелкните **Обзор**, а затем выберите **Найти пользователя**.</span><span class="sxs-lookup"><span data-stu-id="d5372-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Пункт "Найти пользователя"](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="d5372-148">Найдите свою учетную запись и выберите ее.</span><span class="sxs-lookup"><span data-stu-id="d5372-148">Search for your account, and select it when you find it.</span></span>

     ![Поиск пользователя](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="d5372-150">Щелкните **Ресурсы Azure**.</span><span class="sxs-lookup"><span data-stu-id="d5372-150">Select **Azure resources**.</span></span>

     ![Выбор ресурсов](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="d5372-152">Просмотр назначенных ролей и определите tooassign соответствующие разрешения роли приложения tooa AD.</span><span class="sxs-lookup"><span data-stu-id="d5372-152">View your assigned roles, and determine if you have adequate permissions tooassign an AD app tooa role.</span></span> <span data-ttu-id="d5372-153">Если это не так, попросите администратора вашей подписки tooadd вы tooUser доступа к роли администратора.</span><span class="sxs-lookup"><span data-stu-id="d5372-153">If not, ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span> <span data-ttu-id="d5372-154">Следующие изображения hello назначенный toohello роли-владельца для двух подписок, это означает, что этот пользователь имеет достаточные разрешения является пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="d5372-154">In hello following image, hello user is assigned toohello Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![Просмотр разрешений](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="d5372-156">Создание приложения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5372-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="d5372-157">Войдите в tooyour учетную запись Azure через hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5372-157">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d5372-158">Выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5372-158">Select **Azure Active Directory**.</span></span>

     ![Выбор Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="d5372-160">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="d5372-160">Select **App registrations**.</span></span>   

     ![Пункт "Регистрация приложений"](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="d5372-162">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d5372-162">Select **Add**.</span></span>

     ![Действие "Добавить приложение"](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="d5372-164">Укажите имя и URL-адрес для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d5372-164">Provide a name and URL for hello application.</span></span> <span data-ttu-id="d5372-165">Выберите либо **веб-приложения и API** или **собственного** для типа приложения hello требуется toocreate.</span><span class="sxs-lookup"><span data-stu-id="d5372-165">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="d5372-166">После задания значения hello, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="d5372-166">After setting hello values, select **Create**.</span></span>

     ![указание имени приложения](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="d5372-168">Приложение создано.</span><span class="sxs-lookup"><span data-stu-id="d5372-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="d5372-169">Получение идентификатора приложения и ключа проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="d5372-169">Get application ID and authentication key</span></span>
<span data-ttu-id="d5372-170">Программным способом входа в систему требуется идентификатор hello для приложения и ключ проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d5372-170">When programmatically logging in, you need hello ID for your application and an authentication key.</span></span> <span data-ttu-id="d5372-171">те значения, tooget hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="d5372-171">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="d5372-172">В Azure Active Directory в разделе **Регистрация приложений** выберите нужное приложение.</span><span class="sxs-lookup"><span data-stu-id="d5372-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![Выбор приложения](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="d5372-174">Копировать hello **идентификатор приложения** и сохранить ее в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="d5372-174">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="d5372-175">Здравствуйте, приложения hello [образцы приложений](#sample-applications) значение toothis, что идентификатор hello клиента см. раздел.</span><span class="sxs-lookup"><span data-stu-id="d5372-175">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![Идентификатор клиента](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="d5372-177">Выберите ключ проверки подлинности toogenerate **ключей**.</span><span class="sxs-lookup"><span data-stu-id="d5372-177">toogenerate an authentication key, select **Keys**.</span></span>

     ![Пункт "Ключи"](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="d5372-179">Введите описание ключа hello и длительность для ключа hello.</span><span class="sxs-lookup"><span data-stu-id="d5372-179">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="d5372-180">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d5372-180">When done, select **Save**.</span></span>

     ![Сохранение ключа](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="d5372-182">После сохранения ключа hello, отображается значение hello hello ключа.</span><span class="sxs-lookup"><span data-stu-id="d5372-182">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="d5372-183">Скопируйте это значение невозможно, поскольку ключ может tooretrieve hello позже.</span><span class="sxs-lookup"><span data-stu-id="d5372-183">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="d5372-184">Значение ключа hello предоставить toolog идентификатор приложения hello в как приложение hello.</span><span class="sxs-lookup"><span data-stu-id="d5372-184">You provide hello key value with hello application ID toolog in as hello application.</span></span> <span data-ttu-id="d5372-185">Сохраните значение ключа hello, где приложение может вернуть их.</span><span class="sxs-lookup"><span data-stu-id="d5372-185">Store hello key value where your application can retrieve it.</span></span>

     ![сохраненный ключ](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="d5372-187">Получение идентификатора клиента</span><span class="sxs-lookup"><span data-stu-id="d5372-187">Get tenant ID</span></span>
<span data-ttu-id="d5372-188">Программным способом входа в систему необходимо ИД клиента toopass hello вместе с запросом проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d5372-188">When programmatically logging in, you need toopass hello tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="d5372-189">Идентификатор клиента hello tooget, выберите **свойства** для вашего клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5372-189">tooget hello tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![Выбор свойств Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="d5372-191">Копировать hello **каталог с Идентификатором**.</span><span class="sxs-lookup"><span data-stu-id="d5372-191">Copy hello **Directory ID**.</span></span> <span data-ttu-id="d5372-192">Это и есть ваш идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="d5372-192">This value is your tenant ID.</span></span>

     ![Идентификатор клиента](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a><span data-ttu-id="d5372-194">Назначьте toorole приложения</span><span class="sxs-lookup"><span data-stu-id="d5372-194">Assign application toorole</span></span>
<span data-ttu-id="d5372-195">tooaccess ресурсам в подписке, необходимо назначить роль tooa приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d5372-195">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="d5372-196">Решите, какую роль представляет hello нужные разрешения для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d5372-196">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="d5372-197">toolearn о hello доступным ролям, в разделе [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d5372-197">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="d5372-198">Можно установить область hello на уровне hello hello подписки, группы ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d5372-198">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="d5372-199">Разрешения, наследуемые toolower уровни области действия.</span><span class="sxs-lookup"><span data-stu-id="d5372-199">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="d5372-200">Например для добавления роли модуля чтения toohello приложения для группы ресурсов есть может считать группы ресурсов hello и все ресурсы, которые он содержит.</span><span class="sxs-lookup"><span data-stu-id="d5372-200">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="d5372-201">Перейти на уровень toohello области, в которых надо tooassign hello приложению.</span><span class="sxs-lookup"><span data-stu-id="d5372-201">Navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="d5372-202">Например, tooassign роль в области hello подписки, выберите **подписки**.</span><span class="sxs-lookup"><span data-stu-id="d5372-202">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="d5372-203">Или же вы можете выбрать группу ресурсов либо отдельный ресурс.</span><span class="sxs-lookup"><span data-stu-id="d5372-203">You could instead select a resource group or resource.</span></span>

     ![выбрать подписку](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="d5372-205">Выберите приложение hello tooassign hello определенной подписки (группа ресурсов или ресурсов) для.</span><span class="sxs-lookup"><span data-stu-id="d5372-205">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![выбрать подписку для назначения](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="d5372-207">Выберите **Управление доступом (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="d5372-207">Select **Access Control (IAM)**.</span></span>

     ![выбрать доступ](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="d5372-209">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d5372-209">Select **Add**.</span></span>

     ![выбрать "добавить"](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="d5372-211">Выберите роль hello нужно tooassign toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="d5372-211">Select hello role you wish tooassign toohello application.</span></span> <span data-ttu-id="d5372-212">Hello на рисунке показаны hello **чтения** роли.</span><span class="sxs-lookup"><span data-stu-id="d5372-212">hello following image shows hello **Reader** role.</span></span>

     ![выбрать роль](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="d5372-214">Найдите приложение и выберите его.</span><span class="sxs-lookup"><span data-stu-id="d5372-214">Search for your application, and select it.</span></span>

     ![Поиск приложения](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="d5372-216">Выберите **ОК** toofinish назначение роли hello.</span><span class="sxs-lookup"><span data-stu-id="d5372-216">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="d5372-217">Вы видите приложение hello списка пользователей, назначенных роли tooa для данной области.</span><span class="sxs-lookup"><span data-stu-id="d5372-217">You see your application in hello list of users assigned tooa role for that scope.</span></span>

## <a name="log-in-as-hello-application"></a><span data-ttu-id="d5372-218">Войдите в систему как приложение hello</span><span class="sxs-lookup"><span data-stu-id="d5372-218">Log in as hello application</span></span>

<span data-ttu-id="d5372-219">Настройка приложения в Azure Active Directory завершена.</span><span class="sxs-lookup"><span data-stu-id="d5372-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="d5372-220">У вас есть код и ключа toouse для входа в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="d5372-220">You have an ID and key toouse for signing in as hello application.</span></span> <span data-ttu-id="d5372-221">приложение Hello назначается роль tooa делает ее определенные действия, которые они могут выполнять.</span><span class="sxs-lookup"><span data-stu-id="d5372-221">hello application is assigned tooa role that gives it certain actions it can perform.</span></span> <span data-ttu-id="d5372-222">Сведения о входе в систему как hello приложения с помощью различных платформ см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="d5372-222">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="d5372-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5372-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="d5372-224">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="d5372-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="d5372-225">REST</span><span class="sxs-lookup"><span data-stu-id="d5372-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="d5372-226">.NET</span><span class="sxs-lookup"><span data-stu-id="d5372-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="d5372-227">Java</span><span class="sxs-lookup"><span data-stu-id="d5372-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="d5372-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="d5372-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="d5372-229">Python</span><span class="sxs-lookup"><span data-stu-id="d5372-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="d5372-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="d5372-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="d5372-231">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5372-231">Next steps</span></span>
* <span data-ttu-id="d5372-232">tooset копирование многопользовательского приложения, в разделе [tooauthorization руководство разработчика с hello API диспетчера ресурсов Azure](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d5372-232">tooset up a multi-tenant application, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="d5372-233">toolearn о политике безопасности, в разделе [управления доступом на основе ролей Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d5372-233">toolearn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="d5372-234">Список доступных действий, которые могут быть предоставлены или запрещены toousers см. в разделе [операций поставщика ресурсов диспетчера ресурсов Azure](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d5372-234">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
