---
title: "Учебник. Интеграция Azure Active Directory с HR2day by Merces | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и HR2day по Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="980ca-103">Руководство. Интеграция Azure Active Directory с HR2day от Merces</span><span class="sxs-lookup"><span data-stu-id="980ca-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="980ca-104">В этом учебнике вы узнаете, как toointegrate HR2day по Merces с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="980ca-104">In this tutorial, you learn how toointegrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="980ca-105">Интеграция с Azure AD HR2day по Merces предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="980ca-105">Integrating HR2day by Merces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="980ca-106">Можно управлять в Azure AD, имеющего доступ tooHR2day по Merces.</span><span class="sxs-lookup"><span data-stu-id="980ca-106">You can control in Azure AD who has access tooHR2day by Merces.</span></span>
- <span data-ttu-id="980ca-107">Можно включить пользователей tooautomatically получить подписан в tooHR2day Merces с их учетными записями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="980ca-107">You can enable your users tooautomatically get signed in tooHR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="980ca-108">Вы можете управлять учетными записями в одном централизованном месте--hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="980ca-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="980ca-109">Дополнительные сведения об интеграции приложений SaaS с Azure AD см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="980ca-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="980ca-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="980ca-110">Prerequisites</span></span>

<span data-ttu-id="980ca-111">tooconfigure интеграция Azure AD с HR2day по Merces требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="980ca-111">tooconfigure Azure AD integration with HR2day by Merces, you need hello following items:</span></span>

