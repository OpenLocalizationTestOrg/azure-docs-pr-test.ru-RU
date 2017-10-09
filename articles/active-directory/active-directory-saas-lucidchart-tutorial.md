---
title: "Учебник. Интеграция Azure Active Directory с Lucidchart | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Lucidchart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 774e5f423097650a3cae8e8ca13b2c65b8470736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="caa45-103">Руководство. Интеграция Azure Active Directory с Lucidchart</span><span class="sxs-lookup"><span data-stu-id="caa45-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="caa45-104">В этом учебнике вы узнаете, как toointegrate Lucidchart с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="caa45-104">In this tutorial, you learn how toointegrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="caa45-105">Интеграция Lucidchart с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="caa45-105">Integrating Lucidchart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="caa45-106">Можно управлять в Azure AD, имеющего доступ tooLucidchart</span><span class="sxs-lookup"><span data-stu-id="caa45-106">You can control in Azure AD who has access tooLucidchart</span></span>
- <span data-ttu-id="caa45-107">Можно включить на пользователей tooautomatically get вошедшего tooLucidchart (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="caa45-107">You can enable your users tooautomatically get signed-on tooLucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="caa45-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="caa45-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="caa45-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="caa45-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="caa45-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="caa45-110">Prerequisites</span></span>

<span data-ttu-id="caa45-111">tooconfigure интеграция Azure AD с Lucidchart требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="caa45-111">tooconfigure Azure AD integration with Lucidchart, you need hello following items:</span></span>

- <span data-ttu-id="caa45-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="caa45-112">An Azure AD subscription</span></span>
- <span data-ttu-id="caa45-113">Подписка с поддержкой единого входа Lucidchart</span><span class="sxs-lookup"><span data-stu-id="caa45-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="caa45-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="caa45-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="caa45-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="caa45-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="caa45-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="caa45-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="caa45-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="caa45-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="caa45-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="caa45-118">Scenario description</span></span>
<span data-ttu-id="caa45-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="caa45-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="caa45-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="caa45-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="caa45-121">Добавление Lucidchart из галереи hello</span><span class="sxs-lookup"><span data-stu-id="caa45-121">Adding Lucidchart from hello gallery</span></span>
2. <span data-ttu-id="caa45-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="caa45-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-hello-gallery"></a><span data-ttu-id="caa45-123">Добавление Lucidchart из галереи hello</span><span class="sxs-lookup"><span data-stu-id="caa45-123">Adding Lucidchart from hello gallery</span></span>
<span data-ttu-id="caa45-124">tooconfigure hello интеграции Lucidchart в Azure AD, вы должны tooadd Lucidchart из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="caa45-124">tooconfigure hello integration of Lucidchart into Azure AD, you need tooadd Lucidchart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="caa45-125">**tooadd Lucidchart из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="caa45-125">**tooadd Lucidchart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="caa45-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="caa45-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="caa45-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="caa45-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="caa45-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="caa45-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="caa45-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="caa45-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="caa45-133">Введите в поле поиска hello **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="caa45-133">In hello search box, type **Lucidchart**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="caa45-135">В панели результатов hello выберите **Lucidchart**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="caa45-135">In hello results panel, select **Lucidchart**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="caa45-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="caa45-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="caa45-138">В этом разделе описана настройка и проверка единого входа Azure AD в Lucidchart с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="caa45-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="caa45-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Lucidchart является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="caa45-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lucidchart is tooa user in Azure AD.</span></span> <span data-ttu-id="caa45-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Lucidchart должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="caa45-140">In other words, a link relationship between an Azure AD user and hello related user in Lucidchart needs toobe established.</span></span>

<span data-ttu-id="caa45-141">В Lucidchart, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="caa45-141">In Lucidchart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="caa45-142">tooconfigure и теста Azure AD единого входа с Lucidchart, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="caa45-142">tooconfigure and test Azure AD single sign-on with Lucidchart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="caa45-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="caa45-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="caa45-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="caa45-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="caa45-145">**[Создание тестового пользователя Lucidchart](#creating-a-lucidchart-test-user)**  -toohave аналог Саймон Britta в Lucidchart, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="caa45-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - toohave a counterpart of Britta Simon in Lucidchart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="caa45-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="caa45-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="caa45-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="caa45-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="caa45-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="caa45-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="caa45-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="caa45-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="caa45-150">**Azure AD tooconfigure единого входа с Lucidchart, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="caa45-150">**tooconfigure Azure AD single sign-on with Lucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="caa45-151">В hello в hello портала Azure **Lucidchart** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="caa45-151">In hello Azure portal, on hello **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="caa45-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="caa45-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="caa45-155">На hello **URL-адреса и домена Lucidchart** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="caa45-155">On hello **Lucidchart Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="caa45-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="caa45-157">In hello **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="caa45-158">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="caa45-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="caa45-160">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="caa45-160">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="caa45-162">В другом окне веб-браузера зайдите на веб-сайт компании Lucidchart в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="caa45-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="caa45-163">В меню в верхней части hello hello выберите **команды**.</span><span class="sxs-lookup"><span data-stu-id="caa45-163">In hello menu on hello top, click **Team**.</span></span>
   
    <span data-ttu-id="caa45-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team") (Команда)</span><span class="sxs-lookup"><span data-stu-id="caa45-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="caa45-165">Выберите **Приложение \> Управление SAML**.</span><span class="sxs-lookup"><span data-stu-id="caa45-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="caa45-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML") (Управление SAML)</span><span class="sxs-lookup"><span data-stu-id="caa45-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="caa45-167">На hello **параметры проверки подлинности SAML** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="caa45-167">On hello **SAML Authentication Settings** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="caa45-168">а.</span><span class="sxs-lookup"><span data-stu-id="caa45-168">a.</span></span> <span data-ttu-id="caa45-169">Установите флажок **Enable SAML Authentication** (Включить аутентификацию SAML), а затем выберите **Optional** (Необязательно).</span><span class="sxs-lookup"><span data-stu-id="caa45-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="caa45-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings") (Параметры аутентификации SAML)</span><span class="sxs-lookup"><span data-stu-id="caa45-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="caa45-171">b.</span><span class="sxs-lookup"><span data-stu-id="caa45-171">b.</span></span> <span data-ttu-id="caa45-172">В hello **домена** текстовом поле введите имя домена и нажмите кнопку **изменить сертификат**.</span><span class="sxs-lookup"><span data-stu-id="caa45-172">In hello **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="caa45-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate") (Изменить сертификат)</span><span class="sxs-lookup"><span data-stu-id="caa45-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="caa45-174">c.</span><span class="sxs-lookup"><span data-stu-id="caa45-174">c.</span></span> <span data-ttu-id="caa45-175">Откройте скачанный файл метаданных в hello копирования содержимого, а затем вставьте его в hello **Отправка метаданных** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="caa45-175">Open your downloaded metadata file, copy hello content, and then paste it into hello **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="caa45-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata") (Передача метаданных)</span><span class="sxs-lookup"><span data-stu-id="caa45-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="caa45-177">d.</span><span class="sxs-lookup"><span data-stu-id="caa45-177">d.</span></span> <span data-ttu-id="caa45-178">Выберите **автоматически добавлять новые команды toohello пользователей**, а затем нажмите кнопку **сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="caa45-178">Select **Automatically Add new users toohello team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="caa45-179">![Сохранение изменений](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Сохранение изменений")</span><span class="sxs-lookup"><span data-stu-id="caa45-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="caa45-180">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="caa45-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="caa45-181">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="caa45-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="caa45-182">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="caa45-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="caa45-183">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="caa45-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="caa45-184">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="caa45-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="caa45-186">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="caa45-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="caa45-187">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="caa45-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="caa45-189">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="caa45-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="caa45-191">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="caa45-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="caa45-193">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="caa45-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="caa45-195">а.</span><span class="sxs-lookup"><span data-stu-id="caa45-195">a.</span></span> <span data-ttu-id="caa45-196">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="caa45-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="caa45-197">b.</span><span class="sxs-lookup"><span data-stu-id="caa45-197">b.</span></span> <span data-ttu-id="caa45-198">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="caa45-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="caa45-199">c.</span><span class="sxs-lookup"><span data-stu-id="caa45-199">c.</span></span> <span data-ttu-id="caa45-200">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="caa45-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="caa45-201">d.</span><span class="sxs-lookup"><span data-stu-id="caa45-201">d.</span></span> <span data-ttu-id="caa45-202">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="caa45-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="caa45-203">Создание тестового пользователя Lucidchart</span><span class="sxs-lookup"><span data-stu-id="caa45-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="caa45-204">Нет элемента действия для вас tooconfigure подготовки пользователей tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="caa45-204">There is no action item for you tooconfigure user provisioning tooLucidchart.</span></span>  <span data-ttu-id="caa45-205">Когда назначенный пользователь пытается toolog в Lucidchart с помощью панели доступа hello, Lucidchart проверяет, существует ли пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="caa45-205">When an assigned user tries toolog into Lucidchart using hello access panel, Lucidchart checks whether hello user exists.</span></span>  

