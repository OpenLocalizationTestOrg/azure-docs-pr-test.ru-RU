---
title: "Учебник. Интеграция Azure Active Directory с Lifesize Cloud | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и облаком Lifesize."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="df71c-103">Учебник. Интеграция Azure Active Directory с Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="df71c-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="df71c-104">В этом учебнике вы узнаете, как toointegrate Lifesize облака в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df71c-104">In this tutorial, you learn how toointegrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df71c-105">Интеграция с Azure AD Lifesize облако предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="df71c-105">Integrating Lifesize Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="df71c-106">Можно управлять в Azure AD, имеющего доступ tooLifesize облака</span><span class="sxs-lookup"><span data-stu-id="df71c-106">You can control in Azure AD who has access tooLifesize Cloud</span></span>
- <span data-ttu-id="df71c-107">Можно включить на пользователей tooautomatically get вошедшего tooLifesize облака (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="df71c-107">You can enable your users tooautomatically get signed-on tooLifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="df71c-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="df71c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="df71c-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df71c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df71c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="df71c-110">Prerequisites</span></span>

<span data-ttu-id="df71c-111">tooconfigure интеграция Azure AD с облаком Lifesize требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="df71c-111">tooconfigure Azure AD integration with Lifesize Cloud, you need hello following items:</span></span>

- <span data-ttu-id="df71c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="df71c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df71c-113">подписка Lifesize Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="df71c-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df71c-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="df71c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="df71c-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="df71c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df71c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="df71c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="df71c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df71c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df71c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="df71c-118">Scenario description</span></span>
<span data-ttu-id="df71c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="df71c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df71c-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="df71c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df71c-121">Добавление Lifesize облака из галереи hello</span><span class="sxs-lookup"><span data-stu-id="df71c-121">Adding Lifesize Cloud from hello gallery</span></span>
2. <span data-ttu-id="df71c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="df71c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-hello-gallery"></a><span data-ttu-id="df71c-123">Добавление Lifesize облака из галереи hello</span><span class="sxs-lookup"><span data-stu-id="df71c-123">Adding Lifesize Cloud from hello gallery</span></span>
<span data-ttu-id="df71c-124">tooconfigure hello интеграция Lifesize облака в Azure AD, вы должны tooadd Lifesize облако из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="df71c-124">tooconfigure hello integration of Lifesize Cloud into Azure AD, you need tooadd Lifesize Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="df71c-125">**tooadd Lifesize облака из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="df71c-125">**tooadd Lifesize Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="df71c-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="df71c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="df71c-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="df71c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="df71c-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="df71c-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="df71c-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="df71c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="df71c-133">Введите в поле поиска hello **Lifesize облака**.</span><span class="sxs-lookup"><span data-stu-id="df71c-133">In hello search box, type **Lifesize Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="df71c-135">В панели результатов hello, выберите **облака Lifesize**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="df71c-135">In hello results panel, select **Lifesize Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="df71c-137">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df71c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="df71c-138">В этом разделе описана настройка и проверка единого входа Azure AD в Lifesize Cloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df71c-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="df71c-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в облаке Lifesize является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df71c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lifesize Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="df71c-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в облаке Lifesize должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="df71c-140">In other words, a link relationship between an Azure AD user and hello related user in Lifesize Cloud needs toobe established.</span></span>

<span data-ttu-id="df71c-141">В облаке Lifesize присвоить значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="df71c-141">In Lifesize Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="df71c-142">tooconfigure и тестирования Azure AD единого входа с облаком Lifesize, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="df71c-142">tooconfigure and test Azure AD single sign-on with Lifesize Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="df71c-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="df71c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="df71c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="df71c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df71c-145">**[Создание тестового пользователя облака Lifesize](#creating-a-lifesize-cloud-test-user)**  -toohave аналог Саймон Britta в облаке Lifesize, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="df71c-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - toohave a counterpart of Britta Simon in Lifesize Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="df71c-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="df71c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df71c-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="df71c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="df71c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="df71c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="df71c-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Lifesize облачного приложения.</span><span class="sxs-lookup"><span data-stu-id="df71c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="df71c-150">**tooconfigure Azure AD единого входа с облаком Lifesize выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="df71c-150">**tooconfigure Azure AD single sign-on with Lifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="df71c-151">В hello в hello портала Azure **облака Lifesize** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="df71c-151">In hello Azure portal, on hello **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="df71c-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="df71c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="df71c-155">На hello **URL-адреса и домена облака Lifesize** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="df71c-155">On hello **Lifesize Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="df71c-157">а.</span><span class="sxs-lookup"><span data-stu-id="df71c-157">a.</span></span> <span data-ttu-id="df71c-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="df71c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="df71c-159">b.</span><span class="sxs-lookup"><span data-stu-id="df71c-159">b.</span></span> <span data-ttu-id="df71c-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="df71c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="df71c-161">Проверьте **Показывать дополнительные параметры URL-адреса**, выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="df71c-161">Check **Show advanced URL settings**, perform hello following step:</span></span>  
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="df71c-163">В hello **ретрансляции состояние** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="df71c-163">In hello **Relay state** textbox, type a URL using hello following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="df71c-164">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="df71c-164">Please note that these are not hello real values.</span></span> <span data-ttu-id="df71c-165">имеется tooupdate эти значения с hello фактический URL-адрес входа, статус ретрансляции и идентификатора.</span><span class="sxs-lookup"><span data-stu-id="df71c-165">you have tooupdate these values with hello actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="df71c-166">Обратитесь к [группа поддержки клиента облака Lifesize](https://www.lifesize.com/support) tooget URL-адрес входа и значений идентификаторов, чтобы получить значение состояния ретрансляции из конфигурации единого входа, которая описывается далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="df71c-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) tooget Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in hello tutorial.</span></span>

4. <span data-ttu-id="df71c-167">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="df71c-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="df71c-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="df71c-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="df71c-171">На hello **конфигурации облака Lifesize** щелкните **Настройка облака Lifesize** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="df71c-171">On hello **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="df71c-172">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="df71c-172">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="df71c-174">tooget SSO настроен для вашего приложения, имя входа в hello Lifesize облачного приложения с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="df71c-174">tooget SSO configured for your application, login into hello Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="df71c-175">В hello правом верхнем углу щелкните свое имя и нажмите кнопку на hello **параметры обработки**.</span><span class="sxs-lookup"><span data-stu-id="df71c-175">In hello top right corner click on your name and then click on hello **Advance Settings**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="df71c-177">В параметры обработки щелкните hello hello **Настройка единого входа** ссылку.</span><span class="sxs-lookup"><span data-stu-id="df71c-177">In hello Advance Settings now click on hello **SSO Configuration** link.</span></span> <span data-ttu-id="df71c-178">Откроется страница hello настройку единого входа для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="df71c-178">It will open hello SSO Configuration page for your instance.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="df71c-180">Теперь можно настройте следующие значения в пользовательский Интерфейс для настройки единого входа hello hello.</span><span class="sxs-lookup"><span data-stu-id="df71c-180">Now configure hello following values in hello SSO configuration UI.</span></span>    
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="df71c-182">а.</span><span class="sxs-lookup"><span data-stu-id="df71c-182">a.</span></span> <span data-ttu-id="df71c-183">В **издатель поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="df71c-183">In **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="df71c-184">b.</span><span class="sxs-lookup"><span data-stu-id="df71c-184">b.</span></span>  <span data-ttu-id="df71c-185">В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="df71c-185">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="df71c-186">c.</span><span class="sxs-lookup"><span data-stu-id="df71c-186">c.</span></span> <span data-ttu-id="df71c-187">Откройте сертификат в кодировке base-64 в блокноте, загруженные из портала Azure hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="df71c-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="df71c-188">d.</span><span class="sxs-lookup"><span data-stu-id="df71c-188">d.</span></span> <span data-ttu-id="df71c-189">В атрибут SAML hello сопоставления для hello имя текстового поля введите значение hello как **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="df71c-189">In hello SAML Attribute mappings for hello First Name text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="df71c-190">д.</span><span class="sxs-lookup"><span data-stu-id="df71c-190">e.</span></span> <span data-ttu-id="df71c-191">В сопоставлении атрибут SAML hello для hello **Фамилия** текстовом поле введите значение hello как **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="df71c-191">In hello SAML Attribute mapping for hello **Last Name** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="df71c-192">f.</span><span class="sxs-lookup"><span data-stu-id="df71c-192">f.</span></span> <span data-ttu-id="df71c-193">В сопоставлении атрибут SAML hello для hello **электронной почты** текстовом поле введите значение hello как **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="df71c-193">In hello SAML Attribute mapping for hello **Email** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="df71c-194">можно щелкнуть hello конфигурации hello toocheck **тест** кнопки.</span><span class="sxs-lookup"><span data-stu-id="df71c-194">toocheck hello configuration you can click on hello **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="df71c-195">Для успешного тестирования требуется мастер настройки toocomplete hello в Azure AD и также предоставить доступ toousers или группы, которые можно выполнить проверку hello.</span><span class="sxs-lookup"><span data-stu-id="df71c-195">For successful testing you need toocomplete hello configuration wizard in Azure AD and also provide access toousers or groups who can perform hello test.</span></span>

12. <span data-ttu-id="df71c-196">Включите hello единого входа, установив на hello **Включить единый вход** кнопки.</span><span class="sxs-lookup"><span data-stu-id="df71c-196">Enable hello SSO by checking on hello **Enable SSO** button.</span></span>

13. <span data-ttu-id="df71c-197">Теперь щелкните hello **обновление** кнопку, чтобы все параметры hello сохраняются.</span><span class="sxs-lookup"><span data-stu-id="df71c-197">Now click on hello **Update** button so that all hello settings are saved.</span></span> <span data-ttu-id="df71c-198">Это создаст значение RelayState hello.</span><span class="sxs-lookup"><span data-stu-id="df71c-198">This will generate hello RelayState value.</span></span> <span data-ttu-id="df71c-199">Hello копирования RelayState значение, которое создается в текстовом поле hello, вставьте его в hello **состояние ретрансляции** текстовое поле в разделе **URL-адреса и домена облака Lifesize** раздела.</span><span class="sxs-lookup"><span data-stu-id="df71c-199">Copy hello RelayState value, which is generated in hello text box, paste it in hello **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="df71c-200">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="df71c-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="df71c-201">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="df71c-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="df71c-202">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="df71c-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="df71c-203">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="df71c-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="df71c-204">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="df71c-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="df71c-206">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="df71c-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="df71c-207">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="df71c-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="df71c-209">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="df71c-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="df71c-211">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="df71c-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df71c-213">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="df71c-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="df71c-215">а.</span><span class="sxs-lookup"><span data-stu-id="df71c-215">a.</span></span> <span data-ttu-id="df71c-216">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df71c-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df71c-217">b.</span><span class="sxs-lookup"><span data-stu-id="df71c-217">b.</span></span> <span data-ttu-id="df71c-218">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="df71c-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="df71c-219">c.</span><span class="sxs-lookup"><span data-stu-id="df71c-219">c.</span></span> <span data-ttu-id="df71c-220">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="df71c-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="df71c-221">d.</span><span class="sxs-lookup"><span data-stu-id="df71c-221">d.</span></span> <span data-ttu-id="df71c-222">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="df71c-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="df71c-223">Создание тестового пользователя Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="df71c-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="df71c-224">В этом разделе описано, как создать пользователя Britta Simon в приложении Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="df71c-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="df71c-225">Lifesize Cloud поддерживает автоматическую подготовку пользователей.</span><span class="sxs-lookup"><span data-stu-id="df71c-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="df71c-226">После успешной проверки подлинности в Azure AD hello пользователя будут автоматически подготовлены приложения hello.</span><span class="sxs-lookup"><span data-stu-id="df71c-226">After successful authentication at Azure AD, hello user will be automatically provisioned in hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="df71c-227">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="df71c-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="df71c-228">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLifesize облака.</span><span class="sxs-lookup"><span data-stu-id="df71c-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLifesize Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="df71c-230">**tooassign tooLifesize Britta Simon облака, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="df71c-230">**tooassign Britta Simon tooLifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="df71c-231">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="df71c-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="df71c-233">В списке приложений hello выберите **Lifesize облака**.</span><span class="sxs-lookup"><span data-stu-id="df71c-233">In hello applications list, select **Lifesize Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="df71c-235">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="df71c-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="df71c-237">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="df71c-237">Click **Add** button.</span></span> <span data-ttu-id="df71c-238">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="df71c-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="df71c-240">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="df71c-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="df71c-241">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="df71c-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df71c-242">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="df71c-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="df71c-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="df71c-243">Testing single sign-on</span></span>

<span data-ttu-id="df71c-244">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="df71c-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="df71c-245">При нажатии кнопки hello облака Lifesize плитки в панели доступа hello, должно появиться страница входа Lifesize облачного приложения.</span><span class="sxs-lookup"><span data-stu-id="df71c-245">When you click hello Lifesize Cloud tile in hello Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="df71c-246">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="df71c-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="df71c-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="df71c-247">Additional resources</span></span>

* [<span data-ttu-id="df71c-248">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df71c-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df71c-249">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df71c-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

