---
title: "Руководство по интеграции Azure Active Directory с Overdrive | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Overdrive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e68cede7-1130-4813-bd55-22a9a6fc6bf5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0aafacdedee25587132fc88ff93829f4367b0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-overdrive"></a><span data-ttu-id="26cfe-103">Руководство по интеграции Azure Active Directory с Overdrive</span><span class="sxs-lookup"><span data-stu-id="26cfe-103">Tutorial: Azure Active Directory integration with Overdrive</span></span> 

<span data-ttu-id="26cfe-104">В этом учебнике вы узнаете, как toointegrate Overdrive с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26cfe-104">In this tutorial, you learn how toointegrate Overdrive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26cfe-105">Интеграция Overdrive с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="26cfe-105">Integrating Overdrive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="26cfe-106">Можно управлять в Azure AD, имеющего доступ tooOverdrive</span><span class="sxs-lookup"><span data-stu-id="26cfe-106">You can control in Azure AD who has access tooOverdrive</span></span> 
- <span data-ttu-id="26cfe-107">Можно включить на пользователей tooautomatically get вошедшего tooOverdrive (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="26cfe-107">You can enable your users tooautomatically get signed-on tooOverdrive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="26cfe-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="26cfe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="26cfe-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26cfe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26cfe-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="26cfe-110">Prerequisites</span></span>

<span data-ttu-id="26cfe-111">tooconfigure интеграция Azure AD с Overdrive требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="26cfe-111">tooconfigure Azure AD integration with Overdrive, you need hello following items:</span></span>

- <span data-ttu-id="26cfe-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="26cfe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26cfe-113">подписка Overdrive с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="26cfe-113">An Overdrive single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26cfe-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="26cfe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26cfe-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="26cfe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26cfe-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="26cfe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26cfe-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26cfe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26cfe-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="26cfe-118">Scenario description</span></span>
<span data-ttu-id="26cfe-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="26cfe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26cfe-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="26cfe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26cfe-121">Добавление Overdrive из галереи hello</span><span class="sxs-lookup"><span data-stu-id="26cfe-121">Adding Overdrive from hello gallery</span></span>
2. <span data-ttu-id="26cfe-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="26cfe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-overdrive-from-hello-gallery"></a><span data-ttu-id="26cfe-123">Добавление Overdrive из галереи hello</span><span class="sxs-lookup"><span data-stu-id="26cfe-123">Adding Overdrive from hello gallery</span></span>
<span data-ttu-id="26cfe-124">интеграции hello tooconfigure Overdrive в Azure AD, вы должны tooadd Overdrive из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="26cfe-124">tooconfigure hello integration of Overdrive into Azure AD, you need tooadd Overdrive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="26cfe-125">**tooadd Overdrive из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="26cfe-125">**tooadd Overdrive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="26cfe-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="26cfe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="26cfe-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="26cfe-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="26cfe-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="26cfe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="26cfe-133">Введите в поле поиска hello **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-133">In hello search box, type **Overdrive**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_search.png)

5. <span data-ttu-id="26cfe-135">В панели результатов hello выберите **Overdrive**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="26cfe-135">In hello results panel, select **Overdrive**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="26cfe-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="26cfe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="26cfe-138">В этом разделе описаны настройка и проверка единого входа Azure AD в приложение Overdrive с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26cfe-138">In this section, you configure and test Azure AD single sign-on with Overdrive based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26cfe-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Overdrive является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26cfe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Overdrive is tooa user in Azure AD.</span></span> <span data-ttu-id="26cfe-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Overdrive должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="26cfe-140">In other words, a link relationship between an Azure AD user and hello related user in Overdrive needs toobe established.</span></span>

<span data-ttu-id="26cfe-141">В Overdrive, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="26cfe-141">In Overdrive, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="26cfe-142">tooconfigure и теста Azure AD единого входа с Overdrive, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="26cfe-142">tooconfigure and test Azure AD single sign-on with Overdrive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="26cfe-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="26cfe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="26cfe-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="26cfe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26cfe-145">**[Создание тестового пользователя, прошедшего Overdrive](#creating-an-overdrive-test-user)**  -toohave аналог Саймон Britta в Overdrive, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="26cfe-145">**[Creating an Overdrive test user](#creating-an-overdrive-test-user)** - toohave a counterpart of Britta Simon in Overdrive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="26cfe-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="26cfe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26cfe-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="26cfe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="26cfe-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="26cfe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="26cfe-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Overdrive.</span><span class="sxs-lookup"><span data-stu-id="26cfe-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Overdrive  application.</span></span>

<span data-ttu-id="26cfe-150">**Azure AD tooconfigure единого входа с Overdrive, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="26cfe-150">**tooconfigure Azure AD single sign-on with Overdrive, perform hello following steps:**</span></span>

1. <span data-ttu-id="26cfe-151">В hello в hello портала Azure **Overdrive** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-151">In hello Azure portal, on hello **Overdrive** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="26cfe-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="26cfe-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_samlbase.png)

3. <span data-ttu-id="26cfe-155">На hello **URL-адреса и домена Overdrive** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="26cfe-155">On hello **Overdrive Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_url.png)

    <span data-ttu-id="26cfe-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://<subdomain>.libraryreserve.com`</span><span class="sxs-lookup"><span data-stu-id="26cfe-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<subdomain>.libraryreserve.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="26cfe-158">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="26cfe-158">hello value is not real.</span></span> <span data-ttu-id="26cfe-159">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="26cfe-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="26cfe-160">Обратитесь к [группа поддержки Overdrive клиента](https://help.overdrive.com/) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="26cfe-160">Contact [Overdrive Client support team](https://help.overdrive.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="26cfe-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="26cfe-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_certificate.png) 

