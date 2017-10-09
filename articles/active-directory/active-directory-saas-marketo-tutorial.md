---
title: "Учебник. Интеграция Azure Active Directory с Marketo | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="680fe-103">Руководство. Интеграция Azure Active Directory с Marketo</span><span class="sxs-lookup"><span data-stu-id="680fe-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="680fe-104">В этом учебнике вы узнаете, как toointegrate Marketo с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="680fe-104">In this tutorial, you learn how toointegrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="680fe-105">Интеграция Marketo с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="680fe-105">Integrating Marketo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="680fe-106">Можно управлять в Azure AD, имеющего доступ tooMarketo</span><span class="sxs-lookup"><span data-stu-id="680fe-106">You can control in Azure AD who has access tooMarketo</span></span>
- <span data-ttu-id="680fe-107">Можно включить на пользователей tooautomatically get вошедшего tooMarketo (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="680fe-107">You can enable your users tooautomatically get signed-on tooMarketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="680fe-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="680fe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="680fe-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="680fe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="680fe-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="680fe-110">Prerequisites</span></span>

<span data-ttu-id="680fe-111">tooconfigure интеграция Azure AD с Marketo требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="680fe-111">tooconfigure Azure AD integration with Marketo, you need hello following items:</span></span>

- <span data-ttu-id="680fe-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="680fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="680fe-113">подписка Marketo с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="680fe-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="680fe-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="680fe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="680fe-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="680fe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="680fe-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="680fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="680fe-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="680fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="680fe-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="680fe-118">Scenario description</span></span>
<span data-ttu-id="680fe-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="680fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="680fe-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="680fe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="680fe-121">Добавление Marketo из галереи hello</span><span class="sxs-lookup"><span data-stu-id="680fe-121">Adding Marketo from hello gallery</span></span>
2. <span data-ttu-id="680fe-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="680fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-hello-gallery"></a><span data-ttu-id="680fe-123">Добавление Marketo из галереи hello</span><span class="sxs-lookup"><span data-stu-id="680fe-123">Adding Marketo from hello gallery</span></span>
<span data-ttu-id="680fe-124">tooconfigure hello интеграции Marketo в Azure AD, вы должны tooadd Marketo из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="680fe-124">tooconfigure hello integration of Marketo into Azure AD, you need tooadd Marketo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="680fe-125">**tooadd Marketo из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="680fe-125">**tooadd Marketo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="680fe-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="680fe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="680fe-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="680fe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="680fe-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="680fe-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="680fe-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="680fe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="680fe-133">Введите в поле поиска hello **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="680fe-133">In hello search box, type **Marketo**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="680fe-135">В панели результатов hello выберите **Marketo**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="680fe-135">In hello results panel, select **Marketo**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="680fe-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="680fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="680fe-138">В этом разделе описана настройка и проверка единого входа Azure AD в Marketo для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="680fe-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="680fe-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Marketo является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="680fe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Marketo is tooa user in Azure AD.</span></span> <span data-ttu-id="680fe-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Marketo должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="680fe-140">In other words, a link relationship between an Azure AD user and hello related user in Marketo needs toobe established.</span></span>

<span data-ttu-id="680fe-141">В Marketo, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="680fe-141">In Marketo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="680fe-142">tooconfigure и теста Azure AD единого входа с Marketo, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="680fe-142">tooconfigure and test Azure AD single sign-on with Marketo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="680fe-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="680fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="680fe-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="680fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="680fe-145">**[Создание тестового пользователя Marketo](#creating-a-marketo-test-user)**  -toohave аналог Саймон Britta в Marketo, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="680fe-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - toohave a counterpart of Britta Simon in Marketo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="680fe-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="680fe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="680fe-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="680fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="680fe-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="680fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="680fe-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Marketo.</span><span class="sxs-lookup"><span data-stu-id="680fe-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="680fe-150">**tooconfigure Azure AD единого входа с Marketo, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="680fe-150">**tooconfigure Azure AD single sign-on with Marketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="680fe-151">В hello в hello портала Azure **Marketo** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="680fe-151">In hello Azure portal, on hello **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="680fe-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="680fe-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="680fe-155">На hello **URL-адреса и домена Marketo** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="680fe-155">On hello **Marketo Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="680fe-157">а.</span><span class="sxs-lookup"><span data-stu-id="680fe-157">a.</span></span> <span data-ttu-id="680fe-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="680fe-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="680fe-159">b.</span><span class="sxs-lookup"><span data-stu-id="680fe-159">b.</span></span> <span data-ttu-id="680fe-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="680fe-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="680fe-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="680fe-161">These values are not real.</span></span> <span data-ttu-id="680fe-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="680fe-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="680fe-163">Обратитесь к [Marketo поддержки](http://investors.marketo.com/contactus.cfm) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="680fe-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) tooget these values.</span></span>
 
4. <span data-ttu-id="680fe-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="680fe-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="680fe-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="680fe-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="680fe-168">На hello **конфигурации Marketo** щелкните **Настройка Marketo** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="680fe-168">On hello **Marketo Configuration** section, click **Configure Marketo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="680fe-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="680fe-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="680fe-171">tooget Munchkin идентификатор приложения, войдите в tooMarketo, используя учетные данные администратора и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="680fe-171">tooget Munchkin Id of your application, log in tooMarketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="680fe-172">а.</span><span class="sxs-lookup"><span data-stu-id="680fe-172">a.</span></span> <span data-ttu-id="680fe-173">Войдите в приложение tooMarketo, используя учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="680fe-173">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="680fe-174">b.</span><span class="sxs-lookup"><span data-stu-id="680fe-174">b.</span></span> <span data-ttu-id="680fe-175">Нажмите кнопку hello **администратора** кнопку на верхней панели навигации панели hello.</span><span class="sxs-lookup"><span data-stu-id="680fe-175">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="680fe-177">c.</span><span class="sxs-lookup"><span data-stu-id="680fe-177">c.</span></span> <span data-ttu-id="680fe-178">Перейдите в меню toohello интеграции и нажмите кнопку hello **Munchkin ссылку**.</span><span class="sxs-lookup"><span data-stu-id="680fe-178">Navigate toohello Integration menu and click hello **Munchkin link**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="680fe-180">d.</span><span class="sxs-lookup"><span data-stu-id="680fe-180">d.</span></span> <span data-ttu-id="680fe-181">Скопируйте hello Munchkin код на экране приветствия и завершения URL-адрес ответа в мастер настройки hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="680fe-181">Copy hello Munchkin Id shown on hello screen and complete your Reply URL in hello Azure AD configuration wizard.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="680fe-183">hello tooconfigure единого входа в приложение hello выполните hello шаги, описанные ниже.</span><span class="sxs-lookup"><span data-stu-id="680fe-183">tooconfigure hello SSO in hello application, follow hello below steps:</span></span>
   
    <span data-ttu-id="680fe-184">а.</span><span class="sxs-lookup"><span data-stu-id="680fe-184">a.</span></span> <span data-ttu-id="680fe-185">Войдите в приложение tooMarketo, используя учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="680fe-185">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="680fe-186">b.</span><span class="sxs-lookup"><span data-stu-id="680fe-186">b.</span></span> <span data-ttu-id="680fe-187">Нажмите кнопку hello **администратора** кнопку на верхней панели навигации панели hello.</span><span class="sxs-lookup"><span data-stu-id="680fe-187">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="680fe-189">c.</span><span class="sxs-lookup"><span data-stu-id="680fe-189">c.</span></span> <span data-ttu-id="680fe-190">Перейдите в меню toohello интеграции и нажмите кнопку **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="680fe-190">Navigate toohello Integration menu and click **Single Sign On**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="680fe-192">d.</span><span class="sxs-lookup"><span data-stu-id="680fe-192">d.</span></span> <span data-ttu-id="680fe-193">Щелкните tooenable hello параметры SAML **изменить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="680fe-193">tooenable hello SAML Settings, click **Edit** button.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="680fe-195">д.</span><span class="sxs-lookup"><span data-stu-id="680fe-195">e.</span></span> <span data-ttu-id="680fe-196">**Включите** параметры единого входа.</span><span class="sxs-lookup"><span data-stu-id="680fe-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="680fe-197">f.</span><span class="sxs-lookup"><span data-stu-id="680fe-197">f.</span></span> <span data-ttu-id="680fe-198">Вставить hello **идентификатор сущности SAML**, в hello **ИД издателя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="680fe-198">Paste hello **SAML Entity ID**, in hello **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="680fe-199">ж.</span><span class="sxs-lookup"><span data-stu-id="680fe-199">g.</span></span> <span data-ttu-id="680fe-200">В hello **идентификатор сущности** текстовом поле введите URL-адрес hello как `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="680fe-200">In hello **Entity ID** textbox, enter hello URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="680fe-201">h.</span><span class="sxs-lookup"><span data-stu-id="680fe-201">h.</span></span> <span data-ttu-id="680fe-202">Выберите hello местоположение идентификатора пользователя как **элемент идентификатора имени**.</span><span class="sxs-lookup"><span data-stu-id="680fe-202">Select hello User ID Location as **Name Identifier element**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="680fe-204">Если ваш идентификатор пользователя не значение имени участника-пользователя, а затем значение hello изменения на вкладке атрибут hello.</span><span class="sxs-lookup"><span data-stu-id="680fe-204">If your User Identifier is not UPN value then change hello value in hello Attribute tab.</span></span>
   
    <span data-ttu-id="680fe-205">i.</span><span class="sxs-lookup"><span data-stu-id="680fe-205">i.</span></span> <span data-ttu-id="680fe-206">Отправьте сертификат hello, который вы скачали из мастера настройки Azure AD.</span><span class="sxs-lookup"><span data-stu-id="680fe-206">Upload hello certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="680fe-207">**Сохранить** hello параметры.</span><span class="sxs-lookup"><span data-stu-id="680fe-207">**Save** hello settings.</span></span>
   
    <span data-ttu-id="680fe-208">j.</span><span class="sxs-lookup"><span data-stu-id="680fe-208">j.</span></span> <span data-ttu-id="680fe-209">Изменение параметров перенаправления страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="680fe-209">Edit hello Redirect Pages settings.</span></span>
   
    <span data-ttu-id="680fe-210">k.</span><span class="sxs-lookup"><span data-stu-id="680fe-210">k.</span></span> <span data-ttu-id="680fe-211">Вставить hello **SAML единого входа URL-адрес службы** в hello **URL-адрес входа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="680fe-211">Paste hello **SAML Single Sign-On Service URL** in hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="680fe-212">l.</span><span class="sxs-lookup"><span data-stu-id="680fe-212">l.</span></span> <span data-ttu-id="680fe-213">Вставить hello **URL-адрес выхода** в hello **URL-адрес выхода** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="680fe-213">Paste hello **Sign-Out URL** in hello **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="680fe-214">m.</span><span class="sxs-lookup"><span data-stu-id="680fe-214">m.</span></span> <span data-ttu-id="680fe-215">В hello **URL-адрес ошибки**, копия вашего **URL-адрес экземпляра Marketo** и нажмите кнопку **Сохранить** кнопку toosave параметры.</span><span class="sxs-lookup"><span data-stu-id="680fe-215">In hello **Error URL**, copy your **Marketo instance URL** and click **Save** button toosave settings.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="680fe-217">tooenable hello единого входа для пользователей, завершения hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="680fe-217">tooenable hello SSO for users, complete hello following actions:</span></span>
   
    <span data-ttu-id="680fe-218">а.</span><span class="sxs-lookup"><span data-stu-id="680fe-218">a.</span></span> <span data-ttu-id="680fe-219">Войдите в приложение tooMarketo, используя учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="680fe-219">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="680fe-220">b.</span><span class="sxs-lookup"><span data-stu-id="680fe-220">b.</span></span> <span data-ttu-id="680fe-221">Нажмите кнопку hello **администратора** кнопку на верхней панели навигации панели hello.</span><span class="sxs-lookup"><span data-stu-id="680fe-221">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="680fe-223">c.</span><span class="sxs-lookup"><span data-stu-id="680fe-223">c.</span></span> <span data-ttu-id="680fe-224">Перейдите toohello **безопасности** меню и выберите пункт **параметры входа**.</span><span class="sxs-lookup"><span data-stu-id="680fe-224">Navigate toohello **Security** menu and click **Login Settings**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="680fe-226">d.</span><span class="sxs-lookup"><span data-stu-id="680fe-226">d.</span></span> <span data-ttu-id="680fe-227">Проверьте hello **единого входа требуется** параметр и **Сохранить** hello параметры.</span><span class="sxs-lookup"><span data-stu-id="680fe-227">Check hello **Require SSO** option and **Save** hello settings.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="680fe-229">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="680fe-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="680fe-230">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="680fe-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="680fe-231">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="680fe-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="680fe-232">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="680fe-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="680fe-233">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="680fe-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="680fe-235">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="680fe-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="680fe-236">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="680fe-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="680fe-238">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="680fe-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="680fe-240">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="680fe-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="680fe-242">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="680fe-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="680fe-244">а.</span><span class="sxs-lookup"><span data-stu-id="680fe-244">a.</span></span> <span data-ttu-id="680fe-245">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="680fe-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="680fe-246">b.</span><span class="sxs-lookup"><span data-stu-id="680fe-246">b.</span></span> <span data-ttu-id="680fe-247">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="680fe-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="680fe-248">c.</span><span class="sxs-lookup"><span data-stu-id="680fe-248">c.</span></span> <span data-ttu-id="680fe-249">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="680fe-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="680fe-250">d.</span><span class="sxs-lookup"><span data-stu-id="680fe-250">d.</span></span> <span data-ttu-id="680fe-251">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="680fe-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="680fe-252">Создание тестового пользователя Marketo</span><span class="sxs-lookup"><span data-stu-id="680fe-252">Creating a Marketo test user</span></span>

<span data-ttu-id="680fe-253">В этом разделе описано, как создать пользователя Britta Simon в приложении Marketo.</span><span class="sxs-lookup"><span data-stu-id="680fe-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="680fe-254">Выполните эти шаги toocreate пользователя на платформе Marketo.</span><span class="sxs-lookup"><span data-stu-id="680fe-254">follow these steps toocreate a user in Marketo platform.</span></span>

1. <span data-ttu-id="680fe-255">Войдите в приложение tooMarketo, используя учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="680fe-255">Log in tooMarketo app using admin credentials.</span></span>

2. <span data-ttu-id="680fe-256">Нажмите кнопку hello **администратора** кнопку на верхней панели навигации панели hello.</span><span class="sxs-lookup"><span data-stu-id="680fe-256">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="680fe-258">Перейдите toohello **безопасности** меню и выберите пункт **пользователей и ролей**</span><span class="sxs-lookup"><span data-stu-id="680fe-258">Navigate toohello **Security** menu and click **Users & Roles**</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="680fe-260">Нажмите кнопку hello **пригласить нового пользователя** ссылку на вкладку "пользователи" hello</span><span class="sxs-lookup"><span data-stu-id="680fe-260">Click hello **Invite New User** link on hello Users tab</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="680fe-262">В hello пригласить нового пользователя мастер заполнения hello следующую информацию</span><span class="sxs-lookup"><span data-stu-id="680fe-262">In hello Invite New User wizard fill hello following information</span></span>
   
    <span data-ttu-id="680fe-263">а.</span><span class="sxs-lookup"><span data-stu-id="680fe-263">a.</span></span> <span data-ttu-id="680fe-264">Введите пользователя hello **электронной почты** адрес в текстовом поле hello</span><span class="sxs-lookup"><span data-stu-id="680fe-264">Enter hello user **Email** address in hello textbox</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="680fe-266">b.</span><span class="sxs-lookup"><span data-stu-id="680fe-266">b.</span></span> <span data-ttu-id="680fe-267">Введите hello **имя** в текстовом поле hello</span><span class="sxs-lookup"><span data-stu-id="680fe-267">Enter hello **First Name** in hello textbox</span></span>
   
    <span data-ttu-id="680fe-268">c.</span><span class="sxs-lookup"><span data-stu-id="680fe-268">c.</span></span> <span data-ttu-id="680fe-269">Введите hello **Фамилия** в текстовом поле hello</span><span class="sxs-lookup"><span data-stu-id="680fe-269">Enter hello **Last Name**  in hello textbox</span></span>
   
    <span data-ttu-id="680fe-270">d.</span><span class="sxs-lookup"><span data-stu-id="680fe-270">d.</span></span> <span data-ttu-id="680fe-271">Щелкните **Далее**</span><span class="sxs-lookup"><span data-stu-id="680fe-271">Click **Next**</span></span>

6. <span data-ttu-id="680fe-272">В hello **разрешений** вкладке, выберите hello **userRoles** и нажмите кнопку **Далее**</span><span class="sxs-lookup"><span data-stu-id="680fe-272">In hello **Permissions** tab, select hello **userRoles** and click **Next**</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="680fe-274">Нажмите кнопку hello **отправки** кнопку toosend hello пользователю приглашение</span><span class="sxs-lookup"><span data-stu-id="680fe-274">Click hello **Send** button toosend hello user invitation</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="680fe-276">Пользователь получает уведомление по электронной почте hello и имеет hello tooclick ссылку и измените пароль tooactivate hello hello-учетной записи.</span><span class="sxs-lookup"><span data-stu-id="680fe-276">User receives hello email notification and has tooclick hello link and change hello password tooactivate hello account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="680fe-277">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="680fe-277">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="680fe-278">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooMarketo доступа.</span><span class="sxs-lookup"><span data-stu-id="680fe-278">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMarketo.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="680fe-280">**tooassign tooMarketo Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="680fe-280">**tooassign Britta Simon tooMarketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="680fe-281">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="680fe-281">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="680fe-283">В списке приложений hello выберите **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="680fe-283">In hello applications list, select **Marketo**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="680fe-285">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="680fe-285">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="680fe-287">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="680fe-287">Click **Add** button.</span></span> <span data-ttu-id="680fe-288">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="680fe-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="680fe-290">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="680fe-290">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="680fe-291">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="680fe-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="680fe-292">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="680fe-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="680fe-293">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="680fe-293">Testing single sign-on</span></span>

<span data-ttu-id="680fe-294">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="680fe-294">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="680fe-295">При нажатии кнопки hello Marketo плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Marketo приложения.</span><span class="sxs-lookup"><span data-stu-id="680fe-295">When you click hello Marketo tile in hello Access Panel, you should get automatically signed-on tooyour Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="680fe-296">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="680fe-296">Additional resources</span></span>

* [<span data-ttu-id="680fe-297">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="680fe-297">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="680fe-298">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="680fe-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

