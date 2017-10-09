---
title: "Руководство по интеграции Azure Active Directory с Ariba | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Ariba."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: a1b17129c1298b59c155a0890e41e41ff9544a24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="804b8-103">Руководство. Интеграция Azure Active Directory с Ariba</span><span class="sxs-lookup"><span data-stu-id="804b8-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="804b8-104">В этом учебнике вы узнаете, как toointegrate Ariba с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="804b8-104">In this tutorial, you learn how toointegrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="804b8-105">Интеграция с Azure AD Ariba предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="804b8-105">Integrating Ariba with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="804b8-106">Можно управлять в Azure AD, имеющего доступ tooAriba</span><span class="sxs-lookup"><span data-stu-id="804b8-106">You can control in Azure AD who has access tooAriba</span></span>
- <span data-ttu-id="804b8-107">Можно включить на пользователей tooautomatically get вошедшего tooAriba (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="804b8-107">You can enable your users tooautomatically get signed-on tooAriba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="804b8-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="804b8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="804b8-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="804b8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="804b8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="804b8-110">Prerequisites</span></span>

<span data-ttu-id="804b8-111">tooconfigure интеграция Azure AD с Ariba требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="804b8-111">tooconfigure Azure AD integration with Ariba, you need hello following items:</span></span>

- <span data-ttu-id="804b8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="804b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="804b8-113">подписка Ariba с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="804b8-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="804b8-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="804b8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="804b8-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="804b8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="804b8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="804b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="804b8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="804b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="804b8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="804b8-118">Scenario description</span></span>
<span data-ttu-id="804b8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="804b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="804b8-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="804b8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="804b8-121">Добавление Ariba из галереи hello</span><span class="sxs-lookup"><span data-stu-id="804b8-121">Adding Ariba from hello gallery</span></span>
2. <span data-ttu-id="804b8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="804b8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-hello-gallery"></a><span data-ttu-id="804b8-123">Добавление Ariba из галереи hello</span><span class="sxs-lookup"><span data-stu-id="804b8-123">Adding Ariba from hello gallery</span></span>
<span data-ttu-id="804b8-124">tooconfigure hello интеграции Ariba в Azure AD, вы должны tooadd Ariba из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="804b8-124">tooconfigure hello integration of Ariba into Azure AD, you need tooadd Ariba from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="804b8-125">**tooadd Ariba из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="804b8-125">**tooadd Ariba from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="804b8-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="804b8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="804b8-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="804b8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="804b8-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="804b8-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="804b8-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="804b8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="804b8-133">Введите в поле поиска hello **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="804b8-133">In hello search box, type **Ariba**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="804b8-135">В панели результатов hello выберите **Ariba**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="804b8-135">In hello results panel, select **Ariba**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="804b8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="804b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="804b8-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Ariba с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="804b8-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="804b8-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Ariba является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="804b8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ariba is tooa user in Azure AD.</span></span> <span data-ttu-id="804b8-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Ariba должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="804b8-140">In other words, a link relationship between an Azure AD user and hello related user in Ariba needs toobe established.</span></span>

<span data-ttu-id="804b8-141">В Ariba, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="804b8-141">In Ariba, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="804b8-142">tooconfigure и теста Azure AD единого входа с Ariba, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="804b8-142">tooconfigure and test Azure AD single sign-on with Ariba, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="804b8-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="804b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="804b8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="804b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="804b8-145">**[Создание тестового пользователя, прошедшего Ariba](#creating-an-ariba-test-user)**  -toohave аналог Саймон Britta в Ariba, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="804b8-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - toohave a counterpart of Britta Simon in Ariba that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="804b8-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="804b8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="804b8-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="804b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="804b8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="804b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="804b8-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Ariba.</span><span class="sxs-lookup"><span data-stu-id="804b8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="804b8-150">**tooconfigure Azure AD единого входа с Ariba, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="804b8-150">**tooconfigure Azure AD single sign-on with Ariba, perform hello following steps:**</span></span>

1. <span data-ttu-id="804b8-151">В hello в hello портала Azure **Ariba** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="804b8-151">In hello Azure portal, on hello **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="804b8-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="804b8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="804b8-155">На hello **URL-адреса и домена Ariba** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="804b8-155">On hello **Ariba Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="804b8-157">а.</span><span class="sxs-lookup"><span data-stu-id="804b8-157">a.</span></span> <span data-ttu-id="804b8-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello: `https://<subdomain>.sourcing.ariba.com` или`https://<subdomain>.supplier.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="804b8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="804b8-159">b.</span><span class="sxs-lookup"><span data-stu-id="804b8-159">b.</span></span> <span data-ttu-id="804b8-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="804b8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="804b8-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="804b8-161">These values are not real.</span></span> <span data-ttu-id="804b8-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="804b8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="804b8-163">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="804b8-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="804b8-164">Обратитесь в службу поддержки клиентов Ariba на **1-866-218-2155** tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="804b8-164">Contact Ariba Client support team at **1-866-218-2155** tooget these values.</span></span> 
 

4. <span data-ttu-id="804b8-165">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="804b8-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate  file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="804b8-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="804b8-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="804b8-169">tooget SSO настроен для вашего приложения, вызывать Ariba поддержки для **1-866-218-2155** и они будут поможет дальнейшей на способа загрузки их hello tooprovide **сертификата (Base64)** файла.</span><span class="sxs-lookup"><span data-stu-id="804b8-169">tooget SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how tooprovide them hello downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="804b8-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="804b8-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="804b8-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="804b8-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="804b8-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="804b8-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="804b8-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="804b8-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="804b8-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="804b8-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="804b8-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="804b8-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="804b8-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="804b8-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="804b8-179">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="804b8-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="804b8-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="804b8-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="804b8-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="804b8-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="804b8-185">а.</span><span class="sxs-lookup"><span data-stu-id="804b8-185">a.</span></span> <span data-ttu-id="804b8-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="804b8-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="804b8-187">b.</span><span class="sxs-lookup"><span data-stu-id="804b8-187">b.</span></span> <span data-ttu-id="804b8-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="804b8-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="804b8-189">c.</span><span class="sxs-lookup"><span data-stu-id="804b8-189">c.</span></span> <span data-ttu-id="804b8-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="804b8-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="804b8-191">d.</span><span class="sxs-lookup"><span data-stu-id="804b8-191">d.</span></span> <span data-ttu-id="804b8-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="804b8-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="804b8-193">Создание тестового пользователя Ariba</span><span class="sxs-lookup"><span data-stu-id="804b8-193">Creating an Ariba test user</span></span>

<span data-ttu-id="804b8-194">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в Ariba.</span><span class="sxs-lookup"><span data-stu-id="804b8-194">hello objective of this section is toocreate a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="804b8-195">Работать с группой поддержки Ariba на **1-866-218-2155** tooadd hello пользователей в системе Ariba hello.</span><span class="sxs-lookup"><span data-stu-id="804b8-195">Work with Ariba support team at **1-866-218-2155** tooadd hello users in hello Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="804b8-196">При необходимости toocreate пользователя вручную, необходимо toocontact группа поддержки Ariba hello в **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="804b8-196">If you need toocreate a user manually, you need toocontact hello Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="804b8-197">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="804b8-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="804b8-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAriba доступа.</span><span class="sxs-lookup"><span data-stu-id="804b8-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAriba.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="804b8-200">**tooassign tooAriba Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="804b8-200">**tooassign Britta Simon tooAriba, perform hello following steps:**</span></span>

1. <span data-ttu-id="804b8-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="804b8-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="804b8-203">В списке приложений hello выберите **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="804b8-203">In hello applications list, select **Ariba**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="804b8-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="804b8-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="804b8-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="804b8-207">Click **Add** button.</span></span> <span data-ttu-id="804b8-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="804b8-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="804b8-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="804b8-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="804b8-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="804b8-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="804b8-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="804b8-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="804b8-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="804b8-213">Testing single sign-on</span></span>
<span data-ttu-id="804b8-214">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="804b8-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="804b8-215">При выборе плитки Ariba hello в hello панели доступа, следует получать автоматически вошедшего tooyour Ariba приложения.</span><span class="sxs-lookup"><span data-stu-id="804b8-215">When you click hello Ariba tile in hello Access Panel, you should get automatically signed-on tooyour Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="804b8-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="804b8-216">Additional resources</span></span>

* [<span data-ttu-id="804b8-217">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="804b8-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="804b8-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="804b8-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

