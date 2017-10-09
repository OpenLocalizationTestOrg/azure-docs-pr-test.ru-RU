---
title: "Руководство. Интеграция Azure Active Directory с AirWatch | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="c37c0-103">Руководство. Интеграция Azure Active Directory с AirWatch</span><span class="sxs-lookup"><span data-stu-id="c37c0-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="c37c0-104">В этом учебнике вы узнаете, как toointegrate AirWatch с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c37c0-104">In this tutorial, you learn how toointegrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c37c0-105">Интеграция AirWatch с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c37c0-105">Integrating AirWatch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c37c0-106">Можно управлять в Azure AD, имеющего доступ tooAirWatch</span><span class="sxs-lookup"><span data-stu-id="c37c0-106">You can control in Azure AD who has access tooAirWatch</span></span>
- <span data-ttu-id="c37c0-107">Можно включить на пользователей tooautomatically get вошедшего tooAirWatch (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="c37c0-107">You can enable your users tooautomatically get signed-on tooAirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c37c0-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c37c0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c37c0-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c37c0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c37c0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c37c0-110">Prerequisites</span></span>

<span data-ttu-id="c37c0-111">tooconfigure интеграция Azure AD с AirWatch требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c37c0-111">tooconfigure Azure AD integration with AirWatch, you need hello following items:</span></span>

- <span data-ttu-id="c37c0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c37c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c37c0-113">подписка AirWatch с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c37c0-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c37c0-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c37c0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c37c0-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c37c0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c37c0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c37c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c37c0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c37c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c37c0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c37c0-118">Scenario description</span></span>
<span data-ttu-id="c37c0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c37c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c37c0-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c37c0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c37c0-121">Добавление AirWatch из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c37c0-121">Adding AirWatch from hello gallery</span></span>
2. <span data-ttu-id="c37c0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c37c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-hello-gallery"></a><span data-ttu-id="c37c0-123">Добавление AirWatch из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c37c0-123">Adding AirWatch from hello gallery</span></span>
<span data-ttu-id="c37c0-124">tooconfigure hello интеграции AirWatch в Azure AD, вы должны tooadd AirWatch от hello коллекции tooyour список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c37c0-124">tooconfigure hello integration of AirWatch into Azure AD, you need tooadd AirWatch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c37c0-125">**tooadd AirWatch из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c37c0-125">**tooadd AirWatch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c37c0-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c37c0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c37c0-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c37c0-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c37c0-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c37c0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c37c0-133">Введите в поле поиска hello **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-133">In hello search box, type **AirWatch**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="c37c0-135">В панели результатов hello выберите **AirWatch**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c37c0-135">In hello results panel, select **AirWatch**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c37c0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c37c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c37c0-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение AirWatch с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c37c0-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c37c0-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в AirWatch является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c37c0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AirWatch is tooa user in Azure AD.</span></span> <span data-ttu-id="c37c0-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в AirWatch должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c37c0-140">In other words, a link relationship between an Azure AD user and hello related user in AirWatch needs toobe established.</span></span>

<span data-ttu-id="c37c0-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в AirWatch.</span><span class="sxs-lookup"><span data-stu-id="c37c0-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in AirWatch.</span></span>

<span data-ttu-id="c37c0-142">tooconfigure и теста Azure AD единого входа с AirWatch, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c37c0-142">tooconfigure and test Azure AD single sign-on with AirWatch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c37c0-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c37c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c37c0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c37c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c37c0-145">**[Создание тестового пользователя AirWatch](#creating-a-airwatch-test-user)**  -toohave аналог Саймон Britta в AirWatch, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c37c0-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - toohave a counterpart of Britta Simon in AirWatch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c37c0-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c37c0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c37c0-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c37c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c37c0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c37c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c37c0-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение AirWatch.</span><span class="sxs-lookup"><span data-stu-id="c37c0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="c37c0-150">**tooconfigure Azure AD единого входа с AirWatch, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c37c0-150">**tooconfigure Azure AD single sign-on with AirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="c37c0-151">В hello в hello портала Azure **AirWatch** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-151">In hello Azure portal, on hello **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c37c0-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c37c0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="c37c0-155">На hello **URL-адреса и домена AirWatch** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c37c0-155">On hello **AirWatch Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="c37c0-157">а.</span><span class="sxs-lookup"><span data-stu-id="c37c0-157">a.</span></span> <span data-ttu-id="c37c0-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="c37c0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="c37c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="c37c0-159">b.</span></span> <span data-ttu-id="c37c0-160">В hello **идентификатор** текстовое поле, значение типа hello как`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="c37c0-160">In hello **Identifier** textbox, type hello value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c37c0-161">Это значение не реальными hello.</span><span class="sxs-lookup"><span data-stu-id="c37c0-161">This value is not hello real.</span></span> <span data-ttu-id="c37c0-162">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="c37c0-162">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="c37c0-163">Обратитесь к [группа поддержки клиента AirWatch](http://www.air-watch.com/company/contact-us/) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="c37c0-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) tooget this value.</span></span> 
 
4. <span data-ttu-id="c37c0-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c37c0-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="c37c0-166">На hello **конфигурации AirWatch** щелкните **Настройка AirWatch** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="c37c0-166">On hello **AirWatch Configuration** section, click **Configure AirWatch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c37c0-167">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="c37c0-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="c37c0-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c37c0-169">Click **Save** button.</span></span>

    <span data-ttu-id="c37c0-170">![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="c37c0-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="c37c0-171">В другом окне браузера Войдите на сайте компании AirWatch tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c37c0-171">In a different web browser window, log in tooyour AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="c37c0-172">Hello панели навигации слева щелкните **учетные записи**, а затем нажмите кнопку **Администраторы**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-172">In hello left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="c37c0-173">![Администраторы](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Администраторы")</span><span class="sxs-lookup"><span data-stu-id="c37c0-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="c37c0-174">Разверните hello **параметры** меню, а затем нажмите **службы каталогов**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-174">Expand hello **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="c37c0-175">![Параметры](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="c37c0-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="c37c0-176">Нажмите кнопку hello **пользователя** hello на вкладке **базовое DN** текстовом поле введите имя домена и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-176">Click hello **User** tab, in hello **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="c37c0-177">![Пользователь](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Пользователь")</span><span class="sxs-lookup"><span data-stu-id="c37c0-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="c37c0-178">Нажмите кнопку hello **сервера** вкладки.</span><span class="sxs-lookup"><span data-stu-id="c37c0-178">Click hello **Server** tab.</span></span>
   
   <span data-ttu-id="c37c0-179">![Сервер](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Сервер")</span><span class="sxs-lookup"><span data-stu-id="c37c0-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="c37c0-180">Выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c37c0-180">Perform hello following steps:</span></span>
    
    <span data-ttu-id="c37c0-181">![Передача](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Передача")</span><span class="sxs-lookup"><span data-stu-id="c37c0-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="c37c0-182">а.</span><span class="sxs-lookup"><span data-stu-id="c37c0-182">a.</span></span> <span data-ttu-id="c37c0-183">Для параметра **Directory Type** (Тип каталога) выберите значение **None** (Нет).</span><span class="sxs-lookup"><span data-stu-id="c37c0-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="c37c0-184">b.</span><span class="sxs-lookup"><span data-stu-id="c37c0-184">b.</span></span> <span data-ttu-id="c37c0-185">Установите флажок **Use SAML For Authentication**(Использовать SAML для проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="c37c0-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="c37c0-186">c.</span><span class="sxs-lookup"><span data-stu-id="c37c0-186">c.</span></span> <span data-ttu-id="c37c0-187">tooupload Здравствуйте Скачанный сертификат, нажмите кнопку **отправить**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-187">tooupload hello downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="c37c0-188">В hello **запроса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c37c0-188">In hello **Request** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="c37c0-189">![Запрос](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Запрос")</span><span class="sxs-lookup"><span data-stu-id="c37c0-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="c37c0-190">а.</span><span class="sxs-lookup"><span data-stu-id="c37c0-190">a.</span></span> <span data-ttu-id="c37c0-191">Для параметра **Request Binding Type** (Тип привязки запроса) выберите значение **POST**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="c37c0-192">b.</span><span class="sxs-lookup"><span data-stu-id="c37c0-192">b.</span></span> <span data-ttu-id="c37c0-193">В hello в hello портала Azure **настройки единого входа в Airwatch** странице диалогового окна, hello копирования **SAML единого входа URL-адрес службы** значение, а затем вставьте его в hello **поставщика удостоверений Один на URL-адрес входа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="c37c0-193">In hello Azure portal, on hello **Configure single sign-on at Airwatch** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="c37c0-194">c.</span><span class="sxs-lookup"><span data-stu-id="c37c0-194">c.</span></span> <span data-ttu-id="c37c0-195">Для параметра **NameID Format** (Формат идентификатора имени) выберите значение **Email Address** (Адрес электронной почты).</span><span class="sxs-lookup"><span data-stu-id="c37c0-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="c37c0-196">г)</span><span class="sxs-lookup"><span data-stu-id="c37c0-196">d.</span></span> <span data-ttu-id="c37c0-197">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-197">Click **Save**.</span></span>

14. <span data-ttu-id="c37c0-198">Нажмите кнопку hello **пользователя** вкладку еще раз.</span><span class="sxs-lookup"><span data-stu-id="c37c0-198">Click hello **User** tab again.</span></span>
    
    <span data-ttu-id="c37c0-199">![Пользователь](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Пользователь")</span><span class="sxs-lookup"><span data-stu-id="c37c0-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="c37c0-200">В hello **атрибута** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c37c0-200">In hello **Attribute** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="c37c0-201">![Атрибут](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Атрибут")</span><span class="sxs-lookup"><span data-stu-id="c37c0-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="c37c0-202">а.</span><span class="sxs-lookup"><span data-stu-id="c37c0-202">a.</span></span> <span data-ttu-id="c37c0-203">В hello **идентификатор объекта** введите **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-203">In hello **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="c37c0-204">b.</span><span class="sxs-lookup"><span data-stu-id="c37c0-204">b.</span></span> <span data-ttu-id="c37c0-205">В hello **Username** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-205">In hello **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="c37c0-206">c.</span><span class="sxs-lookup"><span data-stu-id="c37c0-206">c.</span></span> <span data-ttu-id="c37c0-207">В hello **отображаемое имя** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-207">In hello **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="c37c0-208">d.</span><span class="sxs-lookup"><span data-stu-id="c37c0-208">d.</span></span> <span data-ttu-id="c37c0-209">В hello **имя** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-209">In hello **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="c37c0-210">д.</span><span class="sxs-lookup"><span data-stu-id="c37c0-210">e.</span></span> <span data-ttu-id="c37c0-211">В hello **Фамилия** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-211">In hello **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="c37c0-212">f.</span><span class="sxs-lookup"><span data-stu-id="c37c0-212">f.</span></span> <span data-ttu-id="c37c0-213">В hello **электронной почты** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-213">In hello **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="c37c0-214">ж.</span><span class="sxs-lookup"><span data-stu-id="c37c0-214">g.</span></span> <span data-ttu-id="c37c0-215">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c37c0-216">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c37c0-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="c37c0-217">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c37c0-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c37c0-219">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c37c0-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c37c0-220">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c37c0-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c37c0-222">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c37c0-224">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="c37c0-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c37c0-226">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c37c0-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c37c0-228">а.</span><span class="sxs-lookup"><span data-stu-id="c37c0-228">a.</span></span> <span data-ttu-id="c37c0-229">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c37c0-230">b.</span><span class="sxs-lookup"><span data-stu-id="c37c0-230">b.</span></span> <span data-ttu-id="c37c0-231">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c37c0-231">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="c37c0-232">c.</span><span class="sxs-lookup"><span data-stu-id="c37c0-232">c.</span></span> <span data-ttu-id="c37c0-233">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c37c0-234">d.</span><span class="sxs-lookup"><span data-stu-id="c37c0-234">d.</span></span> <span data-ttu-id="c37c0-235">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="c37c0-236">Создание тестового пользователя AirWatch</span><span class="sxs-lookup"><span data-stu-id="c37c0-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="c37c0-237">Пользователи toolog tooenable Azure AD в tooAirWatch, их необходимо подготовить в tooAirWatch.</span><span class="sxs-lookup"><span data-stu-id="c37c0-237">tooenable Azure AD users toolog in tooAirWatch, they must be provisioned in tooAirWatch.</span></span>

* <span data-ttu-id="c37c0-238">Подготовка в AirWatch выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="c37c0-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="c37c0-239">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c37c0-239">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c37c0-240">Войдите в tooyour **AirWatch** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="c37c0-240">Log in tooyour **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="c37c0-241">Hello hello левой панели навигации щелкните **учетные записи**, а затем нажмите кнопку **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-241">In hello navigation pane on hello left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="c37c0-242">![Пользователи](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="c37c0-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="c37c0-243">В hello **пользователей** меню, нажмите кнопку **представление списка**, а затем нажмите кнопку **добавить \> добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-243">In hello **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="c37c0-244">![Добавление пользователя](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="c37c0-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="c37c0-245">На hello **Добавление и изменение пользователей** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c37c0-245">On hello **Add / Edit User** dialog, perform hello following steps:</span></span>

   <span data-ttu-id="c37c0-246">![Добавление пользователя](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="c37c0-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="c37c0-247">Тип hello **Username**, **пароль**, **подтверждение пароля**, **имя**, **Фамилия**,  **Адрес электронной почты** из допустимых Azure связанные с учетной записью Active Directory требуется tooprovision в hello текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="c37c0-247">Type hello **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="c37c0-248">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="c37c0-249">Можно использовать любые другие AirWatch пользователя средства создания учетных записей или интерфейсы API, предоставляемые AirWatch tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="c37c0-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c37c0-250">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c37c0-250">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c37c0-251">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAirWatch доступа.</span><span class="sxs-lookup"><span data-stu-id="c37c0-251">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAirWatch.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c37c0-253">**tooassign tooAirWatch Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c37c0-253">**tooassign Britta Simon tooAirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="c37c0-254">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-254">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c37c0-256">В списке приложений hello выберите **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-256">In hello applications list, select **AirWatch**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="c37c0-258">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-258">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c37c0-260">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-260">Click **Add** button.</span></span> <span data-ttu-id="c37c0-261">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c37c0-263">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c37c0-263">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c37c0-264">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c37c0-265">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c37c0-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c37c0-266">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c37c0-266">Testing single sign-on</span></span>

<span data-ttu-id="c37c0-267">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c37c0-267">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c37c0-268">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c37c0-268">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="c37c0-269">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c37c0-269">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c37c0-270">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c37c0-270">Additional resources</span></span>

* [<span data-ttu-id="c37c0-271">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c37c0-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c37c0-272">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c37c0-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

