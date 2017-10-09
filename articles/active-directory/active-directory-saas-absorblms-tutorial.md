---
title: "Руководство. Интеграция Azure Active Directory с Absorb LMS | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LMS запоминаются."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="0763e-103">Руководство. Интеграция Azure Active Directory с Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="0763e-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="0763e-104">В этом учебнике вы узнаете, как toointegrate Absorb LMS с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0763e-104">In this tutorial, you learn how toointegrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0763e-105">Интеграция LMS справиться с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0763e-105">Integrating Absorb LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0763e-106">Можно управлять в Azure AD, имеющего доступ tooAbsorb LMS</span><span class="sxs-lookup"><span data-stu-id="0763e-106">You can control in Azure AD who has access tooAbsorb LMS</span></span>
- <span data-ttu-id="0763e-107">Можно включить на пользователей tooautomatically get вошедшего tooAbsorb LMS (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="0763e-107">You can enable your users tooautomatically get signed-on tooAbsorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0763e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0763e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0763e-109">Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0763e-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="0763e-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0763e-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0763e-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0763e-111">Prerequisites</span></span>

<span data-ttu-id="0763e-112">tooconfigure интеграция Azure AD с запоминаются LMS требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0763e-112">tooconfigure Azure AD integration with Absorb LMS, you need hello following items:</span></span>

- <span data-ttu-id="0763e-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0763e-113">An Azure AD subscription</span></span>
- <span data-ttu-id="0763e-114">подписка Absorb LMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0763e-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0763e-115">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="0763e-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0763e-116">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="0763e-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0763e-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0763e-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0763e-118">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0763e-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0763e-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0763e-119">Scenario description</span></span>
<span data-ttu-id="0763e-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0763e-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0763e-121">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="0763e-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0763e-122">Добавление запоминаются LMS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0763e-122">Adding Absorb LMS from hello gallery</span></span>
2. <span data-ttu-id="0763e-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0763e-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-hello-gallery"></a><span data-ttu-id="0763e-124">Добавление запоминаются LMS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0763e-124">Adding Absorb LMS from hello gallery</span></span>
<span data-ttu-id="0763e-125">tooconfigure hello интеграции запоминаются LMS в tooAzure AD, вы должны tooadd Absorb LMS из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0763e-125">tooconfigure hello integration of Absorb LMS in tooAzure AD, you need tooadd Absorb LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0763e-126">**tooadd Absorb LMS из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0763e-126">**tooadd Absorb LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0763e-127">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0763e-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="0763e-129">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="0763e-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0763e-130">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0763e-130">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="0763e-132">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0763e-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="0763e-134">Введите в поле поиска hello **запоминаются LMS**выберите **запоминаются LMS** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0763e-134">In hello search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Запоминаются LMS в списке результатов hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0763e-136">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0763e-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0763e-137">В этом разделе описана настройка и проверка единого входа Azure AD в Absorb LMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0763e-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0763e-138">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в запоминаются LMS является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0763e-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Absorb LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="0763e-139">Другими словами связи между пользователя Azure AD и связанных пользователей hello в запоминаются LMS должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="0763e-139">In other words, a link relationship between an Azure AD user and hello related user in Absorb LMS needs toobe established.</span></span>

<span data-ttu-id="0763e-140">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в LMS запоминаются.</span><span class="sxs-lookup"><span data-stu-id="0763e-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Absorb LMS.</span></span>

<span data-ttu-id="0763e-141">tooconfigure и теста Azure AD единого входа с запоминаются LMS, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0763e-141">tooconfigure and test Azure AD single sign-on with Absorb LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0763e-142">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="0763e-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0763e-143">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0763e-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0763e-144">**[Создание тестового пользователя, прошедшего запоминаются LMS](#create-an-absorb-lms-test-user)**  -toohave аналог Саймон Britta в запоминаются LMS, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="0763e-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - toohave a counterpart of Britta Simon in Absorb LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0763e-145">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="0763e-145">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0763e-146">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0763e-146">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0763e-147">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="0763e-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0763e-148">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LMS запоминаются.</span><span class="sxs-lookup"><span data-stu-id="0763e-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="0763e-149">**tooconfigure Azure AD единого входа с запоминаются управления Обучением выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0763e-149">**tooconfigure Azure AD single sign-on with Absorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="0763e-150">В hello в hello портала Azure **запоминаются LMS** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0763e-150">In hello Azure portal, on hello **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="0763e-152">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="0763e-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="0763e-154">На hello **URL-адреса и домена запоминаются LMS** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0763e-154">On hello **Absorb LMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="0763e-156">а.</span><span class="sxs-lookup"><span data-stu-id="0763e-156">a.</span></span> <span data-ttu-id="0763e-157">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="0763e-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="0763e-158">b.</span><span class="sxs-lookup"><span data-stu-id="0763e-158">b.</span></span> <span data-ttu-id="0763e-159">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="0763e-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0763e-160">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="0763e-160">These values are not hello real.</span></span> <span data-ttu-id="0763e-161">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="0763e-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="0763e-162">Обратитесь к [группа поддержки запоминаются клиента LMS](https://www.absorblms.com/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="0763e-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) tooget these values.</span></span> 

