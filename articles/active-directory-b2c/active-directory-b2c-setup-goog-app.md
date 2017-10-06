---
title: "Azure Active Directory B2C: настройка Google+ | Документация Майкрософт"
description: "Предоставляют tooconsumers регистрации и входе в систему с учетными записями Google + в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a><span data-ttu-id="4bf4f-103">Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Google +</span><span class="sxs-lookup"><span data-stu-id="4bf4f-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="4bf4f-104">Создание приложения Google+</span><span class="sxs-lookup"><span data-stu-id="4bf4f-104">Create a Google+ application</span></span>
<span data-ttu-id="4bf4f-105">toouse Google + как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения Google + и передайте в него hello нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-105">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="4bf4f-106">Требуется учетная запись toodo Google +.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-106">You need a Google+ account toodo this.</span></span> <span data-ttu-id="4bf4f-107">Если у вас ее нет, вы можете создать такую учетную запись на странице [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="4bf4f-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="4bf4f-108">Go toohello [Google Developers Console](https://console.developers.google.com/) и выполните вход с помощью Google + данные своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-108">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="4bf4f-109">Щелкните **Create project** (Создать проект), введите значение в поле **Project name** (Имя проекта) и щелкните **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="4bf4f-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+: приступая к работе](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+: создание проекта](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="4bf4f-112">Нажмите кнопку **API диспетчера** и нажмите кнопку **учетные данные** в hello навигации слева.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-112">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
4. <span data-ttu-id="4bf4f-113">Нажмите кнопку hello **экран согласия OAuth** вкладку вверху hello.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-113">Click hello **OAuth consent screen** tab at hello top.</span></span>
   
    ![Google+: учетные данные](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="4bf4f-115">Выберите или укажите допустимый **электронный адрес**, заполните поле **Product name** (Название продукта) и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="4bf4f-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+: экран согласия OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="4bf4f-117">Щелкните **New credentials** (Создать учетные данные) и выберите **OAuth client ID** (Идентификатор клиента OAuth).</span><span class="sxs-lookup"><span data-stu-id="4bf4f-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+: экран согласия OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="4bf4f-119">Из списка **Application type** (Тип приложения) выберите **Web application** (Веб-приложение).</span><span class="sxs-lookup"><span data-stu-id="4bf4f-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+: экран согласия OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="4bf4f-121">Укажите **имя** приложения, введите `https://login.microsoftonline.com` в hello **право JavaScript origins** поля, и `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **авторизованные URIперенаправления**поля.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="4bf4f-122">Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4bf4f-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="4bf4f-123">Hello **{tenant}** значение учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-123">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="4bf4f-124">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-124">Click **Create**.</span></span>
   
    ![Google+: создание идентификатора клиента](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="4bf4f-126">Скопируйте значения hello **идентификатор клиента** и **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-126">Copy hello values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="4bf4f-127">Вам потребуется обеих функций tooconfigure Google + как поставщик удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-127">You will need both of them tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="4bf4f-128">**Секрет клиента** — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+: секрет клиента](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="4bf4f-130">Настройка Google+ в качестве поставщика удостоверений в клиенте</span><span class="sxs-lookup"><span data-stu-id="4bf4f-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="4bf4f-131">Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="4bf4f-132">В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="4bf4f-133">Нажмите кнопку **+ добавить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="4bf4f-134">Укажите понятное **имя** hello конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="4bf4f-135">Например, введите G+.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="4bf4f-136">Щелкните **Тип поставщика удостоверений**, выберите **Google** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="4bf4f-137">Нажмите кнопку **настройки этого поставщика удостоверений** и введите hello клиента идентификатор и секрет клиента из hello приложения Google +, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-137">Click **Set up this identity provider** and enter hello client ID and client secret of hello Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="4bf4f-138">Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave конфигурации Google +.</span><span class="sxs-lookup"><span data-stu-id="4bf4f-138">Click **OK** and then click **Create** toosave your Google+ configuration.</span></span>

