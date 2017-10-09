---
title: "aaaAzure Mobile Engagement пользовательского интерфейса: сегменты"
description: "Узнайте, как toocreate и управления ими сегментов пользователей tooidentify использования шаблонов с помощью Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a><span data-ttu-id="edfab-103">Как toocreate и сегментов пользователей tooidentify использование шаблонов элементов управления</span><span class="sxs-lookup"><span data-stu-id="edfab-103">How toocreate and manage segments of users tooidentify usage patterns</span></span>
<span data-ttu-id="edfab-104">В этой статье описывается hello **СЕГМЕНТЫ** вкладка hello **мобильного охвата** портала.</span><span class="sxs-lookup"><span data-stu-id="edfab-104">This article describes hello **SEGMENTS** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="edfab-105">Использовать hello **мобильного охвата** портала toomonitor мобильных приложений и управления.</span><span class="sxs-lookup"><span data-stu-id="edfab-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span>

<span data-ttu-id="edfab-106">раздел сегментов Hello hello пользовательского интерфейса позволяет toowork на сегментирование на основе другое поведение hello и анализа, можно получить из приложения hello, а также можно обращаться из hello API сегментов пользователей.</span><span class="sxs-lookup"><span data-stu-id="edfab-106">hello Segments section of hello UI allows you toowork on segmenting your users based on hello different behavior and analytics that you can get from hello application and can also access through hello Segments API.</span></span> <span data-ttu-id="edfab-107">Сегменты сначала вычисляются 24 часа после их создания, и они вычисляются каждые 24 часа, на основе последних сведений analytics hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on hello latest analytics information.</span></span> <span data-ttu-id="edfab-108">После расчета сегмент отображает диаграмму «День tooday журнала» каждый день.</span><span class="sxs-lookup"><span data-stu-id="edfab-108">Once a segment is calculated, it displays a "Day tooday history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="edfab-109">Число разделов hello **Mobile Engagement** пользовательском Интерфейсе портала содержат hello **ОТОБРАЖАТЬ СПРАВКУ** кнопки.</span><span class="sxs-lookup"><span data-stu-id="edfab-109">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="edfab-110">Контекстные сведения о разделе нажмите клавишу tooget этой кнопки.</span><span class="sxs-lookup"><span data-stu-id="edfab-110">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="edfab-111">Создание сегментов</span><span class="sxs-lookup"><span data-stu-id="edfab-111">Create Segments</span></span>
<span data-ttu-id="edfab-112">Можно создать на основе условия too10 в определенный период вверх too60 дней в hello сегмент прошлом из раздела analytics hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-112">You can create a segment based on up too10 criteria on a specific period up too60 days in hello past from hello analytics section.</span></span> <span data-ttu-id="edfab-113">Например можно создать сегмент основании hello специалистами поиск конкретного содержимого в приложение в пределах hello последние 10 дней или просматривать определенные страницы.</span><span class="sxs-lookup"><span data-stu-id="edfab-113">For example, you can create a segment based on hello people who have viewed certain pages or searched for specific content within your app within hello last 10 days.</span></span> <span data-ttu-id="edfab-114">Эта информация доступна в разделе analytics hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-114">This information is available in hello analytics section.</span></span> <span data-ttu-id="edfab-115">Таким образом, можно использовать его toocreate сегмент и затем настроить tootarget принудительной уведомления это подмножество пользователей tooget их toocome задней toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="edfab-115">So, you can use it toocreate a segment, and then set up a push notification tootarget this subset of users tooget them toocome back toohello application.</span></span> 

