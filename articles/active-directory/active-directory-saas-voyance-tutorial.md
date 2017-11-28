---
title: "Руководство по интеграции Azure Active Directory с Voyance | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="7f973-103">Руководство по интеграции Azure Active Directory с Voyance</span><span class="sxs-lookup"><span data-stu-id="7f973-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="7f973-104">В этом учебнике вы узнаете, как toointegrate Voyance с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f973-104">In this tutorial, you learn how toointegrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f973-105">Интеграция с Azure AD Voyance предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7f973-105">Integrating Voyance with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7f973-106">Можно управлять в Azure AD, имеющего доступ tooVoyance</span><span class="sxs-lookup"><span data-stu-id="7f973-106">You can control in Azure AD who has access tooVoyance</span></span>
- <span data-ttu-id="7f973-107">Можно включить на пользователей tooautomatically get вошедшего tooVoyance (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f973-107">You can enable your users tooautomatically get signed-on tooVoyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7f973-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7f973-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7f973-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f973-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f973-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7f973-110">Prerequisites</span></span>

<span data-ttu-id="7f973-111">tooconfigure интеграция Azure AD с Voyance требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7f973-111">tooconfigure Azure AD integration with Voyance, you need hello following items:</span></span>

- <span data-ttu-id="7f973-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7f973-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f973-113">подписка Voyance с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f973-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f973-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7f973-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f973-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7f973-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f973-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7f973-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f973-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f973-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f973-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7f973-118">Scenario description</span></span>
<span data-ttu-id="7f973-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7f973-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f973-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7f973-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f973-121">Добавление Voyance из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7f973-121">Adding Voyance from hello gallery</span></span>
2. <span data-ttu-id="7f973-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f973-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-hello-gallery"></a><span data-ttu-id="7f973-123">Добавление Voyance из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7f973-123">Adding Voyance from hello gallery</span></span>
<span data-ttu-id="7f973-124">tooconfigure hello интеграции Voyance в Azure AD, вы должны tooadd Voyance из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7f973-124">tooconfigure hello integration of Voyance into Azure AD, you need tooadd Voyance from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7f973-125">**tooadd Voyance из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7f973-125">**tooadd Voyance from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f973-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7f973-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="7f973-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="7f973-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7f973-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7f973-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="7f973-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7f973-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="7f973-133">Введите в поле поиска hello **Voyance**выберите **Voyance** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f973-133">In hello search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Voyance в списке результатов hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7f973-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f973-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7f973-136">В этом разделе описана настройка и проверка единого входа Azure AD в Voyance с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f973-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f973-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Voyance является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f973-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Voyance is tooa user in Azure AD.</span></span> <span data-ttu-id="7f973-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Voyance должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7f973-138">In other words, a link relationship between an Azure AD user and hello related user in Voyance needs toobe established.</span></span>

<span data-ttu-id="7f973-139">В Voyance, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="7f973-139">In Voyance, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7f973-140">tooconfigure и теста Azure AD единого входа с Voyance, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7f973-140">tooconfigure and test Azure AD single sign-on with Voyance, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7f973-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7f973-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7f973-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7f973-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f973-143">**[Создание тестового пользователя Voyance](#create-a-voyance-test-user)**  -toohave аналог Саймон Britta в Voyance, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f973-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - toohave a counterpart of Britta Simon in Voyance that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f973-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7f973-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f973-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7f973-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7f973-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f973-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7f973-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Voyance.</span><span class="sxs-lookup"><span data-stu-id="7f973-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="7f973-148">**tooconfigure Azure AD единого входа с Voyance, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7f973-148">**tooconfigure Azure AD single sign-on with Voyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f973-149">В hello в hello портала Azure **Voyance** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7f973-149">In hello Azure portal, on hello **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="7f973-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f973-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="7f973-153">На hello **Voyance доменов и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="7f973-153">On hello **Voyance Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа Voyance для поставщика удостоверений](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="7f973-155">а.</span><span class="sxs-lookup"><span data-stu-id="7f973-155">a.</span></span> <span data-ttu-id="7f973-156">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="7f973-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="7f973-157">b.</span><span class="sxs-lookup"><span data-stu-id="7f973-157">b.</span></span> <span data-ttu-id="7f973-158">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="7f973-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="7f973-159">Проверьте **Показывать дополнительные параметры URL-адреса** и выполните следующий шаг при желании tooconfigure приложения hello в hello **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="7f973-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа Voyance для поставщика услуг](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="7f973-161">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="7f973-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7f973-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="7f973-162">These values are not real.</span></span> <span data-ttu-id="7f973-163">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="7f973-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7f973-164">Обратитесь к [группа поддержки клиента Voyance](mailto:support@nyansa.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="7f973-164">Contact [Voyance Client support team](mailto:support@nyansa.com) tooget these values.</span></span> 

5. <span data-ttu-id="7f973-165">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="7f973-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="7f973-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7f973-167">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="7f973-169">На hello **конфигурации Voyance** щелкните **Настройка Voyance** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="7f973-169">On hello **Voyance Configuration** section, click **Configure Voyance** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7f973-170">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="7f973-170">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="7f973-172">В другом окне браузера, клиент Voyance tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="7f973-172">In a different web browser window, sign-on tooyour Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="7f973-173">Перейдите toohello правом верхнем углу панели навигации hello и щелкните hello раскрывающийся список с надписью «**университета Acme**».</span><span class="sxs-lookup"><span data-stu-id="7f973-173">Go toohello top right corner of hello navigation bar and click on hello drop-down that says "**Acme University**".</span></span>
    
    ![Настройка единого входа на стороне приложения. Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="7f973-175">Щелкните **Admin Settings** (Параметры администрирования).</span><span class="sxs-lookup"><span data-stu-id="7f973-175">Click "**Admin Settings**".</span></span>

    ![Настройка единого входа на стороне приложения. Параметры администрирования](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="7f973-177">Щелкните вкладку **User Access** (Доступ пользователей).</span><span class="sxs-lookup"><span data-stu-id="7f973-177">Click "**User Access**" tab.</span></span>

    ![Настройка единого входа на стороне приложения. Доступ пользователей](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="7f973-179">Щелкните hello»**единого входа отключена**"tooconfigure кнопку Azure AD как поставщика удостоверений с помощью SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="7f973-179">Click hello "**SSO is disabled**" button tooconfigure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Настройка единого входа на стороне приложения. Кнопка SSO is disabled (Единый вход отключен)](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="7f973-181">Go слишком**SAML v2** раздел и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7f973-181">Go too**SAML v2** section and perform below steps:</span></span>

    ![Настройка единого входа на стороне приложения. SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="7f973-183">а.</span><span class="sxs-lookup"><span data-stu-id="7f973-183">a.</span></span> <span data-ttu-id="7f973-184">Щелкните **Включено**.</span><span class="sxs-lookup"><span data-stu-id="7f973-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="7f973-185">b.</span><span class="sxs-lookup"><span data-stu-id="7f973-185">b.</span></span> <span data-ttu-id="7f973-186">Вставить **SAML единого входа URL-адрес службы**, которого вы скопировали из портала Azure hello в hello **URL-адрес входа поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="7f973-186">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal Into hello **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="7f973-187">c.</span><span class="sxs-lookup"><span data-stu-id="7f973-187">c.</span></span> <span data-ttu-id="7f973-188">Откройте загруженный сертификат в кодировке Base64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификата поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="7f973-188">Open your downloaded Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="7f973-189">d.</span><span class="sxs-lookup"><span data-stu-id="7f973-189">d.</span></span> <span data-ttu-id="7f973-190">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7f973-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7f973-191">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="7f973-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7f973-192">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="7f973-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7f973-193">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7f973-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7f973-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f973-194">Create an Azure AD test user</span></span>

<span data-ttu-id="7f973-195">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7f973-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="7f973-197">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7f973-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f973-198">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7f973-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7f973-200">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7f973-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7f973-202">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="7f973-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7f973-204">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7f973-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f973-206">а.</span><span class="sxs-lookup"><span data-stu-id="7f973-206">a.</span></span> <span data-ttu-id="7f973-207">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f973-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f973-208">b.</span><span class="sxs-lookup"><span data-stu-id="7f973-208">b.</span></span> <span data-ttu-id="7f973-209">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7f973-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f973-210">c.</span><span class="sxs-lookup"><span data-stu-id="7f973-210">c.</span></span> <span data-ttu-id="7f973-211">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="7f973-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7f973-212">d.</span><span class="sxs-lookup"><span data-stu-id="7f973-212">d.</span></span> <span data-ttu-id="7f973-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7f973-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="7f973-214">Создание тестового пользователя Voyance</span><span class="sxs-lookup"><span data-stu-id="7f973-214">Create a Voyance test user</span></span>

<span data-ttu-id="7f973-215">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Voyance.</span><span class="sxs-lookup"><span data-stu-id="7f973-215">hello objective of this section is toocreate a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="7f973-216">Приложение Voyance поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7f973-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="7f973-217">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="7f973-217">There is no action item for you in this section.</span></span> <span data-ttu-id="7f973-218">Новый пользователь создается во время попытки tooaccess Voyance, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="7f973-218">A new user is created during an attempt tooaccess Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="7f973-219">Если требуется toocreate пользователя вручную, необходимо toocontact [Voyance поддержки](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="7f973-219">If you need toocreate a user manually, you need toocontact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7f973-220">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7f973-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7f973-221">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooVoyance доступа.</span><span class="sxs-lookup"><span data-stu-id="7f973-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVoyance.</span></span>

![Назначение пользователям ролей hello][200]

<span data-ttu-id="7f973-223">**tooassign tooVoyance Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7f973-223">**tooassign Britta Simon tooVoyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f973-224">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7f973-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7f973-226">В списке приложений hello выберите **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="7f973-226">In hello applications list, select **Voyance**.</span></span>

    ![ссылка Voyance Hello в списке приложений hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="7f973-228">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="7f973-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="7f973-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7f973-230">Click **Add** button.</span></span> <span data-ttu-id="7f973-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7f973-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="7f973-233">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7f973-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7f973-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7f973-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f973-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7f973-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7f973-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7f973-236">Test single sign-on</span></span>

<span data-ttu-id="7f973-237">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="7f973-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7f973-238">При нажатии кнопки hello Voyance плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Voyance приложения.</span><span class="sxs-lookup"><span data-stu-id="7f973-238">When you click hello Voyance tile in hello Access Panel, you should get automatically signed-on tooyour Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7f973-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7f973-239">Additional resources</span></span>

* [<span data-ttu-id="7f973-240">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f973-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f973-241">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f973-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

