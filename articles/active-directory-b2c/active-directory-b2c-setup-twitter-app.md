---
title: "Azure Active Directory B2C: настройка Twitter | Документы Майкрософт"
description: "Обеспечение регистрации и входа для пользователей с учетными записями Twitter в приложениях, защищенных с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 82a001dd53cdddcf3b360090f3250af593c96fbb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-twitter-accounts"></a><span data-ttu-id="c40b1-103">Azure Active Directory B2C: организация регистрации и входа для потребителей с учетными записями Twitter</span><span class="sxs-lookup"><span data-stu-id="c40b1-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="c40b1-104">Эта функция предоставляется в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="c40b1-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="c40b1-105">Создание приложения Twitter</span><span class="sxs-lookup"><span data-stu-id="c40b1-105">Create a Twitter application</span></span>
<span data-ttu-id="c40b1-106">Чтобы использовать Twitter в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, нужно сначала создать приложение Twitter и задать в нем правильные параметры.</span><span class="sxs-lookup"><span data-stu-id="c40b1-106">To use Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Twitter application and supply it with the right parameters.</span></span> <span data-ttu-id="c40b1-107">Для этого потребуется учетная запись разработчика Twitter.</span><span class="sxs-lookup"><span data-stu-id="c40b1-107">You need a Twitter developer account to do this.</span></span> <span data-ttu-id="c40b1-108">Если у вас ее нет, вы можете создать такую учетную запись на сайте [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="c40b1-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="c40b1-109">Перейдите на [веб-сайт разработчиков Twitter](https://dev.twitter.com/) и войдите с помощью своих учетных данных.</span><span class="sxs-lookup"><span data-stu-id="c40b1-109">Go to the [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="c40b1-110">Щелкните **My apps** (Мои приложения) в разделе **Tools & Support** (Средства и поддержка), а затем выберите **Create New App** (Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="c40b1-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="c40b1-111">В форме укажите значения для полей **Name** (Имя), **Description** (Описание) и **Website** (Веб-сайт).</span><span class="sxs-lookup"><span data-stu-id="c40b1-111">In the form, provide a value for the **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="c40b1-112">В поле **Callback URL** (URL-адрес обратного вызова) введите значение `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="c40b1-112">For the **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="c40b1-113">Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="c40b1-113">Make sure to replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="c40b1-114">Установите флажок, чтобы принять **соглашение с разработчиком** и нажмите кнопку **Create your Twitter application** (Создать приложение Twitter).</span><span class="sxs-lookup"><span data-stu-id="c40b1-114">Check the box to agree to the **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="c40b1-115">После создания приложения щелкните **Keys and Access Tokens** (Ключи и токены доступа).</span><span class="sxs-lookup"><span data-stu-id="c40b1-115">Once the app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="c40b1-116">Скопируйте значения **Consumer Key** (Ключ потребителя) и **Consumer Secret** (Секрет потребителя).</span><span class="sxs-lookup"><span data-stu-id="c40b1-116">Copy the value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="c40b1-117">Оба значения необходимы для настройки Twitter в качестве поставщика удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="c40b1-117">You will need both of them to configure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="c40b1-118">Настройка Twitter в качестве поставщика удостоверений в клиенте</span><span class="sxs-lookup"><span data-stu-id="c40b1-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="c40b1-119">Выполните эти действия, чтобы [перейти к колонке функций B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c40b1-119">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="c40b1-120">В колонке функций B2C щелкните **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="c40b1-120">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="c40b1-121">Нажмите **+Добавить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="c40b1-121">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="c40b1-122">Укажите понятное **имя** конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c40b1-122">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="c40b1-123">Например, введите Twitter.</span><span class="sxs-lookup"><span data-stu-id="c40b1-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="c40b1-124">Щелкните **Тип поставщика удостоверений**, выберите **Twitter** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c40b1-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="c40b1-125">Щелкните **Настроить этот поставщик удостоверений** и введите **ключ потребителя** в поле **Идентификатор клиента** и **секрет потребителя** Twitter в поле **Секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="c40b1-125">Click **Set up this identity provider** and enter the Twitter **Consumer Key** for the **Client id** and the Twitter **Consumer Secret** for the **Client secret**.</span></span>
7. <span data-ttu-id="c40b1-126">Нажмите кнопку **ОК**, а затем — **Создать**, чтобы сохранить конфигурацию Twitter.</span><span class="sxs-lookup"><span data-stu-id="c40b1-126">Click **OK**, and then click **Create** to save your Twitter configuration.</span></span>

