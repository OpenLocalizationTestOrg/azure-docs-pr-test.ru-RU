---
title: "Azure Active Directory B2C: настройка QQ | Документация Майкрософт"
description: "Обеспечение регистрации и входа для пользователей с учетными записями QQ в приложениях, защищенных с помощью Azure Active Directory B2C."
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
ms.openlocfilehash: b32e81494b8c84799485f154ae43ad30af394caa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-qq-accounts"></a><span data-ttu-id="f06a2-103">Azure Active Directory B2C: обеспечение регистрации и входа для пользователей с учетными записями QQ</span><span class="sxs-lookup"><span data-stu-id="f06a2-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="f06a2-104">Эта функция предоставляется в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="f06a2-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="f06a2-105">Создание приложения QQ</span><span class="sxs-lookup"><span data-stu-id="f06a2-105">Create a QQ application</span></span>

<span data-ttu-id="f06a2-106">Чтобы использовать QQ в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо сначала создать приложение QQ и задать в нем правильные параметры.</span><span class="sxs-lookup"><span data-stu-id="f06a2-106">To use QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a QQ application and supply it with the right parameters.</span></span> <span data-ttu-id="f06a2-107">Для этого потребуется учетная запись QQ.</span><span class="sxs-lookup"><span data-stu-id="f06a2-107">You need a QQ account to do this.</span></span> <span data-ttu-id="f06a2-108">Если у вас ее нет, ее можно получить на странице [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="f06a2-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-the-qq-developer-program"></a><span data-ttu-id="f06a2-109">Регистрация в программе разработчиков QQ</span><span class="sxs-lookup"><span data-stu-id="f06a2-109">Register for the QQ developer program</span></span>

1. <span data-ttu-id="f06a2-110">Перейдите на [портал разработчиков QQ](http://open.qq.com) и войдите с помощью своих учетных данных QQ.</span><span class="sxs-lookup"><span data-stu-id="f06a2-110">Go to the [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="f06a2-111">После входа перейдите на страницу [http://open.qq.com/reg](http://open.qq.com/reg), чтобы зарегистрироваться в качестве разработчика.</span><span class="sxs-lookup"><span data-stu-id="f06a2-111">After signing in, go to [http://open.qq.com/reg](http://open.qq.com/reg) to register yourself as a developer.</span></span>
3. <span data-ttu-id="f06a2-112">В меню выберите**个人**(Индивидуальный разработчик).</span><span class="sxs-lookup"><span data-stu-id="f06a2-112">In the menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="f06a2-113">Введите требуемые сведения в форму и нажмите кнопку**下一步**(Следующий шаг).</span><span class="sxs-lookup"><span data-stu-id="f06a2-113">Enter the required information into the form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="f06a2-114">Выполните проверку по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="f06a2-114">Complete the email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="f06a2-115">После регистрации в качестве разработчика вам придется подождать утверждения в течение нескольких дней.</span><span class="sxs-lookup"><span data-stu-id="f06a2-115">You will need to wait a few days to be approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="f06a2-116">Регистрация приложения QQ</span><span class="sxs-lookup"><span data-stu-id="f06a2-116">Register a QQ application</span></span>

1. <span data-ttu-id="f06a2-117">Перейдите на страницу [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="f06a2-117">Go to [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="f06a2-118">Щелкните**应用管理**(Управление приложениями).</span><span class="sxs-lookup"><span data-stu-id="f06a2-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="f06a2-119">Щелкните**创建应用**(Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="f06a2-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="f06a2-120">Введите необходимые сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="f06a2-120">Enter the necessary app information.</span></span>
5. <span data-ttu-id="f06a2-121">Щелкните**创建应用**(Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="f06a2-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="f06a2-122">Введите необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="f06a2-122">Enter the required information.</span></span>
7. <span data-ttu-id="f06a2-123">В поле **授权回调域**(URL-адрес обратного вызова) введите `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f06a2-123">For the **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="f06a2-124">Например если `tenant_name` — contoso.onmicrosoft.com, задайте URL-адрес `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f06a2-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="f06a2-125">Щелкните**创建应用**(Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="f06a2-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="f06a2-126">На странице подтверждения щелкните **应用管理** (Управление приложениями), чтобы вернуться на страницу управления приложениями.</span><span class="sxs-lookup"><span data-stu-id="f06a2-126">On the confirmation page, click on **应用管理** (app management) to return to the app management page.</span></span>
10. <span data-ttu-id="f06a2-127">Щелкните**查看** (Просмотр) рядом с только что созданным приложением.</span><span class="sxs-lookup"><span data-stu-id="f06a2-127">Click on **查看** (view) next to the app you just created.</span></span>
11. <span data-ttu-id="f06a2-128">Щелкните**修改**(Изменить).</span><span class="sxs-lookup"><span data-stu-id="f06a2-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="f06a2-129">В верхней части страницы скопируйте значения **APP ID** (Идентификатор приложения) и **APP KEY** (Ключ приложения).</span><span class="sxs-lookup"><span data-stu-id="f06a2-129">From the top of the page, copy the **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="f06a2-130">Настройка QQ в качестве поставщика удостоверений в клиенте</span><span class="sxs-lookup"><span data-stu-id="f06a2-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="f06a2-131">Выполните эти действия, чтобы [перейти к колонке функций B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f06a2-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="f06a2-132">В колонке функций B2C щелкните **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="f06a2-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="f06a2-133">Нажмите **+Добавить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="f06a2-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="f06a2-134">Укажите понятное **имя** конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="f06a2-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="f06a2-135">Например, введите "QQ".</span><span class="sxs-lookup"><span data-stu-id="f06a2-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="f06a2-136">Щелкните **Тип поставщика удостоверений**, выберите **QQ** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f06a2-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="f06a2-137">Щелкните **Настроить этот поставщик удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="f06a2-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="f06a2-138">Введите **ключ приложения**, скопированный ранее, в поле **Идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="f06a2-138">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="f06a2-139">Введите **секрет приложения**, скопированный ранее, в поле **Секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="f06a2-139">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="f06a2-140">Нажмите кнопку **ОК**, а затем — **Создать**, чтобы сохранить конфигурацию QQ.</span><span class="sxs-lookup"><span data-stu-id="f06a2-140">Click **OK** and then click **Create** to save your QQ configuration.</span></span>

