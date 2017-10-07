---
title: "Руководство по интеграции Azure Active Directory с Gigya | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Gigya."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 1992c5ad09b097563377a488fbf5a375f6511020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="c5c02-103">Руководство. Интеграция Azure Active Directory с Gigya</span><span class="sxs-lookup"><span data-stu-id="c5c02-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="c5c02-104">В этом учебнике вы узнаете, как toointegrate Gigya с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5c02-104">In this tutorial, you learn how toointegrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5c02-105">Интеграция Gigya с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c5c02-105">Integrating Gigya with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5c02-106">Можно управлять в Azure AD, имеющего доступ tooGigya</span><span class="sxs-lookup"><span data-stu-id="c5c02-106">You can control in Azure AD who has access tooGigya</span></span>
- <span data-ttu-id="c5c02-107">Можно включить на пользователей tooautomatically get вошедшего tooGigya (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5c02-107">You can enable your users tooautomatically get signed-on tooGigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5c02-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c5c02-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c5c02-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5c02-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5c02-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c5c02-110">Prerequisites</span></span>

<span data-ttu-id="c5c02-111">tooconfigure интеграция Azure AD с Gigya, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c5c02-111">tooconfigure Azure AD integration with Gigya, you need hello following items:</span></span>

- <span data-ttu-id="c5c02-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c5c02-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5c02-113">подписка Gigya с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c5c02-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5c02-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c5c02-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5c02-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c5c02-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5c02-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c5c02-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5c02-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5c02-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5c02-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c5c02-118">Scenario description</span></span>
<span data-ttu-id="c5c02-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c5c02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5c02-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c5c02-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5c02-121">Добавление Gigya из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c5c02-121">Adding Gigya from hello gallery</span></span>
2. <span data-ttu-id="c5c02-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5c02-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-hello-gallery"></a><span data-ttu-id="c5c02-123">Добавление Gigya из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c5c02-123">Adding Gigya from hello gallery</span></span>
<span data-ttu-id="c5c02-124">tooconfigure hello интеграции Gigya в Azure AD, вы должны tooadd Gigya из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c5c02-124">tooconfigure hello integration of Gigya into Azure AD, you need tooadd Gigya from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5c02-125">**tooadd Gigya из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c5c02-125">**tooadd Gigya from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5c02-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c5c02-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5c02-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5c02-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c5c02-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c5c02-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c5c02-133">Введите в поле поиска hello **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-133">In hello search box, type **Gigya**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="c5c02-135">В панели результатов hello выберите **Gigya**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c5c02-135">In hello results panel, select **Gigya**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5c02-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5c02-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5c02-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Gigya с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5c02-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5c02-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Gigya является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5c02-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Gigya is tooa user in Azure AD.</span></span> <span data-ttu-id="c5c02-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Gigya должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c5c02-140">In other words, a link relationship between an Azure AD user and hello related user in Gigya needs toobe established.</span></span>

<span data-ttu-id="c5c02-141">В Gigya, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="c5c02-141">In Gigya, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c5c02-142">tooconfigure и теста Azure AD единого входа с Gigya, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c5c02-142">tooconfigure and test Azure AD single sign-on with Gigya, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5c02-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c5c02-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5c02-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c5c02-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5c02-145">**[Создание тестового пользователя Gigya](#creating-a-gigya-test-user)**  -toohave аналог Саймон Britta в Gigya, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c5c02-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - toohave a counterpart of Britta Simon in Gigya that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5c02-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c5c02-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5c02-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c5c02-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5c02-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5c02-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5c02-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Gigya приложения.</span><span class="sxs-lookup"><span data-stu-id="c5c02-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="c5c02-150">**Azure AD tooconfigure единого входа с Gigya, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c5c02-150">**tooconfigure Azure AD single sign-on with Gigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5c02-151">В hello в hello портала Azure **Gigya** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-151">In hello Azure portal, on hello **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c5c02-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c5c02-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="c5c02-155">На hello **URL-адреса и домена Gigya** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c5c02-155">On hello **Gigya Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="c5c02-157">а.</span><span class="sxs-lookup"><span data-stu-id="c5c02-157">a.</span></span> <span data-ttu-id="c5c02-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="c5c02-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="c5c02-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5c02-159">b.</span></span> <span data-ttu-id="c5c02-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c5c02-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5c02-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c5c02-161">These values are not real.</span></span> <span data-ttu-id="c5c02-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="c5c02-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c5c02-163">Обратитесь к [группа поддержки клиента Gigya](https://www.gigya.com/support-policy/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="c5c02-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) tooget these values.</span></span> 
 