<span data-ttu-id="caa45-206">Если учетная запись пользователя отсутствует, Lucidchart автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="caa45-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="caa45-207">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="caa45-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="caa45-208">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLucidchart доступа.</span><span class="sxs-lookup"><span data-stu-id="caa45-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLucidchart.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="caa45-210">**tooassign tooLucidchart Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="caa45-210">**tooassign Britta Simon tooLucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="caa45-211">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="caa45-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="caa45-213">В списке приложений hello выберите **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="caa45-213">In hello applications list, select **Lucidchart**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="caa45-215">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="caa45-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="caa45-217">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="caa45-217">Click **Add** button.</span></span> <span data-ttu-id="caa45-218">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="caa45-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="caa45-220">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="caa45-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="caa45-221">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="caa45-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="caa45-222">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="caa45-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="caa45-223">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="caa45-223">Testing single sign-on</span></span>

<span data-ttu-id="caa45-224">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="caa45-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="caa45-225">При нажатии кнопки hello Lucidchart плитки в панели доступа hello, вы должны получить приложение Lucidchart автоматически вошедшего tooyour.</span><span class="sxs-lookup"><span data-stu-id="caa45-225">When you click hello Lucidchart tile in hello Access Panel, you should get automatically signed-on tooyour Lucidchart application.</span></span>
<span data-ttu-id="caa45-226">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="caa45-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="caa45-227">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="caa45-227">Additional resources</span></span>

* [<span data-ttu-id="caa45-228">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="caa45-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="caa45-229">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="caa45-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

