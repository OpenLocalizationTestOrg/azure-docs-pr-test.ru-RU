---
title: "Руководство по интеграции Azure Active Directory с решением SilkRoad Life Suite | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SilkRoad жизни набора."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="2e160-103">Руководство по интеграции Azure Active Directory с решением SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="2e160-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="2e160-104">Hello цель этого учебника — tooshow вы как toointegrate SilkRoad жизни набора с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e160-104">hello objective of this tutorial is tooshow you how toointegrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="2e160-105">Интеграция с Azure AD SilkRoad жизни Suite предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="2e160-105">Integrating SilkRoad Life Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="2e160-106">Можно управлять в Azure AD, имеющего доступ tooSilkRoad жизни набора</span><span class="sxs-lookup"><span data-stu-id="2e160-106">You can control in Azure AD who has access tooSilkRoad Life Suite</span></span> 
* <span data-ttu-id="2e160-107">Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooSilkRoad жизни набора единого входа (SSO)</span><span class="sxs-lookup"><span data-stu-id="2e160-107">You can enable your users tooautomatically get signed-on tooSilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="2e160-108">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e160-108">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e160-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2e160-109">Prerequisites</span></span>
<span data-ttu-id="2e160-110">tooconfigure интеграция Azure AD с SilkRoad жизни набора необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="2e160-110">tooconfigure Azure AD integration with SilkRoad Life Suite, you need hello following items:</span></span>

* <span data-ttu-id="2e160-111">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="2e160-111">An Azure AD subscription</span></span>
* <span data-ttu-id="2e160-112">подписка SilkRoad Life Suite с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="2e160-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="2e160-113">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="2e160-113">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="2e160-114">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="2e160-114">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="2e160-115">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="2e160-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="2e160-116">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e160-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="2e160-117">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="2e160-117">Scenario Description</span></span>
<span data-ttu-id="2e160-118">Hello цель этого учебника — tooenable вы tootest единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="2e160-118">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="2e160-119">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="2e160-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e160-120">Добавление SilkRoad жизни набора из галереи hello</span><span class="sxs-lookup"><span data-stu-id="2e160-120">Adding SilkRoad Life Suite from hello gallery</span></span> 
2. <span data-ttu-id="2e160-121">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e160-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-hello-gallery"></a><span data-ttu-id="2e160-122">Добавьте набор жизни SilkRoad из галереи hello</span><span class="sxs-lookup"><span data-stu-id="2e160-122">Add SilkRoad Life Suite from hello gallery</span></span>
<span data-ttu-id="2e160-123">tooconfigure hello интеграция SilkRoad жизни набора в Azure AD, вы должны tooadd SilkRoad жизни набора из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="2e160-123">tooconfigure hello integration of SilkRoad Life Suite into Azure AD, you need tooadd SilkRoad Life Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2e160-124">**tooadd SilkRoad жизни набора из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2e160-124">**tooadd SilkRoad Life Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e160-125">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e160-125">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="2e160-127">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="2e160-127">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="2e160-128">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="2e160-128">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Приложения][2]

4. <span data-ttu-id="2e160-130">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="2e160-130">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Приложения][3]

5. <span data-ttu-id="2e160-132">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="2e160-132">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Приложения][4]

6. <span data-ttu-id="2e160-134">Введите в поле поиска hello **SilkRoad жизни набора**.</span><span class="sxs-lookup"><span data-stu-id="2e160-134">In hello search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Приложения][5]

7. <span data-ttu-id="2e160-136">В области результатов hello выберите **SilkRoad жизни набора**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2e160-136">In hello results pane, select **SilkRoad Life Suite**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Приложения][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2e160-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e160-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2e160-139">Цель этого раздела Hello является tooshow как tooconfigure и Azure AD SSO с SilkRoad жизни набора тестов на основе тестового пользователя с именем «Britta Simon».</span><span class="sxs-lookup"><span data-stu-id="2e160-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e160-140">Для toowork единого входа Azure AD необходима tooknow пользователь аналог какие hello в жизни набора SilkRoad tooan пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e160-140">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SilkRoad Life Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="2e160-141">Другими словами связи между пользователя Azure AD и связанных пользователей hello в наборе SilkRoad жизни должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="2e160-141">In other words, a link relationship between an Azure AD user and hello related user in SilkRoad Life Suite needs toobe established.</span></span>

