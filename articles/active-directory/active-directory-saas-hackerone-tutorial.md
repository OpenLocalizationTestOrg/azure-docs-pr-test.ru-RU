---
title: "Руководство по интеграции Azure Active Directory с HackerOne | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Hackerone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: c9dc033e26e79a7233dcfb3899c62684d4a19652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="a56ea-103">Учебник. Интеграция Azure Active Directory с HackerOn</span><span class="sxs-lookup"><span data-stu-id="a56ea-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="a56ea-104">В этом учебнике вы узнаете, как toointegrate HackerOne с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a56ea-104">In this tutorial, you learn how toointegrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a56ea-105">Интеграция с Azure AD HackerOne предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a56ea-105">Integrating HackerOne with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a56ea-106">Можно управлять в Azure AD, имеющего доступ tooHackerOne</span><span class="sxs-lookup"><span data-stu-id="a56ea-106">You can control in Azure AD who has access tooHackerOne</span></span>
- <span data-ttu-id="a56ea-107">Можно включить на пользователей tooautomatically get вошедшего tooHackerOne (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="a56ea-107">You can enable your users tooautomatically get signed-on tooHackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a56ea-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a56ea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a56ea-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a56ea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a56ea-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a56ea-110">Prerequisites</span></span>

<span data-ttu-id="a56ea-111">tooconfigure интеграция Azure AD с HackerOne требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a56ea-111">tooconfigure Azure AD integration with HackerOne, you need hello following items:</span></span>

- <span data-ttu-id="a56ea-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a56ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a56ea-113">подписка с поддержкой единого входа HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a56ea-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a56ea-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a56ea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a56ea-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a56ea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a56ea-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a56ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a56ea-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a56ea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a56ea-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a56ea-118">Scenario description</span></span>
<span data-ttu-id="a56ea-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a56ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a56ea-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a56ea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a56ea-121">Добавление HackerOne из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a56ea-121">Adding HackerOne from hello gallery</span></span>
2. <span data-ttu-id="a56ea-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a56ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-hello-gallery"></a><span data-ttu-id="a56ea-123">Добавление HackerOne из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a56ea-123">Adding HackerOne from hello gallery</span></span>
<span data-ttu-id="a56ea-124">tooconfigure hello интеграции HackerOne в Azure AD, вы должны tooadd HackerOne из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a56ea-124">tooconfigure hello integration of HackerOne into Azure AD, you need tooadd HackerOne from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a56ea-125">**tooadd HackerOne из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a56ea-125">**tooadd HackerOne from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a56ea-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a56ea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a56ea-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a56ea-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a56ea-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a56ea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a56ea-133">Введите в поле поиска hello **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-133">In hello search box, type **HackerOne**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="a56ea-135">В панели результатов hello выберите **HackerOne**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a56ea-135">In hello results panel, select **HackerOne**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a56ea-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a56ea-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a56ea-138">В этом разделе описана настройка и проверка единого входа Azure AD в HackerOne с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a56ea-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a56ea-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в HackerOne является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a56ea-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HackerOne is tooa user in Azure AD.</span></span> <span data-ttu-id="a56ea-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в HackerOne должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a56ea-140">In other words, a link relationship between an Azure AD user and hello related user in HackerOne needs toobe established.</span></span>

<span data-ttu-id="a56ea-141">В HackerOne, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a56ea-141">In HackerOne, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a56ea-142">tooconfigure и теста Azure AD единого входа с HackerOne, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a56ea-142">tooconfigure and test Azure AD single sign-on with HackerOne, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a56ea-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a56ea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a56ea-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a56ea-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a56ea-145">**[Создание тестового пользователя HackerOne](#creating-a-hackerone-test-user)**  -toohave аналог Саймон Britta в HackerOne, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a56ea-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - toohave a counterpart of Britta Simon in HackerOne that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a56ea-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a56ea-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a56ea-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a56ea-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a56ea-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a56ea-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a56ea-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a56ea-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="a56ea-150">**tooconfigure Azure AD единого входа с HackerOne, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a56ea-150">**tooconfigure Azure AD single sign-on with HackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="a56ea-151">В hello в hello портала Azure **HackerOne** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-151">In hello Azure portal, on hello **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a56ea-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a56ea-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="a56ea-155">На hello **HackerOne один URL-адрес входа и идентификатор** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a56ea-155">On hello **HackerOne Single sign-on URL and Identifier** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="a56ea-157">а.</span><span class="sxs-lookup"><span data-stu-id="a56ea-157">a.</span></span> <span data-ttu-id="a56ea-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="a56ea-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="a56ea-159">b.</span><span class="sxs-lookup"><span data-stu-id="a56ea-159">b.</span></span> <span data-ttu-id="a56ea-160">В hello **идентификатор** текстовом поле введите URL-адрес как:`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="a56ea-160">In hello **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="a56ea-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="a56ea-161">This value is not real.</span></span> <span data-ttu-id="a56ea-162">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="a56ea-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="a56ea-163">Обратитесь к [HackerOne поддержки](mailto:support@hackerone.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="a56ea-163">Contact [HackerOne support team](mailto:support@hackerone.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="a56ea-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a56ea-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="a56ea-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a56ea-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a56ea-168">На hello **конфигурации HackerOne** щелкните **Настройка HackerOne** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="a56ea-168">On hello **HackerOne Configuration** section, click **Configure HackerOne** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a56ea-169">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="a56ea-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="a56ea-171">Вход tooyour HackerOne клиента с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a56ea-171">Sign On tooyour HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="a56ea-172">В меню в верхней части hello hello щелкните hello»**параметры**.»</span><span class="sxs-lookup"><span data-stu-id="a56ea-172">In hello menu on hello top, click hello "**Settings**."</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="a56ea-174">Перейдите слишком»**проверки подлинности**«и нажмите кнопку»**добавить параметры SAML**.»</span><span class="sxs-lookup"><span data-stu-id="a56ea-174">Navigate too"**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="a56ea-176">На hello **параметры SAML** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a56ea-176">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="a56ea-178">а.</span><span class="sxs-lookup"><span data-stu-id="a56ea-178">a.</span></span> <span data-ttu-id="a56ea-179">В hello **домена электронной почты** текстовом поле введите зарегистрированный домен.</span><span class="sxs-lookup"><span data-stu-id="a56ea-179">In hello **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="a56ea-180">b.</span><span class="sxs-lookup"><span data-stu-id="a56ea-180">b.</span></span> <span data-ttu-id="a56ea-181">В **адрес единого входа** текстовые поля, вставьте значение hello **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a56ea-181">In  **Single Sign On URL** textboxes, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a56ea-182">c.</span><span class="sxs-lookup"><span data-stu-id="a56ea-182">c.</span></span> <span data-ttu-id="a56ea-183">Откройте ваш **файл сертификата** в блокноте, Скачанный с портала Azure скопируйте hello содержимое в буфер обмена, а затем вставьте его toohello **X509 сертификатов** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a56ea-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="a56ea-184">d.</span><span class="sxs-lookup"><span data-stu-id="a56ea-184">d.</span></span> <span data-ttu-id="a56ea-185">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-185">Click **Save**.</span></span>

11. <span data-ttu-id="a56ea-186">В диалоговом окне Параметры проверки подлинности hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="a56ea-186">On hello Authentication Settings dialog, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="a56ea-188">а.</span><span class="sxs-lookup"><span data-stu-id="a56ea-188">a.</span></span> <span data-ttu-id="a56ea-189">Щелкните **Run test**(Выполнить проверку).</span><span class="sxs-lookup"><span data-stu-id="a56ea-189">Click **Run test**.</span></span>

    <span data-ttu-id="a56ea-190">b.</span><span class="sxs-lookup"><span data-stu-id="a56ea-190">b.</span></span> <span data-ttu-id="a56ea-191">Если hello значение hello **состояние** содержат значение **последнее состояние теста: создан**, обратитесь в службу вашей [HackerOne поддержки](mailto:support@hackerone.com) toorequest проверки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a56ea-191">If hello value of hello **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) toorequest a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="a56ea-192">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a56ea-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a56ea-193">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a56ea-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a56ea-194">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a56ea-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a56ea-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a56ea-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="a56ea-196">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a56ea-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a56ea-198">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a56ea-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a56ea-199">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a56ea-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a56ea-201">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a56ea-203">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a56ea-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a56ea-205">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a56ea-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a56ea-207">а.</span><span class="sxs-lookup"><span data-stu-id="a56ea-207">a.</span></span> <span data-ttu-id="a56ea-208">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a56ea-209">b.</span><span class="sxs-lookup"><span data-stu-id="a56ea-209">b.</span></span> <span data-ttu-id="a56ea-210">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a56ea-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a56ea-211">c.</span><span class="sxs-lookup"><span data-stu-id="a56ea-211">c.</span></span> <span data-ttu-id="a56ea-212">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a56ea-213">d.</span><span class="sxs-lookup"><span data-stu-id="a56ea-213">d.</span></span> <span data-ttu-id="a56ea-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="a56ea-215">Создание тестового пользователя HackerOne</span><span class="sxs-lookup"><span data-stu-id="a56ea-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="a56ea-216">Затем нужно создать пользователя Britta Simon в приложении HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a56ea-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="a56ea-217">Приложение HackerOne поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a56ea-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="a56ea-218">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="a56ea-218">There is no action item for you in this section.</span></span> <span data-ttu-id="a56ea-219">Новый пользователь, если он еще не существует, создается при доступе к HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a56ea-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a56ea-220">Если вам требуется toocreate пользователя вручную, необходимо группа поддержки Certify toocontact hello.</span><span class="sxs-lookup"><span data-stu-id="a56ea-220">If you need toocreate a user manually, you need toocontact hello Certify support team.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a56ea-221">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a56ea-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a56ea-222">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooHackerOne доступа.</span><span class="sxs-lookup"><span data-stu-id="a56ea-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHackerOne.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a56ea-224">**tooassign tooHackerOne Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a56ea-224">**tooassign Britta Simon tooHackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="a56ea-225">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a56ea-227">В списке приложений hello выберите **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-227">In hello applications list, select **HackerOne**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="a56ea-229">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a56ea-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-231">Click **Add** button.</span></span> <span data-ttu-id="a56ea-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a56ea-234">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a56ea-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a56ea-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a56ea-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a56ea-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a56ea-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a56ea-237">Testing single sign-on</span></span>

<span data-ttu-id="a56ea-238">Наконец при тестировании конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="a56ea-238">Finally, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="a56ea-239">При нажатии кнопки hello HackerOne плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour HackerOne приложения.</span><span class="sxs-lookup"><span data-stu-id="a56ea-239">When you click hello HackerOne tile in hello Access Panel, you should get automatically signed-on tooyour HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a56ea-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a56ea-240">Additional resources</span></span>

* [<span data-ttu-id="a56ea-241">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a56ea-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a56ea-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a56ea-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

