---
title: "Azure Active Directory B2C: настройка LinkedIn | Документация Майкрософт"
description: "Регистрация и вход пользователей с помощью учетных записей LinkedIn в приложениях, защищенных с помощью Azure Active Directory B2C"
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
ms.openlocfilehash: 1a6c4b19261aa34e668554ccad2b6340cddf9bf5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-linkedin-accounts"></a><span data-ttu-id="08085-103">Azure Active Directory B2C: регистрация и вход пользователей с помощью учетных записей LinkedIn</span><span class="sxs-lookup"><span data-stu-id="08085-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="08085-104">Создание приложения LinkedIn</span><span class="sxs-lookup"><span data-stu-id="08085-104">Create a LinkedIn application</span></span>
<span data-ttu-id="08085-105">Чтобы использовать LinkedIn в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо создать приложение LinkedIn и задать в нем правильные параметры.</span><span class="sxs-lookup"><span data-stu-id="08085-105">To use LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a LinkedIn application and supply it with the right parameters.</span></span> <span data-ttu-id="08085-106">Для этого потребуется учетная запись LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="08085-106">You need a LinkedIn account to do this.</span></span> <span data-ttu-id="08085-107">Если у вас ее нет, вы можете получить такую учетную запись на сайте [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="08085-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="08085-108">Посетите [сайт разработчиков LinkedIn](https://www.developer.linkedin.com/) и войдите с помощью своих учетных данных LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="08085-108">Go to the [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="08085-109">Щелкните **Мои приложения** в верхней строке меню и нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="08085-109">Click **My Apps** in the top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn — создание приложения](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="08085-111">В форме **Создание нового приложения** укажите соответствующие сведения (**Название компании**, **Имя**, **Описание**, **URL-адрес логотипа приложения**, **Применение приложения**, **URL-адрес веб-сайта**, **Адрес электронной почты компании** и **Рабочий телефон**).</span><span class="sxs-lookup"><span data-stu-id="08085-111">In the **Create a New Application** form, fill in the relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="08085-112">Примите **условия использования LinkedIn API** и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="08085-112">Agree to the **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn — регистрация приложения](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="08085-114">Скопируйте значения **Идентификатор клиента** и **Секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="08085-114">Copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="08085-115">Их можно найти в разделе **Ключи аутентификации**. Оба значения необходимы для настройки LinkedIn в качестве поставщика удостоверений для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="08085-115">(You can find them under **Authentication Keys**.) You will need both of them to configure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="08085-116">**Секрет клиента** — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="08085-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="08085-117">Введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в поле **Разрешённые URL-адреса перенаправления** (в разделе **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="08085-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="08085-118">Замените **{tenant}** именем своего клиента (например, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="08085-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="08085-119">Нажмите кнопку **Добавить**, затем нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="08085-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="08085-120">В значении **{клиент}** необходимо учитывать регистр.</span><span class="sxs-lookup"><span data-stu-id="08085-120">The **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn — настройка приложения](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="08085-122">Настройка LinkedIn в качестве поставщика удостоверений для клиента</span><span class="sxs-lookup"><span data-stu-id="08085-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="08085-123">Выполните следующие действия, чтобы [перейти к колонке функций B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="08085-123">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="08085-124">В колонке функций B2C щелкните **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="08085-124">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="08085-125">Нажмите **+Добавить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="08085-125">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="08085-126">Укажите понятное **имя** конфигурации поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="08085-126">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="08085-127">Например, введите "LI".</span><span class="sxs-lookup"><span data-stu-id="08085-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="08085-128">Нажмите **Тип поставщика удостоверений**, выберите **LinkedIn** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="08085-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="08085-129">Нажмите **Настроить этот поставщик удостоверений** и введите идентификатор клиента и секрет клиента ранее созданного приложения LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="08085-129">Click **Set up this identity provider** and enter the client ID and client secret of the LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="08085-130">Нажмите кнопку **ОК**, а затем — **Создать**, чтобы сохранить конфигурацию LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="08085-130">Click **OK** and then click **Create** to save your LinkedIn configuration.</span></span>