<span data-ttu-id="2e160-142">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** SilkRoad жизни набора.</span><span class="sxs-lookup"><span data-stu-id="2e160-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="2e160-143">tooconfigure и теста Azure AD единого входа с SilkRoad жизни набора, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="2e160-143">tooconfigure and test Azure AD single sign-on with SilkRoad Life Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2e160-144">**[Настройка Azure AD единого входа](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="2e160-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2e160-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="2e160-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e160-146">**[Создание тестового пользователя Suite жизни SilkRoad](#creating-a-silkroad-life-suite-test-user)**  -toohave аналог Саймон Britta в наборе SilkRoad жизни, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="2e160-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - toohave a counterpart of Britta Simon in SilkRoad Life Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="2e160-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="2e160-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e160-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2e160-148">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2e160-149">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e160-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="2e160-150">Цель этого раздела Hello — tooenable единого входа Azure AD в hello классический портал Azure и tooconfigure единого входа в приложении SilkRoad жизни набора.</span><span class="sxs-lookup"><span data-stu-id="2e160-150">hello objective of this section is tooenable Azure AD SSO in hello Azure classic portal and tooconfigure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="2e160-151">**tooconfigure Azure AD единого входа с набором SilkRoad жизни, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2e160-151">**tooconfigure Azure AD single sign-on with SilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e160-152">Корпоративный сайт SilkRoad tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="2e160-152">Sign-on tooyour SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="2e160-153">toohello tooobtain доступа приложения проверки подлинности Suite жизни SilkRoad по настройке федерации с Microsoft Azure AD, обратитесь в службу поддержки SilkRoad либо с Вашим представителем службы SilkRoad.</span><span class="sxs-lookup"><span data-stu-id="2e160-153">tooobtain access toohello SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="2e160-154">Go слишком**поставщика услуг**и нажмите кнопку **сведения федерации**.</span><span class="sxs-lookup"><span data-stu-id="2e160-154">Go too**Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Единый вход в Azure AD][10] 

3. <span data-ttu-id="2e160-156">Нажмите кнопку **загрузить метаданные федерации**, а затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="2e160-156">Click **Download Federation Metadata**, and then save hello metadata file on your computer.</span></span>
   
    ![Единый вход в Azure AD][11] 

4. <span data-ttu-id="2e160-158">В классический портал Azure, на hello hello **SilkRoad жизни набора** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**  диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="2e160-158">In hello Azure classic portal, on hello **SilkRoad Life Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Настройка единого входа][6] 

5. <span data-ttu-id="2e160-160">На hello **предпочитаемый как toosign пользователей на tooSilkRoad жизни набора** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e160-160">On hello **How would you like users toosign on tooSilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Единый вход в Azure AD][7] 

