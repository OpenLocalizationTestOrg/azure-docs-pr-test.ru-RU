---
title: "Руководство по интеграции Azure Active Directory с Five9 Plus Adapter (CTI, Contact Center Agents) | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Five9 адаптера, а также (контакт Center агентов, CTI)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="86069-103">Руководство по интеграции Azure Active Directory с Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="86069-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="86069-104">В этом учебнике вы узнаете, как toointegrate Five9 Plus адаптера (CTI, агенты Center контактов) с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86069-104">In this tutorial, you learn how toointegrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86069-105">Интеграция Five9 адаптера, а также (CTI, агенты Center контактов) с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="86069-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="86069-106">Можно управлять в Azure AD, имеющего доступ tooFive9 плюс адаптера (контакт Center агентов, CTI)</span><span class="sxs-lookup"><span data-stu-id="86069-106">You can control in Azure AD who has access tooFive9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="86069-107">Можно включить пользователя пользователей tooautomatically get вошедшего tooFive9 плюс адаптера (CTI, агенты Center контакт) (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="86069-107">You can enable your users tooautomatically get signed-on tooFive9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86069-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="86069-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="86069-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86069-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86069-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="86069-110">Prerequisites</span></span>

<span data-ttu-id="86069-111">Интеграция tooconfigure Azure AD с Five9 плюс адаптером (CTI, агенты Center контакт), необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="86069-111">tooconfigure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need hello following items:</span></span>

- <span data-ttu-id="86069-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="86069-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86069-113">подписка Five9 Plus Adapter (CTI, Contact Center Agents) с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="86069-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86069-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="86069-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86069-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="86069-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86069-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="86069-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86069-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86069-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86069-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="86069-118">Scenario description</span></span>
<span data-ttu-id="86069-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="86069-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86069-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="86069-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86069-121">Добавление Five9 адаптера, а также (CTI, агенты Center контакт) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="86069-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
2. <span data-ttu-id="86069-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="86069-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a><span data-ttu-id="86069-123">Добавление Five9 адаптера, а также (CTI, агенты Center контакт) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="86069-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
<span data-ttu-id="86069-124">tooconfigure hello интеграция Five9 адаптера, а также (CTI, агенты Center контактов) в Azure AD, вы должны tooadd Five9 адаптера, а также (CTI, агенты Center контакт) из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="86069-124">tooconfigure hello integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="86069-125">**tooadd Five9 плюс адаптера (CTI, агенты Center контакт) из коллекции hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="86069-125">**tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="86069-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="86069-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="86069-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="86069-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="86069-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="86069-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="86069-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="86069-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="86069-133">Введите в поле поиска hello **Five9 адаптера, а также (CTI, агенты Center контакт)**.</span><span class="sxs-lookup"><span data-stu-id="86069-133">In hello search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="86069-135">В панели результатов hello выберите **Five9 адаптера, а также (контакт Center агентов, CTI)**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="86069-135">In hello results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="86069-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="86069-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="86069-138">В этом разделе описана настройка и проверка единого входа Azure AD в Five9 Plus Adapter (CTI, Contact Center Agents) для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86069-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="86069-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Five9 адаптера, а также (CTI, агенты Center контакт) является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86069-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is tooa user in Azure AD.</span></span> <span data-ttu-id="86069-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Five9 адаптера, а также (CTI, агенты Center контакт) должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="86069-140">In other words, a link relationship between an Azure AD user and hello related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs toobe established.</span></span>

