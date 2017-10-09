---
title: "Учебник. Интеграция Azure Active Directory с GaggleAMP | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и GaggleAMP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9761019a79f935b6695a5ae1214c256c887df457
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="4d904-103">Руководство. Интеграция Azure Active Directory с GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="4d904-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="4d904-104">В этом учебнике вы узнаете, как toointegrate GaggleAMP с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d904-104">In this tutorial, you learn how toointegrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d904-105">Интеграция с Azure AD GaggleAMP предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4d904-105">Integrating GaggleAMP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4d904-106">Можно управлять в Azure AD, имеющего доступ tooGaggleAMP</span><span class="sxs-lookup"><span data-stu-id="4d904-106">You can control in Azure AD who has access tooGaggleAMP</span></span>
- <span data-ttu-id="4d904-107">Можно включить на пользователей tooautomatically get вошедшего tooGaggleAMP (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d904-107">You can enable your users tooautomatically get signed-on tooGaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d904-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="4d904-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4d904-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d904-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d904-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4d904-110">Prerequisites</span></span>

<span data-ttu-id="4d904-111">tooconfigure интеграция Azure AD с GaggleAMP требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4d904-111">tooconfigure Azure AD integration with GaggleAMP, you need hello following items:</span></span>

- <span data-ttu-id="4d904-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="4d904-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d904-113">подписка на GaggleAMP с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="4d904-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d904-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="4d904-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d904-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="4d904-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d904-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="4d904-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d904-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d904-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d904-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="4d904-118">Scenario description</span></span>
<span data-ttu-id="4d904-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="4d904-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d904-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="4d904-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d904-121">Добавление GaggleAMP из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4d904-121">Adding GaggleAMP from hello gallery</span></span>
2. <span data-ttu-id="4d904-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d904-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-hello-gallery"></a><span data-ttu-id="4d904-123">Добавление GaggleAMP из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4d904-123">Adding GaggleAMP from hello gallery</span></span>
<span data-ttu-id="4d904-124">tooconfigure hello интеграции GaggleAMP в Azure AD, вы должны tooadd GaggleAMP из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="4d904-124">tooconfigure hello integration of GaggleAMP into Azure AD, you need tooadd GaggleAMP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4d904-125">**tooadd GaggleAMP из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d904-125">**tooadd GaggleAMP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d904-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4d904-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4d904-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="4d904-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4d904-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4d904-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="4d904-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4d904-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="4d904-133">Введите в поле поиска hello **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="4d904-133">In hello search box, type **GaggleAMP**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="4d904-135">В панели результатов hello выберите **GaggleAMP**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4d904-135">In hello results panel, select **GaggleAMP**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4d904-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d904-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4d904-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение GaggleAMP для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d904-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4d904-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в GaggleAMP является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d904-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GaggleAMP is tooa user in Azure AD.</span></span> <span data-ttu-id="4d904-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в GaggleAMP должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="4d904-140">In other words, a link relationship between an Azure AD user and hello related user in GaggleAMP needs toobe established.</span></span>

<span data-ttu-id="4d904-141">В GaggleAMP, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="4d904-141">In GaggleAMP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4d904-142">tooconfigure и теста Azure AD единого входа с GaggleAMP, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4d904-142">tooconfigure and test Azure AD single sign-on with GaggleAMP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4d904-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="4d904-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4d904-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="4d904-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d904-145">**[Создание тестового пользователя GaggleAMP](#creating-a-gaggleamp-test-user)**  -toohave аналог Саймон Britta в GaggleAMP, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="4d904-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - toohave a counterpart of Britta Simon in GaggleAMP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d904-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="4d904-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d904-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4d904-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4d904-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d904-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4d904-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="4d904-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="4d904-150">**tooconfigure Azure AD единого входа с GaggleAMP, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d904-150">**tooconfigure Azure AD single sign-on with GaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d904-151">В hello в hello портала Azure **GaggleAMP** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="4d904-151">In hello Azure portal, on hello **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="4d904-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="4d904-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="4d904-155">На hello **URL-адреса и домена GaggleAMP** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4d904-155">On hello **GaggleAMP Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="4d904-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="4d904-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4d904-158">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="4d904-158">hello value is not real.</span></span> <span data-ttu-id="4d904-159">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="4d904-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4d904-160">Обратитесь к [группа поддержки клиента GaggleAMP](mailto:sales@gaggleamp.com) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="4d904-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="4d904-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="4d904-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="4d904-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="4d904-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4d904-165">На hello **конфигурации GaggleAMP** щелкните **Настройка GaggleAMP** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="4d904-165">On hello **GaggleAMP Configuration** section, click **Configure GaggleAMP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4d904-166">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="4d904-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="4d904-168">В другом экземпляре браузера перейдите toohello страницы единого входа SAML, созданные для вас hello того поддержки (например: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="4d904-168">In another browser instance, navigate toohello SAML SSO page created for you by hello Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="4d904-169">На ваш **единого входа SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4d904-169">On your **SAML SSO** page, perform hello following steps:</span></span>  
   
    ![Единый вход в GaggleAMP](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="4d904-171">а.</span><span class="sxs-lookup"><span data-stu-id="4d904-171">a.</span></span> <span data-ttu-id="4d904-172">В hello **издатель поставщика удостоверений** текстовое значение hello вставить **URL-адрес издателя** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4d904-172">In hello **Identity Provider Issuer** textbox, paste hello value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="4d904-173">b.</span><span class="sxs-lookup"><span data-stu-id="4d904-173">b.</span></span> <span data-ttu-id="4d904-174">В hello **удостоверений единого входа URL-адрес поставщика** текстовое значение hello вставить **единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4d904-174">In hello **Identity Provider Single Sign-On URL** textbox, paste hello  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="4d904-175">c.</span><span class="sxs-lookup"><span data-stu-id="4d904-175">c.</span></span> <span data-ttu-id="4d904-176">Нажмите кнопку **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="4d904-176">Click **Save**</span></span>      

    <span data-ttu-id="4d904-177">d.</span><span class="sxs-lookup"><span data-stu-id="4d904-177">d.</span></span> <span data-ttu-id="4d904-178">Отправить hello **сертификата (Base64)** сертификатов tooyour [GaggleAMP поддержки](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="4d904-178">Send hello **Certificate (Base64)** certificate tooyour [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="4d904-179">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="4d904-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4d904-180">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="4d904-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4d904-181">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d904-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4d904-182">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d904-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="4d904-183">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4d904-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="4d904-185">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d904-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d904-186">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4d904-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d904-188">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4d904-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d904-190">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="4d904-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d904-192">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4d904-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d904-194">а.</span><span class="sxs-lookup"><span data-stu-id="4d904-194">a.</span></span> <span data-ttu-id="4d904-195">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d904-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d904-196">b.</span><span class="sxs-lookup"><span data-stu-id="4d904-196">b.</span></span> <span data-ttu-id="4d904-197">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4d904-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d904-198">c.</span><span class="sxs-lookup"><span data-stu-id="4d904-198">c.</span></span> <span data-ttu-id="4d904-199">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="4d904-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4d904-200">d.</span><span class="sxs-lookup"><span data-stu-id="4d904-200">d.</span></span> <span data-ttu-id="4d904-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4d904-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="4d904-202">Создание тестового пользователя GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="4d904-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="4d904-203">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="4d904-203">hello objective of this section is toocreate a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="4d904-204">Приложение GaggleAMP поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4d904-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4d904-205">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="4d904-205">There is no action item for you in this section.</span></span> <span data-ttu-id="4d904-206">Новый пользователь создается во время попытки tooaccess GaggleAMP, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="4d904-206">A new user is created during an attempt tooaccess GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4d904-207">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="4d904-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4d904-208">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooGaggleAMP доступа.</span><span class="sxs-lookup"><span data-stu-id="4d904-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGaggleAMP.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="4d904-210">**tooassign tooGaggleAMP Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d904-210">**tooassign Britta Simon tooGaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d904-211">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4d904-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="4d904-213">В списке приложений hello выберите **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="4d904-213">In hello applications list, select **GaggleAMP**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="4d904-215">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="4d904-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="4d904-217">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4d904-217">Click **Add** button.</span></span> <span data-ttu-id="4d904-218">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4d904-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="4d904-220">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="4d904-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4d904-221">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4d904-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d904-222">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="4d904-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4d904-223">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="4d904-223">Testing single sign-on</span></span>

<span data-ttu-id="4d904-224">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="4d904-224">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4d904-225">При нажатии кнопки hello GaggleAMP плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour GaggleAMP приложения.</span><span class="sxs-lookup"><span data-stu-id="4d904-225">When you click hello GaggleAMP tile in hello Access Panel, you should get automatically signed-on tooyour GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4d904-226">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4d904-226">Additional resources</span></span>

* [<span data-ttu-id="4d904-227">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d904-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d904-228">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d904-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

