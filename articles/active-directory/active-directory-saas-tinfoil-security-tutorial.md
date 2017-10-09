---
title: "Руководство по интеграции Azure Active Directory с TINFOIL SECURITY | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="129cb-103">Руководство по интеграции Azure Active Directory с TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="129cb-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="129cb-104">В этом учебнике вы узнаете, как toointegrate TINFOIL SECURITY с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="129cb-104">In this tutorial, you learn how toointegrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="129cb-105">Интеграция TINFOIL SECURITY с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="129cb-105">Integrating TINFOIL SECURITY with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="129cb-106">Можно управлять в Azure AD, имеющего доступ tooTINFOIL безопасности</span><span class="sxs-lookup"><span data-stu-id="129cb-106">You can control in Azure AD who has access tooTINFOIL SECURITY</span></span>
- <span data-ttu-id="129cb-107">Можно включить на пользователей tooautomatically get вошедшего tooTINFOIL безопасности (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="129cb-107">You can enable your users tooautomatically get signed-on tooTINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="129cb-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="129cb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="129cb-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="129cb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="129cb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="129cb-110">Prerequisites</span></span>

<span data-ttu-id="129cb-111">tooconfigure интеграция Azure AD с TINFOIL SECURITY требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="129cb-111">tooconfigure Azure AD integration with TINFOIL SECURITY, you need hello following items:</span></span>

- <span data-ttu-id="129cb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="129cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="129cb-113">подписка TINFOIL SECURITY с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="129cb-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="129cb-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="129cb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="129cb-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="129cb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="129cb-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="129cb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="129cb-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="129cb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="129cb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="129cb-118">Scenario description</span></span>
<span data-ttu-id="129cb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="129cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="129cb-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="129cb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="129cb-121">Добавление TINFOIL SECURITY из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="129cb-121">Add TINFOIL SECURITY from hello gallery</span></span>
2. <span data-ttu-id="129cb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="129cb-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-hello-gallery"></a><span data-ttu-id="129cb-123">Добавление TINFOIL SECURITY из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="129cb-123">Add TINFOIL SECURITY from hello gallery</span></span>
<span data-ttu-id="129cb-124">tooconfigure hello интеграции TINFOIL SECURITY в Azure AD, вы должны tooadd TINFOIL SECURITY из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="129cb-124">tooconfigure hello integration of TINFOIL SECURITY into Azure AD, you need tooadd TINFOIL SECURITY from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="129cb-125">**tooadd TINFOIL SECURITY из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="129cb-125">**tooadd TINFOIL SECURITY from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="129cb-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="129cb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="129cb-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="129cb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="129cb-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="129cb-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="129cb-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="129cb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="129cb-133">Введите в поле поиска hello **TINFOIL SECURITY**выберите **TINFOIL SECURITY** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="129cb-133">In hello search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Добавление TINFOIL SECURITY из коллекции](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="129cb-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="129cb-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="129cb-136">В этом разделе описана настройка и проверка единого входа Azure AD в TINFOIL SECURITY с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="129cb-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="129cb-137">Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в TINFOIL SECURITY — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="129cb-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TINFOIL SECURITY is tooa user in Azure AD.</span></span> <span data-ttu-id="129cb-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в TINFOIL SECURITY должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="129cb-138">In other words, a link relationship between an Azure AD user and hello related user in TINFOIL SECURITY needs toobe established.</span></span>

<span data-ttu-id="129cb-139">В TINFOIL SECURITY, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="129cb-139">In TINFOIL SECURITY, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="129cb-140">tooconfigure и теста Azure AD единого входа с TINFOIL SECURITY, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="129cb-140">tooconfigure and test Azure AD single sign-on with TINFOIL SECURITY, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="129cb-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="129cb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="129cb-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="129cb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="129cb-143">**[Создание тестового пользователя TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave аналог Саймон Britta в TINFOIL SECURITY, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="129cb-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - toohave a counterpart of Britta Simon in TINFOIL SECURITY that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="129cb-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="129cb-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="129cb-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="129cb-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="129cb-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="129cb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="129cb-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="129cb-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="129cb-148">**tooconfigure Azure AD единого входа с TINFOIL SECURITY, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="129cb-148">**tooconfigure Azure AD single sign-on with TINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="129cb-149">В hello в hello портала Azure **TINFOIL SECURITY** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="129cb-149">In hello Azure portal, on hello **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="129cb-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="129cb-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Вход на основе SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="129cb-153">На hello **TINFOIL безопасности домена и URL-адреса** статьи, hello пользователь не имеет tooperform все меры как приложение hello уже заранее интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="129cb-153">On hello **TINFOIL SECURITY Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="129cb-155">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение.</span><span class="sxs-lookup"><span data-stu-id="129cb-155">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value.</span></span>

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="129cb-157">сопоставления атрибутов hello необходимые tooadd, выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="129cb-157">tooadd hello required attribute mappings, perform hello following steps:</span></span>
    
    <span data-ttu-id="129cb-158">![Атрибуты](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="129cb-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="129cb-159">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="129cb-159">Attribute Name</span></span>    |   <span data-ttu-id="129cb-160">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="129cb-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="129cb-161">accountid</span><span class="sxs-lookup"><span data-stu-id="129cb-161">accountid</span></span> | <span data-ttu-id="129cb-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="129cb-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="129cb-163">а.</span><span class="sxs-lookup"><span data-stu-id="129cb-163">a.</span></span> <span data-ttu-id="129cb-164">Щелкните **добавить атрибут пользователя**.</span><span class="sxs-lookup"><span data-stu-id="129cb-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="129cb-165">![Добавление атрибута](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="129cb-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="129cb-166">![Добавление атрибута](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="129cb-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="129cb-167">b.</span><span class="sxs-lookup"><span data-stu-id="129cb-167">b.</span></span> <span data-ttu-id="129cb-168">В hello **имя атрибута** введите **accountid**.</span><span class="sxs-lookup"><span data-stu-id="129cb-168">In hello **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="129cb-169">c.</span><span class="sxs-lookup"><span data-stu-id="129cb-169">c.</span></span> <span data-ttu-id="129cb-170">В hello **значение атрибута** текстовое значение идентификатора учетной записи hello вставить которого вы получите позднее hello учебника.</span><span class="sxs-lookup"><span data-stu-id="129cb-170">In hello **Attribute Value** textbox, paste hello account ID value which you will get later on hello tutorial.</span></span>
    
    <span data-ttu-id="129cb-171">d.</span><span class="sxs-lookup"><span data-stu-id="129cb-171">d.</span></span> <span data-ttu-id="129cb-172">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="129cb-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="129cb-173">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="129cb-173">Click **Save** button.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="129cb-175">На hello **конфигурация безопасности TINFOIL** щелкните **Настройка TINFOIL SECURITY** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="129cb-175">On hello **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="129cb-176">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="129cb-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="129cb-178">В другом окне веб-браузера войдите на свой корпоративный веб-сайт TINFOIL SECURITY в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="129cb-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="129cb-179">Щелкните hello панели инструментов в верхней части hello **Моя учетная запись**.</span><span class="sxs-lookup"><span data-stu-id="129cb-179">In hello toolbar on hello top, click **My Account**.</span></span>
   
    <span data-ttu-id="129cb-180">![Панель мониторинга](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Панель мониторинга")</span><span class="sxs-lookup"><span data-stu-id="129cb-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="129cb-181">Выберите пункт **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="129cb-181">Click **Security**.</span></span>
   
    <span data-ttu-id="129cb-182">![Безопасность](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="129cb-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="129cb-183">На hello **Single Sign-On** конфигурации выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="129cb-183">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="129cb-184">![Единый вход](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="129cb-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="129cb-185">а.</span><span class="sxs-lookup"><span data-stu-id="129cb-185">a.</span></span> <span data-ttu-id="129cb-186">Выберите **Включить SAML**.</span><span class="sxs-lookup"><span data-stu-id="129cb-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="129cb-187">b.</span><span class="sxs-lookup"><span data-stu-id="129cb-187">b.</span></span> <span data-ttu-id="129cb-188">Щелкните **Настроить вручную**.</span><span class="sxs-lookup"><span data-stu-id="129cb-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="129cb-189">c.</span><span class="sxs-lookup"><span data-stu-id="129cb-189">c.</span></span> <span data-ttu-id="129cb-190">В **URL-адрес Post для SAML** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure</span><span class="sxs-lookup"><span data-stu-id="129cb-190">In **SAML Post URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="129cb-191">d.</span><span class="sxs-lookup"><span data-stu-id="129cb-191">d.</span></span> <span data-ttu-id="129cb-192">В **отпечаток сертификата SAML** текстовое значение hello вставить **отпечаток** скопирован из **сертификат подписи SAML** раздела.</span><span class="sxs-lookup"><span data-stu-id="129cb-192">In **SAML Certificate Fingerprint** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="129cb-193">д.</span><span class="sxs-lookup"><span data-stu-id="129cb-193">e.</span></span> <span data-ttu-id="129cb-194">Копировать **свой идентификатор учетной записи** значение и вставьте значение hello в **значение атрибута** текстовое поле под **Добавление атрибута** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="129cb-194">Copy **Your Account ID** value and paste hello value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="129cb-195">f.</span><span class="sxs-lookup"><span data-stu-id="129cb-195">f.</span></span> <span data-ttu-id="129cb-196">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="129cb-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="129cb-197">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="129cb-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="129cb-198">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="129cb-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="129cb-199">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="129cb-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="129cb-200">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="129cb-200">Create an Azure AD test user</span></span>
<span data-ttu-id="129cb-201">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="129cb-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="129cb-203">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="129cb-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="129cb-204">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="129cb-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="129cb-206">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="129cb-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="129cb-207">Выберите "Пользователи и группы" > "Все пользователи".</span><span class="sxs-lookup"><span data-stu-id="129cb-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="129cb-208">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="129cb-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Пользователь](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="129cb-210">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="129cb-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="129cb-212">а.</span><span class="sxs-lookup"><span data-stu-id="129cb-212">a.</span></span> <span data-ttu-id="129cb-213">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="129cb-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="129cb-214">b.</span><span class="sxs-lookup"><span data-stu-id="129cb-214">b.</span></span> <span data-ttu-id="129cb-215">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="129cb-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="129cb-216">c.</span><span class="sxs-lookup"><span data-stu-id="129cb-216">c.</span></span> <span data-ttu-id="129cb-217">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="129cb-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="129cb-218">d.</span><span class="sxs-lookup"><span data-stu-id="129cb-218">d.</span></span> <span data-ttu-id="129cb-219">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="129cb-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="129cb-220">Создание тестового пользователя TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="129cb-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="129cb-221">В порядке tooenable toolog пользователей Azure AD в TINFOIL SECURITY их необходимо подготовить в TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="129cb-221">In order tooenable Azure AD users toolog into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="129cb-222">В случае TINFOIL SECURITY hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="129cb-222">In hello case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="129cb-223">**tooget пользователь подготовлен, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="129cb-223">**tooget a user provisioned, perform hello following steps:**</span></span>

1. <span data-ttu-id="129cb-224">Hello пользователь входит в учетной записи предприятия, требуется слишком[обратитесь в службу поддержки TINFOIL SECURITY hello](https://www.tinfoilsecurity.com/contact) tooget hello Создание учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="129cb-224">If hello user is a part of an Enterprise account, you need too[contact hello TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) tooget hello user account created.</span></span>

2. <span data-ttu-id="129cb-225">Если пользователь hello обычный пользователь TINFOIL SECURITY SaaS, hello пользователя можно добавить участника совместной работы tooany сайтов hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="129cb-225">If hello user is a regular TINFOIL SECURITY SaaS user, then hello user can add a collaborator tooany of hello user’s sites.</span></span> <span data-ttu-id="129cb-226">Этот триггеры toosend процесс, указанный toohello приглашение по электронной почте toocreate новой учетной записи безопасности TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="129cb-226">This triggers a process toosend an invitation toohello specified email toocreate a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="129cb-227">Можно использовать любые другие TINFOIL SECURITY пользователя средства создания учетных записей или API, предоставленные TINFOIL SECURITY tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="129cb-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY tooprovision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="129cb-228">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="129cb-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="129cb-229">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooTINFOIL безопасности.</span><span class="sxs-lookup"><span data-stu-id="129cb-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTINFOIL SECURITY.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="129cb-231">**tooassign tooTINFOIL Britta Simon безопасности, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="129cb-231">**tooassign Britta Simon tooTINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="129cb-232">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="129cb-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="129cb-234">В списке приложений hello выберите **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="129cb-234">In hello applications list, select **TINFOIL SECURITY**.</span></span>

    ![Выбор TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="129cb-236">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="129cb-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="129cb-238">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="129cb-238">Click **Add** button.</span></span> <span data-ttu-id="129cb-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="129cb-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="129cb-241">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="129cb-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="129cb-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="129cb-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="129cb-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="129cb-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="129cb-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="129cb-244">Test single sign-on</span></span>

<span data-ttu-id="129cb-245">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="129cb-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="129cb-246">При выборе плитки TINFOIL SECURITY hello в hello панели доступа, вы должны получить приложение автоматически вошедшего tooyour TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="129cb-246">When you click hello TINFOIL SECURITY tile in hello Access Panel, you should get automatically signed-on tooyour TINFOIL SECURITY application.</span></span> <span data-ttu-id="129cb-247">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="129cb-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="129cb-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="129cb-248">Additional resources</span></span>

* [<span data-ttu-id="129cb-249">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="129cb-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="129cb-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="129cb-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

