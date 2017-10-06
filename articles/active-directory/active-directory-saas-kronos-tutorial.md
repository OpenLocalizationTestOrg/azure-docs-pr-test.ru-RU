---
title: "Учебник. Интеграция Azure Active Directory с Kronos | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Kronos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 16fd5c203162d10b78f51b00d79017adaf8632c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="68347-103">Учебник. Интеграция Azure Active Directory с Kronos</span><span class="sxs-lookup"><span data-stu-id="68347-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="68347-104">В этом учебнике вы узнаете, как toointegrate Kronos с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="68347-104">In this tutorial, you learn how toointegrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68347-105">Интеграция с Azure AD Kronos предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="68347-105">Integrating Kronos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="68347-106">Можно управлять в Azure AD, имеющего доступ tooKronos</span><span class="sxs-lookup"><span data-stu-id="68347-106">You can control in Azure AD who has access tooKronos</span></span>
- <span data-ttu-id="68347-107">Можно включить на пользователей tooautomatically get вошедшего tooKronos (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="68347-107">You can enable your users tooautomatically get signed-on tooKronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68347-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="68347-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="68347-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="68347-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68347-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="68347-110">Prerequisites</span></span>

<span data-ttu-id="68347-111">tooconfigure интеграция Azure AD с Kronos требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="68347-111">tooconfigure Azure AD integration with Kronos, you need hello following items:</span></span>

- <span data-ttu-id="68347-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="68347-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68347-113">подписка **Kronos Workforce Central** с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="68347-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68347-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="68347-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68347-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="68347-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68347-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="68347-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68347-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68347-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68347-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="68347-118">Scenario description</span></span>
<span data-ttu-id="68347-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="68347-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68347-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="68347-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68347-121">Добавление Kronos из галереи hello</span><span class="sxs-lookup"><span data-stu-id="68347-121">Adding Kronos from hello gallery</span></span>
2. <span data-ttu-id="68347-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="68347-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-hello-gallery"></a><span data-ttu-id="68347-123">Добавление Kronos из галереи hello</span><span class="sxs-lookup"><span data-stu-id="68347-123">Adding Kronos from hello gallery</span></span>
<span data-ttu-id="68347-124">tooconfigure hello интеграции Kronos в Azure AD, вы должны tooadd Kronos из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="68347-124">tooconfigure hello integration of Kronos into Azure AD, you need tooadd Kronos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="68347-125">**tooadd Kronos из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="68347-125">**tooadd Kronos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="68347-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="68347-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="68347-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="68347-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="68347-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="68347-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="68347-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="68347-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="68347-133">Введите в поле поиска hello **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="68347-133">In hello search box, type **Kronos**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="68347-135">В панели результатов hello выберите **Kronos**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="68347-135">In hello results panel, select **Kronos**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="68347-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="68347-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="68347-138">В этом разделе описана настройка и проверка единого входа Azure AD в Kronos с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68347-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="68347-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Kronos является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68347-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kronos is tooa user in Azure AD.</span></span> <span data-ttu-id="68347-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Kronos должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="68347-140">In other words, a link relationship between an Azure AD user and hello related user in Kronos needs toobe established.</span></span>

<span data-ttu-id="68347-141">В Kronos, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="68347-141">In Kronos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="68347-142">tooconfigure и теста Azure AD единого входа с Kronos, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="68347-142">tooconfigure and test Azure AD single sign-on with Kronos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="68347-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="68347-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="68347-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="68347-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68347-145">**[Создание тестового пользователя Kronos](#creating-a-kronos-test-user)**  -toohave аналог Саймон Britta в Kronos, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="68347-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - toohave a counterpart of Britta Simon in Kronos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="68347-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="68347-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68347-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="68347-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="68347-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="68347-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="68347-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Kronos.</span><span class="sxs-lookup"><span data-stu-id="68347-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="68347-150">**tooconfigure Azure AD единого входа с Kronos, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="68347-150">**tooconfigure Azure AD single sign-on with Kronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="68347-151">В hello в hello портала Azure **Kronos** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="68347-151">In hello Azure portal, on hello **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="68347-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="68347-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="68347-155">На hello **URL-адреса и домена Kronos** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="68347-155">On hello **Kronos Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="68347-157">а.</span><span class="sxs-lookup"><span data-stu-id="68347-157">a.</span></span> <span data-ttu-id="68347-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="68347-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="68347-159">b.</span><span class="sxs-lookup"><span data-stu-id="68347-159">b.</span></span> <span data-ttu-id="68347-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="68347-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="68347-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="68347-161">These values are not real.</span></span> <span data-ttu-id="68347-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="68347-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="68347-163">Обратитесь к [Kronos поддержки](https://www.kronos.in/contact/en-in/form) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="68347-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) tooget these values.</span></span>
 
4. <span data-ttu-id="68347-164">Приложение Kronos ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="68347-164">Your Kronos application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="68347-165">Работать с [Kronos поддержки](https://www.kronos.in/contact/en-in/form) первый идентификатор пользователя hello tooidentify, назначенная в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="68347-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first tooidentify hello correct user identifier, which is mapped into hello application.</span></span> <span data-ttu-id="68347-166">Также предпримите hello обоснования hello атрибут, который хочет toouse для данного сопоставления.</span><span class="sxs-lookup"><span data-stu-id="68347-166">Also please take hello guidance about hello attribute, which they want toouse for this mapping.</span></span>
 
     <span data-ttu-id="68347-167">Корпорация Майкрософт рекомендует использовать hello **«NameIdentifier»** атрибут в качестве идентификатора пользователя.</span><span class="sxs-lookup"><span data-stu-id="68347-167">Microsoft recommends using hello **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="68347-168">Вы можете управлять hello значения этих атрибутов из hello **«Атрибуты пользователя»** раздел на странице интеграции приложений.</span><span class="sxs-lookup"><span data-stu-id="68347-168">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="68347-169">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="68347-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="68347-170">Здесь мы сопоставленной hello **идентификатор пользователя (nameid)** с **ExtractMailPrefix()** функция **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="68347-170">Here we have mapped hello **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="68347-171">Это дает значение hello префикс адреса электронной почты пользователя hello, что является hello уникальный ИД пользователя.</span><span class="sxs-lookup"><span data-stu-id="68347-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="68347-172">Это число отправляется приложения Kronos toohello в каждом успешного ответа.</span><span class="sxs-lookup"><span data-stu-id="68347-172">This is sent toohello Kronos application in every successful response.</span></span> 
     
    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="68347-174">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна:</span><span class="sxs-lookup"><span data-stu-id="68347-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="68347-175">а.</span><span class="sxs-lookup"><span data-stu-id="68347-175">a.</span></span> <span data-ttu-id="68347-176">В раскрывающемся списке hello идентификатор пользователя, выберите **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="68347-176">In hello User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="68347-177">b.</span><span class="sxs-lookup"><span data-stu-id="68347-177">b.</span></span> <span data-ttu-id="68347-178">В hello **Mail** раскрывающегося списка выберите **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="68347-178">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="68347-179">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="68347-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="68347-181">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="68347-181">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="68347-183">tooconfigure единого входа на **Kronos** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Kronos поддержки](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="68347-183">tooconfigure single sign-on on **Kronos** side, you need toosend hello downloaded **Metadata XML** too[Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="68347-184">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="68347-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="68347-185">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="68347-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="68347-186">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68347-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="68347-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="68347-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="68347-188">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="68347-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="68347-190">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="68347-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="68347-191">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="68347-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68347-193">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="68347-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68347-195">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="68347-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68347-197">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="68347-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68347-199">а.</span><span class="sxs-lookup"><span data-stu-id="68347-199">a.</span></span> <span data-ttu-id="68347-200">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="68347-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68347-201">b.</span><span class="sxs-lookup"><span data-stu-id="68347-201">b.</span></span> <span data-ttu-id="68347-202">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="68347-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68347-203">c.</span><span class="sxs-lookup"><span data-stu-id="68347-203">c.</span></span> <span data-ttu-id="68347-204">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="68347-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="68347-205">d.</span><span class="sxs-lookup"><span data-stu-id="68347-205">d.</span></span> <span data-ttu-id="68347-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="68347-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="68347-207">Создание тестового пользователя Kronos</span><span class="sxs-lookup"><span data-stu-id="68347-207">Creating a Kronos test user</span></span>

<span data-ttu-id="68347-208">В этом разделе описано, как создать пользователя Britta Simon в приложении Kronos.</span><span class="sxs-lookup"><span data-stu-id="68347-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="68347-209">Kronos приложению все пользователи toobe hello, подготовить в приложении hello перед выполнением единого входа.</span><span class="sxs-lookup"><span data-stu-id="68347-209">Kronos application needs all hello users toobe provisioned in hello application before doing SSO.</span></span> 

<span data-ttu-id="68347-210">Работать с hello [Kronos поддержки](https://www.kronos.in/contact/en-in/form) tooprovision этих пользователей в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="68347-210">Work with hello [Kronos support team](https://www.kronos.in/contact/en-in/form) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="68347-211">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="68347-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="68347-212">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooKronos доступа.</span><span class="sxs-lookup"><span data-stu-id="68347-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKronos.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="68347-214">**tooassign tooKronos Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="68347-214">**tooassign Britta Simon tooKronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="68347-215">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="68347-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="68347-217">В списке приложений hello выберите **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="68347-217">In hello applications list, select **Kronos**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="68347-219">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="68347-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="68347-221">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="68347-221">Click **Add** button.</span></span> <span data-ttu-id="68347-222">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="68347-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="68347-224">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="68347-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="68347-225">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="68347-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68347-226">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="68347-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="68347-227">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="68347-227">Testing single sign-on</span></span>

<span data-ttu-id="68347-228">В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="68347-228">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="68347-229">При нажатии кнопки Kronos плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Kronos приложения.</span><span class="sxs-lookup"><span data-stu-id="68347-229">When you click hello Kronos tile in hello Access Panel, you should get automatically signed-on tooyour Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68347-230">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="68347-230">Additional resources</span></span>

* [<span data-ttu-id="68347-231">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68347-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68347-232">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="68347-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

