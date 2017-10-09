---
title: "aaaAuthorize учетными записями разработчиков с помощью Azure Active Directory B2C - службе управления API Azure | Документы Microsoft"
description: "Узнайте, каким образом tooauthorize пользователей с помощью Azure Active Directory B2C в службе управления API."
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
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="32a5b-103">Как разработчик tooauthorize учетных записей с помощью Azure Active Directory B2C в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="32a5b-103">How tooauthorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="32a5b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="32a5b-104">Overview</span></span>
<span data-ttu-id="32a5b-105">Azure Active Directory B2C — это облачное решение, позволяющее управлять удостоверениями в веб-приложениях и мобильных приложениях, с которыми взаимодействуют клиенты.</span><span class="sxs-lookup"><span data-stu-id="32a5b-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="32a5b-106">Он используется портал разработчиков tooyour toomanage доступа.</span><span class="sxs-lookup"><span data-stu-id="32a5b-106">You can use it toomanage access tooyour developer portal.</span></span> <span data-ttu-id="32a5b-107">В этом руководстве представлены hello конфигурации, необходимые в вашей toointegrate службы управления API с Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="32a5b-107">This guide shows you hello configuration that's required in your API Management service toointegrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="32a5b-108">Сведения о включении портал разработчиков toohello доступ с помощью классической Azure Active Directory см. в разделе [как разработчик tooauthorize учетных записей с помощью Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="32a5b-108">For information about enabling access toohello developer portal by using classic Azure Active Directory, see [How tooauthorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="32a5b-109">toocomplete hello шаги данного руководства, сначала нужно toocreate клиента Azure Active Directory B2C приложение.</span><span class="sxs-lookup"><span data-stu-id="32a5b-109">toocomplete hello steps in this guide, you must first have an Azure Active Directory B2C tenant toocreate an application in.</span></span> <span data-ttu-id="32a5b-110">Кроме того требуются ли toohave регистрации и входа политики готова.</span><span class="sxs-lookup"><span data-stu-id="32a5b-110">Also, you need toohave signup and signin policies ready.</span></span> <span data-ttu-id="32a5b-111">Дополнительные сведения см. в статье [Azure Active Directory B2C: регистрация и вход пользователей в приложения].</span><span class="sxs-lookup"><span data-stu-id="32a5b-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="32a5b-112">Авторизация учетных записей разработчиков с помощью Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="32a5b-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="32a5b-113">tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для вашей службе управления API.</span><span class="sxs-lookup"><span data-stu-id="32a5b-113">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="32a5b-114">Откроется портал издателя управления API toohello.</span><span class="sxs-lookup"><span data-stu-id="32a5b-114">This takes you toohello API Management publisher portal.</span></span>

   ![Портал издателя][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="32a5b-116">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [Приступая к работе с API управления Azure учебника][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="32a5b-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="32a5b-117">На hello **API управления** меню, нажмите кнопку **безопасности**.</span><span class="sxs-lookup"><span data-stu-id="32a5b-117">On hello **API Management** menu, click **Security**.</span></span> <span data-ttu-id="32a5b-118">На hello **удостоверения** выберите **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="32a5b-118">On hello **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Внешние удостоверения 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="32a5b-120">Запишите hello **URL-адрес перенаправления** и переключении tooAzure Active Directory B2C в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="32a5b-120">Make a note of hello **Redirect URL** and switch over tooAzure Active Directory B2C in hello Azure portal.</span></span>

  ![Внешние удостоверения 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="32a5b-122">Нажмите кнопку hello **приложений** кнопки.</span><span class="sxs-lookup"><span data-stu-id="32a5b-122">Click hello **Applications** button.</span></span>

  ![Регистрация нового приложения 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="32a5b-124">Нажмите кнопку hello **добавить** кнопку приложения toocreate новый Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="32a5b-124">Click hello **Add** button toocreate a new Azure Active Directory B2C application.</span></span>

  ![Регистрация нового приложения 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="32a5b-126">В hello **новое приложение** колонки, введите имя для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="32a5b-126">In hello **New application** blade, enter a name for hello application.</span></span> <span data-ttu-id="32a5b-127">Выберите **Да** под параметром **Веб-приложения и веб-API** и **Да** под параметром **Разрешить неявный поток**.</span><span class="sxs-lookup"><span data-stu-id="32a5b-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="32a5b-128">А затем копировать hello **URL-адрес перенаправления** из hello **Azure Active Directory B2C** раздел hello **удостоверения** вкладку в портале издателю hello и вставьте его в hello **URL-адрес ответа** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="32a5b-128">Then copy hello **Redirect URL** from hello **Azure Active Directory B2C** section of hello **Identities** tab in hello publisher portal, and paste it into hello **Reply URL** text box.</span></span>

  ![Регистрация нового приложения 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="32a5b-130">Нажмите кнопку hello **создать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="32a5b-130">Click hello **Create** button.</span></span> <span data-ttu-id="32a5b-131">При создании приложения hello, оно появляется в hello **приложений** колонку.</span><span class="sxs-lookup"><span data-stu-id="32a5b-131">When hello application is created, it appears in hello **Applications** blade.</span></span> <span data-ttu-id="32a5b-132">Щелкните toosee имя приложения hello сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="32a5b-132">Click hello application name toosee its details.</span></span>

  ![Регистрация нового приложения 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="32a5b-134">Из hello **свойства** колонки, hello копирования **идентификатор приложения** toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="32a5b-134">From hello **Properties** blade, copy hello **Application ID** toohello clipboard.</span></span>

  ![Идентификатор приложения 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="32a5b-136">Перейдите назад toohello портал издателя и вставьте идентификатор hello в hello **идентификатор клиента** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="32a5b-136">Switch back toohello publisher portal and paste hello ID into hello **Client Id** text box.</span></span>

  ![Идентификатор приложения 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="32a5b-138">Перейдите назад toohello портал Azure, щелкните hello **ключей** , а затем нажмите **создать ключ**.</span><span class="sxs-lookup"><span data-stu-id="32a5b-138">Switch back toohello Azure portal, click hello **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="32a5b-139">Нажмите кнопку **Сохранить** toosave hello конфигурации и отображения hello **ключ приложения**.</span><span class="sxs-lookup"><span data-stu-id="32a5b-139">Click **Save** toosave hello configuration and display hello **App key**.</span></span> <span data-ttu-id="32a5b-140">Буфер обмена Копировать hello toohello ключа.</span><span class="sxs-lookup"><span data-stu-id="32a5b-140">Copy hello key toohello clipboard.</span></span>

  ![Ключ приложения 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="32a5b-142">Коммутатор задней toohello портала и вставить hello ключ издателя в hello **секрет клиента** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="32a5b-142">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

  ![Ключ приложения 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="32a5b-144">Укажите доменное имя клиента Azure Active Directory B2C hello в hello **допускается клиента**.</span><span class="sxs-lookup"><span data-stu-id="32a5b-144">Specify hello domain name of hello Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Разрешенный клиент][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="32a5b-146">Укажите hello **политики регистрации** и **Signin политики**.</span><span class="sxs-lookup"><span data-stu-id="32a5b-146">Specify hello **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="32a5b-147">При необходимости можно также предоставить hello **редактирование политики профиля** и **политика сброса пароля**.</span><span class="sxs-lookup"><span data-stu-id="32a5b-147">Optionally, you can also provide hello **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Политики][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="32a5b-149">Дополнительные сведения о политиках см. в статье [Azure Active Directory B2C: расширяемая инфраструктура политик].</span><span class="sxs-lookup"><span data-stu-id="32a5b-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="32a5b-150">После выбора hello требуемую конфигурацию, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="32a5b-150">After you've specified hello desired configuration, click **Save**.</span></span>

  <span data-ttu-id="32a5b-151">После сохранения изменений hello разработчикам будет может toocreate новые учетные записи и войдите в портал разработчиков toohello с использованием Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="32a5b-151">After hello changes are saved, developers will be able toocreate new accounts and sign in toohello developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="32a5b-152">Регистрация учетных записей разработчиков с помощью Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="32a5b-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="32a5b-153">toosign для использования учетной записи разработчика с помощью Azure Active Directory B2C откройте новое окно браузера и перейдите на портал разработчиков toohello.</span><span class="sxs-lookup"><span data-stu-id="32a5b-153">toosign up for a developer account by using Azure Active Directory B2C, open a new browser window and go toohello developer portal.</span></span> <span data-ttu-id="32a5b-154">Нажмите кнопку hello **зарегистрироваться** кнопки.</span><span class="sxs-lookup"><span data-stu-id="32a5b-154">Click hello **Sign up** button.</span></span>

   ![Портал разработчика 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="32a5b-156">Выберите toosign с **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="32a5b-156">Choose toosign up with **Azure Active Directory B2C**.</span></span>

   ![Портал разработчика 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="32a5b-158">Вы перенаправленный toohello политики регистрации, настроенную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="32a5b-158">You're redirected toohello signup policy that you configured in hello previous section.</span></span> <span data-ttu-id="32a5b-159">Нажмите кнопку toosign, используя свой адрес электронной почты или один из существующих учетных записей социальных сетей.</span><span class="sxs-lookup"><span data-stu-id="32a5b-159">Choose toosign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="32a5b-160">Если Azure Active Directory B2C hello единственный параметр, который включен в hello **удостоверения** вкладку портала издателя hello, вы будете политики регистрации перенаправленных toohello напрямую.</span><span class="sxs-lookup"><span data-stu-id="32a5b-160">If Azure Active Directory B2C is hello only option that's enabled on hello **Identities** tab in hello publisher portal, you'll be redirected toohello signup policy directly.</span></span>

   ![Портал разработчика][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="32a5b-162">После завершения регистрации hello вы портал разработчиков перенаправленный toohello назад.</span><span class="sxs-lookup"><span data-stu-id="32a5b-162">When hello signup is complete, you're redirected back toohello developer portal.</span></span> <span data-ttu-id="32a5b-163">Теперь, выполнив вход в портал разработчиков toohello для вашего экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="32a5b-163">You're now signed in toohello developer portal for your API Management service instance.</span></span>

    ![Регистрация завершена][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="32a5b-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32a5b-165">Next steps</span></span>

*  <span data-ttu-id="32a5b-166">[Azure Active Directory B2C: регистрация и вход пользователей в приложения]</span><span class="sxs-lookup"><span data-stu-id="32a5b-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="32a5b-167">[Azure Active Directory B2C: расширяемая инфраструктура политик]</span><span class="sxs-lookup"><span data-stu-id="32a5b-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="32a5b-168">[Azure Active Directory (AD) B2C: организация регистрации и входа для потребителей с учетными записями Microsoft]</span><span class="sxs-lookup"><span data-stu-id="32a5b-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="32a5b-169">[Azure Active Directory B2C: организация регистрации и входа для потребителей с учетными записями Google+]</span><span class="sxs-lookup"><span data-stu-id="32a5b-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="32a5b-170">[Azure Active Directory B2C: регистрация и вход пользователей с помощью учетных записей LinkedIn]</span><span class="sxs-lookup"><span data-stu-id="32a5b-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="32a5b-171">[Azure Active Directory B2C: регистрация и вход пользователей с учетными записями Facebook]</span><span class="sxs-lookup"><span data-stu-id="32a5b-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
[Azure Active Directory B2C: регистрация и вход пользователей в приложения]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[как разработчик tooauthorize учетных записей с помощью Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C: расширяемая инфраструктура политик]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Azure Active Directory (AD) B2C: организация регистрации и входа для потребителей с учетными записями Microsoft]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Azure Active Directory B2C: организация регистрации и входа для потребителей с учетными записями Google+]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Azure Active Directory B2C: регистрация и вход пользователей с учетными записями Facebook]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Azure Active Directory B2C: регистрация и вход пользователей с помощью учетных записей LinkedIn]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
