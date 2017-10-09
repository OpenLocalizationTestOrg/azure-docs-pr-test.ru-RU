---
title: "Руководство по интеграции Azure Active Directory с SAP Business ByDesign | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="9d6f0-103">Руководство по интеграции Azure Active Directory с SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="9d6f0-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="9d6f0-104">В этом учебнике вы узнаете, как toointegrate SAP Business ByDesign с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d6f0-104">In this tutorial, you learn how toointegrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d6f0-105">Интеграция SAP Business ByDesign с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9d6f0-105">Integrating SAP Business ByDesign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9d6f0-106">Можно управлять в Azure AD, имеющего доступ tooSAP ByDesign бизнеса.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-106">You can control in Azure AD who has access tooSAP Business ByDesign.</span></span>
- <span data-ttu-id="9d6f0-107">Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooSAP ByDesign бизнеса (Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="9d6f0-107">You can enable your users tooautomatically get signed-on tooSAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9d6f0-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="9d6f0-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d6f0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d6f0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9d6f0-110">Prerequisites</span></span>

<span data-ttu-id="9d6f0-111">tooconfigure интеграция Azure AD с SAP Business ByDesign требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="9d6f0-111">tooconfigure Azure AD integration with SAP Business ByDesign, you need hello following items:</span></span>

- <span data-ttu-id="9d6f0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9d6f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d6f0-113">подписка SAP Business ByDesign с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d6f0-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d6f0-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="9d6f0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d6f0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d6f0-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d6f0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d6f0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9d6f0-118">Scenario description</span></span>
<span data-ttu-id="9d6f0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d6f0-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="9d6f0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d6f0-121">Добавление SAP Business ByDesign из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9d6f0-121">Adding SAP Business ByDesign from hello gallery</span></span>
2. <span data-ttu-id="9d6f0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d6f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a><span data-ttu-id="9d6f0-123">Добавление SAP Business ByDesign из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9d6f0-123">Adding SAP Business ByDesign from hello gallery</span></span>
<span data-ttu-id="9d6f0-124">tooconfigure hello интеграции SAP Business ByDesign в Azure AD, вы должны tooadd SAP Business ByDesign из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-124">tooconfigure hello integration of SAP Business ByDesign into Azure AD, you need tooadd SAP Business ByDesign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9d6f0-125">**tooadd SAP Business ByDesign из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9d6f0-125">**tooadd SAP Business ByDesign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d6f0-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="9d6f0-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9d6f0-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="9d6f0-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="9d6f0-133">Введите в поле поиска hello **SAP Business ByDesign**выберите **SAP Business ByDesign** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-133">In hello search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button tooadd hello application.</span></span>

    ![SAP Business ByDesign в списке результатов hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9d6f0-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d6f0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9d6f0-136">В этом разделе описана настройка и проверка единого входа Azure AD в SAP Business ByDesign с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d6f0-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SAP Business ByDesign является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Business ByDesign is tooa user in Azure AD.</span></span> <span data-ttu-id="9d6f0-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в SAP Business ByDesign должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-138">In other words, a link relationship between an Azure AD user and hello related user in SAP Business ByDesign needs toobe established.</span></span>

<span data-ttu-id="9d6f0-139">В SAP Business ByDesign, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-139">In SAP Business ByDesign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9d6f0-140">tooconfigure и теста Azure AD единого входа с SAP Business ByDesign, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9d6f0-140">tooconfigure and test Azure AD single sign-on with SAP Business ByDesign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9d6f0-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9d6f0-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d6f0-143">**[Создание тестового пользователя, прошедшего SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  -toohave аналог Саймон Britta в SAP Business ByDesign, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - toohave a counterpart of Britta Simon in SAP Business ByDesign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d6f0-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d6f0-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9d6f0-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d6f0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9d6f0-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="9d6f0-148">**tooconfigure Azure AD единого входа с SAP Business ByDesign, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9d6f0-148">**tooconfigure Azure AD single sign-on with SAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d6f0-149">В hello в hello портала Azure **SAP Business ByDesign** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-149">In hello Azure portal, on hello **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="9d6f0-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="9d6f0-153">На hello **URL-адреса и домена ByDesign SAP Business** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9d6f0-153">On hello **SAP Business ByDesign Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="9d6f0-155">а.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-155">a.</span></span> <span data-ttu-id="9d6f0-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="9d6f0-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="9d6f0-157">b.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-157">b.</span></span> <span data-ttu-id="9d6f0-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="9d6f0-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d6f0-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-159">These values are not real.</span></span> <span data-ttu-id="9d6f0-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9d6f0-161">Обратитесь к [группа поддержки SAP Business ByDesign клиента](https://www.sap.com/products/cloud-analytics.support.html) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooget these values.</span></span>

4. <span data-ttu-id="9d6f0-162">На hello **атрибуты пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9d6f0-162">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Раздел атрибутов SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="9d6f0-164">а.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-164">a.</span></span> <span data-ttu-id="9d6f0-165">В **идентификатор пользователя** список, выберите hello **ExtractMailPrefix()** функции.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-165">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="9d6f0-166">b.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-166">b.</span></span> <span data-ttu-id="9d6f0-167">Из hello **Mail** список, атрибут пользователя выберите hello требуется toouse вашей реализации.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-167">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span> <span data-ttu-id="9d6f0-168">Например если требуется toouse hello EmployeeID как уникальный идентификатор пользователя и хранящимся в hello ExtensionAttribute2 значение атрибута hello, выберите user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-168">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>   

5. <span data-ttu-id="9d6f0-169">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="9d6f0-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9d6f0-171">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9d6f0-173">На hello **ByDesign конфигурации SAP Business** щелкните **Настройка SAP Business ByDesign** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-173">On hello **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9d6f0-174">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="9d6f0-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="9d6f0-176">tooget единого входа, настроенному для вашего приложения, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-176">tooget SSO configured for your application, perform hello following steps:</span></span>
   
    <span data-ttu-id="9d6f0-177">а.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-177">a.</span></span> <span data-ttu-id="9d6f0-178">Войдите на портал SAP Business ByDesign tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-178">Sign on tooyour SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="9d6f0-179">b.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-179">b.</span></span> <span data-ttu-id="9d6f0-180">Перейдите в слишком**приложения и общие задачи управления пользователя** и нажмите кнопку hello **поставщика удостоверений** вкладки.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-180">Navigate too**Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="9d6f0-181">c.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-181">c.</span></span> <span data-ttu-id="9d6f0-182">Нажмите кнопку **нового поставщика удостоверений** и выберите hello метаданных XML-файл, загруженный с портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-182">Click **New Identity Provider** and select hello metadata XML file that you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="9d6f0-183">Путем импорта метаданных hello, hello системы автоматически отправляет сертификат подписи требуется указать hello и сертификат шифрования.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-183">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="9d6f0-185">d.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-185">d.</span></span> <span data-ttu-id="9d6f0-186">tooinclude hello **URL-адрес службы утверждения потребителя** в запросе SAML hello, выберите **включает утверждение потребителя URL-адрес службы**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-186">tooinclude hello **Assertion Consumer Service URL** into hello SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="9d6f0-187">д.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-187">e.</span></span> <span data-ttu-id="9d6f0-188">Щелкните **Activate Single Sign-On**(Активировать единый вход).</span><span class="sxs-lookup"><span data-stu-id="9d6f0-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="9d6f0-189">Е.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-189">f.</span></span> <span data-ttu-id="9d6f0-190">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-190">Save your changes.</span></span>
   
    <span data-ttu-id="9d6f0-191">ж.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-191">g.</span></span> <span data-ttu-id="9d6f0-192">Нажмите кнопку hello **Мои системы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-192">Click hello **My System** tab.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="9d6f0-194">h.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-194">h.</span></span> <span data-ttu-id="9d6f0-195">Вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure hello его в hello **URL-адрес входа AD Azure** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-195">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal it into hello **Azure AD Sign On URL** textbox.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="9d6f0-197">i.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-197">i.</span></span> <span data-ttu-id="9d6f0-198">Указать ли hello сотрудника можно вручную выбрать между войти с помощью идентификатора пользователя и пароль или единого входа, выбрав **Выбор поставщика удостоверений вручную**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-198">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="9d6f0-199">j.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-199">j.</span></span> <span data-ttu-id="9d6f0-200">В hello **URL-адрес SSO** статьи, укажите hello URL-адрес, который должен использоваться системой toohello toologon сотрудника hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-200">In hello **SSO URL** section, specify hello URL that should be used by hello employee toologon toohello system.</span></span> 
    <span data-ttu-id="9d6f0-201">Hello URL-адрес отправки tooEmployee раскрывающемся списке можно выбрать hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="9d6f0-201">In hello URL Sent tooEmployee dropdown list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="9d6f0-202">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="9d6f0-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="9d6f0-203">Hello система отправляет только hello нормальная URL-адрес toohello сотрудника.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-203">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="9d6f0-204">Сотрудник Hello не может войти в систему с помощью единого входа и должны использовать пароль или сертификат вместо.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-204">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="9d6f0-205">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="9d6f0-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="9d6f0-206">Hello система отправляет только hello сотрудник toohello URL-адрес единого входа.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-206">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="9d6f0-207">Сотрудник Hello можно войти в систему с помощью единого входа.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-207">hello employee can log on using SSO.</span></span> <span data-ttu-id="9d6f0-208">Перенаправляет запрос проверки подлинности через hello поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-208">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="9d6f0-209">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="9d6f0-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="9d6f0-210">Если единый вход не активен, hello система отправляет hello нормальная URL-адрес toohello сотрудника.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-210">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="9d6f0-211">Если активен единого входа, hello система проверяет, содержит ли сотрудника hello пароль.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-211">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="9d6f0-212">Если пароль, URL-адрес единого входа и URL-адрес единого входа не отправляются toohello сотрудника.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-212">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="9d6f0-213">Тем не менее если сотрудник hello не имеет пароля, toohello сотрудника отправляется только hello URL-адрес единого входа.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-213">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="9d6f0-214">k.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-214">k.</span></span> <span data-ttu-id="9d6f0-215">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="9d6f0-216">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="9d6f0-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9d6f0-217">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9d6f0-218">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d6f0-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9d6f0-219">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d6f0-219">Create an Azure AD test user</span></span>

<span data-ttu-id="9d6f0-220">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="9d6f0-222">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9d6f0-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d6f0-223">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-223">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9d6f0-225">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-225">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9d6f0-227">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-227">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9d6f0-229">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9d6f0-229">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9d6f0-231">а.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-231">a.</span></span> <span data-ttu-id="9d6f0-232">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-232">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d6f0-233">b.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-233">b.</span></span> <span data-ttu-id="9d6f0-234">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-234">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="9d6f0-235">c.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-235">c.</span></span> <span data-ttu-id="9d6f0-236">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-236">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="9d6f0-237">d.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-237">d.</span></span> <span data-ttu-id="9d6f0-238">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="9d6f0-239">Создание тестового пользователя SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="9d6f0-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="9d6f0-240">В этом разделе мы создадим пользователя Britta Simon в приложении SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="9d6f0-241">Можно работать с [группа поддержки SAP Business ByDesign клиента](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello пользователей на платформе SAP Business ByDesign hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello users in hello SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="9d6f0-242">Убедитесь, что значение идентификатора имени должен совпадать с hello поле имени пользователя на платформе SAP Business ByDesign hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-242">Please make sure that NameID value should match with hello username field in hello SAP Business ByDesign platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9d6f0-243">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="9d6f0-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9d6f0-244">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSAP ByDesign бизнеса.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Business ByDesign.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="9d6f0-246">**tooassign tooSAP Britta Simon ByDesign бизнеса выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="9d6f0-246">**tooassign Britta Simon tooSAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d6f0-247">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9d6f0-249">В списке приложений hello выберите **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-249">In hello applications list, select **SAP Business ByDesign**.</span></span>

    ![ссылка SAP Business ByDesign Hello в списке приложений hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="9d6f0-251">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="9d6f0-253">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-253">Click **Add** button.</span></span> <span data-ttu-id="9d6f0-254">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="9d6f0-256">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9d6f0-257">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d6f0-258">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9d6f0-259">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9d6f0-259">Test single sign-on</span></span>

<span data-ttu-id="9d6f0-260">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9d6f0-261">Если щелкнуть плитку SAP Business ByDesign hello в hello панели доступа, следует получать приложения SAP Business ByDesign tooyour автоматически вошедшего.</span><span class="sxs-lookup"><span data-stu-id="9d6f0-261">When you click hello SAP Business ByDesign tile in hello Access Panel, you should get automatically signed-on tooyour SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d6f0-262">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9d6f0-262">Additional resources</span></span>

* [<span data-ttu-id="9d6f0-263">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d6f0-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d6f0-264">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d6f0-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

