---
title: "Руководство по интеграции Azure Active Directory с Tidemark | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Tidemark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5cf80d4e-6e8b-48ec-81c8-27872af5e5d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 4fffee30370d928ae8070a5904c58ba8a7a06343
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tidemark"></a><span data-ttu-id="3228f-103">Руководство. Интеграция Azure Active Directory с Tidemark</span><span class="sxs-lookup"><span data-stu-id="3228f-103">Tutorial: Azure Active Directory integration with Tidemark</span></span>

<span data-ttu-id="3228f-104">В этом учебнике вы узнаете, как toointegrate Tidemark с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3228f-104">In this tutorial, you learn how toointegrate Tidemark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3228f-105">Интеграция с Azure AD Tidemark предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3228f-105">Integrating Tidemark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3228f-106">Можно управлять в Azure AD, имеющего доступ tooTidemark</span><span class="sxs-lookup"><span data-stu-id="3228f-106">You can control in Azure AD who has access tooTidemark</span></span>
- <span data-ttu-id="3228f-107">Можно включить на пользователей tooautomatically get вошедшего tooTidemark (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="3228f-107">You can enable your users tooautomatically get signed-on tooTidemark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3228f-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3228f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3228f-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3228f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3228f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3228f-110">Prerequisites</span></span>

<span data-ttu-id="3228f-111">tooconfigure интеграция Azure AD с Tidemark требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3228f-111">tooconfigure Azure AD integration with Tidemark, you need hello following items:</span></span>

- <span data-ttu-id="3228f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3228f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3228f-113">подписка Tidemark с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3228f-113">A Tidemark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3228f-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="3228f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3228f-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="3228f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3228f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3228f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3228f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3228f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3228f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3228f-118">Scenario description</span></span>
<span data-ttu-id="3228f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3228f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3228f-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="3228f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3228f-121">Добавление Tidemark из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3228f-121">Adding Tidemark from hello gallery</span></span>
2. <span data-ttu-id="3228f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3228f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tidemark-from-hello-gallery"></a><span data-ttu-id="3228f-123">Добавление Tidemark из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3228f-123">Adding Tidemark from hello gallery</span></span>
<span data-ttu-id="3228f-124">tooconfigure hello интеграции Tidemark в Azure AD, вы должны tooadd Tidemark из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3228f-124">tooconfigure hello integration of Tidemark into Azure AD, you need tooadd Tidemark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3228f-125">**tooadd Tidemark из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3228f-125">**tooadd Tidemark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3228f-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3228f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3228f-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="3228f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3228f-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3228f-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3228f-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="3228f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3228f-133">Введите в поле поиска hello **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="3228f-133">In hello search box, type **Tidemark**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_search.png)

5. <span data-ttu-id="3228f-135">В панели результатов hello выберите **Tidemark**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3228f-135">In hello results panel, select **Tidemark**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3228f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3228f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3228f-138">В этом разделе описана настройка и проверка единого входа Azure AD в Tidemark с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3228f-138">In this section, you configure and test Azure AD single sign-on with Tidemark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3228f-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Tidemark является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3228f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tidemark is tooa user in Azure AD.</span></span> <span data-ttu-id="3228f-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Tidemark должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="3228f-140">In other words, a link relationship between an Azure AD user and hello related user in Tidemark needs toobe established.</span></span>

<span data-ttu-id="3228f-141">В Tidemark, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="3228f-141">In Tidemark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3228f-142">tooconfigure и теста Azure AD единого входа с Tidemark, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="3228f-142">tooconfigure and test Azure AD single sign-on with Tidemark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3228f-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="3228f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3228f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="3228f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3228f-145">**[Создание тестового пользователя Tidemark](#creating-a-tidemark-test-user)**  -toohave аналог Саймон Britta в Tidemark, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="3228f-145">**[Creating a Tidemark test user](#creating-a-tidemark-test-user)** - toohave a counterpart of Britta Simon in Tidemark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3228f-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="3228f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3228f-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3228f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3228f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3228f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3228f-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Tidemark.</span><span class="sxs-lookup"><span data-stu-id="3228f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tidemark application.</span></span>

<span data-ttu-id="3228f-150">**tooconfigure Azure AD единого входа с Tidemark, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3228f-150">**tooconfigure Azure AD single sign-on with Tidemark, perform hello following steps:**</span></span>

1. <span data-ttu-id="3228f-151">В hello в hello портала Azure **Tidemark** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3228f-151">In hello Azure portal, on hello **Tidemark** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3228f-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="3228f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_samlbase.png)

