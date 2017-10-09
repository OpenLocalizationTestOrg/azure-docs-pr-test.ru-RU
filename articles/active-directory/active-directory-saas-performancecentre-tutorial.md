---
title: "Руководство по интеграции Azure Active Directory с PerformanceCentre | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и PerformanceCentre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 19781c0087093a67c70dc90072cf1a119bb2ade0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="f1a7f-103">Руководство по интеграции Azure Active Directory с PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="f1a7f-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="f1a7f-104">В этом учебнике вы узнаете, как toointegrate PerformanceCentre с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1a7f-104">In this tutorial, you learn how toointegrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1a7f-105">Интеграция с Azure AD PerformanceCentre предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f1a7f-105">Integrating PerformanceCentre with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1a7f-106">Можно управлять в Azure AD, имеющего доступ tooPerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="f1a7f-106">You can control in Azure AD who has access tooPerformanceCentre</span></span>
- <span data-ttu-id="f1a7f-107">Можно включить на пользователей tooautomatically get вошедшего tooPerformanceCentre (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1a7f-107">You can enable your users tooautomatically get signed-on tooPerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1a7f-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f1a7f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f1a7f-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1a7f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1a7f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f1a7f-110">Prerequisites</span></span>

<span data-ttu-id="f1a7f-111">tooconfigure интеграция Azure AD с PerformanceCentre требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f1a7f-111">tooconfigure Azure AD integration with PerformanceCentre, you need hello following items:</span></span>

- <span data-ttu-id="f1a7f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f1a7f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1a7f-113">подписка PerformanceCentre с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1a7f-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1a7f-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f1a7f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1a7f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1a7f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1a7f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1a7f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f1a7f-118">Scenario description</span></span>
<span data-ttu-id="f1a7f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1a7f-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f1a7f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1a7f-121">Добавление PerformanceCentre из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f1a7f-121">Adding PerformanceCentre from hello gallery</span></span>
2. <span data-ttu-id="f1a7f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1a7f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-hello-gallery"></a><span data-ttu-id="f1a7f-123">Добавление PerformanceCentre из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f1a7f-123">Adding PerformanceCentre from hello gallery</span></span>
<span data-ttu-id="f1a7f-124">tooconfigure hello интеграции PerformanceCentre в Azure AD, вы должны tooadd PerformanceCentre из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-124">tooconfigure hello integration of PerformanceCentre into Azure AD, you need tooadd PerformanceCentre from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1a7f-125">**tooadd PerformanceCentre из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1a7f-125">**tooadd PerformanceCentre from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1a7f-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1a7f-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f1a7f-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f1a7f-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f1a7f-133">Введите в поле поиска hello **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-133">In hello search box, type **PerformanceCentre**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="f1a7f-135">В панели результатов hello выберите **PerformanceCentre**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-135">In hello results panel, select **PerformanceCentre**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1a7f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1a7f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1a7f-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение PerformanceCentre с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1a7f-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в PerformanceCentre является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PerformanceCentre is tooa user in Azure AD.</span></span> <span data-ttu-id="f1a7f-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в PerformanceCentre должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-140">In other words, a link relationship between an Azure AD user and hello related user in PerformanceCentre needs toobe established.</span></span>

<span data-ttu-id="f1a7f-141">В PerformanceCentre, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-141">In PerformanceCentre, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f1a7f-142">tooconfigure и теста Azure AD единого входа с PerformanceCentre, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f1a7f-142">tooconfigure and test Azure AD single sign-on with PerformanceCentre, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1a7f-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1a7f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1a7f-145">**[Создание тестового пользователя PerformanceCentre](#creating-a-performancecentre-test-user)**  -toohave аналог Саймон Britta в PerformanceCentre, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - toohave a counterpart of Britta Simon in PerformanceCentre that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1a7f-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1a7f-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1a7f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1a7f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1a7f-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="f1a7f-150">**tooconfigure Azure AD единого входа с PerformanceCentre, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1a7f-150">**tooconfigure Azure AD single sign-on with PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1a7f-151">В hello в hello портала Azure **PerformanceCentre** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-151">In hello Azure portal, on hello **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f1a7f-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="f1a7f-155">На hello **URL-адреса и домена PerformanceCentre** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f1a7f-155">On hello **PerformanceCentre Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="f1a7f-157">а.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-157">a.</span></span> <span data-ttu-id="f1a7f-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="f1a7f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="f1a7f-159">b.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-159">b.</span></span> <span data-ttu-id="f1a7f-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="f1a7f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1a7f-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-161">These values are not real.</span></span> <span data-ttu-id="f1a7f-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f1a7f-163">Обратитесь к [группа поддержки клиента PerformanceCentre](https://www.performancecentre.com/contact-us/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="f1a7f-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="f1a7f-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f1a7f-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f1a7f-168">На hello **конфигурации PerformanceCentre** щелкните **Настройка PerformanceCentre** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-168">On hello **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f1a7f-169">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="f1a7f-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="f1a7f-171">Tooyour входа **PerformanceCentre** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-171">Sign-on tooyour **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="f1a7f-172">На вкладке hello hello левой стороны, нажмите кнопку **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-172">In hello tab on hello left side, click **Configure**.</span></span>
   
    ![Единый вход в Azure AD][10]

9. <span data-ttu-id="f1a7f-174">На вкладке hello hello левой стороны, нажмите кнопку **Разное**, а затем нажмите кнопку **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-174">In hello tab on hello left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Единый вход в Azure AD][11]

10. <span data-ttu-id="f1a7f-176">В поле **Protocol** (Протокол) выберите **SAML**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Единый вход в Azure AD][12]

11. <span data-ttu-id="f1a7f-178">Откройте скачанный файл метаданных в блокноте копирования содержимого hello, вставьте его в hello **метаданные поставщика удостоверений** текстовое поле, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-178">Open your downloaded metadata file in notepad, copy hello content, paste it into hello **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Единый вход в Azure AD][13]

12. <span data-ttu-id="f1a7f-180">Убедитесь, что hello значения для hello **сущности базовый URL-адрес** и **URL-адрес идентификатор сущности** заданы правильно.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-180">Verify that hello values for hello **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Единый вход в Azure AD][14]

> [!TIP]
> <span data-ttu-id="f1a7f-182">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f1a7f-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f1a7f-183">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f1a7f-184">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1a7f-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1a7f-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1a7f-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1a7f-186">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f1a7f-188">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1a7f-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1a7f-189">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1a7f-191">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1a7f-193">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f1a7f-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1a7f-195">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f1a7f-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1a7f-197">а.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-197">a.</span></span> <span data-ttu-id="f1a7f-198">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1a7f-199">b.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-199">b.</span></span> <span data-ttu-id="f1a7f-200">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1a7f-201">c.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-201">c.</span></span> <span data-ttu-id="f1a7f-202">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f1a7f-203">d.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-203">d.</span></span> <span data-ttu-id="f1a7f-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="f1a7f-205">Создание тестового пользователя PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="f1a7f-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="f1a7f-206">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-206">hello objective of this section is toocreate a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="f1a7f-207">**toocreate пользователя с именем Саймон Britta в PerformanceCentre, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1a7f-207">**toocreate a user called Britta Simon in PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1a7f-208">Войдите на tooyour PerformanceCentre сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-208">Sign on tooyour PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="f1a7f-209">В меню слева hello hello выберите **Interrelate**и нажмите кнопку **создать участника**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-209">In hello menu on hello left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Создание пользователя][400]

3. <span data-ttu-id="f1a7f-211">На hello **между — создать участника** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f1a7f-211">On hello **Interrelate - Create Participant** dialog, perform hello following steps:</span></span>
   
    ![Создание пользователя][401]
    
    <span data-ttu-id="f1a7f-213">а.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-213">a.</span></span> <span data-ttu-id="f1a7f-214">Тип hello необходимые атрибуты для Саймон Britta в соответствующие текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-214">Type hello required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="f1a7f-215">Имя пользователя Britta должен быть атрибут в PerformanceCentre hello так же, как hello имя пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-215">Britta's User Name attribute in PerformanceCentre must be hello same as hello User Name in Azure AD.</span></span>
    
    <span data-ttu-id="f1a7f-216">b.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-216">b.</span></span> <span data-ttu-id="f1a7f-217">Выберите значение **Client Administrator** (Администратор клиента) в поле **Choose Role** (Выберите роль).</span><span class="sxs-lookup"><span data-stu-id="f1a7f-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="f1a7f-218">c.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-218">c.</span></span> <span data-ttu-id="f1a7f-219">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-219">Click **Save**.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f1a7f-220">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f1a7f-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f1a7f-221">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPerformanceCentre доступа.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerformanceCentre.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f1a7f-223">**tooassign tooPerformanceCentre Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1a7f-223">**tooassign Britta Simon tooPerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1a7f-224">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f1a7f-226">В списке приложений hello выберите **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-226">In hello applications list, select **PerformanceCentre**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="f1a7f-228">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f1a7f-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-230">Click **Add** button.</span></span> <span data-ttu-id="f1a7f-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f1a7f-233">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f1a7f-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1a7f-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1a7f-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f1a7f-236">Testing single sign-on</span></span>

<span data-ttu-id="f1a7f-237">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="f1a7f-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="f1a7f-238">При нажатии кнопки hello PerformanceCentre плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour PerformanceCentre приложения.</span><span class="sxs-lookup"><span data-stu-id="f1a7f-238">When you click hello PerformanceCentre tile in hello Access Panel, you should get automatically signed-on tooyour PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1a7f-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f1a7f-239">Additional resources</span></span>

* [<span data-ttu-id="f1a7f-240">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1a7f-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1a7f-241">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1a7f-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

