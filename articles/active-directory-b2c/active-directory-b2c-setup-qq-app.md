---
title: "Azure Active Directory B2C: настройка QQ | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями б в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a><span data-ttu-id="e4b9b-103">Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями б</span><span class="sxs-lookup"><span data-stu-id="e4b9b-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="e4b9b-104">Эта функция предоставляется в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="e4b9b-105">Создание приложения QQ</span><span class="sxs-lookup"><span data-stu-id="e4b9b-105">Create a QQ application</span></span>

<span data-ttu-id="e4b9b-106">toouse б как поставщик удостоверений в Azure Active Directory (Azure AD) B2C требуется toocreate приложение б и предоставить его hello нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-106">toouse QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a QQ application and supply it with hello right parameters.</span></span> <span data-ttu-id="e4b9b-107">Требуется toodo б учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-107">You need a QQ account toodo this.</span></span> <span data-ttu-id="e4b9b-108">Если у вас ее нет, ее можно получить на странице [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="e4b9b-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-hello-qq-developer-program"></a><span data-ttu-id="e4b9b-109">Регистрация для разработчика б hello</span><span class="sxs-lookup"><span data-stu-id="e4b9b-109">Register for hello QQ developer program</span></span>

1. <span data-ttu-id="e4b9b-110">Go toohello [портал разработчиков б](http://open.qq.com) и выполните вход с учетными данными б.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-110">Go toohello [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="e4b9b-111">После входа в систему, перейдите слишком[http://open.qq.com/reg](http://open.qq.com/reg) tooregister самостоятельно разработчику.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-111">After signing in, go too[http://open.qq.com/reg](http://open.qq.com/reg) tooregister yourself as a developer.</span></span>
3. <span data-ttu-id="e4b9b-112">Выберите в меню hello**个人**(отдельных разработчиков).</span><span class="sxs-lookup"><span data-stu-id="e4b9b-112">In hello menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="e4b9b-113">Введите в форму hello hello необходимые сведения и нажмите кнопку**下一步**(следующий шаг).</span><span class="sxs-lookup"><span data-stu-id="e4b9b-113">Enter hello required information into hello form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="e4b9b-114">Завершить процесс проверки по электронной почте hello.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-114">Complete hello email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="e4b9b-115">Вам потребуется toowait toobe несколько дней, утвержденные после регистрации разработчику.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-115">You will need toowait a few days toobe approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="e4b9b-116">Регистрация приложения QQ</span><span class="sxs-lookup"><span data-stu-id="e4b9b-116">Register a QQ application</span></span>

1. <span data-ttu-id="e4b9b-117">Go слишком[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="e4b9b-117">Go too[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="e4b9b-118">Щелкните**应用管理**(Управление приложениями).</span><span class="sxs-lookup"><span data-stu-id="e4b9b-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="e4b9b-119">Щелкните**创建应用**(Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="e4b9b-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="e4b9b-120">Введите сведения о необходимости приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-120">Enter hello necessary app information.</span></span>
5. <span data-ttu-id="e4b9b-121">Щелкните**创建应用**(Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="e4b9b-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="e4b9b-122">Введите сведения о необходимых hello.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-122">Enter hello required information.</span></span>
7. <span data-ttu-id="e4b9b-123">Для hello**授权回调域**(URL-адрес обратного вызова) введите `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-123">For hello **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="e4b9b-124">Например если ваш `tenant_name` — contoso.onmicrosoft.com toobe URL-адрес набора hello `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="e4b9b-125">Щелкните**创建应用**(Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="e4b9b-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="e4b9b-126">На странице подтверждения hello, нажмите кнопку**应用管理**страницы управления приложения toohello tooreturn (Управление приложениями).</span><span class="sxs-lookup"><span data-stu-id="e4b9b-126">On hello confirmation page, click on **应用管理** (app management) tooreturn toohello app management page.</span></span>
10. <span data-ttu-id="e4b9b-127">Щелкните**查看**(Просмотр) Далее toohello приложения вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-127">Click on **查看** (view) next toohello app you just created.</span></span>
11. <span data-ttu-id="e4b9b-128">Щелкните**修改**(Изменить).</span><span class="sxs-lookup"><span data-stu-id="e4b9b-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="e4b9b-129">Hello вверху страницы приветствия, скопируйте hello **идентификатор приложения** и **ключ приложения**.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-129">From hello top of hello page, copy hello **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="e4b9b-130">Настройка QQ в качестве поставщика удостоверений в клиенте</span><span class="sxs-lookup"><span data-stu-id="e4b9b-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="e4b9b-131">Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="e4b9b-132">В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="e4b9b-133">Нажмите кнопку **+ добавить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="e4b9b-134">Укажите понятное **имя** hello конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="e4b9b-135">Например, введите "QQ".</span><span class="sxs-lookup"><span data-stu-id="e4b9b-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="e4b9b-136">Щелкните **Тип поставщика удостоверений**, выберите **QQ** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="e4b9b-137">Щелкните **Настроить этот поставщик удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="e4b9b-138">Введите hello **ключ приложения** , скопированное ранее как hello **идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-138">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="e4b9b-139">Введите hello **секрет приложения** , скопированное ранее как hello **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-139">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="e4b9b-140">Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave конфигурацию б.</span><span class="sxs-lookup"><span data-stu-id="e4b9b-140">Click **OK** and then click **Create** toosave your QQ configuration.</span></span>

