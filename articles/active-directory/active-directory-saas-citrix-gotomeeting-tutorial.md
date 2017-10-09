---
title: "Руководство по интеграции Azure Active Directory с Citrix GoToMeeting | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 46a5da7504806202a5ec29f73c504e772c61bc2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="269d4-103">Учебник. Интеграция Azure Active Directory с Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="269d4-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="269d4-104">В этом учебнике вы узнаете, как toointegrate Citrix GoToMeeting с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="269d4-104">In this tutorial, you learn how toointegrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="269d4-105">Интеграция Citrix GoToMeeting с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="269d4-105">Integrating Citrix GoToMeeting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="269d4-106">Можно управлять в Azure AD, имеющего доступ tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="269d4-106">You can control in Azure AD who has access tooCitrix GoToMeeting</span></span>
- <span data-ttu-id="269d4-107">Можно включить на пользователей tooautomatically get вошедшего tooCitrix GoToMeeting (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="269d4-107">You can enable your users tooautomatically get signed-on tooCitrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="269d4-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="269d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="269d4-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="269d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="269d4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="269d4-110">Prerequisites</span></span>

<span data-ttu-id="269d4-111">tooconfigure интеграция Azure AD с Citrix GoToMeeting требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="269d4-111">tooconfigure Azure AD integration with Citrix GoToMeeting, you need hello following items:</span></span>

- <span data-ttu-id="269d4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="269d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="269d4-113">подписка Citrix GoToMeeting с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="269d4-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="269d4-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="269d4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="269d4-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="269d4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="269d4-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="269d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="269d4-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="269d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="269d4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="269d4-118">Scenario description</span></span>
<span data-ttu-id="269d4-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="269d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="269d4-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="269d4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="269d4-121">Добавление Citrix GoToMeeting из галереи hello</span><span class="sxs-lookup"><span data-stu-id="269d4-121">Adding Citrix GoToMeeting from hello gallery</span></span>
2. <span data-ttu-id="269d4-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="269d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-hello-gallery"></a><span data-ttu-id="269d4-123">Добавление Citrix GoToMeeting из галереи hello</span><span class="sxs-lookup"><span data-stu-id="269d4-123">Adding Citrix GoToMeeting from hello gallery</span></span>
<span data-ttu-id="269d4-124">tooconfigure hello интеграции Citrix GoToMeeting в Azure AD, вы должны tooadd Citrix GoToMeeting из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="269d4-124">tooconfigure hello integration of Citrix GoToMeeting into Azure AD, you need tooadd Citrix GoToMeeting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="269d4-125">**tooadd Citrix GoToMeeting из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="269d4-125">**tooadd Citrix GoToMeeting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="269d4-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="269d4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="269d4-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="269d4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="269d4-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="269d4-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="269d4-131">Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="269d4-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="269d4-133">Введите в поле поиска hello **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="269d4-133">In hello search box, type **Citrix GoToMeeting**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="269d4-135">В панели результатов hello выберите **Citrix GoToMeeting**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="269d4-135">In hello results panel, select **Citrix GoToMeeting**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="269d4-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="269d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="269d4-138">В этом разделе описана настройка и проверка единого входа Azure AD в Citrix GoToMeeting с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="269d4-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="269d4-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Citrix GoToMeeting является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="269d4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix GoToMeeting is tooa user in Azure AD.</span></span> <span data-ttu-id="269d4-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Citrix GoToMeeting должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="269d4-140">In other words, a link relationship between an Azure AD user and hello related user in Citrix GoToMeeting needs toobe established.</span></span>

<span data-ttu-id="269d4-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="269d4-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="269d4-142">tooconfigure и теста Azure AD единого входа с Citrix GoToMeeting, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="269d4-142">tooconfigure and test Azure AD single sign-on with Citrix GoToMeeting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="269d4-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="269d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="269d4-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="269d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="269d4-145">**[Создание тестового пользователя Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)**  -toohave аналог Саймон Britta в Citrix GoToMeeting, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="269d4-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - toohave a counterpart of Britta Simon in Citrix GoToMeeting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="269d4-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="269d4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="269d4-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="269d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="269d4-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="269d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="269d4-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="269d4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="269d4-150">**tooconfigure Azure AD единого входа с Citrix GoToMeeting, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="269d4-150">**tooconfigure Azure AD single sign-on with Citrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="269d4-151">В hello в hello портала Azure **Citrix GoToMeeting** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="269d4-151">In hello Azure portal, on hello **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="269d4-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="269d4-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="269d4-155">На hello **URL-адреса и домена Citrix GoToMeeting** статьи, нет необходимости tooperform никаких действий.</span><span class="sxs-lookup"><span data-stu-id="269d4-155">On hello **Citrix GoToMeeting Domain and URLs** section, no need tooperform any steps.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="269d4-157">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="269d4-157">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="269d4-159">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="269d4-159">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="269d4-161">На hello раздел конфигурации SAML Citrix GoToMeeting нажмите кнопку настроить SAML Citrix GoToMeeting tooopen Настройка единого входа окна.</span><span class="sxs-lookup"><span data-stu-id="269d4-161">On hello Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="269d4-162">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="269d4-162">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

6. <span data-ttu-id="269d4-163">В другом окне браузера войдите в tooyour [Center организации Citrix](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="269d4-163">In a different browser window, log in tooyour [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="269d4-164">Нажмите кнопку hello **поставщика удостоверений** вкладку, а затем выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="269d4-164">Click hello **Identity Provider** tab, and then perform hello following steps:</span></span>  
   
    <span data-ttu-id="269d4-165">![Настройка SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Настройка SAML")</span><span class="sxs-lookup"><span data-stu-id="269d4-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="269d4-166">а.</span><span class="sxs-lookup"><span data-stu-id="269d4-166">a.</span></span> <span data-ttu-id="269d4-167">Выберите **Вручную**</span><span class="sxs-lookup"><span data-stu-id="269d4-167">Select **Manual**</span></span>

    <span data-ttu-id="269d4-168">b.</span><span class="sxs-lookup"><span data-stu-id="269d4-168">b.</span></span> <span data-ttu-id="269d4-169">В hello в hello портала Azure **настройки единого входа в Citrix GoToMeeting** странице диалогового окна, hello копирования **SAML единого входа URL-адрес службы** значение, а затем вставьте его в hello **страницы входа URL-адрес** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="269d4-169">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="269d4-170">c.</span><span class="sxs-lookup"><span data-stu-id="269d4-170">c.</span></span> <span data-ttu-id="269d4-171">В hello в hello портала Azure **настройки единого входа в Citrix GoToMeeting** странице диалогового окна, hello копирования **URL-адрес выхода** значение, а затем вставьте его в hello **URL-адрес страницы выхода**текстового поля.</span><span class="sxs-lookup"><span data-stu-id="269d4-171">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **Sign-Out URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="269d4-172">d.</span><span class="sxs-lookup"><span data-stu-id="269d4-172">d.</span></span> <span data-ttu-id="269d4-173">В hello в hello портала Azure **настройки единого входа в Citrix GoToMeeting** странице диалогового окна, hello копирования **идентификатор сущности SAML** значение, а затем вставьте его в hello **идентификатор сущности поставщика удостоверений**  текстового поля.</span><span class="sxs-lookup"><span data-stu-id="269d4-173">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Entity ID** value, and then paste it into hello **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="269d4-174">д.</span><span class="sxs-lookup"><span data-stu-id="269d4-174">e.</span></span> <span data-ttu-id="269d4-175">tooupload загруженный сертификат, нажмите кнопку **передать сертификат**.</span><span class="sxs-lookup"><span data-stu-id="269d4-175">tooupload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="269d4-176">f.</span><span class="sxs-lookup"><span data-stu-id="269d4-176">f.</span></span> <span data-ttu-id="269d4-177">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="269d4-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="269d4-178">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="269d4-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="269d4-179">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="269d4-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="269d4-180">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="269d4-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="269d4-181">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="269d4-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="269d4-182">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="269d4-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="269d4-184">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="269d4-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="269d4-185">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="269d4-185">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="269d4-187">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="269d4-187">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="269d4-189">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="269d4-189">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="269d4-191">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="269d4-191">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="269d4-193">а.</span><span class="sxs-lookup"><span data-stu-id="269d4-193">a.</span></span> <span data-ttu-id="269d4-194">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="269d4-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="269d4-195">b.</span><span class="sxs-lookup"><span data-stu-id="269d4-195">b.</span></span> <span data-ttu-id="269d4-196">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="269d4-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="269d4-197">c.</span><span class="sxs-lookup"><span data-stu-id="269d4-197">c.</span></span> <span data-ttu-id="269d4-198">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="269d4-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="269d4-199">d.</span><span class="sxs-lookup"><span data-stu-id="269d4-199">d.</span></span> <span data-ttu-id="269d4-200">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="269d4-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="269d4-201">Создание тестового пользователя Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="269d4-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="269d4-202">В этом разделе вы создадите в Citrix GoToMeeting пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="269d4-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="269d4-203">Приложение Citrix GoToMeeting поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="269d4-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="269d4-204">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="269d4-204">There is no action item for you in this section.</span></span> <span data-ttu-id="269d4-205">Если пользователь еще не существует в Citrix GoToMeeting, создается новый, при попытке tooaccess Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="269d4-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt tooaccess Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="269d4-206">При необходимости пользователь вручную, обратитесь в службу toocreate [группа поддержки Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="269d4-206">If you need toocreate a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="269d4-207">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="269d4-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="269d4-208">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="269d4-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix GoToMeeting.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="269d4-210">**tooassign Britta Simon tooCitrix GoToMeeting, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="269d4-210">**tooassign Britta Simon tooCitrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="269d4-211">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="269d4-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="269d4-213">В списке приложений hello выберите **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="269d4-213">In hello applications list, select **Citrix GoToMeeting**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="269d4-215">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="269d4-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="269d4-217">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="269d4-217">Click **Add** button.</span></span> <span data-ttu-id="269d4-218">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="269d4-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="269d4-220">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="269d4-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="269d4-221">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="269d4-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="269d4-222">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="269d4-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="269d4-223">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="269d4-223">Testing single sign-on</span></span>

<span data-ttu-id="269d4-224">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="269d4-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="269d4-225">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="269d4-225">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="269d4-226">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="269d4-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="269d4-227">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="269d4-227">Additional resources</span></span>

* [<span data-ttu-id="269d4-228">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="269d4-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="269d4-229">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="269d4-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="269d4-230">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="269d4-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