6. <span data-ttu-id="2e160-162">На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2e160-162">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Единый вход в Azure AD][8]   
 1. <span data-ttu-id="2e160-164">В hello **на URL-адрес входа** textbox hello введите URL-адрес, используемые на сайте SilkRoad жизни набора tooyour toosign на пользователей (например: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="2e160-164">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="2e160-165">Откройте hello загружены **Silkroad** файла метаданных.</span><span class="sxs-lookup"><span data-stu-id="2e160-165">Open hello downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="2e160-166">Найдите hello **AssertionConsumerService** тега, а затем копировать hello **расположение** атрибута.</span><span class="sxs-lookup"><span data-stu-id="2e160-166">Locate hello **AssertionConsumerService** tag, and then copy hello **Location** attribute.</span></span>         
   
    ![Единый вход в Azure AD][21] 
 4. <span data-ttu-id="2e160-168">Вставьте значение hello в hello **URL-адрес ответа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="2e160-168">Paste hello value into hello **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="2e160-169">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e160-169">Click **Next**.</span></span>

6. <span data-ttu-id="2e160-170">На hello **настроить единый вход в жизни набора SilkRoad** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2e160-170">On hello **Configure single sign-on at SilkRoad Life Suite** page, perform hello following steps:</span></span>
   
    ![Единый вход в Azure AD][9]  
 1. <span data-ttu-id="2e160-172">Нажмите кнопку загрузки сертификата, а затем сохраните файл hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="2e160-172">Click Download certificate, and then save hello file on your computer.</span></span>  
 2. <span data-ttu-id="2e160-173">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e160-173">Click **Next**.</span></span>

7. <span data-ttu-id="2e160-174">В приложении **SilkRoad** щелкните **Authentication Sources** (Источники проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="2e160-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![единого входа Azure AD][12] 

8. <span data-ttu-id="2e160-176">Щелкните **Add Authentication Source**(Добавить источник аутентификации).</span><span class="sxs-lookup"><span data-stu-id="2e160-176">Click **Add Authentication Source**.</span></span> 
   
    ![Единый вход в Azure AD][13] 

9. <span data-ttu-id="2e160-178">В hello **добавить источник проверки подлинности** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2e160-178">In hello **Add Authentication Source** section, perform hello following steps:</span></span> 
   
    ![Единый вход в Azure AD][14]  
 1. <span data-ttu-id="2e160-180">В разделе **вариант 2 - файл метаданных**, нажмите кнопку **Обзор** tooupload hello скачать файл метаданных.</span><span class="sxs-lookup"><span data-stu-id="2e160-180">Under **Option 2 - Metadata File**, click **Browse** tooupload hello downloaded metadata file.</span></span>  
 2. <span data-ttu-id="2e160-181">Нажмите кнопку **Создать поставщик удостоверений с помощью данных из файла**.</span><span class="sxs-lookup"><span data-stu-id="2e160-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="2e160-182">В hello **источники проверки подлинности** щелкните **изменить**.</span><span class="sxs-lookup"><span data-stu-id="2e160-182">In hello **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Единый вход в Azure AD][15] 

11. <span data-ttu-id="2e160-184">На hello **изменение проверки подлинности источника** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2e160-184">On hello **Edit Authentication Source** dialog, perform hello following steps:</span></span> 
    
     ![Единый вход в Azure AD][16] 
 1. <span data-ttu-id="2e160-186">В поле **Enabled** (Включено) выберите **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="2e160-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="2e160-187">В hello **описание поставщика удостоверений** в текстовое поле введите описание для конфигурации (например: *единого входа Azure AD*).</span><span class="sxs-lookup"><span data-stu-id="2e160-187">In hello **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="2e160-188">В hello **имя поставщика удостоверений** текстовом поле введите имя, которое является tooyour определенной конфигурации (например: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="2e160-188">In hello **IdP Name** textbox, type a name that is specific tooyour configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="2e160-189">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2e160-189">Click **Save**.</span></span>

12. <span data-ttu-id="2e160-190">Отключите все остальные источники аутентификации.</span><span class="sxs-lookup"><span data-stu-id="2e160-190">Disable all other authentication sources.</span></span> 
    
     ![Единый вход в Azure AD][17]

13. <span data-ttu-id="2e160-192">В классический портал Azure, на hello hello **единого входа для подтверждения** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e160-192">In hello Azure classic portal, on hello **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Единый вход в Azure AD][18]

14. <span data-ttu-id="2e160-194">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="2e160-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Единый вход в Azure AD][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2e160-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e160-196">Create an Azure AD test user</span></span>
<span data-ttu-id="2e160-197">Цель этого раздела Hello — toocreate тестового пользователя в классический портал Azure, вызывается Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="2e160-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][20]

<span data-ttu-id="2e160-199">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2e160-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e160-200">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e160-200">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="2e160-202">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="2e160-202">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="2e160-203">Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2e160-203">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e160-205">tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="2e160-205">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="2e160-207">На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2e160-207">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="2e160-209">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="2e160-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="2e160-210">В имени пользователя hello **textbox**, тип **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e160-210">In hello User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="2e160-211">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e160-211">Click **Next**.</span></span>

6. <span data-ttu-id="2e160-212">На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2e160-212">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="2e160-214">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2e160-214">In hello **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="2e160-215">В hello **Фамилия** текстовое поле, тип, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2e160-215">In hello **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="2e160-216">В hello **отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2e160-216">In hello **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="2e160-217">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="2e160-217">In hello **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="2e160-218">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e160-218">Click **Next**.</span></span>

7. <span data-ttu-id="2e160-219">На hello **получение временного пароля** странице диалогового окна щелкните **создания**.</span><span class="sxs-lookup"><span data-stu-id="2e160-219">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="2e160-221">На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2e160-221">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="2e160-223">Запишите значение hello hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="2e160-223">Write down hello value of hello **New Password**.</span></span> 
 2. <span data-ttu-id="2e160-224">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="2e160-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="2e160-225">Создание тестового пользователя SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="2e160-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="2e160-226">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon SilkRoad жизни набора.</span><span class="sxs-lookup"><span data-stu-id="2e160-226">hello objective of this section is toocreate a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="2e160-227">Britta должен иметь идентификатор единого входа (иногда называется tooas *AuthParam*), соответствующий элемента Britta **emailaddress** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e160-227">Britta's must have an SSO ID (sometimes referred tooas an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="2e160-228">**toocreate пользователя с именем Britta Simon SilkRoad жизни пакета, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2e160-228">**toocreate a user called Britta Simon in SilkRoad Life Suite, perform hello following steps:**</span></span>

- <span data-ttu-id="2e160-229">Попросите пользователя с теми, что вашей toocreate team Suite жизни SilkRoad поддержки **код SSO** hello атрибута совпадает со значением в hello **emailaddress** из Britta Simon в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e160-229">Ask your SilkRoad Life Suite support team toocreate a user that has as **SSO ID** attribute hello same value as hello **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2e160-230">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="2e160-230">Assign hello Azure AD test user</span></span>
<span data-ttu-id="2e160-231">Hello цель этого раздела — tooenable toouse Britta Simon единого входа в Azure, предоставляя свой доступ tooSilkRoad жизни набора.</span><span class="sxs-lookup"><span data-stu-id="2e160-231">hello objective of this section is tooenable Britta Simon toouse Azure SSO by granting her access tooSilkRoad Life Suite.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="2e160-233">**tooassign tooSilkRoad Britta Simon Suite жизни выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="2e160-233">**tooassign Britta Simon tooSilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e160-234">Hello Azure представления приложения hello tooopen в представлении каталога hello классического портала щелкните **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="2e160-234">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Назначение пользователя][201] 

2. <span data-ttu-id="2e160-236">В списке приложений hello выберите **SilkRoad жизни набора**.</span><span class="sxs-lookup"><span data-stu-id="2e160-236">In hello applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Назначение пользователя][202] 

3. <span data-ttu-id="2e160-238">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2e160-238">In hello menu on hello top, click **Users**.</span></span>
   
    ![Назначение пользователя][203] 

4. <span data-ttu-id="2e160-240">В списке пользователей hello выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2e160-240">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="2e160-241">В нижней hello hello инструментов, нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="2e160-241">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Назначение пользователя][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="2e160-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="2e160-243">Test single sign-on</span></span>
<span data-ttu-id="2e160-244">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="2e160-244">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="2e160-245">При выборе плитки SilkRoad жизни набора hello в hello панели доступа, вы должны получить tooyour автоматически вошедшего Suite SilkRoad жизни приложения.</span><span class="sxs-lookup"><span data-stu-id="2e160-245">When you click hello SilkRoad Life Suite tile in hello Access Panel, you should get automatically signed-on tooyour SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2e160-246">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2e160-246">Additional Resources</span></span>
* [<span data-ttu-id="2e160-247">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e160-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e160-248">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2e160-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





