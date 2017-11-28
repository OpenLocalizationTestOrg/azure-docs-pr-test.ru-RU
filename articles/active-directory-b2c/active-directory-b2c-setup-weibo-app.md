---
title: "Azure Active Directory B2C: настройка Weibo | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями Weibo в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a><span data-ttu-id="68781-103">Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Weibo</span><span class="sxs-lookup"><span data-stu-id="68781-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="68781-104">Эта функция предоставляется в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="68781-104">This feature is in preview.</span></span> <span data-ttu-id="68781-105">Не используйте этот поставщик удостоверений в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="68781-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="68781-106">Создание приложения Weibo</span><span class="sxs-lookup"><span data-stu-id="68781-106">Create a Weibo application</span></span>

<span data-ttu-id="68781-107">toouse Weibo как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения Weibo и передайте в него hello нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="68781-107">toouse Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Weibo application and supply it with hello right parameters.</span></span> <span data-ttu-id="68781-108">Требуется toodo Weibo учетной записи.</span><span class="sxs-lookup"><span data-stu-id="68781-108">You need a Weibo account toodo this.</span></span> <span data-ttu-id="68781-109">Если у вас ее нет, эту учетную запись можно получить по адресу: [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="68781-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-hello-weibo-developer-program"></a><span data-ttu-id="68781-110">Регистрация для разработчика Weibo hello</span><span class="sxs-lookup"><span data-stu-id="68781-110">Register for hello Weibo developer program</span></span>

1. <span data-ttu-id="68781-111">Go toohello [портал разработчиков Weibo](http://open.weibo.com/) и выполните вход с учетными данными Weibo.</span><span class="sxs-lookup"><span data-stu-id="68781-111">Go toohello [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="68781-112">После входа в систему, щелкните в правом верхнем углу hello отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="68781-112">After signing in, click on your display name in hello top-right corner.</span></span>
3. <span data-ttu-id="68781-113">Выберите в раскрывающемся списке hello,**编辑开发者信息**(изменить сведения о разработке).</span><span class="sxs-lookup"><span data-stu-id="68781-113">In hello dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="68781-114">Введите в форму hello hello необходимые сведения и нажмите кнопку**提交**(отправить).</span><span class="sxs-lookup"><span data-stu-id="68781-114">Enter hello required information into hello form and click **提交** (submit).</span></span>
5. <span data-ttu-id="68781-115">Завершить процесс проверки по электронной почте hello.</span><span class="sxs-lookup"><span data-stu-id="68781-115">Complete hello email verification process.</span></span>
6. <span data-ttu-id="68781-116">Go toohello [страницы проверки удостоверения](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="68781-116">Go toohello [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="68781-117">Введите в форму hello hello необходимые сведения и нажмите кнопку**提交**(отправить).</span><span class="sxs-lookup"><span data-stu-id="68781-117">Enter hello required information into hello form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="68781-118">Регистрация приложения Weibo</span><span class="sxs-lookup"><span data-stu-id="68781-118">Register a Weibo application</span></span>

1. <span data-ttu-id="68781-119">Go toohello [новую страницу регистрации приложения Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="68781-119">Go toohello [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="68781-120">Введите сведения о необходимости приложения hello.</span><span class="sxs-lookup"><span data-stu-id="68781-120">Enter hello necessary application information.</span></span>
3. <span data-ttu-id="68781-121">Щелкните **创建** (Создать).</span><span class="sxs-lookup"><span data-stu-id="68781-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="68781-122">Скопируйте значения hello **ключ приложения** и **секрет приложения**.</span><span class="sxs-lookup"><span data-stu-id="68781-122">Copy hello values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="68781-123">Этот идентификатор потребуется позднее.</span><span class="sxs-lookup"><span data-stu-id="68781-123">You will need this later.</span></span>
5. <span data-ttu-id="68781-124">Отправить фото необходимые hello и введите необходимые сведения hello.</span><span class="sxs-lookup"><span data-stu-id="68781-124">Upload hello required photos and enter hello necessary information.</span></span>
6. <span data-ttu-id="68781-125">Щелкните **保存以上信息** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="68781-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="68781-126">Щелкните **高级信息** (Дополнительные сведения).</span><span class="sxs-lookup"><span data-stu-id="68781-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="68781-127">Нажмите кнопку**编辑**(изменить) следующего поля toohello для OAuth2.0**授权设置**(перенаправление URL-адреса).</span><span class="sxs-lookup"><span data-stu-id="68781-127">Click **编辑** (edit) next toohello field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="68781-128">Введите `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` в поле **授权设置** (URL-адрес перенаправления) для OAuth2.0.</span><span class="sxs-lookup"><span data-stu-id="68781-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="68781-129">Например если ваш `tenant_name` — contoso.onmicrosoft.com toobe URL-адрес набора hello `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="68781-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="68781-130">Щелкните **提交** (Отправить).</span><span class="sxs-lookup"><span data-stu-id="68781-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="68781-131">Настройка Weibo в качестве поставщика удостоверений в клиенте</span><span class="sxs-lookup"><span data-stu-id="68781-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="68781-132">Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="68781-132">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="68781-133">В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="68781-133">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="68781-134">Нажмите кнопку **+ добавить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="68781-134">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="68781-135">Укажите понятное **имя** hello конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="68781-135">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="68781-136">Например, введите "Weibo".</span><span class="sxs-lookup"><span data-stu-id="68781-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="68781-137">Щелкните **Тип поставщика удостоверений**, выберите **Weibo** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="68781-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="68781-138">Щелкните **Настроить этот поставщик удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="68781-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="68781-139">Введите hello **ключ приложения** , скопированное ранее как hello **идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="68781-139">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="68781-140">Введите hello **секрет приложения** , скопированное ранее как hello **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="68781-140">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="68781-141">Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave Weibo конфигурации.</span><span class="sxs-lookup"><span data-stu-id="68781-141">Click **OK** and then click **Create** toosave your Weibo configuration.</span></span>

