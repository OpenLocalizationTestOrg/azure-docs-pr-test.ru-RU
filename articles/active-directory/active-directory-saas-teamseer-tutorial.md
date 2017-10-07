---
title: "Руководство по интеграции Azure Active Directory с TeamSeer | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и TeamSeer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="43fab-103">Учебник. Интеграция Azure Active Directory с TeamSeer</span><span class="sxs-lookup"><span data-stu-id="43fab-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="43fab-104">В этом учебнике вы узнаете, как toointegrate TeamSeer с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43fab-104">In this tutorial, you learn how toointegrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43fab-105">Интеграция TeamSeer с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="43fab-105">Integrating TeamSeer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="43fab-106">Можно управлять в Azure AD, имеющего доступ tooTeamSeer</span><span class="sxs-lookup"><span data-stu-id="43fab-106">You can control in Azure AD who has access tooTeamSeer</span></span>
- <span data-ttu-id="43fab-107">Можно включить на пользователей tooautomatically get вошедшего tooTeamSeer (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fab-107">You can enable your users tooautomatically get signed-on tooTeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43fab-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="43fab-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="43fab-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="43fab-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43fab-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="43fab-110">Prerequisites</span></span>

<span data-ttu-id="43fab-111">tooconfigure интеграция Azure AD с TeamSeer, необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="43fab-111">tooconfigure Azure AD integration with TeamSeer, you need hello following items:</span></span>

- <span data-ttu-id="43fab-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="43fab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43fab-113">подписка TeamSeer с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="43fab-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="43fab-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="43fab-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="43fab-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="43fab-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43fab-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="43fab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="43fab-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43fab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="43fab-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="43fab-118">Scenario description</span></span>
<span data-ttu-id="43fab-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="43fab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43fab-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="43fab-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43fab-121">Добавление TeamSeer из галереи hello</span><span class="sxs-lookup"><span data-stu-id="43fab-121">Adding TeamSeer from hello gallery</span></span>
2. <span data-ttu-id="43fab-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-hello-gallery"></a><span data-ttu-id="43fab-123">Добавление TeamSeer из галереи hello</span><span class="sxs-lookup"><span data-stu-id="43fab-123">Adding TeamSeer from hello gallery</span></span>
<span data-ttu-id="43fab-124">tooconfigure hello интеграции TeamSeer в tooAzure AD, вы должны tooadd TeamSeer из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="43fab-124">tooconfigure hello integration of TeamSeer in tooAzure AD, you need tooadd TeamSeer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="43fab-125">**tooadd TeamSeer из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="43fab-125">**tooadd TeamSeer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="43fab-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="43fab-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="43fab-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="43fab-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="43fab-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="43fab-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="43fab-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="43fab-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="43fab-133">Введите в поле поиска hello **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="43fab-133">In hello search box, type **TeamSeer**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="43fab-135">В панели результатов hello выберите **TeamSeer**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="43fab-135">In hello results panel, select **TeamSeer**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="43fab-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="43fab-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение TeamSeer с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43fab-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="43fab-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в TeamSeer является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43fab-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TeamSeer is tooa user in Azure AD.</span></span> <span data-ttu-id="43fab-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в TeamSeer должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="43fab-140">In other words, a link relationship between an Azure AD user and hello related user in TeamSeer needs toobe established.</span></span>

<span data-ttu-id="43fab-141">В TeamSeer, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="43fab-141">In TeamSeer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="43fab-142">tooconfigure и теста Azure AD единого входа с TeamSeer, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="43fab-142">tooconfigure and test Azure AD single sign-on with TeamSeer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="43fab-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="43fab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="43fab-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="43fab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="43fab-145">**[Создание тестового пользователя TeamSeer](#creating-a-teamseer-test-user)**  -toohave аналог Саймон Britta в TeamSeer, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="43fab-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - toohave a counterpart of Britta Simon in TeamSeer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="43fab-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="43fab-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="43fab-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="43fab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="43fab-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="43fab-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в TeamSeer приложения.</span><span class="sxs-lookup"><span data-stu-id="43fab-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="43fab-150">**tooconfigure Azure AD единого входа с TeamSeer, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="43fab-150">**tooconfigure Azure AD single sign-on with TeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="43fab-151">В hello в hello портала Azure **TeamSeer** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="43fab-151">In hello Azure portal, on hello **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="43fab-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="43fab-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="43fab-155">На hello **URL-адреса и домена TeamSeer** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="43fab-155">On hello **TeamSeer Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="43fab-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="43fab-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="43fab-158">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="43fab-158">hello value is not real.</span></span> <span data-ttu-id="43fab-159">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="43fab-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="43fab-160">Обратитесь к [группа поддержки клиент TeamSeer](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="43fab-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget hello value.</span></span> 
 
4. <span data-ttu-id="43fab-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="43fab-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="43fab-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="43fab-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="43fab-165">На hello **конфигурации TeamSeer** щелкните **Настройка TeamSeer** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="43fab-165">On hello **TeamSeer Configuration** section, click **Configure TeamSeer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="43fab-166">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="43fab-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="43fab-168">В другом окне браузера войти в корпоративный сайт TeamSeer tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="43fab-168">In a different web browser window, log in tooyour TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="43fab-169">Go слишком**администратор отдела Персонала**.</span><span class="sxs-lookup"><span data-stu-id="43fab-169">Go too**HR Admin**.</span></span>
   
    <span data-ttu-id="43fab-170">![Администратор отдела кадров](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Администратор отдела кадров")</span><span class="sxs-lookup"><span data-stu-id="43fab-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="43fab-171">Щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="43fab-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="43fab-172">![Настройка](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="43fab-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="43fab-173">Щелкните **Задать данные о поставщике SAML**.</span><span class="sxs-lookup"><span data-stu-id="43fab-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="43fab-174">![Параметры SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "Параметры SAML")</span><span class="sxs-lookup"><span data-stu-id="43fab-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="43fab-175">В hello разделе поставщика SAML выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="43fab-175">In hello SAML provider details section, perform hello following steps:</span></span>
   
    <span data-ttu-id="43fab-176">![Параметры SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "Параметры SAML")</span><span class="sxs-lookup"><span data-stu-id="43fab-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="43fab-177">а.</span><span class="sxs-lookup"><span data-stu-id="43fab-177">a.</span></span> <span data-ttu-id="43fab-178">Вставить hello **единого входа URL-адрес службы** значение в toohello **URL-адрес** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="43fab-178">Paste hello **Single Sign-On Service URL** value in toohello **URL** textbox.</span></span>
          
    <span data-ttu-id="43fab-179">b.</span><span class="sxs-lookup"><span data-stu-id="43fab-179">b.</span></span> <span data-ttu-id="43fab-180">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена tooyour, а затем вставьте его toohello **открытый сертификат IdP** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="43fab-180">Open your base-64 encoded certificate in notepad, copy hello content of it in tooyour clipboard, and then paste it toohello **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="43fab-181">hello toocomplete настройки поставщика SAML, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="43fab-181">toocomplete hello SAML provider configuration, perform hello following steps:</span></span>
    
    <span data-ttu-id="43fab-182">![Параметры SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "Параметры SAML")</span><span class="sxs-lookup"><span data-stu-id="43fab-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="43fab-183">а.</span><span class="sxs-lookup"><span data-stu-id="43fab-183">a.</span></span> <span data-ttu-id="43fab-184">В hello **проверки адреса электронной почты**, введите адрес электронной почты hello тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="43fab-184">In hello **Test Email Addresses**, type hello test user’s email address.</span></span> 
  
    <span data-ttu-id="43fab-185">b.</span><span class="sxs-lookup"><span data-stu-id="43fab-185">b.</span></span> <span data-ttu-id="43fab-186">В hello **издателя** текстового поля, типа hello URL-адрес издателя hello поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="43fab-186">In hello **Issuer** textbox, type hello Issuer URL of hello service provider.</span></span> 
  
    <span data-ttu-id="43fab-187">c.</span><span class="sxs-lookup"><span data-stu-id="43fab-187">c.</span></span> <span data-ttu-id="43fab-188">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="43fab-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="43fab-189">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="43fab-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="43fab-190">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="43fab-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="43fab-191">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="43fab-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="43fab-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fab-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="43fab-193">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="43fab-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="43fab-195">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="43fab-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="43fab-196">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="43fab-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="43fab-198">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="43fab-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="43fab-200">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="43fab-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="43fab-202">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="43fab-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="43fab-204">а.</span><span class="sxs-lookup"><span data-stu-id="43fab-204">a.</span></span> <span data-ttu-id="43fab-205">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="43fab-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43fab-206">b.</span><span class="sxs-lookup"><span data-stu-id="43fab-206">b.</span></span> <span data-ttu-id="43fab-207">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="43fab-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="43fab-208">c.</span><span class="sxs-lookup"><span data-stu-id="43fab-208">c.</span></span> <span data-ttu-id="43fab-209">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="43fab-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="43fab-210">d.</span><span class="sxs-lookup"><span data-stu-id="43fab-210">d.</span></span> <span data-ttu-id="43fab-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="43fab-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="43fab-212">Создание тестового пользователя TeamSeer</span><span class="sxs-lookup"><span data-stu-id="43fab-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="43fab-213">Пользователи toolog tooenable Azure AD в tooTeamSeer, их необходимо подготовить в tooShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="43fab-213">tooenable Azure AD users toolog in tooTeamSeer, they must be provisioned in tooShiftPlanning.</span></span> <span data-ttu-id="43fab-214">В случае hello объекта TeamSeer Подготовка осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="43fab-214">In hello case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="43fab-215">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="43fab-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="43fab-216">Войдите в tooyour **TeamSeer** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="43fab-216">Log in tooyour **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="43fab-217">Выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="43fab-217">Perform hello following steps:</span></span>
   
    <span data-ttu-id="43fab-218">![Администратор отдела кадров](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Администратор отдела кадров")</span><span class="sxs-lookup"><span data-stu-id="43fab-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="43fab-219">а.</span><span class="sxs-lookup"><span data-stu-id="43fab-219">a.</span></span> <span data-ttu-id="43fab-220">Go слишком**администратор отдела Персонала \> пользователей**.</span><span class="sxs-lookup"><span data-stu-id="43fab-220">Go too**HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="43fab-221">b.</span><span class="sxs-lookup"><span data-stu-id="43fab-221">b.</span></span> <span data-ttu-id="43fab-222">Нажмите кнопку **запустите мастер добавления нового пользователя hello**.</span><span class="sxs-lookup"><span data-stu-id="43fab-222">Click **Run hello New User wizard**.</span></span>

3. <span data-ttu-id="43fab-223">В hello **сведения о пользователе** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="43fab-223">In hello **User Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="43fab-224">![Сведения о пользователе](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Сведения о пользователе")</span><span class="sxs-lookup"><span data-stu-id="43fab-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="43fab-225">а.</span><span class="sxs-lookup"><span data-stu-id="43fab-225">a.</span></span> <span data-ttu-id="43fab-226">Тип hello **имя**, **Фамилия**, **имя пользователя (адрес электронной почты)** из текстовых полей, связанных с действительной учетной записи AAD, вы хотите tooprovision в toohello.</span><span class="sxs-lookup"><span data-stu-id="43fab-226">Type hello **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want tooprovision in toohello related textboxes.</span></span>
  
    <span data-ttu-id="43fab-227">b.</span><span class="sxs-lookup"><span data-stu-id="43fab-227">b.</span></span> <span data-ttu-id="43fab-228">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="43fab-228">Click **Next**.</span></span>

4. <span data-ttu-id="43fab-229">Следуйте hello на экране инструкциям для добавления нового пользователя, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="43fab-229">Follow hello on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="43fab-230">Можно использовать любые другие TeamSeer пользователя средства создания учетных записей или интерфейсы API, предоставляемые TeamSeer tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43fab-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="43fab-231">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="43fab-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="43fab-232">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooTeamSeer доступа.</span><span class="sxs-lookup"><span data-stu-id="43fab-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTeamSeer.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="43fab-234">**tooassign tooTeamSeer Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="43fab-234">**tooassign Britta Simon tooTeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="43fab-235">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="43fab-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="43fab-237">В списке приложений hello выберите **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="43fab-237">In hello applications list, select **TeamSeer**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="43fab-239">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="43fab-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="43fab-241">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="43fab-241">Click **Add** button.</span></span> <span data-ttu-id="43fab-242">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="43fab-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="43fab-244">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="43fab-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="43fab-245">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="43fab-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="43fab-246">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="43fab-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="43fab-247">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="43fab-247">Testing single sign-on</span></span>

<span data-ttu-id="43fab-248">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="43fab-248">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="43fab-249">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="43fab-249">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43fab-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="43fab-250">Additional resources</span></span>

* [<span data-ttu-id="43fab-251">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43fab-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="43fab-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="43fab-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

