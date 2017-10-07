---
title: "Руководство по интеграции Azure Active Directory с ThirdLight | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ThirdLight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a510e514f6a8c4e89220b9a6f6db29668b451b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="f2ec2-103">Учебник. Интеграция Azure Active Directory с ThirdLight</span><span class="sxs-lookup"><span data-stu-id="f2ec2-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="f2ec2-104">В этом учебнике вы узнаете, как toointegrate ThirdLight с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f2ec2-104">In this tutorial, you learn how toointegrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f2ec2-105">Интеграция с Azure AD ThirdLight предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f2ec2-105">Integrating ThirdLight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f2ec2-106">Можно управлять в Azure AD, имеющего доступ tooThirdLight</span><span class="sxs-lookup"><span data-stu-id="f2ec2-106">You can control in Azure AD who has access tooThirdLight</span></span>
- <span data-ttu-id="f2ec2-107">Можно включить на пользователей tooautomatically get вошедшего tooThirdLight (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2ec2-107">You can enable your users tooautomatically get signed-on tooThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f2ec2-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f2ec2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f2ec2-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f2ec2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2ec2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f2ec2-110">Prerequisites</span></span>

<span data-ttu-id="f2ec2-111">tooconfigure интеграция Azure AD с ThirdLight требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f2ec2-111">tooconfigure Azure AD integration with ThirdLight, you need hello following items:</span></span>

- <span data-ttu-id="f2ec2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f2ec2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f2ec2-113">подписка ThirdLight с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f2ec2-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f2ec2-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f2ec2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f2ec2-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f2ec2-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2ec2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f2ec2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f2ec2-118">Scenario description</span></span>
<span data-ttu-id="f2ec2-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f2ec2-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f2ec2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f2ec2-121">Добавление ThirdLight из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f2ec2-121">Adding ThirdLight from hello gallery</span></span>
2. <span data-ttu-id="f2ec2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2ec2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-hello-gallery"></a><span data-ttu-id="f2ec2-123">Добавление ThirdLight из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f2ec2-123">Adding ThirdLight from hello gallery</span></span>
<span data-ttu-id="f2ec2-124">tooconfigure hello интеграции ThirdLight в Azure AD, вы должны tooadd ThirdLight из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-124">tooconfigure hello integration of ThirdLight into Azure AD, you need tooadd ThirdLight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f2ec2-125">**tooadd ThirdLight из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f2ec2-125">**tooadd ThirdLight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2ec2-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f2ec2-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f2ec2-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f2ec2-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f2ec2-133">Введите в поле поиска hello **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-133">In hello search box, type **ThirdLight**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="f2ec2-135">В панели результатов hello выберите **ThirdLight**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-135">In hello results panel, select **ThirdLight**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f2ec2-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2ec2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f2ec2-138">В этом разделе описана настройка и проверка единого входа Azure AD в ThirdLight с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f2ec2-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ThirdLight является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThirdLight is tooa user in Azure AD.</span></span> <span data-ttu-id="f2ec2-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в ThirdLight должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-140">In other words, a link relationship between an Azure AD user and hello related user in ThirdLight needs toobe established.</span></span>

<span data-ttu-id="f2ec2-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ThirdLight.</span></span>

<span data-ttu-id="f2ec2-142">tooconfigure и теста Azure AD единого входа с ThirdLight, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f2ec2-142">tooconfigure and test Azure AD single sign-on with ThirdLight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f2ec2-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f2ec2-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f2ec2-145">**[Создание тестового пользователя ThirdLight](#creating-a-thirdlight-test-user)**  -toohave аналог Саймон Britta в ThirdLight, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - toohave a counterpart of Britta Simon in ThirdLight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f2ec2-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f2ec2-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f2ec2-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2ec2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f2ec2-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="f2ec2-150">**tooconfigure Azure AD единого входа с ThirdLight, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f2ec2-150">**tooconfigure Azure AD single sign-on with ThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2ec2-151">В hello в hello портала Azure **ThirdLight** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-151">In hello Azure portal, on hello **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f2ec2-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="f2ec2-155">На hello **URL-адреса и домена ThirdLight** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f2ec2-155">On hello **ThirdLight Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="f2ec2-157">а.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-157">a.</span></span> <span data-ttu-id="f2ec2-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="f2ec2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="f2ec2-159">b.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-159">b.</span></span> <span data-ttu-id="f2ec2-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="f2ec2-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f2ec2-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-161">These values are not real.</span></span> <span data-ttu-id="f2ec2-162">Обновить значения hello фактический URL-адрес входа и Identiifer.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-162">Update these values with hello actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="f2ec2-163">Обратитесь к [группа поддержки клиента ThirdLight](https://www.thirdlight.com/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="f2ec2-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="f2ec2-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f2ec2-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f2ec2-168">В другом окне браузера Войдите на сайте компании ThirdLight tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-168">In a different web browser window, log in tooyour ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="f2ec2-169">Go слишком**конфигурации \> системное администрирование**, а затем нажмите кнопку **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-169">Go too**Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="f2ec2-170">![Администрирование системы](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Администрирование системы")</span><span class="sxs-lookup"><span data-stu-id="f2ec2-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="f2ec2-171">В разделе "Конфигурация" hello SAML2 выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-171">In hello SAML2 configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f2ec2-172">![Единый вход SAML](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "Единый вход SAML")</span><span class="sxs-lookup"><span data-stu-id="f2ec2-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="f2ec2-173">а.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-173">a.</span></span> <span data-ttu-id="f2ec2-174">Выберите параметр **Разрешить единый вход SAML2**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="f2ec2-175">b.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-175">b.</span></span> <span data-ttu-id="f2ec2-176">В качестве **источника для метаданных IdP** выберите **Load IdP Metadata from XML** (Загрузить метаданные IdP из XML).</span><span class="sxs-lookup"><span data-stu-id="f2ec2-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="f2ec2-177">c.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-177">c.</span></span> <span data-ttu-id="f2ec2-178">Откройте файл метаданных загружаются hello, скопируйте содержимое hello и вставьте его в hello **XML метаданных поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-178">Open hello downloaded metadata file, copy hello content, and then paste it into hello **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="f2ec2-179">d.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-179">d.</span></span> <span data-ttu-id="f2ec2-180">Щелкните **Сохранить параметры SAML2**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="f2ec2-181">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f2ec2-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f2ec2-182">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f2ec2-183">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f2ec2-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f2ec2-184">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2ec2-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="f2ec2-185">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f2ec2-187">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f2ec2-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2ec2-188">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f2ec2-190">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f2ec2-192">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f2ec2-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f2ec2-194">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f2ec2-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f2ec2-196">а.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-196">a.</span></span> <span data-ttu-id="f2ec2-197">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f2ec2-198">b.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-198">b.</span></span> <span data-ttu-id="f2ec2-199">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-199">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="f2ec2-200">c.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-200">c.</span></span> <span data-ttu-id="f2ec2-201">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f2ec2-202">d.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-202">d.</span></span> <span data-ttu-id="f2ec2-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="f2ec2-204">Создание тестового пользователя ThirdLight</span><span class="sxs-lookup"><span data-stu-id="f2ec2-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="f2ec2-205">Пользователи toolog tooenable Azure AD в tooThirdLight, их необходимо подготовить в ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-205">tooenable Azure AD users toolog in tooThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="f2ec2-206">В случае ThirdLight hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-206">In hello case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="f2ec2-207">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f2ec2-207">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2ec2-208">Войдите в tooyour **ThirdLight** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-208">Log in tooyour **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="f2ec2-209">Go слишком**пользователей** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-209">Go too**Users** tab.</span></span>

3. <span data-ttu-id="f2ec2-210">Выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="f2ec2-211">Щелкните **Добавить пользователя** .</span><span class="sxs-lookup"><span data-stu-id="f2ec2-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="f2ec2-212">Введите **hello имя пользователя, имя или описание, электронной почте, выберите стиль или группу новых членов** действительной учетной записи AAD, вы хотите tooprovision.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-212">Enter **hello Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want tooprovision.</span></span>

6. <span data-ttu-id="f2ec2-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="f2ec2-214">Можно использовать любые другие Thirdlight пользователя средства создания учетных записей или интерфейсы API, предоставляемые Thirdlight tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f2ec2-215">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f2ec2-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f2ec2-216">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooThirdLight доступа.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThirdLight.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f2ec2-218">**tooassign tooThirdLight Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f2ec2-218">**tooassign Britta Simon tooThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2ec2-219">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f2ec2-221">В списке приложений hello выберите **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-221">In hello applications list, select **ThirdLight**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="f2ec2-223">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f2ec2-225">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-225">Click **Add** button.</span></span> <span data-ttu-id="f2ec2-226">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f2ec2-228">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f2ec2-229">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f2ec2-230">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f2ec2-231">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f2ec2-231">Testing single sign-on</span></span>

<span data-ttu-id="f2ec2-232">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f2ec2-233">При нажатии кнопки hello ThirdLight плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour ThirdLight приложения.</span><span class="sxs-lookup"><span data-stu-id="f2ec2-233">When you click hello ThirdLight tile in hello Access Panel, you should get automatically signed-on tooyour ThirdLight application.</span></span>
<span data-ttu-id="f2ec2-234">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f2ec2-234">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f2ec2-235">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f2ec2-235">Additional resources</span></span>

* [<span data-ttu-id="f2ec2-236">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2ec2-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f2ec2-237">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f2ec2-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

