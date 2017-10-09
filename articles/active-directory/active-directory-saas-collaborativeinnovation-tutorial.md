---
title: "Руководство по интеграции Azure Active Directory с Collaborative Innovation | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и совместной работы инноваций."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e85fabfe11a380129f319a101aa7c7a9491260f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="44970-103">Руководство по интеграции Azure Active Directory с Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="44970-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="44970-104">В этом учебнике вы узнаете, как toointegrate инноваций совместной работы с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44970-104">In this tutorial, you learn how toointegrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44970-105">Интеграция инноваций совместной работы с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="44970-105">Integrating Collaborative Innovation with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="44970-106">Можно управлять в Azure AD, имеющего доступ tooCollaborative инноваций</span><span class="sxs-lookup"><span data-stu-id="44970-106">You can control in Azure AD who has access tooCollaborative Innovation</span></span>
- <span data-ttu-id="44970-107">Можно включить на пользователей tooautomatically get вошедшего tooCollaborative инноваций (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="44970-107">You can enable your users tooautomatically get signed-on tooCollaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44970-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="44970-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="44970-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44970-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44970-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="44970-110">Prerequisites</span></span>

<span data-ttu-id="44970-111">tooconfigure интеграция Azure AD с совместной работы инноваций требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="44970-111">tooconfigure Azure AD integration with Collaborative Innovation, you need hello following items:</span></span>

- <span data-ttu-id="44970-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="44970-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44970-113">подписка на Collaborative Innovation с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="44970-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44970-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="44970-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44970-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="44970-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44970-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="44970-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44970-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44970-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44970-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="44970-118">Scenario description</span></span>
<span data-ttu-id="44970-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="44970-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44970-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="44970-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44970-121">Добавление совместной работы инноваций из галереи hello</span><span class="sxs-lookup"><span data-stu-id="44970-121">Adding Collaborative Innovation from hello gallery</span></span>
2. <span data-ttu-id="44970-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44970-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-hello-gallery"></a><span data-ttu-id="44970-123">Добавление совместной работы инноваций из галереи hello</span><span class="sxs-lookup"><span data-stu-id="44970-123">Adding Collaborative Innovation from hello gallery</span></span>
<span data-ttu-id="44970-124">tooconfigure hello интеграция инноваций совместной работы в Azure AD, вы должны tooadd инноваций совместной работы из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="44970-124">tooconfigure hello integration of Collaborative Innovation into Azure AD, you need tooadd Collaborative Innovation from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="44970-125">**tooadd совместной работы инноваций из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="44970-125">**tooadd Collaborative Innovation from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="44970-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="44970-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="44970-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="44970-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="44970-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="44970-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="44970-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="44970-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="44970-133">Введите в поле поиска hello **совместной работы инноваций**.</span><span class="sxs-lookup"><span data-stu-id="44970-133">In hello search box, type **Collaborative Innovation**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="44970-135">В панели результатов hello, выберите **совместной работы инноваций**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="44970-135">In hello results panel, select **Collaborative Innovation**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44970-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44970-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44970-138">В этом разделе описана настройка и проверка единого входа Azure AD в Collaborative Innovation с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44970-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="44970-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello совместной работы инновации является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44970-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Collaborative Innovation is tooa user in Azure AD.</span></span> <span data-ttu-id="44970-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello совместной работы инновации должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="44970-140">In other words, a link relationship between an Azure AD user and hello related user in Collaborative Innovation needs toobe established.</span></span>

<span data-ttu-id="44970-141">Инновации совместной работы, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="44970-141">In Collaborative Innovation, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="44970-142">tooconfigure и теста Azure AD единого входа с совместной работы инноваций, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="44970-142">tooconfigure and test Azure AD single sign-on with Collaborative Innovation, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="44970-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="44970-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="44970-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="44970-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44970-145">**[Создание тестового пользователя совместной работы инноваций](#creating-a-collaborative-innovation-test-user)**  -toohave аналог Саймон Britta совместной работы инновации, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="44970-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - toohave a counterpart of Britta Simon in Collaborative Innovation that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="44970-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="44970-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44970-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="44970-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44970-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44970-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44970-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении инноваций совместной работы.</span><span class="sxs-lookup"><span data-stu-id="44970-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="44970-150">**Azure AD tooconfigure единого входа с совместной работы инновационным выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="44970-150">**tooconfigure Azure AD single sign-on with Collaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="44970-151">В hello в hello портала Azure **совместной работы инноваций** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="44970-151">In hello Azure portal, on hello **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="44970-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="44970-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="44970-155">На hello **URL-адреса и совместной работы домена инноваций** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="44970-155">On hello **Collaborative Innovation Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="44970-157">а.</span><span class="sxs-lookup"><span data-stu-id="44970-157">a.</span></span> <span data-ttu-id="44970-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="44970-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="44970-159">b.</span><span class="sxs-lookup"><span data-stu-id="44970-159">b.</span></span> <span data-ttu-id="44970-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="44970-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="44970-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="44970-161">These values are not real.</span></span> <span data-ttu-id="44970-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="44970-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="44970-163">Обратитесь к [группа поддержки совместной работы клиента инноваций](https://www.unilever.com/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="44970-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) tooget these values.</span></span>  

