---
title: "Руководство. Интеграция Azure Active Directory с Workfront | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Workfront."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: e7249b9ec769f19cf5aa7d44ff6f58705df4020a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="73841-103">Руководство. Интеграция Azure Active Directory с Workfront</span><span class="sxs-lookup"><span data-stu-id="73841-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="73841-104">В этом учебнике вы узнаете, как toointegrate Workfront с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73841-104">In this tutorial, you learn how toointegrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73841-105">Интеграция с Azure AD Workfront предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="73841-105">Integrating Workfront with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="73841-106">Можно управлять в Azure AD, имеющего доступ tooWorkfront</span><span class="sxs-lookup"><span data-stu-id="73841-106">You can control in Azure AD who has access tooWorkfront</span></span>
- <span data-ttu-id="73841-107">Можно включить на пользователей tooautomatically get вошедшего tooWorkfront (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="73841-107">You can enable your users tooautomatically get signed-on tooWorkfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73841-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="73841-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="73841-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73841-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73841-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="73841-110">Prerequisites</span></span>

<span data-ttu-id="73841-111">tooconfigure интеграция Azure AD с Workfront требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="73841-111">tooconfigure Azure AD integration with Workfront, you need hello following items:</span></span>

- <span data-ttu-id="73841-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="73841-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73841-113">подписка Workfront с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="73841-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73841-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="73841-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73841-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="73841-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73841-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="73841-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73841-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73841-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73841-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="73841-118">Scenario description</span></span>
<span data-ttu-id="73841-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="73841-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73841-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="73841-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73841-121">Добавление Workfront из галереи hello</span><span class="sxs-lookup"><span data-stu-id="73841-121">Adding Workfront from hello gallery</span></span>
2. <span data-ttu-id="73841-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="73841-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-hello-gallery"></a><span data-ttu-id="73841-123">Добавление Workfront из галереи hello</span><span class="sxs-lookup"><span data-stu-id="73841-123">Adding Workfront from hello gallery</span></span>
<span data-ttu-id="73841-124">tooconfigure hello интеграции Workfront в Azure AD, вы должны tooadd Workfront из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="73841-124">tooconfigure hello integration of Workfront into Azure AD, you need tooadd Workfront from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="73841-125">**tooadd Workfront из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73841-125">**tooadd Workfront from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="73841-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="73841-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="73841-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="73841-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="73841-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="73841-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="73841-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="73841-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="73841-133">Введите в поле поиска hello **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="73841-133">In hello search box, type **Workfront**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="73841-135">В панели результатов hello выберите **Workfront**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="73841-135">In hello results panel, select **Workfront**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73841-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="73841-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="73841-138">В этом разделе описана настройка и проверка единого входа Azure AD в Workfront с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73841-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="73841-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Workfront является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73841-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workfront is tooa user in Azure AD.</span></span> <span data-ttu-id="73841-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Workfront должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="73841-140">In other words, a link relationship between an Azure AD user and hello related user in Workfront needs toobe established.</span></span>

<span data-ttu-id="73841-141">В Workfront, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="73841-141">In Workfront, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="73841-142">tooconfigure и теста Azure AD единого входа с Workfront, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="73841-142">tooconfigure and test Azure AD single sign-on with Workfront, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="73841-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="73841-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="73841-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="73841-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73841-145">**[Создание тестового пользователя Workfront](#creating-a-workfront-test-user)**  -toohave аналог Саймон Britta в Workfront, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="73841-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - toohave a counterpart of Britta Simon in Workfront that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="73841-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="73841-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73841-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="73841-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73841-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="73841-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73841-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Workfront.</span><span class="sxs-lookup"><span data-stu-id="73841-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="73841-150">**tooconfigure Azure AD единого входа с Workfront, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73841-150">**tooconfigure Azure AD single sign-on with Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="73841-151">В hello в hello портала Azure **Workfront** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="73841-151">In hello Azure portal, on hello **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="73841-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="73841-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="73841-155">На hello **URL-адреса и домена Workfront** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="73841-155">On hello **Workfront Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="73841-157">а.</span><span class="sxs-lookup"><span data-stu-id="73841-157">a.</span></span> <span data-ttu-id="73841-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="73841-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="73841-159">b.</span><span class="sxs-lookup"><span data-stu-id="73841-159">b.</span></span> <span data-ttu-id="73841-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="73841-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73841-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="73841-161">These values are not real.</span></span> <span data-ttu-id="73841-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="73841-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="73841-163">Обратитесь к [группа поддержки клиента Workfront](https://www.workfront.com/contact-us/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="73841-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="73841-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="73841-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="73841-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="73841-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73841-168">На hello **конфигурации Workfront** щелкните **Настройка Workfront** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="73841-168">On hello **Workfront Configuration** section, click **Configure Workfront** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="73841-169">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="73841-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="73841-171">Корпоративный сайт Workfront tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="73841-171">Sign-on tooyour Workfront company site as administrator.</span></span>

8. <span data-ttu-id="73841-172">Go слишком**единого входа на конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="73841-172">Go too**Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="73841-173">На hello **Single Sign-On** диалоговое окно, выполните следующие шаги hello</span><span class="sxs-lookup"><span data-stu-id="73841-173">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
    
    ![Настройка единого входа][23]
   
    <span data-ttu-id="73841-175">а.</span><span class="sxs-lookup"><span data-stu-id="73841-175">a.</span></span> <span data-ttu-id="73841-176">Для параметра **Тип** выберите значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="73841-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="73841-177">b.</span><span class="sxs-lookup"><span data-stu-id="73841-177">b.</span></span> <span data-ttu-id="73841-178">Выберите **идентификатор поставщика службы**.</span><span class="sxs-lookup"><span data-stu-id="73841-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="73841-179">c.</span><span class="sxs-lookup"><span data-stu-id="73841-179">c.</span></span> <span data-ttu-id="73841-180">Вставить hello **SAML единого входа URL-адрес службы** в hello **URL-адрес входа портала** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="73841-180">Paste hello **SAML Single Sign-On Service URL** into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="73841-181">d.</span><span class="sxs-lookup"><span data-stu-id="73841-181">d.</span></span> <span data-ttu-id="73841-182">Вставить **URL-адрес службы единого выхода** в hello **URL-адрес выхода** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="73841-182">Paste **Single Sign-Out Service URL** into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="73841-183">д.</span><span class="sxs-lookup"><span data-stu-id="73841-183">e.</span></span> <span data-ttu-id="73841-184">Вставить **URL-адрес изменения пароля** в hello **URL-адрес изменения пароля** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="73841-184">Paste **Change Password URL** into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="73841-185">f.</span><span class="sxs-lookup"><span data-stu-id="73841-185">f.</span></span> <span data-ttu-id="73841-186">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="73841-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="73841-187">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="73841-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="73841-188">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="73841-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="73841-189">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73841-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73841-190">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="73841-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="73841-191">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="73841-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="73841-193">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73841-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="73841-194">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="73841-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73841-196">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="73841-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73841-198">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="73841-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73841-200">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="73841-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73841-202">а.</span><span class="sxs-lookup"><span data-stu-id="73841-202">a.</span></span> <span data-ttu-id="73841-203">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73841-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73841-204">b.</span><span class="sxs-lookup"><span data-stu-id="73841-204">b.</span></span> <span data-ttu-id="73841-205">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="73841-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73841-206">c.</span><span class="sxs-lookup"><span data-stu-id="73841-206">c.</span></span> <span data-ttu-id="73841-207">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="73841-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="73841-208">d.</span><span class="sxs-lookup"><span data-stu-id="73841-208">d.</span></span> <span data-ttu-id="73841-209">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="73841-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="73841-210">Создание тестового пользователя Workfront</span><span class="sxs-lookup"><span data-stu-id="73841-210">Creating a Workfront test user</span></span>

<span data-ttu-id="73841-211">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Workfront.</span><span class="sxs-lookup"><span data-stu-id="73841-211">hello objective of this section is toocreate a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="73841-212">**toocreate пользователя с именем Саймон Britta в Workfront, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73841-212">**toocreate a user called Britta Simon in Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="73841-213">Войдите на tooyour Workfront сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="73841-213">Sign on tooyour Workfront company site as administrator.</span></span>
2. <span data-ttu-id="73841-214">В меню в верхней части hello hello выберите **людей**.</span><span class="sxs-lookup"><span data-stu-id="73841-214">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="73841-215">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="73841-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="73841-216">В диалоговом окне Новый пользователь hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="73841-216">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Workfront][21] 
   
    <span data-ttu-id="73841-218">а.</span><span class="sxs-lookup"><span data-stu-id="73841-218">a.</span></span> <span data-ttu-id="73841-219">В hello **имя** текстовое поле, введите «Britta».</span><span class="sxs-lookup"><span data-stu-id="73841-219">In hello **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="73841-220">b.</span><span class="sxs-lookup"><span data-stu-id="73841-220">b.</span></span> <span data-ttu-id="73841-221">В hello **Фамилия** текстовое поле, введите «Simon».</span><span class="sxs-lookup"><span data-stu-id="73841-221">In hello **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="73841-222">c.</span><span class="sxs-lookup"><span data-stu-id="73841-222">c.</span></span> <span data-ttu-id="73841-223">В hello **адрес электронной почты** текстовом поле введите адрес электронной почты Britta Simon в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="73841-223">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="73841-224">d.</span><span class="sxs-lookup"><span data-stu-id="73841-224">d.</span></span> <span data-ttu-id="73841-225">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="73841-225">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="73841-226">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="73841-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="73841-227">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWorkfront доступа.</span><span class="sxs-lookup"><span data-stu-id="73841-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkfront.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="73841-229">**tooassign tooWorkfront Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73841-229">**tooassign Britta Simon tooWorkfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="73841-230">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="73841-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="73841-232">В списке приложений hello выберите **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="73841-232">In hello applications list, select **Workfront**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="73841-234">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="73841-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="73841-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="73841-236">Click **Add** button.</span></span> <span data-ttu-id="73841-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="73841-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="73841-239">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="73841-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="73841-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="73841-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73841-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="73841-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73841-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="73841-242">Testing single sign-on</span></span>

<span data-ttu-id="73841-243">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="73841-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="73841-244">При нажатии кнопки hello Workfront плитки в панели доступа hello, должно появиться страница входа Workfront приложения.</span><span class="sxs-lookup"><span data-stu-id="73841-244">When you click hello Workfront tile in hello Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="73841-245">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73841-245">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="73841-246">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="73841-246">Additional resources</span></span>

* [<span data-ttu-id="73841-247">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73841-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73841-248">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="73841-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

