---
title: "Руководство по интеграции Azure Active Directory с Zendesk | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="7b371-103">Руководство. Интеграция Azure Active Directory с Zendesk</span><span class="sxs-lookup"><span data-stu-id="7b371-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="7b371-104">В этом учебнике вы узнаете, как toointegrate Zendesk с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b371-104">In this tutorial, you learn how toointegrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b371-105">Интеграция Zendesk с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7b371-105">Integrating Zendesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7b371-106">Можно управлять в Azure AD, имеющего доступ tooZendesk</span><span class="sxs-lookup"><span data-stu-id="7b371-106">You can control in Azure AD who has access tooZendesk</span></span>
- <span data-ttu-id="7b371-107">Можно включить на пользователей tooautomatically get вошедшего tooZendesk (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b371-107">You can enable your users tooautomatically get signed-on tooZendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b371-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7b371-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7b371-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b371-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b371-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7b371-110">Prerequisites</span></span>

<span data-ttu-id="7b371-111">tooconfigure интеграция Azure AD с Zendesk требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7b371-111">tooconfigure Azure AD integration with Zendesk, you need hello following items:</span></span>

- <span data-ttu-id="7b371-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7b371-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b371-113">подписка Zendesk с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7b371-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="7b371-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7b371-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="7b371-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7b371-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b371-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7b371-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b371-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b371-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="7b371-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7b371-118">Scenario description</span></span>
<span data-ttu-id="7b371-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7b371-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b371-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7b371-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b371-121">Добавление Zendesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7b371-121">Adding Zendesk from hello gallery</span></span>
2. <span data-ttu-id="7b371-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b371-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-hello-gallery"></a><span data-ttu-id="7b371-123">Добавление Zendesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7b371-123">Adding Zendesk from hello gallery</span></span>
<span data-ttu-id="7b371-124">tooconfigure hello интеграции Zendesk в Azure AD, вы должны tooadd Zendesk из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7b371-124">tooconfigure hello integration of Zendesk into Azure AD, you need tooadd Zendesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7b371-125">**tooadd Zendesk из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7b371-125">**tooadd Zendesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b371-126">В hello  **[портала Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7b371-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7b371-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="7b371-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7b371-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7b371-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7b371-131">Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="7b371-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7b371-133">Введите в поле поиска hello **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="7b371-133">In hello search box, type **Zendesk**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="7b371-135">В панели результатов hello выберите **Zendesk**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7b371-135">In hello results panel, select **Zendesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7b371-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b371-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7b371-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Zendesk с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b371-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7b371-139">Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в Zendesk — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b371-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zendesk is tooa user in Azure AD.</span></span> <span data-ttu-id="7b371-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Zendesk должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7b371-140">In other words, a link relationship between an Azure AD user and hello related user in Zendesk needs toobe established.</span></span>

<span data-ttu-id="7b371-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Zendesk.</span><span class="sxs-lookup"><span data-stu-id="7b371-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zendesk.</span></span>

<span data-ttu-id="7b371-142">tooconfigure и теста Azure AD единого входа с Zendesk, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7b371-142">tooconfigure and test Azure AD single sign-on with Zendesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7b371-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7b371-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7b371-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7b371-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b371-145">**[Создание тестового пользователя Zendesk](#creating-a-zendesk-test-user)**  -toohave аналог Саймон Britta в Zendesk, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="7b371-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - toohave a counterpart of Britta Simon in Zendesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b371-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7b371-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b371-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7b371-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7b371-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b371-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7b371-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Zendesk.</span><span class="sxs-lookup"><span data-stu-id="7b371-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="7b371-150">**tooconfigure Azure AD единого входа с помощью Zendesk, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7b371-150">**tooconfigure Azure AD single sign-on with Zendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b371-151">В hello в hello портала Azure **Zendesk** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7b371-151">In hello Azure portal, on hello **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7b371-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="7b371-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="7b371-155">На hello **URL-адреса и домена Zendesk** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7b371-155">On hello **Zendesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="7b371-157">а.</span><span class="sxs-lookup"><span data-stu-id="7b371-157">a.</span></span> <span data-ttu-id="7b371-158">В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="7b371-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="7b371-159">b.</span><span class="sxs-lookup"><span data-stu-id="7b371-159">b.</span></span> <span data-ttu-id="7b371-160">В hello **идентификатор** текстовое значение hello типа, используя следующий шаблон hello:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="7b371-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b371-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="7b371-161">These values are not real.</span></span> <span data-ttu-id="7b371-162">Обновите эти значения с hello фактический URL-адрес входа и URL-адрес идентификатора.</span><span class="sxs-lookup"><span data-stu-id="7b371-162">Update these values with hello actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="7b371-163">Обратитесь к [группа поддержки Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="7b371-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget these values.</span></span> 

4. <span data-ttu-id="7b371-164">Zendesk ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="7b371-164">Zendesk expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7b371-165">Отсутствуют обязательные атрибуты SAML, но при необходимости можно добавить атрибут из **атрибуты пользователя** раздел по hello следующие шаги, описанные ниже:</span><span class="sxs-lookup"><span data-stu-id="7b371-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following hello below steps:</span></span> 

     ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="7b371-167">а.</span><span class="sxs-lookup"><span data-stu-id="7b371-167">a.</span></span> <span data-ttu-id="7b371-168">Нажмите кнопку hello **Просмотр и изменение hello другие атрибуты** флажок.</span><span class="sxs-lookup"><span data-stu-id="7b371-168">Click hello **View and edit all hello other attributes** check box.</span></span>
     
    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="7b371-170">b.</span><span class="sxs-lookup"><span data-stu-id="7b371-170">b.</span></span> <span data-ttu-id="7b371-171">Нажмите кнопку hello **Добавление атрибута** tooopen **добавить атрибут** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7b371-171">Click hello **Add Attribute** tooopen **Add attribute** dialog.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="7b371-173">c.</span><span class="sxs-lookup"><span data-stu-id="7b371-173">c.</span></span> <span data-ttu-id="7b371-174">В hello **имя** в текстовое поле имя атрибута типа hello (например **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="7b371-174">In hello **Name** textbox, type hello attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="7b371-175">d.</span><span class="sxs-lookup"><span data-stu-id="7b371-175">d.</span></span> <span data-ttu-id="7b371-176">Из hello **значение** списка значение атрибута выберите hello (как **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="7b371-176">From hello **Value** list, select hello attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="7b371-177">д.</span><span class="sxs-lookup"><span data-stu-id="7b371-177">e.</span></span> <span data-ttu-id="7b371-178">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7b371-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="7b371-179">Расширения атрибутов tooadd атрибуты, которые не находятся в Azure AD по умолчанию использовать.</span><span class="sxs-lookup"><span data-stu-id="7b371-179">You use extension attributes tooadd attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="7b371-180">Нажмите кнопку [атрибутов пользователей, которые могут быть установлены в SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello SAML в полный список атрибутов, **Zendesk** принимает.</span><span class="sxs-lookup"><span data-stu-id="7b371-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="7b371-181">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.</span><span class="sxs-lookup"><span data-stu-id="7b371-181">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="7b371-183">На hello **конфигурации Zendesk** щелкните **Настройка Zendesk** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="7b371-183">On hello **Zendesk Configuration** section, click **Configure Zendesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7b371-184">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="7b371-184">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="7b371-186">В другом окне браузера войдите на свой корпоративный сайт Zendesk в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="7b371-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="7b371-187">Щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="7b371-187">Click **Admin**.</span></span>

9. <span data-ttu-id="7b371-188">Hello панели навигации слева щелкните **параметры**, а затем нажмите кнопку **безопасности**.</span><span class="sxs-lookup"><span data-stu-id="7b371-188">In hello left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="7b371-189">На hello **безопасности** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7b371-189">On hello **Security** page, perform hello following steps:</span></span> 
   
     <span data-ttu-id="7b371-190">![Безопасность](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="7b371-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="7b371-191">![Единый вход](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="7b371-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="7b371-192">а.</span><span class="sxs-lookup"><span data-stu-id="7b371-192">a.</span></span> <span data-ttu-id="7b371-193">Нажмите кнопку hello **Admin & агенты** вкладки.</span><span class="sxs-lookup"><span data-stu-id="7b371-193">Click hello **Admin & Agents** tab.</span></span>

     <span data-ttu-id="7b371-194">b.</span><span class="sxs-lookup"><span data-stu-id="7b371-194">b.</span></span> <span data-ttu-id="7b371-195">Выберите **Single sign-on (SSO) and SAML** (Единый вход и SAML), а затем щелкните **SAML**.</span><span class="sxs-lookup"><span data-stu-id="7b371-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="7b371-196">c.</span><span class="sxs-lookup"><span data-stu-id="7b371-196">c.</span></span> <span data-ttu-id="7b371-197">В **URL-адрес единого входа SAML** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7b371-197">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="7b371-198">d.</span><span class="sxs-lookup"><span data-stu-id="7b371-198">d.</span></span> <span data-ttu-id="7b371-199">В **URL-адрес удаленного выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7b371-199">In **Remote Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="7b371-200">д.</span><span class="sxs-lookup"><span data-stu-id="7b371-200">e.</span></span> <span data-ttu-id="7b371-201">В **отпечаток сертификата** текстовое поле, вставить hello **отпечаток** значение сертификата, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7b371-201">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="7b371-202">f.</span><span class="sxs-lookup"><span data-stu-id="7b371-202">f.</span></span> <span data-ttu-id="7b371-203">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7b371-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7b371-204">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b371-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="7b371-205">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7b371-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7b371-207">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7b371-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b371-208">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7b371-208">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b371-210">hello toodisplay список пользователей перейти слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7b371-210">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b371-212">Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7b371-212">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b371-214">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7b371-214">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b371-216">а.</span><span class="sxs-lookup"><span data-stu-id="7b371-216">a.</span></span> <span data-ttu-id="7b371-217">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b371-217">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b371-218">b.</span><span class="sxs-lookup"><span data-stu-id="7b371-218">b.</span></span> <span data-ttu-id="7b371-219">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7b371-219">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7b371-220">c.</span><span class="sxs-lookup"><span data-stu-id="7b371-220">c.</span></span> <span data-ttu-id="7b371-221">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="7b371-221">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7b371-222">d.</span><span class="sxs-lookup"><span data-stu-id="7b371-222">d.</span></span> <span data-ttu-id="7b371-223">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7b371-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="7b371-224">Создание тестового пользователя Zendesk</span><span class="sxs-lookup"><span data-stu-id="7b371-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="7b371-225">toolog tooenable Azure AD пользователи в **Zendesk**, их необходимо подготовить в **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="7b371-225">tooenable Azure AD users toolog into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="7b371-226">В зависимости от роли hello, назначенные в приложения hello его hello ожидаемое поведение:</span><span class="sxs-lookup"><span data-stu-id="7b371-226">Depending on hello role assigned in hello apps, it's hello expected behavior:</span></span>

 1. <span data-ttu-id="7b371-227">Учетные записи с ролью **Конечный пользователь** подготавливаются автоматически при входе.</span><span class="sxs-lookup"><span data-stu-id="7b371-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="7b371-228">**Агент** и **администратора** учетные записи должны вручную подготовить в toobe **Zendesk** перед входом в.</span><span class="sxs-lookup"><span data-stu-id="7b371-228">**Agent** and **Admin** accounts need toobe manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="7b371-229">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7b371-229">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b371-230">Войдите в tooyour **Zendesk** клиента.</span><span class="sxs-lookup"><span data-stu-id="7b371-230">Log in tooyour **Zendesk** tenant.</span></span>

2. <span data-ttu-id="7b371-231">Выберите hello **список клиентов** вкладки.</span><span class="sxs-lookup"><span data-stu-id="7b371-231">Select hello **Customer List** tab.</span></span>

3. <span data-ttu-id="7b371-232">Выберите hello **пользователя** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="7b371-232">Select hello **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="7b371-233">![Добавление пользователя](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="7b371-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="7b371-234">Введите адрес электронной почты hello существующей учетной записи Azure AD tooprovision и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7b371-234">Type hello email address of an existing Azure AD account you want tooprovision, and then click **Save**.</span></span>
   
    <span data-ttu-id="7b371-235">![Новый пользователь](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="7b371-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="7b371-236">Можно использовать любые другие Zendesk пользователя средства создания учетных записей или интерфейсы API, предоставляемые Zendesk tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="7b371-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7b371-237">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7b371-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7b371-238">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooZendesk доступа.</span><span class="sxs-lookup"><span data-stu-id="7b371-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZendesk.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7b371-240">**tooassign tooZendesk Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7b371-240">**tooassign Britta Simon tooZendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b371-241">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7b371-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7b371-243">В списке приложений hello выберите **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="7b371-243">In hello applications list, select **Zendesk**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="7b371-245">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="7b371-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7b371-247">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7b371-247">Click **Add** button.</span></span> <span data-ttu-id="7b371-248">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7b371-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7b371-250">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7b371-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7b371-251">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7b371-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b371-252">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7b371-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7b371-253">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7b371-253">Testing single sign-on</span></span>

<span data-ttu-id="7b371-254">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="7b371-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7b371-255">При нажатии кнопки hello Zendesk плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на Zendesk приложения.</span><span class="sxs-lookup"><span data-stu-id="7b371-255">When you click hello Zendesk tile in hello Access Panel, you should get automatically signed-on tooyour Zendesk application.</span></span>
<span data-ttu-id="7b371-256">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b371-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b371-257">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7b371-257">Additional resources</span></span>

* [<span data-ttu-id="7b371-258">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b371-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b371-259">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b371-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
