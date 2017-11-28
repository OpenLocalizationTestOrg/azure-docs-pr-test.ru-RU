---
title: "Руководство по интеграции Azure Active Directory с Promapp | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Promapp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 02de7679b0c86d7aa8cacb41762f900dbf2ff231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="b93e5-103">Руководство по интеграции Azure Active Directory с Promapp</span><span class="sxs-lookup"><span data-stu-id="b93e5-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="b93e5-104">В этом учебнике вы узнаете, как toointegrate Promapp с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b93e5-104">In this tutorial, you learn how toointegrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b93e5-105">Интеграция с Azure AD Promapp предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b93e5-105">Integrating Promapp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b93e5-106">Можно управлять в Azure AD, имеющего доступ tooPromapp</span><span class="sxs-lookup"><span data-stu-id="b93e5-106">You can control in Azure AD who has access tooPromapp</span></span>
- <span data-ttu-id="b93e5-107">Можно включить на пользователей tooautomatically get вошедшего tooPromapp (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b93e5-107">You can enable your users tooautomatically get signed-on tooPromapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b93e5-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b93e5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b93e5-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b93e5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b93e5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b93e5-110">Prerequisites</span></span>

<span data-ttu-id="b93e5-111">tooconfigure интеграция Azure AD с Promapp требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b93e5-111">tooconfigure Azure AD integration with Promapp, you need hello following items:</span></span>

- <span data-ttu-id="b93e5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b93e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b93e5-113">подписка Promapp с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b93e5-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b93e5-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b93e5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b93e5-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b93e5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b93e5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b93e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b93e5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b93e5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b93e5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b93e5-118">Scenario description</span></span>
<span data-ttu-id="b93e5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b93e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b93e5-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b93e5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b93e5-121">Добавление Promapp из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b93e5-121">Adding Promapp from hello gallery</span></span>
2. <span data-ttu-id="b93e5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b93e5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-hello-gallery"></a><span data-ttu-id="b93e5-123">Добавление Promapp из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b93e5-123">Adding Promapp from hello gallery</span></span>
<span data-ttu-id="b93e5-124">tooconfigure hello интеграции Promapp в Azure AD, вы должны tooadd Promapp из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b93e5-124">tooconfigure hello integration of Promapp into Azure AD, you need tooadd Promapp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b93e5-125">**tooadd Promapp из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b93e5-125">**tooadd Promapp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b93e5-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b93e5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b93e5-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b93e5-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b93e5-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b93e5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b93e5-133">Введите в поле поиска hello **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-133">In hello search box, type **Promapp**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="b93e5-135">В панели результатов hello выберите **Promapp**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b93e5-135">In hello results panel, select **Promapp**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b93e5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b93e5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b93e5-138">В этом разделе описана настройка и проверка единого входа Azure AD в Promapp с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b93e5-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b93e5-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Promapp является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b93e5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Promapp is tooa user in Azure AD.</span></span> <span data-ttu-id="b93e5-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Promapp должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b93e5-140">In other words, a link relationship between an Azure AD user and hello related user in Promapp needs toobe established.</span></span>

<span data-ttu-id="b93e5-141">В Promapp, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="b93e5-141">In Promapp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b93e5-142">tooconfigure и теста Azure AD единого входа с Promapp, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b93e5-142">tooconfigure and test Azure AD single sign-on with Promapp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b93e5-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b93e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b93e5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b93e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b93e5-145">**[Создание тестового пользователя Promapp](#creating-a-promapp-test-user)**  -toohave аналог Саймон Britta в Promapp, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b93e5-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - toohave a counterpart of Britta Simon in Promapp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b93e5-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b93e5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b93e5-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b93e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b93e5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b93e5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b93e5-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Promapp.</span><span class="sxs-lookup"><span data-stu-id="b93e5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="b93e5-150">**tooconfigure Azure AD единого входа с Promapp, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b93e5-150">**tooconfigure Azure AD single sign-on with Promapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="b93e5-151">В hello в hello портала Azure **Promapp** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-151">In hello Azure portal, on hello **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b93e5-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b93e5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="b93e5-155">На hello **URL-адреса и домена Promapp** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b93e5-155">On hello **Promapp Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="b93e5-157">а.</span><span class="sxs-lookup"><span data-stu-id="b93e5-157">a.</span></span> <span data-ttu-id="b93e5-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="b93e5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="b93e5-159">b.</span><span class="sxs-lookup"><span data-stu-id="b93e5-159">b.</span></span> <span data-ttu-id="b93e5-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="b93e5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b93e5-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b93e5-161">These values are not real.</span></span> <span data-ttu-id="b93e5-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b93e5-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b93e5-163">Обратитесь к [группа поддержки клиента Promapp](https://www.promapp.com/about-us/contact-us/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="b93e5-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="b93e5-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b93e5-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="b93e5-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b93e5-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b93e5-168">На hello **конфигурации Promapp** щелкните **Настройка Promapp** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="b93e5-168">On hello **Promapp Configuration** section, click **Configure Promapp** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b93e5-169">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="b93e5-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="b93e5-171">Корпоративный сайт Promapp tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="b93e5-171">Sign-on tooyour Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="b93e5-172">В меню в верхней части hello hello выберите **администратора**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-172">In hello menu on hello top, click **Admin**.</span></span> 
   
    ![Единый вход в Azure AD][12]

9. <span data-ttu-id="b93e5-174">Нажмите **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-174">Click **Configure**.</span></span> 
   
    ![Единый вход в Azure AD][13]

10. <span data-ttu-id="b93e5-176">На hello **безопасности** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b93e5-176">On hello **Security** dialog, perform hello following steps:</span></span>
   
    ![Единый вход в Azure AD][14]
    
    <span data-ttu-id="b93e5-178">а.</span><span class="sxs-lookup"><span data-stu-id="b93e5-178">a.</span></span> <span data-ttu-id="b93e5-179">Вставить **SAML единого входа URL-адрес службы**, которой копируются hello портал Azure в hello **URL-адрес входа SSO** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b93e5-179">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="b93e5-180">b.</span><span class="sxs-lookup"><span data-stu-id="b93e5-180">b.</span></span> <span data-ttu-id="b93e5-181">В поле **SSO - Single Sign-on Mode** (SSO — режим единого входа) выберите **Optional** (Необязательно), а затем нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="b93e5-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="b93e5-182">c.</span><span class="sxs-lookup"><span data-stu-id="b93e5-182">c.</span></span> <span data-ttu-id="b93e5-183">Откройте hello загрузить сертификат в блокноте сертификат hello копирования содержимого без первую строку hello (---BEGIN CERTIFICATE---) и последнюю строку hello (---конечный СЕРТИФИКАТ---), вставьте его в hello **сертификат SSO x.509** текстовое поле, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-183">Open hello downloaded certificate in notepad, copy hello certificate content without hello first line (-----BEGIN CERTIFICATE-----) and hello last line (-----END CERTIFICATE-----), paste it into hello **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="b93e5-184">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b93e5-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b93e5-185">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b93e5-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b93e5-186">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b93e5-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b93e5-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b93e5-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="b93e5-188">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b93e5-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b93e5-190">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b93e5-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b93e5-191">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b93e5-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b93e5-193">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b93e5-195">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b93e5-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b93e5-197">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b93e5-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b93e5-199">а.</span><span class="sxs-lookup"><span data-stu-id="b93e5-199">a.</span></span> <span data-ttu-id="b93e5-200">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b93e5-201">b.</span><span class="sxs-lookup"><span data-stu-id="b93e5-201">b.</span></span> <span data-ttu-id="b93e5-202">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b93e5-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b93e5-203">c.</span><span class="sxs-lookup"><span data-stu-id="b93e5-203">c.</span></span> <span data-ttu-id="b93e5-204">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b93e5-205">d.</span><span class="sxs-lookup"><span data-stu-id="b93e5-205">d.</span></span> <span data-ttu-id="b93e5-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="b93e5-207">Создание тестового пользователя Promapp</span><span class="sxs-lookup"><span data-stu-id="b93e5-207">Creating a Promapp test user</span></span>

<span data-ttu-id="b93e5-208">Hello Promapp приложений поддерживает только времени подготовки.</span><span class="sxs-lookup"><span data-stu-id="b93e5-208">hello Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="b93e5-209">Это означает учетной записи пользователя автоматически создается при необходимости во время попытки tooaccess hello приложения с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b93e5-209">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b93e5-210">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b93e5-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b93e5-211">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPromapp доступа.</span><span class="sxs-lookup"><span data-stu-id="b93e5-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPromapp.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b93e5-213">**tooassign tooPromapp Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b93e5-213">**tooassign Britta Simon tooPromapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="b93e5-214">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b93e5-216">В списке приложений hello выберите **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-216">In hello applications list, select **Promapp**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="b93e5-218">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b93e5-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-220">Click **Add** button.</span></span> <span data-ttu-id="b93e5-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b93e5-223">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b93e5-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b93e5-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b93e5-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b93e5-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b93e5-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b93e5-226">Testing single sign-on</span></span>

<span data-ttu-id="b93e5-227">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="b93e5-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="b93e5-228">При нажатии кнопки hello Promapp плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Promapp приложения.</span><span class="sxs-lookup"><span data-stu-id="b93e5-228">When you click hello Promapp tile in hello Access Panel, you should get automatically signed-on tooyour Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b93e5-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b93e5-229">Additional resources</span></span>

* [<span data-ttu-id="b93e5-230">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b93e5-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b93e5-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b93e5-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

