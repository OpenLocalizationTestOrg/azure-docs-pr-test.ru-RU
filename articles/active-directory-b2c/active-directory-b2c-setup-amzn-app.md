---
title: "Azure Active Directory B2C: настройка Amazon | Документация Майкрософт"
description: "Укажите tooconsumers регистрации и входе в систему с учетными записями Amazon в приложениях, которые защищены с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a><span data-ttu-id="4e61e-103">Azure Active Directory B2C: Укажите tooconsumers регистрации и входе в систему с учетными записями Amazon</span><span class="sxs-lookup"><span data-stu-id="4e61e-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="4e61e-104">Создание приложения Amazon</span><span class="sxs-lookup"><span data-stu-id="4e61e-104">Create an Amazon application</span></span>
<span data-ttu-id="4e61e-105">toouse Amazon как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения Amazon и передайте в него hello нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="4e61e-105">toouse Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an Amazon application and supply it with hello right parameters.</span></span> <span data-ttu-id="4e61e-106">Требуется toodo учетной записи Amazon.</span><span class="sxs-lookup"><span data-stu-id="4e61e-106">You need an Amazon account toodo this.</span></span> <span data-ttu-id="4e61e-107">Если у вас ее нет, зарегистрируйте ее на сайте [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="4e61e-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="4e61e-108">Go toohello [Центр разработчиков Amazon](https://login.amazon.com/) и выполните вход с учетными данными Amazon.</span><span class="sxs-lookup"><span data-stu-id="4e61e-108">Go toohello [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="4e61e-109">Если вы еще не сделано, нажмите кнопку **зарегистрироваться**, выполните действия по регистрации разработчика hello и примите политику hello.</span><span class="sxs-lookup"><span data-stu-id="4e61e-109">If you have not already done so, click **Sign Up**, follow hello developer registration steps, and accept hello policy.</span></span>
3. <span data-ttu-id="4e61e-110">Нажмите кнопку **Register new application**(Зарегистрировать новое приложение).</span><span class="sxs-lookup"><span data-stu-id="4e61e-110">Click **Register new application**.</span></span>
   
    ![Регистрация нового приложения на веб-сайте Amazon hello](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="4e61e-112">Укажите информацию о приложении (**имя**, **описание** и **URL-адрес для уведомления о конфиденциальности**) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4e61e-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Предоставление информации для регистрации нового приложения на сайте Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="4e61e-114">В hello **веб-параметров** статьи значения hello копирования **идентификатор клиента** и **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="4e61e-114">In hello **Web Settings** section, copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="4e61e-115">(Требуется tooclick hello **Показать секрет** кнопку toosee это.) Нужны оба из них tooconfigure Amazon как поставщик удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="4e61e-115">(You need tooclick hello **Show Secret** button toosee this.) You need both of them tooconfigure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="4e61e-116">Нажмите кнопку **изменить** hello нижней части раздела hello.</span><span class="sxs-lookup"><span data-stu-id="4e61e-116">Click **Edit** at hello bottom of hello section.</span></span> <span data-ttu-id="4e61e-117">**Секрет клиента** — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="4e61e-117">**Client Secret** is an important security credential.</span></span>
   
    ![Предоставление идентификатора клиента и секрета клиента для нового приложения на сайте Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="4e61e-119">Введите `https://login.microsoftonline.com` в hello **допускается JavaScript Origins** поля и `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **URL-адреса возврата допускается** поля.</span><span class="sxs-lookup"><span data-stu-id="4e61e-119">Enter `https://login.microsoftonline.com` in hello **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Allowed Return URLs** field.</span></span> <span data-ttu-id="4e61e-120">Замените **{tenant}** именем своего клиента (например, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4e61e-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="4e61e-121">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4e61e-121">Click **Save**.</span></span> <span data-ttu-id="4e61e-122">Hello **{tenant}** значение учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="4e61e-122">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![Предоставление источников JavaScript и URL-адресов возврата для нового приложения на сайте Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="4e61e-124">Настройка Amazon в качестве поставщика удостоверений для клиента</span><span class="sxs-lookup"><span data-stu-id="4e61e-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="4e61e-125">Выполните следующие действия слишком[перейдите в колонку функции toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4e61e-125">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="4e61e-126">В колонке функции hello B2C, нажмите кнопку **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="4e61e-126">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="4e61e-127">Нажмите кнопку **+ добавить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="4e61e-127">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="4e61e-128">Укажите понятное **имя** hello конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4e61e-128">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="4e61e-129">Например, введите Amzn.</span><span class="sxs-lookup"><span data-stu-id="4e61e-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="4e61e-130">Щелкните **Тип поставщика удостоверений**, выберите **Amazon** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4e61e-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="4e61e-131">Нажмите кнопку **настройки этого поставщика удостоверений** и введите hello клиента идентификатор и секрет клиента из hello Amazon приложения, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="4e61e-131">Click **Set up this identity provider** and enter hello client ID and client secret of hello Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="4e61e-132">Нажмите кнопку **ОК** и нажмите кнопку **создать** toosave конфигурацию Amazon.</span><span class="sxs-lookup"><span data-stu-id="4e61e-132">Click **OK** and then click **Create** toosave your Amazon configuration.</span></span>

