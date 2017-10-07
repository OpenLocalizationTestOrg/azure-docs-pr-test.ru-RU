---
title: "Учебник. Интеграция Azure Active Directory с Icertis Contract Management Platform | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и платформой управления Icertis контракта."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 6eb99553ef9df732512a38fb0489e66b41ba94a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icertis-contract-management-platform"></a><span data-ttu-id="a50fb-103">Руководство. Интеграция Azure Active Directory с приложением Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="a50fb-103">Tutorial: Azure Active Directory integration with Icertis Contract Management Platform</span></span>

<span data-ttu-id="a50fb-104">В этом учебнике вы узнаете, как toointegrate Icertis платформы управления контракта с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a50fb-104">In this tutorial, you learn how toointegrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a50fb-105">Интеграция платформы управления Icertis контракта с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a50fb-105">Integrating Icertis Contract Management Platform with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a50fb-106">Можно управлять в Azure AD, имеющего доступ tooIcertis платформы управления контракта</span><span class="sxs-lookup"><span data-stu-id="a50fb-106">You can control in Azure AD who has access tooIcertis Contract Management Platform</span></span>
- <span data-ttu-id="a50fb-107">Ваш пользователей tooautomatically get вошедшего tooIcertis платформы управления контракта (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="a50fb-107">You can enable your users tooautomatically get signed-on tooIcertis Contract Management Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a50fb-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a50fb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a50fb-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a50fb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a50fb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a50fb-110">Prerequisites</span></span>

<span data-ttu-id="a50fb-111">tooconfigure интеграция Azure AD с платформой управления Icertis контракта необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a50fb-111">tooconfigure Azure AD integration with Icertis Contract Management Platform, you need hello following items:</span></span>

- <span data-ttu-id="a50fb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a50fb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a50fb-113">подписка Icertis Contract Management Platform с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a50fb-113">An Icertis Contract Management Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a50fb-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a50fb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a50fb-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a50fb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a50fb-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a50fb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a50fb-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a50fb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a50fb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a50fb-118">Scenario description</span></span>
<span data-ttu-id="a50fb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a50fb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a50fb-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a50fb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a50fb-121">Добавление платформы управления Icertis контракта из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="a50fb-121">Adding Icertis Contract Management Platform from hello gallery</span></span>
2. <span data-ttu-id="a50fb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a50fb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icertis-contract-management-platform-from-hello-gallery"></a><span data-ttu-id="a50fb-123">Добавление платформы управления Icertis контракта из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="a50fb-123">Adding Icertis Contract Management Platform from hello gallery</span></span>
<span data-ttu-id="a50fb-124">tooconfigure hello Интеграция платформы управления Icertis контракта в Azure AD, вы должны tooadd платформы управления Icertis контракта из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a50fb-124">tooconfigure hello integration of Icertis Contract Management Platform into Azure AD, you need tooadd Icertis Contract Management Platform from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a50fb-125">**tooadd Icertis платформы управления контракта из коллекции hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="a50fb-125">**tooadd Icertis Contract Management Platform from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a50fb-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a50fb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a50fb-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a50fb-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a50fb-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a50fb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a50fb-133">Введите в поле поиска hello **платформы управления контракта Icertis**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-133">In hello search box, type **Icertis Contract Management Platform**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_search.png)

5. <span data-ttu-id="a50fb-135">В панели результатов hello, выберите **платформы управления контракта Icertis**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a50fb-135">In hello results panel, select **Icertis Contract Management Platform**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a50fb-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a50fb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a50fb-138">В этом разделе описана настройка и проверка единого входа Azure AD в Icertis Contract Management Platform для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a50fb-138">In this section, you configure and test Azure AD single sign-on with Icertis Contract Management Platform based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a50fb-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в платформе управления Icertis контракта является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a50fb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Icertis Contract Management Platform is tooa user in Azure AD.</span></span> <span data-ttu-id="a50fb-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в платформе управления Icertis контракт должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a50fb-140">In other words, a link relationship between an Azure AD user and hello related user in Icertis Contract Management Platform needs toobe established.</span></span>

<span data-ttu-id="a50fb-141">На платформе управления Icertis контракта, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a50fb-141">In Icertis Contract Management Platform, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a50fb-142">tooconfigure и теста Azure AD единого входа с платформой управления Icertis контракта, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a50fb-142">tooconfigure and test Azure AD single sign-on with Icertis Contract Management Platform, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a50fb-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a50fb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a50fb-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a50fb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a50fb-145">**[Создание тестового пользователя, прошедшего платформы управления контракта Icertis](#creating-an-icertis-contract-management-platform-test-user)**  -toohave аналог Саймон Britta в платформу управления Icertis контракта, являющийся представлением связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a50fb-145">**[Creating an Icertis Contract Management Platform test user](#creating-an-icertis-contract-management-platform-test-user)** - toohave a counterpart of Britta Simon in Icertis Contract Management Platform that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a50fb-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a50fb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a50fb-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a50fb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a50fb-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a50fb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a50fb-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении платформы управления Icertis контракта.</span><span class="sxs-lookup"><span data-stu-id="a50fb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Icertis Contract Management Platform application.</span></span>

<span data-ttu-id="a50fb-150">**tooconfigure Azure AD единого входа с платформой управления Icertis контракта, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a50fb-150">**tooconfigure Azure AD single sign-on with Icertis Contract Management Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="a50fb-151">В hello в hello портала Azure **платформы управления контракта Icertis** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-151">In hello Azure portal, on hello **Icertis Contract Management Platform** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a50fb-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a50fb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_samlbase.png)

