---
title: "Azure Active Directory B2C: настройка учетной записи Майкрософт | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями Microsoft в приложениях, которые защищены с помощью Azure Active Directory B2C."
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
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a><span data-ttu-id="f05e6-103">Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Microsoft</span><span class="sxs-lookup"><span data-stu-id="f05e6-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="f05e6-104">Создание приложения для учетной записи Майкрософт</span><span class="sxs-lookup"><span data-stu-id="f05e6-104">Create a Microsoft account application</span></span>
<span data-ttu-id="f05e6-105">Учетная запись Майкрософт toouse как поставщик удостоверений в Azure Active Directory (Azure AD) B2C, требуется toocreate приложение учетной записи Microsoft и передайте в него hello нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="f05e6-105">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="f05e6-106">Требуется toodo учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f05e6-106">You need a Microsoft account toodo this.</span></span> <span data-ttu-id="f05e6-107">Если у вас ее нет, вы можете создать такую учетную запись на сайте [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="f05e6-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="f05e6-108">Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) и выполните вход с помощью учетных данных вашей учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f05e6-108">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="f05e6-109">Нажмите кнопку **Добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="f05e6-109">Click **Add an app**.</span></span>
   
    ![Учетная запись Майкрософт: добавление нового приложения](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="f05e6-111">Укажите **имя** приложения и нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="f05e6-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Учетная запись Майкрософт: имя приложения](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="f05e6-113">Скопируйте значение hello **идентификатор приложения**. Вам потребуется tooconfigure учетную запись Майкрософт как поставщик удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="f05e6-113">Copy hello value of **Application Id**. You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Учетная запись Майкрософт: идентификатор приложения](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="f05e6-115">Щелкните **Добавить платформу** и выберите параметр **Веб**.</span><span class="sxs-lookup"><span data-stu-id="f05e6-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Учетная запись Майкрософт: добавление платформы](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Учетная запись Майкрософт: веб](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="f05e6-118">Введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **URI перенаправления** поля.</span><span class="sxs-lookup"><span data-stu-id="f05e6-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="f05e6-119">Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="f05e6-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Учетная запись Майкрософт: URL-адрес перенаправления](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="f05e6-121">Щелкните **создать новый пароль** под hello **секреты приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="f05e6-121">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="f05e6-122">Скопируйте новый пароль hello отображается на экране.</span><span class="sxs-lookup"><span data-stu-id="f05e6-122">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="f05e6-123">Вам потребуется tooconfigure учетную запись Майкрософт как поставщик удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="f05e6-123">You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="f05e6-124">Данный пароль — важный элемент обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="f05e6-124">This password is an important security credential.</span></span>
   
    ![Microsoft учетной записи: создание нового пароля](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft учетной записи: новый пароль](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="f05e6-127">Hello флажок **поддержки пакета SDK Live** под hello **Дополнительно** раздела.</span><span class="sxs-lookup"><span data-stu-id="f05e6-127">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="f05e6-128">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f05e6-128">Click **Save**.</span></span>
   
    ![Учетная запись Майкрософт: поддержка Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="f05e6-130">Настройка учетной записи Майкрософт в качестве поставщика удостоверений в клиенте</span><span class="sxs-lookup"><span data-stu-id="f05e6-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="f05e6-131">Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f05e6-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="f05e6-132">В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="f05e6-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="f05e6-133">Нажмите кнопку **+ добавить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="f05e6-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="f05e6-134">Укажите понятное **имя** hello конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="f05e6-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="f05e6-135">Например, введите "MSA".</span><span class="sxs-lookup"><span data-stu-id="f05e6-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="f05e6-136">Щелкните **Тип поставщика удостоверений**, выберите **Учетная запись Майкрософт** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f05e6-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="f05e6-137">Нажмите кнопку **настройки этого поставщика удостоверений** и введите идентификатор приложения hello и пароль hello приложения учетной записи Майкрософт, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="f05e6-137">Click **Set up this identity provider** and enter hello Application Id and password of hello Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="f05e6-138">Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave конфигурации учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f05e6-138">Click **OK** and then click **Create** toosave your Microsoft account configuration.</span></span>

