---
title: "Руководство. Интеграция Azure Active Directory с приложениями Splunk Enterprise и Splunk Cloud | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и корпоративный Splunk и Splunk облака."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 848e0485131321479f2375501b330c798627e7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="7390c-103">Руководство. Интеграция Azure Active Directory с приложениями Splunk Enterprise и Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="7390c-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="7390c-104">В этом учебнике вы узнаете, как toointegrate Splunk предприятия и Splunk в облаке в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7390c-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7390c-105">Интеграция с Azure AD Splunk предприятия и в облаке Splunk предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7390c-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7390c-106">Можно управлять в Azure AD, который имеет доступ tooSplunk предприятия и Splunk в облаке</span><span class="sxs-lookup"><span data-stu-id="7390c-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="7390c-107">Можно разрешить пользователям tooautomatically get вошедшего tooSplunk Enterprise и Splunk облака (Single Sign-On) с их учетными записями Azure AD</span><span class="sxs-lookup"><span data-stu-id="7390c-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7390c-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7390c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7390c-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7390c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7390c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7390c-110">Prerequisites</span></span>

<span data-ttu-id="7390c-111">tooconfigure интеграция Azure AD с Splunk предприятия и Splunk в облаке необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7390c-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="7390c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7390c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7390c-113">подписка Splunk Enterprise и Splunk Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7390c-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7390c-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7390c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7390c-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7390c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7390c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7390c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7390c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7390c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7390c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7390c-118">Scenario description</span></span>
<span data-ttu-id="7390c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7390c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7390c-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7390c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7390c-121">Добавление Splunk предприятия и в облаке Splunk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7390c-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="7390c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7390c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="7390c-123">Добавление Splunk предприятия и в облаке Splunk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7390c-123">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="7390c-124">tooconfigure hello интеграции Splunk предприятия и Splunk в облаке в Azure AD, необходимо tooadd Splunk предприятия и Splunk облако из списка tooyour hello коллекции из управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7390c-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7390c-125">**tooadd Splunk предприятия и в облаке Splunk из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7390c-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7390c-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7390c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7390c-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="7390c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7390c-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7390c-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7390c-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7390c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7390c-133">Введите в поле поиска hello **Splunk предприятия и в облаке Splunk**.</span><span class="sxs-lookup"><span data-stu-id="7390c-133">In hello search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

5. <span data-ttu-id="7390c-135">В панели результатов hello выберите **Splunk предприятия и в облаке Splunk**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7390c-135">In hello results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7390c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7390c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7390c-138">В этом разделе описывается настройка и проверка единого входа Azure AD в Splunk Enterprise и Splunk Cloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7390c-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7390c-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Splunk предприятия и в облаке Splunk является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7390c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="7390c-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Splunk предприятия и в облаке Splunk должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7390c-140">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="7390c-141">В Splunk предприятия и Splunk в облаке, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="7390c-141">In Splunk Enterprise and Splunk Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7390c-142">tooconfigure и теста Azure AD единого входа с Splunk предприятия и Splunk в облаке, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7390c-142">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7390c-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7390c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7390c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7390c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7390c-145">**[Создание тестового пользователя Splunk предприятия и в облаке Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave аналог Саймон Britta Splunk предприятия и Splunk облако, которое представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="7390c-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7390c-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7390c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7390c-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7390c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7390c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7390c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7390c-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении предприятия Splunk и Splunk в облаке.</span><span class="sxs-lookup"><span data-stu-id="7390c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="7390c-150">**tooconfigure Azure AD единого входа с Splunk предприятия и Splunk в облаке, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7390c-150">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="7390c-151">В hello в hello портала Azure **Splunk предприятия и в облаке Splunk** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7390c-151">In hello Azure portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7390c-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="7390c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

