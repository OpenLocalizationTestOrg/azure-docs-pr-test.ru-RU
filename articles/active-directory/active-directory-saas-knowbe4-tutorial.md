---
title: "Руководство по интеграции Azure Active Directory с KnowBe4 Security Awareness Training | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и KnowBe4 безопасности курса обучения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 907fa814b82c9ffb2376f73470b746a37104c66e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a><span data-ttu-id="eabef-103">Руководство по интеграции Azure Active Directory с KnowBe4 Security Awareness Training</span><span class="sxs-lookup"><span data-stu-id="eabef-103">Tutorial: Azure Active Directory integration with KnowBe4 Security Awareness Training</span></span>

<span data-ttu-id="eabef-104">В этом учебнике вы узнаете, как toointegrate KnowBe4 безопасности курса обучения в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eabef-104">In this tutorial, you learn how toointegrate KnowBe4 Security Awareness Training with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eabef-105">Интеграция KnowBe4 безопасности курса обучения с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="eabef-105">Integrating KnowBe4 Security Awareness Training with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eabef-106">Можно управлять в Azure AD, имеющего доступ к tooKnowBe4 безопасности курса обучения</span><span class="sxs-lookup"><span data-stu-id="eabef-106">You can control in Azure AD who has access tooKnowBe4 Security Awareness Training</span></span>
- <span data-ttu-id="eabef-107">Это позволит пользователям получить tooautomatically вошедшего tooKnowBe4 безопасности курса обучения (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="eabef-107">You can enable your users tooautomatically get signed-on tooKnowBe4 Security Awareness Training (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eabef-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="eabef-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eabef-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eabef-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eabef-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="eabef-110">Prerequisites</span></span>

<span data-ttu-id="eabef-111">tooconfigure интеграция Azure AD с KnowBe4 безопасности курса обучения необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="eabef-111">tooconfigure Azure AD integration with KnowBe4 Security Awareness Training, you need hello following items:</span></span>

- <span data-ttu-id="eabef-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="eabef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eabef-113">подписка KnowBe4 Security Awareness Training с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="eabef-113">A KnowBe4 Security Awareness Training single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eabef-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="eabef-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eabef-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="eabef-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eabef-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="eabef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eabef-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eabef-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eabef-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="eabef-118">Scenario description</span></span>
<span data-ttu-id="eabef-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="eabef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eabef-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="eabef-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eabef-121">Добавление KnowBe4 безопасности курса обучения из галереи hello</span><span class="sxs-lookup"><span data-stu-id="eabef-121">Adding KnowBe4 Security Awareness Training from hello gallery</span></span>
2. <span data-ttu-id="eabef-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="eabef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowbe4-security-awareness-training-from-hello-gallery"></a><span data-ttu-id="eabef-123">Добавление KnowBe4 безопасности курса обучения из галереи hello</span><span class="sxs-lookup"><span data-stu-id="eabef-123">Adding KnowBe4 Security Awareness Training from hello gallery</span></span>
<span data-ttu-id="eabef-124">tooconfigure hello интеграции KnowBe4 безопасности курса обучения в Azure AD, вы должны tooadd KnowBe4 безопасности курса обучения из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="eabef-124">tooconfigure hello integration of KnowBe4 Security Awareness Training into Azure AD, you need tooadd KnowBe4 Security Awareness Training from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eabef-125">**tooadd KnowBe4 безопасности курса обучения из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="eabef-125">**tooadd KnowBe4 Security Awareness Training from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eabef-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="eabef-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eabef-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="eabef-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eabef-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="eabef-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="eabef-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="eabef-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="eabef-133">Введите в поле поиска hello **KnowBe4 безопасности курса обучения**.</span><span class="sxs-lookup"><span data-stu-id="eabef-133">In hello search box, type **KnowBe4 Security Awareness Training**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_search.png)

5. <span data-ttu-id="eabef-135">В панели результатов hello выберите **KnowBe4 безопасности курса обучения**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="eabef-135">In hello results panel, select **KnowBe4 Security Awareness Training**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eabef-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="eabef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eabef-138">В этом разделе описана настройка и проверка единого входа Azure AD в KnowBe4 Security Awareness Training с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eabef-138">In this section, you configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eabef-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в KnowBe4 безопасности курса обучения является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eabef-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in KnowBe4 Security Awareness Training is tooa user in Azure AD.</span></span> <span data-ttu-id="eabef-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в KnowBe4 безопасности курса обучения должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="eabef-140">In other words, a link relationship between an Azure AD user and hello related user in KnowBe4 Security Awareness Training needs toobe established.</span></span>

<span data-ttu-id="eabef-141">При обучении осведомленности KnowBe4 безопасности, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="eabef-141">In KnowBe4 Security Awareness Training, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eabef-142">tooconfigure и теста Azure AD единого входа с KnowBe4 безопасности курса обучения, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="eabef-142">tooconfigure and test Azure AD single sign-on with KnowBe4 Security Awareness Training, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eabef-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="eabef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eabef-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="eabef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eabef-145">**[Создание тестового пользователя курса обучения безопасности KnowBe4](#creating-a-knowbe4-security-awareness-training-test-user)**  -toohave аналог Саймон Britta в KnowBe4 безопасности курса обучения, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="eabef-145">**[Creating a KnowBe4 Security Awareness Training test user](#creating-a-knowbe4-security-awareness-training-test-user)** - toohave a counterpart of Britta Simon in KnowBe4 Security Awareness Training that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eabef-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="eabef-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eabef-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="eabef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eabef-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="eabef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eabef-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении KnowBe4 безопасности курса обучения.</span><span class="sxs-lookup"><span data-stu-id="eabef-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your KnowBe4 Security Awareness Training application.</span></span>

<span data-ttu-id="eabef-150">**tooconfigure Azure AD единого входа с KnowBe4 безопасности курса обучения, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="eabef-150">**tooconfigure Azure AD single sign-on with KnowBe4 Security Awareness Training, perform hello following steps:**</span></span>

1. <span data-ttu-id="eabef-151">В hello в hello портала Azure **KnowBe4 безопасности курса обучения** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="eabef-151">In hello Azure portal, on hello **KnowBe4 Security Awareness Training** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="eabef-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="eabef-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_samlbase.png)

3. <span data-ttu-id="eabef-155">На hello **осведомленности обучения KnowBe4 безопасности домена и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="eabef-155">On hello **KnowBe4 Security Awareness Training Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_url.png)

    <span data-ttu-id="eabef-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="eabef-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eabef-158">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="eabef-158">hello value is not real.</span></span> <span data-ttu-id="eabef-159">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="eabef-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="eabef-160">Обратитесь к [группа поддержки осведомленности обучения KnowBe4 безопасности клиента](mailto:support@KnowBe4.com) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="eabef-160">Contact [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com) tooget hello value.</span></span> 
 

