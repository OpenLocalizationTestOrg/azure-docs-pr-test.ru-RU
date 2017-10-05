---
title: "Azure Active Directory B2C: настройка Google+ | Документация Майкрософт"
description: "Обеспечение регистрации и входа для пользователей с учетными записями Google+ в приложениях, защищенных с помощью Azure Active Directory B2C."
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
ms.openlocfilehash: 6ab73e5c79742ab548733f5712dee1e28461db9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-google-accounts"></a><span data-ttu-id="7af7c-103">Azure Active Directory B2C: организация регистрации и входа для потребителей с учетными записями Google+</span><span class="sxs-lookup"><span data-stu-id="7af7c-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="7af7c-104">Создание приложения Google+</span><span class="sxs-lookup"><span data-stu-id="7af7c-104">Create a Google+ application</span></span>
<span data-ttu-id="7af7c-105">Чтобы использовать Google+ в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо сначала создать приложение Google+ и задать в нем правильные параметры.</span><span class="sxs-lookup"><span data-stu-id="7af7c-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="7af7c-106">Для этого потребуется учетная запись Google+.</span><span class="sxs-lookup"><span data-stu-id="7af7c-106">You need a Google+ account to do this.</span></span> <span data-ttu-id="7af7c-107">Если у вас ее нет, вы можете создать такую учетную запись на странице [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="7af7c-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="7af7c-108">Перейдите на сайт [Google Developers Console](https://console.developers.google.com/) и выполните вход с учетной записью Google+.</span><span class="sxs-lookup"><span data-stu-id="7af7c-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="7af7c-109">Щелкните **Create project** (Создать проект), введите значение в поле **Project name** (Имя проекта) и щелкните **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="7af7c-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+: приступая к работе](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+: создание проекта](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="7af7c-112">В левой области навигации щелкните **API Manager** (Менеджер API), а затем — **Credentials** (Учетные данные).</span><span class="sxs-lookup"><span data-stu-id="7af7c-112">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
4. <span data-ttu-id="7af7c-113">Щелкните вкладку **OAuth consent screen** (Экран согласия OAuth) вверху.</span><span class="sxs-lookup"><span data-stu-id="7af7c-113">Click the **OAuth consent screen** tab at the top.</span></span>
   
    ![Google+: учетные данные](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="7af7c-115">Выберите или укажите допустимый **электронный адрес**, заполните поле **Product name** (Название продукта) и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="7af7c-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+: экран согласия OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="7af7c-117">Щелкните **New credentials** (Создать учетные данные) и выберите **OAuth client ID** (Идентификатор клиента OAuth).</span><span class="sxs-lookup"><span data-stu-id="7af7c-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+: экран согласия OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="7af7c-119">Из списка **Application type** (Тип приложения) выберите **Web application** (Веб-приложение).</span><span class="sxs-lookup"><span data-stu-id="7af7c-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+: экран согласия OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="7af7c-121">В поле **Name** (Имя) введите имя приложения, затем введите `https://login.microsoftonline.com` в поле **Authorized JavaScript origins** (Авторизованные источники JavaScript) и `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` — в поле **Authorized redirect URIs** (Авторизованные URI перенаправления).</span><span class="sxs-lookup"><span data-stu-id="7af7c-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="7af7c-122">Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="7af7c-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="7af7c-123">В значении **{клиент}** необходимо учитывать регистр.</span><span class="sxs-lookup"><span data-stu-id="7af7c-123">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="7af7c-124">Щелкните **Create**(Создать).</span><span class="sxs-lookup"><span data-stu-id="7af7c-124">Click **Create**.</span></span>
   
    ![Google+: создание идентификатора клиента](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="7af7c-126">Скопируйте значения **Идентификатор клиента** и **Секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="7af7c-126">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="7af7c-127">Оба значения необходимы для настройки Google+ в качестве поставщика удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="7af7c-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="7af7c-128">**Секрет клиента** — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="7af7c-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+: секрет клиента](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="7af7c-130">Настройка Google+ в качестве поставщика удостоверений в клиенте</span><span class="sxs-lookup"><span data-stu-id="7af7c-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="7af7c-131">Выполните эти действия, чтобы [перейти к колонке функций B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7af7c-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="7af7c-132">В колонке функций B2C щелкните **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="7af7c-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="7af7c-133">Нажмите **+Добавить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="7af7c-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="7af7c-134">Укажите понятное **имя** конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7af7c-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="7af7c-135">Например, введите G+.</span><span class="sxs-lookup"><span data-stu-id="7af7c-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="7af7c-136">Щелкните **Тип поставщика удостоверений**, выберите **Google** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7af7c-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="7af7c-137">Щелкните **Настроить этот поставщик удостоверений** и введите идентификатор клиента и секрет клиента ранее созданного приложения Google+.</span><span class="sxs-lookup"><span data-stu-id="7af7c-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="7af7c-138">Нажмите кнопку **ОК**, а затем — **Создать**, чтобы сохранить конфигурацию Google+.</span><span class="sxs-lookup"><span data-stu-id="7af7c-138">Click **OK** and then click **Create** to save your Google+ configuration.</span></span>

