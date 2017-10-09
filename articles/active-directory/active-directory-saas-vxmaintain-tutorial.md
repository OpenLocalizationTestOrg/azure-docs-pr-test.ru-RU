---
title: "Руководство по интеграции Azure Active Directory с vxMaintain | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="0ce0a-103">Руководство по интеграции Azure Active Directory с vxMaintain</span><span class="sxs-lookup"><span data-stu-id="0ce0a-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="0ce0a-104">В этом учебнике вы узнаете, как vxMaintain toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ce0a-104">In this tutorial, you learn how toointegrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ce0a-105">Такая интеграция обеспечивает несколько важных преимуществ.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-105">This integration provides several important benefits.</span></span> <span data-ttu-id="0ce0a-106">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="0ce0a-106">You can:</span></span>

- <span data-ttu-id="0ce0a-107">Элемент управления в Azure AD, имеющего доступ к toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-107">Control in Azure AD who has access toovxMaintain.</span></span>
- <span data-ttu-id="0ce0a-108">Включите tooautomatically пользователей при входе в toovxMaintain с единого входа (SSO) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-108">Enable your users tooautomatically sign in toovxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="0ce0a-109">Управление учетными записями в одном централизованном месте: hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="0ce0a-110">toolearn более об интеграции приложений SaaS с Azure AD, в разделе [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ce0a-110">toolearn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ce0a-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0ce0a-111">Prerequisites</span></span>

<span data-ttu-id="0ce0a-112">tooconfigure интеграция Azure AD с vxMaintain требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0ce0a-112">tooconfigure Azure AD integration with vxMaintain, you need hello following items:</span></span>

