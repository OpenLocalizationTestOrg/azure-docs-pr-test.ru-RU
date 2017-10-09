---
title: "Руководство по интеграции Azure Active Directory с SAP Business Object Cloud | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и облаком объекта SAP Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="689b4-103">Руководство по интеграции Azure Active Directory с SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="689b4-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="689b4-104">В этом учебнике вы узнаете, как toointegrate SAP Business объекта облака в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="689b4-104">In this tutorial, you learn how toointegrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="689b4-105">Вы получаете hello при интеграции SAP Business объекта облака в Azure AD следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="689b4-105">You get hello following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="689b4-106">В Azure AD можно управлять, у кого есть доступ tooSAP объекта облачные бизнес.</span><span class="sxs-lookup"><span data-stu-id="689b4-106">In Azure AD, you can control who has access tooSAP Business Object Cloud.</span></span>
- <span data-ttu-id="689b4-107">Вы автоматически вход вашей tooSAP пользователей облака объект бизнес с помощью единого входа и учетная запись пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="689b4-107">You can automatically sign in your users tooSAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="689b4-108">Вы можете управлять учетными записями в один, централизованно, hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="689b4-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="689b4-109">toolearn Дополнительные сведения о программное обеспечение как услуга (SaaS) интеграции приложений с Azure AD, в разделе [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="689b4-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="689b4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="689b4-110">Prerequisites</span></span>

<span data-ttu-id="689b4-111">tooset интеграции с Azure AD с облаком объекта SAP Business необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="689b4-111">tooset up Azure AD integration with SAP Business Object Cloud, you need hello following items:</span></span>

- <span data-ttu-id="689b4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="689b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="689b4-113">подписка SAP Business Object Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="689b4-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="689b4-114">Если вы тестируете hello шаги в этом учебнике, мы рекомендуем не проверяют их в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="689b4-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="689b4-115">Рекомендации для тестирования hello шаги в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="689b4-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="689b4-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="689b4-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="689b4-117">Если у вас нет пробной среды Azure AD, вы можете [получить бесплатную пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="689b4-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="689b4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="689b4-118">Scenario description</span></span>
<span data-ttu-id="689b4-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="689b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="689b4-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="689b4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="689b4-121">Добавление объекта облака SAP Business из коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="689b4-121">Add SAP Business Object Cloud from hello gallery.</span></span>
2. <span data-ttu-id="689b4-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="689b4-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a><span data-ttu-id="689b4-123">Добавление объекта облака SAP Business из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="689b4-123">Add SAP Business Object Cloud from hello gallery</span></span>
<span data-ttu-id="689b4-124">tooset hello интеграции облачных объекта Business SAP в Azure AD в галерее hello, добавить объект облака SAP Business tooyour список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="689b4-124">tooset up hello integration of SAP Business Object Cloud with Azure AD, in hello gallery, add SAP Business Object Cloud tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="689b4-125">tooadd SAP Business объекта облака из галереи hello:</span><span class="sxs-lookup"><span data-stu-id="689b4-125">tooadd SAP Business Object Cloud from hello gallery:</span></span>

