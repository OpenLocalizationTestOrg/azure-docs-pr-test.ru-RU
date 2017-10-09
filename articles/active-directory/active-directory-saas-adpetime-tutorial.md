---
title: "Руководство по интеграции Azure Active Directory с ADP eTime | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ADP eTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="9a722-103">Учебник. Интеграция Azure Active Directory с ADP eTime</span><span class="sxs-lookup"><span data-stu-id="9a722-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="9a722-104">В этом учебнике вы узнаете, как eTime toointegrate ADP в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a722-104">In this tutorial, you learn how toointegrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a722-105">Интеграция с Azure AD ADP eTime предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9a722-105">Integrating ADP eTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9a722-106">Можно управлять в Azure AD, имеющего доступ tooADP eTime</span><span class="sxs-lookup"><span data-stu-id="9a722-106">You can control in Azure AD who has access tooADP eTime</span></span>
- <span data-ttu-id="9a722-107">Можно включить вашей пользователей tooautomatically get вошедшего tooADP eTime (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a722-107">You can enable your users tooautomatically get signed-on tooADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a722-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9a722-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9a722-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a722-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a722-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9a722-110">Prerequisites</span></span>

<span data-ttu-id="9a722-111">tooconfigure интеграция Azure AD с ADP eTime требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="9a722-111">tooconfigure Azure AD integration with ADP eTime, you need hello following items:</span></span>

- <span data-ttu-id="9a722-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9a722-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a722-113">подписка ADP eTime с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9a722-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a722-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9a722-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a722-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="9a722-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a722-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="9a722-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a722-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a722-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a722-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9a722-118">Scenario description</span></span>
<span data-ttu-id="9a722-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9a722-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a722-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="9a722-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a722-121">Добавление ADP eTime из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9a722-121">Adding ADP eTime from hello gallery</span></span>
2. <span data-ttu-id="9a722-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a722-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-hello-gallery"></a><span data-ttu-id="9a722-123">Добавление ADP eTime из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9a722-123">Adding ADP eTime from hello gallery</span></span>
<span data-ttu-id="9a722-124">tooconfigure hello интеграции ADP eTime в Azure AD, вы должны eTime ADP tooadd из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9a722-124">tooconfigure hello integration of ADP eTime into Azure AD, you need tooadd ADP eTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9a722-125">**eTime tooadd ADP из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9a722-125">**tooadd ADP eTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a722-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9a722-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9a722-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="9a722-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9a722-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9a722-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9a722-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9a722-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9a722-133">Введите в поле поиска hello **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="9a722-133">In hello search box, type **ADP eTime**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="9a722-135">В панели результатов hello выберите **ADP eTime**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9a722-135">In hello results panel, select **ADP eTime**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9a722-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a722-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9a722-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение ADP eTime с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a722-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9a722-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ADP eTime является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a722-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP eTime is tooa user in Azure AD.</span></span> <span data-ttu-id="9a722-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в ADP eTime должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="9a722-140">In other words, a link relationship between an Azure AD user and hello related user in ADP eTime needs toobe established.</span></span>

<span data-ttu-id="9a722-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="9a722-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP eTime.</span></span>

<span data-ttu-id="9a722-142">tooconfigure и теста Azure AD единого входа с ADP eTime, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9a722-142">tooconfigure and test Azure AD single sign-on with ADP eTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9a722-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="9a722-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9a722-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="9a722-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a722-145">**[Создание тестового пользователя, прошедшего ADP eTime](#creating-an-adp-etime-test-user)**  -toohave аналог Саймон Britta в eTime ADP, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="9a722-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - toohave a counterpart of Britta Simon in ADP eTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a722-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="9a722-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a722-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9a722-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9a722-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a722-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9a722-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="9a722-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="9a722-150">**tooconfigure Azure AD единого входа с ADP eTime выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9a722-150">**tooconfigure Azure AD single sign-on with ADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a722-151">В hello в hello портала Azure **ADP eTime** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9a722-151">In hello Azure portal, on hello **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9a722-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="9a722-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="9a722-155">На hello **eTime ADP доменов и URL-адреса** выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="9a722-155">On hello **ADP eTime Domain and URLs** section, perform hello following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="9a722-157">а.</span><span class="sxs-lookup"><span data-stu-id="9a722-157">a.</span></span> <span data-ttu-id="9a722-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="9a722-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="9a722-159">b.</span><span class="sxs-lookup"><span data-stu-id="9a722-159">b.</span></span> <span data-ttu-id="9a722-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="9a722-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="9a722-161">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="9a722-161">These values are not hello real.</span></span> <span data-ttu-id="9a722-162">Обновите эти значения с hello фактический URL-адрес ответа и идентификатора.</span><span class="sxs-lookup"><span data-stu-id="9a722-162">Update these values with hello actual Reply URL and Identifier.</span></span> <span data-ttu-id="9a722-163">Обратитесь к [группа поддержки ADP eTime](https://www.adp.com/contact-us/overview.aspx) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="9a722-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooget these values.</span></span>

4. <span data-ttu-id="9a722-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9a722-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="9a722-166">Hello ADP eTime приложения ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="9a722-166">hello ADP eTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="9a722-167">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="9a722-167">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="9a722-168">Hello имя утверждения всегда будет **«PersonImmutableID»** и из которых сопоставленной tooExtensionAttribute2, который содержит значение hello hello EmployeeID hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="9a722-168">hello claim name will always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2 which contains hello EmployeeID of hello user.</span></span> 

    <span data-ttu-id="9a722-169">Здесь hello сопоставление пользователей из Azure AD tooADP eTime будет выполняться на hello EmployeeID, но вы можете сопоставить этот tooa свое значение также параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="9a722-169">Here hello user mapping from Azure AD tooADP eTime will be done on hello EmployeeID but you can map this tooa different value also based on your application settings.</span></span> <span data-ttu-id="9a722-170">Так что произведите рабочих с [группа поддержки ADP eTime](https://www.adp.com/contact-us/overview.aspx) первый toouse hello правильный идентификатор пользователя и сопоставить это значение с hello **«PersonImmutableID»** утверждения.</span><span class="sxs-lookup"><span data-stu-id="9a722-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="9a722-172">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9a722-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="9a722-173">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="9a722-173">Attribute Name</span></span> | <span data-ttu-id="9a722-174">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="9a722-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="9a722-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="9a722-175">PersonImmutableID</span></span> | <span data-ttu-id="9a722-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="9a722-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="9a722-177">а.</span><span class="sxs-lookup"><span data-stu-id="9a722-177">a.</span></span> <span data-ttu-id="9a722-178">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9a722-178">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9a722-181">b.</span><span class="sxs-lookup"><span data-stu-id="9a722-181">b.</span></span> <span data-ttu-id="9a722-182">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="9a722-182">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="9a722-183">c.</span><span class="sxs-lookup"><span data-stu-id="9a722-183">c.</span></span> <span data-ttu-id="9a722-184">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="9a722-184">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="9a722-185">d.</span><span class="sxs-lookup"><span data-stu-id="9a722-185">d.</span></span> <span data-ttu-id="9a722-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9a722-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a722-187">Перед настройкой hello утверждения SAML, необходимо toocontact вашей [группа поддержки ADP eTime](https://www.adp.com/contact-us/overview.aspx) и запросить значение hello hello уникальный идентификатор атрибута для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="9a722-187">Before you can configure hello SAML assertion, you need toocontact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="9a722-188">Необходимо, чтобы это значение tooconfigure hello пользовательского утверждения для приложения.</span><span class="sxs-lookup"><span data-stu-id="9a722-188">You need this value tooconfigure hello custom claim for your application.</span></span> 

7. <span data-ttu-id="9a722-189">На hello **eTime ADP конфигурации** щелкните **eTime Настройка ADP** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="9a722-189">On hello **ADP eTime Configuration** section, click **Configure ADP eTime** tooopen **Configure sign-on** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="9a722-191">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9a722-191">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="9a722-193">tooconfigure единого входа на **ADP eTime** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группа поддержки ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="9a722-193">tooconfigure single sign-on on **ADP eTime** side, you need toosend hello downloaded **Metadata XML** too[ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="9a722-194">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="9a722-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9a722-195">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="9a722-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9a722-196">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a722-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9a722-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a722-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="9a722-198">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9a722-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9a722-200">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9a722-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a722-201">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9a722-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a722-203">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="9a722-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a722-205">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="9a722-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a722-207">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9a722-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a722-209">а.</span><span class="sxs-lookup"><span data-stu-id="9a722-209">a.</span></span> <span data-ttu-id="9a722-210">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a722-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a722-211">b.</span><span class="sxs-lookup"><span data-stu-id="9a722-211">b.</span></span> <span data-ttu-id="9a722-212">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9a722-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a722-213">c.</span><span class="sxs-lookup"><span data-stu-id="9a722-213">c.</span></span> <span data-ttu-id="9a722-214">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="9a722-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9a722-215">d.</span><span class="sxs-lookup"><span data-stu-id="9a722-215">d.</span></span> <span data-ttu-id="9a722-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9a722-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="9a722-217">Создание тестового пользователя ADP eTime</span><span class="sxs-lookup"><span data-stu-id="9a722-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="9a722-218">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="9a722-218">hello objective of this section is toocreate a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="9a722-219">Работать с [группа поддержки ADP eTime](https://www.adp.com/contact-us/overview.aspx) tooadd hello пользователей в учетной записи eTime hello ADP.</span><span class="sxs-lookup"><span data-stu-id="9a722-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP eTime account.</span></span> 
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9a722-220">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="9a722-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9a722-221">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooADP eTime.</span><span class="sxs-lookup"><span data-stu-id="9a722-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP eTime.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9a722-223">**tooassign eTime tooADP Britta Simon, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="9a722-223">**tooassign Britta Simon tooADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a722-224">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9a722-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9a722-226">В списке приложений hello выберите **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="9a722-226">In hello applications list, select **ADP eTime**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="9a722-228">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="9a722-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9a722-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9a722-230">Click **Add** button.</span></span> <span data-ttu-id="9a722-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9a722-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9a722-233">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="9a722-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9a722-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9a722-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a722-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9a722-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9a722-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9a722-236">Testing single sign-on</span></span>

<span data-ttu-id="9a722-237">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="9a722-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9a722-238">При нажатии кнопки hello ADP eTime плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour ADP eTime приложения.</span><span class="sxs-lookup"><span data-stu-id="9a722-238">When you click hello ADP eTime tile in hello Access Panel, you should get automatically signed-on tooyour ADP eTime application.</span></span>
<span data-ttu-id="9a722-239">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9a722-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9a722-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9a722-240">Additional resources</span></span>

* [<span data-ttu-id="9a722-241">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a722-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a722-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a722-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

