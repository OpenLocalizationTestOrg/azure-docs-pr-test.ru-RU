---
title: "Руководство по интеграции Azure Active Directory с RunMyProcess | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и RunMyProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="03c0f-103">Учебник. Интеграция Azure Active Directory с RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="03c0f-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="03c0f-104">В этом учебнике вы узнаете, как toointegrate RunMyProcess с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="03c0f-104">In this tutorial, you learn how toointegrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="03c0f-105">Интеграция RunMyProcess с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="03c0f-105">Integrating RunMyProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="03c0f-106">Можно управлять в Azure AD, имеющего доступ tooRunMyProcess</span><span class="sxs-lookup"><span data-stu-id="03c0f-106">You can control in Azure AD who has access tooRunMyProcess</span></span>
- <span data-ttu-id="03c0f-107">Можно включить на пользователей tooautomatically get вошедшего tooRunMyProcess (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="03c0f-107">You can enable your users tooautomatically get signed-on tooRunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="03c0f-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="03c0f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="03c0f-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="03c0f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03c0f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="03c0f-110">Prerequisites</span></span>

<span data-ttu-id="03c0f-111">tooconfigure интеграция Azure AD с RunMyProcess требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="03c0f-111">tooconfigure Azure AD integration with RunMyProcess, you need hello following items:</span></span>

- <span data-ttu-id="03c0f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="03c0f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="03c0f-113">подписка RunMyProcess с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="03c0f-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03c0f-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="03c0f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="03c0f-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="03c0f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="03c0f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="03c0f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="03c0f-117">Если у вас нет пробной версии среды Azure AD, вы можете получить бесплатную пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03c0f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="03c0f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="03c0f-118">Scenario description</span></span>
<span data-ttu-id="03c0f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="03c0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="03c0f-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="03c0f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="03c0f-121">Добавление RunMyProcess из галереи hello</span><span class="sxs-lookup"><span data-stu-id="03c0f-121">Adding RunMyProcess from hello gallery</span></span>
2. <span data-ttu-id="03c0f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="03c0f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-hello-gallery"></a><span data-ttu-id="03c0f-123">Добавление RunMyProcess из галереи hello</span><span class="sxs-lookup"><span data-stu-id="03c0f-123">Adding RunMyProcess from hello gallery</span></span>
<span data-ttu-id="03c0f-124">tooconfigure hello интеграции RunMyProcess в Azure AD, вы должны tooadd RunMyProcess из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="03c0f-124">tooconfigure hello integration of RunMyProcess into Azure AD, you need tooadd RunMyProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="03c0f-125">**tooadd RunMyProcess из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="03c0f-125">**tooadd RunMyProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="03c0f-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="03c0f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="03c0f-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="03c0f-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="03c0f-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="03c0f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="03c0f-133">Введите в поле поиска hello **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-133">In hello search box, type **RunMyProcess**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="03c0f-135">В панели результатов hello выберите **RunMyProcess**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="03c0f-135">In hello results panel, select **RunMyProcess**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="03c0f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="03c0f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="03c0f-138">В этом разделе описана настройка и проверка единого входа Azure AD в RunMyProcess с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03c0f-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="03c0f-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в RunMyProcess является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03c0f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RunMyProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="03c0f-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в RunMyProcess должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="03c0f-140">In other words, a link relationship between an Azure AD user and hello related user in RunMyProcess needs toobe established.</span></span>

<span data-ttu-id="03c0f-141">В RunMyProcess, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="03c0f-141">In RunMyProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="03c0f-142">tooconfigure и теста Azure AD единого входа с RunMyProcess, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="03c0f-142">tooconfigure and test Azure AD single sign-on with RunMyProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="03c0f-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="03c0f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="03c0f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="03c0f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="03c0f-145">**[Создание тестового пользователя RunMyProcess](#creating-a-runmyprocess-test-user)**  -toohave аналог Саймон Britta в RunMyProcess, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="03c0f-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - toohave a counterpart of Britta Simon in RunMyProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="03c0f-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="03c0f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="03c0f-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="03c0f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="03c0f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="03c0f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="03c0f-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="03c0f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="03c0f-150">**Azure AD tooconfigure единого входа с RunMyProcess, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="03c0f-150">**tooconfigure Azure AD single sign-on with RunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="03c0f-151">В hello в hello портала Azure **RunMyProcess** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-151">In hello Azure portal, on hello **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="03c0f-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="03c0f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="03c0f-155">На hello **URL-адреса и домена RunMyProcess** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="03c0f-155">On hello **RunMyProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="03c0f-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="03c0f-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="03c0f-158">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="03c0f-158">hello value is not real.</span></span> <span data-ttu-id="03c0f-159">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="03c0f-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="03c0f-160">Обратитесь к [группа поддержки клиент RunMyProcess](mailto:support@runmyprocess.com) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="03c0f-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) tooget hello value.</span></span> 

4. <span data-ttu-id="03c0f-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="03c0f-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="03c0f-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="03c0f-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="03c0f-165">На hello **конфигурации RunMyProcess** щелкните **Настройка RunMyProcess** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="03c0f-165">On hello **RunMyProcess Configuration** section, click **Configure RunMyProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="03c0f-166">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="03c0f-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="03c0f-168">В другом окне браузера, клиент RunMyProcess tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="03c0f-168">In a different web browser window, sign-on tooyour RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="03c0f-169">На панели навигации слева щелкните **Учетная запись** и выберите **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="03c0f-171">Go слишком**метод проверки подлинности** раздел и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="03c0f-171">Go too**Authentication method** section and perform below steps:</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="03c0f-173">а.</span><span class="sxs-lookup"><span data-stu-id="03c0f-173">a.</span></span> <span data-ttu-id="03c0f-174">Для параметра **Method** (Метод) выберите значение **SSO with Samlv2** (Единый вход с помощью SAML версии 2).</span><span class="sxs-lookup"><span data-stu-id="03c0f-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="03c0f-175">b.</span><span class="sxs-lookup"><span data-stu-id="03c0f-175">b.</span></span> <span data-ttu-id="03c0f-176">В hello **перенаправления единого входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="03c0f-176">In hello **SSO redirect** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="03c0f-177">c.</span><span class="sxs-lookup"><span data-stu-id="03c0f-177">c.</span></span> <span data-ttu-id="03c0f-178">В hello **перенаправления выхода** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="03c0f-178">In hello **Logout redirect** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="03c0f-179">d.</span><span class="sxs-lookup"><span data-stu-id="03c0f-179">d.</span></span> <span data-ttu-id="03c0f-180">В hello **формат идентификатора имени** текстовое поле, значение типа hello **формат идентификатора имени** как **urn: oasis: имена: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-180">In hello **Name Id Format** textbox, type hello value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="03c0f-181">д.</span><span class="sxs-lookup"><span data-stu-id="03c0f-181">e.</span></span> <span data-ttu-id="03c0f-182">Скопируйте содержимое hello файла hello загруженного сертификата и вставьте его в hello **сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="03c0f-182">Copy hello content of hello downloaded certificate file and then paste it into hello **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="03c0f-183">f.</span><span class="sxs-lookup"><span data-stu-id="03c0f-183">f.</span></span> <span data-ttu-id="03c0f-184">Щелкните значок **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="03c0f-185">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="03c0f-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="03c0f-186">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="03c0f-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="03c0f-187">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="03c0f-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="03c0f-188">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="03c0f-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="03c0f-189">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="03c0f-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="03c0f-191">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="03c0f-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="03c0f-192">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="03c0f-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="03c0f-194">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="03c0f-196">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="03c0f-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="03c0f-198">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="03c0f-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="03c0f-200">а.</span><span class="sxs-lookup"><span data-stu-id="03c0f-200">a.</span></span> <span data-ttu-id="03c0f-201">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="03c0f-202">b.</span><span class="sxs-lookup"><span data-stu-id="03c0f-202">b.</span></span> <span data-ttu-id="03c0f-203">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="03c0f-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="03c0f-204">c.</span><span class="sxs-lookup"><span data-stu-id="03c0f-204">c.</span></span> <span data-ttu-id="03c0f-205">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="03c0f-206">d.</span><span class="sxs-lookup"><span data-stu-id="03c0f-206">d.</span></span> <span data-ttu-id="03c0f-207">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="03c0f-208">Создание тестового пользователя RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="03c0f-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="03c0f-209">В порядке tooenable toolog пользователей Azure AD в tooRunMyProcess их необходимо подготовить в RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="03c0f-209">In order tooenable Azure AD users toolog in tooRunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="03c0f-210">В случае hello объекта RunMyProcess Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="03c0f-210">In hello case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="03c0f-211">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="03c0f-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="03c0f-212">Войдите в tooyour корпоративный сайт RunMyProcess с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="03c0f-212">Log in tooyour RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="03c0f-213">Щелкните **Учетная запись** и выберите **Пользователи** на левой панели навигации. Затем нажмите кнопку **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="03c0f-214">![Новый пользователь](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="03c0f-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="03c0f-215">В hello **параметры пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="03c0f-215">In hello **User Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="03c0f-216">![Профиль](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Профиль")</span><span class="sxs-lookup"><span data-stu-id="03c0f-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="03c0f-217">а.</span><span class="sxs-lookup"><span data-stu-id="03c0f-217">a.</span></span> <span data-ttu-id="03c0f-218">Тип hello **имя** и **электронной почты** из допустимых Azure текстовые поля, связанные с учетной записью AD, которые должны tooprovision hello.</span><span class="sxs-lookup"><span data-stu-id="03c0f-218">Type hello **Name** and **E-mail** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="03c0f-219">b.</span><span class="sxs-lookup"><span data-stu-id="03c0f-219">b.</span></span> <span data-ttu-id="03c0f-220">Выберите значения параметров **IDE language** (Язык интегрированной среды разработки), **Language** (Язык) и **Profile** (Профиль).</span><span class="sxs-lookup"><span data-stu-id="03c0f-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="03c0f-221">c.</span><span class="sxs-lookup"><span data-stu-id="03c0f-221">c.</span></span> <span data-ttu-id="03c0f-222">Выберите **отправки toome электронной почты для создания учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-222">Select **Send account creation e-mail toome**.</span></span> 

    <span data-ttu-id="03c0f-223">d.</span><span class="sxs-lookup"><span data-stu-id="03c0f-223">d.</span></span> <span data-ttu-id="03c0f-224">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="03c0f-225">Можно использовать любые другие RunMyProcess пользователя средства создания учетных записей или API, предоставленные RunMyProcess tooprovision Azure Active Directory учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="03c0f-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess tooprovision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="03c0f-226">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="03c0f-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="03c0f-227">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooRunMyProcess доступа.</span><span class="sxs-lookup"><span data-stu-id="03c0f-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRunMyProcess.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="03c0f-229">**tooassign tooRunMyProcess Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="03c0f-229">**tooassign Britta Simon tooRunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="03c0f-230">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="03c0f-232">В списке приложений hello выберите **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-232">In hello applications list, select **RunMyProcess**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="03c0f-234">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="03c0f-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-236">Click **Add** button.</span></span> <span data-ttu-id="03c0f-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="03c0f-239">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="03c0f-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="03c0f-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="03c0f-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="03c0f-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="03c0f-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="03c0f-242">Testing single sign-on</span></span>

<span data-ttu-id="03c0f-243">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="03c0f-243">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="03c0f-244">При нажатии кнопки RunMyProcess плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour RunMyProcess приложения.</span><span class="sxs-lookup"><span data-stu-id="03c0f-244">When you click hello RunMyProcess tile in hello Access Panel, you should get automatically signed-on tooyour RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="03c0f-245">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="03c0f-245">Additional resources</span></span>

* [<span data-ttu-id="03c0f-246">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03c0f-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="03c0f-247">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="03c0f-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

