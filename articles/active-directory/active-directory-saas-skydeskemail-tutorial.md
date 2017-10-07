---
title: "Руководство по интеграции Azure Active Directory со SkyDesk Email | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SkyDesk электронной почты."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="8d606-103">Учебник. Интеграция Azure Active Directory со SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="8d606-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="8d606-104">В этом учебнике вы узнаете, как toointegrate SkyDesk по электронной почте с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d606-104">In this tutorial, you learn how toointegrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d606-105">Интеграция электронной почты SkyDesk с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8d606-105">Integrating SkyDesk Email with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8d606-106">Можно управлять в Azure AD, имеющего доступ tooSkyDesk электронной почты</span><span class="sxs-lookup"><span data-stu-id="8d606-106">You can control in Azure AD who has access tooSkyDesk Email</span></span>
- <span data-ttu-id="8d606-107">Можно включить на пользователей tooautomatically get вошедшего tooSkyDesk электронной почты (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d606-107">You can enable your users tooautomatically get signed-on tooSkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d606-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8d606-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8d606-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d606-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d606-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8d606-110">Prerequisites</span></span>

<span data-ttu-id="8d606-111">tooconfigure интеграция Azure AD с адресом электронной почты SkyDesk требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8d606-111">tooconfigure Azure AD integration with SkyDesk Email, you need hello following items:</span></span>

- <span data-ttu-id="8d606-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8d606-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d606-113">подписка SkyDesk Email с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8d606-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d606-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8d606-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d606-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8d606-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d606-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8d606-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d606-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d606-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d606-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8d606-118">Scenario description</span></span>
<span data-ttu-id="8d606-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8d606-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d606-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8d606-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d606-121">Добавить адрес электронной почты SkyDesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8d606-121">Adding SkyDesk Email from hello gallery</span></span>
2. <span data-ttu-id="8d606-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d606-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-hello-gallery"></a><span data-ttu-id="8d606-123">Добавить адрес электронной почты SkyDesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8d606-123">Adding SkyDesk Email from hello gallery</span></span>
<span data-ttu-id="8d606-124">tooconfigure hello Интеграция электронной почты SkyDesk в Azure AD, вы должны tooadd SkyDesk электронной почты из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8d606-124">tooconfigure hello integration of SkyDesk Email into Azure AD, you need tooadd SkyDesk Email from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8d606-125">**tooadd SkyDesk электронной почты из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d606-125">**tooadd SkyDesk Email from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d606-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8d606-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d606-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8d606-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8d606-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8d606-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8d606-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8d606-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8d606-133">Введите в поле поиска hello **SkyDesk электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="8d606-133">In hello search box, type **SkyDesk Email**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="8d606-135">В панели результатов hello, выберите **электронной почты SkyDesk**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8d606-135">In hello results panel, select **SkyDesk Email**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d606-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d606-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d606-138">В этом разделе описана настройка и проверка единого входа Azure AD в SkyDesk Email с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d606-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8d606-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в сообщении электронной почты SkyDesk является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d606-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SkyDesk Email is tooa user in Azure AD.</span></span> <span data-ttu-id="8d606-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в сообщении электронной почты SkyDesk должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8d606-140">In other words, a link relationship between an Azure AD user and hello related user in SkyDesk Email needs toobe established.</span></span>

<span data-ttu-id="8d606-141">В сообщении электронной почты SkyDesk, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="8d606-141">In SkyDesk Email, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8d606-142">tooconfigure и теста Azure AD единого входа с SkyDesk электронной почты, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8d606-142">tooconfigure and test Azure AD single sign-on with SkyDesk Email, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8d606-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8d606-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8d606-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8d606-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d606-145">**[Создание тестового пользователя по электронной почте SkyDesk](#creating-a-skydesk-email-test-user)**  -toohave аналог Саймон Britta в SkyDesk электронной почты, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8d606-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - toohave a counterpart of Britta Simon in SkyDesk Email that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d606-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8d606-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d606-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8d606-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d606-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d606-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d606-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении SkyDesk электронной почты.</span><span class="sxs-lookup"><span data-stu-id="8d606-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="8d606-150">**tooconfigure Azure AD единого входа с SkyDesk электронной почты, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d606-150">**tooconfigure Azure AD single sign-on with SkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d606-151">В hello в hello портала Azure **электронной почты SkyDesk** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8d606-151">In hello Azure portal, on hello **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8d606-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8d606-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="8d606-155">На hello **SkyDesk домена электронной почты и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d606-155">On hello **SkyDesk Email Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="8d606-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8d606-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d606-158">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="8d606-158">hello value is not real.</span></span> <span data-ttu-id="8d606-159">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="8d606-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="8d606-160">Обратитесь к [SkyDesk клиента электронной почты поддержки](https://www.skydesk.sg/support/) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="8d606-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="8d606-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8d606-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="8d606-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8d606-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8d606-165">На hello **конфигурации электронной почты SkyDesk** щелкните **настройки электронной почты SkyDesk** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="8d606-165">On hello **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8d606-166">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="8d606-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="8d606-168">tooenable единого входа в **SkyDesk по электронной почте**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d606-168">tooenable SSO in **SkyDesk Email**, perform hello following steps:</span></span>

    <span data-ttu-id="8d606-169">а.</span><span class="sxs-lookup"><span data-stu-id="8d606-169">a.</span></span> <span data-ttu-id="8d606-170">Вход tooyour SkyDesk электронной почты учетной записи, от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="8d606-170">Sign-on tooyour SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="8d606-171">b.</span><span class="sxs-lookup"><span data-stu-id="8d606-171">b.</span></span> <span data-ttu-id="8d606-172">В меню в верхней части hello hello выберите **установки**и выберите **Org**.</span><span class="sxs-lookup"><span data-stu-id="8d606-172">In hello menu on hello top, click **Setup**, and select **Org**.</span></span> 
    
      ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="8d606-174">c.</span><span class="sxs-lookup"><span data-stu-id="8d606-174">c.</span></span> <span data-ttu-id="8d606-175">Щелкните **домены** из левой панели hello.</span><span class="sxs-lookup"><span data-stu-id="8d606-175">Click on **Domains** from hello left panel.</span></span>
    
      ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="8d606-177">г)</span><span class="sxs-lookup"><span data-stu-id="8d606-177">d.</span></span> <span data-ttu-id="8d606-178">Щелкните **Add Domain** (Добавить домен).</span><span class="sxs-lookup"><span data-stu-id="8d606-178">Click on **Add Domain**.</span></span>
    
      ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="8d606-180">д.</span><span class="sxs-lookup"><span data-stu-id="8d606-180">e.</span></span> <span data-ttu-id="8d606-181">Введите имя домена и установите hello домена.</span><span class="sxs-lookup"><span data-stu-id="8d606-181">Enter your Domain name, and then verify hello Domain.</span></span>
    
      ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="8d606-183">f.</span><span class="sxs-lookup"><span data-stu-id="8d606-183">f.</span></span> <span data-ttu-id="8d606-184">Щелкните **проверку подлинности SAML** из левой панели hello.</span><span class="sxs-lookup"><span data-stu-id="8d606-184">Click on **SAML Authentication** from hello left panel.</span></span>
    
      ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="8d606-186">На hello **проверку подлинности SAML** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d606-186">On hello **SAML Authentication** dialog page, perform hello following steps:</span></span>
   
      ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="8d606-188">Проверка подлинности на основе toouse SAML, должны быть установлены **проверенного домена** или **портала URL-адрес** установки.</span><span class="sxs-lookup"><span data-stu-id="8d606-188">toouse SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="8d606-189">Можно установить портал hello URL-адрес с уникальным именем hello.</span><span class="sxs-lookup"><span data-stu-id="8d606-189">You can set hello portal URL with hello unique name.</span></span>
    > 
    > 
   
    ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="8d606-191">а.</span><span class="sxs-lookup"><span data-stu-id="8d606-191">a.</span></span> <span data-ttu-id="8d606-192">В hello **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8d606-192">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="8d606-193">b.</span><span class="sxs-lookup"><span data-stu-id="8d606-193">b.</span></span> <span data-ttu-id="8d606-194">В hello **выхода** URL-адрес в текстовое поле значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8d606-194">In hello **Logout** URL textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8d606-195">c.</span><span class="sxs-lookup"><span data-stu-id="8d606-195">c.</span></span> <span data-ttu-id="8d606-196">**Изменить URL-адрес пароля** является необязательным, поэтому оставьте его пустым.</span><span class="sxs-lookup"><span data-stu-id="8d606-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="8d606-197">d.</span><span class="sxs-lookup"><span data-stu-id="8d606-197">d.</span></span> <span data-ttu-id="8d606-198">Щелкните **получить ключ из файла** tooselect загруженный сертификат на портал Azure и нажмите кнопку **откройте** tooupload hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="8d606-198">Click on **Get Key From File** tooselect your downloaded certificate from Azure portal, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="8d606-199">д.</span><span class="sxs-lookup"><span data-stu-id="8d606-199">e.</span></span> <span data-ttu-id="8d606-200">В поле **Algorithm** (Алгоритм) задайте значение **RSA**.</span><span class="sxs-lookup"><span data-stu-id="8d606-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="8d606-201">f.</span><span class="sxs-lookup"><span data-stu-id="8d606-201">f.</span></span> <span data-ttu-id="8d606-202">Нажмите кнопку **ОК** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="8d606-202">Click **Ok** toosave hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="8d606-203">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="8d606-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8d606-204">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="8d606-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8d606-205">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d606-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d606-206">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d606-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d606-207">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8d606-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8d606-209">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d606-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d606-210">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8d606-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d606-212">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8d606-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d606-214">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="8d606-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d606-216">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d606-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d606-218">а.</span><span class="sxs-lookup"><span data-stu-id="8d606-218">a.</span></span> <span data-ttu-id="8d606-219">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d606-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d606-220">b.</span><span class="sxs-lookup"><span data-stu-id="8d606-220">b.</span></span> <span data-ttu-id="8d606-221">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8d606-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d606-222">c.</span><span class="sxs-lookup"><span data-stu-id="8d606-222">c.</span></span> <span data-ttu-id="8d606-223">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="8d606-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8d606-224">d.</span><span class="sxs-lookup"><span data-stu-id="8d606-224">d.</span></span> <span data-ttu-id="8d606-225">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8d606-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="8d606-226">Создание тестового пользователя SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="8d606-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="8d606-227">В этом разделе описано, как создать пользователя Britta Simon в приложении SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="8d606-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="8d606-228">Щелкните **доступа пользователей** из hello слева панели в SkyDesk электронной почты, а затем введите свое имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="8d606-228">Click on **User Access** from hello left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="8d606-230">При необходимости пользователи массового toocreate требуется toocontact hello [SkyDesk клиента электронной почты поддержки](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="8d606-230">If you need toocreate bulk users, you need toocontact hello [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8d606-231">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8d606-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8d606-232">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSkyDesk электронной почты.</span><span class="sxs-lookup"><span data-stu-id="8d606-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkyDesk Email.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8d606-234">**tooassign tooSkyDesk Britta Simon электронной почты, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="8d606-234">**tooassign Britta Simon tooSkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d606-235">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8d606-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8d606-237">В списке приложений hello выберите **SkyDesk электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="8d606-237">In hello applications list, select **SkyDesk Email**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="8d606-239">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8d606-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8d606-241">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8d606-241">Click **Add** button.</span></span> <span data-ttu-id="8d606-242">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8d606-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8d606-244">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8d606-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8d606-245">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8d606-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d606-246">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8d606-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d606-247">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8d606-247">Testing single sign-on</span></span>

<span data-ttu-id="8d606-248">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="8d606-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="8d606-249">При нажатии кнопки hello электронной почты SkyDesk плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour приложения SkyDesk электронной почты.</span><span class="sxs-lookup"><span data-stu-id="8d606-249">When you click hello SkyDesk Email tile in hello Access Panel, you should get automatically signed-on tooyour SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d606-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8d606-250">Additional resources</span></span>

* [<span data-ttu-id="8d606-251">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d606-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d606-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d606-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