<span data-ttu-id="86069-141">В Five9 плюс адаптера (контакт Center агентов, CTI), присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="86069-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="86069-142">tooconfigure и теста Azure AD единого входа с Five9 плюс адаптера (CTI, агенты Center контакт), требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="86069-142">tooconfigure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="86069-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="86069-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="86069-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="86069-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86069-145">**[Создание тестового пользователя Five9 адаптера, а также (CTI, агенты Center контакт)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave аналог Саймон Britta в Five9, а также адаптер (контакт Center агентов, CTI), представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="86069-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - toohave a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="86069-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="86069-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86069-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="86069-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="86069-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="86069-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="86069-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Five9 адаптера, а также (контакт Center агентов, CTI).</span><span class="sxs-lookup"><span data-stu-id="86069-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="86069-150">**tooconfigure Azure AD единого входа с Five9 адаптером, а также (CTI, обратитесь в службу центра агенты), выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="86069-150">**tooconfigure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="86069-151">В hello в hello портала Azure **Five9 адаптера, а также (CTI, агенты Center контакт)** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="86069-151">In hello Azure portal, on hello **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="86069-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="86069-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="86069-155">На hello **Five9 адаптера, а также (CTI, агенты Center контакт) домена и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="86069-155">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="86069-157">а.</span><span class="sxs-lookup"><span data-stu-id="86069-157">a.</span></span> <span data-ttu-id="86069-158">В hello **идентификатор** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="86069-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>

    |    <span data-ttu-id="86069-159">Среда</span><span class="sxs-lookup"><span data-stu-id="86069-159">Environment</span></span>      |       <span data-ttu-id="86069-160">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="86069-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="86069-161">Для "Five9 Plus Adapter for Microsoft Dynamics CRM"</span><span class="sxs-lookup"><span data-stu-id="86069-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="86069-162">Для "Five9 Plus Adapter for Zendesk"</span><span class="sxs-lookup"><span data-stu-id="86069-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="86069-163">Для "Five9 Plus Adapter for Agent Desktop Toolkit"</span><span class="sxs-lookup"><span data-stu-id="86069-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="86069-164">b.</span><span class="sxs-lookup"><span data-stu-id="86069-164">b.</span></span> <span data-ttu-id="86069-165">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="86069-165">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    |      <span data-ttu-id="86069-166">Среда</span><span class="sxs-lookup"><span data-stu-id="86069-166">Environment</span></span>     |      <span data-ttu-id="86069-167">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="86069-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="86069-168">Для "Five9 Plus Adapter for Microsoft Dynamics CRM"</span><span class="sxs-lookup"><span data-stu-id="86069-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="86069-169">Для "Five9 Plus Adapter for Zendesk"</span><span class="sxs-lookup"><span data-stu-id="86069-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="86069-170">Для "Five9 Plus Adapter for Agent Desktop Toolkit"</span><span class="sxs-lookup"><span data-stu-id="86069-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="86069-171">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="86069-171">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="86069-173">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="86069-173">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="86069-175">На hello **конфигурация Five9 адаптера, а также (CTI, агенты Center контакт)** щелкните **Настройка Five9 плюс адаптера (CTI, агенты Center контакт)** tooopen **Настройкавхода** окна.</span><span class="sxs-lookup"><span data-stu-id="86069-175">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="86069-176">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="86069-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="86069-178">tooconfigure единого входа на **Five9 адаптера, а также (CTI, агенты Center контакт)** стороны, необходимо загрузить hello toosend **Certificate(Base64), URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[Five9 Plus (CTI, агенты Center контакт) поддержка адаптеров](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="86069-178">tooconfigure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="86069-179">Также Кроме того, для дальнейшей настройки единого входа выполните hello toohello адаптера в соответствии с шаги, описанные ниже.</span><span class="sxs-lookup"><span data-stu-id="86069-179">Also additionally, for configuring SSO further please follow hello below steps according toohello adapter:</span></span>

    <span data-ttu-id="86069-180">а.</span><span class="sxs-lookup"><span data-stu-id="86069-180">a.</span></span> <span data-ttu-id="86069-181">Руководство администратора "Five9 Plus Adapter for Agent Desktop Toolkit": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="86069-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="86069-182">b.</span><span class="sxs-lookup"><span data-stu-id="86069-182">b.</span></span> <span data-ttu-id="86069-183">Руководство администратора "Five9 Plus Adapter for Microsoft Dynamics CRM": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="86069-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="86069-184">c.</span><span class="sxs-lookup"><span data-stu-id="86069-184">c.</span></span> <span data-ttu-id="86069-185">Руководство администратора "Five9 Plus Adapter for Zendesk": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="86069-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="86069-186">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="86069-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="86069-187">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="86069-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="86069-188">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86069-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="86069-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="86069-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="86069-190">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="86069-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="86069-192">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="86069-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="86069-193">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="86069-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86069-195">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="86069-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86069-197">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="86069-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86069-199">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="86069-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86069-201">а.</span><span class="sxs-lookup"><span data-stu-id="86069-201">a.</span></span> <span data-ttu-id="86069-202">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86069-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86069-203">b.</span><span class="sxs-lookup"><span data-stu-id="86069-203">b.</span></span> <span data-ttu-id="86069-204">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="86069-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86069-205">c.</span><span class="sxs-lookup"><span data-stu-id="86069-205">c.</span></span> <span data-ttu-id="86069-206">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="86069-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="86069-207">d.</span><span class="sxs-lookup"><span data-stu-id="86069-207">d.</span></span> <span data-ttu-id="86069-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="86069-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="86069-209">Создание тестового пользователя Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="86069-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="86069-210">В этом разделе вы создадите тестового пользователя по имени Britta Simon в Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="86069-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="86069-211">Работать с [Five9 Plus (CTI, агенты Center контакт) поддержка адаптеров](https://www.five9.com/about/contact) для добавления пользователей hello в платформе hello Five9 адаптера, а также (контакт Center агентов, CTI).</span><span class="sxs-lookup"><span data-stu-id="86069-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add hello users in hello Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="86069-212">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="86069-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="86069-213">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="86069-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="86069-214">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooFive9 плюс адаптера (контакт Center агентов, CTI).</span><span class="sxs-lookup"><span data-stu-id="86069-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFive9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="86069-216">**tooassign Britta Simon tooFive9 плюс адаптера (CTI, обратитесь в службу центра агенты), выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="86069-216">**tooassign Britta Simon tooFive9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="86069-217">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="86069-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="86069-219">В списке приложений hello выберите **Five9 адаптера, а также (CTI, агенты Center контакт)**.</span><span class="sxs-lookup"><span data-stu-id="86069-219">In hello applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="86069-221">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="86069-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="86069-223">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="86069-223">Click **Add** button.</span></span> <span data-ttu-id="86069-224">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="86069-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="86069-226">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="86069-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="86069-227">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="86069-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86069-228">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="86069-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="86069-229">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="86069-229">Testing single sign-on</span></span>

<span data-ttu-id="86069-230">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="86069-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="86069-231">При нажатии кнопки hello Five9 адаптера, а также (контакт Center агентов, CTI) плитки в панели доступа hello, вы должны получить приложения автоматически вошедшего tooyour Five9 адаптера, а также (контакт Center агентов, CTI).</span><span class="sxs-lookup"><span data-stu-id="86069-231">When you click hello Five9 Plus Adapter (CTI, Contact Center Agents) tile in hello Access Panel, you should get automatically signed-on tooyour Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="86069-232">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="86069-232">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86069-233">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="86069-233">Additional resources</span></span>

* [<span data-ttu-id="86069-234">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86069-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86069-235">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="86069-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

