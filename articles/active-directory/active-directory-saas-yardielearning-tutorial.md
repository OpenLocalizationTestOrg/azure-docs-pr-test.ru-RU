---
title: "Руководство по интеграции Azure Active Directory с Yardi eLearning | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Yardi электронного обучения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7ea58b54-ec5b-4576-8586-814b11d0f4fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 47c95fe024e76a67aa5c5b3ee6f81cbafc50ff07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yardi-elearning"></a><span data-ttu-id="f0819-103">Учебник. Интеграция Azure Active Directory с Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="f0819-103">Tutorial: Azure Active Directory integration with Yardi eLearning</span></span>

<span data-ttu-id="f0819-104">В этом учебнике вы узнаете, как электронного Yardi toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0819-104">In this tutorial, you learn how toointegrate Yardi eLearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0819-105">Интеграция Yardi электронного обучения с помощью Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f0819-105">Integrating Yardi eLearning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f0819-106">Можно управлять в Azure AD, имеющего электронного tooYardi доступа</span><span class="sxs-lookup"><span data-stu-id="f0819-106">You can control in Azure AD who has access tooYardi eLearning</span></span>
- <span data-ttu-id="f0819-107">Можно включить на пользователей tooautomatically get tooYardi вошедшего электронного (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0819-107">You can enable your users tooautomatically get signed-on tooYardi eLearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0819-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f0819-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f0819-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0819-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0819-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f0819-110">Prerequisites</span></span>

<span data-ttu-id="f0819-111">tooconfigure интеграция Azure AD с помощью электронного Yardi требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f0819-111">tooconfigure Azure AD integration with Yardi eLearning, you need hello following items:</span></span>

- <span data-ttu-id="f0819-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f0819-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0819-113">подписка Yardi eLearning с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f0819-113">A Yardi eLearning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0819-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f0819-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0819-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f0819-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0819-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f0819-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0819-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0819-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0819-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f0819-118">Scenario description</span></span>
<span data-ttu-id="f0819-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f0819-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0819-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f0819-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0819-121">Добавление электронного Yardi из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f0819-121">Adding Yardi eLearning from hello gallery</span></span>
2. <span data-ttu-id="f0819-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0819-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yardi-elearning-from-hello-gallery"></a><span data-ttu-id="f0819-123">Добавление электронного Yardi из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f0819-123">Adding Yardi eLearning from hello gallery</span></span>
<span data-ttu-id="f0819-124">tooconfigure hello интеграции Yardi электронного обучения в Azure AD, вы должны электронного Yardi tooadd из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f0819-124">tooconfigure hello integration of Yardi eLearning into Azure AD, you need tooadd Yardi eLearning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f0819-125">**tooadd Yardi электронного из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="f0819-125">**tooadd Yardi eLearning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0819-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f0819-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f0819-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f0819-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f0819-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f0819-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f0819-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f0819-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f0819-133">Введите в поле поиска hello **Yardi электронного**.</span><span class="sxs-lookup"><span data-stu-id="f0819-133">In hello search box, type **Yardi eLearning**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_search.png)

5. <span data-ttu-id="f0819-135">В панели результатов hello выберите **электронного Yardi**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f0819-135">In hello results panel, select **Yardi eLearning**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0819-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0819-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0819-138">Этот раздел описывает настройку и проверку единого входа Azure AD в Yardi eLearning с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0819-138">In this section, you configure and test Azure AD single sign-on with Yardi eLearning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f0819-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Yardi электронного является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0819-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Yardi eLearning is tooa user in Azure AD.</span></span> <span data-ttu-id="f0819-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Yardi электронного должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f0819-140">In other words, a link relationship between an Azure AD user and hello related user in Yardi eLearning needs toobe established.</span></span>

<span data-ttu-id="f0819-141">В Yardi электронного обучения, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="f0819-141">In Yardi eLearning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f0819-142">tooconfigure и теста Azure AD единого входа с Yardi электронного обучения, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f0819-142">tooconfigure and test Azure AD single sign-on with Yardi eLearning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f0819-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f0819-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f0819-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f0819-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0819-145">**[Создание тестового пользователя электронного Yardi](#creating-a-yardi-elearning-test-user)**  -toohave аналог Саймон Britta в Yardi электронного обучения, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f0819-145">**[Creating a Yardi eLearning test user](#creating-a-yardi-elearning-test-user)** - toohave a counterpart of Britta Simon in Yardi eLearning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f0819-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f0819-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0819-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f0819-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f0819-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0819-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f0819-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Yardi электронного обучения.</span><span class="sxs-lookup"><span data-stu-id="f0819-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Yardi eLearning application.</span></span>

<span data-ttu-id="f0819-150">**tooconfigure Azure AD единого входа с помощью электронного Yardi выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f0819-150">**tooconfigure Azure AD single sign-on with Yardi eLearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0819-151">В hello в hello портала Azure **электронного Yardi** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f0819-151">In hello Azure portal, on hello **Yardi eLearning** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f0819-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f0819-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_samlbase.png)

3. <span data-ttu-id="f0819-155">На hello **Yardi электронного URL-адреса и домена** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f0819-155">On hello **Yardi eLearning Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_url.png)

    <span data-ttu-id="f0819-157">а.</span><span class="sxs-lookup"><span data-stu-id="f0819-157">a.</span></span> <span data-ttu-id="f0819-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.yardielearning.com/login`</span><span class="sxs-lookup"><span data-stu-id="f0819-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.yardielearning.com/login`</span></span>

    <span data-ttu-id="f0819-159">b.</span><span class="sxs-lookup"><span data-stu-id="f0819-159">b.</span></span> <span data-ttu-id="f0819-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.yardielearning.com/trust`</span><span class="sxs-lookup"><span data-stu-id="f0819-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.yardielearning.com/trust`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f0819-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f0819-161">These values are not real.</span></span> <span data-ttu-id="f0819-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="f0819-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f0819-163">Обратитесь к [группа поддержки клиента электронного Yardi](mailto:elearning@yardi.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f0819-163">Contact [Yardi eLearning Client support team](mailto:elearning@yardi.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="f0819-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f0819-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_certificate.png) 

5. <span data-ttu-id="f0819-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f0819-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-yardielearning-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f0819-168">tooconfigure единого входа на **электронного Yardi** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группа поддержки электронного Yardi](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="f0819-168">tooconfigure single sign-on on **Yardi eLearning** side, you need toosend hello downloaded **Metadata XML** too[Yardi eLearning support team](mailto:elearning@yardi.com).</span></span> 

> [!TIP]
> <span data-ttu-id="f0819-169">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f0819-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f0819-170">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f0819-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f0819-171">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0819-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0819-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0819-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0819-173">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f0819-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f0819-175">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f0819-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0819-176">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f0819-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f0819-178">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f0819-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f0819-180">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f0819-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f0819-182">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f0819-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0819-184">а.</span><span class="sxs-lookup"><span data-stu-id="f0819-184">a.</span></span> <span data-ttu-id="f0819-185">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0819-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0819-186">b.</span><span class="sxs-lookup"><span data-stu-id="f0819-186">b.</span></span> <span data-ttu-id="f0819-187">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f0819-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0819-188">c.</span><span class="sxs-lookup"><span data-stu-id="f0819-188">c.</span></span> <span data-ttu-id="f0819-189">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f0819-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f0819-190">d.</span><span class="sxs-lookup"><span data-stu-id="f0819-190">d.</span></span> <span data-ttu-id="f0819-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f0819-191">Click **Create**.</span></span>
 
### <a name="creating-a-yardi-elearning-test-user"></a><span data-ttu-id="f0819-192">Создание тестового пользователя Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="f0819-192">Creating a Yardi eLearning test user</span></span>

<span data-ttu-id="f0819-193">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Yardi электронного обучения.</span><span class="sxs-lookup"><span data-stu-id="f0819-193">hello objective of this section is toocreate a user called Britta Simon in Yardi eLearning.</span></span> <span data-ttu-id="f0819-194">Приложение Yardi eLearning поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f0819-194">Yardi eLearning supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f0819-195">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="f0819-195">There is no action item for you in this section.</span></span> <span data-ttu-id="f0819-196">Новый пользователь создается во время попытки tooaccess Yardi электронного, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="f0819-196">A new user is created during an attempt tooaccess Yardi eLearning if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="f0819-197">Если требуется toocreate пользователя вручную, необходимо toocontact hello [группа поддержки электронного Yardi](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="f0819-197">If you need toocreate a user manually, you need toocontact hello [Yardi eLearning support team](mailto:elearning@yardi.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f0819-198">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f0819-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f0819-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooYardi электронного.</span><span class="sxs-lookup"><span data-stu-id="f0819-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYardi eLearning.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f0819-201">**tooassign Britta Simon tooYardi электронного обучения, выполнять hello следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="f0819-201">**tooassign Britta Simon tooYardi eLearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0819-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f0819-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f0819-204">В списке приложений hello выберите **Yardi электронного**.</span><span class="sxs-lookup"><span data-stu-id="f0819-204">In hello applications list, select **Yardi eLearning**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_app.png) 

3. <span data-ttu-id="f0819-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f0819-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f0819-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f0819-208">Click **Add** button.</span></span> <span data-ttu-id="f0819-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f0819-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f0819-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f0819-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f0819-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f0819-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0819-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f0819-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f0819-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f0819-214">Testing single sign-on</span></span>

<span data-ttu-id="f0819-215">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="f0819-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f0819-216">При выборе плитки электронного Yardi hello в hello панели доступа, следует получать автоматически вошедшего tooyour Yardi электронного приложения.</span><span class="sxs-lookup"><span data-stu-id="f0819-216">When you click hello Yardi eLearning tile in hello Access Panel, you should get automatically signed-on tooyour Yardi eLearning application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f0819-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f0819-217">Additional resources</span></span>

* [<span data-ttu-id="f0819-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0819-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0819-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0819-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_203.png