4. <span data-ttu-id="44970-164">Приложение для совместной работы инноваций ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="44970-164">Collaborative Innovation application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="44970-165">Выполните настройку следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="44970-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="44970-166">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="44970-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="44970-167">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="44970-167">hello following screenshot shows an example for this.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="44970-169">Нажмите кнопку **представление и редактировать все остальные атрибуты пользователя** флажок в hello **атрибуты пользователя** статьи tooexpand hello атрибуты.</span><span class="sxs-lookup"><span data-stu-id="44970-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="44970-170">Выполните следующие действия на каждом из hello отображаются атрибуты - hello</span><span class="sxs-lookup"><span data-stu-id="44970-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="44970-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="44970-171">Attribute Name</span></span> | <span data-ttu-id="44970-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="44970-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="44970-173">givenname</span><span class="sxs-lookup"><span data-stu-id="44970-173">givenname</span></span> | <span data-ttu-id="44970-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="44970-174">user.givenname</span></span> |
    | <span data-ttu-id="44970-175">surname</span><span class="sxs-lookup"><span data-stu-id="44970-175">surname</span></span> | <span data-ttu-id="44970-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="44970-176">user.surname</span></span> |
    | <span data-ttu-id="44970-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="44970-177">emailaddress</span></span> | <span data-ttu-id="44970-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="44970-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="44970-179">name</span><span class="sxs-lookup"><span data-stu-id="44970-179">name</span></span> | <span data-ttu-id="44970-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="44970-180">user.userprincipalname</span></span> |

    <span data-ttu-id="44970-181">а.</span><span class="sxs-lookup"><span data-stu-id="44970-181">a.</span></span> <span data-ttu-id="44970-182">Нажмите кнопку hello атрибут tooopen hello **изменение атрибута** окна.</span><span class="sxs-lookup"><span data-stu-id="44970-182">Click hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="44970-184">b.</span><span class="sxs-lookup"><span data-stu-id="44970-184">b.</span></span> <span data-ttu-id="44970-185">Удалить значение URL-адрес hello из hello **пространства имен**.</span><span class="sxs-lookup"><span data-stu-id="44970-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="44970-186">c.</span><span class="sxs-lookup"><span data-stu-id="44970-186">c.</span></span> <span data-ttu-id="44970-187">Нажмите кнопку **ОК** toosave приветствия.</span><span class="sxs-lookup"><span data-stu-id="44970-187">Click **Ok** toosave hello setting.</span></span>

6. <span data-ttu-id="44970-188">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="44970-188">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="44970-190">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="44970-190">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="44970-192">tooconfigure единого входа на **совместной работы инноваций** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группа поддержки совместной работы инноваций](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="44970-192">tooconfigure single sign-on on **Collaborative Innovation** side, you need toosend hello downloaded **Metadata XML** too[Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="44970-193">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="44970-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="44970-194">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="44970-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="44970-195">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="44970-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="44970-196">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="44970-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44970-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="44970-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="44970-198">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="44970-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="44970-200">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="44970-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="44970-201">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="44970-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44970-203">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="44970-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44970-205">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="44970-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44970-207">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="44970-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44970-209">а.</span><span class="sxs-lookup"><span data-stu-id="44970-209">a.</span></span> <span data-ttu-id="44970-210">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44970-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44970-211">b.</span><span class="sxs-lookup"><span data-stu-id="44970-211">b.</span></span> <span data-ttu-id="44970-212">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="44970-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44970-213">c.</span><span class="sxs-lookup"><span data-stu-id="44970-213">c.</span></span> <span data-ttu-id="44970-214">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="44970-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="44970-215">d.</span><span class="sxs-lookup"><span data-stu-id="44970-215">d.</span></span> <span data-ttu-id="44970-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="44970-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="44970-217">Создание тестового пользователя Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="44970-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="44970-218">Пользователи toolog tooenable Azure AD в tooCollaborative инноваций, их необходимо подготовить в инноваций совместной работы.</span><span class="sxs-lookup"><span data-stu-id="44970-218">tooenable Azure AD users toolog in tooCollaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="44970-219">В случае это приложение подготовки происходит автоматически, что приложение hello поддерживает только в время подготовки пользователей.</span><span class="sxs-lookup"><span data-stu-id="44970-219">In case of this application provisioning is automatic as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="44970-220">Поэтому нет нет необходимости tooperform какие шаги здесь.</span><span class="sxs-lookup"><span data-stu-id="44970-220">So there is no need tooperform any steps here.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="44970-221">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="44970-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="44970-222">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCollaborative инноваций.</span><span class="sxs-lookup"><span data-stu-id="44970-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCollaborative Innovation.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="44970-224">**tooassign tooCollaborative Britta Simon инноваций выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="44970-224">**tooassign Britta Simon tooCollaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="44970-225">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="44970-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="44970-227">В списке приложений hello выберите **совместной работы инноваций**.</span><span class="sxs-lookup"><span data-stu-id="44970-227">In hello applications list, select **Collaborative Innovation**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="44970-229">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="44970-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="44970-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="44970-231">Click **Add** button.</span></span> <span data-ttu-id="44970-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="44970-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="44970-234">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="44970-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="44970-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="44970-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44970-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="44970-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="44970-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="44970-237">Testing single sign-on</span></span>

<span data-ttu-id="44970-238">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="44970-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="44970-239">При выборе плитки hello совместной работы инновации в hello панели доступа, должно появиться страница входа инноваций совместной работы приложения.</span><span class="sxs-lookup"><span data-stu-id="44970-239">When you click hello Collaborative Innovation tile in hello Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="44970-240">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44970-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="44970-241">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="44970-241">Additional resources</span></span>

* [<span data-ttu-id="44970-242">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44970-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44970-243">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44970-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

