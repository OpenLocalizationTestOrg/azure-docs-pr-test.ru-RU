---
title: "Руководство. Интеграция Azure Active Directory с Citrix ShareFile | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="96f0b-103">Руководство. Интеграция Azure Active Directory с Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="96f0b-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="96f0b-104">В этом учебнике вы узнаете, как toointegrate Citrix ShareFile с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96f0b-104">In this tutorial, you learn how toointegrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96f0b-105">Интеграция Citrix ShareFile с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="96f0b-105">Integrating Citrix ShareFile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="96f0b-106">Можно управлять в Azure AD, имеющего доступ tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="96f0b-106">You can control in Azure AD who has access tooCitrix ShareFile.</span></span>
- <span data-ttu-id="96f0b-107">Можно включить на пользователей tooautomatically get вошедшего tooCitrix ShareFile (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96f0b-107">You can enable your users tooautomatically get signed-on tooCitrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="96f0b-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="96f0b-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="96f0b-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96f0b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96f0b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="96f0b-110">Prerequisites</span></span>

<span data-ttu-id="96f0b-111">tooconfigure интеграция Azure AD с Citrix ShareFile требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="96f0b-111">tooconfigure Azure AD integration with Citrix ShareFile, you need hello following items:</span></span>

- <span data-ttu-id="96f0b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="96f0b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96f0b-113">подписка Citrix ShareFile с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="96f0b-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96f0b-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="96f0b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96f0b-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="96f0b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96f0b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="96f0b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96f0b-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96f0b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96f0b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="96f0b-118">Scenario description</span></span>
<span data-ttu-id="96f0b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="96f0b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96f0b-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="96f0b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96f0b-121">Добавление Citrix ShareFile из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="96f0b-121">Add Citrix ShareFile from hello gallery</span></span>
2. <span data-ttu-id="96f0b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f0b-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-hello-gallery"></a><span data-ttu-id="96f0b-123">Добавление Citrix ShareFile из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="96f0b-123">Add Citrix ShareFile from hello gallery</span></span>
<span data-ttu-id="96f0b-124">tooconfigure hello интеграции Citrix ShareFile в Azure AD, вы должны tooadd Citrix ShareFile из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="96f0b-124">tooconfigure hello integration of Citrix ShareFile into Azure AD, you need tooadd Citrix ShareFile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="96f0b-125">**tooadd Citrix ShareFile из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96f0b-125">**tooadd Citrix ShareFile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="96f0b-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="96f0b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="96f0b-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="96f0b-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="96f0b-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="96f0b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="96f0b-133">Введите в поле поиска hello **Citrix ShareFile**выберите **Citrix ShareFile** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="96f0b-133">In hello search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Список результатов Citrix ShareFile в hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="96f0b-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f0b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="96f0b-136">В этом разделе описана настройка и проверка единого входа Azure AD в Citrix ShareFile с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96f0b-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96f0b-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Citrix ShareFile является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96f0b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix ShareFile is tooa user in Azure AD.</span></span> <span data-ttu-id="96f0b-138">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Citrix ShareFile должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="96f0b-138">In other words, a link relationship between an Azure AD user and hello related user in Citrix ShareFile needs toobe established.</span></span>

<span data-ttu-id="96f0b-139">В Citrix ShareFile, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="96f0b-139">In Citrix ShareFile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="96f0b-140">tooconfigure и теста Azure AD единого входа с Citrix ShareFile, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="96f0b-140">tooconfigure and test Azure AD single sign-on with Citrix ShareFile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="96f0b-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="96f0b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="96f0b-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="96f0b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96f0b-143">**[Создание тестового пользователя Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave аналог Саймон Britta в Citrix ShareFile, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="96f0b-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - toohave a counterpart of Britta Simon in Citrix ShareFile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="96f0b-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="96f0b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96f0b-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="96f0b-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="96f0b-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f0b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="96f0b-147">В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в приложение Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="96f0b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="96f0b-148">**tooconfigure Azure AD единого входа с Citrix ShareFile, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96f0b-148">**tooconfigure Azure AD single sign-on with Citrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="96f0b-149">В hello в hello портала Azure **Citrix ShareFile** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-149">In hello Azure portal, on hello **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="96f0b-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="96f0b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="96f0b-153">На hello **URL-адреса и домена Citrix ShareFile** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="96f0b-153">On hello **Citrix ShareFile Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="96f0b-155">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="96f0b-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96f0b-156">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="96f0b-156">This value is not real.</span></span> <span data-ttu-id="96f0b-157">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="96f0b-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="96f0b-158">Обратитесь к [группа поддержки клиента Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="96f0b-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) tooget this value.</span></span> 

4. <span data-ttu-id="96f0b-159">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="96f0b-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="96f0b-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="96f0b-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="96f0b-163">На hello **конфигурации Citrix ShareFile** щелкните **Настройка Citrix ShareFile** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="96f0b-163">On hello **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="96f0b-164">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="96f0b-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="96f0b-166">В другом окне веб-браузера войдите на свой корпоративный веб-сайт **Citrix ShareFile** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="96f0b-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="96f0b-167">Щелкните hello панели инструментов в верхней части hello **администратора**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-167">In hello toolbar on hello top, click **Admin**.</span></span>

9. <span data-ttu-id="96f0b-168">В области навигации слева hello выберите **настройки единого входа**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-168">In hello left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="96f0b-169">![Администрирование учетной записи](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Администрирование учетной записи")</span><span class="sxs-lookup"><span data-stu-id="96f0b-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="96f0b-170">На hello **единого входа и конфигурации SAML 2.0** в разделе **основные параметры**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="96f0b-170">On hello **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform hello following steps:</span></span>
   
    <span data-ttu-id="96f0b-171">![Единый вход](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="96f0b-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="96f0b-172">а.</span><span class="sxs-lookup"><span data-stu-id="96f0b-172">a.</span></span> <span data-ttu-id="96f0b-173">Выберите команду **Enable SAML**(Включить SAML).</span><span class="sxs-lookup"><span data-stu-id="96f0b-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="96f0b-174">b.</span><span class="sxs-lookup"><span data-stu-id="96f0b-174">b.</span></span> <span data-ttu-id="96f0b-175">В **издатель IDP / идентификатор сущности** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="96f0b-175">In **Your IDP Issuer/ Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="96f0b-176">c.</span><span class="sxs-lookup"><span data-stu-id="96f0b-176">c.</span></span> <span data-ttu-id="96f0b-177">Нажмите кнопку **изменений** Далее toohello **сертификат X.509** поле, а затем отправить hello сертификат, загруженный из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="96f0b-177">Click **Change** next toohello **X.509 Certificate** field and then upload hello certificate you downloaded from hello Azure portal.</span></span>
    
    <span data-ttu-id="96f0b-178">d.</span><span class="sxs-lookup"><span data-stu-id="96f0b-178">d.</span></span> <span data-ttu-id="96f0b-179">В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="96f0b-179">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="96f0b-180">д.</span><span class="sxs-lookup"><span data-stu-id="96f0b-180">e.</span></span> <span data-ttu-id="96f0b-181">В **URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="96f0b-181">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="96f0b-182">Нажмите кнопку **Сохранить** на портале управления Citrix ShareFile hello.</span><span class="sxs-lookup"><span data-stu-id="96f0b-182">Click **Save** on hello Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="96f0b-183">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="96f0b-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="96f0b-184">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="96f0b-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="96f0b-185">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96f0b-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="96f0b-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f0b-186">Create an Azure AD test user</span></span>

<span data-ttu-id="96f0b-187">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="96f0b-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="96f0b-189">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96f0b-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="96f0b-190">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="96f0b-190">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="96f0b-192">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-192">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="96f0b-194">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="96f0b-194">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="96f0b-196">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="96f0b-196">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="96f0b-198">а.</span><span class="sxs-lookup"><span data-stu-id="96f0b-198">a.</span></span> <span data-ttu-id="96f0b-199">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-199">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96f0b-200">b.</span><span class="sxs-lookup"><span data-stu-id="96f0b-200">b.</span></span> <span data-ttu-id="96f0b-201">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="96f0b-201">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="96f0b-202">c.</span><span class="sxs-lookup"><span data-stu-id="96f0b-202">c.</span></span> <span data-ttu-id="96f0b-203">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="96f0b-203">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="96f0b-204">d.</span><span class="sxs-lookup"><span data-stu-id="96f0b-204">d.</span></span> <span data-ttu-id="96f0b-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="96f0b-206">Создание тестового пользователя Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="96f0b-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="96f0b-207">В порядке tooenable toolog пользователей Azure AD в Citrix ShareFile их необходимо подготовить в Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="96f0b-207">In order tooenable Azure AD users toolog into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="96f0b-208">В случае hello объекта Citrix ShareFile Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="96f0b-208">In hello case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="96f0b-209">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96f0b-209">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="96f0b-210">Войдите в tooyour **Citrix ShareFile** клиента.</span><span class="sxs-lookup"><span data-stu-id="96f0b-210">Log in tooyour **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="96f0b-211">Последовательно выберите пункты **Manage Users \> Manage Users Home \> + Create Employee** (Управление пользователями > Управление домашним ресурсом пользователей > + Создать сотрудника).</span><span class="sxs-lookup"><span data-stu-id="96f0b-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="96f0b-212">![Создание сотрудника](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Создание сотрудника")</span><span class="sxs-lookup"><span data-stu-id="96f0b-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="96f0b-213">На hello **основные сведения** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="96f0b-213">On hello **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="96f0b-214">![Основные сведения](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Основные сведения")</span><span class="sxs-lookup"><span data-stu-id="96f0b-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="96f0b-215">а.</span><span class="sxs-lookup"><span data-stu-id="96f0b-215">a.</span></span> <span data-ttu-id="96f0b-216">В hello **адрес электронной почты** в текстовое поле введите адрес электронной почты hello Саймон Britta как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="96f0b-216">In hello **Email Address** textbox, type hello email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="96f0b-217">b.</span><span class="sxs-lookup"><span data-stu-id="96f0b-217">b.</span></span> <span data-ttu-id="96f0b-218">В hello **имя** введите **имя** пользователя как **Britta**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-218">In hello **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="96f0b-219">c.</span><span class="sxs-lookup"><span data-stu-id="96f0b-219">c.</span></span> <span data-ttu-id="96f0b-220">В hello **Фамилия** введите **Фамилия** пользователя как **Simon**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-220">In hello **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="96f0b-221">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="96f0b-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="96f0b-222">Владелец учетной записи Azure AD Hello получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной. Можно использовать любые другие Citrix ShareFile пользователя средства создания учетных записей или интерфейсы API, предоставляемые Citrix ShareFile tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96f0b-222">hello Azure AD account holder will receive an email and follow a link tooconfirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="96f0b-223">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="96f0b-223">Assign hello Azure AD test user</span></span>

<span data-ttu-id="96f0b-224">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="96f0b-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix ShareFile.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="96f0b-226">**tooassign Britta Simon tooCitrix ShareFile, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96f0b-226">**tooassign Britta Simon tooCitrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="96f0b-227">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="96f0b-229">В списке приложений hello выберите **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-229">In hello applications list, select **Citrix ShareFile**.</span></span>

    ![Hello Citrix ShareFile ссылку в списке приложений hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="96f0b-231">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="96f0b-233">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-233">Click **Add** button.</span></span> <span data-ttu-id="96f0b-234">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="96f0b-236">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="96f0b-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="96f0b-237">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96f0b-238">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="96f0b-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="96f0b-239">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="96f0b-239">Test single sign-on</span></span>

<span data-ttu-id="96f0b-240">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="96f0b-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="96f0b-241">При нажатии кнопки hello Citrix ShareFile плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour приложение Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="96f0b-241">When you click hello Citrix ShareFile tile in hello Access Panel, you should get automatically signed-on tooyour Citrix ShareFile application.</span></span>
<span data-ttu-id="96f0b-242">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="96f0b-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="96f0b-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="96f0b-243">Additional resources</span></span>

* [<span data-ttu-id="96f0b-244">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96f0b-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96f0b-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="96f0b-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

