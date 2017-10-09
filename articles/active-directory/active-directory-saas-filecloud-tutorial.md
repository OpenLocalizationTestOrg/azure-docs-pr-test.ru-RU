---
title: "Учебник. Интеграция Azure Active Directory с FileCloud | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и FileCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: fe58d01f02d6ce99ee9e2f83e7dc72c4434e13b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="6da5b-103">Учебник. Интеграция Azure Active Directory с FileCloud</span><span class="sxs-lookup"><span data-stu-id="6da5b-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="6da5b-104">В этом учебнике вы узнаете, как toointegrate FileCloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6da5b-104">In this tutorial, you learn how toointegrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6da5b-105">Интеграция с Azure AD FileCloud предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="6da5b-105">Integrating FileCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6da5b-106">Можно управлять в Azure AD, имеющего доступ tooFileCloud.</span><span class="sxs-lookup"><span data-stu-id="6da5b-106">You can control in Azure AD who has access tooFileCloud.</span></span>
- <span data-ttu-id="6da5b-107">Можно включить на пользователей tooautomatically get вошедшего tooFileCloud (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6da5b-107">You can enable your users tooautomatically get signed-on tooFileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6da5b-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6da5b-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6da5b-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6da5b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6da5b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6da5b-110">Prerequisites</span></span>

<span data-ttu-id="6da5b-111">tooconfigure интеграция Azure AD с FileCloud требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="6da5b-111">tooconfigure Azure AD integration with FileCloud, you need hello following items:</span></span>

- <span data-ttu-id="6da5b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="6da5b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6da5b-113">подписка FileCloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="6da5b-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6da5b-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="6da5b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6da5b-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="6da5b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6da5b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="6da5b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6da5b-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6da5b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6da5b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="6da5b-118">Scenario description</span></span>
<span data-ttu-id="6da5b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="6da5b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6da5b-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="6da5b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6da5b-121">Добавление FileCloud из галереи hello</span><span class="sxs-lookup"><span data-stu-id="6da5b-121">Adding FileCloud from hello gallery</span></span>
2. <span data-ttu-id="6da5b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6da5b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-hello-gallery"></a><span data-ttu-id="6da5b-123">Добавление FileCloud из галереи hello</span><span class="sxs-lookup"><span data-stu-id="6da5b-123">Adding FileCloud from hello gallery</span></span>
<span data-ttu-id="6da5b-124">tooconfigure hello интеграции FileCloud в Azure AD, вы должны tooadd FileCloud из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="6da5b-124">tooconfigure hello integration of FileCloud into Azure AD, you need tooadd FileCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6da5b-125">**tooadd FileCloud из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6da5b-125">**tooadd FileCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6da5b-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="6da5b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="6da5b-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6da5b-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="6da5b-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="6da5b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="6da5b-133">Введите в поле поиска hello **FileCloud**выберите **FileCloud** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6da5b-133">In hello search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button tooadd hello application.</span></span>

    ![FileCloud в списке результатов hello](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6da5b-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6da5b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6da5b-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение FileCloud с помощью тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6da5b-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6da5b-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в FileCloud является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6da5b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FileCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="6da5b-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в FileCloud должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="6da5b-138">In other words, a link relationship between an Azure AD user and hello related user in FileCloud needs toobe established.</span></span>

<span data-ttu-id="6da5b-139">В FileCloud, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="6da5b-139">In FileCloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6da5b-140">tooconfigure и теста Azure AD единого входа с FileCloud, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6da5b-140">tooconfigure and test Azure AD single sign-on with FileCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6da5b-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="6da5b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6da5b-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="6da5b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6da5b-143">**[Создание тестового пользователя FileCloud](#create-a-filecloud-test-user)**  -toohave аналог Саймон Britta в FileCloud, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="6da5b-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - toohave a counterpart of Britta Simon in FileCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6da5b-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="6da5b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6da5b-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6da5b-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6da5b-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="6da5b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6da5b-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении FileCloud.</span><span class="sxs-lookup"><span data-stu-id="6da5b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="6da5b-148">**tooconfigure Azure AD единого входа с FileCloud, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6da5b-148">**tooconfigure Azure AD single sign-on with FileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="6da5b-149">В hello в hello портала Azure **FileCloud** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-149">In hello Azure portal, on hello **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="6da5b-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="6da5b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="6da5b-153">На hello **URL-адреса и домена FileCloud** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6da5b-153">On hello **FileCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="6da5b-155">а.</span><span class="sxs-lookup"><span data-stu-id="6da5b-155">a.</span></span> <span data-ttu-id="6da5b-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="6da5b-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="6da5b-157">b.</span><span class="sxs-lookup"><span data-stu-id="6da5b-157">b.</span></span> <span data-ttu-id="6da5b-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="6da5b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6da5b-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="6da5b-159">These values are not real.</span></span> <span data-ttu-id="6da5b-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="6da5b-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6da5b-161">Обратитесь к [группа поддержки клиента FileCloud](mailto:support@codelathe.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="6da5b-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) tooget these values.</span></span>

4. <span data-ttu-id="6da5b-162">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="6da5b-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="6da5b-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="6da5b-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6da5b-166">На hello **конфигурации FileCloud** щелкните **Настройка FileCloud** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="6da5b-166">On hello **FileCloud Configuration** section, click **Configure FileCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6da5b-167">Копировать hello **идентификатор сущности SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="6da5b-167">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Настройка FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="6da5b-169">В другом окне браузера, клиент FileCloud tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="6da5b-169">In a different web browser window, sign-on tooyour FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="6da5b-170">На панели навигации слева hello, нажмите кнопку **параметры**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-170">On hello left navigation pane, click **Settings**.</span></span> 
   
    ![Раздел "Settings" (Параметры) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="6da5b-172">Щелкните вкладку **SSO** (Единый вход) в разделе "Settings" (Параметры).</span><span class="sxs-lookup"><span data-stu-id="6da5b-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Вкладка "Single Sign-On" (Единый вход) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="6da5b-174">На панели **Single Sign On (SSO) Settings** (Параметры единого входа) для параметра **Default SSO Type** (Тип единого входа по умолчанию) выберите значение **SAML**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Панель "Single Sign-On Settings" (Параметры единого входа) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="6da5b-176">Вставить **идентификатор сущности SAML**, который вы скопировали из портала Azure в hello **URL-адрес конечной точки поставщика удостоверений** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="6da5b-176">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP End Point URL** textbox.</span></span>

    ![Текстовое поле "IDP End Point URL" (URL-адрес конечной точки IDP)](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="6da5b-178">Откройте скачанный файл метаданных в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **метаданные поставщика удостоверений** текстового поля на **параметры SAML** панель.</span><span class="sxs-lookup"><span data-stu-id="6da5b-178">Open your downloaded metadata file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Раздел "IDP Meta Data" (Метаданные IDP) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="6da5b-180">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="6da5b-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="6da5b-181">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="6da5b-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6da5b-182">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="6da5b-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6da5b-183">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6da5b-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6da5b-184">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6da5b-184">Create an Azure AD test user</span></span>

<span data-ttu-id="6da5b-185">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6da5b-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="6da5b-187">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6da5b-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6da5b-188">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6da5b-188">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6da5b-190">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-190">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6da5b-192">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="6da5b-192">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6da5b-194">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6da5b-194">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6da5b-196">а.</span><span class="sxs-lookup"><span data-stu-id="6da5b-196">a.</span></span> <span data-ttu-id="6da5b-197">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-197">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6da5b-198">b.</span><span class="sxs-lookup"><span data-stu-id="6da5b-198">b.</span></span> <span data-ttu-id="6da5b-199">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="6da5b-199">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6da5b-200">c.</span><span class="sxs-lookup"><span data-stu-id="6da5b-200">c.</span></span> <span data-ttu-id="6da5b-201">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="6da5b-201">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6da5b-202">d.</span><span class="sxs-lookup"><span data-stu-id="6da5b-202">d.</span></span> <span data-ttu-id="6da5b-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="6da5b-204">Создание тестового пользователя FileCloud</span><span class="sxs-lookup"><span data-stu-id="6da5b-204">Create a FileCloud test user</span></span>

<span data-ttu-id="6da5b-205">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в FileCloud.</span><span class="sxs-lookup"><span data-stu-id="6da5b-205">hello objective of this section is toocreate a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="6da5b-206">FileCloud поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6da5b-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="6da5b-207">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="6da5b-207">There is no action item for you in this section.</span></span> <span data-ttu-id="6da5b-208">Новый пользователь создается во время попытки tooaccess FileCloud, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="6da5b-208">A new user is created during an attempt tooaccess FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="6da5b-209">Если требуется toocreate пользователя вручную, необходимо toocontact hello [FileCloud клиента поддержки](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="6da5b-209">If you need toocreate a user manually, you need toocontact hello [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6da5b-210">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="6da5b-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6da5b-211">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooFileCloud доступа.</span><span class="sxs-lookup"><span data-stu-id="6da5b-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFileCloud.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="6da5b-213">**tooassign tooFileCloud Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6da5b-213">**tooassign Britta Simon tooFileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="6da5b-214">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="6da5b-216">В списке приложений hello выберите **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-216">In hello applications list, select **FileCloud**.</span></span>

    ![ссылка FileCloud Hello в списке приложений hello](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="6da5b-218">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="6da5b-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-220">Click **Add** button.</span></span> <span data-ttu-id="6da5b-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="6da5b-223">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="6da5b-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6da5b-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6da5b-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="6da5b-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6da5b-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="6da5b-226">Test single sign-on</span></span>

<span data-ttu-id="6da5b-227">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="6da5b-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="6da5b-228">При нажатии кнопки hello FileCloud плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour FileCloud приложения.</span><span class="sxs-lookup"><span data-stu-id="6da5b-228">When you click hello FileCloud tile in hello Access Panel, you should get automatically signed-on tooyour FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6da5b-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6da5b-229">Additional resources</span></span>

* [<span data-ttu-id="6da5b-230">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6da5b-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6da5b-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6da5b-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

