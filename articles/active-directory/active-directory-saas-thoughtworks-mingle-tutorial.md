---
title: "Руководство по интеграции Azure Active Directory с Thoughtworks Mingle | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="9ac6a-103">Учебник. Интеграция Azure Active Directory с Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="9ac6a-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="9ac6a-104">В этом учебнике вы узнаете, как toointegrate Thoughtworks Mingle с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9ac6a-104">In this tutorial, you learn how toointegrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ac6a-105">Интеграция Thoughtworks Mingle с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9ac6a-105">Integrating Thoughtworks Mingle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9ac6a-106">Можно управлять в Azure AD, имеющего доступ tooThoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="9ac6a-106">You can control in Azure AD who has access tooThoughtworks Mingle</span></span>
- <span data-ttu-id="9ac6a-107">Можно включить на пользователей tooautomatically get вошедшего tooThoughtworks Mingle (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ac6a-107">You can enable your users tooautomatically get signed-on tooThoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9ac6a-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9ac6a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9ac6a-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ac6a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ac6a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9ac6a-110">Prerequisites</span></span>

<span data-ttu-id="9ac6a-111">tooconfigure интеграция Azure AD с Thoughtworks Mingle требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="9ac6a-111">tooconfigure Azure AD integration with Thoughtworks Mingle, you need hello following items:</span></span>

- <span data-ttu-id="9ac6a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9ac6a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9ac6a-113">подписка Thoughtworks Mingle с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9ac6a-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9ac6a-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="9ac6a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9ac6a-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9ac6a-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ac6a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9ac6a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9ac6a-118">Scenario description</span></span>
<span data-ttu-id="9ac6a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9ac6a-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="9ac6a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ac6a-121">Добавление Thoughtworks Mingle из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9ac6a-121">Adding Thoughtworks Mingle from hello gallery</span></span>
2. <span data-ttu-id="9ac6a-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ac6a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a><span data-ttu-id="9ac6a-123">Добавление Thoughtworks Mingle из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9ac6a-123">Adding Thoughtworks Mingle from hello gallery</span></span>
<span data-ttu-id="9ac6a-124">tooconfigure hello интеграции Thoughtworks Mingle в Azure AD, вы должны tooadd Thoughtworks Mingle из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-124">tooconfigure hello integration of Thoughtworks Mingle into Azure AD, you need tooadd Thoughtworks Mingle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9ac6a-125">**tooadd Thoughtworks Mingle из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9ac6a-125">**tooadd Thoughtworks Mingle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ac6a-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="9ac6a-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9ac6a-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="9ac6a-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="9ac6a-133">Введите в поле поиска hello **Thoughtworks Mingle**выберите **Thoughtworks Mingle** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-133">In hello search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ThoughtWorks Mingle в списке результатов hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9ac6a-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ac6a-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9ac6a-136">В этом разделе описана настройка и проверка единого входа Azure AD в Thoughtworks Mingle с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9ac6a-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Thoughtworks Mingle является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Thoughtworks Mingle is tooa user in Azure AD.</span></span> <span data-ttu-id="9ac6a-138">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Thoughtworks Mingle должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-138">In other words, a link relationship between an Azure AD user and hello related user in Thoughtworks Mingle needs toobe established.</span></span>

<span data-ttu-id="9ac6a-139">В Thoughtworks Mingle, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-139">In Thoughtworks Mingle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9ac6a-140">tooconfigure и теста Azure AD единого входа с Thoughtworks Mingle, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9ac6a-140">tooconfigure and test Azure AD single sign-on with Thoughtworks Mingle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9ac6a-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9ac6a-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ac6a-143">**[Создание тестового пользователя Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**  -toohave аналог Саймон Britta в Thoughtworks Mingle, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - toohave a counterpart of Britta Simon in Thoughtworks Mingle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9ac6a-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ac6a-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9ac6a-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ac6a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9ac6a-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="9ac6a-148">**tooconfigure Azure AD единого входа с Thoughtworks Mingle, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9ac6a-148">**tooconfigure Azure AD single sign-on with Thoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ac6a-149">В hello в hello портала Azure **Thoughtworks Mingle** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-149">In hello Azure portal, on hello **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9ac6a-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="9ac6a-153">На hello **Thoughtworks Mingle доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9ac6a-153">On hello **Thoughtworks Mingle Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="9ac6a-155">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="9ac6a-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9ac6a-156">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-156">hello value is not real.</span></span> <span data-ttu-id="9ac6a-157">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-157">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9ac6a-158">Обратитесь к [Thoughtworks Mingle клиента поддержки](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello value.</span></span> 
 
4. <span data-ttu-id="9ac6a-159">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="9ac6a-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9ac6a-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9ac6a-163">Войдите в tooyour **Thoughtworks Mingle** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-163">Log in tooyour **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="9ac6a-164">Нажмите кнопку hello **администратора** , а затем щелкните **Настройка Единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-164">Click hello **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="9ac6a-165">![Вкладка Admin](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="9ac6a-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="9ac6a-166">В hello **Настройка Единого входа** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9ac6a-166">In hello **SSO Config** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9ac6a-167">![Настройка единого входа](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="9ac6a-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="9ac6a-168">а.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-168">a.</span></span> <span data-ttu-id="9ac6a-169">файл метаданных tooupload hello, нажмите кнопку **выбрать файл**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-169">tooupload hello metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="9ac6a-170">b.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-170">b.</span></span> <span data-ttu-id="9ac6a-171">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="9ac6a-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="9ac6a-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9ac6a-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9ac6a-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9ac6a-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9ac6a-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ac6a-175">Create an Azure AD test user</span></span>
<span data-ttu-id="9ac6a-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="9ac6a-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9ac6a-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ac6a-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9ac6a-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9ac6a-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="9ac6a-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9ac6a-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9ac6a-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9ac6a-187">а.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-187">a.</span></span> <span data-ttu-id="9ac6a-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9ac6a-189">b.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-189">b.</span></span> <span data-ttu-id="9ac6a-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9ac6a-191">c.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-191">c.</span></span> <span data-ttu-id="9ac6a-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9ac6a-193">d.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-193">d.</span></span> <span data-ttu-id="9ac6a-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="9ac6a-195">Создание тестового пользователя Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="9ac6a-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="9ac6a-196">Для Azure AD пользователи toobe может toosign в они должны быть подготовленных toohello Thoughtworks Mingle приложения с использованием своих имен пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-196">For Azure AD users toobe able toosign in, they must be provisioned toohello Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="9ac6a-197">В случае Thoughtworks Mingle hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-197">In hello case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="9ac6a-198">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9ac6a-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ac6a-199">Войдите в систему tooyour сайт Thoughtworks Mingle компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-199">Log in tooyour Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="9ac6a-200">Щелкните **Профиль**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="9ac6a-201">![Ваш первый проект](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Ваш первый проект")</span><span class="sxs-lookup"><span data-stu-id="9ac6a-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="9ac6a-202">Нажмите кнопку hello **администратора** , а затем щелкните **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-202">Click hello **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="9ac6a-203">![Пользователи](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="9ac6a-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="9ac6a-204">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-204">Click **New User**.</span></span>
   
    <span data-ttu-id="9ac6a-205">![Новый пользователь](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="9ac6a-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="9ac6a-206">На hello **нового пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9ac6a-206">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="9ac6a-207">![Диалоговое окно нового пользователя](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="9ac6a-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="9ac6a-208">а.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-208">a.</span></span> <span data-ttu-id="9ac6a-209">Тип hello **учетное имя**, **отображаемое имя**, **выбранные пароль**, **подтверждение пароля** из допустимых Azure требуется tooprovision учетной записи AD в hello связанные текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-209">Type hello **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="9ac6a-210">b.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-210">b.</span></span> <span data-ttu-id="9ac6a-211">В поле **User type** (Тип пользователя) выберите значение **Full user** (С полным доступом).</span><span class="sxs-lookup"><span data-stu-id="9ac6a-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="9ac6a-212">c.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-212">c.</span></span> <span data-ttu-id="9ac6a-213">Щелкните **Создать этот профиль**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="9ac6a-214">Можно использовать любые другие Thoughtworks Mingle пользователя средства создания учетных записей или интерфейсы API, предоставляемые Thoughtworks Mingle tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle tooprovision AAD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9ac6a-215">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="9ac6a-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9ac6a-216">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooThoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThoughtworks Mingle.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="9ac6a-218">**tooassign Britta Simon tooThoughtworks Mingle, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9ac6a-218">**tooassign Britta Simon tooThoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ac6a-219">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9ac6a-221">В списке приложений hello выберите **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-221">In hello applications list, select **Thoughtworks Mingle**.</span></span>

    ![Hello Thoughtworks Mingle ссылку в списке приложений hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="9ac6a-223">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202] 

4. <span data-ttu-id="9ac6a-225">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-225">Click **Add** button.</span></span> <span data-ttu-id="9ac6a-226">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="9ac6a-228">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9ac6a-229">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9ac6a-230">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9ac6a-231">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9ac6a-231">Test single sign-on</span></span>

<span data-ttu-id="9ac6a-232">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="9ac6a-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9ac6a-233">При нажатии кнопки hello Thoughtworks Mingle плитки в панели доступа hello, вы должны получить tooyour автоматически подписью в приложении Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="9ac6a-233">When you click hello Thoughtworks Mingle tile in hello Access Panel, you should get automatically signed-on tooyour Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ac6a-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9ac6a-234">Additional resources</span></span>

* [<span data-ttu-id="9ac6a-235">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ac6a-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ac6a-236">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9ac6a-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