3. <span data-ttu-id="a50fb-155">На hello **URL-адреса и домена платформы управления контракта Icertis** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a50fb-155">On hello **Icertis Contract Management Platform Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_url.png)

    <span data-ttu-id="a50fb-157">а.</span><span class="sxs-lookup"><span data-stu-id="a50fb-157">a.</span></span> <span data-ttu-id="a50fb-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="a50fb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.icertis.com`</span></span>

    <span data-ttu-id="a50fb-159">b.</span><span class="sxs-lookup"><span data-stu-id="a50fb-159">b.</span></span> <span data-ttu-id="a50fb-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="a50fb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.icertis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a50fb-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="a50fb-161">These values are not real.</span></span> <span data-ttu-id="a50fb-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="a50fb-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a50fb-163">Обратитесь к [группа поддержки управления платформы Icertis контракта клиента](https://www.icertis.com/company/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="a50fb-163">Contact [Icertis Contract Management Platform Client support team](https://www.icertis.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="a50fb-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a50fb-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_certificate.png) 

5. <span data-ttu-id="a50fb-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a50fb-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-icertisicm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a50fb-168">На hello **конфигурации платформы управления контракта Icertis** щелкните **настройка платформы управления контракта Icertis** tooopen **настройки единого входа** окна.</span><span class="sxs-lookup"><span data-stu-id="a50fb-168">On hello **Icertis Contract Management Platform Configuration** section, click **Configure Icertis Contract Management Platform** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a50fb-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="a50fb-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_configure.png) 

7. <span data-ttu-id="a50fb-171">tooconfigure единого входа на **платформы управления контракта Icertis** стороны, необходимо загрузить hello toosend **метаданные в формате XML** и **URL-адрес выхода, идентификатор сущности SAML и SAML Single Sign-On URL-адрес службы** слишком[группа поддержки платформы управления контракта Icertis](https://www.icertis.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="a50fb-171">tooconfigure single sign-on on **Icertis Contract Management Platform** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="a50fb-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a50fb-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a50fb-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a50fb-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a50fb-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a50fb-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a50fb-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a50fb-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="a50fb-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a50fb-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a50fb-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a50fb-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a50fb-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a50fb-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a50fb-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a50fb-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a50fb-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a50fb-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a50fb-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a50fb-187">а.</span><span class="sxs-lookup"><span data-stu-id="a50fb-187">a.</span></span> <span data-ttu-id="a50fb-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a50fb-189">b.</span><span class="sxs-lookup"><span data-stu-id="a50fb-189">b.</span></span> <span data-ttu-id="a50fb-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a50fb-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a50fb-191">c.</span><span class="sxs-lookup"><span data-stu-id="a50fb-191">c.</span></span> <span data-ttu-id="a50fb-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a50fb-193">d.</span><span class="sxs-lookup"><span data-stu-id="a50fb-193">d.</span></span> <span data-ttu-id="a50fb-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-194">Click **Create**.</span></span>
 
### <a name="creating-an-icertis-contract-management-platform-test-user"></a><span data-ttu-id="a50fb-195">Создание тестового пользователя Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="a50fb-195">Creating an Icertis Contract Management Platform test user</span></span>

<span data-ttu-id="a50fb-196">В этом разделе описано, как создать пользователя Britta Simon в Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="a50fb-196">In this section, you create a user called Britta Simon in Icertis Contract Management Platform.</span></span> <span data-ttu-id="a50fb-197">Обратитесь [группа поддержки платформы управления контракта Icertis](https://www.icertis.com/company/contact/) tooadd пользователей hello в hello платформы управления Icertis контракта.</span><span class="sxs-lookup"><span data-stu-id="a50fb-197">Please work with [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/) tooadd hello users in hello Icertis Contract Management Platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a50fb-198">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a50fb-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a50fb-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooIcertis платформы управления контракта.</span><span class="sxs-lookup"><span data-stu-id="a50fb-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIcertis Contract Management Platform.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a50fb-201">**tooassign tooIcertis Britta Simon платформы управления контракта, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="a50fb-201">**tooassign Britta Simon tooIcertis Contract Management Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="a50fb-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a50fb-204">В списке приложений hello выберите **платформы управления контракта Icertis**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-204">In hello applications list, select **Icertis Contract Management Platform**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_app.png) 

3. <span data-ttu-id="a50fb-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a50fb-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-208">Click **Add** button.</span></span> <span data-ttu-id="a50fb-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a50fb-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a50fb-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a50fb-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a50fb-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a50fb-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a50fb-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a50fb-214">Testing single sign-on</span></span>

<span data-ttu-id="a50fb-215">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="a50fb-215">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a50fb-216">При выборе плитки платформы управления контракта Icertis hello в hello панели доступа, следует получать автоматически вошедшего tooyour приложения платформа управления Icertis контракта.</span><span class="sxs-lookup"><span data-stu-id="a50fb-216">When you click hello Icertis Contract Management Platform tile in hello Access Panel, you should get automatically signed-on tooyour Icertis Contract Management Platform application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a50fb-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a50fb-217">Additional resources</span></span>

* [<span data-ttu-id="a50fb-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a50fb-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a50fb-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a50fb-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_203.png