- <span data-ttu-id="0ce0a-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0ce0a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="0ce0a-114">подписка vxMaintain с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ce0a-115">При тестировании hello шаги в этом учебнике, рекомендуется не использовать в производственной среде.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-115">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="0ce0a-116">tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="0ce0a-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="0ce0a-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0ce0a-118">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ce0a-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ce0a-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0ce0a-119">Scenario description</span></span>
<span data-ttu-id="0ce0a-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="0ce0a-121">сценарий Hello, описывающий этот учебник состоит из двух основных компонентов.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-121">hello scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="0ce0a-122">Добавление vxMaintain из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0ce0a-122">Adding vxMaintain from hello gallery</span></span>
* <span data-ttu-id="0ce0a-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ce0a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-hello-gallery"></a><span data-ttu-id="0ce0a-124">Добавление vxMaintain из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="0ce0a-124">Add vxMaintain from hello gallery</span></span>
<span data-ttu-id="0ce0a-125">интеграции hello tooconfigure vxMaintain с Azure AD, вы должны vxMaintain tooadd из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-125">tooconfigure hello integration of vxMaintain with Azure AD, you need tooadd vxMaintain from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0ce0a-126">vxMaintain tooadd из галереи hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0ce0a-126">tooadd vxMaintain from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="0ce0a-127">В hello [портал Azure](https://portal.azure.com)в левой области hello, выберите hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-127">In hello [Azure portal](https://portal.azure.com), in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="0ce0a-129">Щелкните **Корпоративные приложения** > **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![панель «Корпоративных приложений» Hello][2]
    
3. <span data-ttu-id="0ce0a-131">приложения, в hello tooadd **все приложения** выберите **новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-131">tooadd an application, in hello **All applications** dialog box, select **New application**.</span></span>

    ![Здравствуйте, «Новое приложение» кнопки][3]

4. <span data-ttu-id="0ce0a-133">Введите в поле поиска hello **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-133">In hello search box, type **vxMaintain**.</span></span>

    ![Hello «В единого входа режим» раскрывающегося списка](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="0ce0a-135">В списке результатов hello выберите **vxMaintain**, а затем выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-135">In hello results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![ссылка vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0ce0a-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ce0a-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0ce0a-138">В этом разделе описана настройка и проверка единого входа Azure AD в vxMaintain с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0ce0a-139">Для toowork единого входа Azure AD необходима toohello tooknow hello vxMaintain аналог пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-139">For SSO toowork, Azure AD needs tooknow hello vxMaintain counterpart toohello Azure AD user.</span></span> <span data-ttu-id="0ce0a-140">То есть необходимо установить связи между hello пользователя Azure AD и соответствующий пользователь vxMaintain hello.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-140">That is, you must establish a link relationship between hello Azure AD user and hello corresponding vxMaintain user.</span></span>

<span data-ttu-id="0ce0a-141">tooestablish hello связи, назначьте hello vxMaintain **имя пользователя** значение как hello Azure AD **Username** значение.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-141">tooestablish hello link relationship, assign hello vxMaintain **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="0ce0a-142">tooconfigure и Azure AD SSO с помощью vxMaintain завершения hello следующие стандартные блоки тестов.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-142">tooconfigure and test Azure AD SSO by using vxMaintain, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="0ce0a-143">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ce0a-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="0ce0a-144">В этом разделе можно включить единый вход Azure AD в hello портал Azure и настройки единого входа в вашем приложении vxMaintain, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="0ce0a-144">In this section, you can both enable Azure AD SSO in hello Azure portal and configure SSO in your vxMaintain application by doing hello following:</span></span>

1. <span data-ttu-id="0ce0a-145">В hello в hello портала Azure **vxMaintain** странице интеграции приложений выберите **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-145">In hello Azure portal, on hello **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![Здравствуйте, команда «Единый вход»][4]

2. <span data-ttu-id="0ce0a-147">tooenable единого входа, в hello **режим-** раскрывающемся списке выберите **входа на базе SAML**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-147">tooenable SSO, in hello **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Hello команды на основе SAML на «вход»](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="0ce0a-149">В разделе **vxMaintain URL-адреса и домена**, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0ce0a-149">Under **vxMaintain Domain and URLs**, do hello following:</span></span>

    ![Здравствуйте, vxMaintain разделе URL-адреса и домена](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="0ce0a-151">а.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-151">a.</span></span> <span data-ttu-id="0ce0a-152">В hello **идентификатор** введите URL-адрес имеет hello синтаксис:`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="0ce0a-152">In hello **Identifier** box, type a URL that has hello following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="0ce0a-153">b.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-153">b.</span></span> <span data-ttu-id="0ce0a-154">В hello **URL-адрес ответа** введите URL-адрес имеет hello синтаксис:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="0ce0a-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0ce0a-155">Hello выше значения не являются реальными.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-155">hello preceding values are not real.</span></span> <span data-ttu-id="0ce0a-156">Дополнить фактический идентификатор hello и URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-156">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="0ce0a-157">значения tooobtain hello, обратитесь в службу hello [vxMaintain поддержки](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="0ce0a-157">tooobtain hello values, contact hello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="0ce0a-158">В разделе **сертификат подписи SAML**выберите **метаданные в формате XML**и сохраните файл tooyour hello метаданных компьютера.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file tooyour computer.</span></span>

    ![раздел «Сертификат подписи SAML» Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="0ce0a-160">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-160">Select **Save**.</span></span>

    ![Кнопка "Сохранить" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0ce0a-162">tooconfigure **vxMaintain** единого входа, загружаются hello отправки **метаданные в формате XML** файл toohello [vxMaintain поддержки](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="0ce0a-162">tooconfigure **vxMaintain** SSO, send hello downloaded **Metadata XML** file toohello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="0ce0a-163">При настройке приложения hello, могут читать четкими версию перед инструкции в hello hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ce0a-163">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0ce0a-164">После добавления приложение hello с hello **Active Directory** > **корпоративных приложений** раздел, выберите hello **Single Sign-On** вкладку, а затем hello доступа внедренные документации из hello **конфигурации** раздела.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-164">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab, and then access hello embedded documentation from hello **Configuration** section.</span></span> 
>
><span data-ttu-id="0ce0a-165">toolearn Дополнительные сведения о функции hello внедренные документации, в разделе [управление единого входа для корпоративных приложений](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="0ce0a-165">toolearn more about hello embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0ce0a-166">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ce0a-166">Create an Azure AD test user</span></span>
<span data-ttu-id="0ce0a-167">В этом разделе создайте тестового пользователя Саймон Britta в hello портал Azure, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="0ce0a-167">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Hello Azure AD тестового пользователя][100]

1. <span data-ttu-id="0ce0a-169">В hello **портал Azure**в левой области hello, выберите hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-169">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![Кнопка «Azure Active Directory» Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0ce0a-171">список пользователей, toodisplay go слишком**пользователей и групп** > **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-171">toodisplay a list of users, go too**Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="0ce0a-172">![Здравствуйте, «Все пользователи» ссылки](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="0ce0a-172">![hello "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="0ce0a-173">Hello **всех пользователей** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-173">hello **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="0ce0a-174">tooopen hello **пользователя** выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-174">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0ce0a-176">В hello **пользователя** диалогового окна поле, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0ce0a-176">In hello **User** dialog box, do hello following:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0ce0a-178">а.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-178">a.</span></span> <span data-ttu-id="0ce0a-179">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-179">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0ce0a-180">b.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-180">b.</span></span> <span data-ttu-id="0ce0a-181">В hello **имя пользователя** поле введите адрес электронной почты hello тестового пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-181">In hello **User name** box, type hello email address of test user Britta Simon.</span></span>

    <span data-ttu-id="0ce0a-182">c.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-182">c.</span></span> <span data-ttu-id="0ce0a-183">Выберите hello **Показать пароль** флажок, а затем значение hello примечание, созданный в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-183">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="0ce0a-184">d.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-184">d.</span></span> <span data-ttu-id="0ce0a-185">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="0ce0a-186">Создание тестового пользователя vxMaintain</span><span class="sxs-lookup"><span data-stu-id="0ce0a-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="0ce0a-187">В этом разделе вы создадите тестового пользователя Britta Simon в vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="0ce0a-188">Пользователи tooadd на платформе vxMaintain hello, работать с [vxMaintain поддержки](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="0ce0a-188">tooadd users in hello vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="0ce0a-189">Прежде чем использовать единый вход, создание и активация пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-189">Before you use SSO, create and activate hello users.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0ce0a-190">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="0ce0a-190">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0ce0a-191">В этом разделе включите тестового пользователя toouse Britta Simon Azure единого входа путем предоставления доступа toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-191">In this section, you enable test user Britta Simon toouse Azure SSO by granting access toovxMaintain.</span></span> <span data-ttu-id="0ce0a-192">toodo таким образом, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0ce0a-192">toodo so, do hello following:</span></span>

![Тестовый пользователь в списке отображаемое имя hello][200] 

1. <span data-ttu-id="0ce0a-194">В hello портал Azure **приложений** просмотреть, перейдите в слишком**каталога** представление > **корпоративных приложений** > **всех приложений**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-194">In hello Azure portal **Applications** view, go too**Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![Здравствуйте, «Все приложения» ссылки][201] 

2. <span data-ttu-id="0ce0a-196">В hello **приложений** выберите **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-196">In hello **Applications** list, select **vxMaintain**.</span></span>

    ![ссылка vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="0ce0a-198">Выберите в левой области hello **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-198">In hello left pane, select **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202] 

4. <span data-ttu-id="0ce0a-200">Выберите **добавить** и затем в hello **добавить назначение** выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-200">Select **Add** and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][203]

5. <span data-ttu-id="0ce0a-202">В hello **пользователей и групп** диалогового окна hello **пользователей** выберите **Britta Simon**и затем выберите hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-202">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**, and then select hello **Select** button.</span></span>

7. <span data-ttu-id="0ce0a-203">В hello **добавить назначение** выберите **назначить**.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-203">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="0ce0a-204">Проверка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ce0a-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="0ce0a-205">В этом разделе можно проверить конфигурацию единого входа Azure AD с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-205">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="0ce0a-206">Выбор hello **vxMaintain** плитки в панели доступа hello следует приложения vxMaintain tooyour автоматического входа.</span><span class="sxs-lookup"><span data-stu-id="0ce0a-206">Selecting hello **vxMaintain** tile in hello Access Panel should sign you in tooyour vxMaintain application automatically.</span></span>

<span data-ttu-id="0ce0a-207">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0ce0a-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ce0a-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0ce0a-208">Next steps</span></span>

* [<span data-ttu-id="0ce0a-209">Список руководств по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ce0a-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ce0a-210">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0ce0a-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

