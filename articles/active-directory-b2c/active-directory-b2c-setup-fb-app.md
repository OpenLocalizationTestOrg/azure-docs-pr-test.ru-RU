---
title: "Azure Active Directory B2C: настройка Facebook | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями Facebook в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a><span data-ttu-id="cbd3f-103">Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Facebook</span><span class="sxs-lookup"><span data-stu-id="cbd3f-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="cbd3f-104">Создание приложения Facebook</span><span class="sxs-lookup"><span data-stu-id="cbd3f-104">Create a Facebook application</span></span>
<span data-ttu-id="cbd3f-105">toouse Facebook как поставщик удостоверений в Azure Active Directory (Azure AD) B2C требуется toocreate приложение Facebook и передайте в него hello нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-105">toouse Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Facebook application and supply it with hello right parameters.</span></span> <span data-ttu-id="cbd3f-106">Требуется toodo учетную запись Facebook.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-106">You need a Facebook account toodo this.</span></span> <span data-ttu-id="cbd3f-107">Если у вас ее нет, создайте ее на сайте [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="cbd3f-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="cbd3f-108">Go toohello [Facebook для разработчиков](https://developers.facebook.com/) веб-сайта и выполните вход с вашей Facebook учетные данные учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-108">Go toohello [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="cbd3f-109">Если вы еще не сделали необходимо tooregister разработчику Facebook.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-109">If you have not already done so, you need tooregister as a Facebook developer.</span></span> <span data-ttu-id="cbd3f-110">toodo, нажмите кнопку **зарегистрировать** (на hello правом верхнем углу страницы приветствия) принятия политик, Facebook и выполните действия по регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-110">toodo this, click **Register** (on hello upper-right corner of hello page), accept Facebook's policies, and complete hello registration steps.</span></span>
3. <span data-ttu-id="cbd3f-111">Щелкните **Мои приложения**, а затем — **Добавить новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="cbd3f-112">В форме hello предоставляют **отображаемое имя** и является допустимым **адрес электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-112">In hello form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="cbd3f-113">Нажмите кнопку **Создайте ID приложения**.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-113">Click **Create App ID**.</span></span> <span data-ttu-id="cbd3f-114">Это может потребовать tooaccept Facebook платформы политик и проверки безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-114">This may require you tooaccept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="cbd3f-115">В левом столбце hello, щелкните **параметры** , а затем выберите **основные** Если не было сделано ранее.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-115">In hello left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="cbd3f-116">Выберите **категорию**.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="cbd3f-117">Щелкните **+Добавить платформу** и выберите **Веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook — настройки](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook — настройки — веб-сайт](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="cbd3f-120">Введите `https://login.microsoftonline.com/` в hello **URL-адрес сайта** и нажмите кнопку **сохранить изменения** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-120">Enter `https://login.microsoftonline.com/` in hello **Site URL** field and then click **Save Changes** at hello bottom of hello page.</span></span>
   
    ![Facebook — URL-адрес сайта](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="cbd3f-122">Скопируйте значение hello **идентификатор приложения**.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-122">Copy hello value of **App ID**.</span></span> <span data-ttu-id="cbd3f-123">Нажмите кнопку **Показать** и скопируйте значение hello **секрет приложения**.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-123">Click **Show** and copy hello value of **App Secret**.</span></span> <span data-ttu-id="cbd3f-124">Вам потребуется обеих функций tooconfigure Facebook в качестве поставщика удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-124">You will need both of them tooconfigure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="cbd3f-125">**Секрет приложения** — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook — идентификатор приложения и секрет приложения](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="cbd3f-127">Нажмите кнопку **+ добавить продукт** hello навигации слева, а затем hello **Set Up** кнопку для **входа Facebook**.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-127">Click **+ Add Product** on hello left navigation and then hello **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook — вход в Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="cbd3f-129">Нажмите кнопку **параметры** на hello правая панель навигации в разделе **входа Facebook**</span><span class="sxs-lookup"><span data-stu-id="cbd3f-129">Click **Settings** on hello right nav under **Facebook Login**</span></span>

    ![Facebook — параметры входа в Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="cbd3f-131">Введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **OAuth допустимый URI перенаправления** в hello **параметры клиента OAuth** раздела.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Valid OAuth redirect URIs** field in hello **Client OAuth Settings** section.</span></span> <span data-ttu-id="cbd3f-132">Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="cbd3f-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="cbd3f-133">Нажмите кнопку **сохранить изменения** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-133">Click **Save Changes** at hello bottom of hello page.</span></span>
    
    ![Facebook — универсальный код ресурса (URI) перенаправления OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="cbd3f-135">toomake приложения Facebook можно использовать с Azure AD B2C, toomake необходимо его общедоступным.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-135">toomake your Facebook application usable by Azure AD B2C, you need toomake it publicly available.</span></span> <span data-ttu-id="cbd3f-136">Это можно сделать, щелкнув **проверки приложения** на hello слева навигации и путем включения hello переключиться в начале hello страницы приветствия слишком**Да** и щелкнув **Подтверждение**.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-136">You can do this by clicking **App Review** on hello left navigation and by turning hello switch at hello top of hello page too**YES** and clicking **Confirm**.</span></span>
    
    ![Facebook — публикация приложения](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="cbd3f-138">Настройка Facebook в качестве поставщика удостоверений для клиента</span><span class="sxs-lookup"><span data-stu-id="cbd3f-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="cbd3f-139">Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-139">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="cbd3f-140">В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-140">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="cbd3f-141">Нажмите кнопку **+ добавить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-141">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="cbd3f-142">Укажите понятное **имя** hello конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-142">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="cbd3f-143">Например, введите Facebook.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="cbd3f-144">Щелкните **Identity provider type** (Тип поставщика удостоверений), выберите **Facebook** и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="cbd3f-145">Нажмите кнопку **настройки этого поставщика удостоверений** и введите hello приложения код и приложения секрет (hello приложения Facebook, которое было создано ранее) в hello **идентификатор клиента** и **секрет клиента**поля соответственно.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-145">Click **Set up this identity provider** and enter hello app ID and app secret (of hello Facebook application that you created earlier) in hello **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="cbd3f-146">Нажмите кнопку **ОК**, а затем нажмите кнопку **создать** toosave конфигурацию Facebook.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-146">Click **OK**, and then click **Create** toosave your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="cbd3f-147">Добавление **поставщика удостоверений** tooyour клиента не изменяет существующие политики.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-147">Adding an **Identity provider** tooyour tenant does not modify your existing policies.</span></span> <span data-ttu-id="cbd3f-148">Запомнить tooupdate политик, включая hello поставщик удостоверений, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="cbd3f-148">Remember tooupdate your policies by including hello identity provider you just created.</span></span>
>