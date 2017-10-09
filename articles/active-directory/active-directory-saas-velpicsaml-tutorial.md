---
title: "Руководство по интеграции Azure Active Directory с Velpic SAML | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Velpic SAML."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="0b46b-103">Руководство. Интеграция Azure Active Directory с Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="0b46b-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="0b46b-104">В этом учебнике вы узнаете, как toointegrate Velpic SAML в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b46b-104">In this tutorial, you learn how toointegrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b46b-105">Интеграция с Azure AD Velpic SAML предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0b46b-105">Integrating Velpic SAML with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0b46b-106">Можно управлять в Azure AD, имеющего доступ tooVelpic SAML</span><span class="sxs-lookup"><span data-stu-id="0b46b-106">You can control in Azure AD who has access tooVelpic SAML</span></span>
- <span data-ttu-id="0b46b-107">Можно включить на пользователей tooautomatically get вошедшего tooVelpic SAML (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b46b-107">You can enable your users tooautomatically get signed-on tooVelpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b46b-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="0b46b-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="0b46b-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b46b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b46b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0b46b-110">Prerequisites</span></span>

<span data-ttu-id="0b46b-111">tooconfigure интеграция Azure AD с Velpic SAML требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0b46b-111">tooconfigure Azure AD integration with Velpic SAML, you need hello following items:</span></span>

- <span data-ttu-id="0b46b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0b46b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b46b-113">подписка на приложение Velpic SAML с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0b46b-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b46b-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="0b46b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b46b-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="0b46b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b46b-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="0b46b-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0b46b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b46b-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b46b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0b46b-118">Scenario description</span></span>
<span data-ttu-id="0b46b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0b46b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b46b-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="0b46b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b46b-121">Добавление Velpic SAML из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0b46b-121">Adding Velpic SAML from hello gallery</span></span>
2. <span data-ttu-id="0b46b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b46b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-hello-gallery"></a><span data-ttu-id="0b46b-123">Добавление Velpic SAML из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0b46b-123">Adding Velpic SAML from hello gallery</span></span>
<span data-ttu-id="0b46b-124">tooconfigure hello интеграции Velpic SAML в Azure AD, вы должны tooadd Velpic SAML из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0b46b-124">tooconfigure hello integration of Velpic SAML into Azure AD, you need tooadd Velpic SAML from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0b46b-125">**tooadd Velpic SAML из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0b46b-125">**tooadd Velpic SAML from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b46b-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0b46b-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0b46b-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0b46b-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0b46b-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="0b46b-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0b46b-133">Введите в поле поиска hello **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-133">In hello search box, type **Velpic SAML**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="0b46b-135">В панели результатов hello выберите **Velpic SAML**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0b46b-135">In hello results panel, select **Velpic SAML**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b46b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b46b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0b46b-138">В этом разделе описана настройка и проверка единого входа Azure AD в Velpic SAML с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b46b-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0b46b-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Velpic SAML является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b46b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Velpic SAML is tooa user in Azure AD.</span></span> <span data-ttu-id="0b46b-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Velpic SAML должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="0b46b-140">In other words, a link relationship between an Azure AD user and hello related user in Velpic SAML needs toobe established.</span></span>

<span data-ttu-id="0b46b-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="0b46b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Velpic SAML.</span></span>

<span data-ttu-id="0b46b-142">tooconfigure и теста Azure AD единого входа с Velpic SAML, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0b46b-142">tooconfigure and test Azure AD single sign-on with Velpic SAML, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0b46b-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="0b46b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0b46b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0b46b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b46b-145">**[Создание тестового пользователя Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave аналог Саймон Britta в Velpic SAML, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="0b46b-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - toohave a counterpart of Britta Simon in Velpic SAML that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="0b46b-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="0b46b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b46b-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b46b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b46b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b46b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b46b-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="0b46b-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="0b46b-150">**tooconfigure Azure AD единого входа с Velpic SAML, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0b46b-150">**tooconfigure Azure AD single sign-on with Velpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b46b-151">На портале управления Azure hello на hello **Velpic SAML** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-151">In hello Azure Management portal, on hello **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0b46b-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="0b46b-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="0b46b-155">Введите сведения hello в hello **URL-адреса и домена SAML Velpic** раздел -</span><span class="sxs-lookup"><span data-stu-id="0b46b-155">Enter hello details in hello **Velpic SAML Domain and URLs** section-</span></span>

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="0b46b-157">а.</span><span class="sxs-lookup"><span data-stu-id="0b46b-157">a.</span></span> <span data-ttu-id="0b46b-158">В hello **URL-адрес входа** текстовое поле, значение типа hello как:`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="0b46b-158">In hello **Sign-on URL** textbox, type hello value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="0b46b-159">b.</span><span class="sxs-lookup"><span data-stu-id="0b46b-159">b.</span></span> <span data-ttu-id="0b46b-160">В hello **идентификатор** текстовое поле, вставить hello **«Единый вход на URL-адрес»** значение`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="0b46b-160">In hello **Identifier** textbox, paste hello **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="0b46b-161">Обратите внимание, что hello URL-адрес входа будут предоставляться hello team Velpic SAML и значение идентификатора, будут доступны при настройке hello надстройки SSO на ОСНОВЕ Velpic SAML стороны.</span><span class="sxs-lookup"><span data-stu-id="0b46b-161">Please note that hello Sign on URL will be provided by hello Velpic SAML team and Identifier value will be available when you configure hello SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="0b46b-162">Необходимо toocopy, от Velpic SAML страницы приложения и вставьте его здесь.</span><span class="sxs-lookup"><span data-stu-id="0b46b-162">You need toocopy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="0b46b-163">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0b46b-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="0b46b-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0b46b-165">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0b46b-167">На hello раздел конфигурации Velpic SAML нажмите кнопку настроить SAML Velpic tooopen Настройка единого входа окна.</span><span class="sxs-lookup"><span data-stu-id="0b46b-167">On hello Velpic SAML Configuration section, click Configure Velpic SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="0b46b-168">Скопируйте идентификатор сущности SAML hello из hello краткий справочник.</span><span class="sxs-lookup"><span data-stu-id="0b46b-168">Copy hello SAML Entity ID from hello Quick Reference section.</span></span>

7. <span data-ttu-id="0b46b-169">В другом окне веб-браузера войдите на корпоративный сайт Velpic SAML с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="0b46b-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="0b46b-170">Щелкните **управление** вкладку и перейти слишком**интеграции** раздел, где требуется tooclick на **подключаемые модули** кнопку toocreate нового подключаемого модуля для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="0b46b-170">Click on **Manage** tab and go too**Integration** section where you need tooclick on **Plugins** button toocreate new plugin for Sign-In.</span></span>

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="0b46b-172">Щелкните hello **«Добавить подключаемый модуль»** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0b46b-172">Click on hello **‘Add plugin’** button.</span></span>
    
    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="0b46b-174">Щелкните hello **SAML** плитку на странице приветствия добавить подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="0b46b-174">Click on hello **SAML** tile in hello Add Plugin page.</span></span>
    
    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="0b46b-176">Введите имя hello hello нового подключаемого модуля SAML и нажмите кнопку hello **«Add»** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0b46b-176">Enter hello name of hello new SAML plugin and click hello **‘Add’** button.</span></span>

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="0b46b-178">Введите сведения о hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0b46b-178">Enter hello details as follows:</span></span>

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="0b46b-180">а.</span><span class="sxs-lookup"><span data-stu-id="0b46b-180">a.</span></span> <span data-ttu-id="0b46b-181">В hello **имя** текстовое поле, имя типа hello SAML подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="0b46b-181">In hello **Name** textbox, type hello name of SAML plugin.</span></span>

    <span data-ttu-id="0b46b-182">b.</span><span class="sxs-lookup"><span data-stu-id="0b46b-182">b.</span></span> <span data-ttu-id="0b46b-183">В hello **URL-адрес издателя** текстовое поле, вставить hello **идентификатор сущности SAML** копируются hello **Настройка входа** окно hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0b46b-183">In hello **Issuer URL** textbox, paste hello **SAML Entity ID** you copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="0b46b-184">c.</span><span class="sxs-lookup"><span data-stu-id="0b46b-184">c.</span></span> <span data-ttu-id="0b46b-185">В hello **конфигурации поставщика метаданных** отправить hello файл метаданные в формате XML, который был загружен с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="0b46b-185">In hello **Provider Metadata Config** upload hello Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="0b46b-186">d.</span><span class="sxs-lookup"><span data-stu-id="0b46b-186">d.</span></span> <span data-ttu-id="0b46b-187">Вы также можете tooenable SAML на время подготовки, включив hello **«Автоматическое создание новых пользователей»** флажок.</span><span class="sxs-lookup"><span data-stu-id="0b46b-187">You can also choose tooenable SAML just in time provisioning by enabling hello **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="0b46b-188">Если этот флаг не включен, пользователь не существует в Velpic, произойдет ошибка входа hello из Azure.</span><span class="sxs-lookup"><span data-stu-id="0b46b-188">If a user doesn’t exist in Velpic and this flag is not enabled, hello login from Azure will fail.</span></span> <span data-ttu-id="0b46b-189">Если флаг hello не включена hello пользователя будет автоматически подготовить в Velpic во время hello имени входа.</span><span class="sxs-lookup"><span data-stu-id="0b46b-189">If hello flag is enabled hello user will automatically be provisioned into Velpic at hello time of login.</span></span> 

    <span data-ttu-id="0b46b-190">д.</span><span class="sxs-lookup"><span data-stu-id="0b46b-190">e.</span></span> <span data-ttu-id="0b46b-191">Копировать hello **единый вход на URL-адрес** из hello текстовое поле и вставить его в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0b46b-191">Copy hello **Single sign on URL** from hello text box and paste it in hello Azure portal.</span></span>
    
    <span data-ttu-id="0b46b-192">f.</span><span class="sxs-lookup"><span data-stu-id="0b46b-192">f.</span></span> <span data-ttu-id="0b46b-193">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b46b-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b46b-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="0b46b-195">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0b46b-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0b46b-197">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0b46b-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b46b-198">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0b46b-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b46b-200">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="0b46b-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b46b-202">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0b46b-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b46b-204">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0b46b-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b46b-206">а.</span><span class="sxs-lookup"><span data-stu-id="0b46b-206">a.</span></span> <span data-ttu-id="0b46b-207">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b46b-208">b.</span><span class="sxs-lookup"><span data-stu-id="0b46b-208">b.</span></span> <span data-ttu-id="0b46b-209">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0b46b-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b46b-210">c.</span><span class="sxs-lookup"><span data-stu-id="0b46b-210">c.</span></span> <span data-ttu-id="0b46b-211">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0b46b-212">d.</span><span class="sxs-lookup"><span data-stu-id="0b46b-212">d.</span></span> <span data-ttu-id="0b46b-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="0b46b-214">Создание тестового пользователя Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="0b46b-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="0b46b-215">Этот шаг необязателен обычно как приложение hello поддерживает только в время подготовки пользователей.</span><span class="sxs-lookup"><span data-stu-id="0b46b-215">This step is usually not required as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="0b46b-216">Hello автоматическую подготовку пользователя не включено Создание пользователя вручную можно сделать, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="0b46b-216">If hello automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="0b46b-217">Войдите на корпоративный сайт Velpic SAML с правами администратора и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0b46b-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="0b46b-218">Выберите вкладку "Управление" и перейдите tooUsers раздела, затем щелкните на новых пользователей tooadd кнопки.</span><span class="sxs-lookup"><span data-stu-id="0b46b-218">Click on Manage tab and go tooUsers section, then click on New button tooadd users.</span></span>

    ![добавить пользователя](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="0b46b-220">На hello **«Создать нового пользователя»** диалогового окна выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="0b46b-220">On hello **“Create New User”** dialog page, perform hello following steps.</span></span>

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="0b46b-222">а.</span><span class="sxs-lookup"><span data-stu-id="0b46b-222">a.</span></span> <span data-ttu-id="0b46b-223">В hello **имя** текстовое поле, имя первого типа hello Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0b46b-223">In hello **First Name** textbox, type hello first name of Britta Simon.</span></span>

    <span data-ttu-id="0b46b-224">b.</span><span class="sxs-lookup"><span data-stu-id="0b46b-224">b.</span></span> <span data-ttu-id="0b46b-225">В hello **Фамилия** текстового поля, типа hello Фамилия Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0b46b-225">In hello **Last Name** textbox, type hello last name of Britta Simon.</span></span>

    <span data-ttu-id="0b46b-226">c.</span><span class="sxs-lookup"><span data-stu-id="0b46b-226">c.</span></span> <span data-ttu-id="0b46b-227">В hello **имя пользователя** текстовом поле введите имя пользователя hello объекта Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0b46b-227">In hello **User Name** textbox, type hello user name of Britta Simon.</span></span>

    <span data-ttu-id="0b46b-228">d.</span><span class="sxs-lookup"><span data-stu-id="0b46b-228">d.</span></span> <span data-ttu-id="0b46b-229">В hello **электронной почты** текстовом поле введите адрес электронной почты hello Саймон Britta учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0b46b-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="0b46b-230">д.</span><span class="sxs-lookup"><span data-stu-id="0b46b-230">e.</span></span> <span data-ttu-id="0b46b-231">Остальные сведения hello является необязательным, можно заполнить его при необходимости.</span><span class="sxs-lookup"><span data-stu-id="0b46b-231">Rest of hello information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="0b46b-232">f.</span><span class="sxs-lookup"><span data-stu-id="0b46b-232">f.</span></span> <span data-ttu-id="0b46b-233">Щелкните **СОХРАНИТЬ**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-233">Click **SAVE**.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0b46b-234">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="0b46b-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0b46b-235">В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooVelpic SAML.</span><span class="sxs-lookup"><span data-stu-id="0b46b-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooVelpic SAML.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0b46b-237">**tooassign tooVelpic Britta Simon SAML, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="0b46b-237">**tooassign Britta Simon tooVelpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b46b-238">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-238">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0b46b-240">В списке приложений hello выберите **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-240">In hello applications list, select **Velpic SAML**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="0b46b-242">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0b46b-244">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-244">Click **Add** button.</span></span> <span data-ttu-id="0b46b-245">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0b46b-247">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="0b46b-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0b46b-248">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b46b-249">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0b46b-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0b46b-250">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0b46b-250">Testing single sign-on</span></span>

<span data-ttu-id="0b46b-251">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="0b46b-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="0b46b-252">При нажатии кнопки hello Velpic SAML плитки в панели доступа hello, должно появиться страница входа Velpic SAML приложения.</span><span class="sxs-lookup"><span data-stu-id="0b46b-252">When you click hello Velpic SAML tile in hello Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="0b46b-253">Вы увидите hello **«Войти с Azure AD»** кнопку на страницу входа hello.</span><span class="sxs-lookup"><span data-stu-id="0b46b-253">You should see hello **‘Log In With Azure AD’** button on hello sign in page.</span></span>

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="0b46b-255">Щелкните hello **«Войти с Azure AD»** toolog кнопки в tooVelpic с помощью учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b46b-255">Click on hello **‘Log In With Azure AD’** button toolog in tooVelpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0b46b-256">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0b46b-256">Additional resources</span></span>

* [<span data-ttu-id="0b46b-257">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b46b-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b46b-258">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0b46b-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

