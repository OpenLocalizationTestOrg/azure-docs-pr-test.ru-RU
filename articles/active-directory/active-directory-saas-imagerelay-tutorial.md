---
title: "Руководство по интеграции Azure Active Directory с Image Relay | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ретрансляции изображения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="40007-103">Руководство по интеграции Azure Active Directory с приложением Image Relay</span><span class="sxs-lookup"><span data-stu-id="40007-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="40007-104">В этом учебнике вы узнаете, как toointegrate ретрансляции образа в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40007-104">In this tutorial, you learn how toointegrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40007-105">Интеграция ретрансляции изображения с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="40007-105">Integrating Image Relay with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="40007-106">Можно управлять в Azure AD, имеющего доступ tooImage ретрансляции</span><span class="sxs-lookup"><span data-stu-id="40007-106">You can control in Azure AD who has access tooImage Relay</span></span>
- <span data-ttu-id="40007-107">Можно включить на пользователей tooautomatically get вошедшего tooImage ретрансляции (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="40007-107">You can enable your users tooautomatically get signed-on tooImage Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="40007-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="40007-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="40007-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40007-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40007-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="40007-110">Prerequisites</span></span>

<span data-ttu-id="40007-111">tooconfigure интеграция Azure AD с ретрансляции образа необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="40007-111">tooconfigure Azure AD integration with Image Relay, you need hello following items:</span></span>

- <span data-ttu-id="40007-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="40007-112">An Azure AD subscription</span></span>
- <span data-ttu-id="40007-113">подписка Image Relay с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="40007-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="40007-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="40007-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="40007-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="40007-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40007-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="40007-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="40007-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40007-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40007-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="40007-118">Scenario description</span></span>
<span data-ttu-id="40007-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="40007-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40007-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="40007-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40007-121">Добавление ретрансляции образа из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="40007-121">Adding Image Relay from hello gallery</span></span>
2. <span data-ttu-id="40007-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40007-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-hello-gallery"></a><span data-ttu-id="40007-123">Добавление ретрансляции образа из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="40007-123">Adding Image Relay from hello gallery</span></span>
<span data-ttu-id="40007-124">tooconfigure hello интеграции ретрансляции образа в Azure AD, вы должны tooadd ретрансляции изображений из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="40007-124">tooconfigure hello integration of Image Relay into Azure AD, you need tooadd Image Relay from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="40007-125">**tooadd ретрансляции образа из коллекции hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="40007-125">**tooadd Image Relay from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="40007-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="40007-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40007-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="40007-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="40007-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="40007-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="40007-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="40007-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="40007-133">Введите в поле поиска hello **ретрансляции изображения**.</span><span class="sxs-lookup"><span data-stu-id="40007-133">In hello search box, type **Image Relay**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="40007-135">В панели результатов hello выберите **ретрансляции изображения**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="40007-135">In hello results panel, select **Image Relay**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="40007-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40007-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="40007-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Image Relay для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40007-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40007-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ретрансляции изображения является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40007-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Image Relay is tooa user in Azure AD.</span></span> <span data-ttu-id="40007-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в ретрансляции образа должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="40007-140">In other words, a link relationship between an Azure AD user and hello related user in Image Relay needs toobe established.</span></span>

<span data-ttu-id="40007-141">В образ ретрансляции, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="40007-141">In Image Relay, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="40007-142">tooconfigure и теста Azure AD единого входа с образа ретрансляции, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="40007-142">tooconfigure and test Azure AD single sign-on with Image Relay, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="40007-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="40007-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="40007-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="40007-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40007-145">**[Создание тестового пользователя, прошедшего ретрансляции изображения](#creating-an-image-relay-test-user)**  -toohave аналог Саймон Britta в образ ретрансляции, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="40007-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - toohave a counterpart of Britta Simon in Image Relay that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="40007-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="40007-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40007-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="40007-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="40007-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40007-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="40007-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении изображения ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="40007-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="40007-150">**Azure AD tooconfigure единого входа с ретрансляции образа выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="40007-150">**tooconfigure Azure AD single sign-on with Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="40007-151">В hello в hello портала Azure **ретрансляции изображения** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="40007-151">In hello Azure portal, on hello **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="40007-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="40007-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="40007-155">На hello **домен ретрансляции изображения и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="40007-155">On hello **Image Relay Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="40007-157">а.</span><span class="sxs-lookup"><span data-stu-id="40007-157">a.</span></span> <span data-ttu-id="40007-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="40007-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="40007-159">b.</span><span class="sxs-lookup"><span data-stu-id="40007-159">b.</span></span> <span data-ttu-id="40007-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="40007-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="40007-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="40007-161">These values are not real.</span></span> <span data-ttu-id="40007-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="40007-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="40007-163">Обратитесь к [группа поддержки клиента ретрансляции изображения](http://support.imagerelay.com/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="40007-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="40007-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="40007-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="40007-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="40007-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="40007-168">На hello **конфигурация ретрансляции изображения** щелкните **Настройка ретрансляции изображения** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="40007-168">On hello **Image Relay Configuration** section, click **Configure Image Relay** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="40007-169">Копировать hello **URL-адрес выхода службы и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="40007-169">Copy hello **Sign-Out Service URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="40007-171">В другом окне браузера войдите tooyour изображения ретрансляции корпоративный сайт с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="40007-171">In another browser window, sign in tooyour Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="40007-172">Hello инструментов в верхней части hello нажмите hello **& разрешения для пользователей** рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="40007-172">In hello toolbar on hello top, click hello **Users & Permissions** workload.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="40007-174">Щелкните **Создать новое разрешение**.</span><span class="sxs-lookup"><span data-stu-id="40007-174">Click **Create New Permission**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="40007-176">В hello **настройки единого входа** рабочей нагрузки, выберите hello **эта группа может только войти через Single Sign On** флажок и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="40007-176">In hello **Single Sign On Settings** workload, select hello **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="40007-178">Go слишком**параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="40007-178">Go too**Account Settings**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="40007-180">Go toohello **настройки единого входа** рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="40007-180">Go toohello **Single Sign On Settings** workload.</span></span>
    
     ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="40007-182">На hello **параметры SAML** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="40007-182">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="40007-184">а.</span><span class="sxs-lookup"><span data-stu-id="40007-184">a.</span></span> <span data-ttu-id="40007-185">В **URL-адрес входа** текстовое значение hello вставить **единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="40007-185">In **Login URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="40007-186">b.</span><span class="sxs-lookup"><span data-stu-id="40007-186">b.</span></span> <span data-ttu-id="40007-187">В **URL-адрес выхода** текстовое значение hello вставить **URL-адрес службы единого выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="40007-187">In **Logout URL**  textbox, paste hello value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="40007-188">c.</span><span class="sxs-lookup"><span data-stu-id="40007-188">c.</span></span> <span data-ttu-id="40007-189">В поле **Name Id Format** (Формат ИД имени) выберите **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="40007-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="40007-190">d.</span><span class="sxs-lookup"><span data-stu-id="40007-190">d.</span></span> <span data-ttu-id="40007-191">Как **привязки параметров для запросов от hello поставщика услуг (изображение ретрансляции)**выберите **привязки POST**.</span><span class="sxs-lookup"><span data-stu-id="40007-191">As **Binding Options for Requests from hello Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="40007-192">д.</span><span class="sxs-lookup"><span data-stu-id="40007-192">e.</span></span> <span data-ttu-id="40007-193">В разделе **Сертификат X.509** щелкните **Обновить сертификат**.</span><span class="sxs-lookup"><span data-stu-id="40007-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="40007-195">f.</span><span class="sxs-lookup"><span data-stu-id="40007-195">f.</span></span> <span data-ttu-id="40007-196">Откройте сертификат загружаются hello в блокноте, скопируйте содержимое hello и вставьте его в текстовое поле сертификата x.509 hello.</span><span class="sxs-lookup"><span data-stu-id="40007-196">Open hello downloaded certificate in notepad, copy hello content, and then paste it into hello x.509 Certificate textbox.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="40007-198">ж.</span><span class="sxs-lookup"><span data-stu-id="40007-198">g.</span></span> <span data-ttu-id="40007-199">В **подготовки пользователей JIT –** раздел, выберите hello **включить JIT – подготовки пользователей**.</span><span class="sxs-lookup"><span data-stu-id="40007-199">In **Just-In-Time User Provisioning** section, select hello **Enable Just-In-Time User Provisioning**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="40007-201">h.</span><span class="sxs-lookup"><span data-stu-id="40007-201">h.</span></span> <span data-ttu-id="40007-202">Группы разрешений SELECT hello (например, **SSO основные**) это разрешено toosign в только с помощью единого входа.</span><span class="sxs-lookup"><span data-stu-id="40007-202">Select hello permission group (for example, **SSO Basic**) which is allowed toosign in only through single sign-on.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="40007-204">i.</span><span class="sxs-lookup"><span data-stu-id="40007-204">i.</span></span> <span data-ttu-id="40007-205">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="40007-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="40007-206">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="40007-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="40007-207">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="40007-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="40007-208">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="40007-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="40007-209">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="40007-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="40007-210">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="40007-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="40007-212">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="40007-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="40007-213">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="40007-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40007-215">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="40007-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40007-217">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="40007-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40007-219">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="40007-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="40007-221">а.</span><span class="sxs-lookup"><span data-stu-id="40007-221">a.</span></span> <span data-ttu-id="40007-222">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40007-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="40007-223">b.</span><span class="sxs-lookup"><span data-stu-id="40007-223">b.</span></span> <span data-ttu-id="40007-224">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="40007-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="40007-225">c.</span><span class="sxs-lookup"><span data-stu-id="40007-225">c.</span></span> <span data-ttu-id="40007-226">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="40007-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="40007-227">d.</span><span class="sxs-lookup"><span data-stu-id="40007-227">d.</span></span> <span data-ttu-id="40007-228">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="40007-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="40007-229">Создание тестового пользователя Image Relay</span><span class="sxs-lookup"><span data-stu-id="40007-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="40007-230">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в образ ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="40007-230">hello objective of this section is toocreate a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="40007-231">**toocreate пользователя с именем Britta Simon в ретрансляции образа выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="40007-231">**toocreate a user called Britta Simon in Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="40007-232">Корпоративный сайт ретрансляции изображения tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="40007-232">Sign-on tooyour Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="40007-233">Go слишком**& разрешения для пользователей** и выберите **создание единого входа пользователя**.</span><span class="sxs-lookup"><span data-stu-id="40007-233">Go too**Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="40007-235">Введите hello **электронной почты**, **имя**, **Фамилия**, и **компании** hello пользователя требуется tooprovision и группы разрешений select hello (например, SSO основные) это группа hello, выполнить вход можно только с помощью единого входа.</span><span class="sxs-lookup"><span data-stu-id="40007-235">Enter hello **Email**, **First Name**, **Last Name**, and **Company** of hello user you want tooprovision and select hello permission group (for example, SSO Basic) which is hello group that can sign in only through single sign-on.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="40007-237">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="40007-237">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="40007-238">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="40007-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="40007-239">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooImage ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="40007-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooImage Relay.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="40007-241">**tooassign tooImage Britta Simon ретрансляции, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="40007-241">**tooassign Britta Simon tooImage Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="40007-242">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="40007-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="40007-244">В списке приложений hello выберите **ретрансляции изображения**.</span><span class="sxs-lookup"><span data-stu-id="40007-244">In hello applications list, select **Image Relay**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="40007-246">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="40007-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="40007-248">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="40007-248">Click **Add** button.</span></span> <span data-ttu-id="40007-249">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="40007-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="40007-251">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="40007-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="40007-252">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="40007-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40007-253">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="40007-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="40007-254">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="40007-254">Testing single sign-on</span></span>

<span data-ttu-id="40007-255">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="40007-255">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>    

<span data-ttu-id="40007-256">Если щелкнуть плитку изображения ретрансляции hello в hello панели доступа, следует получать автоматически вошедшего tooyour ретрансляции образа приложения.</span><span class="sxs-lookup"><span data-stu-id="40007-256">When you click hello Image Relay tile in hello Access Panel, you should get automatically signed-on tooyour Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="40007-257">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="40007-257">Additional resources</span></span>

* [<span data-ttu-id="40007-258">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40007-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40007-259">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="40007-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

