---
title: "Руководство по интеграции Azure Active Directory с Jive | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: f22bf78a55e8a4a9ea2f0020ef2f535be88b6302
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="37f17-103">Руководство. Интеграция Azure Active Directory с Jive</span><span class="sxs-lookup"><span data-stu-id="37f17-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="37f17-104">В этом учебнике вы узнаете, как toointegrate Jive с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37f17-104">In this tutorial, you learn how toointegrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37f17-105">Интеграция с Azure AD Jive предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="37f17-105">Integrating Jive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="37f17-106">Можно управлять в Azure AD, имеющего доступ tooJive</span><span class="sxs-lookup"><span data-stu-id="37f17-106">You can control in Azure AD who has access tooJive</span></span>
- <span data-ttu-id="37f17-107">Можно включить на пользователей tooautomatically get вошедшего tooJive (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f17-107">You can enable your users tooautomatically get signed-on tooJive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37f17-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="37f17-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="37f17-109">Если требуется tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. раздел [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37f17-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37f17-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="37f17-110">Prerequisites</span></span>

<span data-ttu-id="37f17-111">tooconfigure интеграция Azure AD с Jive требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="37f17-111">tooconfigure Azure AD integration with Jive, you need hello following items:</span></span>

- <span data-ttu-id="37f17-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="37f17-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37f17-113">подписка Jive с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="37f17-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37f17-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="37f17-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37f17-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="37f17-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37f17-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="37f17-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37f17-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37f17-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37f17-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="37f17-118">Scenario description</span></span>
<span data-ttu-id="37f17-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="37f17-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37f17-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="37f17-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37f17-121">Добавление Jive из галереи hello</span><span class="sxs-lookup"><span data-stu-id="37f17-121">Adding Jive from hello gallery</span></span>
2. <span data-ttu-id="37f17-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f17-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-hello-gallery"></a><span data-ttu-id="37f17-123">Добавление Jive из галереи hello</span><span class="sxs-lookup"><span data-stu-id="37f17-123">Adding Jive from hello gallery</span></span>
<span data-ttu-id="37f17-124">интеграции hello tooconfigure Jive в Azure AD, вы должны tooadd Jive из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="37f17-124">tooconfigure hello integration of Jive into Azure AD, you need tooadd Jive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="37f17-125">**tooadd Jive из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="37f17-125">**tooadd Jive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="37f17-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="37f17-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="37f17-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="37f17-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="37f17-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="37f17-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="37f17-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="37f17-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="37f17-133">Введите в поле поиска hello **Jive**.</span><span class="sxs-lookup"><span data-stu-id="37f17-133">In hello search box, type **Jive**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="37f17-135">В панели результатов hello выберите **Jive**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="37f17-135">In hello results panel, select **Jive**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37f17-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f17-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37f17-138">В этом разделе описана настройка и проверка единого входа Azure AD в Jive с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37f17-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="37f17-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Jive является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37f17-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jive is tooa user in Azure AD.</span></span> <span data-ttu-id="37f17-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Jive должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="37f17-140">In other words, a link relationship between an Azure AD user and hello related user in Jive needs toobe established.</span></span>

<span data-ttu-id="37f17-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Jive.</span><span class="sxs-lookup"><span data-stu-id="37f17-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Jive.</span></span>

<span data-ttu-id="37f17-142">tooconfigure и теста Azure AD единого входа с Jive, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="37f17-142">tooconfigure and test Azure AD single sign-on with Jive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="37f17-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="37f17-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="37f17-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="37f17-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37f17-145">**[Создание тестового пользователя Jive](#creating-a-jive-test-user)**  -toohave аналог Саймон Britta в Jive, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="37f17-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - toohave a counterpart of Britta Simon in Jive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="37f17-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="37f17-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37f17-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="37f17-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37f17-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f17-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="37f17-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Jive.</span><span class="sxs-lookup"><span data-stu-id="37f17-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="37f17-150">**tooconfigure Azure AD единого входа с Jive, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="37f17-150">**tooconfigure Azure AD single sign-on with Jive, perform hello following steps:**</span></span>

1. <span data-ttu-id="37f17-151">В hello в hello портала Azure **Jive** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="37f17-151">In hello Azure portal, on hello **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="37f17-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="37f17-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="37f17-155">На hello **URL-адреса и домена Jive** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="37f17-155">On hello **Jive Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="37f17-157">а.</span><span class="sxs-lookup"><span data-stu-id="37f17-157">a.</span></span> <span data-ttu-id="37f17-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="37f17-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="37f17-159">b.</span><span class="sxs-lookup"><span data-stu-id="37f17-159">b.</span></span> <span data-ttu-id="37f17-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="37f17-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37f17-161">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="37f17-161">These values are not hello real.</span></span> <span data-ttu-id="37f17-162">Обновите эти значения с hello фактический URL-адрес входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="37f17-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="37f17-163">Обратитесь к [группа поддержки клиента Jive](https://www.jivesoftware.com/services-support/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="37f17-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="37f17-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="37f17-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="37f17-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="37f17-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="37f17-168">tooconfigure единого входа на **Jive** клиента Jive tooyour параллельно, вход от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="37f17-168">tooconfigure single sign-on on **Jive** side, sign-on tooyour Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="37f17-169">В меню hello hello верхней части страницы, нажмите кнопку "**Saml**.»</span><span class="sxs-lookup"><span data-stu-id="37f17-169">In hello menu on hello top, Click "**Saml**."</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="37f17-171">а.</span><span class="sxs-lookup"><span data-stu-id="37f17-171">a.</span></span> <span data-ttu-id="37f17-172">Выберите **включено** под hello **Общие** вкладки.</span><span class="sxs-lookup"><span data-stu-id="37f17-172">Select **Enabled** under hello **General** tab.</span></span>   
    <span data-ttu-id="37f17-173">b.</span><span class="sxs-lookup"><span data-stu-id="37f17-173">b.</span></span> <span data-ttu-id="37f17-174">Нажмите кнопку hello»**сохранить все параметры saml**» кнопки.</span><span class="sxs-lookup"><span data-stu-id="37f17-174">Click hello "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="37f17-175">Перейдите toohello "**метаданные поставщика удостоверений**» вкладки.</span><span class="sxs-lookup"><span data-stu-id="37f17-175">Navigate toohello "**Idp Metadata**" tab.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="37f17-177">а.</span><span class="sxs-lookup"><span data-stu-id="37f17-177">a.</span></span> <span data-ttu-id="37f17-178">Скопируйте содержимое XML-файл метаданных hello загружаются hello, а затем вставьте его в hello **метаданных поставщика удостоверений (IDP)** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="37f17-178">Copy hello content of hello downloaded metadata XML file, and then paste it into hello **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="37f17-179">b.</span><span class="sxs-lookup"><span data-stu-id="37f17-179">b.</span></span> <span data-ttu-id="37f17-180">Нажмите кнопку hello»**сохранить все параметры saml**» кнопки.</span><span class="sxs-lookup"><span data-stu-id="37f17-180">Click hello "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="37f17-181">Go toohello "**сопоставления атрибута**» вкладки.</span><span class="sxs-lookup"><span data-stu-id="37f17-181">Go toohello "**User Attribute Mapping**" tab.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="37f17-183">а.</span><span class="sxs-lookup"><span data-stu-id="37f17-183">a.</span></span> <span data-ttu-id="37f17-184">В hello **электронной почты** текстовое поле, копировать и вставить hello имя **mail** значение.</span><span class="sxs-lookup"><span data-stu-id="37f17-184">In hello **Email** textbox, copy and paste hello attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="37f17-185">b.</span><span class="sxs-lookup"><span data-stu-id="37f17-185">b.</span></span> <span data-ttu-id="37f17-186">В hello **имя** текстовое поле, копировать и вставить hello имя **givenname** значение.</span><span class="sxs-lookup"><span data-stu-id="37f17-186">In hello **First Name** textbox, copy and paste hello attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="37f17-187">c.</span><span class="sxs-lookup"><span data-stu-id="37f17-187">c.</span></span> <span data-ttu-id="37f17-188">В hello **Фамилия** текстовое поле, копировать и вставить hello имя **Фамилия** значение.</span><span class="sxs-lookup"><span data-stu-id="37f17-188">In hello **Last Name** textbox, copy and paste hello attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="37f17-189">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="37f17-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="37f17-190">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="37f17-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="37f17-191">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37f17-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37f17-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f17-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="37f17-193">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="37f17-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="37f17-195">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="37f17-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="37f17-196">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="37f17-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37f17-198">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="37f17-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37f17-200">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="37f17-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37f17-202">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="37f17-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37f17-204">а.</span><span class="sxs-lookup"><span data-stu-id="37f17-204">a.</span></span> <span data-ttu-id="37f17-205">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37f17-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37f17-206">b.</span><span class="sxs-lookup"><span data-stu-id="37f17-206">b.</span></span> <span data-ttu-id="37f17-207">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37f17-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37f17-208">c.</span><span class="sxs-lookup"><span data-stu-id="37f17-208">c.</span></span> <span data-ttu-id="37f17-209">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="37f17-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="37f17-210">d.</span><span class="sxs-lookup"><span data-stu-id="37f17-210">d.</span></span> <span data-ttu-id="37f17-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="37f17-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="37f17-212">Создание тестового пользователя приложения Jive</span><span class="sxs-lookup"><span data-stu-id="37f17-212">Creating a Jive test user</span></span>

<span data-ttu-id="37f17-213">Работать с [группа поддержки клиента Jive](https://www.jivesoftware.com/services-support/) tooadd hello пользователей на платформе Jive hello.</span><span class="sxs-lookup"><span data-stu-id="37f17-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) tooadd hello users in hello Jive platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="37f17-214">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="37f17-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="37f17-215">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooJive доступа.</span><span class="sxs-lookup"><span data-stu-id="37f17-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJive.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="37f17-217">**tooassign tooJive Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="37f17-217">**tooassign Britta Simon tooJive, perform hello following steps:**</span></span>

1. <span data-ttu-id="37f17-218">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="37f17-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="37f17-220">В списке приложений hello выберите **Jive**.</span><span class="sxs-lookup"><span data-stu-id="37f17-220">In hello applications list, select **Jive**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="37f17-222">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="37f17-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="37f17-224">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="37f17-224">Click **Add** button.</span></span> <span data-ttu-id="37f17-225">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="37f17-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="37f17-227">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="37f17-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="37f17-228">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="37f17-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37f17-229">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="37f17-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="37f17-230">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="37f17-230">Testing single sign-on</span></span>

<span data-ttu-id="37f17-231">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="37f17-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="37f17-232">При нажатии кнопки hello Jive плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour Jive.</span><span class="sxs-lookup"><span data-stu-id="37f17-232">When you click hello Jive tile in hello Access Panel, you should get automatically signed-on tooyour Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37f17-233">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="37f17-233">Additional resources</span></span>

* [<span data-ttu-id="37f17-234">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37f17-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37f17-235">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37f17-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="37f17-236">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="37f17-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

