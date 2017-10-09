---
title: "Azure Active Directory B2C: настройка Twitter | Документы Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями Twitter в приложениях, которые защищены с помощью Azure Active Directory B2C."
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
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a><span data-ttu-id="8a90b-103">Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Twitter</span><span class="sxs-lookup"><span data-stu-id="8a90b-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="8a90b-104">Эта функция предоставляется в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="8a90b-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="8a90b-105">Создание приложения Twitter</span><span class="sxs-lookup"><span data-stu-id="8a90b-105">Create a Twitter application</span></span>
<span data-ttu-id="8a90b-106">toouse Twitter как поставщик удостоверений в Azure Active Directory (Azure AD) B2C, требуется toocreate приложения Twitter и передайте в него hello нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="8a90b-106">toouse Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Twitter application and supply it with hello right parameters.</span></span> <span data-ttu-id="8a90b-107">Требуется toodo учетной записи разработчика Twitter.</span><span class="sxs-lookup"><span data-stu-id="8a90b-107">You need a Twitter developer account toodo this.</span></span> <span data-ttu-id="8a90b-108">Если у вас ее нет, вы можете создать такую учетную запись на сайте [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="8a90b-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="8a90b-109">Go toohello [Twitter веб-сайта разработчика](https://dev.twitter.com/) и выполните вход с помощью учетных данных.</span><span class="sxs-lookup"><span data-stu-id="8a90b-109">Go toohello [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="8a90b-110">Щелкните **My apps** (Мои приложения) в разделе **Tools & Support** (Средства и поддержка), а затем выберите **Create New App** (Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="8a90b-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="8a90b-111">В форме hello, укажите значение для hello **имя**, **описание**, и **веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="8a90b-111">In hello form, provide a value for hello **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="8a90b-112">Для hello **URL-адрес обратного вызова**, введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="8a90b-112">For hello **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="8a90b-113">Убедитесь, что tooreplace **{tenant}** с именем вашего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="8a90b-113">Make sure tooreplace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="8a90b-114">Проверьте hello поле tooagree toohello **соглашение разработчика** и нажмите кнопку **создания приложения Twitter**.</span><span class="sxs-lookup"><span data-stu-id="8a90b-114">Check hello box tooagree toohello **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="8a90b-115">После создания приложения hello щелкните **ключей и маркеры доступа**.</span><span class="sxs-lookup"><span data-stu-id="8a90b-115">Once hello app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="8a90b-116">Скопируйте значение hello **ключ потребителя** и **секрет пользователя**.</span><span class="sxs-lookup"><span data-stu-id="8a90b-116">Copy hello value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="8a90b-117">Вам потребуется обеих функций tooconfigure Twitter в качестве поставщика удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="8a90b-117">You will need both of them tooconfigure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="8a90b-118">Настройка Twitter в качестве поставщика удостоверений в клиенте</span><span class="sxs-lookup"><span data-stu-id="8a90b-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="8a90b-119">Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8a90b-119">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="8a90b-120">В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="8a90b-120">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="8a90b-121">Нажмите кнопку **+ добавить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="8a90b-121">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="8a90b-122">Укажите понятное **имя** hello конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="8a90b-122">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="8a90b-123">Например, введите Twitter.</span><span class="sxs-lookup"><span data-stu-id="8a90b-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="8a90b-124">Щелкните **Тип поставщика удостоверений**, выберите **Twitter** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8a90b-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="8a90b-125">Нажмите кнопку **настройки этого поставщика удостоверений** и введите hello Twitter **ключ потребителя** для hello **идентификатор клиента** и hello Twitter **секрет пользователя**для hello **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="8a90b-125">Click **Set up this identity provider** and enter hello Twitter **Consumer Key** for hello **Client id** and hello Twitter **Consumer Secret** for hello **Client secret**.</span></span>
7. <span data-ttu-id="8a90b-126">Нажмите кнопку **ОК**, а затем нажмите кнопку **создать** toosave конфигурацию Twitter.</span><span class="sxs-lookup"><span data-stu-id="8a90b-126">Click **OK**, and then click **Create** toosave your Twitter configuration.</span></span>