3. <span data-ttu-id="7390c-155">На hello **Splunk предприятия и Splunk облака домена и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="7390c-155">On hello **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="7390c-157">а.</span><span class="sxs-lookup"><span data-stu-id="7390c-157">a.</span></span> <span data-ttu-id="7390c-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="7390c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="7390c-159">b.</span><span class="sxs-lookup"><span data-stu-id="7390c-159">b.</span></span> <span data-ttu-id="7390c-160">В hello **идентификатор** текстовом поле введите URL-адрес hello Splunk сервера.</span><span class="sxs-lookup"><span data-stu-id="7390c-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>

    <span data-ttu-id="7390c-161">c.</span><span class="sxs-lookup"><span data-stu-id="7390c-161">c.</span></span> <span data-ttu-id="7390c-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="7390c-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7390c-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="7390c-163">These values are not real.</span></span> <span data-ttu-id="7390c-164">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="7390c-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7390c-165">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="7390c-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="7390c-166">Обратитесь к [Splunk предприятия и клиентских облачных Splunk поддержки](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="7390c-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget these values.</span></span> 

4. <span data-ttu-id="7390c-167">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="7390c-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

5. <span data-ttu-id="7390c-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7390c-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7390c-171">tooconfigure единого входа на **Splunk предприятия и в облаке Splunk** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Splunk предприятия и в облаке Splunk поддержки](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="7390c-171">tooconfigure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need toosend hello downloaded **Metadata XML** too[Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="7390c-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="7390c-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7390c-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="7390c-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7390c-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7390c-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7390c-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7390c-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="7390c-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7390c-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7390c-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7390c-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7390c-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7390c-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7390c-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7390c-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7390c-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="7390c-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7390c-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7390c-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7390c-187">а.</span><span class="sxs-lookup"><span data-stu-id="7390c-187">a.</span></span> <span data-ttu-id="7390c-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7390c-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7390c-189">b.</span><span class="sxs-lookup"><span data-stu-id="7390c-189">b.</span></span> <span data-ttu-id="7390c-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7390c-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7390c-191">c.</span><span class="sxs-lookup"><span data-stu-id="7390c-191">c.</span></span> <span data-ttu-id="7390c-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="7390c-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7390c-193">d.</span><span class="sxs-lookup"><span data-stu-id="7390c-193">d.</span></span> <span data-ttu-id="7390c-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7390c-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="7390c-195">Создание тестового пользователя Splunk Enterprise и Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="7390c-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="7390c-196">В этом разделе описано, как создать пользователя Britta Simon в Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="7390c-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="7390c-197">Работать с [Splunk предприятия и в облаке Splunk поддержки](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooadd пользователей hello hello Splunk предприятия и Splunk облачной платформы.</span><span class="sxs-lookup"><span data-stu-id="7390c-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7390c-198">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7390c-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7390c-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSplunk предприятия и Splunk в облаке.</span><span class="sxs-lookup"><span data-stu-id="7390c-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7390c-201">**tooassign Britta Simon tooSplunk предприятия и облака Splunk выполняют hello следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="7390c-201">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="7390c-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7390c-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7390c-204">В списке приложений hello выберите **Splunk предприятия и в облаке Splunk**.</span><span class="sxs-lookup"><span data-stu-id="7390c-204">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

3. <span data-ttu-id="7390c-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="7390c-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7390c-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7390c-208">Click **Add** button.</span></span> <span data-ttu-id="7390c-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7390c-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7390c-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7390c-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7390c-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7390c-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7390c-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7390c-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7390c-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7390c-214">Testing single sign-on</span></span>

<span data-ttu-id="7390c-215">В этом разделе тестирования вашей SSOonfiguration Azure AD, с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="7390c-215">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="7390c-216">При нажатии кнопки hello Splunk предприятия и облака Splunk плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Splunk предприятия и Splunk облачных приложений.</span><span class="sxs-lookup"><span data-stu-id="7390c-216">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7390c-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7390c-217">Additional resources</span></span>

* [<span data-ttu-id="7390c-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7390c-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7390c-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7390c-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png

