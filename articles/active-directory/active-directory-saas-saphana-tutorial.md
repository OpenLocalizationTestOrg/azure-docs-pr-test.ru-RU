---
title: "Руководство по интеграции Azure Active Directory с SAP HANA | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="010ec-103">Руководство по интеграции Azure Active Directory с SAP HANA</span><span class="sxs-lookup"><span data-stu-id="010ec-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="010ec-104">В этом учебнике вы узнаете, как toointegrate SAP HANA с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="010ec-104">In this tutorial, you learn how toointegrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="010ec-105">Интеграция SAP HANA с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="010ec-105">Integrating SAP HANA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="010ec-106">Можно управлять в Azure AD, имеющего доступ tooSAP HANA</span><span class="sxs-lookup"><span data-stu-id="010ec-106">You can control in Azure AD who has access tooSAP HANA</span></span>
- <span data-ttu-id="010ec-107">Можно включить на пользователей tooautomatically get вошедшего tooSAP HANA (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="010ec-107">You can enable your users tooautomatically get signed-on tooSAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="010ec-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="010ec-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="010ec-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="010ec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="010ec-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="010ec-110">Prerequisites</span></span>

<span data-ttu-id="010ec-111">tooconfigure интеграция Azure AD с SAP HANA, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="010ec-111">tooconfigure Azure AD integration with SAP HANA, you need hello following items:</span></span>

- <span data-ttu-id="010ec-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="010ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="010ec-113">подписка SAP HANA с поддержкой единого входа;</span><span class="sxs-lookup"><span data-stu-id="010ec-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="010ec-114">экземпляр HANA, выполняемый на любой общедоступной IaaS, локально, на виртуальной машине Azure или в решении "Крупные экземпляры SAP в Azure";</span><span class="sxs-lookup"><span data-stu-id="010ec-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="010ec-115">Hello XSA администрирования веб-интерфейса, а также HANA Studio установлена на экземпляре HANA hello.</span><span class="sxs-lookup"><span data-stu-id="010ec-115">hello XSA Administration Web Interface as well as HANA Studio installed on hello HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="010ec-116">в этом учебнике шаги tootest hello, не рекомендуется использовать рабочей среде SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="010ec-116">tootest hello steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="010ec-117">Сначала протестируйте интеграцию hello в разработки или промежуточной среде приложения hello, а затем используйте hello рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="010ec-117">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="010ec-118">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="010ec-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="010ec-119">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="010ec-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="010ec-120">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="010ec-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="010ec-121">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="010ec-121">Scenario description</span></span>
<span data-ttu-id="010ec-122">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="010ec-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="010ec-123">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="010ec-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="010ec-124">Добавление SAP HANA из галереи hello</span><span class="sxs-lookup"><span data-stu-id="010ec-124">Adding SAP HANA from hello gallery</span></span>
2. <span data-ttu-id="010ec-125">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="010ec-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-hello-gallery"></a><span data-ttu-id="010ec-126">Добавление SAP HANA из галереи hello</span><span class="sxs-lookup"><span data-stu-id="010ec-126">Adding SAP HANA from hello gallery</span></span>
<span data-ttu-id="010ec-127">tooconfigure hello интеграции SAP HANA в Azure AD, вы должны tooadd SAP HANA из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="010ec-127">tooconfigure hello integration of SAP HANA into Azure AD, you need tooadd SAP HANA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="010ec-128">**tooadd SAP HANA из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="010ec-128">**tooadd SAP HANA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="010ec-129">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="010ec-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="010ec-131">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="010ec-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="010ec-132">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="010ec-132">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="010ec-134">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="010ec-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="010ec-136">Введите в поле поиска hello **SAP HANA**выберите **SAP HANA** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="010ec-136">In hello search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button tooadd hello application.</span></span> 

    ![Новое приложение Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="010ec-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="010ec-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="010ec-139">В этом разделе описана настройка и проверка единого входа Azure AD в приложение SAP HANA с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="010ec-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="010ec-140">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SAP HANA является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="010ec-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA is tooa user in Azure AD.</span></span> <span data-ttu-id="010ec-141">Другими словами связи между пользователя Azure AD и связанных пользователей hello в SAP HANA должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="010ec-141">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA needs toobe established.</span></span>

<span data-ttu-id="010ec-142">В SAP HANA, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="010ec-142">In SAP HANA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="010ec-143">tooconfigure и теста Azure AD единого входа с SAP HANA, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="010ec-143">tooconfigure and test Azure AD single sign-on with SAP HANA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="010ec-144">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="010ec-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="010ec-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="010ec-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="010ec-146">**[Создание тестового пользователя SAP HANA](#creating-a-sap-hana-test-user)**  -toohave аналог Саймон Britta в SAP HANA, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="010ec-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - toohave a counterpart of Britta Simon in SAP HANA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="010ec-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="010ec-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="010ec-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="010ec-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="010ec-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="010ec-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="010ec-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="010ec-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="010ec-151">**tooconfigure Azure AD единого входа с SAP HANA, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="010ec-151">**tooconfigure Azure AD single sign-on with SAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="010ec-152">В hello в hello портала Azure **SAP HANA** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="010ec-152">In hello Azure portal, on hello **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="010ec-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="010ec-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="010ec-156">На hello **URL-адреса и SAP HANA домена** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="010ec-156">On hello **SAP HANA Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="010ec-158">а.</span><span class="sxs-lookup"><span data-stu-id="010ec-158">a.</span></span> <span data-ttu-id="010ec-159">В hello **идентификатор** текстовое поле, тип, что:`HA100`</span><span class="sxs-lookup"><span data-stu-id="010ec-159">In hello **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="010ec-160">b.</span><span class="sxs-lookup"><span data-stu-id="010ec-160">b.</span></span> <span data-ttu-id="010ec-161">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="010ec-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="010ec-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="010ec-162">These values are not real.</span></span> <span data-ttu-id="010ec-163">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="010ec-163">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="010ec-164">Обратитесь к [группа поддержки клиента SAP HANA](https://cloudplatform.sap.com/contact.html) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="010ec-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="010ec-165">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="010ec-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="010ec-167">Если сертификат не используется затем сделайте его активным, щелкнув hello флажок «Сделать новый сертификат active» в hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="010ec-167">If certificate is not active then make it active by clicking hello “Make new certificate active” checkbox in hello Azure AD.</span></span> 

5. <span data-ttu-id="010ec-168">SAP HANA приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="010ec-168">SAP HANA application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="010ec-169">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="010ec-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="010ec-170">Здесь мы сопоставленной hello **идентификатор пользователя** с **ExtractMailPrefix()** функция **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="010ec-170">Here we have mapped hello **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="010ec-171">Это дает значение hello префикс адреса электронной почты пользователя hello, что является hello уникальный ИД пользователя.</span><span class="sxs-lookup"><span data-stu-id="010ec-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="010ec-172">Это число отправляется toohello приложения SAP HANA в каждом успешного ответа.</span><span class="sxs-lookup"><span data-stu-id="010ec-172">This is sent toohello SAP HANA application in every successful response.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="010ec-174">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна:</span><span class="sxs-lookup"><span data-stu-id="010ec-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="010ec-175">а.</span><span class="sxs-lookup"><span data-stu-id="010ec-175">a.</span></span> <span data-ttu-id="010ec-176">В hello **идентификатор пользователя** раскрывающегося списка выберите **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="010ec-176">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="010ec-177">b.</span><span class="sxs-lookup"><span data-stu-id="010ec-177">b.</span></span> <span data-ttu-id="010ec-178">В hello **Mail** раскрывающегося списка выберите **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="010ec-178">In hello **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="010ec-179">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="010ec-179">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="010ec-181">tooconfigure единого входа на **SAP HANA** стороны, tooyour входа **HANA XSA веб-консоли** путем просмотра toohello соответствующей конечной точки HTTPS.</span><span class="sxs-lookup"><span data-stu-id="010ec-181">tooconfigure single sign-on on **SAP HANA** side, login tooyour **HANA XSA Web Console**  by browsing toohello respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="010ec-182">В конфигурации по умолчанию hello URL-адрес hello перенаправляет hello запроса tooa входа в систему, что требует учетные данные hello прошедшего проверку подлинности SAP HANA базы данных toocomplete hello процесса входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="010ec-182">In hello default configuration, hello URL redirects hello request tooa logon screen, which requires hello credentials of an authenticated SAP HANA database user toocomplete hello logon process.</span></span> <span data-ttu-id="010ec-183">Hello пользователь, вошедший должен иметь задач администрирования SAML tooperform необходимые привилегии hello.</span><span class="sxs-lookup"><span data-stu-id="010ec-183">hello user who logs on must have hello privileges required tooperform SAML administration tasks.</span></span>

9. <span data-ttu-id="010ec-184">Hello XSA веб-интерфейса, перейдите слишком**поставщика удостоверений SAML** и после этого нажмите кнопку hello **«+»** -кнопку внизу hello hello экрана toodisplay hello добавить сведения о поставщике удостоверений области и выполнение Здравствуйте, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="010ec-184">In hello XSA Web Interface, navigate too**SAML Identity Provider** and from there, click hello **“+”** -button on hello bottom of hello screen toodisplay hello Add Identity Provider Info pane and perform hello following steps:</span></span>

    ![Добавление поставщика удостоверений](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="010ec-186">а.</span><span class="sxs-lookup"><span data-stu-id="010ec-186">a.</span></span> <span data-ttu-id="010ec-187">В hello **добавить сведения о поставщике удостоверений** область, содержимое hello вставить hello метаданных XML-код, загруженный с портала Azure в hello **метаданные** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="010ec-187">In hello **Add Identity Provider Info** pane, paste hello contents of hello Metadata XML, which you have downloaded from Azure portal into hello **Metadata** textbox.</span></span>

    ![Добавление параметров поставщика удостоверений](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="010ec-189">b.</span><span class="sxs-lookup"><span data-stu-id="010ec-189">b.</span></span> <span data-ttu-id="010ec-190">Если содержимое hello hello XML-документа являются допустимыми, hello синтаксического анализа процесса извлекает сведения, необходимые tooinsert hello в hello **тему, идентификатор сущности и издателя** поля в общие данные hello область экрана и hello URL-адрес поля в hello Области экрана назначения, например,  **базовый URL-адрес и URL-адрес единого входа (*)**.</span><span class="sxs-lookup"><span data-stu-id="010ec-190">If hello contents of hello XML document are valid, hello parsing process extracts hello information required tooinsert into hello **Subject, Entity ID, and Issuer** fields in hello General Data screen area, and hello URL fields in hello Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Добавление параметров поставщика удостоверений](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="010ec-192">c.</span><span class="sxs-lookup"><span data-stu-id="010ec-192">c.</span></span> <span data-ttu-id="010ec-193">В поле имя hello hello общие данные область экрана, введите имя для нового поставщика удостоверений единого входа SAML hello.</span><span class="sxs-lookup"><span data-stu-id="010ec-193">In hello Name box of hello General Data screen area, enter a name for hello new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="010ec-194">Имя Hello hello Удостоверений SAML является обязательным и должно быть уникальным; оно появляется в список доступных IDPs SAML, который отображается, hello выборе SAML как hello метод проверки подлинности для toouse приложений SAP HANA XS, например, в области экрана приветствия проверки подлинности средства администрирования артефакта XS hello.</span><span class="sxs-lookup"><span data-stu-id="010ec-194">hello name of hello SAML IDP is mandatory and must be unique; it appears in hello list of available SAML IDPs that is displayed, if you select SAML as hello authentication method for SAP HANA XS applications toouse, for example, in hello Authentication screen area of hello XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="010ec-195">Сохраните сведения о hello hello нового поставщика удостоверений SAML.</span><span class="sxs-lookup"><span data-stu-id="010ec-195">Save hello details of hello new SAML identity provider.</span></span> <span data-ttu-id="010ec-196">Выберите **Сохранить** toosave hello сведений поставщика удостоверений SAML hello и добавьте hello нового поставщика Удостоверений SAML toohello список известных IDPs SAML.</span><span class="sxs-lookup"><span data-stu-id="010ec-196">Choose **Save** toosave hello details of hello SAML identity provider and add hello new SAML IDP toohello list of known SAML IDPs.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="010ec-198">В в системных свойств hello hello Studio HANA **конфигурации** вкладки, просто фильтрации настроек по **saml** и настроить hello **assertion_timeout** из **10 сек** слишком**120 сек**.</span><span class="sxs-lookup"><span data-stu-id="010ec-198">In HANA Studio within hello system properties of hello **Configuration** tab, just filter settings by **saml** and adjust hello **assertion_timeout** from **10 sec** too**120 sec**.</span></span>

    ![Параметр assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="010ec-200">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="010ec-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="010ec-201">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="010ec-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="010ec-202">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="010ec-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="010ec-203">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="010ec-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="010ec-204">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="010ec-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="010ec-206">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="010ec-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="010ec-207">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="010ec-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="010ec-209">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="010ec-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="010ec-211">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="010ec-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="010ec-213">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="010ec-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="010ec-215">а.</span><span class="sxs-lookup"><span data-stu-id="010ec-215">a.</span></span> <span data-ttu-id="010ec-216">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="010ec-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="010ec-217">b.</span><span class="sxs-lookup"><span data-stu-id="010ec-217">b.</span></span> <span data-ttu-id="010ec-218">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="010ec-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="010ec-219">c.</span><span class="sxs-lookup"><span data-stu-id="010ec-219">c.</span></span> <span data-ttu-id="010ec-220">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="010ec-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="010ec-221">d.</span><span class="sxs-lookup"><span data-stu-id="010ec-221">d.</span></span> <span data-ttu-id="010ec-222">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="010ec-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="010ec-223">Создание тестового пользователя SAP HANA</span><span class="sxs-lookup"><span data-stu-id="010ec-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="010ec-224">Пользователи toolog tooenable Azure AD в tooSAP HANA, их необходимо подготовить в SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="010ec-224">tooenable Azure AD users toolog in tooSAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="010ec-225">SAP HANA поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="010ec-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="010ec-226">При необходимости toocreate пользователя вручную, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="010ec-226">If you need toocreate a user manually, perform hello following steps:</span></span>

>[!Note]
><span data-ttu-id="010ec-227">Вы можете изменить hello внешней проверки подлинности, используемый пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="010ec-227">You can change hello external authentication used by hello user.</span></span>
<span data-ttu-id="010ec-228">Внешние пользователи проходят проверку подлинности с помощью внешней системы, например системы Kerberos.</span><span class="sxs-lookup"><span data-stu-id="010ec-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="010ec-229">Чтобы получить дополнительные сведения о внешних удостоверениях, свяжитесь со своим [администратором домена](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="010ec-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="010ec-230">Откройте hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) как администратор и включить hello DB пользователя для единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="010ec-230">Open hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable hello DB-User for SAML SSO.</span></span>

    ![создать пользователя](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="010ec-232">Деления hello невидимой флажок toohello слева от **SAML** и настройка hello по ссылке.</span><span class="sxs-lookup"><span data-stu-id="010ec-232">Tick hello invisible checkbox toohello left of **SAML** and follow hello Configure link.</span></span>

3. <span data-ttu-id="010ec-233">Нажмите кнопку **добавить** tooadd hello Удостоверений SAML и нажмите кнопку **ОК** при выборе соответствующего поставщика Удостоверений SAML "hello".</span><span class="sxs-lookup"><span data-stu-id="010ec-233">Click **Add** tooadd hello SAML IDP and click **OK** selecting hello appropriate SAML IDP.</span></span>

4. <span data-ttu-id="010ec-234">Добавить hello **внешнего идентификатора** (например)</span><span class="sxs-lookup"><span data-stu-id="010ec-234">Add hello **External Identity** (ex.</span></span> <span data-ttu-id="010ec-235">Britta Simon) или выберите **Any** (Любой) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="010ec-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="010ec-236">Если не установлен флажок «ANY», то имя пользователя hello в HANA должно tooexactly соответствия hello имя пользователя hello в hello UPN перед суффикс домена hello (т. е. BrittaSimon@contoso.com стал бы BrittaSimon в HANA).</span><span class="sxs-lookup"><span data-stu-id="010ec-236">If "ANY" check-box is not checked, then hello user name in HANA needs tooexactly match hello name of hello user in hello UPN before hello domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="010ec-237">Для целей тестирования, назначьте все **«XS»** toohello пользователя роли.</span><span class="sxs-lookup"><span data-stu-id="010ec-237">For testing purposes, assign all **"XS"** roles toohello user.</span></span>

    ![Назначение ролей](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="010ec-239">Следует предоставить разрешения, которые подходят только для вашего варианта использования.</span><span class="sxs-lookup"><span data-stu-id="010ec-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="010ec-240">Сохраните hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="010ec-240">Save hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="010ec-241">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="010ec-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="010ec-242">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSAP HANA.</span><span class="sxs-lookup"><span data-stu-id="010ec-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP HANA.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="010ec-244">**tooassign Britta Simon tooSAP HANA, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="010ec-244">**tooassign Britta Simon tooSAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="010ec-245">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="010ec-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="010ec-247">В списке приложений hello выберите **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="010ec-247">In hello applications list, select **SAP HANA**.</span></span>

    ![Назначение пользователя](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="010ec-249">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="010ec-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202] 

4. <span data-ttu-id="010ec-251">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="010ec-251">Click **Add** button.</span></span> <span data-ttu-id="010ec-252">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="010ec-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="010ec-254">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="010ec-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="010ec-255">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="010ec-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="010ec-256">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="010ec-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="010ec-257">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="010ec-257">Testing single sign-on</span></span>

<span data-ttu-id="010ec-258">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="010ec-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="010ec-259">При нажатии кнопки hello SAP HANA плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour приложения SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="010ec-259">When you click hello SAP HANA tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA application.</span></span>
<span data-ttu-id="010ec-260">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="010ec-260">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="010ec-261">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="010ec-261">Additional resources</span></span>

* [<span data-ttu-id="010ec-262">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="010ec-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="010ec-263">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="010ec-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

