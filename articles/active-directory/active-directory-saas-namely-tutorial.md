---
title: "Руководство по интеграции Azure Active Directory с Namely | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и т."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="49c9c-103">Руководство по интеграции Azure Active Directory с Namely</span><span class="sxs-lookup"><span data-stu-id="49c9c-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="49c9c-104">В этом учебнике вы узнаете, как toointegrate, а именно с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49c9c-104">In this tutorial, you learn how toointegrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49c9c-105">А именно: интеграция с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="49c9c-105">Integrating Namely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="49c9c-106">Можно управлять в Azure AD, имеющего доступ tooNamely</span><span class="sxs-lookup"><span data-stu-id="49c9c-106">You can control in Azure AD who has access tooNamely</span></span>
- <span data-ttu-id="49c9c-107">Можно включить на пользователей tooautomatically get вошедшего tooNamely (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c9c-107">You can enable your users tooautomatically get signed-on tooNamely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="49c9c-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="49c9c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="49c9c-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49c9c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49c9c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="49c9c-110">Prerequisites</span></span>

<span data-ttu-id="49c9c-111">Интеграция tooconfigure Azure AD, вам требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="49c9c-111">tooconfigure Azure AD integration with Namely, you need hello following items:</span></span>

- <span data-ttu-id="49c9c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="49c9c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49c9c-113">подписка Namely с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="49c9c-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="49c9c-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="49c9c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="49c9c-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="49c9c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49c9c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="49c9c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="49c9c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49c9c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49c9c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="49c9c-118">Scenario description</span></span>
<span data-ttu-id="49c9c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="49c9c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49c9c-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="49c9c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49c9c-121">А именно: Добавление из галереи hello</span><span class="sxs-lookup"><span data-stu-id="49c9c-121">Adding Namely from hello gallery</span></span>
2. <span data-ttu-id="49c9c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c9c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-hello-gallery"></a><span data-ttu-id="49c9c-123">А именно: Добавление из галереи hello</span><span class="sxs-lookup"><span data-stu-id="49c9c-123">Adding Namely from hello gallery</span></span>
<span data-ttu-id="49c9c-124">tooconfigure hello интеграции а именно в Azure AD, вы должны tooadd, а именно из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="49c9c-124">tooconfigure hello integration of Namely into Azure AD, you need tooadd Namely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="49c9c-125">**tooadd, а именно из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="49c9c-125">**tooadd Namely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c9c-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="49c9c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="49c9c-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="49c9c-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="49c9c-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="49c9c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="49c9c-133">Введите в поле поиска hello **а именно**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-133">In hello search box, type **Namely**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="49c9c-135">В панели результатов hello выберите **а именно**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="49c9c-135">In hello results panel, select **Namely**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="49c9c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c9c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="49c9c-138">В этом разделе описаны настройка и проверка единого входа Azure AD в приложение Namely с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49c9c-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="49c9c-139">Для единого входа toowork Azure AD необходима tooknow какие hello аналога в а именно он tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49c9c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Namely is tooa user in Azure AD.</span></span> <span data-ttu-id="49c9c-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в а именно должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="49c9c-140">In other words, a link relationship between an Azure AD user and hello related user in Namely needs toobe established.</span></span>

<span data-ttu-id="49c9c-141">В а именно, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="49c9c-141">In Namely, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="49c9c-142">tooconfigure и тестирования Azure AD единого входа, а именно, вам требуется hello toocomplete следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="49c9c-142">tooconfigure and test Azure AD single sign-on with Namely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="49c9c-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="49c9c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="49c9c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="49c9c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49c9c-145">**[Создание а именно тестовый пользователь](#creating-a-namely-test-user)**  -toohave квантор Саймон Britta, в т. то есть связанного toohello представление пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49c9c-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - toohave a counterpart of Britta Simon in Namely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="49c9c-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="49c9c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49c9c-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="49c9c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="49c9c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c9c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="49c9c-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в а именно приложение.</span><span class="sxs-lookup"><span data-stu-id="49c9c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="49c9c-150">**tooconfigure Azure AD единого входа с а именно, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="49c9c-150">**tooconfigure Azure AD single sign-on with Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c9c-151">В hello в hello портала Azure **а именно** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-151">In hello Azure portal, on hello **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="49c9c-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="49c9c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="49c9c-155">На hello **URL-адреса и домена а именно** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="49c9c-155">On hello **Namely Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="49c9c-157">а.</span><span class="sxs-lookup"><span data-stu-id="49c9c-157">a.</span></span> <span data-ttu-id="49c9c-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="49c9c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="49c9c-159">b.</span><span class="sxs-lookup"><span data-stu-id="49c9c-159">b.</span></span> <span data-ttu-id="49c9c-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="49c9c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="49c9c-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="49c9c-161">These values are not real.</span></span> <span data-ttu-id="49c9c-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="49c9c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="49c9c-163">Обратитесь к [группа поддержки а именно клиент](https://www.namely.com/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="49c9c-163">Contact [Namely Client support team](https://www.namely.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="49c9c-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="49c9c-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="49c9c-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="49c9c-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="49c9c-168">На hello **а именно конфигурации** щелкните **Настройка а именно** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="49c9c-168">On hello **Namely Configuration** section, click **Configure Namely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="49c9c-169">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="49c9c-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="49c9c-171">В другом окне браузера Войдите на tooyour а именно на сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="49c9c-171">In another browser window, sign on tooyour Namely company site as an administrator.</span></span>

8. <span data-ttu-id="49c9c-172">Щелкните hello панели инструментов в верхней части hello **компании**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-172">In hello toolbar on hello top, click **Company**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="49c9c-174">Нажмите кнопку hello **параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="49c9c-174">Click hello **Settings** tab.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="49c9c-176">Нажмите кнопку **SAML**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-176">Click **SAML**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="49c9c-178">На hello **параметры SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="49c9c-178">On hello **SAML Settings** page, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="49c9c-180">а.</span><span class="sxs-lookup"><span data-stu-id="49c9c-180">a.</span></span> <span data-ttu-id="49c9c-181">Выберите команду **Enable SAML**(Включить SAML).</span><span class="sxs-lookup"><span data-stu-id="49c9c-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="49c9c-182">b.</span><span class="sxs-lookup"><span data-stu-id="49c9c-182">b.</span></span> <span data-ttu-id="49c9c-183">В hello **URL-адрес единого входа поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="49c9c-183">In hello **Identity provider SSO url** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="49c9c-184">c.</span><span class="sxs-lookup"><span data-stu-id="49c9c-184">c.</span></span> <span data-ttu-id="49c9c-185">Откройте загруженный сертификат в блокноте, hello копирования содержимого, а затем вставьте его в hello **сертификат поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="49c9c-185">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="49c9c-186">d.</span><span class="sxs-lookup"><span data-stu-id="49c9c-186">d.</span></span> <span data-ttu-id="49c9c-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="49c9c-188">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="49c9c-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="49c9c-189">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="49c9c-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="49c9c-190">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="49c9c-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="49c9c-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c9c-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="49c9c-192">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="49c9c-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="49c9c-194">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="49c9c-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c9c-195">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="49c9c-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49c9c-197">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49c9c-199">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="49c9c-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49c9c-201">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="49c9c-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49c9c-203">а.</span><span class="sxs-lookup"><span data-stu-id="49c9c-203">a.</span></span> <span data-ttu-id="49c9c-204">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="49c9c-205">b.</span><span class="sxs-lookup"><span data-stu-id="49c9c-205">b.</span></span> <span data-ttu-id="49c9c-206">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="49c9c-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="49c9c-207">c.</span><span class="sxs-lookup"><span data-stu-id="49c9c-207">c.</span></span> <span data-ttu-id="49c9c-208">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="49c9c-209">d.</span><span class="sxs-lookup"><span data-stu-id="49c9c-209">d.</span></span> <span data-ttu-id="49c9c-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="49c9c-211">Создание тестового пользователя Namely</span><span class="sxs-lookup"><span data-stu-id="49c9c-211">Creating a Namely test user</span></span>

<span data-ttu-id="49c9c-212">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon, а именно.</span><span class="sxs-lookup"><span data-stu-id="49c9c-212">hello objective of this section is toocreate a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="49c9c-213">**toocreate пользователя с именем Britta Simon, а именно, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="49c9c-213">**toocreate a user called Britta Simon in Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c9c-214">А именно tooyour входа компании сайта от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="49c9c-214">Sign-on tooyour Namely company site as an administrator.</span></span>

2. <span data-ttu-id="49c9c-215">Щелкните hello панели инструментов в верхней части hello **людей**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-215">In hello toolbar on hello top, click **People**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="49c9c-217">Нажмите кнопку hello **каталога** вкладки.</span><span class="sxs-lookup"><span data-stu-id="49c9c-217">Click hello **Directory** tab.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="49c9c-219">Щелкните **Add New Person**(Добавить нового пользователя).</span><span class="sxs-lookup"><span data-stu-id="49c9c-219">Click **Add New Person**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="49c9c-221">На hello **Добавление нового человека** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="49c9c-221">On hello **Add New Person** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="49c9c-222">а.</span><span class="sxs-lookup"><span data-stu-id="49c9c-222">a.</span></span> <span data-ttu-id="49c9c-223">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-223">In hello **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="49c9c-224">b.</span><span class="sxs-lookup"><span data-stu-id="49c9c-224">b.</span></span> <span data-ttu-id="49c9c-225">В hello **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-225">In hello **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="49c9c-226">c.</span><span class="sxs-lookup"><span data-stu-id="49c9c-226">c.</span></span> <span data-ttu-id="49c9c-227">В hello **электронной почты** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="49c9c-227">In hello **Email** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="49c9c-228">d.</span><span class="sxs-lookup"><span data-stu-id="49c9c-228">d.</span></span> <span data-ttu-id="49c9c-229">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-229">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="49c9c-230">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="49c9c-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="49c9c-231">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooNamely доступа.</span><span class="sxs-lookup"><span data-stu-id="49c9c-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNamely.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="49c9c-233">**tooassign tooNamely Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="49c9c-233">**tooassign Britta Simon tooNamely, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c9c-234">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="49c9c-236">В списке приложений hello выберите **а именно**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-236">In hello applications list, select **Namely**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="49c9c-238">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="49c9c-240">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-240">Click **Add** button.</span></span> <span data-ttu-id="49c9c-241">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="49c9c-243">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="49c9c-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="49c9c-244">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49c9c-245">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="49c9c-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="49c9c-246">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="49c9c-246">Testing single sign-on</span></span>

<span data-ttu-id="49c9c-247">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="49c9c-247">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="49c9c-248">При нажатии кнопки hello а именно плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour а именно приложение</span><span class="sxs-lookup"><span data-stu-id="49c9c-248">When you click hello Namely tile in hello Access Panel, you should get automatically signed-on tooyour Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49c9c-249">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="49c9c-249">Additional resources</span></span>

* [<span data-ttu-id="49c9c-250">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49c9c-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49c9c-251">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49c9c-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

