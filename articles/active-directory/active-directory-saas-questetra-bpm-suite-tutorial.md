---
title: "Руководство по интеграции Azure Active Directory с Questetra BPM Suite | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="8d2b2-103">Учебник. Интеграция Azure Active Directory с Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="8d2b2-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="8d2b2-104">Hello цель этого учебника — tooshow вы как toointegrate Questetra BPM Suite с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d2b2-104">hello objective of this tutorial is tooshow you how toointegrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="8d2b2-105">Интеграция с Azure AD Questetra BPM Suite предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8d2b2-105">Integrating Questetra BPM Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="8d2b2-106">Можно управлять в Azure AD, имеющего доступ tooQuestetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="8d2b2-106">You can control in Azure AD who has access tooQuestetra BPM Suite</span></span> 
* <span data-ttu-id="8d2b2-107">Ваш пользователей tooautomatically get вошедшего tooQuestetra Suite BPM (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d2b2-107">You can enable your users tooautomatically get signed-on tooQuestetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="8d2b2-108">Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="8d2b2-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="8d2b2-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d2b2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d2b2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8d2b2-110">Prerequisites</span></span>
<span data-ttu-id="8d2b2-111">tooconfigure интеграция Azure AD с набором BPM Questetra требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8d2b2-111">tooconfigure Azure AD integration with Questetra BPM Suite, you need hello following items:</span></span>

* <span data-ttu-id="8d2b2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8d2b2-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8d2b2-113">Подписка [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) с включенным единым входом.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d2b2-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="8d2b2-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8d2b2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8d2b2-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8d2b2-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d2b2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="8d2b2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8d2b2-118">Scenario Description</span></span>
<span data-ttu-id="8d2b2-119">Hello цель этого учебника — tooenable tootest Azure AD единого входа в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="8d2b2-120">Hello сценарий, описанный в этом учебнике состоит из трех основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8d2b2-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="8d2b2-121">Добавление набора BPM Questetra из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8d2b2-121">Adding Questetra BPM Suite from hello gallery</span></span> 
2. <span data-ttu-id="8d2b2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d2b2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a><span data-ttu-id="8d2b2-123">Добавление набора BPM Questetra из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8d2b2-123">Adding Questetra BPM Suite from hello gallery</span></span>
<span data-ttu-id="8d2b2-124">tooconfigure hello интеграции Questetra BPM Suite в Azure AD, вы должны tooadd Questetra BPM набор из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-124">tooconfigure hello integration of Questetra BPM Suite into Azure AD, you need tooadd Questetra BPM Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8d2b2-125">**tooadd Questetra BPM набор из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="8d2b2-125">**tooadd Questetra BPM Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d2b2-126">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="8d2b2-128">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="8d2b2-129">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Приложения][2]

4. <span data-ttu-id="8d2b2-131">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Приложения][3]

5. <span data-ttu-id="8d2b2-133">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Приложения][4]

6. <span data-ttu-id="8d2b2-135">Введите в поле поиска hello **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-135">In hello search box, type **Questetra BPM Suite**.</span></span>
   
    ![Приложения][5]

7. <span data-ttu-id="8d2b2-137">В области результатов hello выберите **Questetra BPM Suite**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-137">In hello results pane, select **Questetra BPM Suite**, and then click **Complete** tooadd hello application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d2b2-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d2b2-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d2b2-139">Цель этого раздела Hello является tooshow как tooconfigure и тестирования Azure AD единого входа с набором BPM Questetra на основе тестового пользователя с именем «Britta Simon».</span><span class="sxs-lookup"><span data-stu-id="8d2b2-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8d2b2-140">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в набор BPM Questetra tooan пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Questetra BPM Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="8d2b2-141">Другими словами связи между пользователя Azure AD и связанных пользователей hello в наборе BPM Questetra должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-141">In other words, a link relationship between an Azure AD user and hello related user in Questetra BPM Suite needs toobe established.</span></span>  
<span data-ttu-id="8d2b2-142">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** Questetra BPM набора.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="8d2b2-143">tooconfigure и тестирования Azure AD единого входа с набором BPM Questetra, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8d2b2-143">tooconfigure and test Azure AD single sign-on with Questetra BPM Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8d2b2-144">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8d2b2-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d2b2-146">**[Создание тестового пользователя Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  -toohave аналог Саймон Britta в наборе BPM Questetra, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - toohave a counterpart of Britta Simon in Questetra BPM Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="8d2b2-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d2b2-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d2b2-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d2b2-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="8d2b2-150">Цель этого раздела Hello — tooenable Azure AD единого входа в hello классический портал Azure и tooconfigure единого входа в приложении Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-150">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="8d2b2-151">**tooconfigure Azure AD единого входа с набором BPM Questetra, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d2b2-151">**tooconfigure Azure AD single sign-on with Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d2b2-152">В классический портал Azure, на hello hello **Questetra BPM Suite** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**  диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-152">In hello Azure classic portal, on hello **Questetra BPM Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Настройка единого входа][8]

