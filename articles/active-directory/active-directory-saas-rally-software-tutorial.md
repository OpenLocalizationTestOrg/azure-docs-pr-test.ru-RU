---
title: "Учебник. Интеграция Azure Active Directory с Rally Software | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Rally Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="8da35-103">Учебник. Интеграция Azure Active Directory с Rally Software</span><span class="sxs-lookup"><span data-stu-id="8da35-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="8da35-104">В этом учебнике вы узнаете, как toointegrate Rally Software с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8da35-104">In this tutorial, you learn how toointegrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8da35-105">Интеграция Rally Software с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8da35-105">Integrating Rally Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8da35-106">Можно управлять в Azure AD, имеющего доступ tooRally программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="8da35-106">You can control in Azure AD who has access tooRally Software.</span></span>
- <span data-ttu-id="8da35-107">Можно включить на пользователей tooautomatically get вошедшего tooRally программного обеспечения (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8da35-107">You can enable your users tooautomatically get signed-on tooRally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8da35-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8da35-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="8da35-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8da35-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8da35-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8da35-110">Prerequisites</span></span>

<span data-ttu-id="8da35-111">tooconfigure интеграция Azure AD с Rally Software, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8da35-111">tooconfigure Azure AD integration with Rally Software, you need hello following items:</span></span>

- <span data-ttu-id="8da35-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8da35-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8da35-113">подписка Rally Software с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8da35-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8da35-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8da35-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8da35-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8da35-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8da35-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8da35-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8da35-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8da35-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8da35-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8da35-118">Scenario description</span></span>
<span data-ttu-id="8da35-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8da35-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8da35-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8da35-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8da35-121">Добавление Rally Software из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8da35-121">Adding Rally Software from hello gallery</span></span>
2. <span data-ttu-id="8da35-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8da35-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-hello-gallery"></a><span data-ttu-id="8da35-123">Добавление Rally Software из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8da35-123">Adding Rally Software from hello gallery</span></span>
<span data-ttu-id="8da35-124">tooconfigure hello интеграцией Rally Software с Azure AD, вы должны tooadd Rally Software из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8da35-124">tooconfigure hello integration of Rally Software into Azure AD, you need tooadd Rally Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8da35-125">**tooadd Rally Software из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8da35-125">**tooadd Rally Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8da35-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8da35-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="8da35-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8da35-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8da35-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8da35-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="8da35-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8da35-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="8da35-133">Введите в поле поиска hello **Rally Software**выберите **Rally Software** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8da35-133">In hello search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Программное обеспечение Rally в списке результатов hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8da35-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8da35-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8da35-136">В этом разделе описана настройка и проверка единого входа Azure AD в Rally Software для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8da35-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8da35-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Rally Software является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8da35-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rally Software is tooa user in Azure AD.</span></span> <span data-ttu-id="8da35-138">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Rally Software должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8da35-138">In other words, a link relationship between an Azure AD user and hello related user in Rally Software needs toobe established.</span></span>

<span data-ttu-id="8da35-139">В Rally Software, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="8da35-139">In Rally Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8da35-140">tooconfigure и теста Azure AD единого входа с Rally Software, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8da35-140">tooconfigure and test Azure AD single sign-on with Rally Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8da35-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8da35-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8da35-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8da35-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8da35-143">**[Создание тестового пользователя Rally Software](#create-a-rally-software-test-user)**  -toohave аналог Саймон Britta в Rally Software, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8da35-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - toohave a counterpart of Britta Simon in Rally Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8da35-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8da35-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8da35-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8da35-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8da35-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="8da35-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8da35-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Rally Software.</span><span class="sxs-lookup"><span data-stu-id="8da35-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="8da35-148">**tooconfigure Azure AD единого входа с Rally Software, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8da35-148">**tooconfigure Azure AD single sign-on with Rally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="8da35-149">В hello в hello портала Azure **Rally Software** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8da35-149">In hello Azure portal, on hello **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="8da35-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8da35-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="8da35-153">На hello **URL-адреса и домена программное обеспечение Rally** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8da35-153">On hello **Rally Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="8da35-155">а.</span><span class="sxs-lookup"><span data-stu-id="8da35-155">a.</span></span> <span data-ttu-id="8da35-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="8da35-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="8da35-157">b.</span><span class="sxs-lookup"><span data-stu-id="8da35-157">b.</span></span> <span data-ttu-id="8da35-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="8da35-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8da35-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="8da35-159">These values are not real.</span></span> <span data-ttu-id="8da35-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="8da35-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8da35-161">Обратитесь к [Rally клиентское программное обеспечение поддержки](https://help.rallydev.com/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="8da35-161">Contact [Rally Software Client support team](https://help.rallydev.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="8da35-162">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8da35-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="8da35-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8da35-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8da35-166">На hello **Rally конфигурации программного обеспечения** щелкните **Настройка Rally Software** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="8da35-166">On hello **Rally Software Configuration** section, click **Configure Rally Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8da35-167">Копировать hello **URL-адрес выхода и идентификатор сущности SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="8da35-167">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Настройка Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="8da35-169">Войдите в tooyour **Rally Software** клиента.</span><span class="sxs-lookup"><span data-stu-id="8da35-169">Log in tooyour **Rally Software** tenant.</span></span>

8. <span data-ttu-id="8da35-170">Щелкните hello панели инструментов в верхней части hello **установки**, а затем выберите **подписки**.</span><span class="sxs-lookup"><span data-stu-id="8da35-170">In hello toolbar on hello top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="8da35-171">![Подписка](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Подписка")</span><span class="sxs-lookup"><span data-stu-id="8da35-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="8da35-172">Нажмите кнопку hello **действия** кнопки.</span><span class="sxs-lookup"><span data-stu-id="8da35-172">Click hello **Action** button.</span></span> <span data-ttu-id="8da35-173">Выберите **изменение подписки** в hello верхней правой части панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="8da35-173">Select **Edit Subscription** at hello top right side of hello toolbar.</span></span>

10. <span data-ttu-id="8da35-174">На hello **подписки** странице диалогового окна, выполните следующие шаги hello и нажмите кнопку **сохранить и закрыть**:</span><span class="sxs-lookup"><span data-stu-id="8da35-174">On hello **Subscription** dialog page, perform hello following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="8da35-175">![Аутентификация](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="8da35-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="8da35-176">а.</span><span class="sxs-lookup"><span data-stu-id="8da35-176">a.</span></span> <span data-ttu-id="8da35-177">Из раскрывающегося списка "Аутентификация" выберите пункт **Rally or SSO authentication** (Аутентификация Rally или путем единого входа).</span><span class="sxs-lookup"><span data-stu-id="8da35-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="8da35-178">b.</span><span class="sxs-lookup"><span data-stu-id="8da35-178">b.</span></span> <span data-ttu-id="8da35-179">В hello **URL-адрес поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8da35-179">In hello **Identity provider URL** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="8da35-180">c.</span><span class="sxs-lookup"><span data-stu-id="8da35-180">c.</span></span> <span data-ttu-id="8da35-181">В hello **выхода SSO** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8da35-181">In hello **SSO Logout** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="8da35-182">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="8da35-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8da35-183">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="8da35-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8da35-184">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8da35-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8da35-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8da35-185">Create an Azure AD test user</span></span>

<span data-ttu-id="8da35-186">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8da35-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="8da35-188">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8da35-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8da35-189">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="8da35-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8da35-191">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8da35-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8da35-193">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="8da35-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8da35-195">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8da35-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8da35-197">а.</span><span class="sxs-lookup"><span data-stu-id="8da35-197">a.</span></span> <span data-ttu-id="8da35-198">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8da35-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8da35-199">b.</span><span class="sxs-lookup"><span data-stu-id="8da35-199">b.</span></span> <span data-ttu-id="8da35-200">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8da35-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="8da35-201">c.</span><span class="sxs-lookup"><span data-stu-id="8da35-201">c.</span></span> <span data-ttu-id="8da35-202">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="8da35-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="8da35-203">d.</span><span class="sxs-lookup"><span data-stu-id="8da35-203">d.</span></span> <span data-ttu-id="8da35-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8da35-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="8da35-205">Создание тестового пользователя Rally Software</span><span class="sxs-lookup"><span data-stu-id="8da35-205">Create a Rally Software test user</span></span>

<span data-ttu-id="8da35-206">Для Azure AD пользователи toobe может toosign в они должны быть подготовленных toohello приложении Rally Software с использованием своих имен пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8da35-206">For Azure AD users toobe able toosign in, they must be provisioned toohello Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="8da35-207">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8da35-207">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="8da35-208">Войдите в систему tooyour клиент Rally Software.</span><span class="sxs-lookup"><span data-stu-id="8da35-208">Log in tooyour Rally Software tenant.</span></span>

2. <span data-ttu-id="8da35-209">Go слишком**установки \> пользователей**и нажмите кнопку **+ добавить New**.</span><span class="sxs-lookup"><span data-stu-id="8da35-209">Go too**Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="8da35-210">![Пользователи](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="8da35-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="8da35-211">Введите имя hello в текстовом поле hello нового пользователя и нажмите кнопку **добавить с подробностями**.</span><span class="sxs-lookup"><span data-stu-id="8da35-211">Type hello name in hello New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="8da35-212">В hello **Create User** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8da35-212">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8da35-213">![Создание пользователя](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="8da35-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="8da35-214">а.</span><span class="sxs-lookup"><span data-stu-id="8da35-214">a.</span></span> <span data-ttu-id="8da35-215">В hello **имя пользователя** в текстовое поле имя пользователя как типа hello **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="8da35-215">In hello **User Name** textbox, type hello name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="8da35-216">b.</span><span class="sxs-lookup"><span data-stu-id="8da35-216">b.</span></span> <span data-ttu-id="8da35-217">В **адрес электронной почты** текстовом поле введите адрес электронной почты hello пользователя как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="8da35-217">In **E-mail Address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="8da35-218">c.</span><span class="sxs-lookup"><span data-stu-id="8da35-218">c.</span></span> <span data-ttu-id="8da35-219">В **имя** текста введите имя пользователя, такие как hello **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8da35-219">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="8da35-220">d.</span><span class="sxs-lookup"><span data-stu-id="8da35-220">d.</span></span> <span data-ttu-id="8da35-221">В **Фамилия** текста введите hello фамилию пользователя как **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8da35-221">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="8da35-222">д.</span><span class="sxs-lookup"><span data-stu-id="8da35-222">e.</span></span> <span data-ttu-id="8da35-223">Щелкните **Save & Close** (Сохранить и закрыть).</span><span class="sxs-lookup"><span data-stu-id="8da35-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="8da35-224">Можно использовать любые другие Rally Software пользователя средства создания учетных записей или интерфейсы API, предоставляемые Rally Software tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8da35-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8da35-225">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8da35-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8da35-226">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooRally программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="8da35-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRally Software.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="8da35-228">**tooassign tooRally Britta Simon программное обеспечение, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="8da35-228">**tooassign Britta Simon tooRally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="8da35-229">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8da35-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8da35-231">В списке приложений hello выберите **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="8da35-231">In hello applications list, select **Rally Software**.</span></span>

    ![ссылка Rally Software Hello в списке приложений hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="8da35-233">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8da35-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="8da35-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8da35-235">Click **Add** button.</span></span> <span data-ttu-id="8da35-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8da35-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="8da35-238">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8da35-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8da35-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8da35-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8da35-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8da35-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8da35-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8da35-241">Test single sign-on</span></span>

<span data-ttu-id="8da35-242">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="8da35-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8da35-243">Если щелкнуть плитку Rally Software hello в hello панели доступа, вы должны получить tooyour автоматически подписью в приложении Rally Software.</span><span class="sxs-lookup"><span data-stu-id="8da35-243">When you click hello Rally Software tile in hello Access Panel, you should get automatically signed-on tooyour Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8da35-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8da35-244">Additional resources</span></span>

* [<span data-ttu-id="8da35-245">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8da35-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8da35-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8da35-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

