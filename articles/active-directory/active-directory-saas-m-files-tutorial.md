---
title: "Учебник. Интеграция Azure Active Directory с M-Files | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и M-файлами."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="c5deb-103">Учебник. Интеграция Azure Active Directory с M-Files</span><span class="sxs-lookup"><span data-stu-id="c5deb-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="c5deb-104">В этом учебнике вы узнаете, как toointegrate M-файлы с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5deb-104">In this tutorial, you learn how toointegrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5deb-105">Интеграция M-файлы с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c5deb-105">Integrating M-Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5deb-106">Можно управлять в Azure AD, имеющего доступ tooM файлы</span><span class="sxs-lookup"><span data-stu-id="c5deb-106">You can control in Azure AD who has access tooM-Files</span></span>
- <span data-ttu-id="c5deb-107">Можно включить пользователей tooautomatically get вошедшего tooM файлов (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5deb-107">You can enable your users tooautomatically get signed-on tooM-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5deb-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c5deb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c5deb-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5deb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5deb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c5deb-110">Prerequisites</span></span>

<span data-ttu-id="c5deb-111">tooconfigure интеграция Azure AD с M-файлы, необходимые hello следующих элементов.</span><span class="sxs-lookup"><span data-stu-id="c5deb-111">tooconfigure Azure AD integration with M-Files, you need hello following items:</span></span>

- <span data-ttu-id="c5deb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c5deb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5deb-113">подписка M-Files с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c5deb-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5deb-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c5deb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5deb-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c5deb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5deb-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c5deb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5deb-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5deb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5deb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c5deb-118">Scenario description</span></span>
<span data-ttu-id="c5deb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c5deb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5deb-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c5deb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5deb-121">Добавление файлов M из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c5deb-121">Adding M-Files from hello gallery</span></span>
2. <span data-ttu-id="c5deb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5deb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-hello-gallery"></a><span data-ttu-id="c5deb-123">Добавление файлов M из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c5deb-123">Adding M-Files from hello gallery</span></span>
<span data-ttu-id="c5deb-124">tooconfigure hello интеграция M-файлов в Azure AD, вы должны tooadd M-файлов из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c5deb-124">tooconfigure hello integration of M-Files into Azure AD, you need tooadd M-Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5deb-125">**tooadd M-файлы из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c5deb-125">**tooadd M-Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5deb-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c5deb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5deb-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5deb-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c5deb-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c5deb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c5deb-133">Введите в поле поиска hello **M файлы**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-133">In hello search box, type **M-Files**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="c5deb-135">В панели результатов hello, выберите **M файлы**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c5deb-135">In hello results panel, select **M-Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5deb-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5deb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5deb-138">В этом разделе описана настройка и проверка единого входа Azure AD в M-Files с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5deb-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5deb-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в файлах M является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5deb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in M-Files is tooa user in Azure AD.</span></span> <span data-ttu-id="c5deb-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в файлах M должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c5deb-140">In other words, a link relationship between an Azure AD user and hello related user in M-Files needs toobe established.</span></span>

<span data-ttu-id="c5deb-141">M-файлы, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="c5deb-141">In M-Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c5deb-142">tooconfigure и теста Azure AD единого входа с M-файлы, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="c5deb-142">tooconfigure and test Azure AD single sign-on with M-Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5deb-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c5deb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5deb-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c5deb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5deb-145">**[Создание тестового пользователя файлы M](#creating-a-m-files-test-user)**  -toohave аналог Саймон Britta M-файлы, — представление связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c5deb-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - toohave a counterpart of Britta Simon in M-Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5deb-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c5deb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5deb-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c5deb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5deb-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5deb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5deb-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении M-файлы.</span><span class="sxs-lookup"><span data-stu-id="c5deb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="c5deb-150">**tooconfigure Azure AD единого входа с M-файлы, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c5deb-150">**tooconfigure Azure AD single sign-on with M-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5deb-151">В hello в hello портала Azure **M файлы** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-151">In hello Azure portal, on hello **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c5deb-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c5deb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="c5deb-155">На hello **домена M-файлы и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c5deb-155">On hello **M-Files Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="c5deb-157">а.</span><span class="sxs-lookup"><span data-stu-id="c5deb-157">a.</span></span> <span data-ttu-id="c5deb-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="c5deb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="c5deb-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5deb-159">b.</span></span> <span data-ttu-id="c5deb-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="c5deb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5deb-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c5deb-161">These values are not real.</span></span> <span data-ttu-id="c5deb-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="c5deb-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c5deb-163">Обратитесь к [клиента M файлы поддержки](mailto:support@m-files.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="c5deb-163">Contact [M-Files Client support team](mailto:support@m-files.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="c5deb-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c5deb-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="c5deb-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c5deb-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5deb-168">tooget SSO настроен для вашего приложения, обратитесь в службу [M файлы поддержки](mailto:support@m-files.com) и сообщите hello загрузки метаданных.</span><span class="sxs-lookup"><span data-stu-id="c5deb-168">tooget SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them hello downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="c5deb-169">Выполните следующие шаги hello tooconfigure единого входа для вас классического приложения M-файл.</span><span class="sxs-lookup"><span data-stu-id="c5deb-169">Follow hello next steps if you want tooconfigure SSO for you M-File desktop application.</span></span> <span data-ttu-id="c5deb-170">Без дополнительных шагов не требуется, если требуется только tooconfigure единого входа для веб-версию M-файлы.</span><span class="sxs-lookup"><span data-stu-id="c5deb-170">No extra steps are required if you only want tooconfigure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="c5deb-171">Выполните hello далее шаги tooconfigure hello M файл классического приложения tooenable единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5deb-171">Follow hello next steps tooconfigure hello M-File desktop application tooenable SSO with Azure AD.</span></span> <span data-ttu-id="c5deb-172">toodownload M-файлов, перейдите в слишком[M файлы загрузки](https://www.m-files.com/en/download-latest-version) страницы.</span><span class="sxs-lookup"><span data-stu-id="c5deb-172">toodownload M-Files, go too[M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="c5deb-173">Откройте hello **параметры рабочего стола M файлы** окна.</span><span class="sxs-lookup"><span data-stu-id="c5deb-173">Open hello **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="c5deb-174">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-174">Then, click **Add**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="c5deb-176">На hello **свойств подключения документа хранилище** окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c5deb-176">On hello **Document Vault Connection Properties** window, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="c5deb-178">В разделе hello тип раздела сервера hello значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c5deb-178">Under hello Server section type, hello values as follows:</span></span>  

    <span data-ttu-id="c5deb-179">а.</span><span class="sxs-lookup"><span data-stu-id="c5deb-179">a.</span></span> <span data-ttu-id="c5deb-180">В поле **Name** (Имя) введите `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="c5deb-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="c5deb-181">b.</span><span class="sxs-lookup"><span data-stu-id="c5deb-181">b.</span></span> <span data-ttu-id="c5deb-182">В поле **Port Number** (Номер порта) введите **4466**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="c5deb-183">c.</span><span class="sxs-lookup"><span data-stu-id="c5deb-183">c.</span></span> <span data-ttu-id="c5deb-184">Для параметра **Protocol** (Протокол) выберите **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="c5deb-185">d.</span><span class="sxs-lookup"><span data-stu-id="c5deb-185">d.</span></span> <span data-ttu-id="c5deb-186">В hello **проверки подлинности** выберите **конкретный пользователь Windows**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-186">In hello **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="c5deb-187">Затем отобразится страница подписи.</span><span class="sxs-lookup"><span data-stu-id="c5deb-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="c5deb-188">Введите свои учетные данные Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5deb-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="c5deb-189">д.</span><span class="sxs-lookup"><span data-stu-id="c5deb-189">e.</span></span> <span data-ttu-id="c5deb-190">Для hello **хранилища на сервере**, выберите hello соответствующее хранилище на сервере.</span><span class="sxs-lookup"><span data-stu-id="c5deb-190">For hello **Vault on Server**,  select hello corresponding vault on server.</span></span>
 
    <span data-ttu-id="c5deb-191">f.</span><span class="sxs-lookup"><span data-stu-id="c5deb-191">f.</span></span> <span data-ttu-id="c5deb-192">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="c5deb-193">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c5deb-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5deb-194">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c5deb-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5deb-195">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5deb-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5deb-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5deb-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5deb-197">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c5deb-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c5deb-199">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c5deb-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5deb-200">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c5deb-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5deb-202">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5deb-204">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="c5deb-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5deb-206">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c5deb-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5deb-208">а.</span><span class="sxs-lookup"><span data-stu-id="c5deb-208">a.</span></span> <span data-ttu-id="c5deb-209">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5deb-210">b.</span><span class="sxs-lookup"><span data-stu-id="c5deb-210">b.</span></span> <span data-ttu-id="c5deb-211">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c5deb-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5deb-212">c.</span><span class="sxs-lookup"><span data-stu-id="c5deb-212">c.</span></span> <span data-ttu-id="c5deb-213">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5deb-214">d.</span><span class="sxs-lookup"><span data-stu-id="c5deb-214">d.</span></span> <span data-ttu-id="c5deb-215">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="c5deb-216">Создание тестового пользователя M-Files</span><span class="sxs-lookup"><span data-stu-id="c5deb-216">Creating a M-Files test user</span></span>

<span data-ttu-id="c5deb-217">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon M-файлы.</span><span class="sxs-lookup"><span data-stu-id="c5deb-217">hello objective of this section is toocreate a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="c5deb-218">Работать с [M файлы поддержки](mailto:support@m-files.com) tooadd пользователей hello в hello M-файлы.</span><span class="sxs-lookup"><span data-stu-id="c5deb-218">Work with  [M-Files support team](mailto:support@m-files.com) tooadd hello users in hello M-Files.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5deb-219">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c5deb-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5deb-220">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа к tooM файлам.</span><span class="sxs-lookup"><span data-stu-id="c5deb-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooM-Files.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c5deb-222">**tooassign tooM Britta Simon-файлы, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="c5deb-222">**tooassign Britta Simon tooM-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5deb-223">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c5deb-225">В списке приложений hello выберите **M файлы**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-225">In hello applications list, select **M-Files**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="c5deb-227">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c5deb-229">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-229">Click **Add** button.</span></span> <span data-ttu-id="c5deb-230">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c5deb-232">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c5deb-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5deb-233">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5deb-234">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5deb-235">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c5deb-235">Testing single sign-on</span></span>

<span data-ttu-id="c5deb-236">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="c5deb-236">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5deb-237">При нажатии кнопки hello M файлы плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour M файлы приложения.</span><span class="sxs-lookup"><span data-stu-id="c5deb-237">When you click hello M-Files tile in hello Access Panel, you should get automatically signed-on tooyour M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5deb-238">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c5deb-238">Additional resources</span></span>

* [<span data-ttu-id="c5deb-239">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5deb-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5deb-240">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5deb-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