- <span data-ttu-id="980ca-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="980ca-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="980ca-113">подписка HR2day от Merces с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="980ca-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="980ca-114">Не рекомендуется с помощью рабочей среды tootest hello шаги в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="980ca-114">We don't recommend using a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="980ca-115">tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="980ca-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="980ca-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="980ca-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="980ca-117">Получите [бесплатную пробную версию Azure AD на 1 месяц](https://azure.microsoft.com/pricing/free-trial/), если у вас еще ее нет.</span><span class="sxs-lookup"><span data-stu-id="980ca-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="980ca-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="980ca-118">Scenario description</span></span>
<span data-ttu-id="980ca-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="980ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="980ca-120">сценарий Hello, описанные здесь состоит из двух основных компонентов.</span><span class="sxs-lookup"><span data-stu-id="980ca-120">hello scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="980ca-121">Добавление HR2day по Merces из галереи hello.</span><span class="sxs-lookup"><span data-stu-id="980ca-121">Adding HR2day by Merces from hello gallery.</span></span>
2. <span data-ttu-id="980ca-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="980ca-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-hello-gallery"></a><span data-ttu-id="980ca-123">Добавление HR2day по Merces из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="980ca-123">Add HR2day by Merces from hello gallery</span></span>
<span data-ttu-id="980ca-124">tooconfigure интеграция HR2day по Merces hello в Azure AD, добавить HR2day по Merces из hello коллекции tooyour список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="980ca-124">tooconfigure hello integration of HR2day by Merces into Azure AD, add HR2day by Merces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="980ca-125">**tooadd HR2day по Merces из галереи hello, hello выполните следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="980ca-125">**tooadd HR2day by Merces from hello gallery, take hello following steps:**</span></span>

1. <span data-ttu-id="980ca-126">В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, выберите hello **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="980ca-126">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="980ca-128">Go слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="980ca-128">Go too**Enterprise applications**.</span></span> <span data-ttu-id="980ca-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="980ca-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="980ca-131">tooadd нового приложения, выберите hello **новое приложение** кнопку в верхней части hello диалогового окна «hello».</span><span class="sxs-lookup"><span data-stu-id="980ca-131">tooadd a new application, select hello **New application** button on hello top of hello dialog box.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="980ca-133">Введите в поле поиска hello **HR2day по Merces**.</span><span class="sxs-lookup"><span data-stu-id="980ca-133">In hello search box, type **HR2day by Merces**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="980ca-135">Hello панели результатов выберите **HR2day по Merces**, а затем выберите hello **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="980ca-135">In hello results panel, select **HR2day by Merces**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="980ca-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="980ca-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="980ca-138">В этом разделе описана настройка и проверка единого входа Azure AD в HR2day от Merces с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="980ca-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="980ca-139">Для единого входа toowork Azure AD необходима tooknow кто hello пользователем аналога в HR2day по Merces tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="980ca-139">For single sign-on toowork, Azure AD needs tooknow who hello counterpart user in HR2day by Merces is tooa user in Azure AD.</span></span> <span data-ttu-id="980ca-140">Другими словами необходимо tooestablish связь между пользователя Azure AD и связанных пользователей hello в HR2day по Merces.</span><span class="sxs-lookup"><span data-stu-id="980ca-140">In other words, you need tooestablish a link between an Azure AD user and hello related user in HR2day by Merces.</span></span>

<span data-ttu-id="980ca-141">Присвойте hello в HR2day по Merces **имя пользователя** в Azure AD слишком **имя пользователя** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="980ca-141">In HR2day by Merces, assign hello **user name** in Azure AD too **Username** tooestablish hello relationship.</span></span>

<span data-ttu-id="980ca-142">tooconfigure и теста Azure AD единого входа с HR2day по Merces, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="980ca-142">tooconfigure and test Azure AD single sign-on with HR2day by Merces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="980ca-143">[Настройка Azure AD единого входа](#configuring-azure-ad-single-sign-on): включить эту функцию на toouse пользователей.</span><span class="sxs-lookup"><span data-stu-id="980ca-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users toouse this feature.</span></span>
2. <span data-ttu-id="980ca-144">[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="980ca-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="980ca-145">[Создание HR2day пользователем теста Merces](#creating-an-hr2day-by-merces-test-user): создание аналог Саймон Britta в HR2day по Merces, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="980ca-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="980ca-146">[Назначить hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user): Включение Саймон Britta toouse Azure AD единого входа.</span><span class="sxs-lookup"><span data-stu-id="980ca-146">[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="980ca-147">[Тестирование единого входа](#testing-single-sign-on): Проверьте, работает ли конфигурация hello.</span><span class="sxs-lookup"><span data-stu-id="980ca-147">[Test single sign-on](#testing-single-sign-on): Verify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="980ca-148">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="980ca-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="980ca-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей HR2day Merces приложением.</span><span class="sxs-lookup"><span data-stu-id="980ca-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="980ca-150">**tooconfigure Azure AD единого входа с HR2day по Merces, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="980ca-150">**tooconfigure Azure AD single sign-on with HR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="980ca-151">В hello в hello портала Azure **HR2day по Merces** странице интеграции приложений выберите **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="980ca-151">In hello Azure portal, on hello **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="980ca-153">tooenable единого входа, в hello **единого входа** выберите **режим** как **входа на базе SAML**.</span><span class="sxs-lookup"><span data-stu-id="980ca-153">tooenable single sign-on, in hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="980ca-155">В hello **HR2day Merces доменом и URL-адреса** примите hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="980ca-155">In hello **HR2day by Merces Domain and URLs** section, take hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="980ca-157">а.</span><span class="sxs-lookup"><span data-stu-id="980ca-157">a.</span></span> <span data-ttu-id="980ca-158">В hello **URL-адрес входа** введите URL-адрес, используя следующий шаблон hello: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="980ca-158">In hello **Sign-on URL** box, type a URL by using hello following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="980ca-159">b.</span><span class="sxs-lookup"><span data-stu-id="980ca-159">b.</span></span> <span data-ttu-id="980ca-160">В hello **идентификатор** введите URL-адрес, используя следующий шаблон hello: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="980ca-160">In hello **Identifier** box, type a URL by using hello following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="980ca-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="980ca-161">These values are not real.</span></span> <span data-ttu-id="980ca-162">Обновите эти значения с hello фактический URL-адрес входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="980ca-162">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="980ca-163">Обратитесь в службу hello [HR2day группой поддержки клиента Merces](mailto:servicedesk@merces.nl) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="980ca-163">Contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl) tooget these values.</span></span> 
 


4. <span data-ttu-id="980ca-164">На hello **сертификат подписи SAML** выберите **Certificate(Base64)**, а затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="980ca-164">On hello **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="980ca-166">В этом разделе описываются как tooHR2day tooauthenticate tooenable пользователей по Merces с учетной записью в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="980ca-166">This section describes how tooenable users tooauthenticate tooHR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="980ca-167">Они это сделать с помощью федерации на основании hello протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="980ca-167">They do this by using federation that's based on hello SAML protocol.</span></span>

    <span data-ttu-id="980ca-168">Ваш HR2day приложением Merces ожидает утверждения SAML hello в определенном формате, требующей маркера SAML tooyour сопоставления настраиваемого атрибута tooadd.</span><span class="sxs-lookup"><span data-stu-id="980ca-168">Your HR2day by Merces application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token.</span></span> <span data-ttu-id="980ca-169">Следующий снимок экрана приветствия показан пример этого.</span><span class="sxs-lookup"><span data-stu-id="980ca-169">hello following screenshot shows an example of this.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="980ca-171">Перед настройкой hello утверждения SAML, необходимо обратиться к hello [HR2day группой поддержки клиента Merces](mailto:servicedesk@merces.nl) и запросить значение hello hello уникальный идентификатор атрибута для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="980ca-171">Before you can configure hello SAML assertion, you must contact hello [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="980ca-172">Необходимо, чтобы это значение toocomplete hello действия, описанные в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="980ca-172">You need this value toocomplete hello steps in hello next section.</span></span> 

6. <span data-ttu-id="980ca-173">В hello **единого входа** диалогового окна hello **атрибуты пользователя** статьи, настройте атрибутов токена SAML hello, как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="980ca-173">In hello **Single sign-on** dialog box, in hello **User Attributes** section, configure hello SAML token attribute as shown in hello following image.</span></span> <span data-ttu-id="980ca-174">Затем выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="980ca-174">Then take hello following steps.</span></span>
    
      | <span data-ttu-id="980ca-175">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="980ca-175">Attribute name</span></span>    |   <span data-ttu-id="980ca-176">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="980ca-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="980ca-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="980ca-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="980ca-178">join([mail],"102938475Z","@"</span><span class="sxs-lookup"><span data-stu-id="980ca-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="980ca-179">а.</span><span class="sxs-lookup"><span data-stu-id="980ca-179">a.</span></span> <span data-ttu-id="980ca-180">tooopen hello **Добавление атрибута** диалогового окна выберите **добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="980ca-180">tooopen hello **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="980ca-183">b.</span><span class="sxs-lookup"><span data-stu-id="980ca-183">b.</span></span> <span data-ttu-id="980ca-184">В hello **имя** введите **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="980ca-184">In hello **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="980ca-185">c.</span><span class="sxs-lookup"><span data-stu-id="980ca-185">c.</span></span> <span data-ttu-id="980ca-186">Из hello **значение** выберите **Join()**.</span><span class="sxs-lookup"><span data-stu-id="980ca-186">From hello **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="980ca-187">d.</span><span class="sxs-lookup"><span data-stu-id="980ca-187">d.</span></span> <span data-ttu-id="980ca-188">Из hello **String1** выберите **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="980ca-188">From hello **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="980ca-189">д.</span><span class="sxs-lookup"><span data-stu-id="980ca-189">e.</span></span> <span data-ttu-id="980ca-190">Для **String2**, введите уникальный идентификатор hello, предоставляемая HR2day команды.</span><span class="sxs-lookup"><span data-stu-id="980ca-190">For **String2**, type hello unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="980ca-191">f.</span><span class="sxs-lookup"><span data-stu-id="980ca-191">f.</span></span> <span data-ttu-id="980ca-192">В hello **разделителя** введите  **@** .</span><span class="sxs-lookup"><span data-stu-id="980ca-192">In hello **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="980ca-193">ж.</span><span class="sxs-lookup"><span data-stu-id="980ca-193">g.</span></span> <span data-ttu-id="980ca-194">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="980ca-194">Select **Ok**.</span></span>

7. <span data-ttu-id="980ca-195">Выберите hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="980ca-195">Select hello **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="980ca-197">В hello **HR2day конфигурацией Merces** выберите **Настройка HR2day по Merces** tooopen hello **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="980ca-197">In hello **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="980ca-198">Копировать hello **URL-адрес выхода**, **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** из hello **краткий справочник** раздела.</span><span class="sxs-lookup"><span data-stu-id="980ca-198">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="980ca-200">tooconfigure единого входа для вашего приложения, обратитесь в службу hello [HR2day группой поддержки клиента Merces](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="980ca-200">tooconfigure SSO  for your application, contact hello [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="980ca-201">Присоединение загружаются hello **Certificate(Base64)** файл tooyour электронной почты.</span><span class="sxs-lookup"><span data-stu-id="980ca-201">Attach hello downloaded **Certificate(Base64)** file tooyour email.</span></span> <span data-ttu-id="980ca-202">Также предоставляют hello **URL-адрес выхода**, **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** , чтобы они могут быть настроены для интеграции единого входа.</span><span class="sxs-lookup"><span data-stu-id="980ca-202">Also provide hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="980ca-203">Назовите toohello Merces команды, которые требуется такая интеграция hello набор с шаблоном hello toobe идентификатор сущности **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="980ca-203">Mention toohello Merces team that this integration needs hello Entity ID toobe set with hello pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="980ca-204">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="980ca-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="980ca-205">После добавления этого приложения с hello **Active Directory** > **корпоративных приложений** раздел, выберите hello **Single Sign-On** вкладки. Hello доступа внедряются документации с помощью hello **конфигурации** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="980ca-205">After you add this app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab. Then access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="980ca-206">Вы можете прочитать больше о документации embedded hello в hello [Azure AD внедренных документации]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="980ca-206">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="980ca-207">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="980ca-207">Create an Azure AD test user</span></span>
<span data-ttu-id="980ca-208">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="980ca-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="980ca-210">**toocreate тестового пользователя в Azure AD, hello выполните следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="980ca-210">**toocreate a test user in Azure AD, take hello following steps:**</span></span>

1. <span data-ttu-id="980ca-211">В hello **портал Azure**, на левой панели навигации hello, выберите hello **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="980ca-211">In hello **Azure portal**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="980ca-213">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп**и выберите **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="980ca-213">toodisplay hello list of users, go too**Users and groups**, and then select **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="980ca-215">tooopen hello **пользователя** выберите **добавить** в верхней части hello диалогового окна «hello».</span><span class="sxs-lookup"><span data-stu-id="980ca-215">tooopen hello **User** dialog box, select **Add** on hello top of hello dialog box.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="980ca-217">В hello **пользователя** диалоговом hello выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="980ca-217">In hello **User** dialog box, take hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="980ca-219">а.</span><span class="sxs-lookup"><span data-stu-id="980ca-219">a.</span></span> <span data-ttu-id="980ca-220">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="980ca-220">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="980ca-221">b.</span><span class="sxs-lookup"><span data-stu-id="980ca-221">b.</span></span> <span data-ttu-id="980ca-222">В hello **имя пользователя** поле, тип hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="980ca-222">In hello **User name** box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="980ca-223">c.</span><span class="sxs-lookup"><span data-stu-id="980ca-223">c.</span></span> <span data-ttu-id="980ca-224">Выберите **Показать пароль**и запишите пароль hello.</span><span class="sxs-lookup"><span data-stu-id="980ca-224">Select **Show Password**, and then write down hello password.</span></span>

    <span data-ttu-id="980ca-225">d.</span><span class="sxs-lookup"><span data-stu-id="980ca-225">d.</span></span> <span data-ttu-id="980ca-226">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="980ca-226">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="980ca-227">Создание тестового пользователя HR2day от Merces</span><span class="sxs-lookup"><span data-stu-id="980ca-227">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="980ca-228">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в HR2day по Merces.</span><span class="sxs-lookup"><span data-stu-id="980ca-228">hello objective of this section is toocreate a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="980ca-229">Пользователи tooadd hello в учетной записи hello HR2day, работать с hello [HR2day группой поддержки клиента Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="980ca-229">tooadd hello users in hello HR2day account, work with hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="980ca-230">Если вам требуется toocreate пользователя вручную, обратитесь в службу hello [HR2day группой поддержки клиента Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="980ca-230">If you need toocreate a user manually, contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="980ca-231">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="980ca-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="980ca-232">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooHR2day доступ по Merces.</span><span class="sxs-lookup"><span data-stu-id="980ca-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHR2day by Merces.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="980ca-234">**tooassign tooHR2day Britta Simon по Merces hello выполните следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="980ca-234">**tooassign Britta Simon tooHR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="980ca-235">В hello Azure приложений портала, откройте hello просмотра, перейдите в представление каталога toohello, а затем перейдите слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="980ca-235">In hello Azure portal, open hello applications view, go toohello directory view, and then go too**Enterprise applications**.</span></span> <span data-ttu-id="980ca-236">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="980ca-236">Next, select **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="980ca-238">В списке приложений hello выберите **HR2day по Merces**.</span><span class="sxs-lookup"><span data-stu-id="980ca-238">In hello applications list, select **HR2day by Merces**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="980ca-240">Выберите в меню hello слева hello, **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="980ca-240">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="980ca-242">Выберите hello **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="980ca-242">Select hello **Add** button.</span></span> <span data-ttu-id="980ca-243">Затем в hello **добавить назначение** выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="980ca-243">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="980ca-245">В hello **пользователей и групп** диалогового окна hello **пользователей** выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="980ca-245">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="980ca-246">Нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="980ca-246">Click hello **Select** button.</span></span>

7. <span data-ttu-id="980ca-247">В hello **добавить назначение** выберите **назначить**.</span><span class="sxs-lookup"><span data-stu-id="980ca-247">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="980ca-248">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="980ca-248">Test single sign-on</span></span>

<span data-ttu-id="980ca-249">Hello цель этого раздела — tootest конфигурации Azure AD единого входа с помощью hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="980ca-249">hello objective of this section is tootest your Azure AD single sign-on configuration by using hello Access Panel.</span></span>  

<span data-ttu-id="980ca-250">При выборе hello HR2day путем Merces плитки в панели доступа hello вы автоматически получите вход в tooyour HR2day Merces приложением.</span><span class="sxs-lookup"><span data-stu-id="980ca-250">When you select hello HR2day by Merces tile in hello Access Panel, you automatically get signed in  tooyour HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="980ca-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="980ca-251">Additional resources</span></span>

* [<span data-ttu-id="980ca-252">Список учебников о том, как tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="980ca-252">List of tutorials about how tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="980ca-253">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="980ca-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

