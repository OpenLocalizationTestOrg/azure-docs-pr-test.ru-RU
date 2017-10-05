---
title: "Azure Active Directory B2C: настройка учетной записи Майкрософт | Документация Майкрософт"
description: "Регистрация и вход пользователей с помощью учетных записей Майкрософт в приложениях, защищенных с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 59879dc0b3fc1d7af3e2a1f67f1701f451de9126
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-microsoft-accounts"></a><span data-ttu-id="2168f-103">Azure Active Directory (AD) B2C: организация регистрации и входа для потребителей с учетными записями Microsoft</span><span class="sxs-lookup"><span data-stu-id="2168f-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="2168f-104">Создание приложения для учетной записи Майкрософт</span><span class="sxs-lookup"><span data-stu-id="2168f-104">Create a Microsoft account application</span></span>
<span data-ttu-id="2168f-105">Чтобы использовать учетную запись Майкрософт в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо сначала создать приложение для учетной записи Майкрософт и задать в нем правильные параметры.</span><span class="sxs-lookup"><span data-stu-id="2168f-105">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="2168f-106">Для этого требуется учетная запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2168f-106">You need a Microsoft account to do this.</span></span> <span data-ttu-id="2168f-107">Если у вас ее нет, вы можете создать такую учетную запись на сайте [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="2168f-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="2168f-108">Перейдите в [Центр регистрации приложений Майкрософт](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) и войдите с помощью своей учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2168f-108">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="2168f-109">Нажмите кнопку **Добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="2168f-109">Click **Add an app**.</span></span>
   
    ![Учетная запись Майкрософт: добавление нового приложения](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="2168f-111">Укажите **имя** приложения и нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="2168f-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Учетная запись Майкрософт: имя приложения](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="2168f-113">Скопируйте значение **Идентификатор приложения**. Оно необходимо для настройки учетной записи Майкрософт в качестве поставщика удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="2168f-113">Copy the value of **Application Id**. You will need it to configure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Учетная запись Майкрософт: идентификатор приложения](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="2168f-115">Щелкните **Добавить платформу** и выберите параметр **Веб**.</span><span class="sxs-lookup"><span data-stu-id="2168f-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Учетная запись Майкрософт: добавление платформы](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Учетная запись Майкрософт: веб](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="2168f-118">Введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в поле **URI перенаправления** .</span><span class="sxs-lookup"><span data-stu-id="2168f-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="2168f-119">Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="2168f-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Учетная запись Майкрософт: URL-адрес перенаправления](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="2168f-121">Щелкните **Создать новый пароль** в разделе **Секреты приложения**.</span><span class="sxs-lookup"><span data-stu-id="2168f-121">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="2168f-122">Скопируйте новый пароль с экрана.</span><span class="sxs-lookup"><span data-stu-id="2168f-122">Copy the new password displayed on screen.</span></span> <span data-ttu-id="2168f-123">Оно необходимо для настройки учетной записи Майкрософт в качестве поставщика удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="2168f-123">You will need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="2168f-124">Данный пароль — важный элемент обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="2168f-124">This password is an important security credential.</span></span>
   
    ![Microsoft учетной записи: создание нового пароля](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft учетной записи: новый пароль](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="2168f-127">Установите флажок **Поддержка Live SDK** в разделе **Дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="2168f-127">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="2168f-128">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2168f-128">Click **Save**.</span></span>
   
    ![Учетная запись Майкрософт: поддержка Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="2168f-130">Настройка учетной записи Майкрософт в качестве поставщика удостоверений в клиенте</span><span class="sxs-lookup"><span data-stu-id="2168f-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="2168f-131">Выполните эти действия, чтобы [перейти к колонке функций B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2168f-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="2168f-132">В колонке функций B2C щелкните **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="2168f-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="2168f-133">Нажмите **+Добавить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="2168f-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="2168f-134">Укажите понятное **имя** конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="2168f-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="2168f-135">Например, введите "MSA".</span><span class="sxs-lookup"><span data-stu-id="2168f-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="2168f-136">Щелкните **Тип поставщика удостоверений**, выберите **Учетная запись Майкрософт** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2168f-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="2168f-137">Щелкните **Настроить этот поставщик удостоверений** и введите идентификатор приложения и пароль ранее созданного приложения учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2168f-137">Click **Set up this identity provider** and enter the Application Id and password of the Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="2168f-138">Нажмите кнопку **ОК**, а затем — **Создать**, чтобы сохранить конфигурацию учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2168f-138">Click **OK** and then click **Create** to save your Microsoft account configuration.</span></span>

