---
title: "Руководство по интеграции Azure Active Directory с Kintone | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Kintone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="96ba8-103">Руководство по интеграции Azure Active Directory с Kintone</span><span class="sxs-lookup"><span data-stu-id="96ba8-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="96ba8-104">В этом учебнике вы узнаете, как toointegrate Kintone с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96ba8-104">In this tutorial, you learn how toointegrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96ba8-105">Интеграция Kintone с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="96ba8-105">Integrating Kintone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="96ba8-106">Можно управлять в Azure AD, имеющего доступ tooKintone</span><span class="sxs-lookup"><span data-stu-id="96ba8-106">You can control in Azure AD who has access tooKintone</span></span>
- <span data-ttu-id="96ba8-107">Можно включить на пользователей tooautomatically get вошедшего tooKintone (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="96ba8-107">You can enable your users tooautomatically get signed-on tooKintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96ba8-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="96ba8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="96ba8-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96ba8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96ba8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="96ba8-110">Prerequisites</span></span>

<span data-ttu-id="96ba8-111">tooconfigure интеграция Azure AD с Kintone, необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="96ba8-111">tooconfigure Azure AD integration with Kintone, you need hello following items:</span></span>

- <span data-ttu-id="96ba8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="96ba8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96ba8-113">Подписка с поддержкой единого входа Kintone</span><span class="sxs-lookup"><span data-stu-id="96ba8-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96ba8-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="96ba8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96ba8-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="96ba8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96ba8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="96ba8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96ba8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96ba8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96ba8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="96ba8-118">Scenario description</span></span>
<span data-ttu-id="96ba8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="96ba8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96ba8-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="96ba8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96ba8-121">Добавление Kintone из галереи hello</span><span class="sxs-lookup"><span data-stu-id="96ba8-121">Adding Kintone from hello gallery</span></span>
2. <span data-ttu-id="96ba8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="96ba8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-hello-gallery"></a><span data-ttu-id="96ba8-123">Добавление Kintone из галереи hello</span><span class="sxs-lookup"><span data-stu-id="96ba8-123">Adding Kintone from hello gallery</span></span>
<span data-ttu-id="96ba8-124">tooconfigure hello интеграции Kintone в Azure AD, вы должны tooadd Kintone из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="96ba8-124">tooconfigure hello integration of Kintone into Azure AD, you need tooadd Kintone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="96ba8-125">**tooadd Kintone из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96ba8-125">**tooadd Kintone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="96ba8-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="96ba8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="96ba8-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="96ba8-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="96ba8-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="96ba8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="96ba8-133">Введите в поле поиска hello **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-133">In hello search box, type **Kintone**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="96ba8-135">В панели результатов hello выберите **Kintone**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="96ba8-135">In hello results panel, select **Kintone**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96ba8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="96ba8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96ba8-138">В этом разделе описана настройка и проверка единого входа Azure AD в Kintone для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96ba8-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96ba8-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Kintone является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96ba8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kintone is tooa user in Azure AD.</span></span> <span data-ttu-id="96ba8-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Kintone должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="96ba8-140">In other words, a link relationship between an Azure AD user and hello related user in Kintone needs toobe established.</span></span>

<span data-ttu-id="96ba8-141">В Kintone, присвоить значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="96ba8-141">In Kintone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="96ba8-142">tooconfigure и теста Azure AD единого входа с Kintone, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="96ba8-142">tooconfigure and test Azure AD single sign-on with Kintone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="96ba8-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="96ba8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="96ba8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="96ba8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96ba8-145">**[Создание тестового пользователя Kintone](#creating-a-kintone-test-user)**  -toohave аналог Саймон Britta в Kintone, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="96ba8-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - toohave a counterpart of Britta Simon in Kintone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="96ba8-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="96ba8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96ba8-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="96ba8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96ba8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="96ba8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96ba8-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении-Kintone.</span><span class="sxs-lookup"><span data-stu-id="96ba8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="96ba8-150">**tooconfigure Azure AD единого входа с Kintone, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96ba8-150">**tooconfigure Azure AD single sign-on with Kintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="96ba8-151">В hello в hello портала Azure **Kintone** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-151">In hello Azure portal, on hello **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="96ba8-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="96ba8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="96ba8-155">На hello **URL-адреса и домена Kintone** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="96ba8-155">On hello **Kintone Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="96ba8-157">а.</span><span class="sxs-lookup"><span data-stu-id="96ba8-157">a.</span></span> <span data-ttu-id="96ba8-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="96ba8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="96ba8-159">b.</span><span class="sxs-lookup"><span data-stu-id="96ba8-159">b.</span></span> <span data-ttu-id="96ba8-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="96ba8-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="96ba8-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="96ba8-161">These values are not real.</span></span> <span data-ttu-id="96ba8-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="96ba8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="96ba8-163">Обратитесь к [группа поддержки клиента Kintone](https://www.kintone.com/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="96ba8-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="96ba8-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="96ba8-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="96ba8-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="96ba8-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="96ba8-168">На hello **конфигурации Kintone** щелкните **Настройка Kintone** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="96ba8-168">On hello **Kintone Configuration** section, click **Configure Kintone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="96ba8-169">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="96ba8-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="96ba8-171">В другом окне веб-браузера войдите на веб-сайт **Kintone** компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="96ba8-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="96ba8-172">Щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="96ba8-173">![Параметры](./media/active-directory-saas-kintone-tutorial/ic785879.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="96ba8-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="96ba8-174">Щелкните **Users & System Administration** (Администрирование пользователей и системы).</span><span class="sxs-lookup"><span data-stu-id="96ba8-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="96ba8-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration") (Администрирование пользователей и системы)</span><span class="sxs-lookup"><span data-stu-id="96ba8-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="96ba8-176">Перейдите в раздел **System Administration \> Security** (Системное администрирование > Безопасность) и щелкните **Login** (Вход).</span><span class="sxs-lookup"><span data-stu-id="96ba8-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="96ba8-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login") (Вход)</span><span class="sxs-lookup"><span data-stu-id="96ba8-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="96ba8-178">Установите флажок **Включить проверку подлинности SAML**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="96ba8-179">![Аутентификация SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "Аутентификация SAML")</span><span class="sxs-lookup"><span data-stu-id="96ba8-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="96ba8-180">В hello раздел проверки подлинности SAML выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="96ba8-180">In hello SAML Authentication section, perform hello following steps:</span></span>
    
    <span data-ttu-id="96ba8-181">![Аутентификация SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "Аутентификация SAML")</span><span class="sxs-lookup"><span data-stu-id="96ba8-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="96ba8-182">а.</span><span class="sxs-lookup"><span data-stu-id="96ba8-182">a.</span></span> <span data-ttu-id="96ba8-183">В hello **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="96ba8-183">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="96ba8-184">b.</span><span class="sxs-lookup"><span data-stu-id="96ba8-184">b.</span></span> <span data-ttu-id="96ba8-185">В hello **URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="96ba8-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="96ba8-186">c.</span><span class="sxs-lookup"><span data-stu-id="96ba8-186">c.</span></span> <span data-ttu-id="96ba8-187">Нажмите кнопку **Обзор** tooupload загруженный сертификат.</span><span class="sxs-lookup"><span data-stu-id="96ba8-187">Click **Browse** tooupload your downloaded certificate.</span></span>
    
    <span data-ttu-id="96ba8-188">d.</span><span class="sxs-lookup"><span data-stu-id="96ba8-188">d.</span></span> <span data-ttu-id="96ba8-189">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="96ba8-190">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="96ba8-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="96ba8-191">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="96ba8-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="96ba8-192">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96ba8-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96ba8-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="96ba8-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="96ba8-194">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="96ba8-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="96ba8-196">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96ba8-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="96ba8-197">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="96ba8-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96ba8-199">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96ba8-201">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="96ba8-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96ba8-203">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="96ba8-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96ba8-205">а.</span><span class="sxs-lookup"><span data-stu-id="96ba8-205">a.</span></span> <span data-ttu-id="96ba8-206">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96ba8-207">b.</span><span class="sxs-lookup"><span data-stu-id="96ba8-207">b.</span></span> <span data-ttu-id="96ba8-208">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="96ba8-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96ba8-209">c.</span><span class="sxs-lookup"><span data-stu-id="96ba8-209">c.</span></span> <span data-ttu-id="96ba8-210">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="96ba8-211">d.</span><span class="sxs-lookup"><span data-stu-id="96ba8-211">d.</span></span> <span data-ttu-id="96ba8-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="96ba8-213">Создание тестового пользователя Kintone</span><span class="sxs-lookup"><span data-stu-id="96ba8-213">Creating a Kintone test user</span></span>

<span data-ttu-id="96ba8-214">Пользователи toolog tooenable Azure AD в tooKintone, их необходимо подготовить в Kintone.</span><span class="sxs-lookup"><span data-stu-id="96ba8-214">tooenable Azure AD users toolog in tooKintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="96ba8-215">В случае hello объекта Kintone Подготовка осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="96ba8-215">In hello case of Kintone, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="96ba8-216">tooprovision учетной записи пользователя, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="96ba8-216">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="96ba8-217">Войдите в tooyour **Kintone** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="96ba8-217">Log in tooyour **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="96ba8-218">Щелкните **Параметр**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="96ba8-219">![Параметры](./media/active-directory-saas-kintone-tutorial/ic785879.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="96ba8-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="96ba8-220">Щелкните **Users & System Administration** (Администрирование пользователей и системы).</span><span class="sxs-lookup"><span data-stu-id="96ba8-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="96ba8-221">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration") (Администрирование пользователей и системы)</span><span class="sxs-lookup"><span data-stu-id="96ba8-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="96ba8-222">В разделе **User Administration** (Администрирование пользователей) щелкните **Departments & Users** (Отделы и пользователи).</span><span class="sxs-lookup"><span data-stu-id="96ba8-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="96ba8-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users") (Отделы и пользователи)</span><span class="sxs-lookup"><span data-stu-id="96ba8-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="96ba8-224">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-224">Click **New User**.</span></span>
   
    <span data-ttu-id="96ba8-225">![Новые пользователи](./media/active-directory-saas-kintone-tutorial/ic785889.png "Новые пользователи")</span><span class="sxs-lookup"><span data-stu-id="96ba8-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="96ba8-226">В hello **нового пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="96ba8-226">In hello **New User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="96ba8-227">![Новые пользователи](./media/active-directory-saas-kintone-tutorial/ic785890.png "Новые пользователи")</span><span class="sxs-lookup"><span data-stu-id="96ba8-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="96ba8-228">а.</span><span class="sxs-lookup"><span data-stu-id="96ba8-228">a.</span></span> <span data-ttu-id="96ba8-229">Введите значение **отображаемое имя**, **имя входа**, **новый пароль**, **подтверждение пароля**, **адрес электронной почты**, и другие сведения о действительной учетной записи AAD, требуется tooprovision в hello связаны текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="96ba8-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
 
    <span data-ttu-id="96ba8-230">b.</span><span class="sxs-lookup"><span data-stu-id="96ba8-230">b.</span></span> <span data-ttu-id="96ba8-231">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="96ba8-232">Можно использовать любые другие Kintone пользователя средства создания учетных записей или интерфейсы API, предоставляемые Kintone tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="96ba8-232">You can use any other Kintone user account creation tools or APIs provided by Kintone tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="96ba8-233">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="96ba8-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="96ba8-234">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooKintone доступа.</span><span class="sxs-lookup"><span data-stu-id="96ba8-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKintone.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="96ba8-236">**tooassign tooKintone Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96ba8-236">**tooassign Britta Simon tooKintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="96ba8-237">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="96ba8-239">В списке приложений hello выберите **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-239">In hello applications list, select **Kintone**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="96ba8-241">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="96ba8-243">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-243">Click **Add** button.</span></span> <span data-ttu-id="96ba8-244">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="96ba8-246">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="96ba8-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="96ba8-247">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96ba8-248">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="96ba8-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="96ba8-249">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="96ba8-249">Testing single sign-on</span></span>

<span data-ttu-id="96ba8-250">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="96ba8-250">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="96ba8-251">При нажатии кнопки hello Kintone плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour Kintone.</span><span class="sxs-lookup"><span data-stu-id="96ba8-251">When you click hello Kintone tile in hello Access Panel, you should get automatically signed-on tooyour Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96ba8-252">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="96ba8-252">Additional resources</span></span>

* [<span data-ttu-id="96ba8-253">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96ba8-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96ba8-254">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="96ba8-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