3. <span data-ttu-id="3228f-155">На hello **URL-адреса и домена Tidemark** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3228f-155">On hello **Tidemark Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_url.png)

    <span data-ttu-id="3228f-157">а.</span><span class="sxs-lookup"><span data-stu-id="3228f-157">a.</span></span> <span data-ttu-id="3228f-158">В hello **URL-адрес входа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="3228f-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/login` |
    | `https://<subdomain>.tidemark.net/login` |

    <span data-ttu-id="3228f-159">b.</span><span class="sxs-lookup"><span data-stu-id="3228f-159">b.</span></span> <span data-ttu-id="3228f-160">В hello **идентификатор** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="3228f-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/saml` |
    | `https://<subdomain>.tidemark.net/saml` |

    > [!NOTE] 
    > <span data-ttu-id="3228f-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3228f-161">These values are not real.</span></span> <span data-ttu-id="3228f-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="3228f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3228f-163">Обратитесь к [группа поддержки клиента Tidemark](http://www.tidemark.com/contact-us) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="3228f-163">Contact [Tidemark Client support team](http://www.tidemark.com/contact-us) tooget these values.</span></span> 
 
4. <span data-ttu-id="3228f-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="3228f-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_certificate.png) 

5. <span data-ttu-id="3228f-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3228f-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3228f-168">На hello **конфигурации Tidemark** щелкните **Настройка Tidemark** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="3228f-168">On hello **Tidemark Configuration** section, click **Configure Tidemark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3228f-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="3228f-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_configure.png) 

7. <span data-ttu-id="3228f-171">tooconfigure единого входа на **Tidemark** стороны, необходимо загрузить hello toosend **Certificate(Base64), идентификатор сущности SAML, URL-адрес выхода и SAML единого входа URL-адрес службы** слишком[Tidemark поддержки](http://www.tidemark.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="3228f-171">tooconfigure single sign-on on **Tidemark** side, you need toosend hello downloaded **Certificate(Base64), SAML Entity ID, Sign-Out URL and SAML Single Sign-On Service URL** too[Tidemark support team](http://www.tidemark.com/contact-us).</span></span> <span data-ttu-id="3228f-172">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="3228f-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3228f-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="3228f-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3228f-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="3228f-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3228f-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3228f-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3228f-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3228f-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="3228f-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3228f-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3228f-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3228f-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3228f-180">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3228f-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3228f-182">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="3228f-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3228f-184">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="3228f-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3228f-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3228f-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3228f-188">а.</span><span class="sxs-lookup"><span data-stu-id="3228f-188">a.</span></span> <span data-ttu-id="3228f-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3228f-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3228f-190">b.</span><span class="sxs-lookup"><span data-stu-id="3228f-190">b.</span></span> <span data-ttu-id="3228f-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3228f-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3228f-192">c.</span><span class="sxs-lookup"><span data-stu-id="3228f-192">c.</span></span> <span data-ttu-id="3228f-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="3228f-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3228f-194">d.</span><span class="sxs-lookup"><span data-stu-id="3228f-194">d.</span></span> <span data-ttu-id="3228f-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3228f-195">Click **Create**.</span></span>
 
### <a name="creating-a-tidemark-test-user"></a><span data-ttu-id="3228f-196">Создание тестового пользователя Tidemark</span><span class="sxs-lookup"><span data-stu-id="3228f-196">Creating a Tidemark test user</span></span>

<span data-ttu-id="3228f-197">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Tidemark.</span><span class="sxs-lookup"><span data-stu-id="3228f-197">hello objective of this section is toocreate a user called Britta Simon in Tidemark.</span></span> <span data-ttu-id="3228f-198">Можно работать с [Tidemark поддержки](http://www.tidemark.com/contact-us) tooadd пользователей hello в hello Tidemark учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3228f-198">Please work with [Tidemark support team](http://www.tidemark.com/contact-us) tooadd hello users in hello Tidemark account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3228f-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="3228f-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3228f-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooTidemark доступа.</span><span class="sxs-lookup"><span data-stu-id="3228f-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTidemark.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3228f-202">**tooassign tooTidemark Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3228f-202">**tooassign Britta Simon tooTidemark, perform hello following steps:**</span></span>

1. <span data-ttu-id="3228f-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3228f-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3228f-205">В списке приложений hello выберите **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="3228f-205">In hello applications list, select **Tidemark**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_app.png) 

3. <span data-ttu-id="3228f-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="3228f-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3228f-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3228f-209">Click **Add** button.</span></span> <span data-ttu-id="3228f-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3228f-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3228f-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3228f-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3228f-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3228f-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3228f-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3228f-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3228f-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3228f-215">Testing single sign-on</span></span>

<span data-ttu-id="3228f-216">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="3228f-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3228f-217">При нажатии кнопки hello Tidemark плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Tidemark приложения.</span><span class="sxs-lookup"><span data-stu-id="3228f-217">When you click hello Tidemark tile in hello Access Panel, you should get automatically signed-on tooyour Tidemark application.</span></span>
<span data-ttu-id="3228f-218">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3228f-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3228f-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3228f-219">Additional resources</span></span>

* [<span data-ttu-id="3228f-220">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3228f-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3228f-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3228f-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_203.png

