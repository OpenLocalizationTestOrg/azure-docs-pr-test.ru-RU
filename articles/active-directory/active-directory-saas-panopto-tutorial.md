---
title: "Руководство по интеграции Azure Active Directory с Panopto | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory с Panopto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 76b30e1cd2782bb5fba3d229378b8f82652b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="a2fe7-103">Учебник. Интеграция Azure Active Directory с Panopto</span><span class="sxs-lookup"><span data-stu-id="a2fe7-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="a2fe7-104">В этом учебнике вы узнаете, как toointegrate Panopto с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2fe7-104">In this tutorial, you learn how toointegrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2fe7-105">Интеграция Panopto с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a2fe7-105">Integrating Panopto with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a2fe7-106">Можно управлять в Azure AD, имеющего доступ tooPanopto</span><span class="sxs-lookup"><span data-stu-id="a2fe7-106">You can control in Azure AD who has access tooPanopto</span></span>
- <span data-ttu-id="a2fe7-107">Можно включить на пользователей tooautomatically get вошедшего tooPanopto (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2fe7-107">You can enable your users tooautomatically get signed-on tooPanopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2fe7-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a2fe7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a2fe7-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2fe7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2fe7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a2fe7-110">Prerequisites</span></span>

<span data-ttu-id="a2fe7-111">tooconfigure интеграция Azure AD с Panopto требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a2fe7-111">tooconfigure Azure AD integration with Panopto, you need hello following items:</span></span>

- <span data-ttu-id="a2fe7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a2fe7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2fe7-113">подписка Panopto с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2fe7-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2fe7-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a2fe7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2fe7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2fe7-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2fe7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2fe7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a2fe7-118">Scenario description</span></span>
<span data-ttu-id="a2fe7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2fe7-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a2fe7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2fe7-121">Добавление Panopto из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a2fe7-121">Adding Panopto from hello gallery</span></span>
2. <span data-ttu-id="a2fe7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2fe7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-hello-gallery"></a><span data-ttu-id="a2fe7-123">Добавление Panopto из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a2fe7-123">Adding Panopto from hello gallery</span></span>
<span data-ttu-id="a2fe7-124">tooconfigure hello интеграции Panopto в Azure AD, вы должны tooadd Panopto из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-124">tooconfigure hello integration of Panopto into Azure AD, you need tooadd Panopto from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a2fe7-125">**tooadd Panopto из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a2fe7-125">**tooadd Panopto from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2fe7-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2fe7-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a2fe7-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a2fe7-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a2fe7-133">Введите в поле поиска hello **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-133">In hello search box, type **Panopto**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="a2fe7-135">В панели результатов hello выберите **Panopto**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-135">In hello results panel, select **Panopto**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2fe7-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2fe7-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a2fe7-138">В этом разделе описана настройка и проверка единого входа Azure AD в Panopto с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2fe7-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Panopto является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panopto is tooa user in Azure AD.</span></span> <span data-ttu-id="a2fe7-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Panopto должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-140">In other words, a link relationship between an Azure AD user and hello related user in Panopto needs toobe established.</span></span>

<span data-ttu-id="a2fe7-141">В Panopto, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-141">In Panopto, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a2fe7-142">tooconfigure и теста Azure AD единого входа с Panopto, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a2fe7-142">tooconfigure and test Azure AD single sign-on with Panopto, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a2fe7-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a2fe7-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2fe7-145">**[Создание тестового пользователя Panopto](#creating-a-panopto-test-user)**  -toohave аналог Саймон Britta в Panopto, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - toohave a counterpart of Britta Simon in Panopto that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2fe7-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2fe7-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2fe7-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2fe7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2fe7-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Panopto приложения.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="a2fe7-150">**Azure AD tooconfigure единого входа с Panopto, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a2fe7-150">**tooconfigure Azure AD single sign-on with Panopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2fe7-151">В hello в hello портала Azure **Panopto** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-151">In hello Azure portal, on hello **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a2fe7-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="a2fe7-155">На hello **URL-адреса и домена Panopto** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a2fe7-155">On hello **Panopto Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="a2fe7-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="a2fe7-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2fe7-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-158">This value is not real.</span></span> <span data-ttu-id="a2fe7-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="a2fe7-160">Обратитесь к [группа поддержки клиент Panopto](mailto:support@panopto.com‎) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) tooget this value.</span></span> 
 
4. <span data-ttu-id="a2fe7-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="a2fe7-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a2fe7-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a2fe7-165">На hello **конфигурации Panopto** щелкните **Настройка Panopto** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-165">On hello **Panopto Configuration** section, click **Configure Panopto** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a2fe7-166">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="a2fe7-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="a2fe7-168">В другом окне браузера войти в корпоративный сайт Panopto tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-168">In a different web browser window, log in tooyour Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="a2fe7-169">Щелкните hello панели инструментов слева hello **системы**и нажмите кнопку **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-169">In hello toolbar on hello left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="a2fe7-170">![Система](./media/active-directory-saas-panopto-tutorial/ic777670.png "Система")</span><span class="sxs-lookup"><span data-stu-id="a2fe7-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="a2fe7-171">Щелкните **Добавить поставщик**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="a2fe7-172">![Поставщики удостоверений](./media/active-directory-saas-panopto-tutorial/ic777671.png "Поставщики удостоверений")</span><span class="sxs-lookup"><span data-stu-id="a2fe7-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="a2fe7-173">В hello разделе поставщика SAML выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-173">In hello SAML provider section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a2fe7-174">![Конфигурация SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "Конфигурация SaaS")</span><span class="sxs-lookup"><span data-stu-id="a2fe7-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="a2fe7-175">а.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-175">a.</span></span> <span data-ttu-id="a2fe7-176">Из hello **тип поставщика** выберите **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-176">From hello **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="a2fe7-177">b.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-177">b.</span></span> <span data-ttu-id="a2fe7-178">В hello **имя экземпляра** в текстовое поле введите имя для экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-178">In hello **Instance Name** textbox, type a name for hello instance.</span></span>

    <span data-ttu-id="a2fe7-179">c.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-179">c.</span></span> <span data-ttu-id="a2fe7-180">В hello **понятное описание** текстовом поле введите понятное описание.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-180">In hello **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="a2fe7-181">d.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-181">d.</span></span> <span data-ttu-id="a2fe7-182">В **URL-адрес страницы возврата** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-182">In **Bounce Page Url** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a2fe7-183">д.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-183">e.</span></span> <span data-ttu-id="a2fe7-184">В hello **издателя** текстовое значение hello вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-184">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a2fe7-185">f.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-185">f.</span></span> <span data-ttu-id="a2fe7-186">Откройте base-64 сертификат в кодировке, который вы скачали из содержимого его в буфер обмена tooyour Azure hello портала, копировать, а затем вставьте его toohello **открытый ключ** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it in tooyour clipboard, and then paste it toohello **Public Key**  textbox.</span></span>

11. <span data-ttu-id="a2fe7-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a2fe7-188">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a2fe7-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a2fe7-189">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a2fe7-190">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2fe7-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2fe7-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2fe7-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="a2fe7-192">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a2fe7-194">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a2fe7-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2fe7-195">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2fe7-197">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2fe7-199">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a2fe7-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2fe7-201">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a2fe7-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2fe7-203">а.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-203">a.</span></span> <span data-ttu-id="a2fe7-204">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2fe7-205">b.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-205">b.</span></span> <span data-ttu-id="a2fe7-206">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2fe7-207">c.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-207">c.</span></span> <span data-ttu-id="a2fe7-208">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a2fe7-209">d.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-209">d.</span></span> <span data-ttu-id="a2fe7-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="a2fe7-211">Создание тестового пользователя приложения Panopto</span><span class="sxs-lookup"><span data-stu-id="a2fe7-211">Creating a Panopto test user</span></span>

<span data-ttu-id="a2fe7-212">Нет элемента действия для вас tooconfigure подготовки пользователей tooPanopto.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-212">There is no action item for you tooconfigure user provisioning tooPanopto.</span></span>  
<span data-ttu-id="a2fe7-213">Когда назначенный пользователь пытается toolog в tooPanopto, с помощью панели доступа hello, Panopto проверяет, существует ли пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-213">When an assigned user tries toolog in tooPanopto using hello access panel, Panopto checks whether hello user exists.</span></span>  

<span data-ttu-id="a2fe7-214">Если учетная запись пользователя отсутствует, Panopto автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="a2fe7-215">Можно использовать любые другие Panopto пользователя средства создания учетных записей или API, предоставленные Panopto tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-215">You can use any other Panopto user account creation tools or APIs provided by Panopto tooprovision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a2fe7-216">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a2fe7-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a2fe7-217">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPanopto доступа.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanopto.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a2fe7-219">**tooassign tooPanopto Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a2fe7-219">**tooassign Britta Simon tooPanopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2fe7-220">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a2fe7-222">В списке приложений hello выберите **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-222">In hello applications list, select **Panopto**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="a2fe7-224">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a2fe7-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-226">Click **Add** button.</span></span> <span data-ttu-id="a2fe7-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a2fe7-229">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a2fe7-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2fe7-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2fe7-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a2fe7-232">Testing single sign-on</span></span>

<span data-ttu-id="a2fe7-233">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a2fe7-234">Если щелкнуть плитку Panopto hello в hello панели доступа, следует получать автоматически страницы входа в Panopto приложения.</span><span class="sxs-lookup"><span data-stu-id="a2fe7-234">When you click hello Panopto tile in hello Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="a2fe7-235">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a2fe7-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a2fe7-236">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a2fe7-236">Additional resources</span></span>

* [<span data-ttu-id="a2fe7-237">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2fe7-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2fe7-238">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2fe7-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