1. <span data-ttu-id="689b4-126">В hello [портал Azure](https://portal.azure.com)в левом меню hello, выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="689b4-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="689b4-128">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="689b4-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![страница приложений корпоративного Hello][2]
    
3. <span data-ttu-id="689b4-130">Выберите новое приложение tooadd **новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="689b4-130">tooadd a new application, select **New application**.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="689b4-132">Введите в поле поиска hello, **SAP Business объекта облака**.</span><span class="sxs-lookup"><span data-stu-id="689b4-132">In hello search box, enter **SAP Business Object Cloud**.</span></span>

    ![поле поиска Hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="689b4-134">В панели результатов hello, выберите **SAP Business объекта облака**и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="689b4-134">In hello results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business объекта облака в списке результатов hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="689b4-136">Настройка и проверка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="689b4-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="689b4-137">В этом разделе описана настройка и проверка единого входа Azure AD в SAP Business Object Cloud с использованием тестового пользователя *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="689b4-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="689b4-138">Для единого входа toowork Azure AD требуется пользователь аналог tooknow hello Azure AD в облаке объекта SAP Business.</span><span class="sxs-lookup"><span data-stu-id="689b4-138">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="689b4-139">Ссылочное отношение между пользователем Azure AD и hello связанных пользователей в облаке объекта SAP Business должно быть установлено.</span><span class="sxs-lookup"><span data-stu-id="689b4-139">A link relationship between an Azure AD user and hello related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="689b4-140">tooestablish hello ссылка связи в облаке объекта SAP Business, **Username**, присвойте значение hello hello **имя пользователя** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="689b4-140">tooestablish hello link relationship, in SAP Business Object Cloud, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="689b4-141">tooconfigure и теста Azure AD единого входа с бизнес объектом SAP облака, полный hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="689b4-141">tooconfigure and test Azure AD single sign-on with SAP Business Object Cloud, complete hello following tasks:</span></span>

1. <span data-ttu-id="689b4-142">[Настройка единого входа Azure AD](#set-up-azure-ad-single-sign-on)</span><span class="sxs-lookup"><span data-stu-id="689b4-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="689b4-143">Настраивает эту функцию toouse пользователя.</span><span class="sxs-lookup"><span data-stu-id="689b4-143">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="689b4-144">[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)</span><span class="sxs-lookup"><span data-stu-id="689b4-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="689b4-145">Тесты Azure AD единого входа с пользователем hello Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="689b4-145">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="689b4-146">[Создание тестового пользователя SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user)</span><span class="sxs-lookup"><span data-stu-id="689b4-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="689b4-147">Создает аналог Саймон Britta в SAP Business объекта облака, связанного toohello представление hello пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="689b4-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="689b4-148">[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="689b4-148">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="689b4-149">Устанавливает toouse Britta Simon Azure AD единого входа.</span><span class="sxs-lookup"><span data-stu-id="689b4-149">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="689b4-150">[Проверка единого входа](#test-single-sign-on)</span><span class="sxs-lookup"><span data-stu-id="689b4-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="689b4-151">Подтверждает, что эта конфигурация hello работает.</span><span class="sxs-lookup"><span data-stu-id="689b4-151">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="689b4-152">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="689b4-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="689b4-153">В этом разделе включении Azure AD одним входом в портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="689b4-153">In this section, you turn on Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="689b4-154">и настроить его в приложении SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="689b4-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="689b4-155">tooset копирование Azure AD единого входа с облаком объекта SAP Business:</span><span class="sxs-lookup"><span data-stu-id="689b4-155">tooset up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="689b4-156">В hello в hello портала Azure **SAP Business объекта облака** странице интеграции приложений выберите **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="689b4-156">In hello Azure portal, on hello **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Выбор параметра "Единый вход"][4]

2. <span data-ttu-id="689b4-158">На hello **единого входа** страницы, для **режим**выберите **входа на базе SAML**.</span><span class="sxs-lookup"><span data-stu-id="689b4-158">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Выбор параметра "Вход на основе SAML"](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="689b4-160">В разделе **SAP бизнес-объекта облачной среде и URL-адреса**полный hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="689b4-160">Under **SAP Business Object Cloud Domain and URLs**, complete hello following steps:</span></span>

    1. <span data-ttu-id="689b4-161">В hello **URL-адрес входа** введите URL-адрес, имеющий hello следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="689b4-161">In hello **Sign-on URL** box, enter a URL that has hello following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="689b4-162">В hello **идентификатор** введите URL-адрес, имеющий hello следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="689b4-162">In hello **Identifier** box, enter a URL that has hello following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![Домены и URL-адреса приложения SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="689b4-164">значения Hello в эти URL-адреса являются исключительно для демонстрационных целей.</span><span class="sxs-lookup"><span data-stu-id="689b4-164">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="689b4-165">Обновление hello значениями hello фактическое входа URL-адрес и идентификатор URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="689b4-165">Update hello values with hello actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="689b4-166">tooget hello URL-адрес входа, обратитесь в службу hello [группа поддержки SAP Business объекта облака клиента](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="689b4-166">tooget hello sign-on URL, contact hello [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="689b4-167">URL-адрес идентификатора hello можно получить, загрузив hello SAP Business объекта облачных метаданных из консоли администрирования hello.</span><span class="sxs-lookup"><span data-stu-id="689b4-167">You can get hello identifier URL by downloading hello SAP Business Object Cloud metadata from hello admin console.</span></span> <span data-ttu-id="689b4-168">Это объясняется далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="689b4-168">This is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="689b4-169">В разделе **Сертификат подписи SAML** выберите **XML метаданных**.</span><span class="sxs-lookup"><span data-stu-id="689b4-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="689b4-170">Сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="689b4-170">Then, save hello metadata file on your computer.</span></span>

    ![Выбор XML метаданных](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="689b4-172">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="689b4-172">Select **Save**.</span></span>

    ![Нажатие кнопки "Сохранить"](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="689b4-174">В другом окне браузера Войдите на сайте компании SAP Business объекта облака tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="689b4-174">In a different web browser window, sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="689b4-175">Выберите **Меню** > **Система** > **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="689b4-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Выбор параметров "Меню", "Система" и "Администрирование"](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="689b4-177">На hello **безопасности** вкладке, выберите hello **изменить** значок (перо).</span><span class="sxs-lookup"><span data-stu-id="689b4-177">On hello **Security** tab, select hello **Edit** (pen) icon.</span></span>
    
    ![На вкладке Безопасность hello выберите значок редактирования hello](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="689b4-179">В качестве **метода проверки подлинности** выберите **SAML Single Sign-On (SSO)** (Единый вход SAML (SSO)).</span><span class="sxs-lookup"><span data-stu-id="689b4-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Выберите SAML Single Sign-On для метода проверки подлинности hello](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="689b4-181">toodownload hello поставщика метаданных службы (шаг 1) выберите **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="689b4-181">toodownload hello service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="689b4-182">В файле метаданных hello, найдите и скопируйте hello **entityID** значение.</span><span class="sxs-lookup"><span data-stu-id="689b4-182">In hello metadata file, find and copy hello **entityID** value.</span></span> <span data-ttu-id="689b4-183">В hello Azure портала в разделе **SAP бизнес-объекта облачной среде и URL-адреса**, вставьте значение hello в hello **идентификатор** поле.</span><span class="sxs-lookup"><span data-stu-id="689b4-183">In hello Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste hello value in hello **Identifier** box.</span></span>

    ![Скопируйте и вставьте значение entityID hello](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="689b4-185">tooupload hello поставщика метаданных службы (шаг 2) в файле hello, загруженного из hello портал Azure в разделе **метаданных поставщика удостоверений отправить**выберите **отправить**.</span><span class="sxs-lookup"><span data-stu-id="689b4-185">tooupload hello service provider metadata (Step 2) in hello file that you downloaded from hello Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![Нажатие кнопки "Отправить" в разделе Upload Identity Provider metadata (Отправить метаданные поставщика удостоверений)](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="689b4-187">В hello **атрибут пользователя** список атрибутов пользователя выберите hello (шаг 3), требуется toouse вашей реализации.</span><span class="sxs-lookup"><span data-stu-id="689b4-187">In hello **User Attribute** list, select hello user attribute (Step 3) that you want toouse for your implementation.</span></span> <span data-ttu-id="689b4-188">Этот атрибут пользователя сопоставляет toohello поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="689b4-188">This user attribute maps toohello identity provider.</span></span> <span data-ttu-id="689b4-189">пользовательский атрибут на странице приветствия пользователя, используйте hello tooenter **пользовательские сопоставления SAML** параметр.</span><span class="sxs-lookup"><span data-stu-id="689b4-189">tooenter a custom attribute on hello user's page, use hello **Custom SAML Mapping** option.</span></span> <span data-ttu-id="689b4-190">Или можно выбрать либо **электронной почты** или **идентификатор пользователя** как атрибут пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="689b4-190">Or, you can select either **Email** or **USER ID** as hello user attribute.</span></span> <span data-ttu-id="689b4-191">В нашем примере мы выбрали **электронной почты** так, как мы сопоставим hello утверждение идентификатора пользователя с hello **userprincipalname** атрибута в hello **атрибуты пользователя** раздела hello Портал Azure.</span><span class="sxs-lookup"><span data-stu-id="689b4-191">In our example, we selected **Email** because we mapped hello user identifier claim with hello **userprincipalname** attribute in hello **User Attributes** section in hello Azure portal.</span></span> <span data-ttu-id="689b4-192">Это обеспечивает уникальный адрес электронной почты пользователя, который отправляется toohello SAP Business объекта облачного приложения в каждом успешный ответ SAML.</span><span class="sxs-lookup"><span data-stu-id="689b4-192">This provides a unique user email, which is sent toohello SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Выбор атрибута пользователя](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="689b4-194">Учетная запись hello tooverify с поставщиком удостоверений hello (шаг 4) в hello **учетные данные входа (электронной почты)** введите адрес электронной почты пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="689b4-194">tooverify hello account with hello identity provider (Step 4), in hello **Login Credential (Email)** box, enter hello user's email address.</span></span> <span data-ttu-id="689b4-195">Выберите **Проверить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="689b4-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="689b4-196">система Hello Добавление учетной записи пользователя toohello учетных данных для входа.</span><span class="sxs-lookup"><span data-stu-id="689b4-196">hello system adds sign-in credentials toohello user account.</span></span>

    ![Ввод электронного адреса и нажатие кнопки "Проверить учетную запись"](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="689b4-198">Выберите hello **Сохранить** значок.</span><span class="sxs-lookup"><span data-stu-id="689b4-198">Select hello **Save** icon.</span></span>

    ![Значок "Сохранить"](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="689b4-200">Можно прочитать краткое версии этих инструкций в hello [портал Azure](https://portal.azure.com), тогда как при настройке приложения!</span><span class="sxs-lookup"><span data-stu-id="689b4-200">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="689b4-201">После добавления приложения hello, выбрав **Active Directory** > **корпоративных приложений**выберите hello **Single Sign-On** вкладки. Можно получить доступ к документации hello внедрены в hello **конфигурации** раздел hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="689b4-201">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="689b4-202">Чтобы узнать больше, ознакомьтесь со [встроенной документацией по Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="689b4-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="689b4-203">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="689b4-203">Create an Azure AD test user</span></span>
<span data-ttu-id="689b4-204">В этом разделе создайте тестового пользователя с именем Britta Simon в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="689b4-204">In this section, you create a test user named Britta Simon in hello Azure portal.</span></span>

<span data-ttu-id="689b4-205">toocreate тестового пользователя в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="689b4-205">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="689b4-206">В hello в левом меню hello, портале Azure выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="689b4-206">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="689b4-208">toodisplay hello список пользователей, выберите **пользователей и групп**, а затем выберите **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="689b4-208">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="689b4-210">tooopen hello **пользователя** выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="689b4-210">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="689b4-212">В hello **пользователя** диалоговое окно, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="689b4-212">In hello **User** dialog box, complete hello following steps:</span></span>
 
    1. <span data-ttu-id="689b4-213">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="689b4-213">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="689b4-214">В hello **имя пользователя** введите адрес электронной почты hello hello пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="689b4-214">In hello **User name** box, enter hello email address of hello user Britta Simon.</span></span>

    3. <span data-ttu-id="689b4-215">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="689b4-215">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="689b4-216">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="689b4-216">Select **Create**.</span></span>

        ![диалоговое окно приветствия пользователя](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Создание пользователя Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="689b4-219">Создание тестового пользователя SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="689b4-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="689b4-220">Необходимо подготовить пользователей Azure AD в облаке объекта SAP Business, прежде чем они смогут войти в tooSAP объекта облачные бизнес.</span><span class="sxs-lookup"><span data-stu-id="689b4-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in tooSAP Business Object Cloud.</span></span> <span data-ttu-id="689b4-221">В SAP Business Object Cloud подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="689b4-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="689b4-222">tooprovision учетной записи пользователя:</span><span class="sxs-lookup"><span data-stu-id="689b4-222">tooprovision a user account:</span></span>

1. <span data-ttu-id="689b4-223">Войдите в tooyour SAP Business объекта облаке на сайте компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="689b4-223">Sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="689b4-224">Выберите **Меню** > **Безопасность** > **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="689b4-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="689b4-226">На hello **пользователей** , tooadd новые сведения о пользователе, выберите  **+** .</span><span class="sxs-lookup"><span data-stu-id="689b4-226">On hello **Users** page, tooadd new user details, select **+**.</span></span> 

    ![Страница добавления пользователей](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="689b4-228">Затем выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="689b4-228">Then, complete hello following steps:</span></span>

    1. <span data-ttu-id="689b4-229">В hello **идентификатор пользователя** введите идентификатор hello hello пользователя, таких как **Britta**.</span><span class="sxs-lookup"><span data-stu-id="689b4-229">In hello **USER ID** box, enter hello user ID of hello user, like **Britta**.</span></span>

    2. <span data-ttu-id="689b4-230">В hello **имя** введите имя первого hello hello пользователя, таких как **Britta**.</span><span class="sxs-lookup"><span data-stu-id="689b4-230">In hello **FIRST NAME** box, enter hello first name of hello user, like **Britta**.</span></span>

    3. <span data-ttu-id="689b4-231">В hello **ФАМИЛИЯ** введите hello фамилию пользователя hello, таких как **Simon**.</span><span class="sxs-lookup"><span data-stu-id="689b4-231">In hello **LAST NAME** box, enter hello last name of hello user, like **Simon**.</span></span>

    4. <span data-ttu-id="689b4-232">В hello **ОТОБРАЖАЕМОЕ имя** введите полное имя пользователя hello hello как **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="689b4-232">In hello **DISPLAY NAME** box, enter hello full name of hello user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="689b4-233">В hello **электронной почты** введите адрес электронной почты hello hello пользователя, как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="689b4-233">In hello **E-MAIL** box, enter hello email address of hello user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="689b4-234">На hello **Выбор ролей** выберите hello соответствующую роль для пользователя hello и затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="689b4-234">On hello **Select Roles** page, select hello appropriate role for hello user, and then select **OK**.</span></span>

      ![Выбрать роль](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="689b4-236">Выберите hello **Сохранить** значок.</span><span class="sxs-lookup"><span data-stu-id="689b4-236">Select hello **Save** icon.</span></span>  


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="689b4-237">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="689b4-237">Assign hello Azure AD test user</span></span>

<span data-ttu-id="689b4-238">В этом разделе позволяют hello пользователя Britta Simon toouse Azure AD единого входа путем предоставления hello пользователя учетной записи доступа tooSAP объекта облачные бизнес.</span><span class="sxs-lookup"><span data-stu-id="689b4-238">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooSAP Business Object Cloud.</span></span>

<span data-ttu-id="689b4-239">tooassign tooSAP Britta Simon объекта облачные бизнес:</span><span class="sxs-lookup"><span data-stu-id="689b4-239">tooassign Britta Simon tooSAP Business Object Cloud:</span></span>

1. <span data-ttu-id="689b4-240">В hello портал Azure откройте представление приложения hello, а затем перейдите toohello представления каталога.</span><span class="sxs-lookup"><span data-stu-id="689b4-240">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="689b4-241">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="689b4-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="689b4-243">В списке приложений hello выберите **SAP Business объекта облака**.</span><span class="sxs-lookup"><span data-stu-id="689b4-243">In hello applications list, select **SAP Business Object Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="689b4-245">Выберите в меню слева hello, **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="689b4-245">In hello left menu, select **Users and groups**.</span></span>

    ![Выбор параметра "Пользователи и группы"][202] 

4. <span data-ttu-id="689b4-247">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="689b4-247">Select **Add**.</span></span> <span data-ttu-id="689b4-248">Затем на hello **добавить назначение** выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="689b4-248">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![Страница добавления назначения Hello][203]

5. <span data-ttu-id="689b4-250">На hello **пользователей и групп** страницы в список пользователей, выберите hello **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="689b4-250">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="689b4-251">На hello **пользователей и групп** выберите **выберите**.</span><span class="sxs-lookup"><span data-stu-id="689b4-251">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="689b4-252">На hello **добавить назначение** выберите **назначить**.</span><span class="sxs-lookup"><span data-stu-id="689b4-252">On hello **Add Assignment** page, select **Assign**.</span></span>

![Назначение пользователям ролей hello][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="689b4-254">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="689b4-254">Test single sign-on</span></span>

<span data-ttu-id="689b4-255">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="689b4-255">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="689b4-256">При выборе hello объекта облака SAP Business плитки в панели доступа hello вы должны автоматически входить в tooyour SAP Business объекта облачного приложения.</span><span class="sxs-lookup"><span data-stu-id="689b4-256">When you select hello SAP Business Object Cloud tile in hello access panel, you should be automatically signed in tooyour SAP Business Object Cloud application.</span></span>

<span data-ttu-id="689b4-257">Дополнительные сведения о панели доступа hello см. в разделе [панели доступа введение toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="689b4-257">For more information about hello access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="689b4-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="689b4-258">Additional resources</span></span>

* [<span data-ttu-id="689b4-259">Список учебников по toointegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="689b4-259">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="689b4-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="689b4-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