5. <span data-ttu-id="26cfe-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="26cfe-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="26cfe-165">tooconfigure единого входа на **Overdrive** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[поддержки OverDrive](https://help.overdrive.com/).</span><span class="sxs-lookup"><span data-stu-id="26cfe-165">tooconfigure single sign-on on **Overdrive** side, you need toosend hello downloaded **Metadata XML** too[Overdrive support team](https://help.overdrive.com/).</span></span> <span data-ttu-id="26cfe-166">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="26cfe-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="26cfe-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="26cfe-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="26cfe-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="26cfe-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="26cfe-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="26cfe-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="26cfe-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="26cfe-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="26cfe-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="26cfe-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="26cfe-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="26cfe-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="26cfe-174">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="26cfe-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="26cfe-176">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="26cfe-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="26cfe-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="26cfe-180">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="26cfe-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="26cfe-182">а.</span><span class="sxs-lookup"><span data-stu-id="26cfe-182">a.</span></span> <span data-ttu-id="26cfe-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26cfe-184">b.</span><span class="sxs-lookup"><span data-stu-id="26cfe-184">b.</span></span> <span data-ttu-id="26cfe-185">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="26cfe-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="26cfe-186">c.</span><span class="sxs-lookup"><span data-stu-id="26cfe-186">c.</span></span> <span data-ttu-id="26cfe-187">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="26cfe-188">d.</span><span class="sxs-lookup"><span data-stu-id="26cfe-188">d.</span></span> <span data-ttu-id="26cfe-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-189">Click **Create**.</span></span>
 
### <a name="creating-an-overdrive-test-user"></a><span data-ttu-id="26cfe-190">Создание тестового пользователя Overdrive</span><span class="sxs-lookup"><span data-stu-id="26cfe-190">Creating an Overdrive test user</span></span>

<span data-ttu-id="26cfe-191">Нет элемента действия для вас tooconfigure подготовки пользователей tooOverDrive.</span><span class="sxs-lookup"><span data-stu-id="26cfe-191">There is no action item for you tooconfigure user provisioning tooOverDrive.</span></span>  

<span data-ttu-id="26cfe-192">Когда назначенный пользователь пытается toolog в tooOverDrive учетная запись OverDrive создается автоматически при необходимости.</span><span class="sxs-lookup"><span data-stu-id="26cfe-192">When an assigned user tries toolog in tooOverDrive, an OverDrive account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="26cfe-193">Можно использовать любые другие OverDrive пользователя средства создания учетных записей или интерфейсы API, предоставляемые OverDrive tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="26cfe-193">You can use any other OverDrive user account creation tools or APIs provided by OverDrive tooprovision AAD user accounts.</span></span>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="26cfe-194">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="26cfe-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="26cfe-195">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooOverdrive доступа.</span><span class="sxs-lookup"><span data-stu-id="26cfe-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOverdrive.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="26cfe-197">**tooassign tooOverdrive Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="26cfe-197">**tooassign Britta Simon tooOverdrive, perform hello following steps:**</span></span>

1. <span data-ttu-id="26cfe-198">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="26cfe-200">В списке приложений hello выберите **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-200">In hello applications list, select **Overdrive**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_app.png) 

3. <span data-ttu-id="26cfe-202">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="26cfe-204">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-204">Click **Add** button.</span></span> <span data-ttu-id="26cfe-205">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="26cfe-207">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="26cfe-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="26cfe-208">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26cfe-209">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="26cfe-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="26cfe-210">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="26cfe-210">Testing single sign-on</span></span>

<span data-ttu-id="26cfe-211">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="26cfe-211">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="26cfe-212">При выборе плитки Overdrive hello в hello панели доступа, следует получать автоматически вошедшего tooyour Overdrive приложения.</span><span class="sxs-lookup"><span data-stu-id="26cfe-212">When you click hello Overdrive tile in hello Access Panel, you should get automatically signed-on tooyour Overdrive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="26cfe-213">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="26cfe-213">Additional resources</span></span>

* [<span data-ttu-id="26cfe-214">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26cfe-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26cfe-215">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26cfe-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_203.png

