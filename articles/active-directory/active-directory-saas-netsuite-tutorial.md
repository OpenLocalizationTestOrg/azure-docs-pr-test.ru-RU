---
title: "Руководство по интеграции Azure Active Directory с NetSuite | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="bf826-103">Руководство по интеграции Azure Active Directory с NetSuite</span><span class="sxs-lookup"><span data-stu-id="bf826-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="bf826-104">В этом учебнике вы узнаете, как toointegrate Netsuite с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf826-104">In this tutorial, you learn how toointegrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf826-105">Интеграция Netsuite с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="bf826-105">Integrating Netsuite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bf826-106">Можно управлять в Azure AD, имеющего доступ tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="bf826-106">You can control in Azure AD who has access tooNetsuite</span></span>
- <span data-ttu-id="bf826-107">Можно включить на пользователей tooautomatically get вошедшего tooNetsuite (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf826-107">You can enable your users tooautomatically get signed-on tooNetsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf826-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="bf826-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bf826-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bf826-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf826-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bf826-110">Prerequisites</span></span>

<span data-ttu-id="bf826-111">tooconfigure интеграция Azure AD с Netsuite требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="bf826-111">tooconfigure Azure AD integration with Netsuite, you need hello following items:</span></span>

- <span data-ttu-id="bf826-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bf826-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf826-113">подписка Netsuite с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="bf826-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf826-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="bf826-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf826-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="bf826-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf826-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bf826-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf826-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf826-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf826-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bf826-118">Scenario description</span></span>
<span data-ttu-id="bf826-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bf826-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf826-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="bf826-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf826-121">Добавление Netsuite из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bf826-121">Adding Netsuite from hello gallery</span></span>
2. <span data-ttu-id="bf826-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf826-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-hello-gallery"></a><span data-ttu-id="bf826-123">Добавление Netsuite из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bf826-123">Adding Netsuite from hello gallery</span></span>
<span data-ttu-id="bf826-124">tooconfigure hello интеграции Netsuite в Azure AD, вы должны tooadd Netsuite из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bf826-124">tooconfigure hello integration of Netsuite into Azure AD, you need tooadd Netsuite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bf826-125">**tooadd Netsuite из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bf826-125">**tooadd Netsuite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf826-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bf826-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bf826-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="bf826-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bf826-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bf826-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="bf826-131">Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="bf826-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="bf826-133">Введите в поле поиска hello **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="bf826-133">In hello search box, type **Netsuite**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="bf826-135">В панели результатов hello выберите **Netsuite**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bf826-135">In hello results panel, select **Netsuite**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf826-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf826-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf826-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Netsuite с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf826-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bf826-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Netsuite является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf826-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Netsuite is tooa user in Azure AD.</span></span> <span data-ttu-id="bf826-140">Иными словами связи между пользователя Azure AD и hello связанных пользователей в Netsuite требуется установить toobe.</span><span class="sxs-lookup"><span data-stu-id="bf826-140">In other words, a link relationship between an Azure AD user and hello related user in Netsuite needs toobe established.</span></span>

<span data-ttu-id="bf826-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Netsuite.</span><span class="sxs-lookup"><span data-stu-id="bf826-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Netsuite.</span></span>

<span data-ttu-id="bf826-142">tooconfigure и теста Azure AD единого входа с Netsuite, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bf826-142">tooconfigure and test Azure AD single sign-on with Netsuite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bf826-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="bf826-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bf826-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="bf826-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf826-145">**[Создание тестового пользователя Netsuite](#creating-a-netsuite-test-user)**  -toohave аналог Саймон Britta в Netsuite, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="bf826-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - toohave a counterpart of Britta Simon in Netsuite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf826-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="bf826-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf826-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bf826-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf826-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf826-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf826-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в свое приложение Netsuite.</span><span class="sxs-lookup"><span data-stu-id="bf826-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="bf826-150">**Azure AD tooconfigure единого входа с Netsuite, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bf826-150">**tooconfigure Azure AD single sign-on with Netsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf826-151">В hello в hello портала Azure **Netsuite** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="bf826-151">In hello Azure portal, on hello **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="bf826-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="bf826-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="bf826-155">На hello **URL-адреса и домена Netsuite** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bf826-155">On hello **Netsuite Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="bf826-157">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="bf826-157">In hello **Reply URL** textbox, type a URL using hello following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bf826-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="bf826-158">This value is not real value.</span></span> <span data-ttu-id="bf826-159">Значение hello обновления с hello фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="bf826-159">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="bf826-160">Обратитесь к [Netsuite поддержки](http://www.netsuite.com/portal/services/support.shtml) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="bf826-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) tooget this value.</span></span>
 
4. <span data-ttu-id="bf826-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="bf826-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="bf826-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="bf826-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bf826-165">На hello **конфигурации Netsuite** щелкните **Настройка Netsuite** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="bf826-165">On hello **Netsuite Configuration** section, click **Configure Netsuite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bf826-166">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="bf826-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="bf826-168">Откройте новую вкладку в браузере и войдите как администратор корпоративного сайта NetSuite.</span><span class="sxs-lookup"><span data-stu-id="bf826-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="bf826-169">Щелкните hello панели инструментов вверху hello страницы приветствия **установки**, нажмите кнопку **диспетчер установки**.</span><span class="sxs-lookup"><span data-stu-id="bf826-169">In hello toolbar at hello top of hello page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="bf826-171">Из hello **задачи настройки** выберите **интеграции**.</span><span class="sxs-lookup"><span data-stu-id="bf826-171">From hello **Setup Tasks** list, select **Integration**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="bf826-173">В hello **управление проверкой подлинности** щелкните **SAML Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bf826-173">In hello **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="bf826-175">На hello **Настройка SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bf826-175">On hello **SAML Setup** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="bf826-176">а.</span><span class="sxs-lookup"><span data-stu-id="bf826-176">a.</span></span> <span data-ttu-id="bf826-177">Копировать hello **SAML единого входа URL-адрес службы** значение из **краткий справочник** раздел **Настройка входа** и вставьте его в hello **поставщика удостоверений Страница входа** в Netsuite.</span><span class="sxs-lookup"><span data-stu-id="bf826-177">Copy hello **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into hello **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="bf826-179">b.</span><span class="sxs-lookup"><span data-stu-id="bf826-179">b.</span></span> <span data-ttu-id="bf826-180">В NetSuite выберите раздел **Primary Authentication Method** (Основной метод проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="bf826-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="bf826-181">c.</span><span class="sxs-lookup"><span data-stu-id="bf826-181">c.</span></span> <span data-ttu-id="bf826-182">Для hello поля с меткой **метаданные поставщика удостоверений SAMLV2**выберите **отправьте файл метаданных поставщика Удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="bf826-182">For hello field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="bf826-183">Нажмите кнопку **Обзор** tooupload hello метаданные файла, загруженного с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="bf826-183">Then click **Browse** tooupload hello metadata file that you downloaded from Azure portal.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="bf826-185">г)</span><span class="sxs-lookup"><span data-stu-id="bf826-185">d.</span></span> <span data-ttu-id="bf826-186">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="bf826-186">Click **Submit**.</span></span>

12. <span data-ttu-id="bf826-187">В Azure AD установите флажок **Просмотреть и изменить все другие атрибуты пользователей** и добавьте атрибут.</span><span class="sxs-lookup"><span data-stu-id="bf826-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="bf826-189">Для hello **имя атрибута** введите в `account`.</span><span class="sxs-lookup"><span data-stu-id="bf826-189">For hello **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="bf826-190">Для hello **значение атрибута** введите идентификатора учетной записи в Netsuite. Это значение является константой, а изменение с записью.</span><span class="sxs-lookup"><span data-stu-id="bf826-190">For hello **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="bf826-191">Инструкции о том, как toofind свой идентификатор учетной записи приведены ниже:</span><span class="sxs-lookup"><span data-stu-id="bf826-191">Instructions on how toofind your account ID are included below:</span></span>

      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="bf826-193">а.</span><span class="sxs-lookup"><span data-stu-id="bf826-193">a.</span></span> <span data-ttu-id="bf826-194">В Netsuite, щелкните **установки** меню hello верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="bf826-194">In Netsuite, click **Setup** from hello top navigation menu.</span></span>

    <span data-ttu-id="bf826-195">b.</span><span class="sxs-lookup"><span data-stu-id="bf826-195">b.</span></span> <span data-ttu-id="bf826-196">Выберите в списке hello **задачи настройки** раздел hello левом меню навигации, выберите hello **интеграции** и нажмите кнопку **предпочтений относительно служб Web**.</span><span class="sxs-lookup"><span data-stu-id="bf826-196">Then click under hello **Setup Tasks** section of hello left navigation menu, select hello **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="bf826-197">c.</span><span class="sxs-lookup"><span data-stu-id="bf826-197">c.</span></span> <span data-ttu-id="bf826-198">Ваш ИД учетной записи Netsuite скопируйте и вставьте его в hello **значение атрибута** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf826-198">Copy your Netsuite Account ID and paste it into hello **Attribute Value** field in Azure AD.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="bf826-200">Прежде чем пользователи могут выполнять единый вход в Netsuite, их необходимо сначала назначить hello соответствующие разрешения в Netsuite.</span><span class="sxs-lookup"><span data-stu-id="bf826-200">Before users can perform single sign-on into Netsuite, they must first be assigned hello appropriate permissions in Netsuite.</span></span> <span data-ttu-id="bf826-201">Следуйте инструкциям hello ниже tooassign эти разрешения.</span><span class="sxs-lookup"><span data-stu-id="bf826-201">Follow hello instructions below tooassign these permissions.</span></span>

    <span data-ttu-id="bf826-202">а.</span><span class="sxs-lookup"><span data-stu-id="bf826-202">a.</span></span> <span data-ttu-id="bf826-203">Hello верхней панели навигации выберите команду меню **установки**, нажмите кнопку **диспетчер установки**.</span><span class="sxs-lookup"><span data-stu-id="bf826-203">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="bf826-205">b.</span><span class="sxs-lookup"><span data-stu-id="bf826-205">b.</span></span> <span data-ttu-id="bf826-206">Выберите меню навигации слева hello **пользователи и роли**, нажмите кнопку **управление ролями**.</span><span class="sxs-lookup"><span data-stu-id="bf826-206">On hello left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="bf826-208">c.</span><span class="sxs-lookup"><span data-stu-id="bf826-208">c.</span></span> <span data-ttu-id="bf826-209">Нажмите кнопку **Создать роль**.</span><span class="sxs-lookup"><span data-stu-id="bf826-209">Click **New Role**.</span></span>

    <span data-ttu-id="bf826-210">d.</span><span class="sxs-lookup"><span data-stu-id="bf826-210">d.</span></span> <span data-ttu-id="bf826-211">Введите в **имя** для новой роли и выберите hello **единого входа только** флажок.</span><span class="sxs-lookup"><span data-stu-id="bf826-211">Type in a **Name** for your new role, and select hello **Single Sign-On Only** checkbox.</span></span>
      
      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="bf826-213">д.</span><span class="sxs-lookup"><span data-stu-id="bf826-213">e.</span></span> <span data-ttu-id="bf826-214">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bf826-214">Click **Save**.</span></span>

    <span data-ttu-id="bf826-215">f.</span><span class="sxs-lookup"><span data-stu-id="bf826-215">f.</span></span> <span data-ttu-id="bf826-216">В меню в верхней части hello hello выберите **разрешений**.</span><span class="sxs-lookup"><span data-stu-id="bf826-216">In hello menu on hello top, click **Permissions**.</span></span> <span data-ttu-id="bf826-217">Затем щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="bf826-217">Then click **Setup**.</span></span>
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="bf826-219">g.</span><span class="sxs-lookup"><span data-stu-id="bf826-219">g.</span></span> <span data-ttu-id="bf826-220">Выберите **Set Up SAM Single Sign-on** (Настройка единого входа управления лицензиями) и нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="bf826-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="bf826-221">h.</span><span class="sxs-lookup"><span data-stu-id="bf826-221">h.</span></span> <span data-ttu-id="bf826-222">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bf826-222">Click **Save**.</span></span>

    <span data-ttu-id="bf826-223">i.</span><span class="sxs-lookup"><span data-stu-id="bf826-223">i.</span></span> <span data-ttu-id="bf826-224">Hello верхней панели навигации выберите команду меню **установки**, нажмите кнопку **диспетчер установки**.</span><span class="sxs-lookup"><span data-stu-id="bf826-224">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="bf826-226">j.</span><span class="sxs-lookup"><span data-stu-id="bf826-226">j.</span></span> <span data-ttu-id="bf826-227">Выберите меню навигации слева hello **пользователи и роли**, нажмите кнопку **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="bf826-227">On hello left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="bf826-229">k.</span><span class="sxs-lookup"><span data-stu-id="bf826-229">k.</span></span> <span data-ttu-id="bf826-230">Выберите тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="bf826-230">Select a test user.</span></span> <span data-ttu-id="bf826-231">Нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="bf826-231">Then click **Edit**.</span></span>
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="bf826-233">l.</span><span class="sxs-lookup"><span data-stu-id="bf826-233">l.</span></span> <span data-ttu-id="bf826-234">В диалоговом окне приветствия ролей, выберите роль hello, вы создали и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="bf826-234">On hello Roles dialog, select hello role that you have created and click **Add**.</span></span>
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="bf826-236">m.</span><span class="sxs-lookup"><span data-stu-id="bf826-236">m.</span></span> <span data-ttu-id="bf826-237">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bf826-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="bf826-238">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="bf826-238">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bf826-239">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="bf826-239">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bf826-240">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf826-240">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf826-241">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf826-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf826-242">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bf826-242">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="bf826-244">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bf826-244">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf826-245">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bf826-245">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="bf826-247">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="bf826-247">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf826-249">Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="bf826-249">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf826-251">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bf826-251">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf826-253">а.</span><span class="sxs-lookup"><span data-stu-id="bf826-253">a.</span></span> <span data-ttu-id="bf826-254">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf826-254">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf826-255">b.</span><span class="sxs-lookup"><span data-stu-id="bf826-255">b.</span></span> <span data-ttu-id="bf826-256">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf826-256">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf826-257">c.</span><span class="sxs-lookup"><span data-stu-id="bf826-257">c.</span></span> <span data-ttu-id="bf826-258">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="bf826-258">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bf826-259">d.</span><span class="sxs-lookup"><span data-stu-id="bf826-259">d.</span></span> <span data-ttu-id="bf826-260">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bf826-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="bf826-261">Создание тестового пользователя Netsuite</span><span class="sxs-lookup"><span data-stu-id="bf826-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="bf826-262">В этом разделе вы создадите в Netsuite пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf826-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="bf826-263">Netsuite поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bf826-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="bf826-264">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="bf826-264">There is no action item for you in this section.</span></span> <span data-ttu-id="bf826-265">Если пользователь еще не существует в Netsuite, создается новый, при попытке tooaccess Netsuite.</span><span class="sxs-lookup"><span data-stu-id="bf826-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt tooaccess Netsuite.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bf826-266">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="bf826-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bf826-267">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooNetsuite доступа.</span><span class="sxs-lookup"><span data-stu-id="bf826-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetsuite.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="bf826-269">**tooassign tooNetsuite Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bf826-269">**tooassign Britta Simon tooNetsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf826-270">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bf826-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bf826-272">В списке приложений hello выберите **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="bf826-272">In hello applications list, select **Netsuite**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="bf826-274">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="bf826-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="bf826-276">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bf826-276">Click **Add** button.</span></span> <span data-ttu-id="bf826-277">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bf826-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="bf826-279">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="bf826-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bf826-280">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bf826-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf826-281">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bf826-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf826-282">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bf826-282">Testing single sign-on</span></span>

<span data-ttu-id="bf826-283">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="bf826-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bf826-284">tootest входа параметры единого, откройте hello панель доступа по адресу [https://myapps.microsoft.com](https://myapps.microsoft.com/)входа в hello тестовую учетную запись и нажмите кнопку **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="bf826-284">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into hello test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf826-285">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bf826-285">Additional resources</span></span>

* [<span data-ttu-id="bf826-286">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf826-286">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf826-287">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bf826-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="bf826-288">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="bf826-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