4. <span data-ttu-id="0763e-163">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="0763e-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="0763e-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0763e-165">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="0763e-167">На hello **запоминаются конфигурации LMS** щелкните **Настройка запоминаются LMS** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="0763e-167">On hello **Absorb LMS Configuration** section, click **Configure Absorb LMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0763e-168">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="0763e-168">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="0763e-170">В другом окне браузера Войдите на сайте компании запоминаются LMS tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="0763e-170">In a different web browser window, log in tooyour Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="0763e-171">Нажмите кнопку hello **значок учетной записи** в интерфейсе администратора hello.</span><span class="sxs-lookup"><span data-stu-id="0763e-171">Click hello **Account Icon** on hello admin interface.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="0763e-173">Щелкните **Параметры портала**.</span><span class="sxs-lookup"><span data-stu-id="0763e-173">Click **Portal Settings**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="0763e-175">Нажмите кнопку hello **пользователей** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0763e-175">Click hello **Users** tab.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="0763e-177">Выполните следующие шаги tooaccess hello единым входом поля конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="0763e-177">Perform hello following steps tooaccess hello Single Sign-On configuration fields:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="0763e-179">а.</span><span class="sxs-lookup"><span data-stu-id="0763e-179">a.</span></span> <span data-ttu-id="0763e-180">Выберите hello соответствующие **режим**.</span><span class="sxs-lookup"><span data-stu-id="0763e-180">Select hello appropriate **Mode**.</span></span>

    <span data-ttu-id="0763e-181">b.</span><span class="sxs-lookup"><span data-stu-id="0763e-181">b.</span></span> <span data-ttu-id="0763e-182">Привет открыть сертификат, загруженный из hello портал Azure в блокноте, удалите hello **---BEGIN CERTIFICATE---** и **---конечный СЕРТИФИКАТ---** тега, а затем вставьте hello оставшееся содержимое Hello **ключ** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="0763e-182">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Key** textbox.</span></span>
    
    <span data-ttu-id="0763e-183">c.</span><span class="sxs-lookup"><span data-stu-id="0763e-183">c.</span></span> <span data-ttu-id="0763e-184">В hello **свойства Id**, Здравствуйте, выберите соответствующий атрибут, который вы настроили как hello идентификатор пользователя в hello Azure AD (например, при выборе hello userprinciplename в Azure AD, имя пользователя будет выбираться здесь.)</span><span class="sxs-lookup"><span data-stu-id="0763e-184">In hello **Id Property**, select hello appropriate attribute which you have configured as hello user identifier in hello Azure AD (For example, If hello userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="0763e-185">d.</span><span class="sxs-lookup"><span data-stu-id="0763e-185">d.</span></span> <span data-ttu-id="0763e-186">В hello **URL-адрес входа**, вставьте hello **«SAML единого входа URL-адрес службы»** значением, скопированным из hello **Настройка входа** окно hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0763e-186">In hello **Login URL**, paste hello **“SAML Single Sign-On Service URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="0763e-187">д.</span><span class="sxs-lookup"><span data-stu-id="0763e-187">e.</span></span> <span data-ttu-id="0763e-188">В hello **URL-адрес выхода**, вставьте hello **«URL-адрес выхода»** значением, скопированным из hello **Настройка входа** окно hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0763e-188">In hello **Logout URL**, paste hello **“Sign-Out URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

13. <span data-ttu-id="0763e-189">Включите параметр **Only Allow SSO Login** (Разрешить только единый вход).</span><span class="sxs-lookup"><span data-stu-id="0763e-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="0763e-191">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0763e-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="0763e-192">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="0763e-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0763e-193">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="0763e-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0763e-194">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0763e-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0763e-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0763e-195">Create an Azure AD test user</span></span>

<span data-ttu-id="0763e-196">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0763e-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="0763e-198">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0763e-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0763e-199">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0763e-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0763e-201">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="0763e-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0763e-203">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0763e-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0763e-205">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0763e-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0763e-207">а.</span><span class="sxs-lookup"><span data-stu-id="0763e-207">a.</span></span> <span data-ttu-id="0763e-208">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0763e-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0763e-209">b.</span><span class="sxs-lookup"><span data-stu-id="0763e-209">b.</span></span> <span data-ttu-id="0763e-210">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0763e-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0763e-211">c.</span><span class="sxs-lookup"><span data-stu-id="0763e-211">c.</span></span> <span data-ttu-id="0763e-212">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="0763e-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0763e-213">d.</span><span class="sxs-lookup"><span data-stu-id="0763e-213">d.</span></span> <span data-ttu-id="0763e-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0763e-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="0763e-215">Создание тестового пользователя Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="0763e-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="0763e-216">Пользователи toolog tooenable Azure AD в tooAbsorb LMS, их необходимо подготовить в tooAbsorb управления Обучением.</span><span class="sxs-lookup"><span data-stu-id="0763e-216">tooenable Azure AD users toolog in tooAbsorb LMS, they must be provisioned in tooAbsorb LMS.</span></span>  
<span data-ttu-id="0763e-217">Эта подготовка для Absorb LMS выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="0763e-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="0763e-218">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0763e-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="0763e-219">Войдите в систему tooyour запоминаются LMS сайт компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="0763e-219">Log in tooyour Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="0763e-220">Откройте вкладку **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="0763e-220">Click **Users** tab.</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="0763e-222">Нажмите кнопку **пользователей** под hello **пользователей** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0763e-222">Click **Users** under hello **Users** tab.</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="0763e-224">Выберите **Пользователя** в раскрывающемся списке **Добавить новый**.</span><span class="sxs-lookup"><span data-stu-id="0763e-224">Select **User** from **Add New** drop-down.</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="0763e-226">На hello **добавить пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0763e-226">On hello **Add User** page, perform hello following steps:</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="0763e-228">а.</span><span class="sxs-lookup"><span data-stu-id="0763e-228">a.</span></span> <span data-ttu-id="0763e-229">В hello **имя** текстовое поле, имя первого типа hello как Britta.</span><span class="sxs-lookup"><span data-stu-id="0763e-229">In hello **First Name** textbox, type hello first name like Britta.</span></span>

    <span data-ttu-id="0763e-230">b.</span><span class="sxs-lookup"><span data-stu-id="0763e-230">b.</span></span> <span data-ttu-id="0763e-231">В hello **Фамилия** текстовое поле, имя последнего типа hello как Simon.</span><span class="sxs-lookup"><span data-stu-id="0763e-231">In hello **Last Name** textbox, type hello last name like Simon.</span></span>
    
    <span data-ttu-id="0763e-232">c.</span><span class="sxs-lookup"><span data-stu-id="0763e-232">c.</span></span> <span data-ttu-id="0763e-233">В hello **Username** текстовом поле введите имя пользователя hello как Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0763e-233">In hello **Username** textbox, type hello user name like Britta Simon.</span></span>

    <span data-ttu-id="0763e-234">d.</span><span class="sxs-lookup"><span data-stu-id="0763e-234">d.</span></span> <span data-ttu-id="0763e-235">В hello **пароль** текстового поля, типа hello пароль Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0763e-235">In hello **Password** textbox, type hello password of Britta Simon.</span></span>

    <span data-ttu-id="0763e-236">д.</span><span class="sxs-lookup"><span data-stu-id="0763e-236">e.</span></span> <span data-ttu-id="0763e-237">В hello **подтверждение пароля** текстового поля, типа hello одинаковый пароль.</span><span class="sxs-lookup"><span data-stu-id="0763e-237">In hello **Confirm Password** textbox, type hello same password.</span></span>
    
    <span data-ttu-id="0763e-238">f.</span><span class="sxs-lookup"><span data-stu-id="0763e-238">f.</span></span> <span data-ttu-id="0763e-239">Выберите значение **Активно**.</span><span class="sxs-lookup"><span data-stu-id="0763e-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="0763e-240">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0763e-240">Click **"Save."**</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0763e-241">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="0763e-241">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0763e-242">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="0763e-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbsorb LMS.</span></span>

![Назначение пользователям ролей hello][200]

<span data-ttu-id="0763e-244">**tooassign tooAbsorb Britta Simon управления Обучением выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="0763e-244">**tooassign Britta Simon tooAbsorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="0763e-245">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0763e-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0763e-247">В списке приложений hello выберите **запоминаются LMS**.</span><span class="sxs-lookup"><span data-stu-id="0763e-247">In hello applications list, select **Absorb LMS**.</span></span>

    ![ссылка запоминаются LMS Hello в списке приложений hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="0763e-249">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="0763e-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202] 

4. <span data-ttu-id="0763e-251">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0763e-251">Click **Add** button.</span></span> <span data-ttu-id="0763e-252">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0763e-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="0763e-254">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="0763e-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0763e-255">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0763e-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0763e-256">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0763e-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0763e-257">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0763e-257">Test single sign-on</span></span>

<span data-ttu-id="0763e-258">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="0763e-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0763e-259">Нажмите кнопку hello запоминаются LMS плитки в панели доступа hello вы получите tooyour автоматически вошедшего запоминаются LMS приложения.</span><span class="sxs-lookup"><span data-stu-id="0763e-259">Click hello Absorb LMS tile in hello Access Panel, you will get automatically signed-on tooyour Absorb LMS application.</span></span> <span data-ttu-id="0763e-260">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="0763e-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0763e-261">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0763e-261">Additional resources</span></span>

* [<span data-ttu-id="0763e-262">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0763e-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0763e-263">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0763e-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

