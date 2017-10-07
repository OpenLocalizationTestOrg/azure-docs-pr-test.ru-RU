---
title: "Руководство по интеграции Azure Active Directory с Predictix Price Reporting | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Predictix Reporting цены."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 691d0c43-3aa1-4220-9e46-e7a88db234ad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: c2ba85f613f5a71de72278a0d1916c135b835b60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-price-reporting"></a><span data-ttu-id="b86cd-103">Учебник. Интеграция Azure Active Directory с Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="b86cd-103">Tutorial: Azure Active Directory integration with Predictix Price Reporting</span></span>

<span data-ttu-id="b86cd-104">В этом учебнике вы узнаете, как toointegrate Predictix цена отчетности в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b86cd-104">In this tutorial, you learn how toointegrate Predictix Price Reporting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b86cd-105">Интеграция с Azure AD Predictix цена Reporting предоставляет следующие преимущества hello:</span><span class="sxs-lookup"><span data-stu-id="b86cd-105">Integrating Predictix Price Reporting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b86cd-106">Можно управлять в Azure AD, имеющего доступ tooPredictix Reporting цены.</span><span class="sxs-lookup"><span data-stu-id="b86cd-106">You can control in Azure AD who has access tooPredictix Price Reporting.</span></span>
- <span data-ttu-id="b86cd-107">Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooPredictix цена Reporting (Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="b86cd-107">You can enable your users tooautomatically get signed-on tooPredictix Price Reporting (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b86cd-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b86cd-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b86cd-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b86cd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b86cd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b86cd-110">Prerequisites</span></span>

<span data-ttu-id="b86cd-111">tooconfigure интеграция Azure AD с Predictix цена отчетов необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b86cd-111">tooconfigure Azure AD integration with Predictix Price Reporting, you need hello following items:</span></span>

- <span data-ttu-id="b86cd-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b86cd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b86cd-113">подписка Predictix Price Reporting с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b86cd-113">A Predictix Price Reporting single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b86cd-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b86cd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b86cd-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b86cd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b86cd-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b86cd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b86cd-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b86cd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b86cd-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b86cd-118">Scenario description</span></span>
<span data-ttu-id="b86cd-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b86cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b86cd-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b86cd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b86cd-121">Добавление Predictix цена отчетов из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b86cd-121">Adding Predictix Price Reporting from hello gallery</span></span>
2. <span data-ttu-id="b86cd-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b86cd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-price-reporting-from-hello-gallery"></a><span data-ttu-id="b86cd-123">Добавление Predictix цена отчетов из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b86cd-123">Adding Predictix Price Reporting from hello gallery</span></span>
<span data-ttu-id="b86cd-124">tooconfigure hello интеграции Predictix цена Reporting в Azure AD, вы должны tooadd Predictix цена отчетов из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b86cd-124">tooconfigure hello integration of Predictix Price Reporting into Azure AD, you need tooadd Predictix Price Reporting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b86cd-125">**tooadd Predictix цена отчетов из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b86cd-125">**tooadd Predictix Price Reporting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b86cd-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b86cd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="b86cd-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b86cd-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="b86cd-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b86cd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="b86cd-133">Введите в поле поиска hello **Reporting цены Predictix**выберите **Reporting цены Predictix** из панели «результат» нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b86cd-133">In hello search box, type **Predictix Price Reporting**, select **Predictix Price Reporting** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Predictix цена отчетов в списке результатов hello](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b86cd-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b86cd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b86cd-136">В этом разделе описана настройка и проверка единого входа Azure AD в Predictix Price Reporting с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b86cd-136">In this section, you configure and test Azure AD single sign-on with Predictix Price Reporting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b86cd-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в отчетности Predictix цена является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b86cd-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Price Reporting is tooa user in Azure AD.</span></span> <span data-ttu-id="b86cd-138">Другими словами связи между пользователя Azure AD и hello связанных пользователей в службах Reporting цены Predictix должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b86cd-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Price Reporting needs toobe established.</span></span>

<span data-ttu-id="b86cd-139">В Predictix цена отчетов, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="b86cd-139">In Predictix Price Reporting, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b86cd-140">tooconfigure и теста Azure AD единого входа с Predictix Reporting цены, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="b86cd-140">tooconfigure and test Azure AD single sign-on with Predictix Price Reporting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b86cd-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b86cd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b86cd-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b86cd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b86cd-143">**[Создание тестового пользователя Reporting цены Predictix](#create-a-predictix-price-reporting-test-user)**  -toohave аналог Саймон Britta в Predictix цена отчетности, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b86cd-143">**[Create a Predictix Price Reporting test user](#create-a-predictix-price-reporting-test-user)** - toohave a counterpart of Britta Simon in Predictix Price Reporting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b86cd-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b86cd-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b86cd-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b86cd-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b86cd-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="b86cd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b86cd-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Predictix Reporting цены.</span><span class="sxs-lookup"><span data-stu-id="b86cd-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Price Reporting application.</span></span>

<span data-ttu-id="b86cd-148">**tooconfigure Azure AD единого входа с Predictix Reporting цены, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="b86cd-148">**tooconfigure Azure AD single sign-on with Predictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="b86cd-149">В hello в hello портала Azure **Reporting цены Predictix** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-149">In hello Azure portal, on hello **Predictix Price Reporting** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="b86cd-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b86cd-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_samlbase.png)

3. <span data-ttu-id="b86cd-153">На hello **URL-адреса и домена Reporting цены Predictix** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b86cd-153">On hello **Predictix Price Reporting Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_url.png)

    <span data-ttu-id="b86cd-155">а.</span><span class="sxs-lookup"><span data-stu-id="b86cd-155">a.</span></span> <span data-ttu-id="b86cd-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname-pricing>.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="b86cd-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname-pricing>.predictix.com/sso/request`</span></span>

    <span data-ttu-id="b86cd-157">b.</span><span class="sxs-lookup"><span data-stu-id="b86cd-157">b.</span></span> <span data-ttu-id="b86cd-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="b86cd-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname-pricing>.predictix.com` |
    | `https://<companyname-pricing>.dev.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="b86cd-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b86cd-159">These values are not real.</span></span> <span data-ttu-id="b86cd-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b86cd-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b86cd-161">Обратитесь к [группа поддержки клиентских отчетов цены Predictix](http://www.infor.com/company/customer-center/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="b86cd-161">Contact [Predictix Price Reporting Client support team](http://www.infor.com/company/customer-center/) tooget these values.</span></span> 
 
4. <span data-ttu-id="b86cd-162">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b86cd-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_certificate.png) 

5. <span data-ttu-id="b86cd-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b86cd-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b86cd-166">На hello **Predictix настройки служб Reporting цены** щелкните **настроить отчеты цены Predictix** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="b86cd-166">On hello **Predictix Price Reporting Configuration** section, click **Configure Predictix Price Reporting** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b86cd-167">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="b86cd-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_configure.png) 

7. <span data-ttu-id="b86cd-169">tooconfigure единого входа на **Reporting цены Predictix** стороны, необходимо загрузить hello toosend **сертификата (Base64)**, **URL-адрес выхода, идентификатор сущности SAML и SAML Single Sign-On URL-адрес службы** слишком[Predictix Reporting Цена Группа поддержки](http://www.infor.com/company/customer-center/).</span><span class="sxs-lookup"><span data-stu-id="b86cd-169">tooconfigure single sign-on on **Predictix Price Reporting** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Predictix Price Reporting support team](http://www.infor.com/company/customer-center/).</span></span> <span data-ttu-id="b86cd-170">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="b86cd-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b86cd-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b86cd-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b86cd-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b86cd-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b86cd-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b86cd-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b86cd-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b86cd-174">Create an Azure AD test user</span></span>

<span data-ttu-id="b86cd-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b86cd-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="b86cd-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b86cd-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b86cd-178">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b86cd-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b86cd-180">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b86cd-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b86cd-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b86cd-184">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b86cd-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b86cd-186">а.</span><span class="sxs-lookup"><span data-stu-id="b86cd-186">a.</span></span> <span data-ttu-id="b86cd-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b86cd-188">b.</span><span class="sxs-lookup"><span data-stu-id="b86cd-188">b.</span></span> <span data-ttu-id="b86cd-189">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b86cd-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b86cd-190">c.</span><span class="sxs-lookup"><span data-stu-id="b86cd-190">c.</span></span> <span data-ttu-id="b86cd-191">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="b86cd-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b86cd-192">d.</span><span class="sxs-lookup"><span data-stu-id="b86cd-192">d.</span></span> <span data-ttu-id="b86cd-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-price-reporting-test-user"></a><span data-ttu-id="b86cd-194">Создание тестового пользователя Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="b86cd-194">Create a Predictix Price Reporting test user</span></span>

<span data-ttu-id="b86cd-195">В этом разделе описано, как создать пользователя Britta Simon в приложении Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="b86cd-195">In this section, you create a user called Britta Simon in Predictix Price Reporting.</span></span> <span data-ttu-id="b86cd-196">Работать с [Predictix Reporting Цена Группа поддержки](http://www.infor.com/company/customer-center/) tooadd hello пользователей на платформе Reporting цены Predictix hello.</span><span class="sxs-lookup"><span data-stu-id="b86cd-196">Work with [Predictix Price Reporting support team](http://www.infor.com/company/customer-center/) tooadd hello users in hello Predictix Price Reporting platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b86cd-197">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b86cd-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b86cd-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooPredictix Reporting цены.</span><span class="sxs-lookup"><span data-stu-id="b86cd-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Price Reporting.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="b86cd-200">**tooassign tooPredictix Britta Simon Reporting цены, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="b86cd-200">**tooassign Britta Simon tooPredictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="b86cd-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b86cd-203">В списке приложений hello выберите **Reporting цены Predictix**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-203">In hello applications list, select **Predictix Price Reporting**.</span></span>

    ![Hello Reporting цены Predictix ссылку в списке приложений hello](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_app.png)  

3. <span data-ttu-id="b86cd-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="b86cd-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-207">Click **Add** button.</span></span> <span data-ttu-id="b86cd-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="b86cd-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b86cd-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b86cd-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b86cd-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b86cd-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b86cd-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b86cd-213">Test single sign-on</span></span>

<span data-ttu-id="b86cd-214">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b86cd-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b86cd-215">При нажатии кнопки hello Reporting цены Predictix плитки в панели доступа hello, вы должны получить приложение Reporting цены Predictix tooyour автоматически вошедшего.</span><span class="sxs-lookup"><span data-stu-id="b86cd-215">When you click hello Predictix Price Reporting tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Price Reporting application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b86cd-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b86cd-216">Additional resources</span></span>

* [<span data-ttu-id="b86cd-217">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b86cd-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b86cd-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b86cd-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_203.png

