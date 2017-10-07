---
title: "Руководство. Интеграция Azure Active Directory с Procore SSO | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Procore единого входа."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="aa1f0-103">Руководство. Интеграция Azure Active Directory с Procore SSO</span><span class="sxs-lookup"><span data-stu-id="aa1f0-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="aa1f0-104">В этом учебнике вы узнаете, как toointegrate Procore единого входа в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aa1f0-104">In this tutorial, you learn how toointegrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa1f0-105">Интеграция Procore единого входа с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="aa1f0-105">Integrating Procore SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aa1f0-106">Можно управлять в Azure AD, имеющего доступ tooProcore единого входа</span><span class="sxs-lookup"><span data-stu-id="aa1f0-106">You can control in Azure AD who has access tooProcore SSO</span></span>
- <span data-ttu-id="aa1f0-107">Можно включить на пользователей tooautomatically get вошедшего tooProcore единого входа (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa1f0-107">You can enable your users tooautomatically get signed-on tooProcore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa1f0-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="aa1f0-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="aa1f0-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa1f0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="aa1f0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="aa1f0-110">Prerequisites</span></span>

<span data-ttu-id="aa1f0-111">tooconfigure интеграция Azure AD с помощью Procore единого входа требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="aa1f0-111">tooconfigure Azure AD integration with Procore SSO, you need hello following items:</span></span>

- <span data-ttu-id="aa1f0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="aa1f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa1f0-113">подписка на Procore SSO с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa1f0-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa1f0-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="aa1f0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa1f0-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="aa1f0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa1f0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa1f0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="aa1f0-118">Scenario description</span></span>
<span data-ttu-id="aa1f0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa1f0-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="aa1f0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa1f0-121">Добавление Procore единого входа из галереи hello</span><span class="sxs-lookup"><span data-stu-id="aa1f0-121">Adding Procore SSO from hello gallery</span></span>
2. <span data-ttu-id="aa1f0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa1f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-hello-gallery"></a><span data-ttu-id="aa1f0-123">Добавление Procore единого входа из галереи hello</span><span class="sxs-lookup"><span data-stu-id="aa1f0-123">Adding Procore SSO from hello gallery</span></span>
<span data-ttu-id="aa1f0-124">tooconfigure hello интеграции Procore единого входа в Azure AD, вы должны tooadd Procore единого входа из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-124">tooconfigure hello integration of Procore SSO into Azure AD, you need tooadd Procore SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aa1f0-125">**tooadd Procore единого входа из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="aa1f0-125">**tooadd Procore SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa1f0-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa1f0-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aa1f0-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="aa1f0-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="aa1f0-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="aa1f0-133">Введите в поле поиска hello **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-133">In hello search box, type **Procore SSO**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="aa1f0-135">В панели результатов hello выберите **Procore SSO**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-135">In hello results panel, select **Procore SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aa1f0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa1f0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aa1f0-138">В этом разделе описана настройка и проверка единого входа Azure AD в Procore SSO с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aa1f0-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Procore единого входа является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Procore SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="aa1f0-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Procore единого входа должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-140">In other words, a link relationship between an Azure AD user and hello related user in Procore SSO needs toobe established.</span></span>

<span data-ttu-id="aa1f0-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Procore единого входа.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Procore SSO.</span></span>

<span data-ttu-id="aa1f0-142">tooconfigure и теста Azure AD единого входа с помощью Procore единого входа, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="aa1f0-142">tooconfigure and test Azure AD single sign-on with Procore SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aa1f0-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aa1f0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa1f0-145">**[Создание тестового пользователя Procore SSO](#creating-a-procore-sso-test-user)**  -toohave аналог Саймон Britta в Procore единый вход, являющийся представлением ей связанного toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - toohave a counterpart of Britta Simon in Procore SSO that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="aa1f0-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa1f0-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aa1f0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa1f0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aa1f0-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Procore единого входа.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="aa1f0-150">**tooconfigure Azure AD единого входа с помощью Procore единого входа, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="aa1f0-150">**tooconfigure Azure AD single sign-on with Procore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa1f0-151">На портале управления Azure hello на hello **Procore SSO** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-151">In hello Azure Management portal, on hello **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="aa1f0-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="aa1f0-155">На hello **Procore домена единого входа и URL-адреса** статьи, hello пользователь не имеет tooperform все меры как приложение hello уже заранее интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-155">On hello **Procore SSO Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="aa1f0-157">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="aa1f0-159">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="aa1f0-159">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aa1f0-161">На hello **Procore Настройка единого входа** щелкните **Настройка Procore SSO** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-161">On hello **Procore SSO Configuration** section, click **Configure Procore SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="aa1f0-162">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="aa1f0-162">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="aa1f0-164">tooconfigure единого входа на **Procore SSO** стороны, узел procore компании tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-164">tooconfigure single sign-on on **Procore SSO** side, login tooyour procore company site as an administrator.</span></span>

8. <span data-ttu-id="aa1f0-165">Элементов в раскрывающемся hello вниз, щелкните на **администратора** страницу параметров единого входа tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-165">From hello toolbox drop down, click on **Admin** tooopen hello SSO settings page.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="aa1f0-167">Вставить hello значения в полях hello, как описано ниже-</span><span class="sxs-lookup"><span data-stu-id="aa1f0-167">Paste hello values in hello boxes as described below-</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="aa1f0-169">а.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-169">a.</span></span> <span data-ttu-id="aa1f0-170">В hello **единого входа на URL-адрес издателя** вставьте hello, идентификатор сущности SAML копируются hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-170">In hello **Single Sign On Issuer URL** box, paste hello SAML Entity ID copied from hello Azure portal.</span></span>

    <span data-ttu-id="aa1f0-171">b.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-171">b.</span></span> <span data-ttu-id="aa1f0-172">В hello **SAML на целевой URL-адрес входа** вставьте hello SAML единого входа URL-адрес службы копируются hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-172">In hello **SAML Sign On Target URL** box, paste hello SAML Single Sign-On Service URL copied from hello Azure portal.</span></span>

    <span data-ttu-id="aa1f0-173">c.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-173">c.</span></span> <span data-ttu-id="aa1f0-174">Теперь откройте hello **метаданные в формате XML** загружается выше с hello портал Azure и копирование сертификатов hello в тег hello **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-174">Now open hello **Metadata XML** downloaded above from hello Azure portal and copy hello certficate in hello tag named **X509Certificate**.</span></span> <span data-ttu-id="aa1f0-175">Вставить hello копируется значение hello **сертификат единого входа x509** поле.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-175">Paste hello copied value into hello **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="aa1f0-176">Щелкните **Save Changes** (Сохранить изменения).</span><span class="sxs-lookup"><span data-stu-id="aa1f0-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="aa1f0-177">После этих параметров должен toosend hello **доменное имя** (например **contoso.com**), по которой вход Procore toohello [Procore поддержки](https://support.procore.com/) и они будут Активируйте федеративный единый вход для этого домена.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-177">After these settings, you needs toosend hello **domain name** (e.g **contoso.com**) through which you are logging into Procore toohello [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aa1f0-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa1f0-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="aa1f0-179">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-179">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="aa1f0-181">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="aa1f0-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa1f0-182">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-182">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa1f0-184">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-184">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa1f0-186">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-186">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa1f0-188">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="aa1f0-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa1f0-190">а.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-190">a.</span></span> <span data-ttu-id="aa1f0-191">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa1f0-192">b.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-192">b.</span></span> <span data-ttu-id="aa1f0-193">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa1f0-194">c.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-194">c.</span></span> <span data-ttu-id="aa1f0-195">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aa1f0-196">d.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-196">d.</span></span> <span data-ttu-id="aa1f0-197">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="aa1f0-198">Создание тестового пользователя Procore SSO</span><span class="sxs-lookup"><span data-stu-id="aa1f0-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="aa1f0-199">Следуйте hello ниже шаги toocreate Procore тестового пользователя с их стороны.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-199">Please follow hello below steps toocreate a Procore test user on their side.</span></span>

1. <span data-ttu-id="aa1f0-200">Узел procore компании tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-200">Login tooyour procore company site as an administrator.</span></span>  

2. <span data-ttu-id="aa1f0-201">Элементов в раскрывающемся hello вниз, щелкните на **каталога** страница directory компании tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-201">From hello toolbox drop down, click on **Directory** tooopen hello company directory page.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="aa1f0-203">Щелкните **добавления пользователя** tooopen hello формы и введите выполнять следующие параметра:</span><span class="sxs-lookup"><span data-stu-id="aa1f0-203">Click on **Add a Person** option tooopen hello form and enter perform following options -</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="aa1f0-205">а.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-205">a.</span></span> <span data-ttu-id="aa1f0-206">В hello **имя** в текстовое поле имя пользователя тип как **Britta**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-206">In hello **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="aa1f0-207">b.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-207">b.</span></span> <span data-ttu-id="aa1f0-208">В hello **Фамилия** текстовое поле, Фамилия пользователя тип как **Simon**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-208">In hello **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="aa1f0-209">c.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-209">c.</span></span> <span data-ttu-id="aa1f0-210">В hello **адрес электронной почты** в текстовое поле, например адрес электронной почты пользователя типа  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="aa1f0-210">In hello **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="aa1f0-211">d.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-211">d.</span></span> <span data-ttu-id="aa1f0-212">Для параметра **Permission Template** (Шаблон разрешений) выберите значение **Apply Permission Template Later** (Применить шаблон разрешений позже).</span><span class="sxs-lookup"><span data-stu-id="aa1f0-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="aa1f0-213">д.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-213">e.</span></span> <span data-ttu-id="aa1f0-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-214">Click **Create**.</span></span>

4. <span data-ttu-id="aa1f0-215">Проверьте и обновите hello сведения для hello вновь добавленного контакта.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-215">Check and update hello details for hello newly added contact.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="aa1f0-217">Щелкните **сохранения и отправки Invitiation** (Если приглашение по почте требуется) или **Сохранить** (сохранить непосредственно) регистрация пользователя toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) toocomplete hello user registration.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aa1f0-219">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="aa1f0-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aa1f0-220">В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooProcore единого входа.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooProcore SSO.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="aa1f0-222">**tooassign tooProcore Britta Simon единого входа, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="aa1f0-222">**tooassign Britta Simon tooProcore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa1f0-223">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="aa1f0-225">В списке приложений hello выберите **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-225">In hello applications list, select **Procore SSO**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="aa1f0-227">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="aa1f0-229">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-229">Click **Add** button.</span></span> <span data-ttu-id="aa1f0-230">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="aa1f0-232">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aa1f0-233">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa1f0-234">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aa1f0-235">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="aa1f0-235">Testing single sign-on</span></span>

<span data-ttu-id="aa1f0-236">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="aa1f0-237">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="aa1f0-238">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="aa1f0-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="aa1f0-239">Если щелкнуть плитку hello Procore единого входа в панель доступа hello, вы должны получить приложение автоматически вошедшего tooyour Procore единого входа.</span><span class="sxs-lookup"><span data-stu-id="aa1f0-239">When you click hello Procore SSO tile in hello Access Panel, you should get automatically signed-on tooyour Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa1f0-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="aa1f0-240">Additional resources</span></span>

* [<span data-ttu-id="aa1f0-241">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa1f0-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa1f0-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aa1f0-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

