---
title: "Руководство по интеграции Azure Active Directory с Bambu by Sprout Social | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Bambu по Sprout социальных сетей."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c9998772c032476f9a18054873022f55b4bb78be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="c0d01-103">Руководство по интеграции Azure Active Directory с Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="c0d01-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="c0d01-104">В этом учебнике вы узнаете, как toointegrate Bambu по Sprout социальных сетей, с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0d01-104">In this tutorial, you learn how toointegrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0d01-105">Интеграция Bambu по Sprout социальных сетей с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c0d01-105">Integrating Bambu by Sprout Social with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c0d01-106">Можно управлять в Azure AD, имеющего доступ tooBambu по Sprout социальных сетей</span><span class="sxs-lookup"><span data-stu-id="c0d01-106">You can control in Azure AD who has access tooBambu by Sprout Social</span></span>
- <span data-ttu-id="c0d01-107">Вы можете включить вашей пользователей tooautomatically get вошедшего tooBambu Sprout социальных (Single Sign-On), их учетные записи Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0d01-107">You can enable your users tooautomatically get signed-on tooBambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0d01-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c0d01-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c0d01-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0d01-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Bambu by Sprout Social, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="c0d01-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c0d01-110">Prerequisites</span></span>

<span data-ttu-id="c0d01-111">tooconfigure интеграция Azure AD с Bambu по Sprout социальных сетей необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c0d01-111">tooconfigure Azure AD integration with Bambu by Sprout Social, you need hello following items:</span></span>

- <span data-ttu-id="c0d01-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c0d01-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0d01-113">подписка Bambu by Sprout Social с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c0d01-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0d01-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c0d01-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0d01-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c0d01-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0d01-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="c0d01-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c0d01-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0d01-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0d01-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c0d01-118">Scenario description</span></span>
<span data-ttu-id="c0d01-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c0d01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0d01-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c0d01-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0d01-121">Добавление Bambu Sprout социальных сетей, из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="c0d01-121">Adding Bambu by Sprout Social from hello gallery</span></span>
2. <span data-ttu-id="c0d01-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0d01-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-hello-gallery"></a><span data-ttu-id="c0d01-123">Добавление Bambu Sprout социальных сетей, из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="c0d01-123">Adding Bambu by Sprout Social from hello gallery</span></span>
<span data-ttu-id="c0d01-124">tooconfigure hello интеграции Bambu по Sprout социальных сетей в Azure AD, вы должны tooadd Bambu Sprout социальных сетей, из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c0d01-124">tooconfigure hello integration of Bambu by Sprout Social into Azure AD, you need tooadd Bambu by Sprout Social from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c0d01-125">**tooadd Bambu по Sprout социальных сетей, из коллекции hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="c0d01-125">**tooadd Bambu by Sprout Social from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0d01-126">В hello  **[портала Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c0d01-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0d01-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c0d01-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c0d01-131">Нажмите кнопку **новое приложение** кнопку сверху "hello" hello диалоговое окно tooadd новое приложение.</span><span class="sxs-lookup"><span data-stu-id="c0d01-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c0d01-133">Введите в поле поиска hello **Bambu по Sprout социальных**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-133">In hello search box, type **Bambu by Sprout Social**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="c0d01-135">В панели результатов hello, выберите **Bambu по Sprout социальных**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c0d01-135">In hello results panel, select **Bambu by Sprout Social**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0d01-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0d01-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0d01-138">В этом разделе описана настройка и проверка единого входа Azure AD в Bambu by Sprout Social с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0d01-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0d01-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Bambu по Sprout социальных является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0d01-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bambu by Sprout Social is tooa user in Azure AD.</span></span> <span data-ttu-id="c0d01-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Bambu по Sprout социальных должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c0d01-140">In other words, a link relationship between an Azure AD user and hello related user in Bambu by Sprout Social needs toobe established.</span></span>

