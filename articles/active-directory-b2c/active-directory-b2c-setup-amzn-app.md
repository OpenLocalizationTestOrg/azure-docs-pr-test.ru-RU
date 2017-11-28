---
title: "Azure Active Directory B2C: настройка Amazon | Документация Майкрософт"
description: "Обеспечение регистрации и входа для пользователей с учетными записями Amazon в приложениях, защищенных с помощью Azure Active Directory B2C."
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
ms.openlocfilehash: dcc97e1b7f6287bd7692c52bf068950065a26572
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-amazon-accounts"></a><span data-ttu-id="b6c8b-103">Azure Active Directory B2C: регистрация и вход пользователей с учетными записями Amazon</span><span class="sxs-lookup"><span data-stu-id="b6c8b-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="b6c8b-104">Создание приложения Amazon</span><span class="sxs-lookup"><span data-stu-id="b6c8b-104">Create an Amazon application</span></span>
<span data-ttu-id="b6c8b-105">Чтобы использовать Amazon в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо сначала создать приложение Amazon и задать в нем правильные параметры.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-105">To use Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an Amazon application and supply it with the right parameters.</span></span> <span data-ttu-id="b6c8b-106">Для этого потребуется учетная запись Amazon.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-106">You need an Amazon account to do this.</span></span> <span data-ttu-id="b6c8b-107">Если у вас ее нет, зарегистрируйте ее на сайте [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="b6c8b-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="b6c8b-108">Перейдите на сайт [Amazon Developer Center](https://login.amazon.com/) войдите с помощью учетной записи Amazon.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-108">Go to the [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="b6c8b-109">Если это еще не сделано, нажмите кнопку **Sign Up**(Регистрация), выполните действия для регистрации разработчика и примите условия политики.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-109">If you have not already done so, click **Sign Up**, follow the developer registration steps, and accept the policy.</span></span>
3. <span data-ttu-id="b6c8b-110">Нажмите кнопку **Register new application**(Зарегистрировать новое приложение).</span><span class="sxs-lookup"><span data-stu-id="b6c8b-110">Click **Register new application**.</span></span>
   
    ![Регистрация нового приложения на веб-сайте Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="b6c8b-112">Укажите информацию о приложении (**имя**, **описание** и **URL-адрес для уведомления о конфиденциальности**) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Предоставление информации для регистрации нового приложения на сайте Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="b6c8b-114">В разделе **Веб-параметры** скопируйте значения **Идентификатор клиента** и **Секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-114">In the **Web Settings** section, copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="b6c8b-115">Для отображения этих параметров необходимо нажать кнопку **Показать секрет**. Оба значения необходимы для настройки Amazon в качестве поставщика удостоверений для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-115">(You need to click the **Show Secret** button to see this.) You need both of them to configure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="b6c8b-116">Щелкните **Изменить** в нижней части раздела.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-116">Click **Edit** at the bottom of the section.</span></span> <span data-ttu-id="b6c8b-117">**Секрет клиента** — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-117">**Client Secret** is an important security credential.</span></span>
   
    ![Предоставление идентификатора клиента и секрета клиента для нового приложения на сайте Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="b6c8b-119">Введите `https://login.microsoftonline.com` в поле **Разрешенные источники JavaScript** и `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` — в поле **Разрешенные URL-адреса возврата**.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-119">Enter `https://login.microsoftonline.com` in the **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Allowed Return URLs** field.</span></span> <span data-ttu-id="b6c8b-120">Замените **{tenant}** именем своего клиента (например, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="b6c8b-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="b6c8b-121">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-121">Click **Save**.</span></span> <span data-ttu-id="b6c8b-122">В значении **{клиент}** необходимо учитывать регистр.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-122">The **{tenant}** value is case-sensitive.</span></span>
   
    ![Предоставление источников JavaScript и URL-адресов возврата для нового приложения на сайте Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="b6c8b-124">Настройка Amazon в качестве поставщика удостоверений для клиента</span><span class="sxs-lookup"><span data-stu-id="b6c8b-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="b6c8b-125">Выполните эти действия, чтобы [перейти к колонке функций B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-125">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="b6c8b-126">В колонке функций B2C щелкните **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-126">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="b6c8b-127">Нажмите **+Добавить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-127">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="b6c8b-128">Укажите понятное **имя** конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-128">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="b6c8b-129">Например, введите Amzn.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="b6c8b-130">Щелкните **Тип поставщика удостоверений**, выберите **Amazon** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="b6c8b-131">Щелкните **Set up this identity provider** (Настроить этот поставщик удостоверений), а затем введите идентификатор и секрет клиента ранее созданного приложения Amazon.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-131">Click **Set up this identity provider** and enter the client ID and client secret of the Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="b6c8b-132">Нажмите кнопку **ОК**, а затем — **Создать**, чтобы сохранить конфигурацию Amazon.</span><span class="sxs-lookup"><span data-stu-id="b6c8b-132">Click **OK** and then click **Create** to save your Amazon configuration.</span></span>