4. <span data-ttu-id="eabef-161">На hello **сертификат подписи SAML** щелкните **сертификата (Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="eabef-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_certificate.png) 

5. <span data-ttu-id="eabef-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="eabef-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eabef-165">На hello **KnowBe4 безопасности осведомленности обучения конфигурации** щелкните **курса обучения настройки безопасности KnowBe4** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="eabef-165">On hello **KnowBe4 Security Awareness Training Configuration** section, click **Configure KnowBe4 Security Awareness Training** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eabef-166">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="eabef-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_configure.png) 

7. <span data-ttu-id="eabef-168">tooconfigure единого входа на **KnowBe4 безопасности курса обучения** стороны, необходимо загрузить hello toosend **сертификата (Raw)**, **URL-адрес выхода, идентификатор сущности SAML и SAML Single Sign-On URL-адрес службы** слишком[группа поддержки осведомленности обучения KnowBe4 безопасности клиента](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="eabef-168">tooconfigure single sign-on on **KnowBe4 Security Awareness Training** side, you need toosend hello downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com).</span></span>

> [!TIP]
> <span data-ttu-id="eabef-169">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="eabef-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eabef-170">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="eabef-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eabef-171">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eabef-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eabef-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="eabef-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="eabef-173">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="eabef-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="eabef-175">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="eabef-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eabef-176">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="eabef-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eabef-178">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="eabef-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eabef-180">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="eabef-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eabef-182">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="eabef-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eabef-184">а.</span><span class="sxs-lookup"><span data-stu-id="eabef-184">a.</span></span> <span data-ttu-id="eabef-185">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eabef-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eabef-186">b.</span><span class="sxs-lookup"><span data-stu-id="eabef-186">b.</span></span> <span data-ttu-id="eabef-187">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eabef-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eabef-188">c.</span><span class="sxs-lookup"><span data-stu-id="eabef-188">c.</span></span> <span data-ttu-id="eabef-189">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="eabef-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eabef-190">d.</span><span class="sxs-lookup"><span data-stu-id="eabef-190">d.</span></span> <span data-ttu-id="eabef-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="eabef-191">Click **Create**.</span></span>
 
### <a name="creating-a-knowbe4-security-awareness-training-test-user"></a><span data-ttu-id="eabef-192">Создание тестового пользователя KnowBe4 Security Awareness Training</span><span class="sxs-lookup"><span data-stu-id="eabef-192">Creating a KnowBe4 Security Awareness Training test user</span></span>

<span data-ttu-id="eabef-193">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в KnowBe4 безопасности курса обучения.</span><span class="sxs-lookup"><span data-stu-id="eabef-193">hello objective of this section is toocreate a user called Britta Simon in KnowBe4 Security Awareness Training.</span></span> <span data-ttu-id="eabef-194">Приложение KnowBe4 Security Awareness Training поддерживает JIT-подготовку, включенную по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="eabef-194">KnowBe4 Security Awareness Training supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="eabef-195">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="eabef-195">There is no action item for you in this section.</span></span> <span data-ttu-id="eabef-196">Новый пользователь создается во время попытки tooaccess KnowBe4 безопасности курса обучения, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="eabef-196">A new user is created during an attempt tooaccess KnowBe4 Security Awareness Training if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="eabef-197">Если требуется toocreate пользователя вручную, необходимо toocontact hello [KnowBe4 безопасности курса обучения поддержки](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="eabef-197">If you need toocreate a user manually, you need toocontact hello [KnowBe4 Security Awareness Training support team](mailto:support@KnowBe4.com).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eabef-198">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="eabef-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eabef-199">В этом разделе включите Саймон Britta toouse Azure единого входа путем предоставления доступа к tooKnowBe4 безопасности курса обучения.</span><span class="sxs-lookup"><span data-stu-id="eabef-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKnowBe4 Security Awareness Training.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="eabef-201">**tooassign Britta Simon tooKnowBe4 безопасности курса обучения выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="eabef-201">**tooassign Britta Simon tooKnowBe4 Security Awareness Training, perform hello following steps:**</span></span>

1. <span data-ttu-id="eabef-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="eabef-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="eabef-204">В списке приложений hello выберите **KnowBe4 безопасности курса обучения**.</span><span class="sxs-lookup"><span data-stu-id="eabef-204">In hello applications list, select **KnowBe4 Security Awareness Training**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_app.png) 

3. <span data-ttu-id="eabef-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="eabef-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="eabef-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="eabef-208">Click **Add** button.</span></span> <span data-ttu-id="eabef-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="eabef-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="eabef-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="eabef-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eabef-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="eabef-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eabef-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="eabef-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eabef-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="eabef-214">Testing single sign-on</span></span>

<span data-ttu-id="eabef-215">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="eabef-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="eabef-216">Если щелкнуть плитку KnowBe4 безопасности курса обучения hello в hello панели доступа, следует получать автоматически вошедшего tooyour курса обучения KnowBe4 безопасности приложения.</span><span class="sxs-lookup"><span data-stu-id="eabef-216">When you click hello KnowBe4 Security Awareness Training tile in hello Access Panel, you should get automatically signed-on tooyour KnowBe4 Security Awareness Training application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eabef-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="eabef-217">Additional resources</span></span>

* [<span data-ttu-id="eabef-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eabef-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eabef-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eabef-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_203.png

