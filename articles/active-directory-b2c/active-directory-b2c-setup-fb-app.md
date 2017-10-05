---
title: "Azure Active Directory B2C: настройка Facebook | Документация Майкрософт"
description: "Обеспечьте регистрацию и вход для пользователей с учетными записями Facebook в приложениях, защищенных с помощью Azure Active Directory B2C."
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
ms.openlocfilehash: 8c2154fcf33537358b549395d15b4ba937371cd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-facebook-accounts"></a><span data-ttu-id="e89aa-103">Azure Active Directory B2C: регистрация и вход пользователей с учетными записями Facebook</span><span class="sxs-lookup"><span data-stu-id="e89aa-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="e89aa-104">Создание приложения Facebook</span><span class="sxs-lookup"><span data-stu-id="e89aa-104">Create a Facebook application</span></span>
<span data-ttu-id="e89aa-105">Чтобы использовать Facebook в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо сначала создать приложение Facebook и задать в нем правильные параметры.</span><span class="sxs-lookup"><span data-stu-id="e89aa-105">To use Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Facebook application and supply it with the right parameters.</span></span> <span data-ttu-id="e89aa-106">Для этого потребуется учетная запись Facebook.</span><span class="sxs-lookup"><span data-stu-id="e89aa-106">You need a Facebook account to do this.</span></span> <span data-ttu-id="e89aa-107">Если у вас ее нет, создайте ее на сайте [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="e89aa-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="e89aa-108">Перейдите на [веб-сайт разработчиков Facebook](https://developers.facebook.com/) и войдите с помощью учетной записи Facebook.</span><span class="sxs-lookup"><span data-stu-id="e89aa-108">Go to the [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="e89aa-109">Если вы этого еще не сделали, необходимо зарегистрироваться в качестве разработчика Facebook.</span><span class="sxs-lookup"><span data-stu-id="e89aa-109">If you have not already done so, you need to register as a Facebook developer.</span></span> <span data-ttu-id="e89aa-110">Для этого щелкните **Register** (Зарегистрироваться) в правом верхнем углу страницы, примите политики Facebook и завершите регистрацию.</span><span class="sxs-lookup"><span data-stu-id="e89aa-110">To do this, click **Register** (on the upper-right corner of the page), accept Facebook's policies, and complete the registration steps.</span></span>
3. <span data-ttu-id="e89aa-111">Щелкните **Мои приложения**, а затем — **Добавить новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="e89aa-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="e89aa-112">В форме укажите значения в полях **Отображаемое название** и **Эл. адрес для связи**.</span><span class="sxs-lookup"><span data-stu-id="e89aa-112">In the form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="e89aa-113">Нажмите кнопку **Создайте ID приложения**.</span><span class="sxs-lookup"><span data-stu-id="e89aa-113">Click **Create App ID**.</span></span> <span data-ttu-id="e89aa-114">Для этого может потребоваться принять условия политики платформы Facebook и пройти проверку безопасности в сети.</span><span class="sxs-lookup"><span data-stu-id="e89aa-114">This may require you to accept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="e89aa-115">В левом столбце щелкните **Настройки**, затем выберите пункт **Основное**, если он не выбран.</span><span class="sxs-lookup"><span data-stu-id="e89aa-115">In the left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="e89aa-116">Выберите **категорию**.</span><span class="sxs-lookup"><span data-stu-id="e89aa-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="e89aa-117">Щелкните **+Добавить платформу** и выберите **Веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="e89aa-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook — настройки](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook — настройки — веб-сайт](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="e89aa-120">Введите `https://login.microsoftonline.com/` в поле **URL-адрес сайта** и щелкните **Сохранить изменения** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e89aa-120">Enter `https://login.microsoftonline.com/` in the **Site URL** field and then click **Save Changes** at the bottom of the page.</span></span>
   
    ![Facebook — URL-адрес сайта](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="e89aa-122">Скопируйте значение **App ID**(Идентификатор приложения).</span><span class="sxs-lookup"><span data-stu-id="e89aa-122">Copy the value of **App ID**.</span></span> <span data-ttu-id="e89aa-123">Нажмите кнопку **Show** (Показать) и скопируйте значение **App Secret** (Секрет приложения).</span><span class="sxs-lookup"><span data-stu-id="e89aa-123">Click **Show** and copy the value of **App Secret**.</span></span> <span data-ttu-id="e89aa-124">Оба значения необходимы для настройки Facebook в качестве поставщика удостоверений для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="e89aa-124">You will need both of them to configure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="e89aa-125">**Секрет приложения** — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="e89aa-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook — идентификатор приложения и секрет приложения](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="e89aa-127">В области навигации слева щелкните **+ Add Product** (+ Добавить продукт), а затем нажмите кнопку **Настройка** рядом с разделом **Facebook Login** (Вход в Facebook).</span><span class="sxs-lookup"><span data-stu-id="e89aa-127">Click **+ Add Product** on the left navigation and then the **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook — вход в Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="e89aa-129">Щелкните **Параметры** на правой панели навигации в разделе **Facebook Login** (Вход в Facebook).</span><span class="sxs-lookup"><span data-stu-id="e89aa-129">Click **Settings** on the right nav under **Facebook Login**</span></span>

    ![Facebook — параметры входа в Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="e89aa-131">В разделе **Client OAuth Settings** (Параметры OAuth клиента) в поле **Valid OAuth redirect URIs** (Допустимые URI перенаправления OAuth) введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="e89aa-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Valid OAuth redirect URIs** field in the **Client OAuth Settings** section.</span></span> <span data-ttu-id="e89aa-132">Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="e89aa-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="e89aa-133">Нажмите кнопку **Save Changes** (Сохранить изменения) в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e89aa-133">Click **Save Changes** at the bottom of the page.</span></span>
    
    ![Facebook — универсальный код ресурса (URI) перенаправления OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="e89aa-135">Чтобы подготовить приложение Facebook к использованию Azure AD B2C, необходимо сделать его общедоступным.</span><span class="sxs-lookup"><span data-stu-id="e89aa-135">To make your Facebook application usable by Azure AD B2C, you need to make it publicly available.</span></span> <span data-ttu-id="e89aa-136">Для этого можно щелкнуть **App Review** (Просмотр приложения) в области навигации слева и выбрать для переключателя в верхней части страницы значение **Yes** (Да). Затем следует щелкнуть **Confirm** (Подтвердить).</span><span class="sxs-lookup"><span data-stu-id="e89aa-136">You can do this by clicking **App Review** on the left navigation and by turning the switch at the top of the page to **YES** and clicking **Confirm**.</span></span>
    
    ![Facebook — публикация приложения](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="e89aa-138">Настройка Facebook в качестве поставщика удостоверений для клиента</span><span class="sxs-lookup"><span data-stu-id="e89aa-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="e89aa-139">Выполните эти действия, чтобы [перейти к колонке функций B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e89aa-139">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="e89aa-140">В колонке функций B2C щелкните **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="e89aa-140">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="e89aa-141">Нажмите **+Добавить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="e89aa-141">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="e89aa-142">Укажите понятное **имя** конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="e89aa-142">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="e89aa-143">Например, введите Facebook.</span><span class="sxs-lookup"><span data-stu-id="e89aa-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="e89aa-144">Щелкните **Identity provider type** (Тип поставщика удостоверений), выберите **Facebook** и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="e89aa-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="e89aa-145">Щелкните **Set up this identity provider** (Настроить этот поставщик удостоверений) и введите идентификатор и секрет приложения (ранее созданного приложения Facebook) в поля **Идентификатор клиента** и **Секрет клиента** соответственно.</span><span class="sxs-lookup"><span data-stu-id="e89aa-145">Click **Set up this identity provider** and enter the app ID and app secret (of the Facebook application that you created earlier) in the **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="e89aa-146">Нажмите кнопку **ОК**, а затем — **Создать**, чтобы сохранить конфигурацию Facebook.</span><span class="sxs-lookup"><span data-stu-id="e89aa-146">Click **OK**, and then click **Create** to save your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="e89aa-147">При добавлении **поставщика удостоверений** в клиент имеющиеся политики не изменяются.</span><span class="sxs-lookup"><span data-stu-id="e89aa-147">Adding an **Identity provider** to your tenant does not modify your existing policies.</span></span> <span data-ttu-id="e89aa-148">Не забудьте обновить политики, добавив созданный поставщик удостоверений.</span><span class="sxs-lookup"><span data-stu-id="e89aa-148">Remember to update your policies by including the identity provider you just created.</span></span>
>