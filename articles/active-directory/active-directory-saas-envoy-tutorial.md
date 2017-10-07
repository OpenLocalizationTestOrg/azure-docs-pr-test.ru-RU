---
title: "Учебник. Интеграция Azure Active Directory с Envoy | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и делегатов."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="a3fdc-103">Руководство. Интеграция Azure Active Directory с Envoy</span><span class="sxs-lookup"><span data-stu-id="a3fdc-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="a3fdc-104">В этом учебнике вы узнаете, как toointegrate Envoy с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a3fdc-104">In this tutorial, you learn how toointegrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3fdc-105">Интеграция делегатов с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a3fdc-105">Integrating Envoy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a3fdc-106">Можно управлять в Azure AD, имеющего доступ tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-106">You can control in Azure AD who has access tooEnvoy.</span></span>
- <span data-ttu-id="a3fdc-107">Можно включить на пользователей tooautomatically get вошедшего tooEnvoy (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-107">You can enable your users tooautomatically get signed-on tooEnvoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a3fdc-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="a3fdc-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a3fdc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3fdc-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a3fdc-110">Prerequisites</span></span>

<span data-ttu-id="a3fdc-111">tooconfigure интеграция Azure AD с Envoy требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a3fdc-111">tooconfigure Azure AD integration with Envoy, you need hello following items:</span></span>

- <span data-ttu-id="a3fdc-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a3fdc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a3fdc-113">подписка Envoy с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3fdc-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3fdc-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a3fdc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3fdc-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a3fdc-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3fdc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3fdc-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a3fdc-118">Scenario description</span></span>
<span data-ttu-id="a3fdc-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a3fdc-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a3fdc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3fdc-121">Добавление делегатов из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a3fdc-121">Adding Envoy from hello gallery</span></span>
2. <span data-ttu-id="a3fdc-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3fdc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-hello-gallery"></a><span data-ttu-id="a3fdc-123">Добавление делегатов из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a3fdc-123">Adding Envoy from hello gallery</span></span>
<span data-ttu-id="a3fdc-124">tooconfigure hello интеграция делегатов в Azure AD, вы должны tooadd делегата из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-124">tooconfigure hello integration of Envoy into Azure AD, you need tooadd Envoy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a3fdc-125">**tooadd Envoy из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a3fdc-125">**tooadd Envoy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3fdc-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="a3fdc-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a3fdc-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="a3fdc-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="a3fdc-133">Введите в поле поиска hello **Envoy**выберите **Envoy** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-133">In hello search box, type **Envoy**, select **Envoy** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Envoy в списке результатов hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a3fdc-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3fdc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a3fdc-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Envoy с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a3fdc-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Envoy является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Envoy is tooa user in Azure AD.</span></span> <span data-ttu-id="a3fdc-138">Иными словами связи между пользователя Azure AD и hello связанных пользователей в Envoy требуется установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-138">In other words, a link relationship between an Azure AD user and hello related user in Envoy needs toobe established.</span></span>

<span data-ttu-id="a3fdc-139">В Envoy, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-139">In Envoy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a3fdc-140">tooconfigure и теста Azure AD единого входа с Envoy, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a3fdc-140">tooconfigure and test Azure AD single sign-on with Envoy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a3fdc-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a3fdc-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a3fdc-143">**[Создание тестового пользователя, прошедшего Envoy](#create-an-envoy-test-user)**  -toohave аналог Саймон Britta в Envoy, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - toohave a counterpart of Britta Simon in Envoy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a3fdc-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a3fdc-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a3fdc-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3fdc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a3fdc-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Envoy приложения.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="a3fdc-148">**tooconfigure Azure AD единого входа с Envoy, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a3fdc-148">**tooconfigure Azure AD single sign-on with Envoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3fdc-149">В hello в hello портала Azure **Envoy** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-149">In hello Azure portal, on hello **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="a3fdc-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="a3fdc-153">На hello **URL-адреса и домена Envoy** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a3fdc-153">On hello **Envoy Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="a3fdc-155">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="a3fdc-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="a3fdc-156">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-156">This value is not real.</span></span> <span data-ttu-id="a3fdc-157">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="a3fdc-158">Обратитесь к [группа поддержки клиент Envoy](https://envoy.com/contact/) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-158">Contact [Envoy Client support team](https://envoy.com/contact/) tooget this value.</span></span>

4. <span data-ttu-id="a3fdc-159">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата...</span><span class="sxs-lookup"><span data-stu-id="a3fdc-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate..</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="a3fdc-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a3fdc-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a3fdc-163">На hello **конфигурации Envoy** щелкните **Настройка Envoy** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-163">On hello **Envoy Configuration** section, click **Configure Envoy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a3fdc-164">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="a3fdc-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="a3fdc-166">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Envoy в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="a3fdc-167">Щелкните hello панели инструментов в верхней части hello **параметры**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-167">In hello toolbar on hello top, click **Settings**.</span></span>

    <span data-ttu-id="a3fdc-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="a3fdc-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="a3fdc-169">Нажмите **Компания**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-169">Click **Company**.</span></span>

    <span data-ttu-id="a3fdc-170">![Организация](./media/active-directory-saas-envoy-tutorial/ic776783.png "Организация")</span><span class="sxs-lookup"><span data-stu-id="a3fdc-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="a3fdc-171">Нажмите кнопку **SAML**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-171">Click **SAML**.</span></span>

    <span data-ttu-id="a3fdc-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="a3fdc-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="a3fdc-173">В hello **проверку подлинности SAML** конфигурации выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a3fdc-173">In hello **SAML Authentication** configuration section, perform hello following steps:</span></span>

    <span data-ttu-id="a3fdc-174">![Аутентификация SAML](./media/active-directory-saas-envoy-tutorial/ic776785.png "Аутентификация SAML")</span><span class="sxs-lookup"><span data-stu-id="a3fdc-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="a3fdc-175">Hello для ИД расположения главного Офиса hello значение auto, созданном приложением hello.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-175">hello value for hello HQ location ID is auto generated by hello application.</span></span>
    
    <span data-ttu-id="a3fdc-176">а.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-176">a.</span></span> <span data-ttu-id="a3fdc-177">В **отпечатков пальцев** текстовое поле, вставить hello **отпечаток** значение сертификат, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-177">In **Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a3fdc-178">b.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-178">b.</span></span> <span data-ttu-id="a3fdc-179">Вставить **SAML единого входа URL-адрес службы** значение, которое вы скопировали форме hello Azure портала в hello **URL-адрес HTTP ПОСТАВЩИКА SAML IDENTITY** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form hello Azure portal into hello **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="a3fdc-180">c.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-180">c.</span></span> <span data-ttu-id="a3fdc-181">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="a3fdc-182">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a3fdc-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a3fdc-183">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a3fdc-184">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a3fdc-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a3fdc-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3fdc-185">Create an Azure AD test user</span></span>

<span data-ttu-id="a3fdc-186">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="a3fdc-188">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a3fdc-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3fdc-189">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a3fdc-191">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a3fdc-193">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a3fdc-195">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a3fdc-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a3fdc-197">а.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-197">a.</span></span> <span data-ttu-id="a3fdc-198">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a3fdc-199">b.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-199">b.</span></span> <span data-ttu-id="a3fdc-200">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a3fdc-201">c.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-201">c.</span></span> <span data-ttu-id="a3fdc-202">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a3fdc-203">d.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-203">d.</span></span> <span data-ttu-id="a3fdc-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="a3fdc-205">Создание тестового пользователя Envoy</span><span class="sxs-lookup"><span data-stu-id="a3fdc-205">Create an Envoy test user</span></span>

<span data-ttu-id="a3fdc-206">Нет элемента действия для вас tooconfigure подготовки пользователей tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-206">There is no action item for you tooconfigure user provisioning tooEnvoy.</span></span> <span data-ttu-id="a3fdc-207">Когда назначенный пользователь пытается toolog в Envoy с помощью панели доступа hello, Envoy проверяет, существует ли пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-207">When an assigned user tries toolog into Envoy using hello access panel, Envoy checks whether hello user exists.</span></span> <span data-ttu-id="a3fdc-208">Если учетная запись пользователя отсутствует, Envoy автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a3fdc-209">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a3fdc-209">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a3fdc-210">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooEnvoy доступа.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEnvoy.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="a3fdc-212">**tooassign tooEnvoy Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a3fdc-212">**tooassign Britta Simon tooEnvoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3fdc-213">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a3fdc-215">В списке приложений hello выберите **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-215">In hello applications list, select **Envoy**.</span></span>

    ![ссылка Envoy Hello в списке приложений hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="a3fdc-217">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="a3fdc-219">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-219">Click **Add** button.</span></span> <span data-ttu-id="a3fdc-220">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="a3fdc-222">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a3fdc-223">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a3fdc-224">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a3fdc-225">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a3fdc-225">Test single sign-on</span></span>

<span data-ttu-id="a3fdc-226">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a3fdc-227">При нажатии кнопки hello Envoy плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Envoy приложения.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-227">When you click hello Envoy tile in hello Access Panel, you should get automatically signed-on tooyour Envoy application.</span></span>
<span data-ttu-id="a3fdc-228">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a3fdc-228">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a3fdc-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a3fdc-229">Additional resources</span></span>

* [<span data-ttu-id="a3fdc-230">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3fdc-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3fdc-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a3fdc-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

