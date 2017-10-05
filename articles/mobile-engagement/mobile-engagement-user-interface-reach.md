---
title: "Пользовательский интерфейс Служб мобильного взаимодействия Azure - Рекламные кампании"
description: "Узнайте, как взаимодействовать с пользователями приложения с помощью push-уведомлений на базе Служб мобильного взаимодействия Azure"
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
ms.openlocfilehash: ce30456e41ff1a2f4824bcb64246ee115fdd1ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reach-out-to-the-users-of-your-application-with-push-notifications"></a><span data-ttu-id="06de0-103">Взаимодействие с пользователями приложения с помощью push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="06de0-103">How to reach out to the users of your application with push notifications</span></span>
<span data-ttu-id="06de0-104">В этой статье описывается вкладка **Reach** (Рекламная кампания) портала **Служб мобильного взаимодействия**.</span><span class="sxs-lookup"><span data-stu-id="06de0-104">This article describes the **REACH** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="06de0-105">Портал **Служб мобильного взаимодействия** используется для отслеживания мобильных приложений и управления ими.</span><span class="sxs-lookup"><span data-stu-id="06de0-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="06de0-106">Обратите внимание, что для того, чтобы начать пользоваться порталом, сначала необходимо создать учетную запись **Служб мобильного взаимодействия Azure**.</span><span class="sxs-lookup"><span data-stu-id="06de0-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="06de0-107">Дополнительные сведения см. в статье [Создание приложения Служб мобильного взаимодействия Azure](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="06de0-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="06de0-108">Раздел рекламных кампаний пользовательского интерфейса — это инструмент управления кампанией push-уведомлений, где можно создавать, менять, активировать, завершать, выполнять мониторинг и статистический анализ кампаний push-уведомлений и функций, которые также доступны через Reach API (и некоторые элементы API push-уведомлений низкого уровня).</span><span class="sxs-lookup"><span data-stu-id="06de0-108">The Reach section of the UI is the Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via the Reach API (and some elements of the low level Push API).</span></span> <span data-ttu-id="06de0-109">Учтите, что независимо от того используете ли вы API или пользовательский интерфейс, чтобы использовать рекламные кампании, вам будет необходимо интегрировать Службы мобильного взаимодействия Azure и функцию рекламных кампаний с помощью пакета SDK в приложение для каждой платформы.</span><span class="sxs-lookup"><span data-stu-id="06de0-109">Remember that whether you are using the APIs or the UI, you will need to integrate both Azure Mobile Engagement and Reach into your application for each platform with the SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="06de0-110">Многие части интерфейса портала **Служб мобильного взаимодействия** содержат кнопку **Показать справку**.</span><span class="sxs-lookup"><span data-stu-id="06de0-110">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="06de0-111">Нажмите ее, чтобы получить больше контекстной информации по соответствующему разделу.</span><span class="sxs-lookup"><span data-stu-id="06de0-111">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="06de0-112">Четыре типа push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="06de0-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="06de0-113">Объявления — позволяют отправлять пользователям рекламные сообщения, которые перенаправляют их в другое расположение в приложении, или отправлять рекламные сообщения на веб-страницы или в магазины вне приложения.</span><span class="sxs-lookup"><span data-stu-id="06de0-113">Announcements - allow you to send advertising messages to users that redirect them to another location inside your app or to send them to a webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="06de0-114">Опросы — позволяют собирать информацию от конечных пользователей, задавая им вопросы.</span><span class="sxs-lookup"><span data-stu-id="06de0-114">Polls - allow you to gather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="06de0-115">Отправка данных — позволяет вам отправлять файлы двоичных данных и файлы данных Base64.</span><span class="sxs-lookup"><span data-stu-id="06de0-115">Data Pushes - allow you to send a binary or base64 data file.</span></span> <span data-ttu-id="06de0-116">Информация, содержащаяся в отправленных данных отправляется в ваше приложение для изменения текущей работы пользователей в приложении.</span><span class="sxs-lookup"><span data-stu-id="06de0-116">The information contained in a data push is sent to your application to modify your users' current experience in your app.</span></span> <span data-ttu-id="06de0-117">В вашем приложении должна быть возможность обработки данных в отправленных данных.</span><span class="sxs-lookup"><span data-stu-id="06de0-117">Your application needs to be able to process the data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="06de0-118">Информация о кампании</span><span class="sxs-lookup"><span data-stu-id="06de0-118">Campaign Details</span></span>
<span data-ttu-id="06de0-119">Можно изменять, клонировать, удалять или активировать неактивированные кампании, наведя указатель мыши на их имена, или щелкнуть их, чтобы открыть.</span><span class="sxs-lookup"><span data-stu-id="06de0-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="06de0-120">Можно клонировать уже активированные кампании, наведя указатель мыши на их имена, или щелкнуть их, чтобы открыть.</span><span class="sxs-lookup"><span data-stu-id="06de0-120">You can clone campaigns that have already been activated by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="06de0-121">Однако после активирования кампанию невозможно изменить.</span><span class="sxs-lookup"><span data-stu-id="06de0-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="06de0-123">Отклик на рекламную кампанию</span><span class="sxs-lookup"><span data-stu-id="06de0-123">Reach Feedback</span></span>
<span data-ttu-id="06de0-124">Щелкните пункт **Статистика**, чтобы просмотреть сведения о рекламной кампании.</span><span class="sxs-lookup"><span data-stu-id="06de0-124">Click on **Statistics** to see the details of a Reach campaign.</span></span> <span data-ttu-id="06de0-125">**Простое** представление — это столбчатая диаграмма, показывающая, что произошло после активации кампании.</span><span class="sxs-lookup"><span data-stu-id="06de0-125">The **Simple** view provides a visual representation in the form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="06de0-126">**Расширенное** представление содержит более подробные сведения о кампании push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="06de0-126">The **Advanced** view provides more granular details about the push campaign.</span></span> <span data-ttu-id="06de0-127">При отправке тестовой кампании (т. е. отправке push-уведомления на тестируемое устройство) эти сведения не отображаются.</span><span class="sxs-lookup"><span data-stu-id="06de0-127">These details will not be available if you are sending a test campaign i.e. a push sent to a test device.</span></span> <span data-ttu-id="06de0-128">Эти сведения надлежит интерпретировать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="06de0-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="06de0-129">**Переданные** — это число сообщений, отправленных на устройства.</span><span class="sxs-lookup"><span data-stu-id="06de0-129">**Pushed** - This specifies the number of messages pushed to the devices.</span></span> <span data-ttu-id="06de0-130">Это число зависит от целевой аудитории, указанной при создании кампании push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="06de0-130">This number will depend on the target audience you specified while creating the push campaign.</span></span> <span data-ttu-id="06de0-131">Если целевая аудитория не указана, push-уведомление будет отправлено на все зарегистрированные устройства.</span><span class="sxs-lookup"><span data-stu-id="06de0-131">If you do not specify any target audience, then this push will be sent out to all the registered devices.</span></span> <span data-ttu-id="06de0-132">Как и другие службы push-уведомлений, мы не отправляем уведомления непосредственно на устройства, а передаем их в соответствующие платформе службы push-уведомлений (PNS - APNS/GCM/WNS), чтобы те могли доставить уведомления на устройства.</span><span class="sxs-lookup"><span data-stu-id="06de0-132">Like all other push services, we do not push the notifications directly to the devices but instead push them to the respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver the notifications to the devices.</span></span> 
2. <span data-ttu-id="06de0-133">**Доставленные** — это число сообщений, успешно доставленных службой push-уведомлений на устройство и признанных полученными пакетом SDK для Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="06de0-133">**Delivered** - This specifies the number of messages which are successfully delivered by the PNS to the device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="06de0-134">*Почему число доставленных сообщений может быть меньше числа отправленных:*</span><span class="sxs-lookup"><span data-stu-id="06de0-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="06de0-135">Если пользователь отменил установку приложения на устройство, но на момент отправки push-уведомления служба push-уведомлений об этом не знает, сообщение удаляется.</span><span class="sxs-lookup"><span data-stu-id="06de0-135">If the user has uninstalled the app from the device but the PNS doesn't know about it at the time we send the push to the PNS then the message will be dropped.</span></span>
   2. <span data-ttu-id="06de0-136">Если на устройстве есть приложение, но в течение долгого времени устройство работает автономно, служба push-уведомлений не сможет доставить сообщение на устройство.</span><span class="sxs-lookup"><span data-stu-id="06de0-136">If the device has the app but the devices themselves were offline for long periods of time, then the PNS will fail to deliver the message to the device.</span></span> 
   3. <span data-ttu-id="06de0-137">Если сообщение доставлено на устройство, но пакет SDK для Служб мобильного взаимодействия в приложении не распознал его содержание, сообщение удаляется.</span><span class="sxs-lookup"><span data-stu-id="06de0-137">If the message does get delivered to the device but the Mobile Engagement SDK in the app doesn’t recognize the content of the message, then it drops that message.</span></span> <span data-ttu-id="06de0-138">Это может произойти, если настройка уведомления в приложении создает исключение, которое мы перехватили в SDK, и привела к удалению сообщения.</span><span class="sxs-lookup"><span data-stu-id="06de0-138">This could happen if the customization of the notification in the app generates an exception which we catch in the SDK and drop the message.</span></span> <span data-ttu-id="06de0-139">Подобная проблема также возникает, если приложение на устройстве использует версию SDK для Служб мобильного взаимодействия, которая не может распознать более новую версию push-уведомления, отправленного с платформы, но это возможно только в том случае, если приложение было обновлено после отправки уведомления с платформы службы.</span><span class="sxs-lookup"><span data-stu-id="06de0-139">This could also occur if the app on the device is using a version of the Mobile Engagement SDK which is not able to understand the newer version of the push message sent from the platform but this is only when the app was upgraded after the notification was dispatched from the service platform.</span></span> <span data-ttu-id="06de0-140">На вкладке **Дополнительно** будет указано количество удаленных сообщений.</span><span class="sxs-lookup"><span data-stu-id="06de0-140">The **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="06de0-141">На устройства iOS сообщения могут не доставляться, если уровень заряда аккумулятора слишком низкий или при обработке удаленных уведомлений приложение потребляет слишком много ресурсов.</span><span class="sxs-lookup"><span data-stu-id="06de0-141">On iOS devices, messages sometimes do not get delivered if either the device is on low battery or if the app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="06de0-142">Это — ограничение устройств iOS.</span><span class="sxs-lookup"><span data-stu-id="06de0-142">This is a limitation of the iOS devices.</span></span>   
3. <span data-ttu-id="06de0-143">**Отображенные** — число сообщений, показанных пользователю приложения на устройстве в виде всплывающих уведомлений в центре уведомлений или в самом мобильном приложении.</span><span class="sxs-lookup"><span data-stu-id="06de0-143">**Displayed** - This specifies the number of messages which are successfully shown to the app user on the device in the form of a system push/out-of-app notification in the notification center or an in-app notification within the mobile app.</span></span>  <span data-ttu-id="06de0-144">На вкладке **Дополнительно** будет указано количество системных уведомлений и уведомлений в приложении.</span><span class="sxs-lookup"><span data-stu-id="06de0-144">The **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="06de0-145">*Причины, по которым отображаемое количество меньше доставленного (которое еще будет отображено)*</span><span class="sxs-lookup"><span data-stu-id="06de0-145">*Reasons for Displayed count being less than Delivered count (waiting to be displayed)*</span></span>
   
   1. <span data-ttu-id="06de0-146">Если у кампании уведомлений есть дата окончания, то возможно, что уведомление было доставлено, но когда пришло время открыть и отобразить его пользователю приложения, срок действия кампании уже закончился, поэтому оно так и не было показано.</span><span class="sxs-lookup"><span data-stu-id="06de0-146">If the notification campaign had an end date on it then it is possible that the notification was delivered but when the time came to open and display it to the app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="06de0-147">Если уведомление представляет собой уведомление в приложении, то оно отображается только в том случае, если пользователь открыл приложение.</span><span class="sxs-lookup"><span data-stu-id="06de0-147">If the notification is an in-app notification then the notification is only displayed when the app user opens the app.</span></span> <span data-ttu-id="06de0-148">В случаях, когда пользователь не открыл приложение, пакет SDK сообщит, что уведомление было доставлено, но не будет открыто, пока пользователь не откроет приложение.</span><span class="sxs-lookup"><span data-stu-id="06de0-148">In cases where the app user hasn't opened the app, the SDK will report that the notification was delivered but not yet displayed until the app is opened.</span></span> 
   3. <span data-ttu-id="06de0-149">Если уведомление представляет собой уведомление в приложении и оно привязано к конкретному действию или окну, то оно также будет считаться доставленным, но не показанным, пока пользователь не откроет необходимое окно в приложении.</span><span class="sxs-lookup"><span data-stu-id="06de0-149">If the notification is an in-app notification and configured to be shown on a specific activity/screen then also the notification will be reported as delivered but not yet delivered until the user opens the app on a specific screen.</span></span> 
4. <span data-ttu-id="06de0-150">**Количество взаимодействий с пользователем** — указывает количество сообщений, с которыми взаимодействовал пользователь приложения. Это количество будет включать сообщения, которые были закрыты и для которых были выполнены действия.</span><span class="sxs-lookup"><span data-stu-id="06de0-150">**User Interactions** - This specifies the number of messages which the app user has interacted with and will include the messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="06de0-151">*Пользователь приложения может взаимодействовать с уведомлением одним из следующих способов:*</span><span class="sxs-lookup"><span data-stu-id="06de0-151">*The app user can action a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="06de0-152">Если уведомление является системным или уведомление в приложении отправляется как простое уведомление, пользователь приложения щелкает это уведомление.</span><span class="sxs-lookup"><span data-stu-id="06de0-152">If the notification is a system/out-of-app notification or an in-app notification sent as notification-only then the app user clicks on the notification.</span></span>
     2. <span data-ttu-id="06de0-153">Если это уведомление в приложении с текстом, веб-представлением или опросом, пользователь приложения нажимает кнопку действия в области уведомлений.</span><span class="sxs-lookup"><span data-stu-id="06de0-153">If the notification is an in-app notification with a text or web-view or polls then the app user clicks on the Action button in the notification.</span></span>
     3. <span data-ttu-id="06de0-154">Если это уведомление в приложении с веб-представлением, пользователь приложения щелкает URL-адрес в веб представлении (только на устройствах Android).</span><span class="sxs-lookup"><span data-stu-id="06de0-154">If the notification is an in-app notification with a web-view then the app user clicks on a URL in the web view [Android Only]</span></span>
   * <span data-ttu-id="06de0-155">*Пользователь приложения может выйти из уведомления одним из следующих способов:*</span><span class="sxs-lookup"><span data-stu-id="06de0-155">*The app user can exit a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="06de0-156">Нажав кнопку "Закрыть" в самом уведомлении.</span><span class="sxs-lookup"><span data-stu-id="06de0-156">Clicking the close button on the notification directly.</span></span> 
     2. <span data-ttu-id="06de0-157">Смахнув или удалив уведомление.</span><span class="sxs-lookup"><span data-stu-id="06de0-157">Swiping away or deleting the notification.</span></span> 
     3. <span data-ttu-id="06de0-158">Уведомления в приложении с текстом или веб-содержимым и опросами обычно отображаются пользователям приложения в два этапа.</span><span class="sxs-lookup"><span data-stu-id="06de0-158">In-app notifications with text/web content and polls are typically displayed to the app user in a two-step process.</span></span> <span data-ttu-id="06de0-159">Сначала пользователь видит уведомление, а после щелчка по уведомлению — последующий текст, веб-содержимое или опрос.</span><span class="sxs-lookup"><span data-stu-id="06de0-159">They see a notification first and when they click on it, they see the subsequent text/web/poll content.</span></span> <span data-ttu-id="06de0-160">Пользователь приложения может выйти из уведомления любым из указанных выше способов. Соответствующие данные появятся на вкладке "Дополнительно".</span><span class="sxs-lookup"><span data-stu-id="06de0-160">The app user can exit a notification in either of these steps and the details in the Advanced view captures this.</span></span> 
5. <span data-ttu-id="06de0-161">**Выполненные** — указывает количество сообщений, для которых пользователь явно выполнил действия.</span><span class="sxs-lookup"><span data-stu-id="06de0-161">**Actioned** - This specifies the number of messages which were explicitly actioned by the app user.</span></span> <span data-ttu-id="06de0-162">Это — наиболее интересный показатель, указывающий, сколько пользователей приложения заинтересовались переданным вами push-уведомлением.</span><span class="sxs-lookup"><span data-stu-id="06de0-162">This is the most interesting number as this tells how many app users were interested by the message you pushed out in the notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="06de0-163">Если пользователь платформы iOS или Windows открывает приложение и кампания не включает временных ограничений, системное уведомление и уведомление в приложении могут появиться одновременно.</span><span class="sxs-lookup"><span data-stu-id="06de0-163">On iOS & Windows platforms, if the user has the app open and the campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at the same time.</span></span> <span data-ttu-id="06de0-164">В результате число отображенных сообщений может оказаться выше числа доставленных.</span><span class="sxs-lookup"><span data-stu-id="06de0-164">This may cause a Displayed count higher than the Delivered.</span></span> <span data-ttu-id="06de0-165">Если пользователь взаимодействует с уведомлением или предпринимает какие-то действия, то даже число взаимодействий может быть выше числа доставленных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="06de0-165">If the user interacts or actions the notification, then even the User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="06de0-167">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="06de0-167">See also</span></span>
* <span data-ttu-id="06de0-168">[Основные понятия Azure Mobile Engagement][Link 6]</span><span class="sxs-lookup"><span data-stu-id="06de0-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="06de0-169">[Поиск и устранение неполадок в службе][Link 24]</span><span class="sxs-lookup"><span data-stu-id="06de0-169">[Troubleshooting Guide Service][Link 24]</span></span>

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

