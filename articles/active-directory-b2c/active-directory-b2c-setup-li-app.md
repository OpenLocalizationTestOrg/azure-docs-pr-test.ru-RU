---
title: "Azure Active Directory B2C: настройка LinkedIn | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями LinkedIn в приложениях, которые защищены с помощью Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a><span data-ttu-id="4ec06-103">Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями LinkedIn</span><span class="sxs-lookup"><span data-stu-id="4ec06-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="4ec06-104">Создание приложения LinkedIn</span><span class="sxs-lookup"><span data-stu-id="4ec06-104">Create a LinkedIn application</span></span>
<span data-ttu-id="4ec06-105">toouse LinkedIn как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения LinkedIn и передайте в него hello нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="4ec06-105">toouse LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a LinkedIn application and supply it with hello right parameters.</span></span> <span data-ttu-id="4ec06-106">Требуется toodo LinkedIn учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4ec06-106">You need a LinkedIn account toodo this.</span></span> <span data-ttu-id="4ec06-107">Если у вас ее нет, вы можете получить такую учетную запись на сайте [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="4ec06-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="4ec06-108">Go toohello [веб-сайт разработчиков LinkedIn](https://www.developer.linkedin.com/) и выполните вход с учетными данными LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="4ec06-108">Go toohello [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="4ec06-109">Нажмите кнопку **Мои приложения** в hello верхней строке меню, а затем нажмите кнопку **Создание приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ec06-109">Click **My Apps** in hello top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn — создание приложения](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="4ec06-111">В hello **создайте новое приложение** форме, заполните необходимые сведения hello (**название компании**, **имя**, **описание**, **URL-адрес для приложения логотип**, **приложения используйте**, **URL-адрес веб-сайта**, **рабочей электронной почты** и **рабочий телефон**).</span><span class="sxs-lookup"><span data-stu-id="4ec06-111">In hello **Create a New Application** form, fill in hello relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="4ec06-112">Согласовать toohello **условия использования API LinkedIn** и нажмите кнопку **отправить**.</span><span class="sxs-lookup"><span data-stu-id="4ec06-112">Agree toohello **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn — регистрация приложения](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="4ec06-114">Скопируйте значения hello **идентификатор клиента** и **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="4ec06-114">Copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="4ec06-115">Их можно найти в разделе **Ключи аутентификации**. Вам потребуется обеих функций tooconfigure LinkedIn как поставщик удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="4ec06-115">(You can find them under **Authentication Keys**.) You will need both of them tooconfigure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4ec06-116">**Секрет клиента** — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="4ec06-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="4ec06-117">Введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **URL-адреса перенаправления авторизованных** поле (под **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="4ec06-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="4ec06-118">Замените **{tenant}** именем своего клиента (например, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4ec06-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="4ec06-119">Нажмите кнопку **Добавить**, затем нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="4ec06-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="4ec06-120">Hello **{tenant}** значение учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="4ec06-120">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn — настройка приложения](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="4ec06-122">Настройка LinkedIn в качестве поставщика удостоверений для клиента</span><span class="sxs-lookup"><span data-stu-id="4ec06-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="4ec06-123">Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec06-123">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="4ec06-124">В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="4ec06-124">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="4ec06-125">Нажмите кнопку **+ добавить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="4ec06-125">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="4ec06-126">Укажите понятное **имя** hello конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4ec06-126">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="4ec06-127">Например, введите "LI".</span><span class="sxs-lookup"><span data-stu-id="4ec06-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="4ec06-128">Нажмите **Тип поставщика удостоверений**, выберите **LinkedIn** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4ec06-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="4ec06-129">Нажмите кнопку **настройки этого поставщика удостоверений** и введите hello клиента идентификатор и секрет клиента из hello LinkedIn приложения, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="4ec06-129">Click **Set up this identity provider** and enter hello client ID and client secret of hello LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="4ec06-130">Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave конфигурацию LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="4ec06-130">Click **OK** and then click **Create** toosave your LinkedIn configuration.</span></span>

