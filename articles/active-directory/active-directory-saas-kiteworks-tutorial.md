---
title: "Учебник по интеграции Azure Active Directory с Kiteworks | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Kiteworks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 406417dd7f58cc3f1fa0d9e86b5cad0c1d7be750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="297ea-103">Руководство по интеграции Azure Active Directory с Kiteworks</span><span class="sxs-lookup"><span data-stu-id="297ea-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="297ea-104">В этом учебнике вы узнаете, как toointegrate Kiteworks с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="297ea-104">In this tutorial, you learn how toointegrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="297ea-105">Интеграция с Azure AD Kiteworks предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="297ea-105">Integrating Kiteworks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="297ea-106">Можно управлять в Azure AD, имеющего доступ tooKiteworks</span><span class="sxs-lookup"><span data-stu-id="297ea-106">You can control in Azure AD who has access tooKiteworks</span></span>
- <span data-ttu-id="297ea-107">Можно включить на пользователей tooautomatically get вошедшего tooKiteworks (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="297ea-107">You can enable your users tooautomatically get signed-on tooKiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="297ea-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="297ea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="297ea-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="297ea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="297ea-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="297ea-110">Prerequisites</span></span>

<span data-ttu-id="297ea-111">tooconfigure интеграция Azure AD с Kiteworks требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="297ea-111">tooconfigure Azure AD integration with Kiteworks, you need hello following items:</span></span>

- <span data-ttu-id="297ea-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="297ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="297ea-113">подписка Kiteworks с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="297ea-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="297ea-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="297ea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="297ea-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="297ea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="297ea-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="297ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="297ea-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="297ea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="297ea-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="297ea-118">Scenario description</span></span>
<span data-ttu-id="297ea-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="297ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="297ea-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="297ea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="297ea-121">Добавление Kiteworks из галереи hello</span><span class="sxs-lookup"><span data-stu-id="297ea-121">Adding Kiteworks from hello gallery</span></span>
2. <span data-ttu-id="297ea-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="297ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-hello-gallery"></a><span data-ttu-id="297ea-123">Добавление Kiteworks из галереи hello</span><span class="sxs-lookup"><span data-stu-id="297ea-123">Adding Kiteworks from hello gallery</span></span>
<span data-ttu-id="297ea-124">tooconfigure hello интеграции Kiteworks в Azure AD, вы должны tooadd Kiteworks из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="297ea-124">tooconfigure hello integration of Kiteworks into Azure AD, you need tooadd Kiteworks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="297ea-125">**tooadd Kiteworks из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="297ea-125">**tooadd Kiteworks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="297ea-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="297ea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="297ea-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="297ea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="297ea-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="297ea-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="297ea-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="297ea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="297ea-133">Введите в поле поиска hello **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="297ea-133">In hello search box, type **Kiteworks**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="297ea-135">В панели результатов hello выберите **Kiteworks**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="297ea-135">In hello results panel, select **Kiteworks**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="297ea-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="297ea-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="297ea-138">В этом разделе описана настройка и проверка единого входа Azure AD в Kiteworks с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="297ea-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="297ea-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Kiteworks является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="297ea-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kiteworks is tooa user in Azure AD.</span></span> <span data-ttu-id="297ea-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Kiteworks должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="297ea-140">In other words, a link relationship between an Azure AD user and hello related user in Kiteworks needs toobe established.</span></span>

<span data-ttu-id="297ea-141">В Kiteworks, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="297ea-141">In Kiteworks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="297ea-142">tooconfigure и теста Azure AD единого входа с Kiteworks, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="297ea-142">tooconfigure and test Azure AD single sign-on with Kiteworks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="297ea-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="297ea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="297ea-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="297ea-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="297ea-145">**[Создание тестового пользователя Kiteworks](#creating-a-kiteworks-test-user)**  -toohave аналог Саймон Britta в Kiteworks, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="297ea-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - toohave a counterpart of Britta Simon in Kiteworks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="297ea-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="297ea-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="297ea-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="297ea-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="297ea-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="297ea-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="297ea-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="297ea-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="297ea-150">**tooconfigure Azure AD единого входа с Kiteworks, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="297ea-150">**tooconfigure Azure AD single sign-on with Kiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="297ea-151">В hello в hello портала Azure **Kiteworks** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="297ea-151">In hello Azure portal, on hello **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="297ea-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="297ea-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="297ea-155">На hello **URL-адреса и домена Kiteworks** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="297ea-155">On hello **Kiteworks Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="297ea-157">а.</span><span class="sxs-lookup"><span data-stu-id="297ea-157">a.</span></span> <span data-ttu-id="297ea-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="297ea-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="297ea-159">b.</span><span class="sxs-lookup"><span data-stu-id="297ea-159">b.</span></span> <span data-ttu-id="297ea-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="297ea-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="297ea-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="297ea-161">These values are not real.</span></span> <span data-ttu-id="297ea-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="297ea-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="297ea-163">Обратитесь к [группа поддержки клиента Kiteworks](http://accellion.com/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="297ea-163">Contact [Kiteworks Client support team](http://accellion.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="297ea-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="297ea-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="297ea-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="297ea-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="297ea-168">На hello **конфигурации Kiteworks** щелкните **Настройка Kiteworks** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="297ea-168">On hello **Kiteworks Configuration** section, click **Configure Kiteworks** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="297ea-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="297ea-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="297ea-171">Войдите на tooyour Kiteworks корпоративный сайт с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="297ea-171">Sign on tooyour Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="297ea-172">Щелкните hello панели инструментов в верхней части hello **параметры**.</span><span class="sxs-lookup"><span data-stu-id="297ea-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="297ea-174">В hello **проверки подлинности и авторизации** щелкните **настройки единого входа**.</span><span class="sxs-lookup"><span data-stu-id="297ea-174">In hello **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="297ea-176">На странице настройки единого входа hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="297ea-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="297ea-178">а.</span><span class="sxs-lookup"><span data-stu-id="297ea-178">a.</span></span> <span data-ttu-id="297ea-179">Установите флажок **Проверка подлинности с помощью единого входа**.</span><span class="sxs-lookup"><span data-stu-id="297ea-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="297ea-180">b.</span><span class="sxs-lookup"><span data-stu-id="297ea-180">b.</span></span> <span data-ttu-id="297ea-181">Выберите **Initiate AuthnRequest**(Инициировать запрос на проверку подлинности).</span><span class="sxs-lookup"><span data-stu-id="297ea-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="297ea-182">c.</span><span class="sxs-lookup"><span data-stu-id="297ea-182">c.</span></span> <span data-ttu-id="297ea-183">В hello **идентификатор сущности поставщика Удостоверений** текстовое значение hello вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="297ea-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="297ea-184">d.</span><span class="sxs-lookup"><span data-stu-id="297ea-184">d.</span></span> <span data-ttu-id="297ea-185">В hello **единого входа URL-адрес службы** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="297ea-185">In hello **Single Sign-On Service URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="297ea-186">д.</span><span class="sxs-lookup"><span data-stu-id="297ea-186">e.</span></span> <span data-ttu-id="297ea-187">В hello **URL-адрес службы единого выхода** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="297ea-187">In hello **Single Logout Service URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="297ea-188">f.</span><span class="sxs-lookup"><span data-stu-id="297ea-188">f.</span></span> <span data-ttu-id="297ea-189">Откройте загруженный сертификат в блокноте, hello копирования содержимого, а затем вставьте его в hello **сертификат открытого ключа RSA** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="297ea-189">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="297ea-190">ж.</span><span class="sxs-lookup"><span data-stu-id="297ea-190">g.</span></span> <span data-ttu-id="297ea-191">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="297ea-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="297ea-192">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="297ea-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="297ea-193">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="297ea-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="297ea-194">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="297ea-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="297ea-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="297ea-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="297ea-196">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="297ea-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="297ea-198">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="297ea-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="297ea-199">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="297ea-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="297ea-201">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="297ea-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="297ea-203">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="297ea-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="297ea-205">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="297ea-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="297ea-207">а.</span><span class="sxs-lookup"><span data-stu-id="297ea-207">a.</span></span> <span data-ttu-id="297ea-208">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="297ea-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="297ea-209">b.</span><span class="sxs-lookup"><span data-stu-id="297ea-209">b.</span></span> <span data-ttu-id="297ea-210">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="297ea-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="297ea-211">c.</span><span class="sxs-lookup"><span data-stu-id="297ea-211">c.</span></span> <span data-ttu-id="297ea-212">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="297ea-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="297ea-213">d.</span><span class="sxs-lookup"><span data-stu-id="297ea-213">d.</span></span> <span data-ttu-id="297ea-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="297ea-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="297ea-215">Создание тестового пользователя Kiteworks</span><span class="sxs-lookup"><span data-stu-id="297ea-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="297ea-216">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="297ea-216">hello objective of this section is toocreate a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="297ea-217">Приложение Kiteworks поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="297ea-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="297ea-218">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="297ea-218">There is no action item for you in this section.</span></span> <span data-ttu-id="297ea-219">Новый пользователь создается во время попытки tooaccess Kitewors, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="297ea-219">A new user is created during an attempt tooaccess Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="297ea-220">Если требуется toocreate пользователя вручную, необходимо toocontact hello [Kiteworks поддержки](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="297ea-220">If you need toocreate a user manually, you need toocontact hello [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="297ea-221">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="297ea-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="297ea-222">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooKiteworks доступа.</span><span class="sxs-lookup"><span data-stu-id="297ea-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKiteworks.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="297ea-224">**tooassign tooKiteworks Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="297ea-224">**tooassign Britta Simon tooKiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="297ea-225">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="297ea-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="297ea-227">В списке приложений hello выберите **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="297ea-227">In hello applications list, select **Kiteworks**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="297ea-229">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="297ea-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="297ea-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="297ea-231">Click **Add** button.</span></span> <span data-ttu-id="297ea-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="297ea-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="297ea-234">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="297ea-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="297ea-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="297ea-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="297ea-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="297ea-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="297ea-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="297ea-237">Testing single sign-on</span></span>

<span data-ttu-id="297ea-238">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="297ea-238">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="297ea-239">При нажатии кнопки Kiteworks плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Kiteworks приложения.</span><span class="sxs-lookup"><span data-stu-id="297ea-239">When you click hello Kiteworks tile in hello Access Panel, you should get automatically signed-on tooyour Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="297ea-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="297ea-240">Additional resources</span></span>

* [<span data-ttu-id="297ea-241">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="297ea-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="297ea-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="297ea-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