<span data-ttu-id="c0d01-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **имя пользователя** в Bambu по Sprout социальных сетей.</span><span class="sxs-lookup"><span data-stu-id="c0d01-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="c0d01-142">tooconfigure и теста Azure AD единого входа с Bambu по Sprout социальных сетей, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c0d01-142">tooconfigure and test Azure AD single sign-on with Bambu by Sprout Social, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c0d01-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c0d01-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c0d01-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c0d01-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0d01-145">**[Создание Bambu Sprout социальных пользователем теста](#creating-a-bambu-by-sprout-social-test-user)**  -toohave аналог Саймон Britta в Bambu по Sprout социальных сетей, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="c0d01-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - toohave a counterpart of Britta Simon in Bambu by Sprout Social that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c0d01-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c0d01-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0d01-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c0d01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0d01-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0d01-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0d01-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей Bambu Sprout социальных приложением.</span><span class="sxs-lookup"><span data-stu-id="c0d01-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="c0d01-150">**tooconfigure Azure AD единого входа с Bambu по Sprout социальных сетей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0d01-150">**tooconfigure Azure AD single sign-on with Bambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0d01-151">В hello в hello портала Azure **Bambu по Sprout социальных** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-151">In hello Azure portal, on hello **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c0d01-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c0d01-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="c0d01-155">На hello **Bambu Sprout социальных доменом и URL-адреса** статьи, hello пользователь не имеет tooperform все меры как приложение hello уже заранее интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d01-155">On hello **Bambu by Sprout Social Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="c0d01-157">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c0d01-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="c0d01-159">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c0d01-159">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="c0d01-161">На hello **Bambu Sprout социальных конфигурацией** щелкните **Настройка Bambu по Sprout социальных** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="c0d01-161">On hello **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c0d01-162">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="c0d01-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="c0d01-164">tooconfigure единого входа на **Bambu по Sprout социальных** стороны, необходимо загрузить hello toosend **метаданные в формате XML** и **SAML единого входа URL-адрес службы** слишком[Bambu Sprout социальных поддержки](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="c0d01-164">tooconfigure single sign-on on **Bambu by Sprout Social** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="c0d01-165">Они будут устанавливается в порядке toohave hello правильно настроенной на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="c0d01-165">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c0d01-166">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c0d01-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c0d01-167">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello **Конфигурации** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c0d01-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click on hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c0d01-168">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0d01-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

tooensure users can sign-in tooBambu by Sprout Social after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooBambu by Sprout Social in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0d01-169">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0d01-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0d01-170">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d01-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c0d01-172">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0d01-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0d01-173">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c0d01-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0d01-175">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="c0d01-175">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0d01-177">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c0d01-177">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0d01-179">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c0d01-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0d01-181">а.</span><span class="sxs-lookup"><span data-stu-id="c0d01-181">a.</span></span> <span data-ttu-id="c0d01-182">В hello **имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-182">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="c0d01-183">b.</span><span class="sxs-lookup"><span data-stu-id="c0d01-183">b.</span></span> <span data-ttu-id="c0d01-184">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c0d01-184">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="c0d01-185">c.</span><span class="sxs-lookup"><span data-stu-id="c0d01-185">c.</span></span> <span data-ttu-id="c0d01-186">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c0d01-187">d.</span><span class="sxs-lookup"><span data-stu-id="c0d01-187">d.</span></span> <span data-ttu-id="c0d01-188">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="c0d01-189">Создание тестового пользователя для Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="c0d01-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="c0d01-190">В время подготовки пользователей и после проверки подлинности пользователей в приложении hello автоматически создаются непосредственно поддерживает приложение.</span><span class="sxs-lookup"><span data-stu-id="c0d01-190">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c0d01-191">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c0d01-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c0d01-192">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooBambu доступ по Sprout социальных сетей.</span><span class="sxs-lookup"><span data-stu-id="c0d01-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBambu by Sprout Social.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c0d01-194">**tooassign tooBambu Britta Simon по Sprout социальных сетей, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="c0d01-194">**tooassign Britta Simon tooBambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0d01-195">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c0d01-197">В списке приложений hello выберите **Bambu по Sprout социальных**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-197">In hello applications list, select **Bambu by Sprout Social**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="c0d01-199">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c0d01-201">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-201">Click **Add** button.</span></span> <span data-ttu-id="c0d01-202">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c0d01-204">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c0d01-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c0d01-205">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0d01-206">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c0d01-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0d01-207">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c0d01-207">Testing single sign-on</span></span>

<span data-ttu-id="c0d01-208">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c0d01-208">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c0d01-209">При нажатии кнопки hello Bambu по Sprout социальных плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Bambu Sprout социальных приложением.</span><span class="sxs-lookup"><span data-stu-id="c0d01-209">When you click hello Bambu by Sprout Social tile in hello Access Panel, you should get automatically signed-on tooyour Bambu by Sprout Social application.</span></span> <span data-ttu-id="c0d01-210">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="c0d01-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c0d01-211">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c0d01-211">Additional resources</span></span>

* [<span data-ttu-id="c0d01-212">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0d01-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0d01-213">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0d01-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