> [!NOTE]
> <span data-ttu-id="edfab-116">После вычисления сегмент нельзя изменять. Его можно только клонировать (копировать) или уничтожить (удалить).</span><span class="sxs-lookup"><span data-stu-id="edfab-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="edfab-117">Можно клонировать сегмент в hello того же приложения (с hello же AppID), и его можно клонировать также в других приложениях (различных AppID).</span><span class="sxs-lookup"><span data-stu-id="edfab-117">A segment can be cloned within hello same application (with hello same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="edfab-119">Примеры сегментов</span><span class="sxs-lookup"><span data-stu-id="edfab-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="edfab-121">Сегменты позволяют toosegment hello конечных пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="edfab-121">Segments allow you toosegment hello end-users of your application.</span></span>
<span data-ttu-id="edfab-122">Сегментирование пользователей — важная маркетинговая стратегия.</span><span class="sxs-lookup"><span data-stu-id="edfab-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="edfab-123">Azure Mobile Engagement позволяет вам tooget статистические данные и создать пользовательские сегменты.</span><span class="sxs-lookup"><span data-stu-id="edfab-123">Azure Mobile Engagement allows you tooget historic data and create custom segments.</span></span> <span data-ttu-id="edfab-124">Это мощное средство позволяет toolearn о ваших клиентов с пользователем в приложении.</span><span class="sxs-lookup"><span data-stu-id="edfab-124">This powerful tool enables you toolearn about your customers’ experience in your application.</span></span> <span data-ttu-id="edfab-125">Вы можете без труда анализировать сегменты и отправлять по ним push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="edfab-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="edfab-126">Распространенным вариантом применения является требуется toosend извещающие уведомления tooencourage вашей toorate конечных пользователей приложения в магазине hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-126">A common use-case is that you want toosend a push a notification tooencourage your end-users toorate your application in hello store.</span></span> <span data-ttu-id="edfab-127">Вместо отправки tooall уведомление конечных пользователей, можно создать в сегмент, следует указать только пользователей, которые использовали приложение каждый день для hello последний месяц и имели отличный пользовательский интерфейс для использования.</span><span class="sxs-lookup"><span data-stu-id="edfab-127">Rather than sending a notification tooall your end-users, you can create a segment that would specify only users that have used your application every day for hello last month and have had a great user experience.</span></span> <span data-ttu-id="edfab-128">При отправке меньшего количества push-уведомлений, цели которых легче достичь, повышается рентабельность инвестиций.</span><span class="sxs-lookup"><span data-stu-id="edfab-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a><span data-ttu-id="edfab-130">Сегменты, которые можно создать на основе hello основных Azure Mobile Engagement элементов:</span><span class="sxs-lookup"><span data-stu-id="edfab-130">Segments you can create based on hello major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="edfab-131">Событие: создайте сегмент одно определенное событие приложения hello, которое произошло более чем вдвое превышает недели, целевые объекты.</span><span class="sxs-lookup"><span data-stu-id="edfab-131">Event: create a segment that targets one specific event of hello application that happened more than twice a week.</span></span> 
* <span data-ttu-id="edfab-132">Сеанс: создание сегмента пользователей, которые использовали приложение hello более 5 раз прошлой неделе.</span><span class="sxs-lookup"><span data-stu-id="edfab-132">Session: create a segment of users that have used hello application more than 5 times last week.</span></span>
* <span data-ttu-id="edfab-133">Действие. Создайте сегмент пользователей, которые использовали одну страницу или одно и то же содержимое более 10 раз за последний месяц.</span><span class="sxs-lookup"><span data-stu-id="edfab-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="edfab-134">Задание. Создайте сегмент пользователей, которые выполнили одно задание более чем дважды за день.</span><span class="sxs-lookup"><span data-stu-id="edfab-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="edfab-135">Сбой: создайте сегмент всех пользователей hello, для которых сбоя прошлой неделе больше 10 раз.</span><span class="sxs-lookup"><span data-stu-id="edfab-135">Crash: create a segment of all hello users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="edfab-136">(Вы можете отправить сегмент с извинениями или даже купоном!)</span><span class="sxs-lookup"><span data-stu-id="edfab-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="edfab-137">Ошибка: создайте сегмент всех hello пользователей, у которых возникли ошибки более чем в 100 раз последние 3 дней.</span><span class="sxs-lookup"><span data-stu-id="edfab-137">Error: create a segment of all hello users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="edfab-138">Информация приложения: создайте сегмент, предназначенный для пользовательской информация приложения, которое произошло во время hello последние 25 дней.</span><span class="sxs-lookup"><span data-stu-id="edfab-138">App Info: create a segment that targets a custom App Info that happened during hello last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="edfab-140">toouse сегмент оптимальным образом, необходимо проделать интеграции пакета SDK для hello в приложении с помощью тегов плана теги «Информация приложения».</span><span class="sxs-lookup"><span data-stu-id="edfab-140">toouse Segment in an optimal way, you must have done a customized integration of hello SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="edfab-141">Затем перейти на домашнюю страницу toohello hello интерфейса, выберите приложение hello и щелкните в разделе «Сегментов» hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-141">Then, go toohello home page of hello interface, select hello application you want and click on hello "Segments" section.</span></span>

