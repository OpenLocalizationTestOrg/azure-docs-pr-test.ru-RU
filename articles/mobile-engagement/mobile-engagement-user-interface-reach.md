---
title: "Пользовательский интерфейс Mobile Engagement - Reach aaaAzure"
description: "Узнайте, как tooreach toohello пользователей приложения с push-уведомления с помощью Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a><span data-ttu-id="10826-103">Как tooreach toohello пользователей приложения с push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="10826-103">How tooreach out toohello users of your application with push notifications</span></span>
<span data-ttu-id="10826-104">В этой статье описывается hello **ДОСТИЧЬ** вкладка hello **мобильного охвата** портала.</span><span class="sxs-lookup"><span data-stu-id="10826-104">This article describes hello **REACH** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="10826-105">Использовать hello **мобильного охвата** портала toomonitor мобильных приложений и управления.</span><span class="sxs-lookup"><span data-stu-id="10826-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="10826-106">Обратите внимание, что toostart с помощью портала hello, необходимо сначала toocreate **Azure Mobile Engagement** учетной записи.</span><span class="sxs-lookup"><span data-stu-id="10826-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="10826-107">Дополнительные сведения см. в статье [Создание приложения Служб мобильного взаимодействия Azure](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="10826-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="10826-108">Hello достичь раздел пользовательского интерфейса приветствия hello кампании Push управления средства, где можно создать или изменить или активировать/Готово/монитор и получить статистику на Push-кампаний, уведомления и функции, которые можно получить через Reach API hello (и некоторые элементы hello низкий уровень Push API).</span><span class="sxs-lookup"><span data-stu-id="10826-108">hello Reach section of hello UI is hello Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via hello Reach API (and some elements of hello low level Push API).</span></span> <span data-ttu-id="10826-109">Помните, что вы используете hello API-интерфейсы или hello пользовательского интерфейса, следует ли toointegrate Azure Mobile Engagement и интегрировать приложения для каждой платформы с hello перед использованием пакета SDK для достижения кампании.</span><span class="sxs-lookup"><span data-stu-id="10826-109">Remember that whether you are using hello APIs or hello UI, you will need toointegrate both Azure Mobile Engagement and Reach into your application for each platform with hello SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="10826-110">Число разделов hello **Mobile Engagement** пользовательском Интерфейсе портала содержат hello **ОТОБРАЖАТЬ СПРАВКУ** кнопки.</span><span class="sxs-lookup"><span data-stu-id="10826-110">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="10826-111">Контекстные сведения о разделе нажмите клавишу tooget этой кнопки.</span><span class="sxs-lookup"><span data-stu-id="10826-111">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="10826-112">Четыре типа push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="10826-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="10826-113">Извещения - разрешить toousers toosend рекламных сообщений, которое перенаправит их расположение tooanother внутри приложения или toosend их tooa веб-страницу или сохранить за пределами приложения.</span><span class="sxs-lookup"><span data-stu-id="10826-113">Announcements - allow you toosend advertising messages toousers that redirect them tooanother location inside your app or toosend them tooa webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="10826-114">Опрашивает - разрешить toogather сведения от конечных пользователей, задав их вопросы.</span><span class="sxs-lookup"><span data-stu-id="10826-114">Polls - allow you toogather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="10826-115">Отправок данных — разрешить toosend файл данных binary или base64.</span><span class="sxs-lookup"><span data-stu-id="10826-115">Data Pushes - allow you toosend a binary or base64 data file.</span></span> <span data-ttu-id="10826-116">Hello сведения, содержащиеся в принудительной отправки данных отправлено toomodify приложения tooyour текущий интерфейс пользователей в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="10826-116">hello information contained in a data push is sent tooyour application toomodify your users' current experience in your app.</span></span> <span data-ttu-id="10826-117">Приложения должны toobe может tooprocess hello принудительной отправки данных.</span><span class="sxs-lookup"><span data-stu-id="10826-117">Your application needs toobe able tooprocess hello data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="10826-118">Информация о кампании</span><span class="sxs-lookup"><span data-stu-id="10826-118">Campaign Details</span></span>
<span data-ttu-id="10826-119">Можно изменить, клонирование, удалить или активировать кампаний, которые не была активирована, наведя на их имена или щелкнуть tooopen их.</span><span class="sxs-lookup"><span data-stu-id="10826-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="10826-120">Можно клонировать кампаний, которые уже были активированы при наведении указателя мыши на их имена или щелкнуть tooopen их.</span><span class="sxs-lookup"><span data-stu-id="10826-120">You can clone campaigns that have already been activated by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="10826-121">Однако после активирования кампанию невозможно изменить.</span><span class="sxs-lookup"><span data-stu-id="10826-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="10826-123">Отклик на рекламную кампанию</span><span class="sxs-lookup"><span data-stu-id="10826-123">Reach Feedback</span></span>
<span data-ttu-id="10826-124">Щелкните **статистики** toosee hello сведений о кампании Reach.</span><span class="sxs-lookup"><span data-stu-id="10826-124">Click on **Statistics** toosee hello details of a Reach campaign.</span></span> <span data-ttu-id="10826-125">Hello **простой** представление предоставляет визуальное отображение в форме hello гистограмму столбец о том, что произошло после активации кампании.</span><span class="sxs-lookup"><span data-stu-id="10826-125">hello **Simple** view provides a visual representation in hello form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="10826-126">Hello **Дополнительно** содержит детальные сведения о hello кампании push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="10826-126">hello **Advanced** view provides more granular details about hello push campaign.</span></span> <span data-ttu-id="10826-127">Эти сведения будет недоступен при отправке кампании теста т. е. принудительной отправки tooa тестовое устройство.</span><span class="sxs-lookup"><span data-stu-id="10826-127">These details will not be available if you are sending a test campaign i.e. a push sent tooa test device.</span></span> <span data-ttu-id="10826-128">Эти сведения надлежит интерпретировать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="10826-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="10826-129">**Передано** -указывает hello количество сообщений, отправленных toohello устройств.</span><span class="sxs-lookup"><span data-stu-id="10826-129">**Pushed** - This specifies hello number of messages pushed toohello devices.</span></span> <span data-ttu-id="10826-130">Это число будет зависеть от целевой аудитории hello, указанному при создании кампании push hello.</span><span class="sxs-lookup"><span data-stu-id="10826-130">This number will depend on hello target audience you specified while creating hello push campaign.</span></span> <span data-ttu-id="10826-131">Если любой целевой аудитории не указан, это push будут отправляться out tooall hello зарегистрированные устройства.</span><span class="sxs-lookup"><span data-stu-id="10826-131">If you do not specify any target audience, then this push will be sent out tooall hello registered devices.</span></span> <span data-ttu-id="10826-132">Как и другие службы принудительной мы не извещающих уведомлений hello непосредственно toohello устройства, но вместо этого отправить их соответствующих платформы toohello конкретных службах Push Notification Service (службе PNS - APNS, GCM/WNS), чтобы они доставлять уведомления hello toohello устройств.</span><span class="sxs-lookup"><span data-stu-id="10826-132">Like all other push services, we do not push hello notifications directly toohello devices but instead push them toohello respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver hello notifications toohello devices.</span></span> 
2. <span data-ttu-id="10826-133">**Доставлено** -это задает hello количество сообщений, которые успешно доставлено на устройство toohello PNS hello и подтверждения как принято пакет SDK Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="10826-133">**Delivered** - This specifies hello number of messages which are successfully delivered by hello PNS toohello device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="10826-134">*Почему число доставленных сообщений может быть меньше числа отправленных:*</span><span class="sxs-lookup"><span data-stu-id="10826-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="10826-135">Если hello пользователь удалил приложение hello hello устройства, но hello PNS не знает о нем в момент hello мы отправляем hello принудительной toohello PNS приветственное сообщение отбрасывается.</span><span class="sxs-lookup"><span data-stu-id="10826-135">If hello user has uninstalled hello app from hello device but hello PNS doesn't know about it at hello time we send hello push toohello PNS then hello message will be dropped.</span></span>
   2. <span data-ttu-id="10826-136">Если устройство hello имеет приложение hello самих устройств hello находился в автономном режиме длительные периоды времени, затем hello PNS произойдет сбой устройства toohello сообщение hello toodeliver.</span><span class="sxs-lookup"><span data-stu-id="10826-136">If hello device has hello app but hello devices themselves were offline for long periods of time, then hello PNS will fail toodeliver hello message toohello device.</span></span> 
   3. <span data-ttu-id="10826-137">Если приветственное сообщение будет доставлено toohello устройства, но hello Mobile Engagement SDK в приложение hello не распознает hello содержимое сообщения hello, удаляет сообщение.</span><span class="sxs-lookup"><span data-stu-id="10826-137">If hello message does get delivered toohello device but hello Mobile Engagement SDK in hello app doesn’t recognize hello content of hello message, then it drops that message.</span></span> <span data-ttu-id="10826-138">Это может произойти, если настройки hello hello уведомления в приложение hello создает исключение, которое мы catch в приветственное сообщение hello SDK и drop.</span><span class="sxs-lookup"><span data-stu-id="10826-138">This could happen if hello customization of hello notification in hello app generates an exception which we catch in hello SDK and drop hello message.</span></span> <span data-ttu-id="10826-139">Эта ошибка также возникает, если приложение hello на устройстве hello с помощью версии hello Mobile Engagement SDK, который не может toounderstand hello push-сообщение hello в более новой версии отправленных hello платформы, но это только в том случае, когда приложение hello был обновлен после уведомления hello была подготовлена с hello службы платформы.</span><span class="sxs-lookup"><span data-stu-id="10826-139">This could also occur if hello app on hello device is using a version of hello Mobile Engagement SDK which is not able toounderstand hello newer version of hello push message sent from hello platform but this is only when hello app was upgraded after hello notification was dispatched from hello service platform.</span></span> <span data-ttu-id="10826-140">Hello **Дополнительно** вкладку поможет определить, сколько сообщений было удалено.</span><span class="sxs-lookup"><span data-stu-id="10826-140">hello **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="10826-141">На устройствах iOS сообщения иногда не будет доставлено при либо hello устройства на низком заряде батарей или если приложение hello потребляет значительный объем power при обработке удаленного уведомления.</span><span class="sxs-lookup"><span data-stu-id="10826-141">On iOS devices, messages sometimes do not get delivered if either hello device is on low battery or if hello app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="10826-142">Это ограничение hello устройств iOS.</span><span class="sxs-lookup"><span data-stu-id="10826-142">This is a limitation of hello iOS devices.</span></span>   
3. <span data-ttu-id="10826-143">**Отображается** -указывает hello количество сообщений, показанных успешно toohello пользователя приложения на устройстве hello в форме hello Системное уведомление принудительной/out объекта приложения в центре уведомлений hello или уведомление в приложении в hello мобильных устройств приложение.</span><span class="sxs-lookup"><span data-stu-id="10826-143">**Displayed** - This specifies hello number of messages which are successfully shown toohello app user on hello device in hello form of a system push/out-of-app notification in hello notification center or an in-app notification within hello mobile app.</span></span>  <span data-ttu-id="10826-144">Hello **Дополнительно** вкладку сообщит, сколько были системных уведомлений и сколько составил уведомления в приложения.</span><span class="sxs-lookup"><span data-stu-id="10826-144">hello **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="10826-145">*Причины отображается число меньше доставлено count (toobe ожидания отображаются)*</span><span class="sxs-lookup"><span data-stu-id="10826-145">*Reasons for Displayed count being less than Delivered count (waiting toobe displayed)*</span></span>
   
   1. <span data-ttu-id="10826-146">Если hello уведомление кампании имеет дату окончания на нем возможно hello уведомление было доставлено, но когда время hello документации tooopen и отобразить ее toohello пользователя приложения, уже истек, никогда не отображается.</span><span class="sxs-lookup"><span data-stu-id="10826-146">If hello notification campaign had an end date on it then it is possible that hello notification was delivered but when hello time came tooopen and display it toohello app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="10826-147">Если уведомление об hello уведомление в приложении затем hello уведомления отображаются, только если пользователь приложения hello открывает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="10826-147">If hello notification is an in-app notification then hello notification is only displayed when hello app user opens hello app.</span></span> <span data-ttu-id="10826-148">В случаях, где пользователь приложения hello еще не открыл приложение hello hello SDK сообщит, что уведомления hello был доставки, но еще не отображается, пока не будет открыт приложение hello.</span><span class="sxs-lookup"><span data-stu-id="10826-148">In cases where hello app user hasn't opened hello app, hello SDK will report that hello notification was delivered but not yet displayed until hello app is opened.</span></span> 
   3. <span data-ttu-id="10826-149">Если уведомление hello уведомление в приложении и настроен toobe, отображаемый на определенные действия и экрана, также будут считаться hello уведомления в конфигурации, а затем, но еще не доставлены до hello пользователь открывает приложение hello на указанный экран.</span><span class="sxs-lookup"><span data-stu-id="10826-149">If hello notification is an in-app notification and configured toobe shown on a specific activity/screen then also hello notification will be reported as delivered but not yet delivered until hello user opens hello app on a specific screen.</span></span> 
4. <span data-ttu-id="10826-150">**Взаимодействие с пользователем** -указывает hello количество сообщений, какой пользователь приложения hello взаимодействовать с ними и будет содержать сообщения hello, которые обработаны или закрыты.</span><span class="sxs-lookup"><span data-stu-id="10826-150">**User Interactions** - This specifies hello number of messages which hello app user has interacted with and will include hello messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="10826-151">*Hello приложения пользователь может отреагировать уведомлений в одном из следующих способов hello:*</span><span class="sxs-lookup"><span data-stu-id="10826-151">*hello app user can action a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="10826-152">Если hello уведомления уведомление системы/out объекта приложения или отправлено уведомление в приложении только для уведомления то hello приложения пользователь щелкает hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="10826-152">If hello notification is a system/out-of-app notification or an in-app notification sent as notification-only then hello app user clicks on hello notification.</span></span>
     2. <span data-ttu-id="10826-153">Если уведомления hello уведомление в приложении с текстом или веб-представление или опрашивает затем hello приложения пользователь нажимает кнопку hello кнопка в уведомлении hello.</span><span class="sxs-lookup"><span data-stu-id="10826-153">If hello notification is an in-app notification with a text or web-view or polls then hello app user clicks on hello Action button in hello notification.</span></span>
     3. <span data-ttu-id="10826-154">Если уведомление об hello уведомление в приложении с веб представление затем hello приложения щелчки мышью на URL-адрес в веб-представление hello [Android только]</span><span class="sxs-lookup"><span data-stu-id="10826-154">If hello notification is an in-app notification with a web-view then hello app user clicks on a URL in hello web view [Android Only]</span></span>
   * <span data-ttu-id="10826-155">*пользователь приложения Hello может выйти уведомлений в одном из следующих способов hello:*</span><span class="sxs-lookup"><span data-stu-id="10826-155">*hello app user can exit a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="10826-156">Кнопки hello закрыть на hello уведомлений напрямую.</span><span class="sxs-lookup"><span data-stu-id="10826-156">Clicking hello close button on hello notification directly.</span></span> 
     2. <span data-ttu-id="10826-157">Считывания отсутствовали или удаление hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="10826-157">Swiping away or deleting hello notification.</span></span> 
     3. <span data-ttu-id="10826-158">Уведомления в приложении с текстовыми и веб-содержимого и опрашивает являются пользователя приложения обычно отображается toohello в два этапа.</span><span class="sxs-lookup"><span data-stu-id="10826-158">In-app notifications with text/web content and polls are typically displayed toohello app user in a two-step process.</span></span> <span data-ttu-id="10826-159">Они видят уведомление, и при щелчке на нем, они видят hello последующее содержимое текста, веб-или опрос.</span><span class="sxs-lookup"><span data-stu-id="10826-159">They see a notification first and when they click on it, they see hello subsequent text/web/poll content.</span></span> <span data-ttu-id="10826-160">Hello приложения пользователь может выйти уведомлений в одно из этих действий и подробности hello в расширенном представлении hello записывает это.</span><span class="sxs-lookup"><span data-stu-id="10826-160">hello app user can exit a notification in either of these steps and hello details in hello Advanced view captures this.</span></span> 
5. <span data-ttu-id="10826-161">**Обработанных** -указывает hello количество сообщений, которые были явно обработанных пользователем приложения hello.</span><span class="sxs-lookup"><span data-stu-id="10826-161">**Actioned** - This specifies hello number of messages which were explicitly actioned by hello app user.</span></span> <span data-ttu-id="10826-162">Это число наиболее интересные hello сообщает, сколько пользователей приложения были нужны сообщение hello, распространить hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="10826-162">This is hello most interesting number as this tells how many app users were interested by hello message you pushed out in hello notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="10826-163">IOS & платформ Windows, если пользователя Привет открыть приложение hello и hello кампании была кампании «В любое время» возможно, что из приложения и в приложении уведомления поисковые hello то же время.</span><span class="sxs-lookup"><span data-stu-id="10826-163">On iOS & Windows platforms, if hello user has hello app open and hello campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at hello same time.</span></span> <span data-ttu-id="10826-164">Это может привести к счетчик отображаемые выше, чем hello доставлено.</span><span class="sxs-lookup"><span data-stu-id="10826-164">This may cause a Displayed count higher than hello Delivered.</span></span> <span data-ttu-id="10826-165">Если пользователь hello взаимодействует или действия hello уведомления, затем даже hello число взаимодействий пользователей/Actioned может быть больше, чем доставлено.</span><span class="sxs-lookup"><span data-stu-id="10826-165">If hello user interacts or actions hello notification, then even hello User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="10826-167">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="10826-167">See also</span></span>
* <span data-ttu-id="10826-168">[Основные понятия Azure Mobile Engagement][Link 6]</span><span class="sxs-lookup"><span data-stu-id="10826-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="10826-169">[Поиск и устранение неполадок в службе][Link 24]</span><span class="sxs-lookup"><span data-stu-id="10826-169">[Troubleshooting Guide Service][Link 24]</span></span>

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

