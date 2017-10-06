---
title: "Руководство по интеграции Azure Active Directory с Veracode | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="8a3dd-103">Руководство. Интеграция Azure Active Directory с Veracode</span><span class="sxs-lookup"><span data-stu-id="8a3dd-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="8a3dd-104">В этом учебнике вы узнаете, как toointegrate Veracode с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a3dd-104">In this tutorial, you learn how toointegrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a3dd-105">Интеграция с Azure AD Veracode предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8a3dd-105">Integrating Veracode with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8a3dd-106">Можно управлять в Azure AD, имеющего доступ tooVeracode.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-106">You can control in Azure AD who has access tooVeracode.</span></span>
- <span data-ttu-id="8a3dd-107">Можно включить на пользователей tooautomatically get вошедшего tooVeracode (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-107">You can enable your users tooautomatically get signed-on tooVeracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8a3dd-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="8a3dd-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a3dd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a3dd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8a3dd-110">Prerequisites</span></span>

<span data-ttu-id="8a3dd-111">tooconfigure интеграция Azure AD с Veracode требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8a3dd-111">tooconfigure Azure AD integration with Veracode, you need hello following items:</span></span>

- <span data-ttu-id="8a3dd-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8a3dd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a3dd-113">Подписка Veracode с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a3dd-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a3dd-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8a3dd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a3dd-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a3dd-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a3dd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a3dd-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8a3dd-118">Scenario description</span></span>
<span data-ttu-id="8a3dd-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a3dd-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8a3dd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a3dd-121">Добавление Veracode из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="8a3dd-121">Add Veracode from hello gallery</span></span>
2. <span data-ttu-id="8a3dd-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a3dd-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-hello-gallery"></a><span data-ttu-id="8a3dd-123">Добавление Veracode из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="8a3dd-123">Add Veracode from hello gallery</span></span>
<span data-ttu-id="8a3dd-124">tooconfigure hello интеграции Veracode в Azure AD, вы должны tooadd Veracode из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-124">tooconfigure hello integration of Veracode into Azure AD, you need tooadd Veracode from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8a3dd-125">**tooadd Veracode из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-125">**tooadd Veracode from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a3dd-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="8a3dd-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8a3dd-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="8a3dd-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="8a3dd-133">Введите в поле поиска hello **Veracode**выберите **Veracode** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-133">In hello search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Veracode в списке результатов hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8a3dd-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a3dd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8a3dd-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Veracode с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a3dd-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Veracode является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veracode is tooa user in Azure AD.</span></span> <span data-ttu-id="8a3dd-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Veracode должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-138">In other words, a link relationship between an Azure AD user and hello related user in Veracode needs toobe established.</span></span>

<span data-ttu-id="8a3dd-139">В Veracode, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-139">In Veracode, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8a3dd-140">tooconfigure и теста Azure AD единого входа с Veracode, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8a3dd-140">tooconfigure and test Azure AD single sign-on with Veracode, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8a3dd-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8a3dd-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a3dd-143">**[Создание тестового пользователя Veracode](#create-a-veracode-test-user)**  -toohave аналог Саймон Britta в Veracode, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - toohave a counterpart of Britta Simon in Veracode that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a3dd-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a3dd-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8a3dd-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a3dd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8a3dd-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Veracode.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="8a3dd-148">**Azure AD tooconfigure единого входа с Veracode, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-148">**tooconfigure Azure AD single sign-on with Veracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a3dd-149">В hello в hello портала Azure **Veracode** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-149">In hello Azure portal, on hello **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="8a3dd-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="8a3dd-153">На hello **URL-адреса и домена Veracode** раздела, пользователь не имеет tooperform все меры как приложение hello уже заранее интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-153">On hello **Veracode Domain and URLs** section, the user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="8a3dd-155">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-155">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="8a3dd-157">Цель этого раздела Hello — toooutline как tooVeracode tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-157">hello objective of this section is toooutline how tooenable users tooauthenticate tooVeracode with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="8a3dd-158">Приложение Veracode ожидает утверждения SAML hello в определенном формате, требующий tooadd настраиваемого атрибута сопоставления tooyour **атрибутов токена saml** конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-158">Your Veracode application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> <span data-ttu-id="8a3dd-159">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-159">hello following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="8a3dd-160">![Атрибуты](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="8a3dd-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="8a3dd-161">сопоставления атрибутов hello необходимые tooadd, выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-161">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="8a3dd-162">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="8a3dd-162">Attribute Name</span></span> | <span data-ttu-id="8a3dd-163">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="8a3dd-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="8a3dd-164">firstname</span><span class="sxs-lookup"><span data-stu-id="8a3dd-164">firstname</span></span> |<span data-ttu-id="8a3dd-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="8a3dd-165">User.givenname</span></span> |
    | <span data-ttu-id="8a3dd-166">lastname</span><span class="sxs-lookup"><span data-stu-id="8a3dd-166">lastname</span></span> |<span data-ttu-id="8a3dd-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="8a3dd-167">User.surname</span></span> |
    | <span data-ttu-id="8a3dd-168">email</span><span class="sxs-lookup"><span data-stu-id="8a3dd-168">email</span></span> |<span data-ttu-id="8a3dd-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="8a3dd-169">User.mail</span></span> |
    
    <span data-ttu-id="8a3dd-170">а.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-170">a.</span></span> <span data-ttu-id="8a3dd-171">Для каждой строки данных в таблице hello выше, щелкните **добавить атрибут пользователя**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-171">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="8a3dd-172">![Атрибуты](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="8a3dd-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="8a3dd-173">![Атрибуты](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="8a3dd-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="8a3dd-174">b.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-174">b.</span></span> <span data-ttu-id="8a3dd-175">В hello **имя атрибута** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-175">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8a3dd-176">c.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-176">c.</span></span> <span data-ttu-id="8a3dd-177">В hello **значение атрибута** текстовое поле, значение атрибута выберите hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-177">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8a3dd-178">d.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-178">d.</span></span> <span data-ttu-id="8a3dd-179">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-179">Click **Ok**.</span></span>

7. <span data-ttu-id="8a3dd-180">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8a3dd-180">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8a3dd-182">На hello **конфигурации Veracode** щелкните **Настройка Veracode** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-182">On hello **Veracode Configuration** section, click **Configure Veracode** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8a3dd-183">Копировать hello **идентификатор сущности SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-183">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Конфигурация Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="8a3dd-185">В другом окне веб-браузера войдите на веб-сайт Veracode вашей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="8a3dd-186">В меню в верхней части hello hello выберите **параметры**и нажмите кнопку **администратора**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-186">In hello menu on hello top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="8a3dd-187">![Администрирование](./media/active-directory-saas-veracode-tutorial/ic802911.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="8a3dd-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="8a3dd-188">Нажмите кнопку hello **SAML** вкладки.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-188">Click hello **SAML** tab.</span></span>

12. <span data-ttu-id="8a3dd-189">В hello **параметры SAML организации** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8a3dd-189">In hello **Organization SAML Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8a3dd-190">![Администрирование](./media/active-directory-saas-veracode-tutorial/ic802912.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="8a3dd-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="8a3dd-191">а.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-191">a.</span></span>  <span data-ttu-id="8a3dd-192">В **издателя** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-192">In  **Issuer** textbox, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="8a3dd-193">b.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-193">b.</span></span> <span data-ttu-id="8a3dd-194">щелкните загруженный сертификат из портала Azure tooupload **выбрать файл**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-194">tooupload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="8a3dd-195">c.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-195">c.</span></span> <span data-ttu-id="8a3dd-196">Выберите параметр **Включить саморегистрацию**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="8a3dd-197">В hello **параметры регистрации Self** статьи, выполните следующие шаги hello и нажмите кнопку **Сохранить**:</span><span class="sxs-lookup"><span data-stu-id="8a3dd-197">In hello **Self Registration Settings** section, perform hello following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="8a3dd-198">![Администрирование](./media/active-directory-saas-veracode-tutorial/ic802913.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="8a3dd-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="8a3dd-199">а.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-199">a.</span></span> <span data-ttu-id="8a3dd-200">Для параметра **New User Activation** (Активация нового пользователя) выберите значение **No Activation Required** (Активация не требуется).</span><span class="sxs-lookup"><span data-stu-id="8a3dd-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="8a3dd-201">b.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-201">b.</span></span> <span data-ttu-id="8a3dd-202">Для параметра **User Data Updates** (Обновления пользовательских данных) выберите значение **Preference Veracode User Data** (Предпочтение пользовательских данных Veracode).</span><span class="sxs-lookup"><span data-stu-id="8a3dd-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="8a3dd-203">c.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-203">c.</span></span> <span data-ttu-id="8a3dd-204">Для **сведений об атрибутах SAML**, выберите hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8a3dd-204">For **SAML Attribute Details**, select hello following:</span></span>
      * <span data-ttu-id="8a3dd-205">**роли пользователей;**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-205">**User Roles**</span></span>
      * <span data-ttu-id="8a3dd-206">**администратор политики;**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="8a3dd-207">**рецензент;**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-207">**Reviewer**</span></span>
      * <span data-ttu-id="8a3dd-208">**руководитель безопасности;**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-208">**Security Lead**</span></span>
      * <span data-ttu-id="8a3dd-209">**руководитель;**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-209">**Executive**</span></span>
      * <span data-ttu-id="8a3dd-210">**отправитель;**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-210">**Submitter**</span></span>
      * <span data-ttu-id="8a3dd-211">**создатель;**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-211">**Creator**</span></span>
      * <span data-ttu-id="8a3dd-212">**все типы проверки;**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-212">**All Scan Types**</span></span>
      * <span data-ttu-id="8a3dd-213">**участие в группе;**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-213">**Team Memberships**</span></span>
      * <span data-ttu-id="8a3dd-214">**группа по умолчанию.**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="8a3dd-215">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="8a3dd-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8a3dd-216">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8a3dd-217">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a3dd-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8a3dd-218">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a3dd-218">Create an Azure AD test user</span></span>

<span data-ttu-id="8a3dd-219">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="8a3dd-221">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a3dd-222">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-222">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8a3dd-224">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-224">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8a3dd-226">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-226">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8a3dd-228">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8a3dd-228">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8a3dd-230">а.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-230">a.</span></span> <span data-ttu-id="8a3dd-231">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-231">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a3dd-232">b.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-232">b.</span></span> <span data-ttu-id="8a3dd-233">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-233">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="8a3dd-234">c.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-234">c.</span></span> <span data-ttu-id="8a3dd-235">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-235">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="8a3dd-236">d.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-236">d.</span></span> <span data-ttu-id="8a3dd-237">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="8a3dd-238">Создание тестового пользователя Veracode</span><span class="sxs-lookup"><span data-stu-id="8a3dd-238">Create a Veracode test user</span></span>
<span data-ttu-id="8a3dd-239">В порядке tooenable toolog пользователей Azure AD в Veracode их необходимо подготовить в Veracode.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-239">In order tooenable Azure AD users toolog into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="8a3dd-240">В случае Veracode hello Подготовка — это автоматизированная задача.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-240">In hello case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="8a3dd-241">С вашей стороны никакие действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-241">There is no action item for you.</span></span> <span data-ttu-id="8a3dd-242">Пользователи создаются автоматически при необходимости hello первой единого входа попытки.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-242">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="8a3dd-243">Можно использовать любые другие Veracode пользователя средства создания учетных записей или интерфейсы API, предоставляемые Veracode tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-243">You can use any other Veracode user account creation tools or APIs provided by Veracode tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8a3dd-244">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8a3dd-244">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8a3dd-245">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooVeracode доступа.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeracode.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="8a3dd-247">**tooassign tooVeracode Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8a3dd-247">**tooassign Britta Simon tooVeracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a3dd-248">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8a3dd-250">В списке приложений hello выберите **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-250">In hello applications list, select **Veracode**.</span></span>

    ![ссылка Veracode Hello в списке приложений hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="8a3dd-252">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="8a3dd-254">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-254">Click **Add** button.</span></span> <span data-ttu-id="8a3dd-255">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="8a3dd-257">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8a3dd-258">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a3dd-259">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8a3dd-260">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8a3dd-260">Test single sign-on</span></span>

<span data-ttu-id="8a3dd-261">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8a3dd-262">При нажатии кнопки hello Veracode плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Veracode приложения.</span><span class="sxs-lookup"><span data-stu-id="8a3dd-262">When you click hello Veracode tile in hello Access Panel, you should get automatically signed-on tooyour Veracode application.</span></span>
<span data-ttu-id="8a3dd-263">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8a3dd-263">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8a3dd-264">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8a3dd-264">Additional resources</span></span>

* [<span data-ttu-id="8a3dd-265">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a3dd-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a3dd-266">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8a3dd-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

