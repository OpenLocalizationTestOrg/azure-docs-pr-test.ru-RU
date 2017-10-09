---
title: "Руководство по интеграции Azure Active Directory с Qlik Sense Enterprise | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и корпоративный Qlik смысле."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="59e1d-103">Руководство. Интеграция Azure Active Directory с Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="59e1d-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="59e1d-104">В этом учебнике вы узнаете, как toointegrate Qlik смысле предприятия в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59e1d-104">In this tutorial, you learn how toointegrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59e1d-105">Интеграция Qlik смысле предприятия с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="59e1d-105">Integrating Qlik Sense Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="59e1d-106">Можно управлять в Azure AD, имеющего доступ tooQlik смысле предприятия.</span><span class="sxs-lookup"><span data-stu-id="59e1d-106">You can control in Azure AD who has access tooQlik Sense Enterprise.</span></span>
- <span data-ttu-id="59e1d-107">Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooQlik смысле предприятия (Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="59e1d-107">You can enable your users tooautomatically get signed-on tooQlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="59e1d-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="59e1d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="59e1d-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="59e1d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59e1d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="59e1d-110">Prerequisites</span></span>

<span data-ttu-id="59e1d-111">tooconfigure интеграция Azure AD с Qlik смысле предприятия необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="59e1d-111">tooconfigure Azure AD integration with Qlik Sense Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="59e1d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="59e1d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59e1d-113">подписка Qlik Sense Enterprise с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="59e1d-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59e1d-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="59e1d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59e1d-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="59e1d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59e1d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="59e1d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59e1d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59e1d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59e1d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="59e1d-118">Scenario description</span></span>
<span data-ttu-id="59e1d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="59e1d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59e1d-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="59e1d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59e1d-121">Добавление Qlik смысле Enterprise из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="59e1d-121">Adding Qlik Sense Enterprise from hello gallery</span></span>
2. <span data-ttu-id="59e1d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e1d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a><span data-ttu-id="59e1d-123">Добавление Qlik смысле Enterprise из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="59e1d-123">Adding Qlik Sense Enterprise from hello gallery</span></span>
<span data-ttu-id="59e1d-124">tooconfigure hello интеграции Qlik смысле предприятия в Azure AD, вы должны tooadd Enterprise смысле Qlik из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="59e1d-124">tooconfigure hello integration of Qlik Sense Enterprise into Azure AD, you need tooadd Qlik Sense Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="59e1d-125">**tooadd Enterprise смысле Qlik из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="59e1d-125">**tooadd Qlik Sense Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e1d-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="59e1d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="59e1d-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="59e1d-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="59e1d-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="59e1d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="59e1d-133">Введите в поле поиска hello **Enterprise смысле Qlik**выберите **Qlik смысле Enterprise** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-133">In hello search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Enterprise смысле Qlik в списке результатов hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="59e1d-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e1d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="59e1d-136">В этом разделе описана настройка и проверка единого входа Azure AD в Qlik Sense Enterprise с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59e1d-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="59e1d-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в смысле Enterprise Qlik является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59e1d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Qlik Sense Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="59e1d-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в смысле Enterprise Qlik должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="59e1d-138">In other words, a link relationship between an Azure AD user and hello related user in Qlik Sense Enterprise needs toobe established.</span></span>

<span data-ttu-id="59e1d-139">В Enterprise смысле Qlik, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="59e1d-139">In Qlik Sense Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="59e1d-140">tooconfigure и теста Azure AD единого входа с Qlik смысле Enterprise, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="59e1d-140">tooconfigure and test Azure AD single sign-on with Qlik Sense Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="59e1d-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="59e1d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="59e1d-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="59e1d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59e1d-143">**[Создание тестового пользователя Enterprise смысле Qlik](#create-a-qlik-sense-enterprise-test-user)**  -toohave аналог Саймон Britta Qlik смысле предприятии, которая является представлением связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="59e1d-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - toohave a counterpart of Britta Simon in Qlik Sense Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="59e1d-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="59e1d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59e1d-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="59e1d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="59e1d-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e1d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="59e1d-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении предприятия Qlik смысле.</span><span class="sxs-lookup"><span data-stu-id="59e1d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="59e1d-148">**tooconfigure Azure AD единого входа с Qlik смысле Enterprise, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="59e1d-148">**tooconfigure Azure AD single sign-on with Qlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e1d-149">В hello в hello портала Azure **Enterprise смысле Qlik** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-149">In hello Azure portal, on hello **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="59e1d-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="59e1d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="59e1d-153">На hello **URL-адреса и домена предприятия смысле Qlik** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="59e1d-153">On hello **Qlik Sense Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах в приложении Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="59e1d-155">а.</span><span class="sxs-lookup"><span data-stu-id="59e1d-155">a.</span></span> <span data-ttu-id="59e1d-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="59e1d-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="59e1d-157">Обратите внимание, hello завершающей косой чертой в конце hello данного универсального кода ресурса.</span><span class="sxs-lookup"><span data-stu-id="59e1d-157">Note hello trailing slash at hello end of this URI.</span></span> <span data-ttu-id="59e1d-158">Она обязательная.</span><span class="sxs-lookup"><span data-stu-id="59e1d-158">It is required.</span></span>
    
    <span data-ttu-id="59e1d-159">b.</span><span class="sxs-lookup"><span data-stu-id="59e1d-159">b.</span></span> <span data-ttu-id="59e1d-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="59e1d-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="59e1d-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-161">These values are not real.</span></span> <span data-ttu-id="59e1d-162">Обновление, эти значения с hello фактический URL-адрес входа и идентификатора, которые рассматриваются далее в этот учебник или обратитесь к [Qlik смысле корпоративный клиент поддержки](https://www.qlik.com/us/services/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="59e1d-162">Update these values with hello actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="59e1d-163">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="59e1d-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="59e1d-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="59e1d-165">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="59e1d-167">Подготовьте файл hello XML метаданных федерации можно передать этот сервер tooQlik смысле.</span><span class="sxs-lookup"><span data-stu-id="59e1d-167">Prepare hello Federation Metadata XML file so that you can upload that tooQlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="59e1d-168">Перед отправкой toohello метаданных поставщика удостоверений hello смысле Qlik сервера, необходимо изменить toobe tooremove сведения tooensure правильную работу между Azure AD файл hello и смысле Qlik сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-168">Before uploading hello IdP metadata toohello Qlik Sense server, hello file needs toobe edited tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="59e1d-170">а.</span><span class="sxs-lookup"><span data-stu-id="59e1d-170">a.</span></span> <span data-ttu-id="59e1d-171">Откройте файл FederationMetaData.xml hello, который вы скачали из портала Azure в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="59e1d-171">Open hello FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="59e1d-172">b.</span><span class="sxs-lookup"><span data-stu-id="59e1d-172">b.</span></span> <span data-ttu-id="59e1d-173">Найдите значение hello **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-173">Search for hello value **RoleDescriptor**.</span></span>  <span data-ttu-id="59e1d-174">Вы найдете четыре записи (две пары открывающих и закрывающих тегов для элементов).</span><span class="sxs-lookup"><span data-stu-id="59e1d-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="59e1d-175">c.</span><span class="sxs-lookup"><span data-stu-id="59e1d-175">c.</span></span> <span data-ttu-id="59e1d-176">Удалите теги RoleDescriptor hello и все данные из файла hello между ними.</span><span class="sxs-lookup"><span data-stu-id="59e1d-176">Delete hello RoleDescriptor tags and all information in between from hello file.</span></span>
   
    <span data-ttu-id="59e1d-177">d.</span><span class="sxs-lookup"><span data-stu-id="59e1d-177">d.</span></span> <span data-ttu-id="59e1d-178">Сохраните файл hello и сохранить его ближайших для дальнейшего использования в этом документе.</span><span class="sxs-lookup"><span data-stu-id="59e1d-178">Save hello file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="59e1d-179">Перейдите toohello Qlik управления Qlik смысле консоли (QMC) от пользователя, который можно создать конфигурации виртуального прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-179">Navigate toohello Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="59e1d-180">Hello QMC щелкнуть hello **виртуальные учетные записи-посредники** элемента меню.</span><span class="sxs-lookup"><span data-stu-id="59e1d-180">In hello QMC, click on hello **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="59e1d-182">Hello нижней части экрана приветствия, щелкните hello **создать новый** кнопки.</span><span class="sxs-lookup"><span data-stu-id="59e1d-182">At hello bottom of hello screen, click hello **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="59e1d-184">Появится экран Редактирование Hello виртуальной прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-184">hello Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="59e1d-185">На hello в правой части экрана приветствия — это меню для отображения параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="59e1d-185">On hello right side of hello screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="59e1d-187">Параметр меню идентификации hello этот флажок установлен введите hello идентифицирующие сведения для настройки прокси-сервера Azure виртуальных hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-187">With hello Identification menu option checked, enter hello identifying information for hello Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="59e1d-189">а.</span><span class="sxs-lookup"><span data-stu-id="59e1d-189">a.</span></span> <span data-ttu-id="59e1d-190">Hello **описание** поля — это понятное имя для конфигурации виртуального прокси hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-190">hello **Description** field is a friendly name for hello virtual proxy configuration.</span></span>  <span data-ttu-id="59e1d-191">Введите значение в поле Description (Описание).</span><span class="sxs-lookup"><span data-stu-id="59e1d-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="59e1d-192">b.</span><span class="sxs-lookup"><span data-stu-id="59e1d-192">b.</span></span> <span data-ttu-id="59e1d-193">Hello **префикса** поле определяет конечную hello виртуального прокси для соединения с Azure AD Single Sign-On tooQlik смысле.</span><span class="sxs-lookup"><span data-stu-id="59e1d-193">hello **Prefix** field identifies hello virtual proxy endpoint for connecting tooQlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="59e1d-194">Введите уникальное имя префикса для этого виртуального прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="59e1d-195">c.</span><span class="sxs-lookup"><span data-stu-id="59e1d-195">c.</span></span> <span data-ttu-id="59e1d-196">**Время ожидания сеанса простоя (в минутах)** hello время ожидания для подключения через этот виртуальный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="59e1d-196">**Session inactivity timeout (minutes)** is hello timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="59e1d-197">d.</span><span class="sxs-lookup"><span data-stu-id="59e1d-197">d.</span></span> <span data-ttu-id="59e1d-198">Hello **имя заголовка файла cookie сеанса** является хранение имя файла cookie hello hello идентификатор сеанса для hello смысле Qlik сеанса пользователь получает после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="59e1d-198">hello **Session cookie header name** is hello cookie name storing hello session identifier for hello Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="59e1d-199">Это имя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="59e1d-199">This name must be unique.</span></span>

12. <span data-ttu-id="59e1d-200">Щелкните меню параметр hello проверки подлинности toomake его видимым.</span><span class="sxs-lookup"><span data-stu-id="59e1d-200">Click on hello Authentication menu option toomake it visible.</span></span>  <span data-ttu-id="59e1d-201">Появится экран приветствия проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="59e1d-201">hello Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="59e1d-203">а.</span><span class="sxs-lookup"><span data-stu-id="59e1d-203">a.</span></span> <span data-ttu-id="59e1d-204">Hello **режим анонимного доступа** определяет раскрывающийся список, если анонимные пользователи могут обращаться к Qlik смысле через виртуальный hello прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-204">hello **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through hello virtual proxy.</span></span>  <span data-ttu-id="59e1d-205">анонимный пользователь не параметр по умолчанию Hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-205">hello default option is No anonymous user.</span></span>
    
    <span data-ttu-id="59e1d-206">b.</span><span class="sxs-lookup"><span data-stu-id="59e1d-206">b.</span></span> <span data-ttu-id="59e1d-207">Hello **метод проверки подлинности** раскрывающийся список определяет, будет использоваться виртуальный прокси схемы проверки подлинности hello hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-207">hello **Authentication method** drop-down determines hello authentication scheme hello virtual proxy will use.</span></span>  <span data-ttu-id="59e1d-208">Выберите SAML из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-208">Select SAML from hello drop-down list.</span></span>  <span data-ttu-id="59e1d-209">После этого появятся дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="59e1d-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="59e1d-210">c.</span><span class="sxs-lookup"><span data-stu-id="59e1d-210">c.</span></span> <span data-ttu-id="59e1d-211">В hello **поле URI узла SAML**, входной hello hostname пользователи вводят tooaccess Qlik смысле через этот прокси виртуального SAML.</span><span class="sxs-lookup"><span data-stu-id="59e1d-211">In hello **SAML host URI field**, input hello hostname users enter tooaccess Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="59e1d-212">Имя узла Hello представляет uri hello hello server Qlik смысле.</span><span class="sxs-lookup"><span data-stu-id="59e1d-212">hello hostname is hello uri of hello Qlik Sense server.</span></span>
    
    <span data-ttu-id="59e1d-213">d.</span><span class="sxs-lookup"><span data-stu-id="59e1d-213">d.</span></span> <span data-ttu-id="59e1d-214">В hello **идентификатор сущности SAML**, введите hello того же значения, указанного для узла URI hello SAML поля.</span><span class="sxs-lookup"><span data-stu-id="59e1d-214">In hello **SAML entity ID**, enter hello same value entered for hello SAML host URI field.</span></span>
    
    <span data-ttu-id="59e1d-215">д.</span><span class="sxs-lookup"><span data-stu-id="59e1d-215">e.</span></span> <span data-ttu-id="59e1d-216">Hello **метаданные поставщика удостоверений SAML** — файл hello изменить ранее в hello **редактирование метаданных федерации из конфигурации Azure AD** раздела.</span><span class="sxs-lookup"><span data-stu-id="59e1d-216">hello **SAML IdP metadata** is hello file edited earlier in hello **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="59e1d-217">**Перед отправкой hello метаданные поставщика удостоверений, необходимо изменить toobe файл hello** tooremove сведения tooensure правильную работу между Azure AD и смысле Qlik сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-217">**Before uploading hello IdP metadata, hello file needs toobe edited** tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="59e1d-218">**Если файл hello имеет еще toobe изменить см. выше toohello инструкций.**</span><span class="sxs-lookup"><span data-stu-id="59e1d-218">**Please refer toohello instructions above if hello file has yet toobe edited.**</span></span>  <span data-ttu-id="59e1d-219">Если hello файл был изменен нажмите кнопку обзора hello и выберите hello измененные метаданные файла tooupload его toohello Конфигурация виртуальных прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-219">If hello file has been edited click on hello Browse button and select hello edited metadata file tooupload it toohello virtual proxy configuration.</span></span>
    
    <span data-ttu-id="59e1d-220">f.</span><span class="sxs-lookup"><span data-stu-id="59e1d-220">f.</span></span> <span data-ttu-id="59e1d-221">Введите имя или схема ссылку hello атрибут для hello атрибут SAML, представляющий hello **UserID** Azure AD отправляет toohello смысле Qlik сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-221">Enter hello attribute name or schema reference for hello SAML attribute representing hello **UserID** Azure AD sends toohello Qlik Sense server.</span></span>  <span data-ttu-id="59e1d-222">Схемы справочная информация доступна в конфигурации записи экраны hello приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="59e1d-222">Schema reference information is available in hello Azure app screens post configuration.</span></span>  <span data-ttu-id="59e1d-223">атрибут имени toouse hello, введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="59e1d-223">toouse hello name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="59e1d-224">ж.</span><span class="sxs-lookup"><span data-stu-id="59e1d-224">g.</span></span> <span data-ttu-id="59e1d-225">Введите значение hello hello **каталог пользователя** , которые будут вложенного toousers при проверке подлинности сервера смысле tooQlik через Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59e1d-225">Enter hello value for hello **user directory** that will be attached toousers when they authenticate tooQlik Sense server through Azure AD.</span></span>  <span data-ttu-id="59e1d-226">Жестко заданные значения нужно заключить в **квадратные скобки []**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="59e1d-227">toouse атрибут, отправляемый в hello утверждения Azure AD SAML, введите имя hello hello атрибута в этом текстовом поле **без** квадратные скобки.</span><span class="sxs-lookup"><span data-stu-id="59e1d-227">toouse an attribute sent in hello Azure AD SAML assertion, enter hello name of hello attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="59e1d-228">h.</span><span class="sxs-lookup"><span data-stu-id="59e1d-228">h.</span></span> <span data-ttu-id="59e1d-229">Hello **алгоритм подписи SAML** наборов hello подписи для конфигурации виртуального прокси hello сертификата службы поставщика (в этого обращения Qlik смысле сервера).</span><span class="sxs-lookup"><span data-stu-id="59e1d-229">hello **SAML signing algorithm** sets hello service provider (in this case Qlik Sense server) certificate signing for hello virtual proxy configuration.</span></span>  <span data-ttu-id="59e1d-230">Если сервер смысле Qlik использует доверенный сертификат, созданный с помощью Microsoft Enhanced RSA и AES Cryptographic Provider, измените алгоритм подписи SAML hello слишком**SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change hello SAML signing algorithm too**SHA-256**.</span></span>
    
    <span data-ttu-id="59e1d-231">i.</span><span class="sxs-lookup"><span data-stu-id="59e1d-231">i.</span></span> <span data-ttu-id="59e1d-232">для дополнительных атрибутов, таких как группы toobe отправлено tooQlik смысле для использования в правилах безопасности позволяет Hello разделе сопоставление атрибута SAML.</span><span class="sxs-lookup"><span data-stu-id="59e1d-232">hello SAML attribute mapping section allows for additional attributes like groups toobe sent tooQlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="59e1d-233">Щелкните hello **БАЛАНСИРОВКИ НАГРУЗКИ** toomake параметр меню его видимым.</span><span class="sxs-lookup"><span data-stu-id="59e1d-233">Click on hello **LOAD BALANCING** menu option toomake it visible.</span></span>  <span data-ttu-id="59e1d-234">Появится экран балансировки нагрузки Hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-234">hello Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="59e1d-236">Щелкните hello **добавить новый узел сервера** кнопку engine выберите узел или узлы Qlik смысле отправки в целях балансировки нагрузки toofor сеансы и щелкните hello **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="59e1d-236">Click on hello **Add new server node** button, select engine node or nodes Qlik Sense will send sessions toofor load balancing purposes, and click hello **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="59e1d-238">Щелкните toomake параметр меню "Дополнительно" hello его видимым.</span><span class="sxs-lookup"><span data-stu-id="59e1d-238">Click on hello Advanced menu option toomake it visible.</span></span> <span data-ttu-id="59e1d-239">Появится экран дополнительных Hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-239">hello Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="59e1d-241">список разрешенных Hello узла определяет имена узлов, которые принимаются при подключении toohello смысле Qlik сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-241">hello Host white list identifies hostnames that are accepted when connecting toohello Qlik Sense server.</span></span>  <span data-ttu-id="59e1d-242">**Введите имя узла hello, которую пользователи будут указывать при подключении сервера tooQlik смысле.**</span><span class="sxs-lookup"><span data-stu-id="59e1d-242">**Enter hello hostname users will specify when connecting tooQlik Sense server.**</span></span> <span data-ttu-id="59e1d-243">Имя узла Hello — hello одинаковое значение как hello SAML uri узла без hello https://.</span><span class="sxs-lookup"><span data-stu-id="59e1d-243">hello hostname is hello same value as hello SAML host uri without hello https://.</span></span>

16. <span data-ttu-id="59e1d-244">Нажмите кнопку hello **применить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="59e1d-244">Click hello **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="59e1d-246">Нажмите кнопку ОК tooaccept hello предупредительное сообщение, указывающее прокси-серверы виртуальных toohello связанный прокси-сервер будет перезапущен.</span><span class="sxs-lookup"><span data-stu-id="59e1d-246">Click OK tooaccept hello warning message that states proxies linked toohello virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="59e1d-248">Hello правой части экрана приветствия появится hello связанные элементы меню.</span><span class="sxs-lookup"><span data-stu-id="59e1d-248">On hello right side of hello screen, hello Associated items menu appears.</span></span>  <span data-ttu-id="59e1d-249">Щелкните hello **учетные записи-посредники** пункт меню.</span><span class="sxs-lookup"><span data-stu-id="59e1d-249">Click on hello **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="59e1d-251">Появится экран приветствия прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-251">hello proxy screen appears.</span></span>  <span data-ttu-id="59e1d-252">Нажмите кнопку hello **ссылку** , расположенную в нижней toolink hello виртуального прокси toohello прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-252">Click hello **Link** button at hello bottom toolink a proxy toohello virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="59e1d-254">Узел прокси-сервера выберите hello, который будет поддерживать этот виртуальный прокси-подключения и нажмите кнопку hello **ссылку** кнопки.</span><span class="sxs-lookup"><span data-stu-id="59e1d-254">Select hello proxy node that will support this virtual proxy connection and click hello **Link** button.</span></span>  <span data-ttu-id="59e1d-255">После связывания, hello прокси-сервера будут перечислены под ними прокси-серверы.</span><span class="sxs-lookup"><span data-stu-id="59e1d-255">After linking, hello proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="59e1d-258">После будут отображаться пять секунд tooten, обновите QMC сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-258">After about five tooten seconds, hello Refresh QMC message will appear.</span></span>  <span data-ttu-id="59e1d-259">Нажмите кнопку hello **QMC обновление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="59e1d-259">Click hello **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="59e1d-261">После обновления hello QMC щелкните hello **виртуальные учетные записи-посредники** элемента меню.</span><span class="sxs-lookup"><span data-stu-id="59e1d-261">When hello QMC refreshes, click on hello **Virtual proxies** menu item.</span></span> <span data-ttu-id="59e1d-262">Hello новая запись SAML виртуального прокси-сервера перечислены в таблице hello на экране приветствия.</span><span class="sxs-lookup"><span data-stu-id="59e1d-262">hello new SAML virtual proxy entry is listed in hello table on hello screen.</span></span>  <span data-ttu-id="59e1d-263">Одним щелчком на запись hello виртуального прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="59e1d-263">Single click on hello virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="59e1d-265">Hello нижней части экрана приветствия активируется кнопка метаданные SP загрузить hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-265">At hello bottom of hello screen, hello Download SP metadata button will activate.</span></span>  <span data-ttu-id="59e1d-266">Щелкните hello **метаданные SP загрузить** файл tooa метаданных hello toosave кнопки.</span><span class="sxs-lookup"><span data-stu-id="59e1d-266">Click hello **Download SP metadata** button toosave hello metadata tooa file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="59e1d-268">Файл метаданных Привет открыть пакет.</span><span class="sxs-lookup"><span data-stu-id="59e1d-268">Open hello sp metadata file.</span></span>  <span data-ttu-id="59e1d-269">Наблюдать за hello **entityID** входа и hello **AssertionConsumerService** входа.</span><span class="sxs-lookup"><span data-stu-id="59e1d-269">Observe hello **entityID** entry and hello **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="59e1d-270">Эти значения имеют эквивалентные toohello **идентификатор** и hello **URL-адрес входа** в конфигурации приложения hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59e1d-270">These values are equivalent toohello **Identifier** and hello **Sign on URL** in hello Azure AD application configuration.</span></span> <span data-ttu-id="59e1d-271">Вставьте эти значения в hello **URL-адреса и домена предприятия смысле Qlik** раздела конфигурации приложения hello Azure AD, если они не совпадают, то их следует заменить приветствия мастера настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59e1d-271">Paste these values in hello **Qlik Sense Enterprise Domain and URLs** section in hello Azure AD application configuration if they are not matching, then you should replace them in hello Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="59e1d-273">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="59e1d-273">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="59e1d-274">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-274">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="59e1d-275">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59e1d-275">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="59e1d-276">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e1d-276">Create an Azure AD test user</span></span>
<span data-ttu-id="59e1d-277">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="59e1d-277">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="59e1d-279">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="59e1d-279">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e1d-280">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="59e1d-280">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

   ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="59e1d-282">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-282">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

   ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="59e1d-284">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="59e1d-284">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

   ![Кнопка "Добавить" Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="59e1d-286">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="59e1d-286">In hello **User** dialog box, perform hello following steps:</span></span>

   ![диалоговое окно приветствия пользователя](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="59e1d-288">а.</span><span class="sxs-lookup"><span data-stu-id="59e1d-288">a.</span></span> <span data-ttu-id="59e1d-289">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-289">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="59e1d-290">b.</span><span class="sxs-lookup"><span data-stu-id="59e1d-290">b.</span></span> <span data-ttu-id="59e1d-291">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="59e1d-291">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="59e1d-292">c.</span><span class="sxs-lookup"><span data-stu-id="59e1d-292">c.</span></span> <span data-ttu-id="59e1d-293">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="59e1d-293">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="59e1d-294">d.</span><span class="sxs-lookup"><span data-stu-id="59e1d-294">d.</span></span> <span data-ttu-id="59e1d-295">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="59e1d-296">Создание тестового пользователя Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="59e1d-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="59e1d-297">В этом разделе описано, как создать пользователя Britta Simon в приложении Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="59e1d-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="59e1d-298">Работать с [Qlik смысле корпоративный клиент поддержки](https://www.qlik.com/us/services/support) для добавления пользователей hello в hello Qlik смысле корпоративной платформы.</span><span class="sxs-lookup"><span data-stu-id="59e1d-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add hello users in hello Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="59e1d-299">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="59e1d-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="59e1d-300">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="59e1d-300">Assign hello Azure AD test user</span></span>

<span data-ttu-id="59e1d-301">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooQlik смысле предприятия.</span><span class="sxs-lookup"><span data-stu-id="59e1d-301">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQlik Sense Enterprise.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="59e1d-303">**tooassign tooQlik Britta Simon смысле Enterprise, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="59e1d-303">**tooassign Britta Simon tooQlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e1d-304">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-304">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="59e1d-306">В списке приложений hello выберите **Qlik смысле Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-306">In hello applications list, select **Qlik Sense Enterprise**.</span></span>

    ![ссылка на корпоративный смысле Qlik Hello в списке приложений hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="59e1d-308">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-308">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="59e1d-310">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-310">Click **Add** button.</span></span> <span data-ttu-id="59e1d-311">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="59e1d-313">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-313">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="59e1d-314">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59e1d-315">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="59e1d-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="59e1d-316">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="59e1d-316">Test single sign-on</span></span>

<span data-ttu-id="59e1d-317">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="59e1d-317">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="59e1d-318">Если щелкнуть плитку Enterprise смысле Qlik hello в hello панели доступа, следует получать автоматически вошедшего tooyour Qlik смысле корпоративного приложения.</span><span class="sxs-lookup"><span data-stu-id="59e1d-318">When you click hello Qlik Sense Enterprise tile in hello Access Panel, you should get automatically signed-on tooyour Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="59e1d-319">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="59e1d-319">Additional resources</span></span>

* [<span data-ttu-id="59e1d-320">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59e1d-320">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59e1d-321">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59e1d-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

