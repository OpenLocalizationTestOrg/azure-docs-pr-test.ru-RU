---
title: "Руководство по интеграции Azure Active Directory с Recognize | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и распознать."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="78987-103">Руководство по интеграции Azure Active Directory с Recognize</span><span class="sxs-lookup"><span data-stu-id="78987-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="78987-104">В этом учебнике вы узнаете, как распознать toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78987-104">In this tutorial, you learn how toointegrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78987-105">Интеграция с Azure AD распознать предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="78987-105">Integrating Recognize with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="78987-106">Можно управлять в Azure AD, имеющего доступ tooRecognize</span><span class="sxs-lookup"><span data-stu-id="78987-106">You can control in Azure AD who has access tooRecognize</span></span>
- <span data-ttu-id="78987-107">Можно включить на пользователей tooautomatically get вошедшего tooRecognize (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="78987-107">You can enable your users tooautomatically get signed-on tooRecognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78987-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="78987-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="78987-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="78987-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78987-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="78987-110">Prerequisites</span></span>

<span data-ttu-id="78987-111">Интеграция Azure AD tooconfigure распознать, необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="78987-111">tooconfigure Azure AD integration with Recognize, you need hello following items:</span></span>

- <span data-ttu-id="78987-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="78987-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78987-113">подписка Recognize с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="78987-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78987-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="78987-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78987-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="78987-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78987-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="78987-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78987-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78987-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78987-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="78987-118">Scenario description</span></span>
<span data-ttu-id="78987-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="78987-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78987-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="78987-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78987-121">Добавление распознать из галереи hello</span><span class="sxs-lookup"><span data-stu-id="78987-121">Adding Recognize from hello gallery</span></span>
2. <span data-ttu-id="78987-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="78987-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-hello-gallery"></a><span data-ttu-id="78987-123">Добавление распознать из галереи hello</span><span class="sxs-lookup"><span data-stu-id="78987-123">Adding Recognize from hello gallery</span></span>
<span data-ttu-id="78987-124">tooconfigure hello интеграции распознать в Azure AD, вы должны tooadd распознать из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="78987-124">tooconfigure hello integration of Recognize into Azure AD, you need tooadd Recognize from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="78987-125">**tooadd распознать из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="78987-125">**tooadd Recognize from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="78987-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="78987-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="78987-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="78987-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="78987-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="78987-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="78987-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="78987-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="78987-133">Введите в поле поиска hello **распознать**.</span><span class="sxs-lookup"><span data-stu-id="78987-133">In hello search box, type **Recognize**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="78987-135">В панели результатов hello выберите **распознать**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78987-135">In hello results panel, select **Recognize**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78987-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="78987-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78987-138">В этом разделе описана настройка и проверка единого входа Azure AD в Recognize с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78987-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="78987-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в распознать является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78987-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Recognize is tooa user in Azure AD.</span></span> <span data-ttu-id="78987-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в распознать должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="78987-140">In other words, a link relationship between an Azure AD user and hello related user in Recognize needs toobe established.</span></span>

<span data-ttu-id="78987-141">В распознать, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="78987-141">In Recognize, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="78987-142">tooconfigure и Azure AD тестирования единого входа с распознать, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="78987-142">tooconfigure and test Azure AD single sign-on with Recognize, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="78987-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="78987-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="78987-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="78987-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78987-145">**[Создание тестового пользователя распознать](#creating-a-recognize-test-user)**  -toohave аналог Саймон Britta в распознать, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="78987-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - toohave a counterpart of Britta Simon in Recognize that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="78987-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="78987-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78987-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="78987-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78987-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="78987-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78987-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении распознать.</span><span class="sxs-lookup"><span data-stu-id="78987-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="78987-150">**tooconfigure Azure AD единого входа с распознать, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="78987-150">**tooconfigure Azure AD single sign-on with Recognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="78987-151">В hello в hello портала Azure **распознать** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="78987-151">In hello Azure portal, on hello **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="78987-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="78987-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="78987-155">На hello **URL-адреса и домена распознавать** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="78987-155">On hello **Recognize Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="78987-157">а.</span><span class="sxs-lookup"><span data-stu-id="78987-157">a.</span></span> <span data-ttu-id="78987-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="78987-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="78987-159">b.</span><span class="sxs-lookup"><span data-stu-id="78987-159">b.</span></span> <span data-ttu-id="78987-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="78987-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="78987-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="78987-161">These values are not real.</span></span> <span data-ttu-id="78987-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="78987-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="78987-163">Обратитесь к [группа поддержки распознать клиента](mailto:support@recognizeapp.com) получить URL-адрес входа и вы можно получить значение идентификатора, открыв hello URL-адрес метаданных поставщика службы из hello раздел параметров единого входа, который описан далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="78987-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening hello Service Provider Metadata URL from hello SSO Settings section that is explained later in hello tutorial.</span></span> <span data-ttu-id="78987-164">.</span><span class="sxs-lookup"><span data-stu-id="78987-164">.</span></span> 
 
4. <span data-ttu-id="78987-165">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="78987-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="78987-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="78987-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78987-169">На hello **распознает конфигурации** щелкните **Настройка распознает** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="78987-169">On hello **Recognize Configuration** section, click **Configure Recognize** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="78987-170">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="78987-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="78987-172">В другом окне браузера, клиент распознать tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="78987-172">In a different web browser window, sign-on tooyour Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="78987-173">На hello правый верхний угол, щелкните **меню**.</span><span class="sxs-lookup"><span data-stu-id="78987-173">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="78987-174">Go слишком**администратор организации**.</span><span class="sxs-lookup"><span data-stu-id="78987-174">Go too**Company Admin**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="78987-176">На панели навигации слева hello, нажмите кнопку **параметры**.</span><span class="sxs-lookup"><span data-stu-id="78987-176">On hello left navigation pane, click **Settings**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="78987-178">Выполнить hello, выполните действия **настройки единого входа** раздела.</span><span class="sxs-lookup"><span data-stu-id="78987-178">Perform hello following steps on **SSO Settings** section.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="78987-180">а.</span><span class="sxs-lookup"><span data-stu-id="78987-180">a.</span></span> <span data-ttu-id="78987-181">Для параметра **Enable SSO** (Включить единый вход) установите значение **ON** (Включено).</span><span class="sxs-lookup"><span data-stu-id="78987-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="78987-182">b.</span><span class="sxs-lookup"><span data-stu-id="78987-182">b.</span></span> <span data-ttu-id="78987-183">В hello **идентификатор сущности поставщика Удостоверений** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="78987-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="78987-184">c.</span><span class="sxs-lookup"><span data-stu-id="78987-184">c.</span></span> <span data-ttu-id="78987-185">В hello **URL-адрес единого входа для целевого** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="78987-185">In hello **Sso target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="78987-186">d.</span><span class="sxs-lookup"><span data-stu-id="78987-186">d.</span></span> <span data-ttu-id="78987-187">В hello **цели уровня обслуживания целевой URL-адрес** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="78987-187">In hello **Slo target url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="78987-188">д.</span><span class="sxs-lookup"><span data-stu-id="78987-188">e.</span></span> <span data-ttu-id="78987-189">Откройте ваш загруженный **сертификата (Base64)** в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="78987-189">Open your downloaded **Certificate (Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="78987-190">f.</span><span class="sxs-lookup"><span data-stu-id="78987-190">f.</span></span> <span data-ttu-id="78987-191">Нажмите кнопку hello **сохранить параметры** кнопки.</span><span class="sxs-lookup"><span data-stu-id="78987-191">Click hello **Save settings** button.</span></span> 

11. <span data-ttu-id="78987-192">Рядом с hello **настройки единого входа** скопируйте URL-адресом hello в **URL-адрес метаданных службы поставщика**.</span><span class="sxs-lookup"><span data-stu-id="78987-192">Beside hello **SSO Settings** section, copy hello URL under **Service Provider Metadata url**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="78987-194">Откройте hello **ссылку на URL-адрес метаданных** в документ метаданных hello toodownload обозревателя было пустым.</span><span class="sxs-lookup"><span data-stu-id="78987-194">Open hello **Metadata URL link** under a blank browser toodownload hello metadata document.</span></span> <span data-ttu-id="78987-195">Затем скопируйте hello EntityDescriptor value(entityID) из файла hello и вставьте его в **идентификатор** текстовое поле в **распознает доменов и URL-адреса раздела** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="78987-195">Then copy hello EntityDescriptor value(entityID) from hello file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="78987-197">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="78987-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="78987-198">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="78987-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="78987-199">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78987-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78987-200">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="78987-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="78987-201">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="78987-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="78987-203">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="78987-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="78987-204">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="78987-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78987-206">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="78987-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78987-208">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="78987-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78987-210">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="78987-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78987-212">а.</span><span class="sxs-lookup"><span data-stu-id="78987-212">a.</span></span> <span data-ttu-id="78987-213">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78987-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78987-214">b.</span><span class="sxs-lookup"><span data-stu-id="78987-214">b.</span></span> <span data-ttu-id="78987-215">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="78987-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78987-216">c.</span><span class="sxs-lookup"><span data-stu-id="78987-216">c.</span></span> <span data-ttu-id="78987-217">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="78987-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="78987-218">d.</span><span class="sxs-lookup"><span data-stu-id="78987-218">d.</span></span> <span data-ttu-id="78987-219">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="78987-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="78987-220">Создание тестового пользователя Recognize</span><span class="sxs-lookup"><span data-stu-id="78987-220">Creating a Recognize test user</span></span>

<span data-ttu-id="78987-221">В порядке tooenable toolog пользователей Azure AD в распознать их необходимо подготовить в распознать.</span><span class="sxs-lookup"><span data-stu-id="78987-221">In order tooenable Azure AD users toolog into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="78987-222">В случае hello распознать Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="78987-222">In hello case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="78987-223">Это приложение не поддерживает подготовку SCIM, но предусматривает альтернативный механизм синхронизации для подготовки пользователей.</span><span class="sxs-lookup"><span data-stu-id="78987-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="78987-224">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="78987-224">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="78987-225">Войдите на корпоративный сайт Recognize в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="78987-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="78987-226">На hello правый верхний угол, щелкните **меню**.</span><span class="sxs-lookup"><span data-stu-id="78987-226">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="78987-227">Go слишком**администратор организации**.</span><span class="sxs-lookup"><span data-stu-id="78987-227">Go too**Company Admin**.</span></span>

3. <span data-ttu-id="78987-228">На панели навигации слева hello, нажмите кнопку **параметры**.</span><span class="sxs-lookup"><span data-stu-id="78987-228">On hello left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="78987-229">Выполнить hello, выполните действия **синхронизации пользователей** раздела.</span><span class="sxs-lookup"><span data-stu-id="78987-229">Perform hello following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="78987-230">![Новый пользователь](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="78987-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="78987-231">а.</span><span class="sxs-lookup"><span data-stu-id="78987-231">a.</span></span> <span data-ttu-id="78987-232">В поле **Sync Enabled** (Синхронизация включена) выберите **ON** (Включено).</span><span class="sxs-lookup"><span data-stu-id="78987-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="78987-233">b.</span><span class="sxs-lookup"><span data-stu-id="78987-233">b.</span></span> <span data-ttu-id="78987-234">Для параметра **Choose sync provider** (Выбор поставщика синхронизации) выберите значение **Microsoft/Office 365**.</span><span class="sxs-lookup"><span data-stu-id="78987-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="78987-235">c.</span><span class="sxs-lookup"><span data-stu-id="78987-235">c.</span></span> <span data-ttu-id="78987-236">Щелкните **Run User Sync** (Запустить синхронизацию пользователей).</span><span class="sxs-lookup"><span data-stu-id="78987-236">Click **Run User Sync**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="78987-237">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="78987-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="78987-238">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooRecognize доступа.</span><span class="sxs-lookup"><span data-stu-id="78987-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRecognize.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="78987-240">**tooassign tooRecognize Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="78987-240">**tooassign Britta Simon tooRecognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="78987-241">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="78987-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="78987-243">В списке приложений hello выберите **распознать**.</span><span class="sxs-lookup"><span data-stu-id="78987-243">In hello applications list, select **Recognize**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="78987-245">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="78987-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="78987-247">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="78987-247">Click **Add** button.</span></span> <span data-ttu-id="78987-248">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="78987-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="78987-250">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="78987-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="78987-251">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="78987-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78987-252">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="78987-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78987-253">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="78987-253">Testing single sign-on</span></span>

<span data-ttu-id="78987-254">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="78987-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="78987-255">При выборе плитки распознать hello в hello панели доступа, следует получать автоматически вошедшего tooyour распознать приложения.</span><span class="sxs-lookup"><span data-stu-id="78987-255">When you click hello Recognize tile in hello Access Panel, you should get automatically signed-on tooyour Recognize application.</span></span> <span data-ttu-id="78987-256">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="78987-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78987-257">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="78987-257">Additional resources</span></span>

* [<span data-ttu-id="78987-258">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78987-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78987-259">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78987-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

