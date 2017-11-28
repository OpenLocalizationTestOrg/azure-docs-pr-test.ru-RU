---
title: "Учебник. Интеграция Azure Active Directory с Directions on Microsoft | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Directions on Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 59a8b856fd2dc75a37e9bb8f46ced066bcd0fd56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="c3180-103">Руководство. Интеграция Azure Active Directory с Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="c3180-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="c3180-104">В этом учебнике вы узнаете, как toointegrate Directions on Microsoft с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3180-104">In this tutorial, you learn how toointegrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3180-105">Интеграция Directions on Microsoft с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c3180-105">Integrating Directions on Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c3180-106">Можно управлять в Azure AD, имеющего доступ tooDirections на Microsoft</span><span class="sxs-lookup"><span data-stu-id="c3180-106">You can control in Azure AD who has access tooDirections on Microsoft</span></span>
- <span data-ttu-id="c3180-107">Можно включить вашей пользователей tooautomatically get вошедшего tooDirections on Microsoft (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3180-107">You can enable your users tooautomatically get signed-on tooDirections on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c3180-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c3180-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c3180-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3180-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3180-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c3180-110">Prerequisites</span></span>

<span data-ttu-id="c3180-111">tooconfigure интеграция Azure AD с Directions on Microsoft, необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c3180-111">tooconfigure Azure AD integration with Directions on Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="c3180-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c3180-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3180-113">подписка Directions on Microsoft с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c3180-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3180-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c3180-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3180-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c3180-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3180-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c3180-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3180-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3180-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3180-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c3180-118">Scenario description</span></span>
<span data-ttu-id="c3180-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c3180-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3180-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c3180-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3180-121">Добавление документы корпорации Майкрософт из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c3180-121">Adding Directions on Microsoft from hello gallery</span></span>
2. <span data-ttu-id="c3180-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3180-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-hello-gallery"></a><span data-ttu-id="c3180-123">Добавление документы корпорации Майкрософт из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c3180-123">Adding Directions on Microsoft from hello gallery</span></span>
<span data-ttu-id="c3180-124">интеграции hello tooconfigure документы корпорации Майкрософт в Azure AD, вы должны tooadd Directions on Microsoft с hello коллекции tooyour список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c3180-124">tooconfigure hello integration of Directions on Microsoft into Azure AD, you need tooadd Directions on Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c3180-125">**tooadd документы корпорации Майкрософт из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c3180-125">**tooadd Directions on Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3180-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c3180-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c3180-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c3180-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c3180-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c3180-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c3180-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c3180-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c3180-133">Введите в поле поиска hello **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="c3180-133">In hello search box, type **Directions on Microsoft**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="c3180-135">В панели результатов hello выберите **Directions on Microsoft**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c3180-135">In hello results panel, select **Directions on Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c3180-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3180-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c3180-138">В этом разделе описывается настройка и проверка единого входа Azure AD в Directions on Microsoft с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3180-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c3180-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Directions on Microsoft является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3180-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Directions on Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="c3180-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Directions on Microsoft должна установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c3180-140">In other words, a link relationship between an Azure AD user and hello related user in Directions on Microsoft needs toobe established.</span></span>

<span data-ttu-id="c3180-141">В Directions on Microsoft, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="c3180-141">In Directions on Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c3180-142">tooconfigure и теста Azure AD единого входа с Directions on Microsoft, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c3180-142">tooconfigure and test Azure AD single sign-on with Directions on Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c3180-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c3180-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c3180-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c3180-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3180-145">**[Создание инструкции для тестового пользователя Microsoft](#creating-a-directions-on-microsoft-test-user) ** -toohave аналог Саймон Britta в Directions on Microsoft, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c3180-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - toohave a counterpart of Britta Simon in Directions on Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3180-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c3180-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3180-147">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c3180-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c3180-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3180-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c3180-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей Directions on Microsoft application.</span><span class="sxs-lookup"><span data-stu-id="c3180-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="c3180-150">**Azure AD tooconfigure единого входа с Directions on Microsoft, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c3180-150">**tooconfigure Azure AD single sign-on with Directions on Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3180-151">В hello в hello портала Azure **Directions on Microsoft** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c3180-151">In hello Azure portal, on hello **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c3180-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c3180-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="c3180-155">На hello **Directions on Microsoft доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c3180-155">On hello **Directions on Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="c3180-157">а.</span><span class="sxs-lookup"><span data-stu-id="c3180-157">a.</span></span> <span data-ttu-id="c3180-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="c3180-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="c3180-159">b.</span><span class="sxs-lookup"><span data-stu-id="c3180-159">b.</span></span> <span data-ttu-id="c3180-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="c3180-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="c3180-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c3180-161">These values are not real.</span></span> <span data-ttu-id="c3180-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="c3180-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c3180-163">Обратитесь к [поддержки Directions on Microsoft Client](mailto:service@DirectionsOnMicrosoft.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="c3180-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="c3180-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c3180-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="c3180-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c3180-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c3180-168">tooconfigure единого входа на **Directions on Microsoft** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[поддержки Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="c3180-168">tooconfigure single sign-on on **Directions on Microsoft** side, you need toosend hello downloaded **Metadata XML** too[Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="c3180-169">hello tooenable Directions on Microsoft поддерживает toolocate команды членство в федеративном сайте, включают сведения о компании в ваш адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="c3180-169">tooenable hello Directions on Microsoft support team toolocate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="c3180-170">Единого входа для Directions on Microsoft должна включаемые hello toobe [поддержки Directions on Microsoft клиента](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="c3180-170">Single sign-on for Directions on Microsoft needs toobe enabled by hello [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="c3180-171">Вы получите уведомление, когда такой единый вход будет включен.</span><span class="sxs-lookup"><span data-stu-id="c3180-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="c3180-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c3180-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c3180-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c3180-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c3180-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c3180-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c3180-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3180-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="c3180-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c3180-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c3180-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c3180-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3180-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c3180-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c3180-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c3180-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c3180-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="c3180-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c3180-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c3180-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c3180-187">а.</span><span class="sxs-lookup"><span data-stu-id="c3180-187">a.</span></span> <span data-ttu-id="c3180-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3180-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3180-189">b.</span><span class="sxs-lookup"><span data-stu-id="c3180-189">b.</span></span> <span data-ttu-id="c3180-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c3180-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c3180-191">c.</span><span class="sxs-lookup"><span data-stu-id="c3180-191">c.</span></span> <span data-ttu-id="c3180-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c3180-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c3180-193">d.</span><span class="sxs-lookup"><span data-stu-id="c3180-193">d.</span></span> <span data-ttu-id="c3180-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c3180-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="c3180-195">Создание тестового пользователя Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="c3180-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="c3180-196">Нет элемента действия для вас tooconfigure подготовки пользователей tooDirections корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c3180-196">There is no action item for you tooconfigure user provisioning tooDirections on Microsoft.</span></span>  

<span data-ttu-id="c3180-197">Когда назначенный пользователь пытается toolog в tooDirections on Microsoft с помощью панели доступа hello, Directions on Microsoft проверяет, существует ли пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="c3180-197">When an assigned user tries toolog in tooDirections on Microsoft using hello access panel, Directions on Microsoft checks whether hello user exists.</span></span> <span data-ttu-id="c3180-198">Если учетная запись пользователя отсутствует, Directions on Microsoft автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="c3180-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c3180-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c3180-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c3180-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooDirections on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c3180-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirections on Microsoft.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c3180-202">**tooassign tooDirections Britta Simon on Microsoft, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="c3180-202">**tooassign Britta Simon tooDirections on Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3180-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c3180-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c3180-205">В списке приложений hello выберите **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="c3180-205">In hello applications list, select **Directions on Microsoft**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="c3180-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c3180-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c3180-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c3180-209">Click **Add** button.</span></span> <span data-ttu-id="c3180-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c3180-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c3180-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c3180-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c3180-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c3180-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3180-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c3180-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c3180-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c3180-215">Testing single sign-on</span></span>

<span data-ttu-id="c3180-216">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c3180-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="c3180-217">При нажатии кнопки hello Directions on Microsoft плитки в панели доступа hello, вы должны получить направлениях tooyour автоматически вошедшего в приложении Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c3180-217">When you click hello Directions on Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour Directions on Microsoft application.</span></span>

<span data-ttu-id="c3180-218">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c3180-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c3180-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c3180-219">Additional resources</span></span>

* [<span data-ttu-id="c3180-220">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3180-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3180-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c3180-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

