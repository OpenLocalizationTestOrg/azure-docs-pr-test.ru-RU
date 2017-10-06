---
title: "Руководство по интеграции Azure Active Directory с 8x8 Virtual Office | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Office виртуальной 8 x 8."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: df5c5de77285cd3912b68cc3b1e3eee274aa951c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="b61c7-103">Руководство. Интеграция Azure Active Directory с 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="b61c7-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="b61c7-104">В этом учебнике вы узнаете, как toointegrate 8 x 8 виртуальных Office с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b61c7-104">In this tutorial, you learn how toointegrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b61c7-105">Интеграция 8 x 8 виртуальных Office с помощью Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b61c7-105">Integrating 8x8 Virtual Office with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b61c7-106">Можно управлять в Azure AD, имеющего доступ too8x8 виртуальной Office</span><span class="sxs-lookup"><span data-stu-id="b61c7-106">You can control in Azure AD who has access too8x8 Virtual Office</span></span>
- <span data-ttu-id="b61c7-107">Это позволит пользователям получить tooautomatically вошедшего too8x8 виртуального Office (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b61c7-107">You can enable your users tooautomatically get signed-on too8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b61c7-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b61c7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b61c7-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b61c7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b61c7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b61c7-110">Prerequisites</span></span>

<span data-ttu-id="b61c7-111">tooconfigure интеграция Azure AD с 8 x 8 виртуальных Office требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b61c7-111">tooconfigure Azure AD integration with 8x8 Virtual Office, you need hello following items:</span></span>

- <span data-ttu-id="b61c7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b61c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b61c7-113">подписка 8x8 Virtual Office с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b61c7-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b61c7-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b61c7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b61c7-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b61c7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b61c7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b61c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b61c7-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b61c7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b61c7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b61c7-118">Scenario description</span></span>
<span data-ttu-id="b61c7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b61c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b61c7-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b61c7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b61c7-121">Добавление виртуальных Office 8 x 8 из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b61c7-121">Adding 8x8 Virtual Office from hello gallery</span></span>
2. <span data-ttu-id="b61c7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b61c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-hello-gallery"></a><span data-ttu-id="b61c7-123">Добавление виртуальных Office 8 x 8 из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b61c7-123">Adding 8x8 Virtual Office from hello gallery</span></span>
<span data-ttu-id="b61c7-124">tooconfigure hello интеграции Office виртуальной 8 x 8 в Azure AD, необходимо tooadd 8 x 8 виртуальных Office из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b61c7-124">tooconfigure hello integration of 8x8 Virtual Office into Azure AD, you need tooadd 8x8 Virtual Office from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b61c7-125">**выполнять tooadd 8 x 8 виртуальных Office из галереи hello hello следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b61c7-125">**tooadd 8x8 Virtual Office from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b61c7-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b61c7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b61c7-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b61c7-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b61c7-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b61c7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b61c7-133">Введите в поле поиска hello **8 x 8 виртуальных Office**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-133">In hello search box, type **8x8 Virtual Office**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="b61c7-135">В панели результатов hello, выберите **8 x 8 виртуальных Office**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b61c7-135">In hello results panel, select **8x8 Virtual Office**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b61c7-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b61c7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b61c7-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение 8x8 Virtual Office с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b61c7-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b61c7-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в 8 x 8 виртуальных Office является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b61c7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 8x8 Virtual Office is tooa user in Azure AD.</span></span> <span data-ttu-id="b61c7-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в 8 x 8 виртуальных Office должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b61c7-140">In other words, a link relationship between an Azure AD user and hello related user in 8x8 Virtual Office needs toobe established.</span></span>

<span data-ttu-id="b61c7-141">В офисе виртуальной 8 x 8, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="b61c7-141">In 8x8 Virtual Office, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b61c7-142">tooconfigure и теста Azure AD единого входа с 8 x 8 виртуальных Office, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b61c7-142">tooconfigure and test Azure AD single sign-on with 8x8 Virtual Office, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b61c7-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b61c7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b61c7-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b61c7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b61c7-145">**[Создание тестового пользователя виртуальный Office 8 x 8](#creating-a-8x8-virtual-office-test-user) ** -toohave аналог Саймон Britta в 8 x 8 виртуальных Office, которая является представлением связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b61c7-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - toohave a counterpart of Britta Simon in 8x8 Virtual Office that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b61c7-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b61c7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b61c7-147">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b61c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b61c7-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b61c7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b61c7-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Office виртуального 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="b61c7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="b61c7-150">**tooconfigure Azure AD единого входа с 8 x 8 виртуальных Office, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b61c7-150">**tooconfigure Azure AD single sign-on with 8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="b61c7-151">В hello в hello портала Azure **8 x 8 виртуальных Office** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-151">In hello Azure portal, on hello **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b61c7-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b61c7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="b61c7-155">На hello **URL-адреса и домена Office 8 x 8 виртуальных** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b61c7-155">On hello **8x8 Virtual Office Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="b61c7-157">а.</span><span class="sxs-lookup"><span data-stu-id="b61c7-157">a.</span></span> <span data-ttu-id="b61c7-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="b61c7-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="b61c7-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="b61c7-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="b61c7-160">b.</span><span class="sxs-lookup"><span data-stu-id="b61c7-160">b.</span></span> <span data-ttu-id="b61c7-161">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="b61c7-161">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="b61c7-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="b61c7-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b61c7-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b61c7-163">These values are not real.</span></span> <span data-ttu-id="b61c7-164">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b61c7-164">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="b61c7-165">Обратитесь к [группа поддержки 8 x 8 виртуальных Office](https://www.8x8.com/about-us/contact-us) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="b61c7-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) tooget these values.</span></span>
 


4. <span data-ttu-id="b61c7-166">На hello **сертификат подписи SAML** щелкните **сертификата (Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b61c7-166">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="b61c7-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b61c7-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b61c7-170">На hello **конфигурации Office 8 x 8 виртуальных** щелкните **Настройка 8 x 8 виртуальных Office** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="b61c7-170">On hello **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b61c7-171">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="b61c7-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="b61c7-173">Клиент tooyour входа 8 x 8 виртуальных Office с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="b61c7-173">Sign-on tooyour 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="b61c7-174">На панели приложения выберите **Virtual Office Account Mgr** (Диспетчер учетных записей Virtual Office).</span><span class="sxs-lookup"><span data-stu-id="b61c7-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="b61c7-176">Выберите **Business** toomanage учетной записи и нажмите кнопку **входа** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b61c7-176">Select **Business** account toomanage and click **Sign In** button.</span></span>
   
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="b61c7-178">Нажмите кнопку **учетные записи** вкладку в списке меню hello.</span><span class="sxs-lookup"><span data-stu-id="b61c7-178">Click **Accounts** tab in hello menu list.</span></span>
   
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="b61c7-180">Нажмите кнопку **Single Sign On** в hello список учетных записей.</span><span class="sxs-lookup"><span data-stu-id="b61c7-180">Click **Single Sign On** in hello list of Accounts.</span></span>
   
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="b61c7-182">В разделе "Authentication method" (Метод проверки подлинности) установите флажок **Signle Sign On** (Единый вход), а затем установите переключатель **SAML**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="b61c7-184">Копировать **URL-адрес единого входа SAML**, **максимум исходящий адрес службы единого** и **URL-адрес издателя** из Azure AD слишком**в URL-адрес входа**, **Out URL-адрес входа ** и **URL-адрес издателя** в 8 x 8 виртуальных Office.</span><span class="sxs-lookup"><span data-stu-id="b61c7-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD too**Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="b61c7-186">Нажмите кнопку **браузера** tooupload hello сертификат, который был загружен из Azure AD и нажмите кнопку hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b61c7-186">Click **Browser** button tooupload hello certificate which you downloaded from Azure AD, and click hello **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="b61c7-187">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b61c7-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b61c7-188">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b61c7-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b61c7-189">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b61c7-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b61c7-190">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b61c7-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="b61c7-191">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b61c7-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b61c7-193">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b61c7-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b61c7-194">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b61c7-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b61c7-196">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b61c7-198">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b61c7-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b61c7-200">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b61c7-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b61c7-202">а.</span><span class="sxs-lookup"><span data-stu-id="b61c7-202">a.</span></span> <span data-ttu-id="b61c7-203">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b61c7-204">b.</span><span class="sxs-lookup"><span data-stu-id="b61c7-204">b.</span></span> <span data-ttu-id="b61c7-205">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b61c7-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b61c7-206">c.</span><span class="sxs-lookup"><span data-stu-id="b61c7-206">c.</span></span> <span data-ttu-id="b61c7-207">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b61c7-208">d.</span><span class="sxs-lookup"><span data-stu-id="b61c7-208">d.</span></span> <span data-ttu-id="b61c7-209">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="b61c7-210">Создание тестового пользователя 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="b61c7-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="b61c7-211">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в офисе виртуальной 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="b61c7-211">hello objective of this section is toocreate a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="b61c7-212">Приложение 8x8 Virtual Office поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b61c7-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="b61c7-213">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="b61c7-213">There is no action item for you in this section.</span></span> <span data-ttu-id="b61c7-214">Новый пользователь создается во время попытки tooaccess 8 x 8 виртуальных Office, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="b61c7-214">A new user is created during an attempt tooaccess 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="b61c7-215">Если требуется toocreate пользователя вручную, необходимо toocontact hello [группа поддержки виртуального Office 8 x 8](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="b61c7-215">If you need toocreate a user manually, you need toocontact hello [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b61c7-216">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b61c7-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b61c7-217">В этом разделе включите Саймон Britta toouse Azure единого входа путем предоставления доступа к too8x8 виртуального Office.</span><span class="sxs-lookup"><span data-stu-id="b61c7-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too8x8 Virtual Office.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b61c7-219">**tooassign Britta Simon too8x8 виртуального Office, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="b61c7-219">**tooassign Britta Simon too8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="b61c7-220">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b61c7-222">В списке приложений hello выберите **8 x 8 виртуальных Office**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-222">In hello applications list, select **8x8 Virtual Office**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="b61c7-224">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b61c7-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-226">Click **Add** button.</span></span> <span data-ttu-id="b61c7-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b61c7-229">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b61c7-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b61c7-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b61c7-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b61c7-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b61c7-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b61c7-232">Testing single sign-on</span></span>

<span data-ttu-id="b61c7-233">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b61c7-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b61c7-234">При нажатии кнопки hello 8 x 8 виртуальных Office плитки в панели доступа hello, вы должны получить приложение виртуального Office автоматически вошедшего tooyour 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="b61c7-234">When you click hello 8x8 Virtual Office tile in hello Access Panel, you should get automatically signed-on tooyour 8x8 Virtual Office application.</span></span>
<span data-ttu-id="b61c7-235">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="b61c7-235">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b61c7-236">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b61c7-236">Additional resources</span></span>

* [<span data-ttu-id="b61c7-237">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b61c7-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b61c7-238">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b61c7-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

