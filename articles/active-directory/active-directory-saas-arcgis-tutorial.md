---
title: "Руководство по интеграции Azure Active Directory с ArcGIS Online | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ArcGIS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="5e904-103">Руководство по интеграции Azure Active Directory с ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="5e904-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="5e904-104">В этом учебнике вы узнаете, как toointegrate ArcGIS Online с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5e904-104">In this tutorial, you learn how toointegrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5e904-105">Интеграция ArcGIS Online с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5e904-105">Integrating ArcGIS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5e904-106">Можно управлять в Azure AD, имеющего tooArcGIS доступ через Интернет</span><span class="sxs-lookup"><span data-stu-id="5e904-106">You can control in Azure AD who has access tooArcGIS Online</span></span>
- <span data-ttu-id="5e904-107">Можно включить на пользователей tooautomatically get вошедшего tooArcGIS сети (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e904-107">You can enable your users tooautomatically get signed-on tooArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5e904-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5e904-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5e904-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5e904-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="5e904-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5e904-110">Prerequisites</span></span>

<span data-ttu-id="5e904-111">tooconfigure интеграция Azure AD с ArcGIS Online требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5e904-111">tooconfigure Azure AD integration with ArcGIS Online, you need hello following items:</span></span>

- <span data-ttu-id="5e904-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5e904-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5e904-113">подписка ArcGIS Online с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5e904-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5e904-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5e904-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5e904-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="5e904-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5e904-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5e904-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5e904-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5e904-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5e904-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5e904-118">Scenario description</span></span>
<span data-ttu-id="5e904-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5e904-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5e904-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="5e904-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5e904-121">Добавление ArcGIS Online из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5e904-121">Adding ArcGIS Online from hello gallery</span></span>
2. <span data-ttu-id="5e904-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e904-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-hello-gallery"></a><span data-ttu-id="5e904-123">Добавление ArcGIS Online из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5e904-123">Adding ArcGIS Online from hello gallery</span></span>
<span data-ttu-id="5e904-124">tooconfigure hello интеграции ArcGIS сети в Azure AD, вы должны tooadd ArcGIS сети из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5e904-124">tooconfigure hello integration of ArcGIS Online into Azure AD, you need tooadd ArcGIS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5e904-125">**tooadd ArcGIS сети из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="5e904-125">**tooadd ArcGIS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e904-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5e904-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5e904-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="5e904-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5e904-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e904-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5e904-131">Нажмите кнопку **новое приложение** кнопку сверху "hello" hello диалоговое окно tooadd новое приложение.</span><span class="sxs-lookup"><span data-stu-id="5e904-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5e904-133">Введите в поле поиска hello **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="5e904-133">In hello search box, type **ArcGIS Online**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="5e904-135">В панели результатов hello выберите **ArcGIS Online**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5e904-135">In hello results panel, select **ArcGIS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5e904-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e904-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5e904-138">В этом разделе описана настройка и проверка единого входа Azure AD в ArcGIS Online с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e904-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5e904-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ArcGIS сети является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e904-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ArcGIS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="5e904-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в ArcGIS документации должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="5e904-140">In other words, a link relationship between an Azure AD user and hello related user in ArcGIS Online needs toobe established.</span></span>

<span data-ttu-id="5e904-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** ArcGIS документации.</span><span class="sxs-lookup"><span data-stu-id="5e904-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="5e904-142">tooconfigure и тестирования Azure AD единого входа в ArcGIS Online, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5e904-142">tooconfigure and test Azure AD single sign-on with ArcGIS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5e904-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="5e904-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5e904-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="5e904-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5e904-145">**[Создание тестового пользователя, прошедшего ArcGIS Online](#creating-an-arcgis-online-test-user)**  -toohave аналог Саймон Britta документации ArcGIS, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="5e904-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - toohave a counterpart of Britta Simon in ArcGIS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5e904-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="5e904-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5e904-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5e904-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5e904-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e904-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5e904-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в ArcGIS документации приложения.</span><span class="sxs-lookup"><span data-stu-id="5e904-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="5e904-150">**tooconfigure Azure AD единого входа в ArcGIS Online выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5e904-150">**tooconfigure Azure AD single sign-on with ArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e904-151">В hello в hello портала Azure **ArcGIS Online** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5e904-151">In hello Azure portal, on hello **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5e904-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="5e904-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="5e904-155">На hello **URL-адреса и домена ArcGIS** выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="5e904-155">On hello **ArcGIS Online Domain and URLs** section, perform hello following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="5e904-157">В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="5e904-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5e904-158">Это значение не реальными hello.</span><span class="sxs-lookup"><span data-stu-id="5e904-158">This value is not hello real.</span></span> <span data-ttu-id="5e904-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="5e904-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5e904-160">Обратитесь к [группа поддержки клиента в сети ArcGIS](http://support.esri.com/) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="5e904-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) tooget this value.</span></span> 

4. <span data-ttu-id="5e904-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5e904-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="5e904-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5e904-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5e904-165">В другом окне веб-браузера войдите на свой корпоративный веб-сайт ArcGIS в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="5e904-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="5e904-166">Щелкните **EDIT SETTINGS** (Изменить параметры).</span><span class="sxs-lookup"><span data-stu-id="5e904-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="5e904-167">![Изменение параметров](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Изменение параметров")</span><span class="sxs-lookup"><span data-stu-id="5e904-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="5e904-168">Щелкните **Security**(Безопасность).</span><span class="sxs-lookup"><span data-stu-id="5e904-168">Click **Security**.</span></span>

    <span data-ttu-id="5e904-169">![Безопасность](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="5e904-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="5e904-170">В разделе **Enterprise Logins** (Корпоративные имена для входа) установите флажок **Set Identity Provider** (Задать поставщик удостоверений).</span><span class="sxs-lookup"><span data-stu-id="5e904-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="5e904-171">![Корпоративные имена входа](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Корпоративные имена входа")</span><span class="sxs-lookup"><span data-stu-id="5e904-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="5e904-172">На hello **Настройка поставщика удостоверений** конфигурации выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5e904-172">On hello **Set Identity Provider** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="5e904-173">![Назначение поставщика удостоверений](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Назначение поставщика удостоверений")</span><span class="sxs-lookup"><span data-stu-id="5e904-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="5e904-174">а.</span><span class="sxs-lookup"><span data-stu-id="5e904-174">a.</span></span> <span data-ttu-id="5e904-175">В hello **имя** текстовом поле введите имя вашей организации.</span><span class="sxs-lookup"><span data-stu-id="5e904-175">In hello **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="5e904-176">b.</span><span class="sxs-lookup"><span data-stu-id="5e904-176">b.</span></span> <span data-ttu-id="5e904-177">Для **метаданные для hello поставщика удостоверений предприятия будут передаваться с помощью**выберите **файл**.</span><span class="sxs-lookup"><span data-stu-id="5e904-177">For **Metadata for hello Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="5e904-178">c.</span><span class="sxs-lookup"><span data-stu-id="5e904-178">c.</span></span> <span data-ttu-id="5e904-179">tooupload скачанный файл метаданных, щелкните **выбрать файл**.</span><span class="sxs-lookup"><span data-stu-id="5e904-179">tooupload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="5e904-180">d.</span><span class="sxs-lookup"><span data-stu-id="5e904-180">d.</span></span> <span data-ttu-id="5e904-181">Щелкните **SET IDENTITY PROVIDER** (Задать поставщик удостоверений).</span><span class="sxs-lookup"><span data-stu-id="5e904-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="5e904-182">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="5e904-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5e904-183">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="5e904-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5e904-184">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5e904-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5e904-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e904-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="5e904-186">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5e904-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5e904-188">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5e904-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e904-189">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5e904-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5e904-191">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="5e904-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5e904-193">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5e904-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5e904-195">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5e904-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5e904-197">а.</span><span class="sxs-lookup"><span data-stu-id="5e904-197">a.</span></span> <span data-ttu-id="5e904-198">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5e904-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5e904-199">b.</span><span class="sxs-lookup"><span data-stu-id="5e904-199">b.</span></span> <span data-ttu-id="5e904-200">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="5e904-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="5e904-201">c.</span><span class="sxs-lookup"><span data-stu-id="5e904-201">c.</span></span> <span data-ttu-id="5e904-202">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="5e904-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5e904-203">d.</span><span class="sxs-lookup"><span data-stu-id="5e904-203">d.</span></span> <span data-ttu-id="5e904-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5e904-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="5e904-205">Создание тестового пользователя ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="5e904-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="5e904-206">В порядке tooenable toolog пользователей Azure AD в ArcGIS Online их необходимо подготовить в ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="5e904-206">In order tooenable Azure AD users toolog into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="5e904-207">В случае hello документации ArcGIS Подготовка осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="5e904-207">In hello case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="5e904-208">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5e904-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e904-209">Войдите в tooyour **ArcGIS** клиента.</span><span class="sxs-lookup"><span data-stu-id="5e904-209">Log in tooyour **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="5e904-210">Щелкните **INVITE MEMBERS** (Пригласить участников).</span><span class="sxs-lookup"><span data-stu-id="5e904-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="5e904-211">![Приглашение участников](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Приглашение участников")</span><span class="sxs-lookup"><span data-stu-id="5e904-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="5e904-212">Щелкните переключатель **Add members automatically without sending an email** (Добавлять участников автоматически без отправки электронного сообщения) и нажмите кнопку **NEXT** (Далее).</span><span class="sxs-lookup"><span data-stu-id="5e904-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="5e904-213">![Автоматическое добавление участников](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Автоматическое добавление участников")</span><span class="sxs-lookup"><span data-stu-id="5e904-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="5e904-214">На hello **члены** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5e904-214">On hello **Members** dialog page, perform hello following steps:</span></span>
   
     <span data-ttu-id="5e904-215">![Добавление и просмотр](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Добавление и просмотр")</span><span class="sxs-lookup"><span data-stu-id="5e904-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="5e904-216">а.</span><span class="sxs-lookup"><span data-stu-id="5e904-216">a.</span></span> <span data-ttu-id="5e904-217">Введите hello **электронной почты**, **имя**, и **Фамилия** действительной учетной записи AAD, вы хотите tooprovision.</span><span class="sxs-lookup"><span data-stu-id="5e904-217">Enter hello **Email**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision.</span></span>
  
     <span data-ttu-id="5e904-218">b.</span><span class="sxs-lookup"><span data-stu-id="5e904-218">b.</span></span> <span data-ttu-id="5e904-219">Нажмите кнопку **ADD AND REVIEW** (Добавить и просмотреть).</span><span class="sxs-lookup"><span data-stu-id="5e904-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="5e904-220">Просмотрите данные hello введенные данные и нажмите кнопку **добавить ЧЛЕНОВ**.</span><span class="sxs-lookup"><span data-stu-id="5e904-220">Review hello data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="5e904-221">![Добавление участника](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Добавление участника")</span><span class="sxs-lookup"><span data-stu-id="5e904-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="5e904-222">Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="5e904-222">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5e904-223">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="5e904-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5e904-224">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooArcGIS доступа через Интернет.</span><span class="sxs-lookup"><span data-stu-id="5e904-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooArcGIS Online.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5e904-226">**tooassign Britta Simon tooArcGIS через Интернет, выполнять hello следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="5e904-226">**tooassign Britta Simon tooArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e904-227">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e904-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5e904-229">В списке приложений hello выберите **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="5e904-229">In hello applications list, select **ArcGIS Online**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="5e904-231">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="5e904-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5e904-233">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5e904-233">Click **Add** button.</span></span> <span data-ttu-id="5e904-234">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5e904-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5e904-236">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="5e904-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5e904-237">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5e904-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5e904-238">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5e904-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5e904-239">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5e904-239">Testing single sign-on</span></span>

<span data-ttu-id="5e904-240">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="5e904-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5e904-241">При нажатии кнопки hello ArcGIS Online плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour ArcGIS интерактивных приложений.</span><span class="sxs-lookup"><span data-stu-id="5e904-241">When you click hello ArcGIS Online tile in hello Access Panel, you should get automatically signed-on tooyour ArcGIS Online application.</span></span>
<span data-ttu-id="5e904-242">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5e904-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5e904-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5e904-243">Additional resources</span></span>

* [<span data-ttu-id="5e904-244">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e904-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5e904-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5e904-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

