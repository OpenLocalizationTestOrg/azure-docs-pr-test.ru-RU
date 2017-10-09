---
title: "Руководство. Интеграция Azure Active Directory с AnswerHub | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и AnswerHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 90b530da31abe7e6f18bfa2c5409f8ff1d4f1063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="c6435-103">Руководство. Интеграция Azure Active Directory с AnswerHub</span><span class="sxs-lookup"><span data-stu-id="c6435-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="c6435-104">В этом учебнике вы узнаете, как toointegrate AnswerHub с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6435-104">In this tutorial, you learn how toointegrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c6435-105">Интеграция AnswerHub с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c6435-105">Integrating AnswerHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c6435-106">Можно управлять в Azure AD, имеющего доступ tooAnswerHub</span><span class="sxs-lookup"><span data-stu-id="c6435-106">You can control in Azure AD who has access tooAnswerHub</span></span>
- <span data-ttu-id="c6435-107">Можно включить на пользователей tooautomatically get вошедшего tooAnswerHub (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6435-107">You can enable your users tooautomatically get signed-on tooAnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c6435-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c6435-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c6435-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c6435-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6435-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c6435-110">Prerequisites</span></span>

<span data-ttu-id="c6435-111">tooconfigure интеграция Azure AD с AnswerHub требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c6435-111">tooconfigure Azure AD integration with AnswerHub, you need hello following items:</span></span>

- <span data-ttu-id="c6435-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c6435-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6435-113">подписка AnswerHub с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c6435-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c6435-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c6435-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c6435-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c6435-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6435-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c6435-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c6435-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6435-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c6435-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c6435-118">Scenario description</span></span>
<span data-ttu-id="c6435-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c6435-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c6435-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c6435-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6435-121">Добавление AnswerHub из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c6435-121">Adding AnswerHub from hello gallery</span></span>
2. <span data-ttu-id="c6435-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6435-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-hello-gallery"></a><span data-ttu-id="c6435-123">Добавление AnswerHub из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c6435-123">Adding AnswerHub from hello gallery</span></span>
<span data-ttu-id="c6435-124">tooconfigure hello интеграции AnswerHub в Azure AD, вы должны tooadd AnswerHub из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c6435-124">tooconfigure hello integration of AnswerHub into Azure AD, you need tooadd AnswerHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c6435-125">**tooadd AnswerHub из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c6435-125">**tooadd AnswerHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6435-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c6435-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c6435-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c6435-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c6435-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c6435-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c6435-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c6435-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c6435-133">Введите в поле поиска hello **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="c6435-133">In hello search box, type **AnswerHub**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="c6435-135">В панели результатов hello выберите **AnswerHub**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c6435-135">In hello results panel, select **AnswerHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c6435-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6435-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c6435-138">В этом разделе описана настройка и проверка единого входа Azure AD в AnswerHub с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c6435-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c6435-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в AnswerHub является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6435-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AnswerHub is tooa user in Azure AD.</span></span> <span data-ttu-id="c6435-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в AnswerHub должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c6435-140">In other words, a link relationship between an Azure AD user and hello related user in AnswerHub needs toobe established.</span></span>

<span data-ttu-id="c6435-141">В AnswerHub, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="c6435-141">In AnswerHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c6435-142">tooconfigure и теста Azure AD единого входа с AnswerHub, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c6435-142">tooconfigure and test Azure AD single sign-on with AnswerHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c6435-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c6435-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c6435-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c6435-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6435-145">**[Создание тестового пользователя, прошедшего AnswerHub](#creating-an-answerhub-test-user)**  -toohave аналог Саймон Britta в AnswerHub, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c6435-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - toohave a counterpart of Britta Simon in AnswerHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c6435-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c6435-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6435-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c6435-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c6435-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6435-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c6435-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в AnswerHub приложения.</span><span class="sxs-lookup"><span data-stu-id="c6435-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="c6435-150">**tooconfigure Azure AD единого входа с AnswerHub, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c6435-150">**tooconfigure Azure AD single sign-on with AnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6435-151">В hello в hello портала Azure **AnswerHub** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c6435-151">In hello Azure portal, on hello **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c6435-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c6435-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="c6435-155">На hello **URL-адреса и домена AnswerHub** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c6435-155">On hello **AnswerHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="c6435-157">а.</span><span class="sxs-lookup"><span data-stu-id="c6435-157">a.</span></span> <span data-ttu-id="c6435-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="c6435-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="c6435-159">b.</span><span class="sxs-lookup"><span data-stu-id="c6435-159">b.</span></span> <span data-ttu-id="c6435-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="c6435-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c6435-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c6435-161">These values are not real.</span></span> <span data-ttu-id="c6435-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="c6435-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c6435-163">Обратитесь к [группа поддержки клиента AnswerHub](mailto:success@answerhub.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="c6435-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="c6435-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c6435-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="c6435-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c6435-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c6435-168">На hello **конфигурации AnswerHub** щелкните **Настройка AnswerHub** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="c6435-168">On hello **AnswerHub Configuration** section, click **Configure AnswerHub** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c6435-169">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="c6435-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="c6435-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт AnswerHub в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c6435-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="c6435-172">Если вам нужна помощь в настройке AnswerHub, обратитесь в [службу поддержки AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="c6435-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="c6435-173">Go слишком**администрирования**.</span><span class="sxs-lookup"><span data-stu-id="c6435-173">Go too**Administration**.</span></span>

9. <span data-ttu-id="c6435-174">Нажмите кнопку hello **пользователей и групп** вкладки.</span><span class="sxs-lookup"><span data-stu-id="c6435-174">Click hello **User and Group** tab.</span></span>

10. <span data-ttu-id="c6435-175">В область навигации слева в hello hello hello **параметры социальных сетей** щелкните **Настройка SAML**.</span><span class="sxs-lookup"><span data-stu-id="c6435-175">In hello navigation pane on hello left side, in hello **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="c6435-176">Откройте вкладку **IDP Config** (Настройка IDP).</span><span class="sxs-lookup"><span data-stu-id="c6435-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="c6435-177">На hello **поставщика Удостоверений** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c6435-177">On hello **IDP Config** tab, perform hello following steps:</span></span>

     <span data-ttu-id="c6435-178">![Настройка SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "Настройка SAML")</span><span class="sxs-lookup"><span data-stu-id="c6435-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="c6435-179">а.</span><span class="sxs-lookup"><span data-stu-id="c6435-179">a.</span></span> <span data-ttu-id="c6435-180">В текстовое поле **IDP Login URL** (URL-адрес входа IdP) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c6435-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="c6435-181">b.</span><span class="sxs-lookup"><span data-stu-id="c6435-181">b.</span></span> <span data-ttu-id="c6435-182">В текстовое поле **IDP Logout URL** (URL-адрес выхода IdP) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c6435-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="c6435-183">c.</span><span class="sxs-lookup"><span data-stu-id="c6435-183">c.</span></span> <span data-ttu-id="c6435-184">В **формат идентификатора имени поставщика Удостоверений** в текстовое поле введите идентификатор значение таким же, что на портале Azure в пользователя hello **атрибуты пользователя** раздела.</span><span class="sxs-lookup"><span data-stu-id="c6435-184">In **IDP Name Identifier Format** textbox, enter hello user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="c6435-185">d.</span><span class="sxs-lookup"><span data-stu-id="c6435-185">d.</span></span> <span data-ttu-id="c6435-186">Щелкните **Ключи и сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="c6435-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="c6435-187">Вкладки hello ключи и сертификаты выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c6435-187">On hello Keys and Certificates tab, perform hello following steps:</span></span>
    
     <span data-ttu-id="c6435-188">![Ключи и сертификаты](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Ключи и сертификаты")</span><span class="sxs-lookup"><span data-stu-id="c6435-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="c6435-189">а.</span><span class="sxs-lookup"><span data-stu-id="c6435-189">a.</span></span> <span data-ttu-id="c6435-190">Откройте сертификат в кодировке base-64 которой загруженный с портала Azure в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **открытый ключ поставщика Удостоверений (в формате x 509)** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="c6435-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="c6435-191">b.</span><span class="sxs-lookup"><span data-stu-id="c6435-191">b.</span></span> <span data-ttu-id="c6435-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c6435-192">Click **Save**.</span></span>

14. <span data-ttu-id="c6435-193">На hello **поставщика Удостоверений** щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c6435-193">On hello **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c6435-194">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c6435-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c6435-195">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c6435-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c6435-196">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c6435-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c6435-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6435-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="c6435-198">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c6435-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c6435-200">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c6435-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6435-201">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c6435-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c6435-203">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c6435-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c6435-205">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="c6435-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c6435-207">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c6435-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c6435-209">а.</span><span class="sxs-lookup"><span data-stu-id="c6435-209">a.</span></span> <span data-ttu-id="c6435-210">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c6435-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6435-211">b.</span><span class="sxs-lookup"><span data-stu-id="c6435-211">b.</span></span> <span data-ttu-id="c6435-212">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c6435-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c6435-213">c.</span><span class="sxs-lookup"><span data-stu-id="c6435-213">c.</span></span> <span data-ttu-id="c6435-214">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c6435-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c6435-215">d.</span><span class="sxs-lookup"><span data-stu-id="c6435-215">d.</span></span> <span data-ttu-id="c6435-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c6435-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="c6435-217">Создание тестового пользователя AnswerHub</span><span class="sxs-lookup"><span data-stu-id="c6435-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="c6435-218">Пользователи toolog tooenable Azure AD в tooAnswerHub, их необходимо подготовить в AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="c6435-218">tooenable Azure AD users toolog in tooAnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="c6435-219">В случае AnswerHub hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="c6435-219">In hello case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="c6435-220">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c6435-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6435-221">Войдите в tooyour **AnswerHub** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="c6435-221">Log in tooyour **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="c6435-222">Go слишком**администрирования**.</span><span class="sxs-lookup"><span data-stu-id="c6435-222">Go too**Administration**.</span></span>

3. <span data-ttu-id="c6435-223">Нажмите кнопку hello **пользователи и группы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="c6435-223">Click hello **Users & Groups** tab.</span></span>

4. <span data-ttu-id="c6435-224">В область навигации слева в hello hello hello **Управление пользователями** щелкните **создать или импортировать пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c6435-224">In hello navigation pane on hello left side, in hello **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="c6435-225">![Пользователи и группы](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Пользователи и группы")</span><span class="sxs-lookup"><span data-stu-id="c6435-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="c6435-226">Тип hello **адрес электронной почты**, **Username** и **пароль** допустимым Azure учетной записи Active Directory, которые должны tooprovision hello связанные текстовые поля и нажмите кнопку  **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c6435-226">Type hello **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want tooprovision into hello related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="c6435-227">Можно использовать любые другие AnswerHub пользователя средства создания учетных записей или интерфейсы API, предоставляемые AnswerHub tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="c6435-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c6435-228">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c6435-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c6435-229">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAnswerHub доступа.</span><span class="sxs-lookup"><span data-stu-id="c6435-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnswerHub.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c6435-231">**tooassign tooAnswerHub Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c6435-231">**tooassign Britta Simon tooAnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6435-232">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c6435-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c6435-234">В списке приложений hello выберите **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="c6435-234">In hello applications list, select **AnswerHub**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="c6435-236">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c6435-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c6435-238">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c6435-238">Click **Add** button.</span></span> <span data-ttu-id="c6435-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c6435-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c6435-241">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c6435-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c6435-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c6435-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c6435-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c6435-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c6435-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c6435-244">Testing single sign-on</span></span>

<span data-ttu-id="c6435-245">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c6435-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c6435-246">При нажатии кнопки hello AnswerHub плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour AnswerHub приложения.</span><span class="sxs-lookup"><span data-stu-id="c6435-246">When you click hello AnswerHub tile in hello Access Panel, you should get automatically signed-on tooyour AnswerHub application.</span></span>
<span data-ttu-id="c6435-247">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c6435-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c6435-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c6435-248">Additional resources</span></span>

* [<span data-ttu-id="c6435-249">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6435-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6435-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c6435-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

