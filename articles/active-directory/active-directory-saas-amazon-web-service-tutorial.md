---
title: "Руководство по интеграции Azure Active Directory с Amazon Web Services (AWS) | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Amazon Web Services (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="a7508-103">Руководство по интеграции Azure Active Directory с Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="a7508-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="a7508-104">В этом учебнике вы узнаете, как toointegrate Amazon Web Services (AWS) с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7508-104">In this tutorial, you learn how toointegrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7508-105">Интеграция с Azure AD Amazon Web Services (AWS) предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a7508-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a7508-106">Можно управлять в Azure AD, имеющего доступ tooAmazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="a7508-106">You can control in Azure AD who has access tooAmazon Web Services (AWS)</span></span>
- <span data-ttu-id="a7508-107">Ваш пользователей tooautomatically get вошедшего tooAmazon Web Services (AWS) (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7508-107">You can enable your users tooautomatically get signed-on tooAmazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7508-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a7508-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a7508-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7508-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="a7508-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a7508-110">Prerequisites</span></span>

<span data-ttu-id="a7508-111">tooconfigure интеграция Azure AD с Amazon Web Services (AWS) требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a7508-111">tooconfigure Azure AD integration with Amazon Web Services (AWS), you need hello following items:</span></span>

- <span data-ttu-id="a7508-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a7508-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7508-113">Подписка с поддержкой единого входа в Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="a7508-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7508-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a7508-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7508-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a7508-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7508-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="a7508-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a7508-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7508-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7508-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a7508-118">Scenario description</span></span>
<span data-ttu-id="a7508-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a7508-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7508-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a7508-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7508-121">Добавление Amazon Web Services (AWS) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="a7508-121">Adding Amazon Web Services (AWS) from hello gallery</span></span>
2. <span data-ttu-id="a7508-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7508-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a><span data-ttu-id="a7508-123">Добавление Amazon Web Services (AWS) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="a7508-123">Adding Amazon Web Services (AWS) from hello gallery</span></span>
<span data-ttu-id="a7508-124">tooconfigure hello интеграция Amazon Web Services (AWS) в Azure AD, вы должны tooadd Amazon Web Services (AWS) из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a7508-124">tooconfigure hello integration of Amazon Web Services (AWS) into Azure AD, you need tooadd Amazon Web Services (AWS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a7508-125">**tooadd Amazon Web Services (AWS) из коллекции hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a7508-125">**tooadd Amazon Web Services (AWS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7508-126">В hello  **[портала Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a7508-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7508-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a7508-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a7508-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7508-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a7508-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a7508-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a7508-133">Введите в поле поиска hello **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="a7508-133">In hello search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="a7508-135">В панели результатов hello выберите **Amazon Web Services (AWS)**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a7508-135">In hello results panel, select **Amazon Web Services (AWS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7508-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7508-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7508-138">В этом разделе описана настройка и проверка единого входа Azure AD в Amazon Web Services (AWS) с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7508-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7508-139">Для единого входа toowork Azure AD необходима tooknow какие пользователь аналог hello в Amazon Web Services (AWS) является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7508-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Amazon Web Services (AWS) is tooa user in Azure AD.</span></span> <span data-ttu-id="a7508-140">Иными словами связи между пользователя Azure AD и связанных пользователей hello в Amazon Web Services (AWS) необходимо установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a7508-140">In other words, a link relationship between an Azure AD user and hello related user in Amazon Web Services (AWS) needs toobe established.</span></span>

<span data-ttu-id="a7508-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="a7508-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="a7508-142">tooconfigure и тестирования Azure AD единого входа с Amazon Web Services (AWS), необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a7508-142">tooconfigure and test Azure AD single sign-on with Amazon Web Services (AWS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a7508-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a7508-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a7508-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a7508-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7508-145">**[Создание тестового пользователя, прошедшего Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave аналог Саймон Britta в Amazon Web Services (AWS), являющийся представлением ей связанного toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7508-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - toohave a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="a7508-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a7508-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7508-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a7508-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7508-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7508-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7508-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="a7508-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="a7508-150">**tooconfigure Azure AD единого входа с Amazon Web Services (AWS), выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a7508-150">**tooconfigure Azure AD single sign-on with Amazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="a7508-151">В hello портале Azure на hello **Amazon Web Services (AWS)** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a7508-151">In hello Azure Portal, on hello **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a7508-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a7508-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="a7508-155">На hello **Amazon Web Services (AWS) доменов и URL-адреса** статьи, hello пользователь не имеет tooperform все меры как приложение hello уже заранее интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="a7508-155">On hello **Amazon Web Services (AWS) Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="a7508-157">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a7508-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="a7508-159">Hello Amazon Web Services (AWS) приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="a7508-159">hello Amazon Web Services (AWS) Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="a7508-160">Выполните настройку следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a7508-160">Please configure hello following claims for this application.</span></span> <span data-ttu-id="a7508-161">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="a7508-161">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="a7508-162">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="a7508-162">hello following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="a7508-164">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="a7508-164">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="a7508-165">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="a7508-165">Attribute Name</span></span>  | <span data-ttu-id="a7508-166">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="a7508-166">Attribute Value</span></span> | <span data-ttu-id="a7508-167">Пространство имен</span><span class="sxs-lookup"><span data-stu-id="a7508-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="a7508-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="a7508-168">RoleSessionName</span></span> | <span data-ttu-id="a7508-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="a7508-169">user.userprincipalname</span></span> | <span data-ttu-id="a7508-170">https://aws.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="a7508-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="a7508-171">Роль</span><span class="sxs-lookup"><span data-stu-id="a7508-171">Role</span></span>            | <span data-ttu-id="a7508-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="a7508-172">user.assignedroles</span></span> |  <span data-ttu-id="a7508-173">https://aws.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="a7508-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="a7508-174">Необходимо tooconfigure hello Подготовка пользователя к Azure AD toofetch все роли hello из консоли AWS.</span><span class="sxs-lookup"><span data-stu-id="a7508-174">You need tooconfigure hello user provisioning in Azure AD toofetch all hello roles from AWS Console.</span></span> <span data-ttu-id="a7508-175">См. шаги подготовки hello.</span><span class="sxs-lookup"><span data-stu-id="a7508-175">Please refer hello provisioning steps below.</span></span>

    <span data-ttu-id="a7508-176">а.</span><span class="sxs-lookup"><span data-stu-id="a7508-176">a.</span></span> <span data-ttu-id="a7508-177">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a7508-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="a7508-179">b.</span><span class="sxs-lookup"><span data-stu-id="a7508-179">b.</span></span> <span data-ttu-id="a7508-180">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="a7508-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a7508-182">c.</span><span class="sxs-lookup"><span data-stu-id="a7508-182">c.</span></span> <span data-ttu-id="a7508-183">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="a7508-183">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="a7508-184">Добавьте значение пространства имен hello, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="a7508-184">Add hello Namespace value as given above.</span></span>
    
    <span data-ttu-id="a7508-185">d.</span><span class="sxs-lookup"><span data-stu-id="a7508-185">d.</span></span> <span data-ttu-id="a7508-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a7508-186">Click **Ok**.</span></span>

7. <span data-ttu-id="a7508-187">Нажмите кнопку **Сохранить** кнопку Параметры toosave hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="a7508-187">Click **Save** button toosave hello settings on Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a7508-189">В другом окне браузера, tooyour входа на сайт компании Amazon Web Services (AWS) от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="a7508-189">In a different browser window, sign-on tooyour Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="a7508-190">Щелкните **Console Home**(Домашняя страница консоли).</span><span class="sxs-lookup"><span data-stu-id="a7508-190">Click **Console Home**.</span></span>
   
    ![Настройка единого входа][11]

10. <span data-ttu-id="a7508-192">Щелкните **IAM** в службе **Security, Identity & Compliance** (Безопасность, удостоверения и соответствие требованиям).</span><span class="sxs-lookup"><span data-stu-id="a7508-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Настройка единого входа][12]

11. <span data-ttu-id="a7508-194">Щелкните **Identity Providers** (Поставщики удостоверений), затем щелкните **Create Provider** (Создать поставщик).</span><span class="sxs-lookup"><span data-stu-id="a7508-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Настройка единого входа][13]

12. <span data-ttu-id="a7508-196">На hello **настроить поставщик** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a7508-196">On hello **Configure Provider** dialog page, perform hello following steps:</span></span>
   
    ![Настройка единого входа][14]
 
    <span data-ttu-id="a7508-198">а.</span><span class="sxs-lookup"><span data-stu-id="a7508-198">a.</span></span> <span data-ttu-id="a7508-199">Выберите для параметра **Тип поставщика** значение **SAML**.</span><span class="sxs-lookup"><span data-stu-id="a7508-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="a7508-200">b.</span><span class="sxs-lookup"><span data-stu-id="a7508-200">b.</span></span> <span data-ttu-id="a7508-201">В hello **имя поставщика** текстовом поле введите имя поставщика (например: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="a7508-201">In hello **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="a7508-202">c.</span><span class="sxs-lookup"><span data-stu-id="a7508-202">c.</span></span> <span data-ttu-id="a7508-203">tooupload скачанный файл метаданных, щелкните **выбрать файл**.</span><span class="sxs-lookup"><span data-stu-id="a7508-203">tooupload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="a7508-204">d.</span><span class="sxs-lookup"><span data-stu-id="a7508-204">d.</span></span> <span data-ttu-id="a7508-205">Щелкните **Следующий шаг**.</span><span class="sxs-lookup"><span data-stu-id="a7508-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="a7508-206">На hello **проверить сведения о поставщике** странице диалогового окна щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="a7508-206">On hello **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Настройка единого входа][15]

14. <span data-ttu-id="a7508-208">Щелкните **Roles** (Роли), а затем нажмите кнопку **Create New Role** (Создать новую роль).</span><span class="sxs-lookup"><span data-stu-id="a7508-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Настройка единого входа][16]

15. <span data-ttu-id="a7508-210">На hello **задать имя роли** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a7508-210">On hello **Set Role Name** dialog, perform hello following steps:</span></span> 
    
    ![Настройка единого входа][17] 

    <span data-ttu-id="a7508-212">а.</span><span class="sxs-lookup"><span data-stu-id="a7508-212">a.</span></span> <span data-ttu-id="a7508-213">В hello **имя роли** текстовом поле введите имя роли (например: *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="a7508-213">In hello **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="a7508-214">b.</span><span class="sxs-lookup"><span data-stu-id="a7508-214">b.</span></span> <span data-ttu-id="a7508-215">Щелкните **Следующий шаг**.</span><span class="sxs-lookup"><span data-stu-id="a7508-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="a7508-216">На hello **выберите тип роли** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a7508-216">On hello **Select Role Type** dialog, perform hello following steps:</span></span> 
    
    ![Настройка единого входа][18] 

    <span data-ttu-id="a7508-218">а.</span><span class="sxs-lookup"><span data-stu-id="a7508-218">a.</span></span> <span data-ttu-id="a7508-219">Выберите **Роль для доступа поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="a7508-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="a7508-220">b.</span><span class="sxs-lookup"><span data-stu-id="a7508-220">b.</span></span> <span data-ttu-id="a7508-221">В hello **предоставление единого входа через Интернет (WebSSO) поставщики доступа к tooSAML** щелкните **выберите**.</span><span class="sxs-lookup"><span data-stu-id="a7508-221">In hello **Grant Web Single Sign-On (WebSSO) access tooSAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="a7508-222">На hello **установления доверия** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a7508-222">On hello **Establish Trust** dialog, perform hello following steps:</span></span>  
    
    ![Настройка единого входа][19] 

    <span data-ttu-id="a7508-224">а.</span><span class="sxs-lookup"><span data-stu-id="a7508-224">a.</span></span> <span data-ttu-id="a7508-225">В качестве поставщика SAML выбрать поставщика SAML hello, вы создали ранее (например: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="a7508-225">As SAML provider, select hello SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="a7508-226">b.</span><span class="sxs-lookup"><span data-stu-id="a7508-226">b.</span></span> <span data-ttu-id="a7508-227">Щелкните **Следующий шаг**.</span><span class="sxs-lookup"><span data-stu-id="a7508-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="a7508-228">На hello **проверить доверие роли** диалоговое окно, нажмите кнопку **следующий шаг**.</span><span class="sxs-lookup"><span data-stu-id="a7508-228">On hello **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Настройка единого входа][32]

19. <span data-ttu-id="a7508-230">На hello **политики присоединения** диалоговое окно, нажмите кнопку **следующий шаг**.</span><span class="sxs-lookup"><span data-stu-id="a7508-230">On hello **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Настройка единого входа][33]

20. <span data-ttu-id="a7508-232">На hello **проверки** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a7508-232">On hello **Review** dialog, perform hello following steps:</span></span>
    
    ![Настройка единого входа][34]
 
    <span data-ttu-id="a7508-234">а.</span><span class="sxs-lookup"><span data-stu-id="a7508-234">a.</span></span> <span data-ttu-id="a7508-235">Щелкните **Создать роль**.</span><span class="sxs-lookup"><span data-stu-id="a7508-235">Click **Create Role**.</span></span>

    <span data-ttu-id="a7508-236">b.</span><span class="sxs-lookup"><span data-stu-id="a7508-236">b.</span></span> <span data-ttu-id="a7508-237">Создайте столько ролей и сопоставить их toohello поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="a7508-237">Create as many roles as needed and map them toohello Identity Provider.</span></span>

21. <span data-ttu-id="a7508-238">Теперь настройки hello подготовки пользователей toofetch все роли hello из AWS</span><span class="sxs-lookup"><span data-stu-id="a7508-238">Now configure hello user provisioning toofetch all hello roles from AWS</span></span>

    <span data-ttu-id="a7508-239">а.</span><span class="sxs-lookup"><span data-stu-id="a7508-239">a.</span></span> <span data-ttu-id="a7508-240">В имени входа консоли AWS hello с вашей учетной записи root</span><span class="sxs-lookup"><span data-stu-id="a7508-240">In hello AWS Console login with your root account</span></span>

    <span data-ttu-id="a7508-241">b.</span><span class="sxs-lookup"><span data-stu-id="a7508-241">b.</span></span> <span data-ttu-id="a7508-242">В hello правом верхнем углу щелкните свое имя и нажмите кнопку hello **мои учетные данные безопасности** параметр.</span><span class="sxs-lookup"><span data-stu-id="a7508-242">In hello top right corner click your name and then click hello **My Security Credentials** option.</span></span> <span data-ttu-id="a7508-243">Откроется экран с предупреждением.</span><span class="sxs-lookup"><span data-stu-id="a7508-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="a7508-244">Нажмите кнопку "hello" **учетные данные безопасности** toopass кнопку hello экрана.</span><span class="sxs-lookup"><span data-stu-id="a7508-244">Click hello button **Security Credentials** button toopass hello screen.</span></span>
        
       ![Настройка единого входа][36]

       ![Настройка единого входа][37]

    <span data-ttu-id="a7508-247">c.</span><span class="sxs-lookup"><span data-stu-id="a7508-247">c.</span></span> <span data-ttu-id="a7508-248">В hello ключи доступа нажмите кнопку hello **создать новый ключ доступа** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a7508-248">In hello Access Keys section click hello **Create New Access Key** button.</span></span> <span data-ttu-id="a7508-249">Это приводит к возникновению ошибки hello кода доступа и значение маркера.</span><span class="sxs-lookup"><span data-stu-id="a7508-249">This generates hello Access Key ID and a token value.</span></span>
    
       ![Настройка единого входа][38]

    <span data-ttu-id="a7508-251">d.</span><span class="sxs-lookup"><span data-stu-id="a7508-251">d.</span></span> <span data-ttu-id="a7508-252">Скопируйте оба эти значения, а также скачайте их, чтобы не потерять.</span><span class="sxs-lookup"><span data-stu-id="a7508-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="a7508-253">д.</span><span class="sxs-lookup"><span data-stu-id="a7508-253">e.</span></span> <span data-ttu-id="a7508-254">В hello портале Azure на странице интеграции приложения hello Amazon Web Services (AWS), щелкните **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="a7508-254">In hello Azure Portal, on hello Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Настройка единого входа][35]

    <span data-ttu-id="a7508-256">f.</span><span class="sxs-lookup"><span data-stu-id="a7508-256">f.</span></span> <span data-ttu-id="a7508-257">Установить режим подготовки hello слишком**автоматический**</span><span class="sxs-lookup"><span data-stu-id="a7508-257">Set hello Provisioning mode too**Automatic**</span></span>
        
       ![Настройка единого входа][39]

    <span data-ttu-id="a7508-259">ж.</span><span class="sxs-lookup"><span data-stu-id="a7508-259">g.</span></span> <span data-ttu-id="a7508-260">Теперь в hello **clientsecret** и **секрет маркера** вставьте hello соответствующего значения, которые вы скопировали из консоли AWS.</span><span class="sxs-lookup"><span data-stu-id="a7508-260">Now in hello **clientsecret** and **Secret Token** paste hello corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="a7508-261">h.</span><span class="sxs-lookup"><span data-stu-id="a7508-261">h.</span></span> <span data-ttu-id="a7508-262">Можно щелкнуть hello **проверить подключение** кнопку tootest hello подключения.</span><span class="sxs-lookup"><span data-stu-id="a7508-262">You can click hello **Test Connection** button tootest hello connectivity.</span></span> <span data-ttu-id="a7508-263">После успешной можно запустить hello подготовки соединителя.</span><span class="sxs-lookup"><span data-stu-id="a7508-263">Once that is successful then you can start hello provisioning connector.</span></span>
       
       ![Настройка единого входа][40]

    <span data-ttu-id="a7508-265">i.</span><span class="sxs-lookup"><span data-stu-id="a7508-265">i.</span></span> <span data-ttu-id="a7508-266">Теперь включить hello состояние подготовки слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="a7508-266">Now enable hello Provisioning Status too**On**.</span></span> <span data-ttu-id="a7508-267">Запустится выборка hello ролей из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a7508-267">This starts fetching hello roles from hello application.</span></span>

       ![Настройка единого входа][41]

    > [!NOTE]
    > <span data-ttu-id="a7508-269">Запускается служба Azure AD подготовки каждой после некоторых ролей hello время toosync из AWS.</span><span class="sxs-lookup"><span data-stu-id="a7508-269">Azure AD Provisioning service runs every after some time toosync hello roles from AWS.</span></span> <span data-ttu-id="a7508-270">Вы увидите все hello поставщика удостоверений присоединенного AWS роли в Azure AD, и их можно использовать при назначении toousers приложения hello или группы.</span><span class="sxs-lookup"><span data-stu-id="a7508-270">You should see all hello Identity Provider attached AWS roles into Azure AD and you can use them while assigning hello application toousers or groups.</span></span>

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7508-271">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7508-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7508-272">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a7508-272">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a7508-274">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a7508-274">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7508-275">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a7508-275">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7508-277">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="a7508-277">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7508-279">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a7508-279">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7508-281">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a7508-281">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7508-283">а.</span><span class="sxs-lookup"><span data-stu-id="a7508-283">a.</span></span> <span data-ttu-id="a7508-284">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7508-284">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7508-285">b.</span><span class="sxs-lookup"><span data-stu-id="a7508-285">b.</span></span> <span data-ttu-id="a7508-286">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7508-286">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7508-287">c.</span><span class="sxs-lookup"><span data-stu-id="a7508-287">c.</span></span> <span data-ttu-id="a7508-288">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="a7508-288">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a7508-289">d.</span><span class="sxs-lookup"><span data-stu-id="a7508-289">d.</span></span> <span data-ttu-id="a7508-290">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7508-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="a7508-291">Создание тестового пользователя Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="a7508-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="a7508-292">В порядке tooenable toolog пользователей Azure AD в tooAmazon Web Services (AWS) их необходимо подготовить в Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="a7508-292">In order tooenable Azure AD users toolog in tooAmazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="a7508-293">В случае hello Amazon Web Services (AWS) Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="a7508-293">In hello case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="a7508-294">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a7508-294">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7508-295">Войдите в tooyour **Amazon Web Services (AWS)** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="a7508-295">Log in tooyour **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="a7508-296">Нажмите кнопку hello **Главная страница консоли** значок.</span><span class="sxs-lookup"><span data-stu-id="a7508-296">Click hello **Console Home** icon.</span></span> 
   
    ![Настройка единого входа][11]

3. <span data-ttu-id="a7508-298">Щелкните Identity and Access Management (Управление удостоверениями и доступом).</span><span class="sxs-lookup"><span data-stu-id="a7508-298">Click Identity and Access Management.</span></span> 
   
    ![Настройка единого входа][28]

4. <span data-ttu-id="a7508-300">Hello панели мониторинга, щелкните **пользователей**, а затем нажмите кнопку **создания новых пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a7508-300">In hello Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Настройка единого входа][29]

5. <span data-ttu-id="a7508-302">В диалоговом окне приветствия создать пользователя выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="a7508-302">On hello Create User dialog, perform hello following steps:</span></span> 
   
    ![Настройка единого входа][30]   
    
    <span data-ttu-id="a7508-304">а.</span><span class="sxs-lookup"><span data-stu-id="a7508-304">a.</span></span> <span data-ttu-id="a7508-305">В hello **введите имена пользователей** текстовые поля, введите имя пользователя Саймон Brita (userprincipalname) в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7508-305">In hello **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="a7508-306">b.</span><span class="sxs-lookup"><span data-stu-id="a7508-306">b.</span></span> <span data-ttu-id="a7508-307">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7508-307">Click **Create.**</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a7508-308">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a7508-308">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a7508-309">В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooAmazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="a7508-309">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAmazon Web Services (AWS).</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a7508-311">**tooassign tooAmazon Britta Simon Web Services (AWS) выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="a7508-311">**tooassign Britta Simon tooAmazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="a7508-312">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7508-312">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a7508-314">В списке приложений hello выберите **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="a7508-314">In hello applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="a7508-316">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a7508-316">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a7508-318">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7508-318">Click **Add** button.</span></span> <span data-ttu-id="a7508-319">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a7508-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a7508-321">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a7508-321">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a7508-322">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a7508-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7508-323">На **выберите роль** вкладке, выберите hello соответствующую роль для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="a7508-323">On **Select Role** tab, select hello appropriate role for hello user.</span></span> <span data-ttu-id="a7508-324">Эти роли обозначаются hello имя роли и имя поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="a7508-324">All these roles are shown with hello role name and identity provider name.</span></span> <span data-ttu-id="a7508-325">Таким образом, можно легко определить роли hello из AWS.</span><span class="sxs-lookup"><span data-stu-id="a7508-325">This way you can easily identify hello roles from AWS.</span></span>

8. <span data-ttu-id="a7508-326">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a7508-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7508-327">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a7508-327">Testing single sign-on</span></span>

<span data-ttu-id="a7508-328">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="a7508-328">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a7508-329">При нажатии кнопки приветствия Amazon Web Services (AWS) плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour приложения Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="a7508-329">When you click hello Amazon Web Services (AWS) tile in hello Access Panel, you should get automatically signed-on tooyour Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a7508-330">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a7508-330">Additional resources</span></span>

* [<span data-ttu-id="a7508-331">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7508-331">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7508-332">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7508-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
