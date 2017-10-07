---
title: "Руководство по интеграции Azure Active Directory с Learning Seat LMS | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и обучения LMS рабочих мест."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: dc08aa444b85f35a4458768ac560ec663baa1c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="86a9d-103">Руководство по интеграции Azure Active Directory с Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="86a9d-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="86a9d-104">В этом учебнике вы узнаете, как toointegrate LMS рабочее место обучения в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86a9d-104">In this tutorial, you learn how toointegrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86a9d-105">Интеграция рабочих мест LMS обучения с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="86a9d-105">Integrating Learning Seat LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="86a9d-106">Можно управлять в Azure AD, имеющего доступ tooLearning LMS рабочих мест</span><span class="sxs-lookup"><span data-stu-id="86a9d-106">You can control in Azure AD who has access tooLearning Seat LMS</span></span>
- <span data-ttu-id="86a9d-107">Ваш пользователей tooautomatically get вошедшего tooLearning LMS рабочих мест (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a9d-107">You can enable your users tooautomatically get signed-on tooLearning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86a9d-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="86a9d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="86a9d-109">Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86a9d-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="86a9d-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86a9d-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86a9d-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="86a9d-111">Prerequisites</span></span>

<span data-ttu-id="86a9d-112">tooconfigure интеграция Azure AD с LMS обучения рабочих мест необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="86a9d-112">tooconfigure Azure AD integration with Learning Seat LMS, you need hello following items:</span></span>

- <span data-ttu-id="86a9d-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="86a9d-113">An Azure AD subscription</span></span>
- <span data-ttu-id="86a9d-114">подписка на Learning Seat LMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="86a9d-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86a9d-115">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="86a9d-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86a9d-116">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="86a9d-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86a9d-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="86a9d-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86a9d-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86a9d-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86a9d-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="86a9d-119">Scenario description</span></span>
<span data-ttu-id="86a9d-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="86a9d-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86a9d-121">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="86a9d-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86a9d-122">Добавление рабочих мест LMS обучения из галереи hello</span><span class="sxs-lookup"><span data-stu-id="86a9d-122">Adding Learning Seat LMS from hello gallery</span></span>
2. <span data-ttu-id="86a9d-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a9d-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-hello-gallery"></a><span data-ttu-id="86a9d-124">Добавление рабочих мест LMS обучения из галереи hello</span><span class="sxs-lookup"><span data-stu-id="86a9d-124">Adding Learning Seat LMS from hello gallery</span></span>
<span data-ttu-id="86a9d-125">tooconfigure hello Интеграция рабочих мест LMS обучения в Azure AD, вы должны tooadd LMS рабочее место обучения из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="86a9d-125">tooconfigure hello integration of Learning Seat LMS into Azure AD, you need tooadd Learning Seat LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="86a9d-126">**tooadd LMS рабочее место обучения из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="86a9d-126">**tooadd Learning Seat LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a9d-127">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="86a9d-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="86a9d-129">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="86a9d-130">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-130">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="86a9d-132">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="86a9d-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="86a9d-134">Введите в поле поиска hello **LMS рабочее место обучения**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-134">In hello search box, type **Learning Seat LMS**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="86a9d-136">В панели результатов hello выберите **LMS рабочее место обучения**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="86a9d-136">In hello results panel, select **Learning Seat LMS**, and then click **Add** button tooadd hello application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="86a9d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a9d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="86a9d-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Learning Seat LMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86a9d-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="86a9d-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в рабочее место LMS обучения является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86a9d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning Seat LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="86a9d-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в рабочее место LMS обучения должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="86a9d-140">In other words, a link relationship between an Azure AD user and hello related user in Learning Seat LMS needs toobe established.</span></span>

<span data-ttu-id="86a9d-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в рабочее место LMS обучения.</span><span class="sxs-lookup"><span data-stu-id="86a9d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="86a9d-142">tooconfigure и теста Azure AD единого входа с LMS рабочее место обучения, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="86a9d-142">tooconfigure and test Azure AD single sign-on with Learning Seat LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="86a9d-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="86a9d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="86a9d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="86a9d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86a9d-145">**[Создание тестового пользователя LMS рабочее место обучения](#creating-a-learnconnect-test-user)**  -toohave аналог Саймон Britta в LMS рабочее место обучения, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="86a9d-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - toohave a counterpart of Britta Simon in Learning Seat LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="86a9d-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="86a9d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86a9d-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="86a9d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="86a9d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a9d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="86a9d-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LMS обучения рабочих мест.</span><span class="sxs-lookup"><span data-stu-id="86a9d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="86a9d-150">**tooconfigure Azure AD единого входа с LMS обучения рабочее место, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="86a9d-150">**tooconfigure Azure AD single sign-on with Learning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a9d-151">В hello в hello портала Azure **LMS рабочее место обучения** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-151">In hello Azure portal, on hello **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="86a9d-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="86a9d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="86a9d-155">На hello **URL-адреса и домена LMS обучения рабочее место** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="86a9d-155">On hello **Learning Seat LMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="86a9d-157">а.</span><span class="sxs-lookup"><span data-stu-id="86a9d-157">a.</span></span> <span data-ttu-id="86a9d-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="86a9d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="86a9d-159">b.</span><span class="sxs-lookup"><span data-stu-id="86a9d-159">b.</span></span> <span data-ttu-id="86a9d-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="86a9d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="86a9d-161">Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="86a9d-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="86a9d-163">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="86a9d-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="86a9d-164">Эти значения не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="86a9d-164">These values are not hello real values.</span></span> <span data-ttu-id="86a9d-165">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="86a9d-165">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="86a9d-166">Обратитесь к [группа поддержки рабочее место обучения](http://help.learningseatlms.com/help) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="86a9d-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) tooget these values.</span></span> 

5. <span data-ttu-id="86a9d-167">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="86a9d-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="86a9d-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="86a9d-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="86a9d-171">tooconfigure единого входа на **LMS рабочее место обучения** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группа поддержки рабочее место обучения](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="86a9d-171">tooconfigure single sign-on on **Learning Seat LMS** side, you need toosend hello downloaded **Metadata XML** too[Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="86a9d-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="86a9d-172">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="86a9d-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="86a9d-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="86a9d-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86a9d-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="86a9d-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a9d-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="86a9d-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="86a9d-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="86a9d-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="86a9d-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a9d-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="86a9d-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86a9d-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86a9d-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="86a9d-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86a9d-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="86a9d-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86a9d-187">а.</span><span class="sxs-lookup"><span data-stu-id="86a9d-187">a.</span></span> <span data-ttu-id="86a9d-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86a9d-189">b.</span><span class="sxs-lookup"><span data-stu-id="86a9d-189">b.</span></span> <span data-ttu-id="86a9d-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="86a9d-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86a9d-191">c.</span><span class="sxs-lookup"><span data-stu-id="86a9d-191">c.</span></span> <span data-ttu-id="86a9d-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="86a9d-193">d.</span><span class="sxs-lookup"><span data-stu-id="86a9d-193">d.</span></span> <span data-ttu-id="86a9d-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="86a9d-195">Создание тестового пользователя Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="86a9d-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="86a9d-196">В этом разделе описано, как создать пользователя Britta Simon в приложении Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="86a9d-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="86a9d-197">Обратитесь к [группа поддержки рабочее место обучения](http://help.learningseatlms.com/help) со всеми hello пользователя сведения tooadd hello пользователями в hello LMS рабочее место обучения приложения.</span><span class="sxs-lookup"><span data-stu-id="86a9d-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all hello user information tooadd hello users in hello Learning Seat LMS application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="86a9d-198">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="86a9d-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="86a9d-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLearning LMS рабочих мест.</span><span class="sxs-lookup"><span data-stu-id="86a9d-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning Seat LMS.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="86a9d-201">**tooassign tooLearning Britta Simon LMS рабочее место выполнения hello следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="86a9d-201">**tooassign Britta Simon tooLearning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a9d-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="86a9d-204">В списке приложений hello выберите **LMS рабочее место обучения**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-204">In hello applications list, select **Learning Seat LMS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="86a9d-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="86a9d-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-208">Click **Add** button.</span></span> <span data-ttu-id="86a9d-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="86a9d-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="86a9d-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="86a9d-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86a9d-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="86a9d-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="86a9d-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="86a9d-214">Testing single sign-on</span></span>

<span data-ttu-id="86a9d-215">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="86a9d-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="86a9d-216">Щелкните hello LMS рабочее место обучения плитку в hello панель доступа будет автоматически подписан на tooyour LMS рабочее место обучения приложения.</span><span class="sxs-lookup"><span data-stu-id="86a9d-216">Click hello Learning Seat LMS tile in hello Access Panel, you will be automatically signed-on tooyour Learning Seat LMS application.</span></span> <span data-ttu-id="86a9d-217">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="86a9d-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86a9d-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="86a9d-218">Additional resources</span></span>

* [<span data-ttu-id="86a9d-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86a9d-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86a9d-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="86a9d-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

