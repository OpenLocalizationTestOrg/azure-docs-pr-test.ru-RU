---
title: "Руководство по интеграции Azure Active Directory с Mixpanel | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Mixpanel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 8da8aaefee3558c37babe3e10aeba4224ceffa16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="7622e-103">Руководство. Интеграция Azure Active Directory с Mixpanel</span><span class="sxs-lookup"><span data-stu-id="7622e-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="7622e-104">В этом учебнике вы узнаете, как toointegrate Mixpanel с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7622e-104">In this tutorial, you learn how toointegrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7622e-105">Интеграция с Azure AD Mixpanel предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7622e-105">Integrating Mixpanel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7622e-106">Можно управлять в Azure AD, имеющего доступ tooMixpanel</span><span class="sxs-lookup"><span data-stu-id="7622e-106">You can control in Azure AD who has access tooMixpanel</span></span>
- <span data-ttu-id="7622e-107">Можно включить на пользователей tooautomatically get вошедшего tooMixpanel (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7622e-107">You can enable your users tooautomatically get signed-on tooMixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7622e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7622e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7622e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7622e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7622e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7622e-110">Prerequisites</span></span>

<span data-ttu-id="7622e-111">tooconfigure интеграция Azure AD с Mixpanel требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7622e-111">tooconfigure Azure AD integration with Mixpanel, you need hello following items:</span></span>

- <span data-ttu-id="7622e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7622e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7622e-113">подписка с поддержкой единого входа Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="7622e-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7622e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7622e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7622e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7622e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7622e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7622e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7622e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7622e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7622e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7622e-118">Scenario description</span></span>
<span data-ttu-id="7622e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7622e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7622e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7622e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7622e-121">Добавление Mixpanel из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7622e-121">Adding Mixpanel from hello gallery</span></span>
2. <span data-ttu-id="7622e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7622e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-hello-gallery"></a><span data-ttu-id="7622e-123">Добавление Mixpanel из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7622e-123">Adding Mixpanel from hello gallery</span></span>
<span data-ttu-id="7622e-124">tooconfigure hello интеграции Mixpanel в Azure AD, вы должны tooadd Mixpanel из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7622e-124">tooconfigure hello integration of Mixpanel into Azure AD, you need tooadd Mixpanel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7622e-125">**tooadd Mixpanel из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7622e-125">**tooadd Mixpanel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7622e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7622e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7622e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="7622e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7622e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7622e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7622e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7622e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7622e-133">Введите в поле поиска hello **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="7622e-133">In hello search box, type **Mixpanel**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="7622e-135">В панели результатов hello выберите **Mixpanel**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7622e-135">In hello results panel, select **Mixpanel**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7622e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7622e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7622e-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Mixpanel с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7622e-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7622e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Mixpanel является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7622e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mixpanel is tooa user in Azure AD.</span></span> <span data-ttu-id="7622e-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Mixpanel должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7622e-140">In other words, a link relationship between an Azure AD user and hello related user in Mixpanel needs toobe established.</span></span>

<span data-ttu-id="7622e-141">В Mixpanel, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="7622e-141">In Mixpanel, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7622e-142">tooconfigure и теста Azure AD единого входа с Mixpanel, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7622e-142">tooconfigure and test Azure AD single sign-on with Mixpanel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7622e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7622e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7622e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7622e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7622e-145">**[Создание тестового пользователя Mixpanel](#creating-a-mixpanel-test-user)**  -toohave аналог Саймон Britta в Mixpanel, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="7622e-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - toohave a counterpart of Britta Simon in Mixpanel that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7622e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7622e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7622e-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7622e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7622e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7622e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7622e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="7622e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="7622e-150">**tooconfigure Azure AD единого входа с Mixpanel, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7622e-150">**tooconfigure Azure AD single sign-on with Mixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="7622e-151">В hello в hello портала Azure **Mixpanel** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7622e-151">In hello Azure portal, on hello **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7622e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="7622e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="7622e-155">На hello **URL-адреса и домена Mixpanel** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7622e-155">On hello **Mixpanel Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="7622e-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="7622e-157">In hello **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7622e-158">Выполните регистрацию в [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset учетные данные для входа и обратитесь в службу hello [Mixpanel поддержки](mailto:support@mixpanel.com) tooenable настройки единого входа для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="7622e-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset up your login credentials and  contact hello [Mixpanel support team](mailto:support@mixpanel.com) tooenable SSO settings for your tenant.</span></span> <span data-ttu-id="7622e-159">Вы также можете получить URL-адрес единого входа, обратившись в службу поддержки Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="7622e-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="7622e-160">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="7622e-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="7622e-162">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7622e-162">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7622e-164">На hello **конфигурации Mixpanel** щелкните **Настройка Mixpanel** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="7622e-164">On hello **Mixpanel Configuration** section, click **Configure Mixpanel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7622e-165">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="7622e-165">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="7622e-167">В другом окне браузера, tooyour входа Mixpanel приложения от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="7622e-167">In a different browser window, sign-on tooyour Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="7622e-168">В нижней части страницы приветствия щелкните hello немного **шестеренки** значок в левом углу hello.</span><span class="sxs-lookup"><span data-stu-id="7622e-168">On bottom of hello page, click hello little **gear** icon in hello left corner.</span></span> 
   
    ![Единый вход в Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="7622e-170">Нажмите кнопку hello **безопасность доступа к** , а затем щелкните **изменить параметры**.</span><span class="sxs-lookup"><span data-stu-id="7622e-170">Click hello **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Параметры Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="7622e-172">На hello **изменить свой сертификат** странице диалогового окна щелкните **выбрать файл** tooupload Скачанный сертификат, а затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7622e-172">On hello **Change your certificate** dialog page, click **Choose file** tooupload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Параметры Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="7622e-174">В текстовом поле URL-адрес проверки подлинности hello на hello **изменить URL-адрес проверки подлинности** странице диалогового окна, вставить значение hello **SAML единого входа URL-адрес службы** , скопированных из портала Azure и нажмите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7622e-174">In hello authentication URL textbox on hello **Change your authentication  URL** dialog page, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Параметры Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="7622e-176">Нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="7622e-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="7622e-177">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="7622e-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7622e-178">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="7622e-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7622e-179">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7622e-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7622e-180">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7622e-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="7622e-181">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7622e-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7622e-183">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7622e-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7622e-184">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7622e-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7622e-186">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7622e-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7622e-188">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="7622e-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7622e-190">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7622e-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7622e-192">а.</span><span class="sxs-lookup"><span data-stu-id="7622e-192">a.</span></span> <span data-ttu-id="7622e-193">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7622e-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7622e-194">b.</span><span class="sxs-lookup"><span data-stu-id="7622e-194">b.</span></span> <span data-ttu-id="7622e-195">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7622e-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7622e-196">c.</span><span class="sxs-lookup"><span data-stu-id="7622e-196">c.</span></span> <span data-ttu-id="7622e-197">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="7622e-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7622e-198">d.</span><span class="sxs-lookup"><span data-stu-id="7622e-198">d.</span></span> <span data-ttu-id="7622e-199">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7622e-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="7622e-200">Создание тестового пользователя Mixpanel</span><span class="sxs-lookup"><span data-stu-id="7622e-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="7622e-201">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="7622e-201">hello objective of this section is toocreate a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="7622e-202">Войдите на tooyour Mixpanel корпоративный сайт с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="7622e-202">Sign on tooyour Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="7622e-203">Hello нижней страницы приветствия щелкните hello мало шестеренки кнопу hello левом углу tooopen hello **параметры** окна.</span><span class="sxs-lookup"><span data-stu-id="7622e-203">On hello bottom of hello page, click hello little gear button on hello left corner tooopen hello **Settings** window.</span></span>

3. <span data-ttu-id="7622e-204">Нажмите кнопку hello **команды** вкладки.</span><span class="sxs-lookup"><span data-stu-id="7622e-204">Click hello **Team** tab.</span></span>

4. <span data-ttu-id="7622e-205">В hello **член команды** текстовом поле введите адрес электронной почты Britta hello Azure.</span><span class="sxs-lookup"><span data-stu-id="7622e-205">In hello **team member** textbox, type Britta's email address in hello Azure.</span></span>
   
    ![Параметры Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="7622e-207">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="7622e-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="7622e-208">Hello пользователь получит по электронной почте tooset hello профиля.</span><span class="sxs-lookup"><span data-stu-id="7622e-208">hello user will get an email tooset up hello profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7622e-209">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7622e-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7622e-210">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooMixpanel доступа.</span><span class="sxs-lookup"><span data-stu-id="7622e-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMixpanel.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7622e-212">**tooassign tooMixpanel Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7622e-212">**tooassign Britta Simon tooMixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="7622e-213">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7622e-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7622e-215">В списке приложений hello выберите **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="7622e-215">In hello applications list, select **Mixpanel**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="7622e-217">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="7622e-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7622e-219">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7622e-219">Click **Add** button.</span></span> <span data-ttu-id="7622e-220">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7622e-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7622e-222">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7622e-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7622e-223">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7622e-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7622e-224">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7622e-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7622e-225">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7622e-225">Testing single sign-on</span></span>

<span data-ttu-id="7622e-226">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="7622e-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7622e-227">При нажатии кнопки hello Mixpanel плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Mixpanel приложения.</span><span class="sxs-lookup"><span data-stu-id="7622e-227">When you click hello Mixpanel tile in hello Access Panel, you should get automatically signed-on tooyour Mixpanel application.</span></span>
<span data-ttu-id="7622e-228">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7622e-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7622e-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7622e-229">Additional resources</span></span>

* [<span data-ttu-id="7622e-230">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7622e-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7622e-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7622e-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

