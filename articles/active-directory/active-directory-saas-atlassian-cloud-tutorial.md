---
title: "Руководство по интеграции Azure Active Directory с Atlassian Cloud | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и облаком Atlassian."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="7d3fd-103">Руководство по интеграции Azure Active Directory с Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="7d3fd-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="7d3fd-104">В этом учебнике вы узнаете, как toointegrate Atlassian облака в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7d3fd-104">In this tutorial, you learn how toointegrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d3fd-105">Интеграция с Azure AD облака Atlassian предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7d3fd-105">Integrating Atlassian Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7d3fd-106">Можно управлять в Azure AD, имеющего доступ tooAtlassian облака</span><span class="sxs-lookup"><span data-stu-id="7d3fd-106">You can control in Azure AD who has access tooAtlassian Cloud</span></span>
- <span data-ttu-id="7d3fd-107">Можно включить на пользователей tooautomatically get вошедшего tooAtlassian облака (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d3fd-107">You can enable your users tooautomatically get signed-on tooAtlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d3fd-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7d3fd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7d3fd-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7d3fd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d3fd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7d3fd-110">Prerequisites</span></span>

<span data-ttu-id="7d3fd-111">tooconfigure интеграция Azure AD с облаком Atlassian требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7d3fd-111">tooconfigure Azure AD integration with Atlassian Cloud, you need hello following items:</span></span>

- <span data-ttu-id="7d3fd-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7d3fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d3fd-113">подписка Atlassian Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d3fd-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d3fd-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7d3fd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d3fd-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7d3fd-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d3fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d3fd-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7d3fd-118">Scenario description</span></span>
<span data-ttu-id="7d3fd-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d3fd-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7d3fd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d3fd-121">Добавление Atlassian облака из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7d3fd-121">Adding Atlassian Cloud from hello gallery</span></span>
2. <span data-ttu-id="7d3fd-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d3fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-hello-gallery"></a><span data-ttu-id="7d3fd-123">Добавление Atlassian облака из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7d3fd-123">Adding Atlassian Cloud from hello gallery</span></span>
<span data-ttu-id="7d3fd-124">tooconfigure hello интеграция Atlassian облака в Azure AD, вы должны tooadd Atlassian облако из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-124">tooconfigure hello integration of Atlassian Cloud into Azure AD, you need tooadd Atlassian Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7d3fd-125">**tooadd Atlassian облака из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="7d3fd-125">**tooadd Atlassian Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d3fd-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7d3fd-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7d3fd-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7d3fd-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7d3fd-133">Введите в поле поиска hello **Atlassian облака**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-133">In hello search box, type **Atlassian Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="7d3fd-135">В панели результатов hello, выберите **облака Atlassian**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-135">In hello results panel, select **Atlassian Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7d3fd-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d3fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7d3fd-138">В этом разделе описана настройка и проверка единого входа Azure AD в Atlassian Cloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7d3fd-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в облаке Atlassian является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atlassian Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="7d3fd-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в облаке Atlassian должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-140">In other words, a link relationship between an Azure AD user and hello related user in Atlassian Cloud needs toobe established.</span></span>

<span data-ttu-id="7d3fd-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в облаке Atlassian.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="7d3fd-142">tooconfigure и тестирования Azure AD единого входа с облаком Atlassian, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7d3fd-142">tooconfigure and test Azure AD single sign-on with Atlassian Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7d3fd-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7d3fd-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d3fd-145">**[Создание тестового пользователя, прошедшего облака Atlassian](#creating-an-atlassian-cloud-test-user)**  -toohave аналог Саймон Britta в облаке Atlassian, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - toohave a counterpart of Britta Simon in Atlassian Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7d3fd-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d3fd-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7d3fd-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d3fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7d3fd-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Atlassian облачного приложения.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="7d3fd-150">**tooconfigure Azure AD единого входа с облаком Atlassian выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7d3fd-150">**tooconfigure Azure AD single sign-on with Atlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d3fd-151">В hello в hello портала Azure **облака Atlassian** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-151">In hello Azure portal, on hello **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7d3fd-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="7d3fd-155">На hello **Atlassian облака домена и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="7d3fd-155">On hello **Atlassian Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="7d3fd-157">а.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-157">a.</span></span> <span data-ttu-id="7d3fd-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="7d3fd-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="7d3fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-159">b.</span></span> <span data-ttu-id="7d3fd-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес как:`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="7d3fd-160">In hello **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="7d3fd-161">Проверьте **Показывать дополнительные параметры URL-адреса** и выполните следующий шаг при желании tooconfigure приложения hello в hello **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="7d3fd-161">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="7d3fd-163">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="7d3fd-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7d3fd-164">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-164">These values are not real.</span></span> <span data-ttu-id="7d3fd-165">Обновить значения hello фактический идентификатор и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-165">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="7d3fd-166">Hello точные значения можно получить из конфигурации SAML облака Atlassian экрана.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-166">You can get hello exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="7d3fd-167">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="7d3fd-169">На hello **конфигурации облака Atlassian** щелкните **Настройка облака Atlassian** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-169">On hello **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7d3fd-170">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="7d3fd-170">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="7d3fd-172">tooget SSO настроен для вашего приложения, toohello входа Atlassian портал, используя права администратора hello.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-172">tooget SSO configured for your application, login toohello Atlassian Portal using hello administrator rights.</span></span>

8. <span data-ttu-id="7d3fd-173">В разделе проверки подлинности hello hello навигации слева щелкните **домены**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-173">In hello Authentication section of hello left navigation click **Domains**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="7d3fd-175">а.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-175">a.</span></span> <span data-ttu-id="7d3fd-176">В текстовом поле «hello» введите имя домена и нажмите кнопку **добавить домен**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-176">In hello textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="7d3fd-178">b.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-178">b.</span></span> <span data-ttu-id="7d3fd-179">tooverify hello домена, нажмите кнопку **проверьте**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-179">tooverify hello domain, click **Verify**.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="7d3fd-181">c.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-181">c.</span></span> <span data-ttu-id="7d3fd-182">Загрузить файл html проверки домена hello, отправьте его в корневую папку toohello вашего домена веб-сайта и нажмите кнопку **Проверка домена**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-182">Download hello domain verification html file, upload it toohello root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="7d3fd-184">d.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-184">d.</span></span> <span data-ttu-id="7d3fd-185">После проверки домена hello hello значение hello **состояние** поле является **проверено**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-185">Once hello domain is verified, hello value of hello **Status** field is **Verified**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="7d3fd-187">В левой навигационной панели hello, щелкните **SAML**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-187">In hello left navigation bar, click **SAML**.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="7d3fd-189">Создание конфигурации SAML и добавление hello конфигурация поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-189">Create a SAML Configuration and add hello Identity provider configuration.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="7d3fd-191">а.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-191">a.</span></span> <span data-ttu-id="7d3fd-192">В hello **поставщика удостоверений идентификатор сущности** текстовое поле, вставить значение hello **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-192">In hello **Identity provider Entity ID** text box, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7d3fd-193">b.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-193">b.</span></span> <span data-ttu-id="7d3fd-194">В hello **поставщика удостоверений URL-адрес SSO** текстовое поле, вставить значение hello **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-194">In hello **Identity provider SSO URL** text box, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7d3fd-195">c.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-195">c.</span></span> <span data-ttu-id="7d3fd-196">Откройте сертификат hello загружаются из Azure portal и скопировать значения hello без hello начало и конец строки и вставьте его в hello **X509 открытый сертификат** поле.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-196">Open hello downloaded certificate from Azure portal and copy hello values without hello Begin and End lines and paste it in hello **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="7d3fd-197">d.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-197">d.</span></span> <span data-ttu-id="7d3fd-198">Нажмите кнопку **сохранить конфигурацию** tooSave hello параметры.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-198">Click **Save Configuration**  tooSave hello settings.</span></span>
     
11. <span data-ttu-id="7d3fd-199">Обновите hello Azure AD параметры toomake наличие установки hello исправьте идентификатор URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-199">Update hello Azure AD settings toomake sure that you have setup hello correct Identifier URL.</span></span>
  
    <span data-ttu-id="7d3fd-200">а.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-200">a.</span></span> <span data-ttu-id="7d3fd-201">Копировать hello **идентификатор удостоверений SP** hello SAML экране и вставьте его в Azure AD в качестве hello **идентификатор** значение.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-201">Copy hello **SP Identity ID** from hello SAML screen and paste it in Azure AD as hello **Identifier** value.</span></span>

    <span data-ttu-id="7d3fd-202">b.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-202">b.</span></span> <span data-ttu-id="7d3fd-203">На URL-адрес входа — URL-адрес клиента hello Atlassian облака.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-203">Sign On URL is hello tenant URL of your Atlassian Cloud.</span></span>     

     ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="7d3fd-205">В hello портал Azure, щелкните **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-205">In hello Azure portal, Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="7d3fd-207">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="7d3fd-207">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7d3fd-208">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-208">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7d3fd-209">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7d3fd-209">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7d3fd-210">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d3fd-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="7d3fd-211">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-211">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7d3fd-213">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7d3fd-213">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d3fd-214">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-214">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7d3fd-216">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-216">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7d3fd-218">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="7d3fd-218">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d3fd-220">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7d3fd-220">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7d3fd-222">а.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-222">a.</span></span> <span data-ttu-id="7d3fd-223">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-223">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d3fd-224">b.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-224">b.</span></span> <span data-ttu-id="7d3fd-225">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-225">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7d3fd-226">c.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-226">c.</span></span> <span data-ttu-id="7d3fd-227">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-227">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7d3fd-228">d.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-228">d.</span></span> <span data-ttu-id="7d3fd-229">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="7d3fd-230">Создание тестового пользователя Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="7d3fd-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="7d3fd-231">Пользователи toolog tooenable Azure AD в tooAtlassian облака, их необходимо подготовить в облаке Atlassian.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-231">tooenable Azure AD users toolog in tooAtlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="7d3fd-232">В случае Atlassian Cloud подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="7d3fd-233">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7d3fd-233">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d3fd-234">В hello раздел администрирования сайта щелкните hello **пользователей** кнопки</span><span class="sxs-lookup"><span data-stu-id="7d3fd-234">In hello Site administration section, click hello **Users** button</span></span>

    ![Создание пользователя Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="7d3fd-236">Нажмите кнопку hello **Create User** кнопку toocreate пользователя в hello Atlassian облака</span><span class="sxs-lookup"><span data-stu-id="7d3fd-236">Click hello **Create User** button toocreate a user in hello Atlassian Cloud</span></span>

    ![Создание пользователя Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="7d3fd-238">Введите пользователя hello **адрес электронной почты**, **Username**, и **полное имя** и назначить доступ приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-238">Enter hello user's **Email address**, **Username**, and **Full Name** and assign hello application access.</span></span> 

    ![Создание пользователя Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="7d3fd-240">Нажмите кнопку **создать пользователя** кнопка, он отправляет приглашение toohello hello электронной почты пользователя и после принятия hello приглашения hello пользователя будет активным в системе hello.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-240">Click **Create user** button, it will send hello email invitation toohello user and after accepting hello invitation hello user will be active in hello system.</span></span> 

>[!NOTE] 
><span data-ttu-id="7d3fd-241">Можно также создать hello массового пользователей, щелкнув hello **массового создания** кнопку в разделе "пользователи" hello.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-241">You can also create hello bulk users by clicking hello **Bulk Create** button in hello Users section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7d3fd-242">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7d3fd-242">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7d3fd-243">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAtlassian облака.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-243">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtlassian Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7d3fd-245">**tooassign tooAtlassian Britta Simon облака, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="7d3fd-245">**tooassign Britta Simon tooAtlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d3fd-246">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-246">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7d3fd-248">В списке приложений hello выберите **Atlassian облака**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-248">In hello applications list, select **Atlassian Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="7d3fd-250">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-250">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7d3fd-252">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-252">Click **Add** button.</span></span> <span data-ttu-id="7d3fd-253">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7d3fd-255">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-255">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7d3fd-256">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d3fd-257">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7d3fd-258">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7d3fd-258">Testing single sign-on</span></span>

<span data-ttu-id="7d3fd-259">В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-259">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="7d3fd-260">При нажатии кнопки hello облака Atlassian плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Atlassian облачного приложения.</span><span class="sxs-lookup"><span data-stu-id="7d3fd-260">When you click hello Atlassian Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Atlassian Cloud application.</span></span> <span data-ttu-id="7d3fd-261">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7d3fd-261">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7d3fd-262">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7d3fd-262">Additional resources</span></span>

* [<span data-ttu-id="7d3fd-263">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7d3fd-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d3fd-264">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7d3fd-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

