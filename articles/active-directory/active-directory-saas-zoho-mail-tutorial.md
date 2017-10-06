---
title: "Руководство по интеграции Azure Active Directory с Zoho | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="ebbaa-103">Руководство по интеграции Azure Active Directory с Zoho</span><span class="sxs-lookup"><span data-stu-id="ebbaa-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="ebbaa-104">В этом учебнике вы узнаете, как toointegrate Zoho с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ebbaa-104">In this tutorial, you learn how toointegrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ebbaa-105">Интеграция с Azure AD Zoho предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ebbaa-105">Integrating Zoho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ebbaa-106">Можно управлять в Azure AD, имеющего доступ tooZoho.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-106">You can control in Azure AD who has access tooZoho.</span></span>
- <span data-ttu-id="ebbaa-107">Можно включить на пользователей tooautomatically get вошедшего tooZoho (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-107">You can enable your users tooautomatically get signed-on tooZoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ebbaa-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="ebbaa-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ebbaa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebbaa-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ebbaa-110">Prerequisites</span></span>

<span data-ttu-id="ebbaa-111">tooconfigure интеграция Azure AD с Zoho требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ebbaa-111">tooconfigure Azure AD integration with Zoho, you need hello following items:</span></span>

- <span data-ttu-id="ebbaa-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ebbaa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ebbaa-113">подписка Zoho с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ebbaa-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ebbaa-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ebbaa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ebbaa-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ebbaa-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ebbaa-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ebbaa-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ebbaa-118">Scenario description</span></span>
<span data-ttu-id="ebbaa-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ebbaa-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ebbaa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ebbaa-121">Добавление Zoho из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ebbaa-121">Adding Zoho from hello gallery</span></span>
2. <span data-ttu-id="ebbaa-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebbaa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-hello-gallery"></a><span data-ttu-id="ebbaa-123">Добавление Zoho из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ebbaa-123">Adding Zoho from hello gallery</span></span>
<span data-ttu-id="ebbaa-124">tooconfigure hello интеграции Zoho в Azure AD, вы должны tooadd Zoho из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-124">tooconfigure hello integration of Zoho into Azure AD, you need tooadd Zoho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ebbaa-125">**tooadd Zoho из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ebbaa-125">**tooadd Zoho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebbaa-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="ebbaa-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ebbaa-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="ebbaa-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="ebbaa-133">Введите в поле поиска hello **Zoho**выберите **Zoho** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-133">In hello search box, type **Zoho**, select **Zoho** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Zoho в списке результатов hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ebbaa-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebbaa-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ebbaa-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Zoho с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ebbaa-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Zoho является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoho is tooa user in Azure AD.</span></span> <span data-ttu-id="ebbaa-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Zoho должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-138">In other words, a link relationship between an Azure AD user and hello related user in Zoho needs toobe established.</span></span>

<span data-ttu-id="ebbaa-139">В Zoho, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-139">In Zoho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ebbaa-140">tooconfigure и теста Azure AD единого входа с Zoho, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ebbaa-140">tooconfigure and test Azure AD single sign-on with Zoho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ebbaa-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ebbaa-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ebbaa-143">**[Создание тестового пользователя Zoho](#create-a-zoho-test-user)**  -toohave аналог Саймон Britta в Zoho, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - toohave a counterpart of Britta Simon in Zoho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ebbaa-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ebbaa-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ebbaa-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebbaa-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ebbaa-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Zoho.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="ebbaa-148">**Azure AD tooconfigure единого входа с Zoho, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ebbaa-148">**tooconfigure Azure AD single sign-on with Zoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebbaa-149">В hello в hello портала Azure **Zoho** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-149">In hello Azure portal, on hello **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="ebbaa-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="ebbaa-153">На hello **URL-адреса и домена Zoho** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ebbaa-153">On hello **Zoho Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="ebbaa-155">а.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-155">a.</span></span> <span data-ttu-id="ebbaa-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="ebbaa-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ebbaa-157">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-157">This value is not real.</span></span> <span data-ttu-id="ebbaa-158">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-158">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ebbaa-159">Обратитесь к [группа поддержки клиент Zoho](https://www.zoho.com/mail/contact.html) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="ebbaa-160">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="ebbaa-162">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ebbaa-162">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ebbaa-164">На hello **конфигурации Zoho** щелкните **Настройка Zoho** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-164">On hello **Zoho Configuration** section, click **Configure Zoho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ebbaa-165">Копировать hello **URL-адрес выхода, URL-адрес изменения пароля и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="ebbaa-165">Copy hello **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="ebbaa-167">В другом окне браузера войдите на свой корпоративный сайт Zoho Mail в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="ebbaa-168">Go toohello **панели управления**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-168">Go toohello **Control panel**.</span></span>
   
    <span data-ttu-id="ebbaa-169">![Панель управления](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Панель управления")</span><span class="sxs-lookup"><span data-stu-id="ebbaa-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="ebbaa-170">Нажмите кнопку hello **проверку подлинности SAML** вкладки.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-170">Click hello **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="ebbaa-171">![Аутентификация SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Аутентификация SAML")</span><span class="sxs-lookup"><span data-stu-id="ebbaa-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="ebbaa-172">В hello **информация об аутентификации SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ebbaa-172">In hello **SAML Authentication Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ebbaa-173">![Параметры аутентификации SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Параметры аутентификации SAML")</span><span class="sxs-lookup"><span data-stu-id="ebbaa-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="ebbaa-174">а.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-174">a.</span></span> <span data-ttu-id="ebbaa-175">В hello **URL-адрес входа** вставьте **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-175">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="ebbaa-176">b.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-176">b.</span></span> <span data-ttu-id="ebbaa-177">В hello **URL-адрес выхода** вставьте **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-177">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="ebbaa-178">c.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-178">c.</span></span> <span data-ttu-id="ebbaa-179">В hello **URL-адрес изменения пароля** вставьте **URL-адрес изменения пароля** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-179">In hello **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="ebbaa-180">d.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-180">d.</span></span> <span data-ttu-id="ebbaa-181">Откройте сертификат кодировке base-64 загружен с портала Azure в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **PublicKey** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="ebbaa-182">д.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-182">e.</span></span> <span data-ttu-id="ebbaa-183">В поле **Algorithm** (Алгоритм) задайте значение **RSA**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="ebbaa-184">f.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-184">f.</span></span> <span data-ttu-id="ebbaa-185">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="ebbaa-186">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ebbaa-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ebbaa-187">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ebbaa-188">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ebbaa-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ebbaa-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebbaa-189">Create an Azure AD test user</span></span>

<span data-ttu-id="ebbaa-190">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="ebbaa-192">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ebbaa-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebbaa-193">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ebbaa-195">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ebbaa-197">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ebbaa-199">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ebbaa-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ebbaa-201">а.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-201">a.</span></span> <span data-ttu-id="ebbaa-202">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ebbaa-203">b.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-203">b.</span></span> <span data-ttu-id="ebbaa-204">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ebbaa-205">c.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-205">c.</span></span> <span data-ttu-id="ebbaa-206">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ebbaa-207">d.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-207">d.</span></span> <span data-ttu-id="ebbaa-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="ebbaa-209">Создание тестового пользователя Zoho</span><span class="sxs-lookup"><span data-stu-id="ebbaa-209">Create a Zoho test user</span></span>

<span data-ttu-id="ebbaa-210">В порядке tooenable toolog пользователей Azure AD в Zoho Mail их необходимо подготовить в Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-210">In order tooenable Azure AD users toolog into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="ebbaa-211">В случае hello объекта Zoho Mail Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-211">In hello case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="ebbaa-212">Можно использовать любые другие Zoho Mail пользователя средства создания учетных записей или интерфейсы API, предоставляемые Zoho Mail tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail tooprovision AAD user accounts.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="ebbaa-213">tooprovision учетной записи пользователя, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-213">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="ebbaa-214">Войдите в tooyour **Zoho Mail** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-214">Log in tooyour **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="ebbaa-215">Go слишком**панели управления \> почта и документы**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-215">Go too**Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="ebbaa-216">Go слишком**сведения о пользователе \> добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-216">Go too**User Details \> Add User**.</span></span>
   
    <span data-ttu-id="ebbaa-217">![Добавление пользователя](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="ebbaa-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="ebbaa-218">На hello **Добавление пользователей** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ebbaa-218">On hello **Add users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="ebbaa-219">![Добавление пользователя](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="ebbaa-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="ebbaa-220">а.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-220">a.</span></span> <span data-ttu-id="ebbaa-221">В hello **имя** в текстовое поле типа hello имя пользователя как **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-221">In hello **First Name** textbox, type hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="ebbaa-222">b.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-222">b.</span></span> <span data-ttu-id="ebbaa-223">В hello **Фамилия** в текстовое поле типа hello фамилию пользователя как **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-223">In hello **Last Name** textbox, type hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="ebbaa-224">c.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-224">c.</span></span> <span data-ttu-id="ebbaa-225">В hello **адрес электронной почты** текстовое поле, идентификатор типа hello электронной почты пользователя, таких как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ebbaa-225">In hello **Email ID** textbox, type hello email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="ebbaa-226">d.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-226">d.</span></span> <span data-ttu-id="ebbaa-227">В hello **пароль** текстовом поле введите пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-227">In hello **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="ebbaa-228">д.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-228">e.</span></span> <span data-ttu-id="ebbaa-229">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="ebbaa-230">Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты с учетной записью hello tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-230">hello Azure Active Directory account holder will receive an email with a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ebbaa-231">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ebbaa-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ebbaa-232">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooZoho доступа.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoho.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="ebbaa-234">**tooassign tooZoho Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ebbaa-234">**tooassign Britta Simon tooZoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebbaa-235">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ebbaa-237">В списке приложений hello выберите **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-237">In hello applications list, select **Zoho**.</span></span>

    ![ссылка Zoho Hello в списке приложений hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="ebbaa-239">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="ebbaa-241">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-241">Click **Add** button.</span></span> <span data-ttu-id="ebbaa-242">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="ebbaa-244">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ebbaa-245">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ebbaa-246">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ebbaa-247">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ebbaa-247">Test single sign-on</span></span>

<span data-ttu-id="ebbaa-248">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ebbaa-249">При нажатии кнопки hello Zoho плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Zoho приложения.</span><span class="sxs-lookup"><span data-stu-id="ebbaa-249">When you click hello Zoho tile in hello Access Panel, you should get automatically signed-on tooyour Zoho application.</span></span>
<span data-ttu-id="ebbaa-250">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ebbaa-250">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ebbaa-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ebbaa-251">Additional resources</span></span>

* [<span data-ttu-id="ebbaa-252">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ebbaa-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ebbaa-253">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ebbaa-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

