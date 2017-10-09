---
title: "Руководство по интеграции Azure Active Directory с BlueJeans | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="5ff4e-103">Руководство по интеграции Azure Active Directory с BlueJeans</span><span class="sxs-lookup"><span data-stu-id="5ff4e-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="5ff4e-104">В этом учебнике вы узнаете, как toointegrate BlueJeans с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5ff4e-104">In this tutorial, you learn how toointegrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ff4e-105">Интеграция BlueJeans с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5ff4e-105">Integrating BlueJeans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5ff4e-106">Можно управлять в Azure AD, имеющего доступ tooBlueJeans</span><span class="sxs-lookup"><span data-stu-id="5ff4e-106">You can control in Azure AD who has access tooBlueJeans</span></span>
- <span data-ttu-id="5ff4e-107">Можно включить на пользователей tooautomatically get вошедшего tooBlueJeans (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ff4e-107">You can enable your users tooautomatically get signed-on tooBlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ff4e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5ff4e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5ff4e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ff4e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ff4e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5ff4e-110">Prerequisites</span></span>

<span data-ttu-id="5ff4e-111">tooconfigure интеграция Azure AD с BlueJeans требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5ff4e-111">tooconfigure Azure AD integration with BlueJeans, you need hello following items:</span></span>

- <span data-ttu-id="5ff4e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5ff4e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ff4e-113">подписка BlueJeans с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ff4e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ff4e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="5ff4e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ff4e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ff4e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ff4e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ff4e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5ff4e-118">Scenario description</span></span>
<span data-ttu-id="5ff4e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ff4e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="5ff4e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ff4e-121">Добавление BlueJeans из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5ff4e-121">Adding BlueJeans from hello gallery</span></span>
2. <span data-ttu-id="5ff4e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ff4e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-hello-gallery"></a><span data-ttu-id="5ff4e-123">Добавление BlueJeans из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5ff4e-123">Adding BlueJeans from hello gallery</span></span>
<span data-ttu-id="5ff4e-124">tooconfigure hello интеграции BlueJeans в Azure AD, вы должны tooadd BlueJeans из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-124">tooconfigure hello integration of BlueJeans into Azure AD, you need tooadd BlueJeans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5ff4e-125">**tooadd BlueJeans из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5ff4e-125">**tooadd BlueJeans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ff4e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ff4e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5ff4e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5ff4e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5ff4e-133">Введите в поле поиска hello **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-133">In hello search box, type **BlueJeans**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="5ff4e-135">В панели результатов hello выберите **BlueJeans**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-135">In hello results panel, select **BlueJeans**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ff4e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ff4e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ff4e-138">В этом разделе описана настройка и проверка единого входа Azure AD в BlueJeans с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5ff4e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в BlueJeans является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BlueJeans is tooa user in Azure AD.</span></span> <span data-ttu-id="5ff4e-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в BlueJeans должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-140">In other words, a link relationship between an Azure AD user and hello related user in BlueJeans needs toobe established.</span></span>

<span data-ttu-id="5ff4e-141">В BlueJeans, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-141">In BlueJeans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5ff4e-142">tooconfigure и теста Azure AD единого входа с BlueJeans, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5ff4e-142">tooconfigure and test Azure AD single sign-on with BlueJeans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5ff4e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5ff4e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ff4e-145">**[Создание тестового пользователя BlueJeans](#creating-a-bluejeans-test-user)**  -toohave аналог Саймон Britta в BlueJeans, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - toohave a counterpart of Britta Simon in BlueJeans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ff4e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ff4e-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ff4e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ff4e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ff4e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в BlueJeans приложения.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="5ff4e-150">**tooconfigure Azure AD единого входа с BlueJeans, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5ff4e-150">**tooconfigure Azure AD single sign-on with BlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ff4e-151">В hello в hello портала Azure **BlueJeans** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-151">In hello Azure portal, on hello **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5ff4e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="5ff4e-155">На hello **URL-адреса и домена BlueJeans** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5ff4e-155">On hello **BlueJeans Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="5ff4e-157">а.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-157">a.</span></span> <span data-ttu-id="5ff4e-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="5ff4e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="5ff4e-159">b.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-159">b.</span></span> <span data-ttu-id="5ff4e-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="5ff4e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5ff4e-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-161">These values are not real.</span></span> <span data-ttu-id="5ff4e-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5ff4e-163">Обратитесь к [группа поддержки клиента BlueJeans](https://support.bluejeans.com/contact) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="5ff4e-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="5ff4e-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5ff4e-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5ff4e-168">На hello **конфигурации BlueJeans** щелкните **Настройка BlueJeans** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-168">On hello **BlueJeans Configuration** section, click **Configure BlueJeans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5ff4e-169">Копировать hello **URL-адрес выхода, URL-адрес изменения пароля и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="5ff4e-169">Copy hello **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="5ff4e-171">В другом окне браузера, войдите в tooyour **BlueJeans** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-171">In a different web browser window, log in tooyour **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="5ff4e-172">Go слишком**АДМИНИСТРАТОРА \> параметры группы \> безопасности**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-172">Go too**ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="5ff4e-173">![Администратор](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="5ff4e-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="5ff4e-174">В hello **безопасности** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5ff4e-174">In hello **Security** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="5ff4e-175">![Единый вход SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Единый вход SAML")</span><span class="sxs-lookup"><span data-stu-id="5ff4e-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="5ff4e-176">а.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-176">a.</span></span> <span data-ttu-id="5ff4e-177">Выберите параметр **SAML Single Sign On**(Единый вход SAML).</span><span class="sxs-lookup"><span data-stu-id="5ff4e-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="5ff4e-178">b.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-178">b.</span></span> <span data-ttu-id="5ff4e-179">Установите флажок **Enable automatic provisioning**(Включить автоматическую подготовку).</span><span class="sxs-lookup"><span data-stu-id="5ff4e-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="5ff4e-180">Продолжите и hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="5ff4e-180">Move on with hello following steps:</span></span>

    <span data-ttu-id="5ff4e-181">![Путь к сертификату](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Путь к сертификату")</span><span class="sxs-lookup"><span data-stu-id="5ff4e-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="5ff4e-182">а.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-182">a.</span></span> <span data-ttu-id="5ff4e-183">Нажмите кнопку **выбрать файл**и затем передайте сертификат загружаются hello.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-183">Click **Choose File**, and then upload hello downloaded certificate.</span></span>
   
    <span data-ttu-id="5ff4e-184">b.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-184">b.</span></span> <span data-ttu-id="5ff4e-185">Вставить **SAML единого входа URL-адрес службы** в hello **URL-адрес входа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-185">Paste **SAML Single Sign-On Service URL** into hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="5ff4e-186">c.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-186">c.</span></span> <span data-ttu-id="5ff4e-187">Вставить **URL-адрес изменения пароля** в hello **URL-адрес изменения пароля** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-187">Paste **Change Password URL** into hello **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="5ff4e-188">d.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-188">d.</span></span> <span data-ttu-id="5ff4e-189">Вставить **URL-адрес выхода** в hello **URL-адрес выхода** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-189">Paste **Sign-Out URL** into hello **Logout URL** textbox.</span></span>

11. <span data-ttu-id="5ff4e-190">Продолжите и hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="5ff4e-190">Move on with hello following steps:</span></span>
    
    <span data-ttu-id="5ff4e-191">![Сохранение изменений](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Сохранение изменений")</span><span class="sxs-lookup"><span data-stu-id="5ff4e-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="5ff4e-192">а.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-192">a.</span></span> <span data-ttu-id="5ff4e-193">В hello **идентификатор пользователя** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-193">In hello **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="5ff4e-194">b.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-194">b.</span></span> <span data-ttu-id="5ff4e-195">В hello **электронной почты** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-195">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="5ff4e-196">c.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-196">c.</span></span> <span data-ttu-id="5ff4e-197">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5ff4e-198">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="5ff4e-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5ff4e-199">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5ff4e-200">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5ff4e-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ff4e-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ff4e-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ff4e-202">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5ff4e-204">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5ff4e-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ff4e-205">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ff4e-207">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ff4e-209">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="5ff4e-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ff4e-211">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5ff4e-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ff4e-213">а.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-213">a.</span></span> <span data-ttu-id="5ff4e-214">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ff4e-215">b.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-215">b.</span></span> <span data-ttu-id="5ff4e-216">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ff4e-217">c.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-217">c.</span></span> <span data-ttu-id="5ff4e-218">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5ff4e-219">d.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-219">d.</span></span> <span data-ttu-id="5ff4e-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="5ff4e-221">Создание тестового пользователя BlueJeans</span><span class="sxs-lookup"><span data-stu-id="5ff4e-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="5ff4e-222">Пользователи toolog tooenable Azure AD в tooBlueJeans, их необходимо подготовить в BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-222">tooenable Azure AD users toolog in tooBlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="5ff4e-223">В случае BlueJeans подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="5ff4e-224">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="5ff4e-224">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ff4e-225">Войдите в tooyour **BlueJeans** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-225">Log in tooyour **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="5ff4e-226">Go слишком**АДМИНИСТРАТОРА \> Управление пользователями \> добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-226">Go too**ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="5ff4e-227">![Администратор](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="5ff4e-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="5ff4e-228">Hello **добавить пользователя** вкладка доступна, только если в hello **вкладка "Безопасность"**, **включить автоматическую подготовку** снят.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-228">hello **Add User** tab is only available if, in hello **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="5ff4e-229">В hello **добавить пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5ff4e-229">In hello **Add User** section, perform hello following steps:</span></span>

    <span data-ttu-id="5ff4e-230">![Добавление пользователя](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="5ff4e-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="5ff4e-231">а.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-231">a.</span></span> <span data-ttu-id="5ff4e-232">Введите значение **имя пользователя BlueJeans**, **адрес электронной почты**, **идентификатор собрания BlueJeans**, **секретный код модератора**, **полное имя** , hello **компании** из текстовых полей, связанных с действительной учетной записи AAD, которые должны tooprovision hello.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, hello **Company** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
    
    <span data-ttu-id="5ff4e-233">b.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-233">b.</span></span> <span data-ttu-id="5ff4e-234">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="5ff4e-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="5ff4e-235">Можно использовать любые другие BlueJeans пользователя средства создания учетных записей или интерфейсы API, предоставляемые BlueJeans tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5ff4e-236">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="5ff4e-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5ff4e-237">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBlueJeans доступа.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlueJeans.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5ff4e-239">**tooassign tooBlueJeans Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5ff4e-239">**tooassign Britta Simon tooBlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ff4e-240">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5ff4e-242">В списке приложений hello выберите **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-242">In hello applications list, select **BlueJeans**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="5ff4e-244">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5ff4e-246">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-246">Click **Add** button.</span></span> <span data-ttu-id="5ff4e-247">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5ff4e-249">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5ff4e-250">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ff4e-251">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ff4e-252">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5ff4e-252">Testing single sign-on</span></span>

<span data-ttu-id="5ff4e-253">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5ff4e-254">При нажатии кнопки BlueJeans плитки в панели доступа hello приветствия, должно появиться страница входа BlueJeans приложения.</span><span class="sxs-lookup"><span data-stu-id="5ff4e-254">When you click hello BlueJeans tile in hello Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="5ff4e-255">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5ff4e-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5ff4e-256">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5ff4e-256">Additional resources</span></span>

* [<span data-ttu-id="5ff4e-257">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ff4e-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ff4e-258">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5ff4e-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

