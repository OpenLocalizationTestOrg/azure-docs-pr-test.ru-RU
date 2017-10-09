---
title: "Учебник. Интеграция Azure Active Directory с InsideView | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и InsideView."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 979c0c24f3a18a193616061b8c2e78292233a56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="85911-103">Руководство. Интеграция Azure Active Directory с InsideView</span><span class="sxs-lookup"><span data-stu-id="85911-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="85911-104">В этом учебнике вы узнаете, как toointegrate InsideView с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85911-104">In this tutorial, you learn how toointegrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85911-105">Интеграция InsideView с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="85911-105">Integrating InsideView with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="85911-106">Можно управлять в Azure AD, имеющего доступ tooInsideView</span><span class="sxs-lookup"><span data-stu-id="85911-106">You can control in Azure AD who has access tooInsideView</span></span>
- <span data-ttu-id="85911-107">Можно включить на пользователей tooautomatically get вошедшего tooInsideView (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="85911-107">You can enable your users tooautomatically get signed-on tooInsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="85911-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="85911-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="85911-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="85911-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85911-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="85911-110">Prerequisites</span></span>

<span data-ttu-id="85911-111">tooconfigure интеграция Azure AD с InsideView требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="85911-111">tooconfigure Azure AD integration with InsideView, you need hello following items:</span></span>

- <span data-ttu-id="85911-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="85911-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85911-113">подписка с поддержкой единого входа InsideView.</span><span class="sxs-lookup"><span data-stu-id="85911-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85911-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="85911-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85911-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="85911-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85911-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="85911-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85911-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85911-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85911-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="85911-118">Scenario description</span></span>
<span data-ttu-id="85911-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="85911-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85911-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="85911-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85911-121">Добавление InsideView из галереи hello</span><span class="sxs-lookup"><span data-stu-id="85911-121">Adding InsideView from hello gallery</span></span>
2. <span data-ttu-id="85911-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="85911-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-hello-gallery"></a><span data-ttu-id="85911-123">Добавление InsideView из галереи hello</span><span class="sxs-lookup"><span data-stu-id="85911-123">Adding InsideView from hello gallery</span></span>
<span data-ttu-id="85911-124">tooconfigure hello интеграции InsideView в tooAzure AD, вы должны tooadd InsideView из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="85911-124">tooconfigure hello integration of InsideView in tooAzure AD, you need tooadd InsideView from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="85911-125">**tooadd InsideView из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="85911-125">**tooadd InsideView from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="85911-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="85911-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="85911-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="85911-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="85911-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="85911-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="85911-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="85911-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="85911-133">Введите в поле поиска hello **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="85911-133">In hello search box, type **InsideView**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="85911-135">В панели результатов hello выберите **InsideView**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="85911-135">In hello results panel, select **InsideView**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="85911-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="85911-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="85911-138">В этом разделе описана настройка и проверка единого входа Azure AD в InsideView с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85911-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="85911-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в InsideView является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85911-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InsideView is tooa user in Azure AD.</span></span> <span data-ttu-id="85911-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в InsideView должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="85911-140">In other words, a link relationship between an Azure AD user and hello related user in InsideView needs toobe established.</span></span>

<span data-ttu-id="85911-141">В InsideView, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="85911-141">In InsideView, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="85911-142">tooconfigure и теста Azure AD единого входа с InsideView, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="85911-142">tooconfigure and test Azure AD single sign-on with InsideView, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="85911-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="85911-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="85911-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="85911-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85911-145">**[Создание тестового пользователя InsideView](#creating-a-insideview-test-user)**  -toohave аналог Саймон Britta в InsideView, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="85911-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - toohave a counterpart of Britta Simon in InsideView that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="85911-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="85911-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85911-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="85911-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="85911-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="85911-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="85911-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении InsideView.</span><span class="sxs-lookup"><span data-stu-id="85911-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="85911-150">**tooconfigure Azure AD единого входа с InsideView, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="85911-150">**tooconfigure Azure AD single sign-on with InsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="85911-151">В hello в hello портала Azure **InsideView** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="85911-151">In hello Azure portal, on hello **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="85911-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="85911-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="85911-155">На hello **URL-адреса и домена InsideView** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="85911-155">On hello **InsideView Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="85911-157">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="85911-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="85911-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="85911-158">This value is not real.</span></span> <span data-ttu-id="85911-159">Измените значение этого параметра hello фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="85911-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="85911-160">Обратитесь к [InsideView поддержки ](mailto:support@insideview.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="85911-160">Contact [InsideView support team ](mailto:support@insideview.com) tooget this value.</span></span>
 
4. <span data-ttu-id="85911-161">На hello **сертификат подписи SAML** щелкните **сертификата (Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="85911-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="85911-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="85911-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="85911-165">На hello **конфигурации InsideView** щелкните **Настройка InsideView** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="85911-165">On hello **InsideView Configuration** section, click **Configure InsideView** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="85911-166">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="85911-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="85911-168">В другом окне браузера Войдите на сайте компании InsideView tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="85911-168">In a different web browser window, log in tooyour InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="85911-169">Щелкните hello панели инструментов в верхней части hello **администратора**, **параметры единого входа**и нажмите кнопку **добавить SAML**.</span><span class="sxs-lookup"><span data-stu-id="85911-169">In hello toolbar on hello top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="85911-170">![Параметры единого входа SAML](./media/active-directory-saas-insideview-tutorial/ic794135.png "Параметры единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="85911-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="85911-171">В hello **добавить новый SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="85911-171">In hello **Add a New SAML** section, perform hello following steps:</span></span>

    <span data-ttu-id="85911-172">![Добавление SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Добавление SAML")</span><span class="sxs-lookup"><span data-stu-id="85911-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="85911-173">а.</span><span class="sxs-lookup"><span data-stu-id="85911-173">a.</span></span> <span data-ttu-id="85911-174">В hello **имя STS** текстовом поле введите имя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="85911-174">In hello **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="85911-175">b.</span><span class="sxs-lookup"><span data-stu-id="85911-175">b.</span></span> <span data-ttu-id="85911-176">В **конечная точка SamlP/WS-Fed незапрошенные конечной точки** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, которого вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="85911-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="85911-177">c.</span><span class="sxs-lookup"><span data-stu-id="85911-177">c.</span></span> <span data-ttu-id="85911-178">Откройте base-64 сертификат в кодировке, который вы скачали из содержимого его в буфер обмена Azure hello портала, копировать, а затем вставьте его toohello **сертификат STS** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="85911-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **STS Certificate** textbox.</span></span>

    <span data-ttu-id="85911-179">d.</span><span class="sxs-lookup"><span data-stu-id="85911-179">d.</span></span> <span data-ttu-id="85911-180">В hello **сопоставление идентификаторов пользователей Crm** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="85911-180">In hello **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="85911-181">д.</span><span class="sxs-lookup"><span data-stu-id="85911-181">e.</span></span> <span data-ttu-id="85911-182">В hello **сопоставление адресов электронной почты Crm** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="85911-182">In hello **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="85911-183">f.</span><span class="sxs-lookup"><span data-stu-id="85911-183">f.</span></span> <span data-ttu-id="85911-184">В hello **сопоставление имени Crm** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="85911-184">In hello **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="85911-185">ж.</span><span class="sxs-lookup"><span data-stu-id="85911-185">g.</span></span> <span data-ttu-id="85911-186">В hello **Crm lastName сопоставление** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="85911-186">In hello **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="85911-187">h.</span><span class="sxs-lookup"><span data-stu-id="85911-187">h.</span></span> <span data-ttu-id="85911-188">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="85911-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="85911-189">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="85911-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="85911-190">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="85911-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="85911-191">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="85911-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="85911-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="85911-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="85911-193">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="85911-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="85911-195">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="85911-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="85911-196">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="85911-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="85911-198">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="85911-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="85911-200">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="85911-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="85911-202">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="85911-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="85911-204">а.</span><span class="sxs-lookup"><span data-stu-id="85911-204">a.</span></span> <span data-ttu-id="85911-205">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85911-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85911-206">b.</span><span class="sxs-lookup"><span data-stu-id="85911-206">b.</span></span> <span data-ttu-id="85911-207">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="85911-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="85911-208">c.</span><span class="sxs-lookup"><span data-stu-id="85911-208">c.</span></span> <span data-ttu-id="85911-209">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="85911-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="85911-210">d.</span><span class="sxs-lookup"><span data-stu-id="85911-210">d.</span></span> <span data-ttu-id="85911-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="85911-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="85911-212">Создание тестового пользователя InsideView</span><span class="sxs-lookup"><span data-stu-id="85911-212">Creating a InsideView test user</span></span>

<span data-ttu-id="85911-213">Пользователи toolog tooenable Azure AD в tooInsideView, их необходимо подготовить в tooInsideView.</span><span class="sxs-lookup"><span data-stu-id="85911-213">tooenable Azure AD users toolog in tooInsideView, they must be provisioned in tooInsideView.</span></span> <span data-ttu-id="85911-214">В случае hello InsideView Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="85911-214">In hello case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="85911-215">tooget пользователей и контактов, созданных в InsideView, обратитесь к [InsideView поддержки](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="85911-215">tooget users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="85911-216">Можно использовать любые другие InsideView пользователя средства создания учетных записей или интерфейсы API, предоставляемые InsideView tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85911-216">You can use any other InsideView user account creation tools or APIs provided by InsideView tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="85911-217">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="85911-217">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="85911-218">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooInsideView доступа.</span><span class="sxs-lookup"><span data-stu-id="85911-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsideView.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="85911-220">**tooassign tooInsideView Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="85911-220">**tooassign Britta Simon tooInsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="85911-221">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="85911-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="85911-223">В списке приложений hello выберите **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="85911-223">In hello applications list, select **InsideView**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="85911-225">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="85911-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="85911-227">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="85911-227">Click **Add** button.</span></span> <span data-ttu-id="85911-228">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="85911-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="85911-230">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="85911-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="85911-231">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="85911-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85911-232">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="85911-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="85911-233">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="85911-233">Testing single sign-on</span></span>

<span data-ttu-id="85911-234">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="85911-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="85911-235">При нажатии кнопки hello InsideView плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour InsideView.</span><span class="sxs-lookup"><span data-stu-id="85911-235">When you click hello InsideView tile in hello Access Panel, you should get automatically signed-on tooyour InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="85911-236">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="85911-236">Additional resources</span></span>

* [<span data-ttu-id="85911-237">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85911-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85911-238">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="85911-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