1. <span data-ttu-id="edfab-142">Выберите раздел «Сегменты» hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-142">Select hello "Segments" section.</span></span>
2. <span data-ttu-id="edfab-143">Нажмите кнопку «Новый сегмент» hello кнопку toocreate новый сегмент.</span><span class="sxs-lookup"><span data-stu-id="edfab-143">Click on hello "New segment" button toocreate a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="edfab-144">Пример из практики: создание простого сегмента на основе информации в разделе «Сеанс»</span><span class="sxs-lookup"><span data-stu-id="edfab-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="edfab-145">Создайте сегмент все конечные пользователи hello, использовавших приложения по крайней мере 50 раз в hello прошлой неделе.</span><span class="sxs-lookup"><span data-stu-id="edfab-145">Create a segment of all hello end-users that have used your app at least 50 times in hello last week.</span></span> <span data-ttu-id="edfab-146">После этого найти только hello конечных пользователей, тратили менее 30 секунд в приложении за сеанс.</span><span class="sxs-lookup"><span data-stu-id="edfab-146">From there, find only hello end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="edfab-147">При этом будут отображены все hello конечным пользователям, имеющим положительных результатов в приложении.</span><span class="sxs-lookup"><span data-stu-id="edfab-147">This will show all hello end-users who have a positive experience in your app.</span></span> <span data-ttu-id="edfab-148">Затем создания сегмента hello может быть используется toopush tooask конечным пользователям уведомления toothese их хранения toorate приложение hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-148">Then, hello segment created could be used toopush a notification toothese end-users tooask them toorate your app in hello store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="edfab-150">Присвойте имя сегмента в порядке toofind быстро в списке «Сегмент» hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-150">Give your segment a name in order toofind it quickly in hello "Segment" list.</span></span>
2. <span data-ttu-id="edfab-151">Щелкните кнопку «Создать» hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-151">Click on hello "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="edfab-153">Выберите «Сеанс».</span><span class="sxs-lookup"><span data-stu-id="edfab-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="edfab-155">Выберите период hello «Прошлая неделя».</span><span class="sxs-lookup"><span data-stu-id="edfab-155">Select hello period of "Last week".</span></span>
2. <span data-ttu-id="edfab-156">Нажмите кнопку «Далее».</span><span class="sxs-lookup"><span data-stu-id="edfab-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="edfab-158">Выберите hello оператор, который относится списке hello: =; ≥ ≤.</span><span class="sxs-lookup"><span data-stu-id="edfab-158">Select hello Operator that is relevant among hello list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="edfab-159">Введите hello требуется число.</span><span class="sxs-lookup"><span data-stu-id="edfab-159">Enter hello Count you want.</span></span>
5. <span data-ttu-id="edfab-160">Выберите hello вхождение требуется.</span><span class="sxs-lookup"><span data-stu-id="edfab-160">Select hello Occurrence you want.</span></span> 
6. <span data-ttu-id="edfab-161">Нажмите кнопку «Далее».</span><span class="sxs-lookup"><span data-stu-id="edfab-161">Click next.</span></span>
   <span data-ttu-id="edfab-162">В этом примере задается, что более hello на прошлой неделе соответствия пользователей, которые были внесены по меньшей мере 50 сеансов.</span><span class="sxs-lookup"><span data-stu-id="edfab-162">This example is set so that over hello last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="edfab-164">Для hello сеанса сегментации вы можете hello длина каждого сеанса в качестве критериев.</span><span class="sxs-lookup"><span data-stu-id="edfab-164">For hello Session segmentation, you can choose hello length per session as a criteria.</span></span>

1. <span data-ttu-id="edfab-165">Выберите hello оператор из списка hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-165">Select hello Operator from hello list.</span></span>
2. <span data-ttu-id="edfab-166">Укажите hello, длина каждого сеанса.</span><span class="sxs-lookup"><span data-stu-id="edfab-166">Provide hello Length per session.</span></span>
3. <span data-ttu-id="edfab-167">Нажмите кнопку Далее.</span><span class="sxs-lookup"><span data-stu-id="edfab-167">Click Next.</span></span>
   <span data-ttu-id="edfab-168">В этом примере отображается надпись, по всем hello сеансов, которые разбита на сегменты в разделе "вхождения" hello, выбрать только hello пользователи, которые потратили более 30 секунд для сеанса.</span><span class="sxs-lookup"><span data-stu-id="edfab-168">In this example, it says that over all hello sessions that have been segmented on hello occurrence section, select only hello users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="edfab-170">Имя условия отбора в tooretrieve заказа в hello завершения воронкообразные и нажмите "Готово".</span><span class="sxs-lookup"><span data-stu-id="edfab-170">Name your criterion in order tooretrieve it in hello complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="edfab-172">После завершения копирования условия отбора она появится в сегмент воронкообразной hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-172">When you have finished setting up your criterion, it will appear in hello segment funnel.</span></span>
<span data-ttu-id="edfab-173">Так как сегмент основывается на аналитических данных, вычисление сегментов происходит один раз в день.</span><span class="sxs-lookup"><span data-stu-id="edfab-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="edfab-174">В этом примере 47,7% от общего hello конечным пользователям соответствует критерию hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-174">In this example, 47,7% of hello total end-users matched hello criterion.</span></span> <span data-ttu-id="edfab-175">Они должны быть hello пользователей, которые имели хорошие условия работы и будет скорее всего tooprovide выше оценка, если отправить их уведомление попросите их toorate приложение hello в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="edfab-175">They should be hello users who have had a good experience and will be likely tooprovide a higher rating if you push them a notification asking them toorate hello app in hello store.</span></span>

## <a name="see-also"></a><span data-ttu-id="edfab-176">См. также</span><span class="sxs-lookup"><span data-stu-id="edfab-176">See also</span></span>
* <span data-ttu-id="edfab-177">[Основные понятия Azure Mobile Engagement][Link 6]</span><span class="sxs-lookup"><span data-stu-id="edfab-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="edfab-178">[Поиск и устранение неполадок в службе][Link 24]</span><span class="sxs-lookup"><span data-stu-id="edfab-178">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

