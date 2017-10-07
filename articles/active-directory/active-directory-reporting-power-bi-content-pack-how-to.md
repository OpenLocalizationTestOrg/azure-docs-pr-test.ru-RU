---
title: "aaaHow toouse hello Azure Active Directory пакет содержимого Power BI | Документы Microsoft"
description: "Узнайте, как toouse hello Azure Active Directory пакет содержимого Power BI"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a><span data-ttu-id="ff02f-103">Как toouse hello Azure Active Directory пакет содержимого Power BI</span><span class="sxs-lookup"><span data-stu-id="ff02f-103">How toouse hello Azure Active Directory Power BI Content Pack</span></span>

<span data-ttu-id="ff02f-104">Вам, как ИТ-администратору, важно знать, как ваши пользователи внедряют и используют возможности Azure Active Directory. Она позволяет tooplan tooincrease использования ИТ инфраструктуры и обмен данными и tooget hello наиболее эффективно использовать возможности AAD.</span><span class="sxs-lookup"><span data-stu-id="ff02f-104">Understanding how your users adopt and use Azure Active Directory features is critical for you as an IT admin. It allows you tooplan your IT infrastructure and communication tooincrease usage and tooget hello most out of AAD features.</span></span> <span data-ttu-id="ff02f-105">Содержимое Power BI пакет для Azure Active Directory предоставляет hello toofurther возможность анализировать вашей toounderstand данные об использовании этого данных toogather всестороннее анализировать происходящем с их Azure Active Directory для hello различные функциональные возможности вы активно используют.</span><span class="sxs-lookup"><span data-stu-id="ff02f-105">Power BI Content Pack for Azure Active Directory gives you hello ability toofurther analyze your data toounderstand how you can use this data toogather richer insights into what’s going on with their Azure Active Directory for hello various capabilities you heavily rely on.</span></span>  <span data-ttu-id="ff02f-106">С hello интеграции Azure Active Directory, интерфейсы API в Power BI можно легко загрузить hello готовые пакеты содержимого и анализировать действия tooall hello в Azure Active Directory с помощью Power BI предлагает широкие возможности визуализации опытом.</span><span class="sxs-lookup"><span data-stu-id="ff02f-106">With hello integration of Azure Active Directory APIs into Power BI, you can easily download hello pre-built content packs and gain insights tooall hello activities within your Azure Active Directory using rich visualization experience Power BI offers.</span></span> <span data-ttu-id="ff02f-107">Вы можете создавать собственные панели мониторинга и легко предоставлять к ним доступ любому пользователю в организации.</span><span class="sxs-lookup"><span data-stu-id="ff02f-107">You can create your own dashboard and share it easily with anyone in your organization.</span></span> 

<span data-ttu-id="ff02f-108">Этот раздел содержит пошаговые инструкции по hello как tooinstall и использования содержимого пакета в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="ff02f-108">This topic provides you with step-by-step instructions on how tooinstall and use hello content pack in your environment.</span></span>

## <a name="installation"></a><span data-ttu-id="ff02f-109">Установка</span><span class="sxs-lookup"><span data-stu-id="ff02f-109">Installation</span></span>  

<span data-ttu-id="ff02f-110">**hello tooinstall пакет содержимого Power BI:**</span><span class="sxs-lookup"><span data-stu-id="ff02f-110">**tooinstall hello Power BI Content Pack:**</span></span>

