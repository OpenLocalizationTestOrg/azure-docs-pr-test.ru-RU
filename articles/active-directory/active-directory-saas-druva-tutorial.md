---
title: "Руководство по интеграции Azure Active Directory с Druva | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="b3af2-103">Руководство по интеграции Azure Active Directory с Druva</span><span class="sxs-lookup"><span data-stu-id="b3af2-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="b3af2-104">В этом учебнике вы узнаете, как toointegrate Druva с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b3af2-104">In this tutorial, you learn how toointegrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3af2-105">Интеграция Druva с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b3af2-105">Integrating Druva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b3af2-106">Можно управлять в Azure AD, имеющего доступ tooDruva.</span><span class="sxs-lookup"><span data-stu-id="b3af2-106">You can control in Azure AD who has access tooDruva.</span></span>
- <span data-ttu-id="b3af2-107">Можно включить на пользователей tooautomatically get вошедшего tooDruva (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3af2-107">You can enable your users tooautomatically get signed-on tooDruva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b3af2-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b3af2-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b3af2-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b3af2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3af2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b3af2-110">Prerequisites</span></span>

<span data-ttu-id="b3af2-111">tooconfigure интеграция Azure AD с Druva требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b3af2-111">tooconfigure Azure AD integration with Druva, you need hello following items:</span></span>

- <span data-ttu-id="b3af2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b3af2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3af2-113">Подписка с поддержкой единого входа Druva</span><span class="sxs-lookup"><span data-stu-id="b3af2-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3af2-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b3af2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3af2-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b3af2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3af2-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b3af2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3af2-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3af2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3af2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b3af2-118">Scenario description</span></span>
<span data-ttu-id="b3af2-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b3af2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3af2-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b3af2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3af2-121">Добавление Druva из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b3af2-121">Adding Druva from hello gallery</span></span>
2. <span data-ttu-id="b3af2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3af2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-hello-gallery"></a><span data-ttu-id="b3af2-123">Добавление Druva из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b3af2-123">Adding Druva from hello gallery</span></span>
<span data-ttu-id="b3af2-124">tooconfigure hello интеграции Druva в Azure AD, вы должны tooadd Druva из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b3af2-124">tooconfigure hello integration of Druva into Azure AD, you need tooadd Druva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b3af2-125">**tooadd Druva из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b3af2-125">**tooadd Druva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3af2-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b3af2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="b3af2-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b3af2-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="b3af2-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b3af2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="b3af2-133">Введите в поле поиска hello **Druva**выберите **Druva** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b3af2-133">In hello search box, type **Druva**, select **Druva** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Druva в списке результатов hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b3af2-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3af2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b3af2-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Druva с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b3af2-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b3af2-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Druva является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3af2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Druva is tooa user in Azure AD.</span></span> <span data-ttu-id="b3af2-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Druva должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b3af2-138">In other words, a link relationship between an Azure AD user and hello related user in Druva needs toobe established.</span></span>

<span data-ttu-id="b3af2-139">В Druva, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="b3af2-139">In Druva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b3af2-140">tooconfigure и теста Azure AD единого входа с Druva, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b3af2-140">tooconfigure and test Azure AD single sign-on with Druva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b3af2-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b3af2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b3af2-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b3af2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3af2-143">**[Создание тестового пользователя Druva](#create-a-druva-test-user)**  -toohave аналог Саймон Britta в Druva, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b3af2-143">**[Create a Druva test user](#create-a-druva-test-user)** - toohave a counterpart of Britta Simon in Druva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3af2-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b3af2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3af2-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b3af2-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b3af2-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3af2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b3af2-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в свое приложение Druva.</span><span class="sxs-lookup"><span data-stu-id="b3af2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="b3af2-148">**tooconfigure Azure AD единого входа с Druva, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b3af2-148">**tooconfigure Azure AD single sign-on with Druva, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3af2-149">В hello в hello портала Azure **Druva** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-149">In hello Azure portal, on hello **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="b3af2-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b3af2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="b3af2-153">На hello **URL-адреса и домена Druva** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b3af2-153">On hello **Druva Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="b3af2-155">В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="b3af2-155">In hello **Sign-on URL** textbox, type hello URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="b3af2-156">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b3af2-156">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="b3af2-158">Приложение Druva ожидает утверждения SAML hello в определенном формате, поэтому требует сопоставления tooyour tooadd настраиваемого атрибута **атрибутов токена SAML** конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b3af2-158">Your Druva application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="b3af2-160">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна настройки атрибутов токена SAML, как показано в hello предшествующий образ и выполнить следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b3af2-160">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="b3af2-161">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="b3af2-161">Attribute Name</span></span>      | <span data-ttu-id="b3af2-162">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="b3af2-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="b3af2-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="b3af2-163">insync\_auth\_token</span></span> |<span data-ttu-id="b3af2-164">Введите значение маркера созданный hello</span><span class="sxs-lookup"><span data-stu-id="b3af2-164">Enter hello token generated value</span></span> |
    
    <span data-ttu-id="b3af2-165">а.</span><span class="sxs-lookup"><span data-stu-id="b3af2-165">a.</span></span> <span data-ttu-id="b3af2-166">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b3af2-166">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b3af2-169">b.</span><span class="sxs-lookup"><span data-stu-id="b3af2-169">b.</span></span> <span data-ttu-id="b3af2-170">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="b3af2-170">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="b3af2-171">c.</span><span class="sxs-lookup"><span data-stu-id="b3af2-171">c.</span></span> <span data-ttu-id="b3af2-172">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="b3af2-172">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="b3af2-173">значение маркера созданный Hello описан далее в учебнике.</span><span class="sxs-lookup"><span data-stu-id="b3af2-173">hello token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="b3af2-174">d.</span><span class="sxs-lookup"><span data-stu-id="b3af2-174">d.</span></span> <span data-ttu-id="b3af2-175">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="b3af2-176">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b3af2-176">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b3af2-178">На hello **конфигурации Druva** щелкните **Настройка Druva** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="b3af2-178">On hello **Druva Configuration** section, click **Configure Druva** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b3af2-179">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="b3af2-179">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="b3af2-181">В другом окне браузера Войдите на сайте компании Druva tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="b3af2-181">In a different web browser window, log in tooyour Druva company site as an administrator.</span></span>

10. <span data-ttu-id="b3af2-182">Go слишком**управление \> параметры**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-182">Go too**Manage \> Settings**.</span></span>

    <span data-ttu-id="b3af2-183">![Параметры](./media/active-directory-saas-druva-tutorial/ic795091.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="b3af2-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="b3af2-184">В диалоговом окне приветствия параметры единого входа выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="b3af2-184">On hello Single Sign-On Settings dialog, perform hello following steps:</span></span>

    <span data-ttu-id="b3af2-185">![Параметры единого входа](./media/active-directory-saas-druva-tutorial/ic795092.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="b3af2-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="b3af2-186">а.</span><span class="sxs-lookup"><span data-stu-id="b3af2-186">a.</span></span> <span data-ttu-id="b3af2-187">Вставить **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **URL-адрес входа поставщика Идентификаторов** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b3af2-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="b3af2-188">b.</span><span class="sxs-lookup"><span data-stu-id="b3af2-188">b.</span></span> <span data-ttu-id="b3af2-189">Вставить **URL-адрес выхода** значение, которое было скопировано из hello портал Azure в hello **URL-адрес выхода поставщика Идентификаторов** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b3af2-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="b3af2-190">c.</span><span class="sxs-lookup"><span data-stu-id="b3af2-190">c.</span></span> <span data-ttu-id="b3af2-191">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат поставщика Идентификаторов** текстового поля</span><span class="sxs-lookup"><span data-stu-id="b3af2-191">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="b3af2-192">d.</span><span class="sxs-lookup"><span data-stu-id="b3af2-192">d.</span></span> <span data-ttu-id="b3af2-193">tooopen hello **параметры** щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-193">tooopen hello **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="b3af2-194">На hello **параметры** щелкните **создать токен единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-194">On hello **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="b3af2-195">![Параметры](./media/active-directory-saas-druva-tutorial/ic795093.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="b3af2-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="b3af2-196">На hello **единого входа для проверки подлинности маркера** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b3af2-196">On hello **Single Sign-on Authentication Token** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="b3af2-197">![Маркер единого входа](./media/active-directory-saas-druva-tutorial/ic795094.png "Маркер единого входа")</span><span class="sxs-lookup"><span data-stu-id="b3af2-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="b3af2-198">а.</span><span class="sxs-lookup"><span data-stu-id="b3af2-198">a.</span></span> <span data-ttu-id="b3af2-199">Нажмите кнопку **копирования**, Вставка скопированного значения в hello **значение** текстовое поле в hello **Добавление атрибута** раздела.</span><span class="sxs-lookup"><span data-stu-id="b3af2-199">Click **Copy**, Paste copied value in hello **Value** textbox in hello **Add Attribute** section.</span></span>
    
    <span data-ttu-id="b3af2-200">b.</span><span class="sxs-lookup"><span data-stu-id="b3af2-200">b.</span></span> <span data-ttu-id="b3af2-201">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="b3af2-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="b3af2-202">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b3af2-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b3af2-203">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b3af2-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b3af2-204">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3af2-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b3af2-205">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3af2-205">Create an Azure AD test user</span></span>

<span data-ttu-id="b3af2-206">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b3af2-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="b3af2-208">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b3af2-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3af2-209">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b3af2-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b3af2-211">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b3af2-213">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b3af2-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b3af2-215">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b3af2-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b3af2-217">а.</span><span class="sxs-lookup"><span data-stu-id="b3af2-217">a.</span></span> <span data-ttu-id="b3af2-218">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3af2-219">b.</span><span class="sxs-lookup"><span data-stu-id="b3af2-219">b.</span></span> <span data-ttu-id="b3af2-220">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b3af2-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b3af2-221">c.</span><span class="sxs-lookup"><span data-stu-id="b3af2-221">c.</span></span> <span data-ttu-id="b3af2-222">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="b3af2-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b3af2-223">d.</span><span class="sxs-lookup"><span data-stu-id="b3af2-223">d.</span></span> <span data-ttu-id="b3af2-224">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="b3af2-225">Создание тестового пользователя Druva</span><span class="sxs-lookup"><span data-stu-id="b3af2-225">Create a Druva test user</span></span>

<span data-ttu-id="b3af2-226">В порядке tooenable toolog пользователей Azure AD в tooDruva их необходимо подготовить в Druva.</span><span class="sxs-lookup"><span data-stu-id="b3af2-226">In order tooenable Azure AD users toolog in tooDruva, they must be provisioned into Druva.</span></span> <span data-ttu-id="b3af2-227">В случае hello объекта Druva Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="b3af2-227">In hello case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="b3af2-228">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b3af2-228">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3af2-229">Войдите в tooyour **Druva** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="b3af2-229">Log in tooyour **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="b3af2-230">Go слишком**управление \> пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-230">Go too**Manage \> Users**.</span></span>
   
   <span data-ttu-id="b3af2-231">![Управление пользователями](./media/active-directory-saas-druva-tutorial/ic795097.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="b3af2-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="b3af2-232">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="b3af2-233">![Управление пользователями](./media/active-directory-saas-druva-tutorial/ic795098.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="b3af2-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="b3af2-234">В диалоговом окне Создать нового пользователя hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b3af2-234">On hello Create New User dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="b3af2-235">![Создание пользователя](./media/active-directory-saas-druva-tutorial/ic795099.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="b3af2-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="b3af2-236">а.</span><span class="sxs-lookup"><span data-stu-id="b3af2-236">a.</span></span> <span data-ttu-id="b3af2-237">В hello **адрес электронной почты** текстовом поле введите адрес электронной почты hello пользователя как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="b3af2-237">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="b3af2-238">b.</span><span class="sxs-lookup"><span data-stu-id="b3af2-238">b.</span></span> <span data-ttu-id="b3af2-239">В hello **имя** текстовом поле введите имя пользователя, такие как hello **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-239">In hello **Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="b3af2-240">c.</span><span class="sxs-lookup"><span data-stu-id="b3af2-240">c.</span></span> <span data-ttu-id="b3af2-241">Нажмите кнопку **Создать пользователя**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="b3af2-242">Можно использовать любые другие Druva пользователя средства создания учетных записей или интерфейсы API, предоставляемые Druva tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3af2-242">You can use any other Druva user account creation tools or APIs provided by Druva tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b3af2-243">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b3af2-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b3af2-244">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooDruva доступа.</span><span class="sxs-lookup"><span data-stu-id="b3af2-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDruva.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="b3af2-246">**tooassign tooDruva Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b3af2-246">**tooassign Britta Simon tooDruva, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3af2-247">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b3af2-249">В списке приложений hello выберите **Druva**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-249">In hello applications list, select **Druva**.</span></span>

    ![ссылка Druva Hello в списке приложений hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="b3af2-251">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="b3af2-253">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-253">Click **Add** button.</span></span> <span data-ttu-id="b3af2-254">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="b3af2-256">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b3af2-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b3af2-257">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3af2-258">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b3af2-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b3af2-259">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b3af2-259">Test single sign-on</span></span>

<span data-ttu-id="b3af2-260">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b3af2-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b3af2-261">При нажатии кнопки hello Druva плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour Druva.</span><span class="sxs-lookup"><span data-stu-id="b3af2-261">When you click hello Druva tile in hello Access Panel, you should get automatically signed-on tooyour Druva application.</span></span>
<span data-ttu-id="b3af2-262">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b3af2-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b3af2-263">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b3af2-263">Additional resources</span></span>

* [<span data-ttu-id="b3af2-264">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3af2-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3af2-265">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b3af2-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

