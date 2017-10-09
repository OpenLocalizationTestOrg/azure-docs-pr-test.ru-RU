---
title: "Руководство. Интеграция Azure Active Directory с Work.com | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="a653f-103">Руководство. Интеграция Azure Active Directory с Work.com</span><span class="sxs-lookup"><span data-stu-id="a653f-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="a653f-104">В этом учебнике вы узнаете, как toointegrate Work.com с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a653f-104">In this tutorial, you learn how toointegrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a653f-105">Интеграция Work.com с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a653f-105">Integrating Work.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a653f-106">Можно управлять в Azure AD, имеющего доступ tooWork.com</span><span class="sxs-lookup"><span data-stu-id="a653f-106">You can control in Azure AD who has access tooWork.com</span></span>
- <span data-ttu-id="a653f-107">Можно включить на пользователей tooautomatically get вошедшего tooWork.com (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="a653f-107">You can enable your users tooautomatically get signed-on tooWork.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a653f-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a653f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a653f-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a653f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a653f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a653f-110">Prerequisites</span></span>

<span data-ttu-id="a653f-111">tooconfigure интеграция Azure AD с Work.com требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a653f-111">tooconfigure Azure AD integration with Work.com, you need hello following items:</span></span>

- <span data-ttu-id="a653f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a653f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a653f-113">Подписка Work.com с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a653f-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a653f-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a653f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a653f-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a653f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a653f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a653f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a653f-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a653f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a653f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a653f-118">Scenario description</span></span>
<span data-ttu-id="a653f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a653f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a653f-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a653f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a653f-121">Добавление Work.com из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="a653f-121">Add Work.com from hello gallery</span></span>
2. <span data-ttu-id="a653f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a653f-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-hello-gallery"></a><span data-ttu-id="a653f-123">Добавление Work.com из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="a653f-123">Add Work.com from hello gallery</span></span>
<span data-ttu-id="a653f-124">tooconfigure hello интеграции Work.com в Azure AD, вы должны tooadd Work.com из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a653f-124">tooconfigure hello integration of Work.com into Azure AD, you need tooadd Work.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a653f-125">**tooadd Work.com из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a653f-125">**tooadd Work.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a653f-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a653f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a653f-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a653f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a653f-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a653f-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a653f-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a653f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a653f-133">Введите в поле поиска hello **Work.com**выберите **Work.com** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a653f-133">In hello search box, type **Work.com**, select **Work.com** from results panel then click **Add** button tooadd hello application.</span></span>

    ![Добавление из коллекции](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a653f-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a653f-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a653f-136">В этом разделе описана настройка и проверка единого входа Azure AD в Work.com с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a653f-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a653f-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Work.com является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a653f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Work.com is tooa user in Azure AD.</span></span> <span data-ttu-id="a653f-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Work.com должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a653f-138">In other words, a link relationship between an Azure AD user and hello related user in Work.com needs toobe established.</span></span>

<span data-ttu-id="a653f-139">В Work.com, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a653f-139">In Work.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a653f-140">tooconfigure и теста Azure AD единого входа с Work.com, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a653f-140">tooconfigure and test Azure AD single sign-on with Work.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a653f-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a653f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a653f-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a653f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a653f-143">**[Создание тестового пользователя Work.com](#create-a-workcom-test-user)**  -toohave аналог Саймон Britta в Work.com, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a653f-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - toohave a counterpart of Britta Simon in Work.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a653f-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a653f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a653f-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a653f-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a653f-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="a653f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a653f-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Work.com.</span><span class="sxs-lookup"><span data-stu-id="a653f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="a653f-148">tooconfigure единый вход, вы должны toosetup пользовательское имя домена Work.com еще.</span><span class="sxs-lookup"><span data-stu-id="a653f-148">tooconfigure single sign-on, you need toosetup a custom Work.com domain name yet.</span></span> <span data-ttu-id="a653f-149">Требуется по крайней мере домена toodefine имя, проверить имя домена и развернуть ее tooyour всей организации.</span><span class="sxs-lookup"><span data-stu-id="a653f-149">You need toodefine at least a domain name, test your domain name, and deploy it tooyour entire organization.</span></span>

<span data-ttu-id="a653f-150">**tooconfigure Azure AD единого входа с Work.com, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a653f-150">**tooconfigure Azure AD single sign-on with Work.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="a653f-151">В hello в hello портала Azure **Work.com** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a653f-151">In hello Azure portal, on hello **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a653f-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a653f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Параметр "Вход на основе SAML"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="a653f-155">На hello **URL-адреса и домена Work.com** выполните hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a653f-155">On hello **Work.com Domain and URLs** section, perform hello following:</span></span>

    ![Раздел "Домены и URL-адреса приложения Work.com"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="a653f-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="a653f-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a653f-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="a653f-158">This value is not real.</span></span> <span data-ttu-id="a653f-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="a653f-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="a653f-160">Обратитесь к [группа поддержки клиент Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="a653f-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) tooget this value.</span></span> 

4. <span data-ttu-id="a653f-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a653f-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="a653f-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a653f-163">Click **Save** button.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a653f-165">На hello **конфигурации Work.com** щелкните **Настройка Work.com** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="a653f-165">On hello **Work.com Configuration** section, click **Configure Work.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a653f-166">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="a653f-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Раздел "Настройка Work.com"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="a653f-168">Войдите в tooyour Work.com клиента от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="a653f-168">Log in tooyour Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="a653f-169">Go слишком**установки**.</span><span class="sxs-lookup"><span data-stu-id="a653f-169">Go too**Setup**.</span></span>
   
    <span data-ttu-id="a653f-170">![Настройка](./media/active-directory-saas-work-com-tutorial/ic794108.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="a653f-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="a653f-171">На панели навигации слева hello в hello **Администрирование** щелкните **Управление доменами** tooexpand hello соответствующий раздел и нажмите кнопку **Мой домен** tooopen hello  **Мой домен** страницы.</span><span class="sxs-lookup"><span data-stu-id="a653f-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
    <span data-ttu-id="a653f-172">![Мой домен](./media/active-directory-saas-work-com-tutorial/ic767825.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="a653f-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="a653f-173">tooverify, домен настроен неправильно, убедитесь, что он находится в "**шаг 4 развернут tooUsers**» и просмотрите вашей»**мои параметры домена**».</span><span class="sxs-lookup"><span data-stu-id="a653f-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="a653f-174">![Домен развернутые tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser домена развертывания")</span><span class="sxs-lookup"><span data-stu-id="a653f-174">![Domain Deployed tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="a653f-175">Войдите в систему tooyour Work.com клиента.</span><span class="sxs-lookup"><span data-stu-id="a653f-175">Log in tooyour Work.com tenant.</span></span>

12. <span data-ttu-id="a653f-176">Go слишком**установки**.</span><span class="sxs-lookup"><span data-stu-id="a653f-176">Go too**Setup**.</span></span>
    
    <span data-ttu-id="a653f-177">![Настройка](./media/active-directory-saas-work-com-tutorial/ic794108.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="a653f-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="a653f-178">Разверните hello **управления безопасностью** меню, а затем нажмите **параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a653f-178">Expand hello **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="a653f-179">![Параметры единого входа](./media/active-directory-saas-work-com-tutorial/ic794113.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="a653f-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="a653f-180">На hello **параметры единого входа** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a653f-180">On hello **Single Sign-On Settings** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="a653f-181">![Включение SAML](./media/active-directory-saas-work-com-tutorial/ic781026.png "Включение SAML")</span><span class="sxs-lookup"><span data-stu-id="a653f-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="a653f-182">а.</span><span class="sxs-lookup"><span data-stu-id="a653f-182">a.</span></span> <span data-ttu-id="a653f-183">Установите флажок **SAML включен**.</span><span class="sxs-lookup"><span data-stu-id="a653f-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="a653f-184">b.</span><span class="sxs-lookup"><span data-stu-id="a653f-184">b.</span></span> <span data-ttu-id="a653f-185">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a653f-185">Click **New**.</span></span>

15. <span data-ttu-id="a653f-186">В hello **SAML единого входа параметры** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a653f-186">In hello **SAML Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="a653f-187">![Параметры единого входа SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Параметры единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="a653f-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="a653f-188">а.</span><span class="sxs-lookup"><span data-stu-id="a653f-188">a.</span></span> <span data-ttu-id="a653f-189">В hello **имя** текстовом поле введите имя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a653f-189">In hello **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="a653f-190">Предоставить значение для **имя** автоматически заполнять hello **имя API** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a653f-190">Providing a value for **Name** does automatically populate hello **API Name** textbox.</span></span>
    
    <span data-ttu-id="a653f-191">b.</span><span class="sxs-lookup"><span data-stu-id="a653f-191">b.</span></span> <span data-ttu-id="a653f-192">В **издателя** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a653f-192">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a653f-193">c.</span><span class="sxs-lookup"><span data-stu-id="a653f-193">c.</span></span> <span data-ttu-id="a653f-194">сертификат tooupload hello загружен из портала Azure щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="a653f-194">tooupload hello downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="a653f-195">d.</span><span class="sxs-lookup"><span data-stu-id="a653f-195">d.</span></span> <span data-ttu-id="a653f-196">В hello **идентификатор сущности** введите `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="a653f-196">In hello **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="a653f-197">д.</span><span class="sxs-lookup"><span data-stu-id="a653f-197">e.</span></span> <span data-ttu-id="a653f-198">Как **типа удостоверения SAML**выберите **утверждение, содержащее hello идентификатор федерации из объекта пользователя hello**.</span><span class="sxs-lookup"><span data-stu-id="a653f-198">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
    
    <span data-ttu-id="a653f-199">f.</span><span class="sxs-lookup"><span data-stu-id="a653f-199">f.</span></span> <span data-ttu-id="a653f-200">Как **расположения удостоверения SAML**выберите **удостоверение находится в hello элемент NameIdentfier оператора Subject hello**.</span><span class="sxs-lookup"><span data-stu-id="a653f-200">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>
    
    <span data-ttu-id="a653f-201">ж.</span><span class="sxs-lookup"><span data-stu-id="a653f-201">g.</span></span> <span data-ttu-id="a653f-202">В **URL-адрес входа поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a653f-202">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a653f-203">h.</span><span class="sxs-lookup"><span data-stu-id="a653f-203">h.</span></span> <span data-ttu-id="a653f-204">В **URL-адрес выхода поставщика удостоверений** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a653f-204">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a653f-205">i.</span><span class="sxs-lookup"><span data-stu-id="a653f-205">i.</span></span> <span data-ttu-id="a653f-206">В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициированных поставщиком услуг) выберите значение **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="a653f-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="a653f-207">j.</span><span class="sxs-lookup"><span data-stu-id="a653f-207">j.</span></span> <span data-ttu-id="a653f-208">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a653f-208">Click **Save**.</span></span>

16. <span data-ttu-id="a653f-209">В классическом портала Work.com hello левой области навигации, выберите **Управление доменами** tooexpand hello соответствующий раздел и нажмите кнопку **Мой домен** tooopen hello **Мой домен**страницы.</span><span class="sxs-lookup"><span data-stu-id="a653f-209">In your Work.com classic portal, on hello left navigation pane, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="a653f-210">![Мой домен](./media/active-directory-saas-work-com-tutorial/ic794115.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="a653f-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="a653f-211">На hello **Мой домен** страницы в hello **фирменная символика страницы входа** щелкните **изменить**.</span><span class="sxs-lookup"><span data-stu-id="a653f-211">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="a653f-212">![Фирменная символика страницы входа](./media/active-directory-saas-work-com-tutorial/ic767826.png "Фирменная символика страницы входа")</span><span class="sxs-lookup"><span data-stu-id="a653f-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="a653f-213">На hello **фирменная символика страницы входа** страницы в hello **службы проверки подлинности** раздела, название hello вашей **настройки единого входа SAML** отображается.</span><span class="sxs-lookup"><span data-stu-id="a653f-213">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="a653f-214">Выберите его, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a653f-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="a653f-215">![Фирменная символика страницы входа](./media/active-directory-saas-work-com-tutorial/ic784366.png "Фирменная символика страницы входа")</span><span class="sxs-lookup"><span data-stu-id="a653f-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="a653f-216">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a653f-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a653f-217">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a653f-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a653f-218">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a653f-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a653f-219">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a653f-219">Create an Azure AD test user</span></span>
<span data-ttu-id="a653f-220">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a653f-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a653f-222">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a653f-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a653f-223">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a653f-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a653f-225">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a653f-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Выберите "Пользователи и группы" > "Все пользователи".](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a653f-227">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a653f-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Добавить](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a653f-229">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a653f-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a653f-231">а.</span><span class="sxs-lookup"><span data-stu-id="a653f-231">a.</span></span> <span data-ttu-id="a653f-232">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a653f-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a653f-233">b.</span><span class="sxs-lookup"><span data-stu-id="a653f-233">b.</span></span> <span data-ttu-id="a653f-234">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a653f-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a653f-235">c.</span><span class="sxs-lookup"><span data-stu-id="a653f-235">c.</span></span> <span data-ttu-id="a653f-236">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="a653f-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a653f-237">d.</span><span class="sxs-lookup"><span data-stu-id="a653f-237">d.</span></span> <span data-ttu-id="a653f-238">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a653f-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="a653f-239">Создание тестового пользователя Work.com</span><span class="sxs-lookup"><span data-stu-id="a653f-239">Create a Work.com test user</span></span>
<span data-ttu-id="a653f-240">Для Azure Active Directory пользователей toobe может toosign в они должны быть подготовленных tooWork.com. В случае hello Work.com Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="a653f-240">For Azure Active Directory users toobe able toosign in, they must be provisioned tooWork.com. In hello case of Work.com, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="a653f-241">tooconfigure подготовки пользователей, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="a653f-241">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="a653f-242">Войдите на tooyour сайт компании Work.com с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a653f-242">Sign on tooyour Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="a653f-243">Go слишком**установки**.</span><span class="sxs-lookup"><span data-stu-id="a653f-243">Go too**Setup**.</span></span>
   
    <span data-ttu-id="a653f-244">![Настройка](./media/active-directory-saas-work-com-tutorial/IC794108.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="a653f-244">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="a653f-245">Go слишком**Управление пользователями \> пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a653f-245">Go too**Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="a653f-246">![Управление пользователями](./media/active-directory-saas-work-com-tutorial/IC784369.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="a653f-246">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="a653f-247">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="a653f-247">Click **New User**.</span></span>
   
    <span data-ttu-id="a653f-248">![Все пользователи](./media/active-directory-saas-work-com-tutorial/IC794117.png "Все пользователи")</span><span class="sxs-lookup"><span data-stu-id="a653f-248">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="a653f-249">В hello пользователя изменить раздел, выполните следующие шаги в атрибутах допустимым Azure hello текстовые поля, связанные с учетной записью AD, которые должны tooprovision hello:</span><span class="sxs-lookup"><span data-stu-id="a653f-249">In hello User Edit section, perform hello following steps, in attributes of a valid Azure AD account you want tooprovision into hello related textboxes:</span></span>
   
    <span data-ttu-id="a653f-250">![Изменение пользователя](./media/active-directory-saas-work-com-tutorial/ic794118.png "Изменение пользователя")</span><span class="sxs-lookup"><span data-stu-id="a653f-250">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="a653f-251">а.</span><span class="sxs-lookup"><span data-stu-id="a653f-251">a.</span></span> <span data-ttu-id="a653f-252">В hello **имя** в текстовое поле типа hello **имя** пользователя hello **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a653f-252">In hello **First Name** textbox, type hello **first name** of hello user **Britta**.</span></span>
    
    <span data-ttu-id="a653f-253">b.</span><span class="sxs-lookup"><span data-stu-id="a653f-253">b.</span></span> <span data-ttu-id="a653f-254">В hello **Фамилия** в текстовое поле типа hello **Фамилия** пользователя hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a653f-254">In hello **Last Name** textbox, type hello **last name** of hello user **Simon**.</span></span>
    
    <span data-ttu-id="a653f-255">c.</span><span class="sxs-lookup"><span data-stu-id="a653f-255">c.</span></span> <span data-ttu-id="a653f-256">В hello **псевдоним** в текстовое поле типа hello **имя** пользователя hello **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="a653f-256">In hello **Alias** textbox, type hello **name** of hello user **BrittaS**.</span></span>
    
    <span data-ttu-id="a653f-257">d.</span><span class="sxs-lookup"><span data-stu-id="a653f-257">d.</span></span> <span data-ttu-id="a653f-258">В hello **электронной почты** в текстовое поле типа hello **адрес электронной почты** пользователя  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="a653f-258">In hello **Email** textbox, type hello **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="a653f-259">д.</span><span class="sxs-lookup"><span data-stu-id="a653f-259">e.</span></span> <span data-ttu-id="a653f-260">В hello **имя пользователя** текстовое поле, введите имя пользователя, например  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="a653f-260">In hello **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="a653f-261">f.</span><span class="sxs-lookup"><span data-stu-id="a653f-261">f.</span></span> <span data-ttu-id="a653f-262">В hello **псевдоним** текстовом поле введите значение **псевдоним** пользователя **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a653f-262">In hello **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="a653f-263">ж.</span><span class="sxs-lookup"><span data-stu-id="a653f-263">g.</span></span> <span data-ttu-id="a653f-264">Выберите значения параметров **Role** (Роль), **User License** (Пользовательская лицензия) и **Profile** (Профиль).</span><span class="sxs-lookup"><span data-stu-id="a653f-264">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="a653f-265">h.</span><span class="sxs-lookup"><span data-stu-id="a653f-265">h.</span></span> <span data-ttu-id="a653f-266">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a653f-266">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="a653f-267">Владелец учетной записи Hello Azure AD получит сообщение электронной почты, включая учетную запись hello tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="a653f-267">hello Azure AD account holder will get an email including a link tooconfirm hello account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a653f-268">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a653f-268">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a653f-269">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWork.com доступа.</span><span class="sxs-lookup"><span data-stu-id="a653f-269">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWork.com.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a653f-271">**tooassign tooWork.com Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a653f-271">**tooassign Britta Simon tooWork.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="a653f-272">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a653f-272">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a653f-274">В списке приложений hello выберите **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="a653f-274">In hello applications list, select **Work.com**.</span></span>

    ![Work.com в списке приложений](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="a653f-276">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a653f-276">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a653f-278">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a653f-278">Click **Add** button.</span></span> <span data-ttu-id="a653f-279">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a653f-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a653f-281">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a653f-281">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a653f-282">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a653f-282">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a653f-283">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a653f-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a653f-284">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a653f-284">Test single sign-on</span></span>

<span data-ttu-id="a653f-285">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="a653f-285">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a653f-286">При нажатии кнопки hello Work.com плитки в панели доступа hello, вы должны получить tooyour автоматически подписан в приложение Work.com.</span><span class="sxs-lookup"><span data-stu-id="a653f-286">When you click hello Work.com tile in hello Access Panel, you should get automatically signed-on tooyour Work.com application.</span></span>
<span data-ttu-id="a653f-287">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a653f-287">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a653f-288">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a653f-288">Additional resources</span></span>

* [<span data-ttu-id="a653f-289">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a653f-289">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a653f-290">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a653f-290">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

