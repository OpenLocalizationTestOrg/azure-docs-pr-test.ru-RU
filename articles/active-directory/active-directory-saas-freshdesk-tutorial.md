---
title: "Руководство по интеграции Azure Active Directory с FreshDesk | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="9d5e8-103">Руководство по интеграции Azure Active Directory с FreshDesk</span><span class="sxs-lookup"><span data-stu-id="9d5e8-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="9d5e8-104">В этом учебнике вы узнаете, как toointegrate FreshDesk с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d5e8-104">In this tutorial, you learn how toointegrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d5e8-105">Интеграция FreshDesk с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9d5e8-105">Integrating FreshDesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9d5e8-106">Можно управлять в Azure AD, имеющего доступ tooFreshDesk</span><span class="sxs-lookup"><span data-stu-id="9d5e8-106">You can control in Azure AD who has access tooFreshDesk</span></span>
- <span data-ttu-id="9d5e8-107">Можно включить на пользователей tooautomatically get вошедшего tooFreshDesk (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d5e8-107">You can enable your users tooautomatically get signed-on tooFreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d5e8-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="9d5e8-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="9d5e8-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d5e8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d5e8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9d5e8-110">Prerequisites</span></span>

<span data-ttu-id="9d5e8-111">tooconfigure интеграция Azure AD с FreshDesk требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="9d5e8-111">tooconfigure Azure AD integration with FreshDesk, you need hello following items:</span></span>

- <span data-ttu-id="9d5e8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9d5e8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d5e8-113">подписка FreshDesk с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d5e8-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d5e8-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="9d5e8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d5e8-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9d5e8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d5e8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d5e8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9d5e8-118">Scenario description</span></span>
<span data-ttu-id="9d5e8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d5e8-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="9d5e8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d5e8-121">Добавление FreshDesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9d5e8-121">Adding FreshDesk from hello gallery</span></span>
2. <span data-ttu-id="9d5e8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d5e8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-hello-gallery"></a><span data-ttu-id="9d5e8-123">Добавление FreshDesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9d5e8-123">Adding FreshDesk from hello gallery</span></span>
<span data-ttu-id="9d5e8-124">tooconfigure hello интеграции FreshDesk в Azure AD, вы должны tooadd FreshDesk из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-124">tooconfigure hello integration of FreshDesk into Azure AD, you need tooadd FreshDesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9d5e8-125">**tooadd FreshDesk из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9d5e8-125">**tooadd FreshDesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d5e8-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d5e8-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9d5e8-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9d5e8-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="9d5e8-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9d5e8-133">Введите в поле поиска hello **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-133">In hello search box, type **FreshDesk**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="9d5e8-135">В панели результатов hello выберите **FreshDesk**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-135">In hello results panel, select **FreshDesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d5e8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d5e8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d5e8-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение FreshDesk с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d5e8-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в FreshDesk является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshDesk is tooa user in Azure AD.</span></span> <span data-ttu-id="9d5e8-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в FreshDesk требуется toobe установлено.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-140">In other words, a link relationship between an Azure AD user and hello related user in FreshDesk needs toobe established.</span></span>

<span data-ttu-id="9d5e8-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FreshDesk.</span></span>

<span data-ttu-id="9d5e8-142">tooconfigure и теста Azure AD единого входа с FreshDesk, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9d5e8-142">tooconfigure and test Azure AD single sign-on with FreshDesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9d5e8-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9d5e8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d5e8-145">**[Создание тестового пользователя FreshDesk](#creating-a-freshdesk-test-user)**  -toohave аналог Саймон Britta в FreshDesk, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - toohave a counterpart of Britta Simon in FreshDesk that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9d5e8-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d5e8-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d5e8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d5e8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d5e8-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в ваше приложение Freshservice.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="9d5e8-150">**tooconfigure Azure AD единого входа с FreshDesk, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9d5e8-150">**tooconfigure Azure AD single sign-on with FreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d5e8-151">На портале управления Azure hello на hello **FreshDesk** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-151">In hello Azure Management portal, on hello **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9d5e8-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="9d5e8-155">На hello **URL-адреса и домена FreshDesk** статьи, введите hello **URL-адрес входа** как: `https://<tenant-name>.freshdesk.com` или любое другое значение имеет предлагаемых Freshdesk.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-155">On hello **FreshDesk Domain and URLs** section, please enter hello **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="9d5e8-157">Обратите внимание, что это значение используется только в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-157">Please note that this is not the real value.</span></span> <span data-ttu-id="9d5e8-158">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="9d5e8-159">Для получения этого значения обратитесь в [службу поддержки клиентов FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg).</span><span class="sxs-lookup"><span data-stu-id="9d5e8-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="9d5e8-160">На hello **сертификат подписи SAML** щелкните **сертификат** и сохраните hello сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-160">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="9d5e8-162">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9d5e8-162">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d5e8-164">На hello **конфигурации FreshDesk** щелкните **Настройка FreshDesk** tooopen Настройка входа окна.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-164">On hello **FreshDesk Configuration** section, click **Configure FreshDesk** tooopen Configure sign-on window.</span></span> <span data-ttu-id="9d5e8-165">Скопируйте hello SAML единого входа URL-адрес службы и URL-адрес выхода из hello **краткий справочник** раздела.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-165">Copy hello SAML Single Sign-On Service URL and Sign-Out URL from hello **Quick Reference** section.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="9d5e8-167">В другом окне браузера войдите на свой корпоративный веб-сайт Freshdesk в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="9d5e8-168">В меню в верхней части hello hello выберите **администратора**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-168">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="9d5e8-169">![Администратор](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="9d5e8-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="9d5e8-170">В hello **Общие параметры** щелкните **безопасности**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-170">In hello **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="9d5e8-171">![Безопасность](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="9d5e8-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="9d5e8-172">В hello **безопасности** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9d5e8-172">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9d5e8-173">![Единый вход](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="9d5e8-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="9d5e8-174">а.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-174">a.</span></span> <span data-ttu-id="9d5e8-175">Выберите для параметра **Single Sign On (SSO)** (Единый вход) значение **On** (Включено).</span><span class="sxs-lookup"><span data-stu-id="9d5e8-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="9d5e8-176">b.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-176">b.</span></span> <span data-ttu-id="9d5e8-177">Выберите **Единый вход SAML**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="9d5e8-178">c.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-178">c.</span></span> <span data-ttu-id="9d5e8-179">Тип hello **SAML единого входа URL-адрес службы** скопирован из портала Azure в hello **URL-адрес входа SAML** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-179">Type hello **SAML Single Sign-On Service URL** you copied from Azure portal into hello **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="9d5e8-180">d.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-180">d.</span></span> <span data-ttu-id="9d5e8-181">Тип hello **URL-адрес выхода** скопирован из портала Azure в hello **URL-адрес выхода** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-181">Type hello **Sign-Out URL**  you copied from Azure portal into hello **Logout URL** textbox.</span></span>

    <span data-ttu-id="9d5e8-182">д.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-182">e.</span></span> <span data-ttu-id="9d5e8-183">Копировать hello **отпечаток** из сертификата hello загружен с портала Azure и вставьте его в hello **отпечаток сертификата безопасности** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-183">Copy hello **Thumbprint** value from hello downloaded certificate from Azure portal and paste it into hello **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="9d5e8-184">Дополнительные сведения см. в разделе [как tooretrieve значение отпечатка сертификата](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="9d5e8-184">For more details, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="9d5e8-185">f.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-185">f.</span></span> <span data-ttu-id="9d5e8-186">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d5e8-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d5e8-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d5e8-188">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9d5e8-190">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9d5e8-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d5e8-191">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d5e8-193">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d5e8-195">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d5e8-197">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9d5e8-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d5e8-199">а.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-199">a.</span></span> <span data-ttu-id="9d5e8-200">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d5e8-201">b.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-201">b.</span></span> <span data-ttu-id="9d5e8-202">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d5e8-203">c.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-203">c.</span></span> <span data-ttu-id="9d5e8-204">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9d5e8-205">d.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-205">d.</span></span> <span data-ttu-id="9d5e8-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="9d5e8-207">Создание тестового пользователя FreshDesk</span><span class="sxs-lookup"><span data-stu-id="9d5e8-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="9d5e8-208">В порядке tooenable toolog пользователей Azure AD в FreshDesk их необходимо подготовить во FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-208">In order tooenable Azure AD users toolog into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="9d5e8-209">В случае hello объекта FreshDesk Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-209">In hello case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="9d5e8-210">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="9d5e8-210">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d5e8-211">Войдите в tooyour **Freshdesk** клиента.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-211">Log in tooyour **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="9d5e8-212">В меню в верхней части hello hello выберите **администратора**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-212">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="9d5e8-213">![Администратор](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="9d5e8-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="9d5e8-214">В hello **Общие параметры** щелкните **агенты**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-214">In hello **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="9d5e8-215">![Агенты](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Агенты")</span><span class="sxs-lookup"><span data-stu-id="9d5e8-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="9d5e8-216">Нажмите **Создать агента**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="9d5e8-217">![Создание агента](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "Создание агента")</span><span class="sxs-lookup"><span data-stu-id="9d5e8-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="9d5e8-218">В диалоговом окне сведений об агенте hello выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-218">On hello Agent Information dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="9d5e8-219">![Сведения об агенте](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Сведения об агенте")</span><span class="sxs-lookup"><span data-stu-id="9d5e8-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="9d5e8-220">а.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-220">a.</span></span> <span data-ttu-id="9d5e8-221">В hello **полное имя** текстовое поле, имя типа hello hello Azure AD счета tooprovision.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-221">In hello **Full Name** textbox, type hello name of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="9d5e8-222">b.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-222">b.</span></span> <span data-ttu-id="9d5e8-223">В hello **электронной почты** текстового поля, типа hello Azure AD адрес электронной почты учетной записи hello Azure AD будет tooprovision.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-223">In hello **Email** textbox, type hello Azure AD email address of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="9d5e8-224">c.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-224">c.</span></span> <span data-ttu-id="9d5e8-225">В hello **заголовок** текстовом поле введите название hello hello Azure AD счета tooprovision.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-225">In hello **Title** textbox, type hello title of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="9d5e8-226">d.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-226">d.</span></span> <span data-ttu-id="9d5e8-227">Выберите **Agents role** (Роль агента) и нажмите кнопку **Assign** (Назначить).</span><span class="sxs-lookup"><span data-stu-id="9d5e8-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="9d5e8-228">д.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-228">e.</span></span> <span data-ttu-id="9d5e8-229">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="9d5e8-230">Владелец учетной записи Hello Azure AD получит сообщение электронной почты, включает в себя учетную запись hello tooconfirm ссылку, перед его активации.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-230">hello Azure AD account holder will get an email that includes a link tooconfirm hello account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="9d5e8-231">Можно использовать любые другие Freshdesk пользователя средства создания учетных записей или интерфейсы API, предоставляемые Freshdesk tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk tooprovision AAD user accounts.</span></span> <span data-ttu-id="9d5e8-232">tooFreshDesk.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-232">tooFreshDesk.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9d5e8-233">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="9d5e8-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9d5e8-234">В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ панель инструментов.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBox.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9d5e8-236">**tooassign tooFreshDesk Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9d5e8-236">**tooassign Britta Simon tooFreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d5e8-237">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-237">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9d5e8-239">В списке приложений hello выберите **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-239">In hello applications list, select **FreshDesk**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="9d5e8-241">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9d5e8-243">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-243">Click **Add** button.</span></span> <span data-ttu-id="9d5e8-244">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9d5e8-246">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9d5e8-247">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d5e8-248">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d5e8-249">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9d5e8-249">Testing single sign-on</span></span>

<span data-ttu-id="9d5e8-250">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9d5e8-251">При нажатии кнопки hello FreshDesk плитки в панели доступа hello, вы должны получить входа страницы tooget вошедшего tooyour приложение Freshservice.</span><span class="sxs-lookup"><span data-stu-id="9d5e8-251">When you click hello FreshDesk tile in hello Access Panel, you should get login page tooget signed-on tooyour FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d5e8-252">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9d5e8-252">Additional resources</span></span>

* [<span data-ttu-id="9d5e8-253">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d5e8-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d5e8-254">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d5e8-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

