---
title: "Учебник. Интеграция Azure Active Directory с Skillport | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Skillport."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: ba504c3cae5f92767eb90d8453887904690fe0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="8cd12-103">Руководство по интеграции Azure Active Directory с Skillport</span><span class="sxs-lookup"><span data-stu-id="8cd12-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="8cd12-104">В этом учебнике вы узнаете, как toointegrate Skillport с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8cd12-104">In this tutorial, you learn how toointegrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8cd12-105">Интеграция с Azure AD Skillport предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8cd12-105">Integrating Skillport with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8cd12-106">Можно управлять в Azure AD, имеющего доступ tooSkillport</span><span class="sxs-lookup"><span data-stu-id="8cd12-106">You can control in Azure AD who has access tooSkillport</span></span>
- <span data-ttu-id="8cd12-107">Можно включить на пользователей tooautomatically get вошедшего tooSkillport (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cd12-107">You can enable your users tooautomatically get signed-on tooSkillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8cd12-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8cd12-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8cd12-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8cd12-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cd12-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8cd12-110">Prerequisites</span></span>

<span data-ttu-id="8cd12-111">tooconfigure интеграция Azure AD с Skillport требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8cd12-111">tooconfigure Azure AD integration with Skillport, you need hello following items:</span></span>

- <span data-ttu-id="8cd12-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8cd12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8cd12-113">подписка на Skillport с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8cd12-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8cd12-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8cd12-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8cd12-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8cd12-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8cd12-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8cd12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8cd12-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8cd12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8cd12-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8cd12-118">Scenario description</span></span>
<span data-ttu-id="8cd12-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8cd12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8cd12-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8cd12-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8cd12-121">Добавление Skillport из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8cd12-121">Adding Skillport from hello gallery</span></span>
2. <span data-ttu-id="8cd12-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cd12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-hello-gallery"></a><span data-ttu-id="8cd12-123">Добавление Skillport из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8cd12-123">Adding Skillport from hello gallery</span></span>
<span data-ttu-id="8cd12-124">tooconfigure hello интеграции Skillport в Azure AD, вы должны tooadd Skillport из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8cd12-124">tooconfigure hello integration of Skillport into Azure AD, you need tooadd Skillport from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8cd12-125">**tooadd Skillport из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8cd12-125">**tooadd Skillport from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cd12-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8cd12-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8cd12-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8cd12-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8cd12-131">Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="8cd12-131">Click **New Application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8cd12-133">Введите в поле поиска hello **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-133">In hello search box, type **Skillport**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="8cd12-135">В панели результатов hello выберите **Skillport**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8cd12-135">In hello results panel, select **Skillport**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8cd12-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cd12-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8cd12-138">В этом разделе описана настройка и проверка единого входа Azure AD в Skillport с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8cd12-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8cd12-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Skillport является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd12-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Skillport is tooa user in Azure AD.</span></span> <span data-ttu-id="8cd12-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Skillport должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8cd12-140">In other words, a link relationship between an Azure AD user and hello related user in Skillport needs toobe established.</span></span>

<span data-ttu-id="8cd12-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Skillport.</span><span class="sxs-lookup"><span data-stu-id="8cd12-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Skillport.</span></span>

<span data-ttu-id="8cd12-142">tooconfigure и теста Azure AD единого входа с Skillport, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8cd12-142">tooconfigure and test Azure AD single sign-on with Skillport, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8cd12-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8cd12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8cd12-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8cd12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8cd12-145">**[Создание тестового пользователя Skillport](#creating-a-skillport-test-user)**  -toohave аналог Саймон Britta в Skillport, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8cd12-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - toohave a counterpart of Britta Simon in Skillport that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8cd12-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8cd12-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8cd12-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8cd12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8cd12-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cd12-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8cd12-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Skillport.</span><span class="sxs-lookup"><span data-stu-id="8cd12-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="8cd12-150">**tooconfigure Azure AD единого входа с Skillport, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8cd12-150">**tooconfigure Azure AD single sign-on with Skillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cd12-151">В hello в hello портала Azure **Skillport** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-151">In hello Azure  portal, on hello **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8cd12-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8cd12-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="8cd12-155">На hello **URL-адреса и домена Skillport** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8cd12-155">On hello **Skillport Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="8cd12-157">а.</span><span class="sxs-lookup"><span data-stu-id="8cd12-157">a.</span></span> <span data-ttu-id="8cd12-158">В hello **URL-адрес входа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="8cd12-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span>
      
      <span data-ttu-id="8cd12-159">Центр обработки данных в ЕС: `https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="8cd12-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="8cd12-160">Центр обработки данных в США: `https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="8cd12-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="8cd12-161">b.</span><span class="sxs-lookup"><span data-stu-id="8cd12-161">b.</span></span> <span data-ttu-id="8cd12-162">В hello **URL-адрес ответа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="8cd12-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span>
    
      <span data-ttu-id="8cd12-163">Центр обработки данных в ЕС: `https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="8cd12-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="8cd12-164">Центр обработки данных в США: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="8cd12-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8cd12-165">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="8cd12-165">These values are not hello real.</span></span> <span data-ttu-id="8cd12-166">Обновите эти значения с hello фактический URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="8cd12-166">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="8cd12-167">Обратитесь к [группа поддержки клиента Skillport](https://www.skillsoft.com/contact.asp) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="8cd12-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) tooget these values.</span></span>
 
4. <span data-ttu-id="8cd12-168">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8cd12-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="8cd12-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8cd12-170">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8cd12-172">tooconfigure единого входа на **Skillport** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Skillport поддержки](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="8cd12-172">tooconfigure single sign-on on **Skillport** side, you need toosend hello downloaded **Metadata XML** too[Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="8cd12-173">Они устанавливаются его toohave hello правильно настроенной на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="8cd12-173">They will set it up toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8cd12-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cd12-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="8cd12-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8cd12-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8cd12-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8cd12-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cd12-178">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8cd12-178">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8cd12-180">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="8cd12-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8cd12-182">Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8cd12-182">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8cd12-184">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8cd12-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8cd12-186">а.</span><span class="sxs-lookup"><span data-stu-id="8cd12-186">a.</span></span> <span data-ttu-id="8cd12-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8cd12-188">b.</span><span class="sxs-lookup"><span data-stu-id="8cd12-188">b.</span></span> <span data-ttu-id="8cd12-189">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8cd12-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8cd12-190">c.</span><span class="sxs-lookup"><span data-stu-id="8cd12-190">c.</span></span> <span data-ttu-id="8cd12-191">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8cd12-192">d.</span><span class="sxs-lookup"><span data-stu-id="8cd12-192">d.</span></span> <span data-ttu-id="8cd12-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="8cd12-194">Создание тестового пользователя Skillport</span><span class="sxs-lookup"><span data-stu-id="8cd12-194">Creating a Skillport test user</span></span>

<span data-ttu-id="8cd12-195">Порядок toocreate Skillport тестового пользователя нужен toocontact [Skillport поддержки](https://www.skillsoft.com/contact.asp) они имеют несколько бизнес-сценариев, в соответствии с требованием toohello конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="8cd12-195">In order toocreate Skillport test user, you need toocontact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according toohello requirement of end user.</span></span> <span data-ttu-id="8cd12-196">Компания будет настраивать после обсуждения с пользователями hello.</span><span class="sxs-lookup"><span data-stu-id="8cd12-196">They will configure it after discussion with hello users.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8cd12-197">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8cd12-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8cd12-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSkillport доступа.</span><span class="sxs-lookup"><span data-stu-id="8cd12-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkillport.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8cd12-200">**tooassign tooSkillport Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8cd12-200">**tooassign Britta Simon tooSkillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cd12-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8cd12-203">В списке приложений hello выберите **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-203">In hello applications list, select **Skillport**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="8cd12-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8cd12-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-207">Click **Add** button.</span></span> <span data-ttu-id="8cd12-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8cd12-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8cd12-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8cd12-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8cd12-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8cd12-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8cd12-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8cd12-213">Testing single sign-on</span></span>

<span data-ttu-id="8cd12-214">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="8cd12-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8cd12-215">При нажатии кнопки hello Skillport плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Skillport приложения.</span><span class="sxs-lookup"><span data-stu-id="8cd12-215">When you click hello Skillport tile in hello Access Panel, you should get automatically signed-on tooyour Skillport application.</span></span>
<span data-ttu-id="8cd12-216">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="8cd12-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8cd12-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8cd12-217">Additional resources</span></span>

* [<span data-ttu-id="8cd12-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8cd12-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8cd12-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8cd12-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