2. <span data-ttu-id="8d2b2-154">На hello **предпочитаемый как toosign пользователей на tooQuestetra BPM Suite** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-154">On hello **How would you like users toosign on tooQuestetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Единый вход в Azure AD][9]

3. <span data-ttu-id="8d2b2-156">В другом окне веб-браузера войдите в свой корпоративный веб-сайт **Questetra BPM Suite** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="8d2b2-157">В меню в верхней части hello hello выберите **параметры системы**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-157">In hello menu on hello top, click **System Settings**.</span></span> 
   
    ![Единый вход в Azure AD][10]

5. <span data-ttu-id="8d2b2-159">tooopen hello **SingleSignOnSAML** щелкните **единого входа (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-159">tooopen hello **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Единый вход в Azure AD][11]

6. <span data-ttu-id="8d2b2-161">В классический портал Azure, на hello hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d2b2-161">In hello Azure classic portal, on hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Настройка параметров приложения][13]
   
    <span data-ttu-id="8d2b2-163">а.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-163">a.</span></span> <span data-ttu-id="8d2b2-164">На вас **Questetra BPM Suite** корпоративный сайт в hello в разделе сведений SP, hello копирования **URL-адрес ACS**и вставьте его в hello **на URL-адрес входа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-164">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="8d2b2-165">b.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-165">b.</span></span> <span data-ttu-id="8d2b2-166">На вас **Questetra BPM Suite** корпоративный сайт в hello в разделе сведений SP, hello копирования **идентификатор сущности**и вставьте его в hello **URL-адрес издателя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-166">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **Entity ID**, and then paste it into hello **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="8d2b2-167">c.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-167">c.</span></span> <span data-ttu-id="8d2b2-168">На вас **Questetra BPM Suite** корпоративный сайт в hello в разделе сведений SP, hello копирования **URL-адрес ACS**и вставьте его в hello **URL-адрес ответа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-168">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="8d2b2-169">d.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-169">d.</span></span> <span data-ttu-id="8d2b2-170">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-170">Click **Next**.</span></span>

7. <span data-ttu-id="8d2b2-171">На hello **настроить единый вход в набор BPM Questetra** нажмите кнопку **загрузки сертификата**, а затем сохраните файл сертификата hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-171">On hello **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Настройка единого входа][14]

8. <span data-ttu-id="8d2b2-173">На вас **Questetra BPM Suite** компании сайта, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d2b2-173">On you **Questetra BPM Suite** company site, perform hello following steps:</span></span> 
   
    ![Настройка единого входа][15]
   
    <span data-ttu-id="8d2b2-175">а.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-175">a.</span></span> <span data-ttu-id="8d2b2-176">Выберите пункт **Включить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="8d2b2-177">b.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-177">b.</span></span> <span data-ttu-id="8d2b2-178">На hello классического портала Azure скопируйте hello **URL-адрес издателя** значение, а затем вставьте его в hello **идентификатор сущности** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-178">On hello Azure classic portal, copy hello **Issuer URL** value, and then paste it into hello **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="8d2b2-179">c.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-179">c.</span></span> <span data-ttu-id="8d2b2-180">На hello классического портала Azure скопируйте hello **единого входа URL-адрес службы** значение, а затем вставьте его в hello **входа в URL-адрес страницы** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-180">On hello Azure classic portal, copy hello **Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="8d2b2-181">d.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-181">d.</span></span> <span data-ttu-id="8d2b2-182">На hello классического портала Azure скопируйте hello **URL-адрес службы единого выхода** значение, а затем вставьте его в hello **URL-адрес страницы выхода** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-182">On hello Azure classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="8d2b2-183">д.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-183">e.</span></span> <span data-ttu-id="8d2b2-184">В hello **формата идентификатора имени** введите **urn: oasis: имена: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-184">In hello **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="8d2b2-185">f.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-185">f.</span></span> <span data-ttu-id="8d2b2-186">Создайте файл в кодировке Base-64 из загруженного сертификата.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="8d2b2-187">Дополнительные сведения см. в разделе [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="8d2b2-187">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="8d2b2-188">ж.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-188">g.</span></span> <span data-ttu-id="8d2b2-189">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его в hello **проверки сертификата** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="8d2b2-190">h.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-190">h.</span></span> <span data-ttu-id="8d2b2-191">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-191">Click **Save**.</span></span>

1. <span data-ttu-id="8d2b2-192">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-192">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Что такое Azure AD Connect?][17]

2. <span data-ttu-id="8d2b2-194">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Что такое Azure AD Connect?][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d2b2-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d2b2-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d2b2-197">Цель этого раздела Hello — toocreate тестового пользователя в классический портал Azure, вызывается Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="8d2b2-198">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d2b2-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d2b2-199">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-199">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD][100] 

2. <span data-ttu-id="8d2b2-201">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-201">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="8d2b2-202">Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-202">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD][101] 

4. <span data-ttu-id="8d2b2-204">tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-204">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Создание тестового пользователя Azure AD][102] 

5. <span data-ttu-id="8d2b2-206">На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d2b2-206">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD][103]
   
    <span data-ttu-id="8d2b2-208">а.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-208">a.</span></span> <span data-ttu-id="8d2b2-209">В поле **Тип пользователя** выберите значение **Новый пользователь в вашей организации**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="8d2b2-210">b.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-210">b.</span></span> <span data-ttu-id="8d2b2-211">В имени пользователя hello **textbox**, тип **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-211">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="8d2b2-212">c.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-212">c.</span></span> <span data-ttu-id="8d2b2-213">Нажмите кнопку Далее.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-213">Click Next.</span></span>

6. <span data-ttu-id="8d2b2-214">На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d2b2-214">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Создание тестового пользователя Azure AD][104] 
   
    <span data-ttu-id="8d2b2-216">а.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-216">a.</span></span> <span data-ttu-id="8d2b2-217">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-217">In hello **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="8d2b2-218">b.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-218">b.</span></span> <span data-ttu-id="8d2b2-219">В hello **Фамилия** текстовое поле, тип, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-219">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="8d2b2-220">c.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-220">c.</span></span> <span data-ttu-id="8d2b2-221">В hello **отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-221">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="8d2b2-222">d.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-222">d.</span></span> <span data-ttu-id="8d2b2-223">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-223">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="8d2b2-224">д.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-224">e.</span></span> <span data-ttu-id="8d2b2-225">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-225">Click **Next**.</span></span>

7. <span data-ttu-id="8d2b2-226">На hello **получение временного пароля** странице диалогового окна щелкните **создания**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-226">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD][105]  

8. <span data-ttu-id="8d2b2-228">На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d2b2-228">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD][106]   
   
    <span data-ttu-id="8d2b2-230">а.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-230">a.</span></span> <span data-ttu-id="8d2b2-231">Запишите значение hello hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-231">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="8d2b2-232">b.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-232">b.</span></span> <span data-ttu-id="8d2b2-233">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="8d2b2-234">Создание тестового пользователя Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="8d2b2-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="8d2b2-235">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon Questetra BPM набора.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-235">hello objective of this section is toocreate a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="8d2b2-236">**toocreate пользователя с именем Britta Simon Questetra BPM пакета, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d2b2-236">**toocreate a user called Britta Simon in Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d2b2-237">Корпоративный сайт Questetra BPM Suite tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-237">Sign-on tooyour Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="8d2b2-238">Go слишком**параметры системы > список пользователей > нового пользователя**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-238">Go too**System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="8d2b2-239">В диалоговом окне Новый пользователь hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-239">On hello New User dialog, perform hello following steps:</span></span> 
   
    ![Создание тестового пользователя][300] 
   
    <span data-ttu-id="8d2b2-241">а.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-241">a.</span></span> <span data-ttu-id="8d2b2-242">В hello **имя** текстовом поле введите имя пользователя Britta в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-242">In hello **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="8d2b2-243">b.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-243">b.</span></span> <span data-ttu-id="8d2b2-244">В hello **электронной почты** текстовом поле введите имя пользователя Britta в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-244">In hello **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="8d2b2-245">c.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-245">c.</span></span> <span data-ttu-id="8d2b2-246">В hello **пароль** введите пароль.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-246">In hello **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="8d2b2-247">Нажмите кнопку **Добавить нового пользователя**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-247">Click **Add new user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8d2b2-248">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8d2b2-248">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="8d2b2-249">Hello цель этого раздела — tooenabling toouse Britta Simon Azure единого входа, предоставляя свой доступ tooQuestetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-249">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooQuestetra BPM Suite.</span></span>

![Что такое Azure AD Connect?][200]

<span data-ttu-id="8d2b2-251">**tooassign tooQuestetra Britta Simon BPM Suite выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="8d2b2-251">**tooassign Britta Simon tooQuestetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d2b2-252">Hello Azure представления приложения hello tooopen в представлении каталога hello классического портала щелкните **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-252">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Что такое Azure AD Connect?][201]
2. <span data-ttu-id="8d2b2-254">В списке приложений hello выберите **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-254">In hello applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Что такое Azure AD Connect?][205]
3. <span data-ttu-id="8d2b2-256">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-256">In hello menu on hello top, click **Users**.</span></span>
   
    ![Что такое Azure AD Connect?][202]
4. <span data-ttu-id="8d2b2-258">В списке пользователей hello выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-258">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Что такое Azure AD Connect?][203]
5. <span data-ttu-id="8d2b2-260">В нижней hello hello инструментов, нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-260">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Что такое Azure AD Connect?][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="8d2b2-262">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8d2b2-262">Testing Single Sign-On</span></span>
<span data-ttu-id="8d2b2-263">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="8d2b2-263">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="8d2b2-264">При выборе плитки Questetra BPM Suite hello в hello панели доступа, вы должны получить приложению автоматически вошедшего tooyour Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-264">When you click hello Questetra BPM Suite tile in hello Access Panel, you should get automatically signed-on tooyour Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d2b2-265">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8d2b2-265">Additional Resources</span></span>
* [<span data-ttu-id="8d2b2-266">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d2b2-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d2b2-267">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d2b2-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
