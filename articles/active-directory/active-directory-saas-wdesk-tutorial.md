---
title: "Руководство. Интеграция Azure Active Directory с приложением Wdesk | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="3f5bd-103">Руководство. Интеграция Azure Active Directory с Wdesk</span><span class="sxs-lookup"><span data-stu-id="3f5bd-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="3f5bd-104">В этом учебнике вы узнаете, как toointegrate Wdesk с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3f5bd-104">In this tutorial, you learn how toointegrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f5bd-105">Интеграция с Azure AD Wdesk предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-105">Integrating Wdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3f5bd-106">Можно управлять в Azure AD, имеющего доступ tooWdesk</span><span class="sxs-lookup"><span data-stu-id="3f5bd-106">You can control in Azure AD who has access tooWdesk</span></span>
- <span data-ttu-id="3f5bd-107">Можно включить на пользователей tooautomatically get вошедшего tooWdesk (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f5bd-107">You can enable your users tooautomatically get signed-on tooWdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f5bd-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3f5bd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3f5bd-109">Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="3f5bd-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3f5bd-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f5bd-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3f5bd-111">Prerequisites</span></span>

<span data-ttu-id="3f5bd-112">tooconfigure интеграция Azure AD с Wdesk требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-112">tooconfigure Azure AD integration with Wdesk, you need hello following items:</span></span>

- <span data-ttu-id="3f5bd-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3f5bd-113">An Azure AD subscription</span></span>
- <span data-ttu-id="3f5bd-114">подписка Wdesk с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3f5bd-115">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3f5bd-116">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f5bd-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f5bd-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f5bd-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f5bd-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3f5bd-119">Scenario description</span></span>
<span data-ttu-id="3f5bd-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3f5bd-121">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f5bd-122">Добавление Wdesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3f5bd-122">Adding Wdesk from hello gallery</span></span>
2. <span data-ttu-id="3f5bd-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f5bd-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-hello-gallery"></a><span data-ttu-id="3f5bd-124">Добавление Wdesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3f5bd-124">Adding Wdesk from hello gallery</span></span>
<span data-ttu-id="3f5bd-125">tooconfigure hello интеграции Wdesk в Azure AD, вы должны tooadd Wdesk из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-125">tooconfigure hello integration of Wdesk into Azure AD, you need tooadd Wdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3f5bd-126">**tooadd Wdesk из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3f5bd-126">**tooadd Wdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f5bd-127">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f5bd-129">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3f5bd-130">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-130">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3f5bd-132">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3f5bd-134">Введите в поле поиска hello **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-134">In hello search box, type **Wdesk**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="3f5bd-136">В панели результатов hello выберите **Wdesk**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-136">In hello results panel, select **Wdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3f5bd-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f5bd-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3f5bd-139">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Wdesk с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3f5bd-140">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Wdesk является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="3f5bd-141">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Wdesk должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-141">In other words, a link relationship between an Azure AD user and hello related user in Wdesk needs toobe established.</span></span>

<span data-ttu-id="3f5bd-142">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Wdesk.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wdesk.</span></span>

<span data-ttu-id="3f5bd-143">tooconfigure и теста Azure AD единого входа с Wdesk, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-143">tooconfigure and test Azure AD single sign-on with Wdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3f5bd-144">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3f5bd-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f5bd-146">**[Создание тестового пользователя Wdesk](#creating-a-wdesk-test-user)**  -toohave аналог Саймон Britta в Wdesk, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - toohave a counterpart of Britta Simon in Wdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3f5bd-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f5bd-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3f5bd-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f5bd-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3f5bd-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Wdesk.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="3f5bd-151">**tooconfigure Azure AD единого входа с Wdesk, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3f5bd-151">**tooconfigure Azure AD single sign-on with Wdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f5bd-152">В hello в hello портала Azure **Wdesk** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-152">In hello Azure portal, on hello **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3f5bd-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="3f5bd-156">На hello **URL-адреса и домена Wdesk** статьи, при желании tooconfigure приложения hello в **поставщика Удостоверений** инициируемых режиме выполняется hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-156">On hello **Wdesk Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="3f5bd-158">а.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-158">a.</span></span> <span data-ttu-id="3f5bd-159">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="3f5bd-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="3f5bd-160">b.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-160">b.</span></span> <span data-ttu-id="3f5bd-161">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="3f5bd-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="3f5bd-162">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="3f5bd-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="3f5bd-163">При необходимости приложение hello tooconfigure в **SP** инициировал режим, выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-163">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="3f5bd-165">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="3f5bd-165">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3f5bd-166">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-166">These values are not real.</span></span> <span data-ttu-id="3f5bd-167">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3f5bd-168">Вы можете получить эти значения из портала WDesk, при настройке единого входа hello.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-168">You get these values from WDesk portal when you configure hello SSO.</span></span> 
  
5. <span data-ttu-id="3f5bd-169">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="3f5bd-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3f5bd-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3f5bd-173">В другом окне браузера, tooWdesk входа в систему с учетной записью администратора безопасности.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-173">In a different web browser window, login tooWdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="3f5bd-174">В левом нижнем hello, щелкните **администратора** и выберите **администратор учетной записи**:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-174">In hello bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="3f5bd-176">Администратор Wdesk перейдите слишком**безопасности**, затем **SAML** > **параметры SAML**:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-176">In Wdesk Admin, navigate too**Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="3f5bd-178">В разделе **Общие параметры**, проверьте hello **включить SAML Single Sign On**:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-178">Under **General Settings**, check hello **Enable SAML Single Sign On**:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="3f5bd-180">В разделе **подробные сведения о поставщике службы**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-180">Under **Service Provider Details**, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="3f5bd-182">а.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-182">a.</span></span> <span data-ttu-id="3f5bd-183">Копировать hello **URL-адрес входа** и вставьте его в **URL-адрес входа** текстовое поле на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-183">Copy hello **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="3f5bd-184">b.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-184">b.</span></span> <span data-ttu-id="3f5bd-185">Копировать hello **URL-адрес метаданных** и вставьте его в **идентификатор** текстовое поле на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-185">Copy hello **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="3f5bd-186">c.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-186">c.</span></span> <span data-ttu-id="3f5bd-187">Копировать hello **URL-адрес потребителя** и вставьте его в **URL-адрес ответа** текстовое поле на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-187">Copy hello **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="3f5bd-188">d.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-188">d.</span></span> <span data-ttu-id="3f5bd-189">Нажмите кнопку **Сохранить** об изменениях hello Azure toosave портала.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-189">Click **Save** on Azure portal toosave hello changes.</span></span>      

12. <span data-ttu-id="3f5bd-190">Нажмите кнопку **настроить параметры поставщика удостоверений** tooopen **изменение параметров поставщика удостоверений** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-190">Click **Configure IdP Settings** tooopen **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="3f5bd-191">Нажмите кнопку **выбрать файл** toolocate hello **Metadata.xml** файл, сохраненный с портала Azure, затем передать его.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-191">Click **Choose File** toolocate hello **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="3f5bd-193">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-193">Click **Save changes**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="3f5bd-195">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="3f5bd-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3f5bd-196">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3f5bd-197">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3f5bd-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3f5bd-198">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f5bd-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="3f5bd-199">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3f5bd-201">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3f5bd-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f5bd-202">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f5bd-204">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f5bd-206">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="3f5bd-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f5bd-208">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3f5bd-210">а.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-210">a.</span></span> <span data-ttu-id="3f5bd-211">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f5bd-212">b.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-212">b.</span></span> <span data-ttu-id="3f5bd-213">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3f5bd-214">c.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-214">c.</span></span> <span data-ttu-id="3f5bd-215">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3f5bd-216">d.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-216">d.</span></span> <span data-ttu-id="3f5bd-217">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="3f5bd-218">Создание тестового пользователя Wdesk</span><span class="sxs-lookup"><span data-stu-id="3f5bd-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="3f5bd-219">Пользователи toolog tooenable Azure AD в tooWdesk, их необходимо подготовить в Wdesk.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-219">tooenable Azure AD users toolog in tooWdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="3f5bd-220">В Wdesk подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="3f5bd-221">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3f5bd-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f5bd-222">Войдите с учетной записью администратора безопасности tooWdesk.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-222">Log in tooWdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="3f5bd-223">Перейдите в слишком**администратора** > **администратор учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-223">Navigate too**Admin** > **Account Admin**.</span></span>

     ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="3f5bd-225">Щелкните элемент **Members** (Участники) в разделе **People** (Люди).</span><span class="sxs-lookup"><span data-stu-id="3f5bd-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="3f5bd-226">Теперь щелкните **Add Member** tooopen **Add Member** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-226">Now click **Add Member** tooopen **Add Member** dialog box.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="3f5bd-228">В **пользователя** текста введите hello имя пользователя как  **brittasimon@contoso.com**  и нажмите кнопку **Продолжить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-228">In **User** text box, enter hello username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="3f5bd-230">Введите сведения hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="3f5bd-230">Enter hello details as shown below:</span></span>
  
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="3f5bd-232">а.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-232">a.</span></span> <span data-ttu-id="3f5bd-233">В **электронной почты** текста введите hello электронной почты пользователя, таких как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="3f5bd-233">In **E-mail** text box, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="3f5bd-234">b.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-234">b.</span></span> <span data-ttu-id="3f5bd-235">В **имя** текста введите имя пользователя, такие как hello **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-235">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="3f5bd-236">c.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-236">c.</span></span> <span data-ttu-id="3f5bd-237">В **Фамилия** текста введите hello фамилию пользователя как **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-237">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

7. <span data-ttu-id="3f5bd-238">Щелкните кнопку **Save Member** (Сохранить участника).</span><span class="sxs-lookup"><span data-stu-id="3f5bd-238">Click **Save Member** button.</span></span>  

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3f5bd-240">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="3f5bd-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3f5bd-241">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWdesk доступа.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWdesk.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3f5bd-243">**tooassign tooWdesk Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3f5bd-243">**tooassign Britta Simon tooWdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f5bd-244">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3f5bd-246">В списке приложений hello выберите **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-246">In hello applications list, select **Wdesk**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="3f5bd-248">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3f5bd-250">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-250">Click **Add** button.</span></span> <span data-ttu-id="3f5bd-251">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3f5bd-253">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3f5bd-254">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f5bd-255">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3f5bd-256">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3f5bd-256">Testing single sign-on</span></span>

<span data-ttu-id="3f5bd-257">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-257">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3f5bd-258">При нажатии кнопки hello Wdesk плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Wdesk приложения.</span><span class="sxs-lookup"><span data-stu-id="3f5bd-258">When you click hello Wdesk tile in hello Access Panel, you should get automatically signed-on tooyour Wdesk application.</span></span>
<span data-ttu-id="3f5bd-259">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3f5bd-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3f5bd-260">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3f5bd-260">Additional resources</span></span>

* [<span data-ttu-id="3f5bd-261">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f5bd-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f5bd-262">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3f5bd-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

