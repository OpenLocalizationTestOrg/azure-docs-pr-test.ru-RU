---
title: "Учебник. Интеграция Azure Active Directory с Front | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и передней панели."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="2a966-103">Учебник. Интеграция Azure Active Directory с Front</span><span class="sxs-lookup"><span data-stu-id="2a966-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="2a966-104">В этом учебнике вы узнаете, как toointegrate передней панели с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2a966-104">In this tutorial, you learn how toointegrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2a966-105">Интеграция с Azure AD передней предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="2a966-105">Integrating Front with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2a966-106">Можно управлять в Azure AD, имеющего доступ tooFront.</span><span class="sxs-lookup"><span data-stu-id="2a966-106">You can control in Azure AD who has access tooFront.</span></span>
- <span data-ttu-id="2a966-107">Можно включить на пользователей tooautomatically get вошедшего tooFront (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a966-107">You can enable your users tooautomatically get signed-on tooFront (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2a966-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2a966-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="2a966-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2a966-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a966-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2a966-110">Prerequisites</span></span>

<span data-ttu-id="2a966-111">Интеграция tooconfigure Azure AD с частотой, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="2a966-111">tooconfigure Azure AD integration with Front, you need hello following items:</span></span>

- <span data-ttu-id="2a966-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="2a966-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2a966-113">подписка с поддержкой единого входа Front.</span><span class="sxs-lookup"><span data-stu-id="2a966-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2a966-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="2a966-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2a966-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="2a966-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2a966-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="2a966-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2a966-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a966-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2a966-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="2a966-118">Scenario description</span></span>
<span data-ttu-id="2a966-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="2a966-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2a966-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="2a966-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2a966-121">Добавление передней из галереи hello</span><span class="sxs-lookup"><span data-stu-id="2a966-121">Adding Front from hello gallery</span></span>
2. <span data-ttu-id="2a966-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a966-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-hello-gallery"></a><span data-ttu-id="2a966-123">Добавление передней из галереи hello</span><span class="sxs-lookup"><span data-stu-id="2a966-123">Adding Front from hello gallery</span></span>
<span data-ttu-id="2a966-124">tooconfigure hello интеграции передней панели в Azure AD, вы должны tooadd передний план из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="2a966-124">tooconfigure hello integration of Front into Azure AD, you need tooadd Front from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2a966-125">**tooadd передней из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="2a966-125">**tooadd Front from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a966-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="2a966-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="2a966-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="2a966-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2a966-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2a966-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="2a966-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="2a966-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="2a966-133">Введите в поле поиска hello **передней**выберите **передней** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2a966-133">In hello search box, type **Front**, select **Front** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Передний план в списке результатов hello](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2a966-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a966-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2a966-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Front с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a966-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2a966-137">Для единого входа toowork Azure AD необходима tooknow какие hello аналог пользователь на переднем плане является tooa пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a966-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Front is tooa user in Azure AD.</span></span> <span data-ttu-id="2a966-138">Другими словами связи между пользователя Azure AD и hello связанных пользователей на переднем плане должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="2a966-138">In other words, a link relationship between an Azure AD user and hello related user in Front needs toobe established.</span></span>

<span data-ttu-id="2a966-139">На переднем плане, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="2a966-139">In Front, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2a966-140">tooconfigure и теста Azure AD единого входа с частотой, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="2a966-140">tooconfigure and test Azure AD single sign-on with Front, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2a966-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="2a966-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2a966-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="2a966-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2a966-143">**[Создание тестового пользователя передней](#create-a-front-test-user)**  -toohave аналог Саймон Britta на переднем плане, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="2a966-143">**[Create a Front test user](#create-a-front-test-user)** - toohave a counterpart of Britta Simon in Front that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2a966-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="2a966-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2a966-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2a966-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2a966-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a966-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2a966-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении передней панели.</span><span class="sxs-lookup"><span data-stu-id="2a966-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="2a966-148">**tooconfigure Azure AD единого входа с помощью передней панели, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2a966-148">**tooconfigure Azure AD single sign-on with Front, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a966-149">В hello в hello портала Azure **передней** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="2a966-149">In hello Azure portal, on hello **Front** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="2a966-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="2a966-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="2a966-153">На hello **внешнего домена и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="2a966-153">On hello **Front Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="2a966-155">а.</span><span class="sxs-lookup"><span data-stu-id="2a966-155">a.</span></span> <span data-ttu-id="2a966-156">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="2a966-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="2a966-157">b.</span><span class="sxs-lookup"><span data-stu-id="2a966-157">b.</span></span> <span data-ttu-id="2a966-158">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="2a966-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="2a966-159">Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="2a966-159">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="2a966-161">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="2a966-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2a966-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="2a966-162">These values are not real.</span></span> <span data-ttu-id="2a966-163">Обновление, эти значения с hello фактический идентификатор, URL-адрес ответа и URL-адрес входа которых приведены далее в учебнике или контакт [группа поддержки внешнего клиента](mailto:support@frontapp.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="2a966-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) tooget these values.</span></span> 

5. <span data-ttu-id="2a966-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="2a966-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="2a966-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="2a966-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2a966-168">На hello **передней конфигурации** щелкните **Настройка передней** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="2a966-168">On hello **Front Configuration** section, click **Configure Front** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2a966-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="2a966-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="2a966-171">Клиент передней tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="2a966-171">Sign-on tooyour Front tenant as an administrator.</span></span>

9. <span data-ttu-id="2a966-172">Go слишком**параметры (значок шестеренки hello нижней части левой боковой панели hello) > Параметры**.</span><span class="sxs-lookup"><span data-stu-id="2a966-172">Go too**Settings (cog icon at hello bottom of hello left sidebar) > Preferences**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="2a966-174">Щелкните ссылку **Single Sign On** (Единый вход).</span><span class="sxs-lookup"><span data-stu-id="2a966-174">Click **Single Sign On** link.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="2a966-176">Выберите **SAML** в раскрывающемся списке hello **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="2a966-176">Select **SAML** in hello drop-down list of **Single Sign On**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="2a966-178">В hello **точки входа** textbox помещение значения hello **входа адрес службы единого** из мастера настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a966-178">In hello **Entry Point** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="2a966-180">Откройте ваш загруженный **Certificate(Base64)** в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат подписи** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="2a966-180">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Signing certificate** textbox.</span></span>
    
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="2a966-182">На hello **параметры поставщика службы** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2a966-182">On hello **Service provider settings** section, perform hello following steps:</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="2a966-184">а.</span><span class="sxs-lookup"><span data-stu-id="2a966-184">a.</span></span> <span data-ttu-id="2a966-185">Скопируйте значение hello **идентификатор сущности** и вставьте его в hello **идентификатор** текстовое поле в **внешнего домена и URL-адреса** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2a966-185">Copy hello value of **Entity ID** and paste it into hello **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="2a966-186">b.</span><span class="sxs-lookup"><span data-stu-id="2a966-186">b.</span></span> <span data-ttu-id="2a966-187">Скопируйте значение hello **URL-адрес ACS** и вставьте его в hello **URL-адрес входа** текстовое поле в **внешнего домена и URL-адреса** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2a966-187">Copy hello value of **ACS URL** and paste it into hello **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="2a966-188">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="2a966-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="2a966-189">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="2a966-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2a966-190">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="2a966-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2a966-191">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2a966-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2a966-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a966-192">Create an Azure AD test user</span></span>

<span data-ttu-id="2a966-193">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2a966-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="2a966-195">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2a966-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a966-196">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="2a966-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2a966-198">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2a966-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2a966-200">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="2a966-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2a966-202">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2a966-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2a966-204">а.</span><span class="sxs-lookup"><span data-stu-id="2a966-204">a.</span></span> <span data-ttu-id="2a966-205">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2a966-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2a966-206">b.</span><span class="sxs-lookup"><span data-stu-id="2a966-206">b.</span></span> <span data-ttu-id="2a966-207">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="2a966-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="2a966-208">c.</span><span class="sxs-lookup"><span data-stu-id="2a966-208">c.</span></span> <span data-ttu-id="2a966-209">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="2a966-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="2a966-210">d.</span><span class="sxs-lookup"><span data-stu-id="2a966-210">d.</span></span> <span data-ttu-id="2a966-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2a966-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="2a966-212">Создание тестового пользователя Front</span><span class="sxs-lookup"><span data-stu-id="2a966-212">Create a Front test user</span></span>

<span data-ttu-id="2a966-213">В этом разделе описано, как создать пользователя Britta Simon в приложении Front.</span><span class="sxs-lookup"><span data-stu-id="2a966-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="2a966-214">Работать с [группа поддержки внешнего клиента](mailto:support@frontapp.com) для добавления пользователей hello в платформе передней hello.</span><span class="sxs-lookup"><span data-stu-id="2a966-214">Work with [Front Client support team](mailto:support@frontapp.com) to add hello users in hello Front platform.</span></span> <span data-ttu-id="2a966-215">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="2a966-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2a966-216">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="2a966-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2a966-217">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooFront доступа.</span><span class="sxs-lookup"><span data-stu-id="2a966-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFront.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="2a966-219">**tooassign tooFront Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2a966-219">**tooassign Britta Simon tooFront, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a966-220">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2a966-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="2a966-222">В списке приложений hello выберите **передней**.</span><span class="sxs-lookup"><span data-stu-id="2a966-222">In hello applications list, select **Front**.</span></span>

    ![ссылка передней Hello в списке приложений hello](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="2a966-224">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="2a966-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="2a966-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2a966-226">Click **Add** button.</span></span> <span data-ttu-id="2a966-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2a966-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="2a966-229">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="2a966-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2a966-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="2a966-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2a966-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="2a966-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2a966-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="2a966-232">Test single sign-on</span></span>

<span data-ttu-id="2a966-233">Цель этого раздела Hello — tootest Azure AD SSOconfiguration с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="2a966-233">hello objective of this section is tootest your Azure AD SSOconfiguration using hello Access Panel.</span></span>

<span data-ttu-id="2a966-234">Если щелкнуть плитку передней hello в hello панели доступа, вы должны получить tooyour автоматически подписан на передней панели приложения.</span><span class="sxs-lookup"><span data-stu-id="2a966-234">When you click hello Front tile in hello Access Panel, you should get automatically signed-on tooyour Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2a966-235">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2a966-235">Additional resources</span></span>

* [<span data-ttu-id="2a966-236">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a966-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2a966-237">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2a966-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