1. <span data-ttu-id="ff02f-111">Войдите на [Power BI](https://app.powerbi.com/groups/me/getdata/services) с вашей учетной записью Power BI (это hello учетной записью вашей учетной записи Azure AD или Office 365).</span><span class="sxs-lookup"><span data-stu-id="ff02f-111">Log into [Power BI](https://app.powerbi.com/groups/me/getdata/services) with your Power BI Account (this is hello same account as your O365 or Azure AD Account).</span></span>

2. <span data-ttu-id="ff02f-112">Hello нижней части панели навигации слева hello, выберите **получение данных**.</span><span class="sxs-lookup"><span data-stu-id="ff02f-112">At hello bottom of hello left navigation pane, select **Get Data**.</span></span>

    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. <span data-ttu-id="ff02f-114">В hello **службы** щелкните **получить**.</span><span class="sxs-lookup"><span data-stu-id="ff02f-114">In hello **Services** box, click **Get**.</span></span>
   
    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  <span data-ttu-id="ff02f-116">Выполните поиск по запросу **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff02f-116">Search for **Azure Active Directory**.</span></span>

    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  <span data-ttu-id="ff02f-118">При появлении запроса введите свой идентификатор клиента Azure AD и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ff02f-118">When prompted, type your Azure AD Tenant ID, and then click **Next**.</span></span>

    > [!TIP] 
    > <span data-ttu-id="ff02f-119">Hello tooget быстро ИД клиента для вашего клиента Office 365 или Azure AD — toologin toohello портала Azure AD, детализация углублением toohello каталог и скопируйте идентификатор hello из hello URL-адреса: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ ActiveDirectoryExtension иликаталога/<tenantid>/directoryQuickStart</span><span class="sxs-lookup"><span data-stu-id="ff02f-119">A quick way tooget hello Tenant Id for your Office 365 / Azure AD tenant is toologin toohello Azure AD Portal, drill down toohello directory and copy hello ID from hello following URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span></span>

    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  <span data-ttu-id="ff02f-121">Нажмите кнопку **Войти**.</span><span class="sxs-lookup"><span data-stu-id="ff02f-121">Click **Sign-in**.</span></span> 
 
    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  <span data-ttu-id="ff02f-123">Введите имя пользователя и пароль, а затем нажмите кнопку **Войти**.</span><span class="sxs-lookup"><span data-stu-id="ff02f-123">Enter your username and password, and then click **Sign in**.</span></span>
 
    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  <span data-ttu-id="ff02f-125">В диалоговом окне согласия приложения hello, нажмите кнопку **Accept**.</span><span class="sxs-lookup"><span data-stu-id="ff02f-125">On hello app consent dialog, click **Accept**.</span></span>
 
9.  <span data-ttu-id="ff02f-126">Когда панель мониторинга журналов действий Active Directory Azure будет создана, щелкните ее.</span><span class="sxs-lookup"><span data-stu-id="ff02f-126">When your Azure Active Directory Activity logs dashboard has been created, click it.</span></span>
 
    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a><span data-ttu-id="ff02f-128">Что можно сделать с помощью этого пакета содержимого?</span><span class="sxs-lookup"><span data-stu-id="ff02f-128">What can I do with this content pack?</span></span>

<span data-ttu-id="ff02f-129">Прежде чем мы зайдем в возможностях этого пакета содержимого, Вот краткий обзор hello различных отчетов hello содержимого пакета.</span><span class="sxs-lookup"><span data-stu-id="ff02f-129">Before we jump into what you can do with this content pack, here’s quick preview of hello various reports in hello content pack.</span></span> <span data-ttu-id="ff02f-130">Отчет данных возвращается toohello **последние 30 дней**.</span><span class="sxs-lookup"><span data-stu-id="ff02f-130">Report data goes back toohello **last 30 days**.</span></span>

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a><span data-ttu-id="ff02f-131">Отчеты, включенные в эту версию пакета содержимого журналов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff02f-131">Reports included in this version of Azure Active Directory logs Content Pack</span></span>

<span data-ttu-id="ff02f-132">**Отчет об использовании приложения и тенденции**: анализ приложения hello, используемых в вашей организации и какие из них используются наиболее hello и когда.</span><span class="sxs-lookup"><span data-stu-id="ff02f-132">**App Usage and Trend report**:  Get insights into hello apps used in your organization and which ones are being used hello most and when.</span></span> <span data-ttu-id="ff02f-133">Можно использовать этот отчет toogather ценную информацию об использовании приложения, которые вы недавно распространен в вашей организации или узнать, какие приложения часто используются.</span><span class="sxs-lookup"><span data-stu-id="ff02f-133">You can use this report toogather insights into how an app you recently rolled out in your organization is being used or find out which apps are popular.</span></span> <span data-ttu-id="ff02f-134">Таким образом, можно улучшить использование, если вы видите, если приложение hello не используется.</span><span class="sxs-lookup"><span data-stu-id="ff02f-134">By doing this, you can improve usage if you see if hello app is not being used.</span></span>

<span data-ttu-id="ff02f-135">**Войти в систему пользователями и расположение**: понять все hello входов выполняется с использованием удостоверения Azure и позволяет анализировать hello удостоверения пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ff02f-135">**Sign-ins by location and users**: Get insights into all hello sign-ins performed using Azure Identity and gives insights into hello identity of hello users.</span></span> <span data-ttu-id="ff02f-136">Из этого отчета вы можете получить более подробную информацию об отдельных входах и ответить на следующие вопросы.</span><span class="sxs-lookup"><span data-stu-id="ff02f-136">With this, you can dig deeper into individual sign-ins and answer questions like:</span></span>

- <span data-ttu-id="ff02f-137">Откуда этот пользователь входит в систему?</span><span class="sxs-lookup"><span data-stu-id="ff02f-137">From where did this user sign-ins?</span></span>
- <span data-ttu-id="ff02f-138">Какие пользователя hello большинство входа в систему и где они вход из?</span><span class="sxs-lookup"><span data-stu-id="ff02f-138">Which user has hello most sign-ins and where do they sign-in from?</span></span> 
- <span data-ttu-id="ff02f-139">Успешно войти hello?</span><span class="sxs-lookup"><span data-stu-id="ff02f-139">Was hello sign-in successful?</span></span>  
 
<span data-ttu-id="ff02f-140">Чтобы просмотреть подробные сведения, щелкните определенную дату или расположение.</span><span class="sxs-lookup"><span data-stu-id="ff02f-140">You can drill into details by clicking on a specific date or location.</span></span>

<span data-ttu-id="ff02f-141">**Число уникальных пользователей на каждое приложение.** Узнайте обо всех уникальных пользователях, использующих определенное приложение.</span><span class="sxs-lookup"><span data-stu-id="ff02f-141">**Unique users per app**:  Get a view of all unique users using a given app.</span></span> <span data-ttu-id="ff02f-142">Этот отчет включает только пользователей, которые *успешно* вошли в приложение.</span><span class="sxs-lookup"><span data-stu-id="ff02f-142">This includes only users who have “*successfully*” signed into an application.</span></span>

<span data-ttu-id="ff02f-143">**Войти в систему устройства**: получить представление о hello тип операционной системы и браузеры используются пользователями в организации с подробными сведениями с пользователями hello, включая:</span><span class="sxs-lookup"><span data-stu-id="ff02f-143">**Device sign-ins**: Get a view of hello type of OS and browsers are being used by users in your organization with detailed information on hello users including:</span></span>

- <span data-ttu-id="ff02f-144">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="ff02f-144">User Name</span></span>
- <span data-ttu-id="ff02f-145">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="ff02f-145">IP Address</span></span>
- <span data-ttu-id="ff02f-146">Расположение</span><span class="sxs-lookup"><span data-stu-id="ff02f-146">Location</span></span> 
- <span data-ttu-id="ff02f-147">состояние входа.</span><span class="sxs-lookup"><span data-stu-id="ff02f-147">Sign-in status</span></span> 

<span data-ttu-id="ff02f-148">В этом отчете вы понимаете hello различные профили устройство используется в вашей организации и определить политики устройств, в зависимости от используемой</span><span class="sxs-lookup"><span data-stu-id="ff02f-148">With this report, you can understand hello various device profiles used within your organization and determine device policies based on what’s used</span></span>

<span data-ttu-id="ff02f-149">**Воронка SSPR.** Узнайте, как в вашей организации используется функция сброса пароля.</span><span class="sxs-lookup"><span data-stu-id="ff02f-149">**SSPR Funnel**: Get an understanding on how password resets are being done in your organization.</span></span> <span data-ttu-id="ff02f-150">Взгляните на сколько пароль сбрасывает была предпринята попытка через средство SSPR hello и сколько из них выполнены успешно.</span><span class="sxs-lookup"><span data-stu-id="ff02f-150">Get a peek into how many password resets were attempted through hello SSPR tool and how many of them were successful.</span></span> <span data-ttu-id="ff02f-151">Глубже изучить сбоя сбрасывает пароль hello, с помощью SSPR воронкообразной hello и понять, почему произошел определенных ошибок.</span><span class="sxs-lookup"><span data-stu-id="ff02f-151">Dig deeper into hello Password resets failure using hello SSPR funnel and understand why certain failures occurred.</span></span> <span data-ttu-id="ff02f-152">Этот отчет содержит более глубокого понимания hello SSPR средство использования вашей организации, можно принять правильные решения hello.</span><span class="sxs-lookup"><span data-stu-id="ff02f-152">This report gives a deeper understanding of how hello SSPR tool is used within your organization so you can make hello right decisions.</span></span>

## <a name="customizing-azure-ad-activity-content-pack"></a><span data-ttu-id="ff02f-153">Настройка пакета содержимого действий Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff02f-153">Customizing Azure AD Activity content pack</span></span>

<span data-ttu-id="ff02f-154">**Измените визуализацию**: визуализации отчетов можно изменить, щелкнув **редактировать отчет** и выберите визуализацию hello требуется.</span><span class="sxs-lookup"><span data-stu-id="ff02f-154">**Change Visualization**:  You can change a report visualization by clicking **Edit Report** and select hello visualization you want.</span></span>
 
![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

<span data-ttu-id="ff02f-157">**Включить дополнительные поля**: можно добавить отчет toohello поля или удалите его, выбрав hello visual toowhich tooadd или удалить поле hello.</span><span class="sxs-lookup"><span data-stu-id="ff02f-157">**Include additional fields**:  You can add a field toohello report or remove it by selecting hello visual toowhich you want tooadd/remove hello field.</span></span> <span data-ttu-id="ff02f-158">В следующем примере hello я добавляю представление таблицы toohello поле «состояние».</span><span class="sxs-lookup"><span data-stu-id="ff02f-158">In hello example below, I am adding “sign-in status” field toohello table view.</span></span> 
 
![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

<span data-ttu-id="ff02f-160">**Панель мониторинга tooyour визуализации ПИН-код**: можно настроить информационную панель и включить отчету toohello визуализации и закрепите его toohello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ff02f-160">**Pin visualizations tooyour dashboard**:  You can customize your dashboard and include your own visualizations toohello report and pin it toohello dashboard.</span></span> <span data-ttu-id="ff02f-161">В следующем примере hello добавлен новый фильтр, который называется «состояние» и его включения в отчет hello.</span><span class="sxs-lookup"><span data-stu-id="ff02f-161">In hello example below, I added a new filter called “Sign-in Status” and included it in hello report.</span></span> <span data-ttu-id="ff02f-162">Также заменяли линейчатой диаграммы tooa график визуализации hello и можно закрепить этой панели мониторинга visual toohello.</span><span class="sxs-lookup"><span data-stu-id="ff02f-162">I also changed hello visualization from bar chart tooa line chart and can pin this new visual toohello dashboard.</span></span>

![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


<span data-ttu-id="ff02f-165">**Общий доступ к панели мониторинга**: после создания hello содержимого можно предоставить мониторинга hello hello пользователи в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="ff02f-165">**Sharing your dashboard**: Once you have created hello content you want, you can share hello dashboard with hello users in your organization.</span></span> <span data-ttu-id="ff02f-166">Обратите внимание, что после отправки отчета hello, они могут просматривать hello полей, выбранных в отчете hello.</span><span class="sxs-lookup"><span data-stu-id="ff02f-166">Please remember that once you share hello report, they can see hello fields you have selected in hello report.</span></span>
 
![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a><span data-ttu-id="ff02f-168">Планирование ежедневного обновления отчета Power BI</span><span class="sxs-lookup"><span data-stu-id="ff02f-168">Scheduling a daily refresh of your Power BI report</span></span>

<span data-ttu-id="ff02f-169">tooschedule ежедневного обновления отчета Power BI, перейдите в слишком**наборы данных > Параметры > расписание обновлений** и задайте его, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ff02f-169">tooschedule a daily refresh of your Power BI report, go too**Datasets > Settings > Schedule Refresh** and set it as shown below.</span></span>
 
![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a><span data-ttu-id="ff02f-171">Обновление версии toonewer содержимого пакета</span><span class="sxs-lookup"><span data-stu-id="ff02f-171">Updating toonewer version of content pack</span></span>

<span data-ttu-id="ff02f-172">Если требуется, чтобы tooupdate содержимое пакета tooget более новой версии:</span><span class="sxs-lookup"><span data-stu-id="ff02f-172">If you want tooupdate your content pack tooget a newer version:</span></span>

- <span data-ttu-id="ff02f-173">Загрузите новый пакет содержимого hello и настройте его согласно инструкциям, приведенным в статье.</span><span class="sxs-lookup"><span data-stu-id="ff02f-173">Download hello new content pack and set it up as per instructions listed in this article.</span></span>

- <span data-ttu-id="ff02f-174">После настройки его, перейдите в слишком**источник данных > Параметры > учетные данные источника данных** и повторно введите учетные данные, как показано ниже</span><span class="sxs-lookup"><span data-stu-id="ff02f-174">Once you have set it up, go too**Data Source > Settings > Data source credentials** and re-enter your credentials as shown below</span></span>

    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

<span data-ttu-id="ff02f-176">Как только новая версия пакета содержимого hello hello работает, при необходимости, удалив hello Базовые отчеты и наборы данных, связанные с этим пакетом содержимого можно удалить старую версию hello.</span><span class="sxs-lookup"><span data-stu-id="ff02f-176">As soon as hello new version of hello content pack is working, you can remove hello old version if needed by deleting hello underlying reports and datasets associated with that content pack.</span></span>

## <a name="still-having-issues"></a><span data-ttu-id="ff02f-177">Возникли проблемы?</span><span class="sxs-lookup"><span data-stu-id="ff02f-177">Still having issues?</span></span> 

<span data-ttu-id="ff02f-178">См. [руководство по устранению неполадок](active-directory-reporting-troubleshoot-content-pack.md).</span><span class="sxs-lookup"><span data-stu-id="ff02f-178">Check out our [troubleshooting guide](active-directory-reporting-troubleshoot-content-pack.md).</span></span> <span data-ttu-id="ff02f-179">Общие сведения о Power BI см. в [справочных статьях](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span><span class="sxs-lookup"><span data-stu-id="ff02f-179">For general help with Power BI, check out these [help articles](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span></span>
 

## <a name="next-steps"></a><span data-ttu-id="ff02f-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ff02f-180">Next steps</span></span>

<span data-ttu-id="ff02f-181">Обзор отчетов см. в разделе hello [отчетов Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ff02f-181">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
