---
title: "Авторизация учетных записей разработчиков с помощью Azure Active Directory B2C в службе управления API Azure | Документация Майкрософт"
description: "Сведения об авторизации пользователей с помощью Azure Active Directory B2C в службе управления API."
services: api-management
documentationcenter: API Management
author: miaojiang
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: eb7deb1a79d9db9ac5cfbea69b8d3c564eb55577
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="6c5cb-103">Как авторизовать учетные записи разработчиков с помощью Azure Active Directory B2C в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="6c5cb-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="6c5cb-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6c5cb-104">Overview</span></span>
<span data-ttu-id="6c5cb-105">Azure Active Directory B2C — это облачное решение, позволяющее управлять удостоверениями в веб-приложениях и мобильных приложениях, с которыми взаимодействуют клиенты.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="6c5cb-106">Его можно использовать для управления доступом к порталу разработчика.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-106">You can use it to manage access to your developer portal.</span></span> <span data-ttu-id="6c5cb-107">В этом руководстве объясняется, как настроить службу управления API для интеграции с Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="6c5cb-108">Сведения о предоставлении доступа к порталу разработчика с помощью классической службы Azure Active Directory см. в статье [Авторизация учетных записей разработчиков с помощью Azure Active Directory в управлении API Azure].</span><span class="sxs-lookup"><span data-stu-id="6c5cb-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="6c5cb-109">Для выполнения шагов в этом руководстве вам сначала потребуется клиент Azure Active Directory B2C для создания в нем приложения.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span></span> <span data-ttu-id="6c5cb-110">Кроме того, необходимо настроить политики регистрации и входа.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-110">Also, you need to have signup and signin policies ready.</span></span> <span data-ttu-id="6c5cb-111">Дополнительные сведения см. в статье [Azure Active Directory B2C: регистрация и вход пользователей в приложения].</span><span class="sxs-lookup"><span data-stu-id="6c5cb-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="6c5cb-112">Авторизация учетных записей разработчиков с помощью Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="6c5cb-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="6c5cb-113">Чтобы начать работу, щелкните **Портал издателя** на портале Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="6c5cb-114">Будет открыт портал издателя службы управления API.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-114">This takes you to the API Management publisher portal.</span></span>

   ![Портал издателя][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="6c5cb-116">Если вы еще не создали экземпляр службы управления API, см. сведения в разделе [Создание экземпляра управления API][Create an API Management service instance] руководства [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="6c5cb-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="6c5cb-117">В меню **Управление API** выберите **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-117">On the **API Management** menu, click **Security**.</span></span> <span data-ttu-id="6c5cb-118">На вкладке **Удостоверения** выберите **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Внешние удостоверения 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="6c5cb-120">Запишите **URL-адрес перенаправления** и переключитесь на Azure Active Directory B2C на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span></span>

  ![Внешние удостоверения 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="6c5cb-122">Нажмите кнопку **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-122">Click the **Applications** button.</span></span>

  ![Регистрация нового приложения 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="6c5cb-124">Нажмите кнопку **Добавить**, чтобы создать новое приложение Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span></span>

  ![Регистрация нового приложения 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="6c5cb-126">В колонке **Новое приложение** введите имя для приложения.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-126">In the **New application** blade, enter a name for the application.</span></span> <span data-ttu-id="6c5cb-127">Выберите **Да** под параметром **Веб-приложения и веб-API** и **Да** под параметром **Разрешить неявный поток**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="6c5cb-128">Скопируйте **URL-адрес перенаправления** в разделе **Azure Active Directory B2C** на вкладке **Удостоверения** портала издателя и вставьте его в текстовое поле **URL-адрес ответа**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span></span>

  ![Регистрация нового приложения 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="6c5cb-130">Нажмите кнопку **Создать** .</span><span class="sxs-lookup"><span data-stu-id="6c5cb-130">Click the **Create** button.</span></span> <span data-ttu-id="6c5cb-131">Когда приложение будет создано, оно появится в колонке **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-131">When the application is created, it appears in the **Applications** blade.</span></span> <span data-ttu-id="6c5cb-132">Щелкните имя приложения, чтобы просмотреть сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-132">Click the application name to see its details.</span></span>

  ![Регистрация нового приложения 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="6c5cb-134">В колонке **Свойства** скопируйте в буфер обмена **Идентификатор приложения**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span></span>

  ![Идентификатор приложения 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="6c5cb-136">Вернитесь на портал издателя и вставьте скопированный идентификатор в текстовое поле **Идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span></span>

  ![Идентификатор приложения 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="6c5cb-138">Вернитесь на портал Azure, щелкните раздел **Ключи**, а затем нажмите кнопку **Создать ключ**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="6c5cb-139">Нажмите кнопку **Сохранить**, чтобы сохранить конфигурацию и отобразить **Ключ приложения**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-139">Click **Save** to save the configuration and display the **App key**.</span></span> <span data-ttu-id="6c5cb-140">Скопируйте этот ключ в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-140">Copy the key to the clipboard.</span></span>

  ![Ключ приложения 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="6c5cb-142">Вернитесь на портал издателя и вставьте скопированный ключ в текстовое поле **Секрет клиента** .</span><span class="sxs-lookup"><span data-stu-id="6c5cb-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

  ![Ключ приложения 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="6c5cb-144">Укажите имя домена клиента Azure Active Directory B2C в поле **Разрешенный клиент**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Разрешенный клиент][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="6c5cb-146">Укажите **политику регистрации** и **политику входа**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-146">Specify the **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="6c5cb-147">Дополнительно можно также указать **политику редактирования профиля** и **политику сброса пароля**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Политики][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="6c5cb-149">Дополнительные сведения о политиках см. в статье [Azure Active Directory B2C: расширяемая инфраструктура политик].</span><span class="sxs-lookup"><span data-stu-id="6c5cb-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="6c5cb-150">После указания требуемой конфигурации нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-150">After you've specified the desired configuration, click **Save**.</span></span>

  <span data-ttu-id="6c5cb-151">После сохранения изменений разработчики смогут создавать новые учетные записи и входить на портал разработчика с помощью Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="6c5cb-152">Регистрация учетных записей разработчиков с помощью Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="6c5cb-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="6c5cb-153">Чтобы зарегистрировать учетную запись разработчика с помощью Azure Active Directory B2C, откройте новое окно браузера и перейдите на портал разработчика.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span></span> <span data-ttu-id="6c5cb-154">Нажмите кнопку **Зарегистрироваться**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-154">Click the **Sign up** button.</span></span>

   ![Портал разработчика 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="6c5cb-156">Выберите регистрацию с помощью **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-156">Choose to sign up with **Azure Active Directory B2C**.</span></span>

   ![Портал разработчика 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="6c5cb-158">Вы будете перенаправлены к политике регистрации, настроенной в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-158">You're redirected to the signup policy that you configured in the previous section.</span></span> <span data-ttu-id="6c5cb-159">Выберите регистрацию с помощью адреса электронной почты или существующей учетной записи социальных сетей.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-159">Choose to sign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6c5cb-160">Если Azure Active Directory B2C является единственным активным параметром на вкладке **Удостоверения** на портале издателя, вы будете сразу перенаправлены к политике регистрации.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span></span>

   ![Портал разработчика][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="6c5cb-162">После завершения регистрации вы будете перенаправлены обратно на портал разработчика.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-162">When the signup is complete, you're redirected back to the developer portal.</span></span> <span data-ttu-id="6c5cb-163">Теперь вы вошли на портал разработчика вашего экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="6c5cb-163">You're now signed in to the developer portal for your API Management service instance.</span></span>

    ![Регистрация завершена][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="6c5cb-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c5cb-165">Next steps</span></span>

*  <span data-ttu-id="6c5cb-166">[Azure Active Directory B2C: регистрация и вход пользователей в приложения]</span><span class="sxs-lookup"><span data-stu-id="6c5cb-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="6c5cb-167">[Azure Active Directory B2C: расширяемая инфраструктура политик]</span><span class="sxs-lookup"><span data-stu-id="6c5cb-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="6c5cb-168">[Azure Active Directory (AD) B2C: организация регистрации и входа для потребителей с учетными записями Microsoft]</span><span class="sxs-lookup"><span data-stu-id="6c5cb-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="6c5cb-169">[Azure Active Directory B2C: организация регистрации и входа для потребителей с учетными записями Google+]</span><span class="sxs-lookup"><span data-stu-id="6c5cb-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="6c5cb-170">[Azure Active Directory B2C: регистрация и вход пользователей с помощью учетных записей LinkedIn]</span><span class="sxs-lookup"><span data-stu-id="6c5cb-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="6c5cb-171">[Azure Active Directory B2C: регистрация и вход пользователей с учетными записями Facebook]</span><span class="sxs-lookup"><span data-stu-id="6c5cb-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
<span data-ttu-id="6c5cb-172">[Azure Active Directory B2C: регистрация и вход пользователей в приложения]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span><span class="sxs-lookup"><span data-stu-id="6c5cb-172">[Azure Active Directory B2C overview]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span></span>
<span data-ttu-id="6c5cb-173">[Авторизация учетных записей разработчиков с помощью Azure Active Directory в управлении API Azure]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span><span class="sxs-lookup"><span data-stu-id="6c5cb-173">[How to authorize developer accounts using Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span></span>
<span data-ttu-id="6c5cb-174">[Azure Active Directory B2C: расширяемая инфраструктура политик]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span><span class="sxs-lookup"><span data-stu-id="6c5cb-174">[Azure Active Directory B2C: Extensible policy framework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span></span>
<span data-ttu-id="6c5cb-175">[Azure Active Directory (AD) B2C: организация регистрации и входа для потребителей с учетными записями Microsoft]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span><span class="sxs-lookup"><span data-stu-id="6c5cb-175">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span></span>
<span data-ttu-id="6c5cb-176">[Azure Active Directory B2C: организация регистрации и входа для потребителей с учетными записями Google+]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span><span class="sxs-lookup"><span data-stu-id="6c5cb-176">[Use a Google account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span></span>
<span data-ttu-id="6c5cb-177">[Azure Active Directory B2C: регистрация и вход пользователей с учетными записями Facebook]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span><span class="sxs-lookup"><span data-stu-id="6c5cb-177">[Use a Facebook account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span></span>
<span data-ttu-id="6c5cb-178">[Azure Active Directory B2C: регистрация и вход пользователей с помощью учетных записей LinkedIn]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span><span class="sxs-lookup"><span data-stu-id="6c5cb-178">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span></span>

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
