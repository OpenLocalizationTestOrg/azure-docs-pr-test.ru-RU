---
title: "Azure Active Directory B2C: настройка WeChat | Документация Майкрософт"
description: "Обеспечение регистрации и входа для пользователей с учетными записями WeChat в приложениях, защищенных с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: a54aec23d951610118246e9f70cdd27752ef39a6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-wechat-accounts"></a><span data-ttu-id="f9a3d-103">Azure Active Directory B2C: организация регистрации и входа для потребителей с учетными записями WeChat</span><span class="sxs-lookup"><span data-stu-id="f9a3d-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="f9a3d-104">Эта функция предоставляется в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="f9a3d-105">Создание приложения WeChat</span><span class="sxs-lookup"><span data-stu-id="f9a3d-105">Create a WeChat application</span></span>

<span data-ttu-id="f9a3d-106">Чтобы использовать WeChat в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо сначала создать приложение WeChat и задать в нем правильные параметры.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-106">To use WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a WeChat application and supply it with the right parameters.</span></span> <span data-ttu-id="f9a3d-107">Для этого потребуется учетная запись WeChat.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-107">You need a WeChat account to do this.</span></span> <span data-ttu-id="f9a3d-108">Если у вас ее нет, эту учетную запись можно получить, зарегистрировавшись с помощью одного из мобильных приложений WeChat или своего номера QQ.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="f9a3d-109">После этого зарегистрируйте учетную запись в программе для разработчиков WeChat.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-109">After that, get your account registered with the WeChat developer program.</span></span> <span data-ttu-id="f9a3d-110">Дополнительные сведения см. [здесь](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span><span class="sxs-lookup"><span data-stu-id="f9a3d-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="f9a3d-111">Регистрация приложения WeChat</span><span class="sxs-lookup"><span data-stu-id="f9a3d-111">Register a WeChat application</span></span>

1. <span data-ttu-id="f9a3d-112">Перейдите на сайт [https://open.weixin.qq.com](https://open.weixin.qq.com/) и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-112">Go to [https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="f9a3d-113">Щелкните **管理中心** (Центр управления).</span><span class="sxs-lookup"><span data-stu-id="f9a3d-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="f9a3d-114">Выполните отображаемые инструкции, чтобы зарегистрировать новое приложение.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-114">Follow the necessary steps to register a new application.</span></span>
4. <span data-ttu-id="f9a3d-115">В поле **授权回调域** (URL-адрес обратного вызова) введите `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="f9a3d-116">Например, если используется `tenant_name` contoso.onmicrosoft.com, укажите URL-адрес `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="f9a3d-117">Найдите и скопируйте **идентификатор приложения** и **ключ приложения**.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-117">Find and copy the **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="f9a3d-118">Они вам потребуются позднее.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="f9a3d-119">Настройка WeChat в качестве поставщика удостоверений в клиенте</span><span class="sxs-lookup"><span data-stu-id="f9a3d-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="f9a3d-120">Выполните эти действия, чтобы [перейти к колонке функций B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-120">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="f9a3d-121">В колонке функций B2C щелкните **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-121">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="f9a3d-122">Нажмите **+Добавить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-122">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="f9a3d-123">Укажите понятное **имя** конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-123">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="f9a3d-124">Например, введите "WeChat".</span><span class="sxs-lookup"><span data-stu-id="f9a3d-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="f9a3d-125">Щелкните **Тип поставщика удостоверений**, выберите **WeChat** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="f9a3d-126">Щелкните **Настроить этот поставщик удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="f9a3d-127">Введите **ключ приложения**, скопированный ранее, в поле **Идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-127">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="f9a3d-128">Введите **секрет приложения**, скопированный ранее, в поле **Секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-128">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="f9a3d-129">Нажмите кнопку **ОК**, а затем — **Создать**, чтобы сохранить конфигурацию WeChat.</span><span class="sxs-lookup"><span data-stu-id="f9a3d-129">Click **OK** and then click **Create** to save your WeChat configuration.</span></span>

