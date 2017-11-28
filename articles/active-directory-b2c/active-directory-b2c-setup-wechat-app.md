---
title: "Azure Active Directory B2C: настройка WeChat | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями WeChat в приложениях, которые защищены с помощью Azure Active Directory B2C."
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
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a><span data-ttu-id="c98c6-103">Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями WeChat</span><span class="sxs-lookup"><span data-stu-id="c98c6-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="c98c6-104">Эта функция предоставляется в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="c98c6-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="c98c6-105">Создание приложения WeChat</span><span class="sxs-lookup"><span data-stu-id="c98c6-105">Create a WeChat application</span></span>

<span data-ttu-id="c98c6-106">toouse WeChat как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения WeChat и передайте в него hello нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="c98c6-106">toouse WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a WeChat application and supply it with hello right parameters.</span></span> <span data-ttu-id="c98c6-107">Требуется toodo WeChat учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c98c6-107">You need a WeChat account toodo this.</span></span> <span data-ttu-id="c98c6-108">Если у вас ее нет, эту учетную запись можно получить, зарегистрировавшись с помощью одного из мобильных приложений WeChat или своего номера QQ.</span><span class="sxs-lookup"><span data-stu-id="c98c6-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="c98c6-109">После этого получите учетную запись hello WeChat разработчиков программ.</span><span class="sxs-lookup"><span data-stu-id="c98c6-109">After that, get your account registered with hello WeChat developer program.</span></span> <span data-ttu-id="c98c6-110">Дополнительные сведения см. [здесь](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span><span class="sxs-lookup"><span data-stu-id="c98c6-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="c98c6-111">Регистрация приложения WeChat</span><span class="sxs-lookup"><span data-stu-id="c98c6-111">Register a WeChat application</span></span>

1. <span data-ttu-id="c98c6-112">Go слишком[https://open.weixin.qq.com/](https://open.weixin.qq.com/) и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="c98c6-112">Go too[https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="c98c6-113">Щелкните **管理中心** (Центр управления).</span><span class="sxs-lookup"><span data-stu-id="c98c6-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="c98c6-114">Выполните необходимые действия hello tooregister нового приложения.</span><span class="sxs-lookup"><span data-stu-id="c98c6-114">Follow hello necessary steps tooregister a new application.</span></span>
4. <span data-ttu-id="c98c6-115">В поле **授权回调域** (URL-адрес обратного вызова) введите `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="c98c6-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="c98c6-116">Например если ваш `tenant_name` — contoso.onmicrosoft.com toobe URL-адрес набора hello `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="c98c6-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="c98c6-117">Поиск и копирование hello **идентификатор приложения** и **ключ приложения**.</span><span class="sxs-lookup"><span data-stu-id="c98c6-117">Find and copy hello **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="c98c6-118">Они вам потребуются позднее.</span><span class="sxs-lookup"><span data-stu-id="c98c6-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="c98c6-119">Настройка WeChat в качестве поставщика удостоверений в клиенте</span><span class="sxs-lookup"><span data-stu-id="c98c6-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="c98c6-120">Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c98c6-120">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="c98c6-121">В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="c98c6-121">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="c98c6-122">Нажмите кнопку **+ добавить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="c98c6-122">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="c98c6-123">Укажите понятное **имя** hello конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c98c6-123">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="c98c6-124">Например, введите "WeChat".</span><span class="sxs-lookup"><span data-stu-id="c98c6-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="c98c6-125">Щелкните **Тип поставщика удостоверений**, выберите **WeChat** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c98c6-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="c98c6-126">Щелкните **Настроить этот поставщик удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="c98c6-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="c98c6-127">Введите hello **ключ приложения** , скопированное ранее как hello **идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="c98c6-127">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="c98c6-128">Введите hello **секрет приложения** , скопированное ранее как hello **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="c98c6-128">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="c98c6-129">Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave WeChat конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c98c6-129">Click **OK** and then click **Create** toosave your WeChat configuration.</span></span>