4. <span data-ttu-id="c5c02-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c5c02-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="c5c02-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c5c02-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5c02-168">На hello **конфигурации Gigya** щелкните **Настройка Gigya** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="c5c02-168">On hello **Gigya Configuration** section, click **Configure Gigya** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c5c02-169">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="c5c02-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="c5c02-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Gigya в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c5c02-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="c5c02-172">Go слишком**параметры \> входа SAML**и нажмите кнопку hello **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c5c02-172">Go too**Settings \> SAML Login**, and then click hello **Add** button.</span></span>
   
    <span data-ttu-id="c5c02-173">![Вход SAML](./media/active-directory-saas-gigya-tutorial/ic789532.png "Вход SAML")</span><span class="sxs-lookup"><span data-stu-id="c5c02-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="c5c02-174">В hello **входа SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c5c02-174">In hello **SAML Login** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c5c02-175">![Настройка SAML](./media/active-directory-saas-gigya-tutorial/ic789533.png "Настройка SAML")</span><span class="sxs-lookup"><span data-stu-id="c5c02-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="c5c02-176">а.</span><span class="sxs-lookup"><span data-stu-id="c5c02-176">a.</span></span> <span data-ttu-id="c5c02-177">В hello **имя** текстовом поле введите имя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c5c02-177">In hello **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="c5c02-178">b.</span><span class="sxs-lookup"><span data-stu-id="c5c02-178">b.</span></span> <span data-ttu-id="c5c02-179">В **издателя** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c5c02-179">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="c5c02-180">c.</span><span class="sxs-lookup"><span data-stu-id="c5c02-180">c.</span></span> <span data-ttu-id="c5c02-181">В **единого входа URL-адрес службы** текстовое значение hello вставить **единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c5c02-181">In **Single Sign-On Service URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="c5c02-182">d.</span><span class="sxs-lookup"><span data-stu-id="c5c02-182">d.</span></span> <span data-ttu-id="c5c02-183">В **формат идентификатора имени** текстовое значение hello вставить **формат идентификатора имени** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c5c02-183">In **Name ID Format** textbox, paste hello value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="c5c02-184">д.</span><span class="sxs-lookup"><span data-stu-id="c5c02-184">e.</span></span> <span data-ttu-id="c5c02-185">Откройте сертификат в кодировке base-64 в блокноте, загруженные из портала Azure hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="c5c02-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="c5c02-186">f.</span><span class="sxs-lookup"><span data-stu-id="c5c02-186">f.</span></span> <span data-ttu-id="c5c02-187">Нажмите кнопку **Сохранить параметры**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="c5c02-188">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c5c02-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5c02-189">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c5c02-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5c02-190">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5c02-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5c02-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5c02-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="c5c02-192">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c5c02-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c5c02-194">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c5c02-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5c02-195">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c5c02-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5c02-197">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5c02-199">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="c5c02-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5c02-201">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c5c02-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5c02-203">а.</span><span class="sxs-lookup"><span data-stu-id="c5c02-203">a.</span></span> <span data-ttu-id="c5c02-204">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5c02-205">b.</span><span class="sxs-lookup"><span data-stu-id="c5c02-205">b.</span></span> <span data-ttu-id="c5c02-206">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c5c02-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5c02-207">c.</span><span class="sxs-lookup"><span data-stu-id="c5c02-207">c.</span></span> <span data-ttu-id="c5c02-208">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5c02-209">d.</span><span class="sxs-lookup"><span data-stu-id="c5c02-209">d.</span></span> <span data-ttu-id="c5c02-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="c5c02-211">Создание тестового пользователя Gigya</span><span class="sxs-lookup"><span data-stu-id="c5c02-211">Creating a Gigya test user</span></span>

<span data-ttu-id="c5c02-212">В порядке tooenable toolog пользователей Azure AD в Gigya их необходимо подготовить в Gigya.</span><span class="sxs-lookup"><span data-stu-id="c5c02-212">In order tooenable Azure AD users toolog into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="c5c02-213">В случае hello объекта Gigya Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="c5c02-213">In hello case of Gigya, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="c5c02-214">tooprovision учетных записей пользователей, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="c5c02-214">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="c5c02-215">Войдите в tooyour **Gigya** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="c5c02-215">Log in tooyour **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="c5c02-216">Go слишком**администратора \> Управление пользователями**, а затем нажмите кнопку **приглашения пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-216">Go too**Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="c5c02-217">![Управление пользователями](./media/active-directory-saas-gigya-tutorial/ic789535.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="c5c02-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="c5c02-218">В диалоговом окне приглашения пользователя hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c5c02-218">On hello Invite Users dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="c5c02-219">![Приглашение пользователей](./media/active-directory-saas-gigya-tutorial/ic789536.png "приглашение пользователей")</span><span class="sxs-lookup"><span data-stu-id="c5c02-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="c5c02-220">а.</span><span class="sxs-lookup"><span data-stu-id="c5c02-220">a.</span></span> <span data-ttu-id="c5c02-221">В hello **электронной почты** в текстовое поле псевдоним электронной почты типа hello действительной учетной записи Azure Active Directory требуется tooprovision.</span><span class="sxs-lookup"><span data-stu-id="c5c02-221">In hello **Email** textbox, type hello email alias of a valid Azure Active Directory account you want tooprovision.</span></span>
    
    <span data-ttu-id="c5c02-222">b.</span><span class="sxs-lookup"><span data-stu-id="c5c02-222">b.</span></span> <span data-ttu-id="c5c02-223">Нажмите кнопку **Пригласить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="c5c02-224">Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты, который включает учетную запись hello tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="c5c02-224">hello Azure Active Directory account holder will receive an email that includes a link tooconfirm hello account before it becomes active.</span></span>
    > 
    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5c02-225">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c5c02-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5c02-226">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooGigya доступа.</span><span class="sxs-lookup"><span data-stu-id="c5c02-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGigya.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c5c02-228">**tooassign tooGigya Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c5c02-228">**tooassign Britta Simon tooGigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5c02-229">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c5c02-231">В списке приложений hello выберите **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-231">In hello applications list, select **Gigya**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="c5c02-233">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c5c02-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-235">Click **Add** button.</span></span> <span data-ttu-id="c5c02-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c5c02-238">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c5c02-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5c02-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5c02-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c5c02-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5c02-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c5c02-241">Testing single sign-on</span></span>

<span data-ttu-id="c5c02-242">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="c5c02-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5c02-243">При нажатии кнопки hello Gigya плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Gigya приложения.</span><span class="sxs-lookup"><span data-stu-id="c5c02-243">When you click hello Gigya tile in hello Access Panel, you should get automatically signed-on tooyour Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5c02-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c5c02-244">Additional resources</span></span>

* [<span data-ttu-id="c5c02-245">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5c02-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5c02-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5c02-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

