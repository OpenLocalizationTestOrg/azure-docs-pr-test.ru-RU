---
title: "Учебник. Интеграция Azure Active Directory с Litmos | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="705fb-103">Руководство по интеграции Azure Active Directory с Litmos</span><span class="sxs-lookup"><span data-stu-id="705fb-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="705fb-104">В этом учебнике вы узнаете, как toointegrate Litmos с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="705fb-104">In this tutorial, you learn how toointegrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="705fb-105">Интеграция с Azure AD Litmos предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="705fb-105">Integrating Litmos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="705fb-106">Можно управлять в Azure AD, имеющего доступ tooLitmos.</span><span class="sxs-lookup"><span data-stu-id="705fb-106">You can control in Azure AD who has access tooLitmos.</span></span>
- <span data-ttu-id="705fb-107">Можно включить на пользователей tooautomatically get вошедшего tooLitmos (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="705fb-107">You can enable your users tooautomatically get signed-on tooLitmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="705fb-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="705fb-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="705fb-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="705fb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="705fb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="705fb-110">Prerequisites</span></span>

<span data-ttu-id="705fb-111">tooconfigure интеграция Azure AD с Litmos требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="705fb-111">tooconfigure Azure AD integration with Litmos, you need hello following items:</span></span>

- <span data-ttu-id="705fb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="705fb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="705fb-113">подписка Litmos с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="705fb-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="705fb-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="705fb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="705fb-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="705fb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="705fb-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="705fb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="705fb-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="705fb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="705fb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="705fb-118">Scenario description</span></span>
<span data-ttu-id="705fb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="705fb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="705fb-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="705fb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="705fb-121">Добавление Litmos из галереи hello</span><span class="sxs-lookup"><span data-stu-id="705fb-121">Adding Litmos from hello gallery</span></span>
2. <span data-ttu-id="705fb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="705fb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-hello-gallery"></a><span data-ttu-id="705fb-123">Добавление Litmos из галереи hello</span><span class="sxs-lookup"><span data-stu-id="705fb-123">Adding Litmos from hello gallery</span></span>
<span data-ttu-id="705fb-124">tooconfigure hello интеграции Litmos в Azure AD, вы должны tooadd Litmos из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="705fb-124">tooconfigure hello integration of Litmos into Azure AD, you need tooadd Litmos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="705fb-125">**tooadd Litmos из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="705fb-125">**tooadd Litmos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="705fb-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="705fb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="705fb-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="705fb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="705fb-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="705fb-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="705fb-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="705fb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="705fb-133">Введите в поле поиска hello **Litmos**выберите **Litmos** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="705fb-133">In hello search box, type **Litmos**, select **Litmos** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Litmos в списке результатов hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="705fb-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="705fb-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="705fb-136">В этом разделе описана настройка и проверка единого входа Azure AD в Litmos с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="705fb-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="705fb-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Litmos является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="705fb-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Litmos is tooa user in Azure AD.</span></span> <span data-ttu-id="705fb-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Litmos должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="705fb-138">In other words, a link relationship between an Azure AD user and hello related user in Litmos needs toobe established.</span></span>

<span data-ttu-id="705fb-139">В Litmos, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="705fb-139">In Litmos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="705fb-140">tooconfigure и теста Azure AD единого входа с Litmos, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="705fb-140">tooconfigure and test Azure AD single sign-on with Litmos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="705fb-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="705fb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="705fb-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="705fb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="705fb-143">**[Создание тестового пользователя Litmos](#create-a-litmos-test-user)**  -toohave аналог Саймон Britta в Litmos, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="705fb-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - toohave a counterpart of Britta Simon in Litmos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="705fb-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="705fb-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="705fb-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="705fb-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="705fb-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="705fb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="705fb-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Litmos.</span><span class="sxs-lookup"><span data-stu-id="705fb-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="705fb-148">**tooconfigure Azure AD единого входа с Litmos, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="705fb-148">**tooconfigure Azure AD single sign-on with Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="705fb-149">В hello в hello портала Azure **Litmos** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="705fb-149">In hello Azure portal, on hello **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="705fb-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="705fb-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="705fb-153">На hello **URL-адреса и домена Litmos** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="705fb-153">On hello **Litmos Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="705fb-155">а.</span><span class="sxs-lookup"><span data-stu-id="705fb-155">a.</span></span> <span data-ttu-id="705fb-156">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="705fb-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="705fb-157">b.</span><span class="sxs-lookup"><span data-stu-id="705fb-157">b.</span></span> <span data-ttu-id="705fb-158">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="705fb-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="705fb-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="705fb-159">These values are not real.</span></span> <span data-ttu-id="705fb-160">Обновить эти значения hello фактический идентификатор и ответ по URL-адресу, которые рассматриваются далее в учебнике или контакт [Litmos поддержки](https://www.litmos.com/contact-us/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="705fb-160">Update these values with hello actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="705fb-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="705fb-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="705fb-163">В составе конфигурации hello требуется toocustomize hello **атрибутов токена SAML** Litmos приложения.</span><span class="sxs-lookup"><span data-stu-id="705fb-163">As part of hello configuration, you need toocustomize hello **SAML Token Attributes** for your Litmos application.</span></span>

    ![Раздел "Атрибут"](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="705fb-165">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="705fb-165">Attribute Name</span></span>   | <span data-ttu-id="705fb-166">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="705fb-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="705fb-167">FirstName</span><span class="sxs-lookup"><span data-stu-id="705fb-167">FirstName</span></span> |<span data-ttu-id="705fb-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="705fb-168">user.givenname</span></span> |
    | <span data-ttu-id="705fb-169">LastName</span><span class="sxs-lookup"><span data-stu-id="705fb-169">LastName</span></span>  |<span data-ttu-id="705fb-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="705fb-170">user.surname</span></span> |
    | <span data-ttu-id="705fb-171">Email</span><span class="sxs-lookup"><span data-stu-id="705fb-171">Email</span></span> |<span data-ttu-id="705fb-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="705fb-172">user.mail</span></span> |

    <span data-ttu-id="705fb-173">а.</span><span class="sxs-lookup"><span data-stu-id="705fb-173">a.</span></span> <span data-ttu-id="705fb-174">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="705fb-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Добавление атрибута](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Диалоговое окно "Добавление атрибута"](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="705fb-177">b.</span><span class="sxs-lookup"><span data-stu-id="705fb-177">b.</span></span> <span data-ttu-id="705fb-178">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="705fb-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="705fb-179">c.</span><span class="sxs-lookup"><span data-stu-id="705fb-179">c.</span></span> <span data-ttu-id="705fb-180">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="705fb-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="705fb-181">d.</span><span class="sxs-lookup"><span data-stu-id="705fb-181">d.</span></span> <span data-ttu-id="705fb-182">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="705fb-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="705fb-183">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="705fb-183">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="705fb-185">В другом окне браузера, сайт компании Litmos tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="705fb-185">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

8. <span data-ttu-id="705fb-186">Hello hello левой панели навигации щелкните **учетные записи**.</span><span class="sxs-lookup"><span data-stu-id="705fb-186">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Раздел "Accounts" (Учетные записи) на стороне приложения][22] 

9. <span data-ttu-id="705fb-188">Нажмите кнопку hello **интеграции** вкладки.</span><span class="sxs-lookup"><span data-stu-id="705fb-188">Click hello **Integrations** tab.</span></span>
   
    ![Вкладка "Integrations" (Интеграция)][23] 

10. <span data-ttu-id="705fb-190">На hello **интеграции** Перейдите вниз слишком**интеграции сторонних производителей**, а затем нажмите кнопку **SAML 2.0** вкладку.</span><span class="sxs-lookup"><span data-stu-id="705fb-190">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![Раздел "SAML 2.0"][24] 

11. <span data-ttu-id="705fb-192">Скопируйте значение hello в **hello конечная точка SAML для litmos:** и вставьте его в hello **URL-адрес ответа** текстовое поле в hello **URL-адреса и домена Litmos** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="705fb-192">Copy hello value under **hello SAML endpoint for litmos is:** and paste it into hello **Reply URL** textbox in hello **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![Конечная точка SAML][26] 

12. <span data-ttu-id="705fb-194">В вашей **Litmos** приложения, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="705fb-194">In your **Litmos** application, perform hello following steps:</span></span>
    
     ![Приложение Litmos][25] 
     
     <span data-ttu-id="705fb-196">а.</span><span class="sxs-lookup"><span data-stu-id="705fb-196">a.</span></span> <span data-ttu-id="705fb-197">Выберите команду **Enable SAML**(Включить SAML).</span><span class="sxs-lookup"><span data-stu-id="705fb-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="705fb-198">b.</span><span class="sxs-lookup"><span data-stu-id="705fb-198">b.</span></span> <span data-ttu-id="705fb-199">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509 SAML** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="705fb-199">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="705fb-200">c.</span><span class="sxs-lookup"><span data-stu-id="705fb-200">c.</span></span> <span data-ttu-id="705fb-201">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="705fb-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="705fb-202">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="705fb-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="705fb-203">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="705fb-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="705fb-204">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="705fb-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="705fb-205">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="705fb-205">Create an Azure AD test user</span></span>

<span data-ttu-id="705fb-206">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="705fb-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="705fb-208">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="705fb-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="705fb-209">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="705fb-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="705fb-211">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="705fb-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="705fb-213">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="705fb-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="705fb-215">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="705fb-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="705fb-217">а.</span><span class="sxs-lookup"><span data-stu-id="705fb-217">a.</span></span> <span data-ttu-id="705fb-218">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="705fb-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="705fb-219">b.</span><span class="sxs-lookup"><span data-stu-id="705fb-219">b.</span></span> <span data-ttu-id="705fb-220">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="705fb-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="705fb-221">c.</span><span class="sxs-lookup"><span data-stu-id="705fb-221">c.</span></span> <span data-ttu-id="705fb-222">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="705fb-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="705fb-223">d.</span><span class="sxs-lookup"><span data-stu-id="705fb-223">d.</span></span> <span data-ttu-id="705fb-224">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="705fb-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="705fb-225">Создание тестового пользователя Litmos</span><span class="sxs-lookup"><span data-stu-id="705fb-225">Create a Litmos test user</span></span>

<span data-ttu-id="705fb-226">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Litmos.</span><span class="sxs-lookup"><span data-stu-id="705fb-226">hello objective of this section is toocreate a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="705fb-227">Hello Litmos приложений поддерживает только времени подготовки.</span><span class="sxs-lookup"><span data-stu-id="705fb-227">hello Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="705fb-228">Это означает учетной записи пользователя автоматически создается при необходимости во время попытки tooaccess hello приложения с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="705fb-228">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

<span data-ttu-id="705fb-229">**toocreate пользователя с именем Саймон Britta в Litmos, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="705fb-229">**toocreate a user called Britta Simon in Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="705fb-230">В другом окне браузера, сайт компании Litmos tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="705fb-230">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

2. <span data-ttu-id="705fb-231">Hello hello левой панели навигации щелкните **учетные записи**.</span><span class="sxs-lookup"><span data-stu-id="705fb-231">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Раздел "Accounts" (Учетные записи) на стороне приложения][22] 

3. <span data-ttu-id="705fb-233">Нажмите кнопку hello **интеграции** вкладки.</span><span class="sxs-lookup"><span data-stu-id="705fb-233">Click hello **Integrations** tab.</span></span>
   
    ![Вкладка "Integrations" (Интеграция)][23] 

4. <span data-ttu-id="705fb-235">На hello **интеграции** Перейдите вниз слишком**интеграции сторонних производителей**, а затем нажмите кнопку **SAML 2.0** вкладку.</span><span class="sxs-lookup"><span data-stu-id="705fb-235">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="705fb-237">Установите флажок **Autogenerate Users** (Автоматически создавать пользователей).</span><span class="sxs-lookup"><span data-stu-id="705fb-237">Select **Autogenerate Users**</span></span>
   
    ![Автоматическое создание пользователей][27] 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="705fb-239">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="705fb-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="705fb-240">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLitmos доступа.</span><span class="sxs-lookup"><span data-stu-id="705fb-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLitmos.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="705fb-242">**tooassign tooLitmos Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="705fb-242">**tooassign Britta Simon tooLitmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="705fb-243">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="705fb-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="705fb-245">В списке приложений hello выберите **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="705fb-245">In hello applications list, select **Litmos**.</span></span>

    ![ссылка Litmos Hello в списке приложений hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="705fb-247">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="705fb-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="705fb-249">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="705fb-249">Click **Add** button.</span></span> <span data-ttu-id="705fb-250">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="705fb-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="705fb-252">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="705fb-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="705fb-253">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="705fb-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="705fb-254">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="705fb-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="705fb-255">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="705fb-255">Test single sign-on</span></span>

<span data-ttu-id="705fb-256">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="705fb-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="705fb-257">При нажатии кнопки Litmos плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Litmos приложения.</span><span class="sxs-lookup"><span data-stu-id="705fb-257">When you click hello Litmos tile in hello Access Panel, you should get automatically signed-on tooyour Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="705fb-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="705fb-258">Additional resources</span></span>

* [<span data-ttu-id="705fb-259">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="705fb-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="705fb-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="705fb-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

