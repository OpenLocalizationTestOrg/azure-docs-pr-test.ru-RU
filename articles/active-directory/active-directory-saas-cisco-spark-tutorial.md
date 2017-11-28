---
title: "Учебник. Интеграция Azure Active Directory с Cisco Spark | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Cisco Spark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="7d2ef-103">Учебник. Интеграция Azure Active Directory с Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="7d2ef-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="7d2ef-104">В этом учебнике вы узнаете, как toointegrate Cisco усилить с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7d2ef-104">In this tutorial, you learn how toointegrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d2ef-105">Интеграция Cisco Spark в Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7d2ef-105">Integrating Cisco Spark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7d2ef-106">Можно управлять в Azure AD, имеющего доступ tooCisco Spark</span><span class="sxs-lookup"><span data-stu-id="7d2ef-106">You can control in Azure AD who has access tooCisco Spark</span></span>
- <span data-ttu-id="7d2ef-107">Можно включить на пользователей tooautomatically get вошедшего tooCisco Spark (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d2ef-107">You can enable your users tooautomatically get signed-on tooCisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d2ef-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7d2ef-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7d2ef-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7d2ef-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d2ef-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7d2ef-110">Prerequisites</span></span>

<span data-ttu-id="7d2ef-111">tooconfigure интеграция Azure AD с Cisco Spark требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7d2ef-111">tooconfigure Azure AD integration with Cisco Spark, you need hello following items:</span></span>

- <span data-ttu-id="7d2ef-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7d2ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d2ef-113">подписка Cisco Spark с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d2ef-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d2ef-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7d2ef-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d2ef-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7d2ef-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d2ef-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d2ef-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7d2ef-118">Scenario description</span></span>
<span data-ttu-id="7d2ef-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d2ef-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7d2ef-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d2ef-121">Добавление Cisco Spark из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7d2ef-121">Adding Cisco Spark from hello gallery</span></span>
2. <span data-ttu-id="7d2ef-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d2ef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-hello-gallery"></a><span data-ttu-id="7d2ef-123">Добавление Cisco Spark из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7d2ef-123">Adding Cisco Spark from hello gallery</span></span>
<span data-ttu-id="7d2ef-124">tooconfigure hello интеграции Cisco Spark в Azure AD, вы должны tooadd Cisco Spark из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-124">tooconfigure hello integration of Cisco Spark into Azure AD, you need tooadd Cisco Spark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7d2ef-125">**tooadd Spark Cisco из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7d2ef-125">**tooadd Cisco Spark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d2ef-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7d2ef-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7d2ef-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7d2ef-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7d2ef-133">Введите в поле поиска hello **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-133">In hello search box, type **Cisco Spark**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="7d2ef-135">В панели результатов hello выберите **Cisco Spark**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-135">In hello results panel, select **Cisco Spark**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7d2ef-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d2ef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7d2ef-138">В этом разделе описана настройка и проверка единого входа Azure AD в Cisco Spark с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7d2ef-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Cisco Spark является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cisco Spark is tooa user in Azure AD.</span></span> <span data-ttu-id="7d2ef-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Cisco Spark должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-140">In other words, a link relationship between an Azure AD user and hello related user in Cisco Spark needs toobe established.</span></span>

<span data-ttu-id="7d2ef-141">В Cisco Spark, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-141">In Cisco Spark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7d2ef-142">tooconfigure и теста Azure AD единого входа с Cisco Spark, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7d2ef-142">tooconfigure and test Azure AD single sign-on with Cisco Spark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7d2ef-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7d2ef-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d2ef-145">**[Создание тестового пользователя Cisco Spark](#creating-a-cisco-spark-test-user)**  -toohave аналог Саймон Britta в Spark Cisco, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - toohave a counterpart of Britta Simon in Cisco Spark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7d2ef-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d2ef-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7d2ef-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d2ef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7d2ef-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="7d2ef-150">**tooconfigure Azure AD единого входа с Cisco Spark, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7d2ef-150">**tooconfigure Azure AD single sign-on with Cisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d2ef-151">В hello в hello портала Azure **Cisco Spark** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-151">In hello Azure portal, on hello **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7d2ef-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="7d2ef-155">На hello **URL-адреса и домена Spark Cisco** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7d2ef-155">On hello **Cisco Spark Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="7d2ef-157">а.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-157">a.</span></span> <span data-ttu-id="7d2ef-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="7d2ef-158">In hello **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="7d2ef-159">b.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-159">b.</span></span> <span data-ttu-id="7d2ef-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="7d2ef-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7d2ef-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-161">This value is not real.</span></span> <span data-ttu-id="7d2ef-162">Измените значение этого параметра hello фактический идентификатор.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="7d2ef-163">Обратитесь к [группа поддержки клиента Cisco Spark](https://support.ciscospark.com/) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) tooget this value.</span></span> 
 
4. <span data-ttu-id="7d2ef-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="7d2ef-166">Cisco Spark приложение ожидает, что определенные атрибуты утверждения SAML toocontain hello.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-166">Cisco Spark application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="7d2ef-167">Настройте следующие атрибуты для данного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="7d2ef-168">Вы можете управлять hello значения этих атрибутов из hello **атрибуты пользователя** раздел на странице интеграции приложений.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-168">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="7d2ef-169">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-169">hello following screenshot shows an example for this.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="7d2ef-171">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7d2ef-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="7d2ef-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="7d2ef-172">Attribute Name</span></span>  | <span data-ttu-id="7d2ef-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="7d2ef-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="7d2ef-174">uid</span><span class="sxs-lookup"><span data-stu-id="7d2ef-174">uid</span></span>    | <span data-ttu-id="7d2ef-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="7d2ef-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="7d2ef-176">а.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-176">a.</span></span> <span data-ttu-id="7d2ef-177">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="7d2ef-180">b.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-180">b.</span></span> <span data-ttu-id="7d2ef-181">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7d2ef-182">c.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-182">c.</span></span> <span data-ttu-id="7d2ef-183">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7d2ef-184">d.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-184">d.</span></span> <span data-ttu-id="7d2ef-185">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-185">Click **Ok**.</span></span>

7. <span data-ttu-id="7d2ef-186">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7d2ef-186">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7d2ef-188">Войдите в слишком[управления совместной работы облачной Cisco](https://admin.ciscospark.com/) с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-188">Sign in too[Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="7d2ef-189">Выберите **параметры** и на странице приветствия **проверки подлинности** щелкните **изменить**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-189">Select **Settings** and under hello **Authentication** section, click **Modify**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="7d2ef-191">Выберите **Integrate a 3rd-party identity provider. (Дополнительно)**  и последовательно выберите toohello следующий экран.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go toohello next screen.</span></span>

11. <span data-ttu-id="7d2ef-192">На hello **импортировать метаданные поставщика удостоверений** страница, либо перетащите файл метаданных hello Azure AD на странице приветствия или использовать браузер параметр hello файл toolocate и отправить файл метаданных hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-192">On hello **Import Idp Metadata** page, either drag and drop hello Azure AD metadata file onto hello page or use hello file browser option toolocate and upload hello Azure AD metadata file.</span></span> <span data-ttu-id="7d2ef-193">Затем выберите **Require certificate signed by a certificate authority in Metadata (more secure)** (Требовать наличия в метаданных сертификата, подписанного центром сертификации) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="7d2ef-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="7d2ef-195">Выберите **Test SSO Connection** (Проверить подключение для единого входа) и, когда откроется новая вкладка браузера, пройдите аутентификацию Azure AD, выполнив вход.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="7d2ef-196">Вернуть toohello **управления совместной работы облачной Cisco** вкладка «браузер». При успешном выполнении теста hello выберите **это проверка выполнена успешно. Enable Single Sign-On option** (Этот тест прошел успешно. Включить единый вход) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="7d2ef-196">Return toohello **Cisco Cloud Collaboration Management** browser tab. If hello test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="7d2ef-197">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="7d2ef-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7d2ef-198">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7d2ef-199">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7d2ef-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7d2ef-200">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d2ef-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="7d2ef-201">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7d2ef-203">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7d2ef-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d2ef-204">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7d2ef-206">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7d2ef-208">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="7d2ef-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d2ef-210">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7d2ef-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7d2ef-212">а.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-212">a.</span></span> <span data-ttu-id="7d2ef-213">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d2ef-214">b.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-214">b.</span></span> <span data-ttu-id="7d2ef-215">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7d2ef-216">c.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-216">c.</span></span> <span data-ttu-id="7d2ef-217">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7d2ef-218">d.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-218">d.</span></span> <span data-ttu-id="7d2ef-219">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-219">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="7d2ef-220">Создание тестового пользователя Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="7d2ef-220">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="7d2ef-221">В этом разделе описано, как создать пользователя Britta Simon в Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-221">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="7d2ef-222">В этом разделе описано, как создать пользователя Britta Simon в Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="7d2ef-223">Go toohello [управления совместной работы облачной Cisco](https://admin.ciscospark.com/) с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-223">Go toohello [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="7d2ef-224">Щелкните **Пользователи** и **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-224">Click **Users** and then **Manage Users**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="7d2ef-226">В hello **управление пользовательскими** выберите **вручную добавить или изменить пользователей** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-226">In hello **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="7d2ef-227">Выберите **Names and Email address** (Имя, фамилия и электронный адрес).</span><span class="sxs-lookup"><span data-stu-id="7d2ef-227">Select **Names and Email address**.</span></span> <span data-ttu-id="7d2ef-228">Затем заполните hello текстовом поле следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7d2ef-228">Then, fill out hello textbox as follows:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="7d2ef-230">а.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-230">a.</span></span> <span data-ttu-id="7d2ef-231">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-231">In hello **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="7d2ef-232">b.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-232">b.</span></span> <span data-ttu-id="7d2ef-233">В hello **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-233">In hello **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="7d2ef-234">c.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-234">c.</span></span> <span data-ttu-id="7d2ef-235">В hello **адрес электронной почты** введите  **britta.simon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="7d2ef-235">In hello **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="7d2ef-236">Нажмите кнопку hello, а также tooadd Britta Simon входа.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-236">Click hello plus sign tooadd Britta Simon.</span></span> <span data-ttu-id="7d2ef-237">Затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-237">Then, click **Next**.</span></span>

6. <span data-ttu-id="7d2ef-238">В hello **Добавление служб для пользователей** окно, нажмите кнопку **Сохранить** и затем **Готово**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-238">In hello **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7d2ef-239">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7d2ef-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7d2ef-240">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCisco Spark.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCisco Spark.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7d2ef-242">**tooassign tooCisco Britta Simon Spark, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="7d2ef-242">**tooassign Britta Simon tooCisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d2ef-243">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7d2ef-245">В списке приложений hello выберите **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-245">In hello applications list, select **Cisco Spark**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="7d2ef-247">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7d2ef-249">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-249">Click **Add** button.</span></span> <span data-ttu-id="7d2ef-250">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7d2ef-252">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7d2ef-253">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d2ef-254">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7d2ef-255">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7d2ef-255">Testing single sign-on</span></span>

<span data-ttu-id="7d2ef-256">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="7d2ef-256">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="7d2ef-257">Если щелкнуть плитку Cisco Spark hello в hello панели доступа, вы должны получить tooyour автоматически вошедшего Cisco Spark приложения.</span><span class="sxs-lookup"><span data-stu-id="7d2ef-257">When you click hello Cisco Spark tile in hello Access Panel, you should get automatically signed-on tooyour Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d2ef-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7d2ef-258">Additional resources</span></span>

* [<span data-ttu-id="7d2ef-259">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7d2ef-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d2ef-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7d2ef-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

