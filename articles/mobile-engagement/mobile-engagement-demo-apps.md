---
title: "Демонстрационное приложение Служб мобильного взаимодействия Azure | Документация Майкрософт"
description: "Описывает, куда загружать, как использовать и как определять преимущества с помощью демонстрационного приложения Служб мобильного взаимодействия Azure."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 8381edb569e19a85c1259f7791b477cfa6e51ea3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-demo-app"></a><span data-ttu-id="34362-103">Демонстрационное приложение Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="34362-103">Azure Mobile Engagement demo app</span></span>
<span data-ttu-id="34362-104">Корпорация Майкрософт опубликовала демонстрационное приложение Служб мобильного взаимодействия Azure для платформ **iOS**, **Android** и **Windows**, чтобы помочь вам найти полезные ресурсы и узнать больше о приложении Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="34362-104">We've published an Azure Mobile Engagement demo app for **iOS**, **Android**, and **Windows** platforms to help you to find useful resources and learn more about Mobile Engagement.</span></span>

<span data-ttu-id="34362-105">Это приложение поможет вам:</span><span class="sxs-lookup"><span data-stu-id="34362-105">The app helps you to:</span></span>

* <span data-ttu-id="34362-106">Легко находить полезные ссылки на ресурсы Служб мобильного взаимодействия, включая видео, документацию, форум, где можно создавать запросы новых функций и т. д.</span><span class="sxs-lookup"><span data-stu-id="34362-106">Easily find useful links to Mobile Engagement resources like videos, documentation, the support forum, and where to go to raise feature requests.</span></span>
* <span data-ttu-id="34362-107">Изучать примеры уведомлений, поддерживаемых приложением Служб мобильного взаимодействия, для получения идей, которые можно использовать в собственных мобильных приложениях.</span><span class="sxs-lookup"><span data-stu-id="34362-107">Experience sample notifications that are supported by Mobile Engagement to get ideas for your own mobile applications.</span></span>
* <span data-ttu-id="34362-108">Используйте эталонную реализацию для изучения способов реализации Служб мобильного взаимодействия в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="34362-108">Use a reference implementation to study how to implement Mobile Engagement into your own app.</span></span> <span data-ttu-id="34362-109">Вы научитесь:</span><span class="sxs-lookup"><span data-stu-id="34362-109">You can learn to:</span></span>
  
  * <span data-ttu-id="34362-110">собирать аналитические данные;</span><span class="sxs-lookup"><span data-stu-id="34362-110">Collect analytics data.</span></span>
  * <span data-ttu-id="34362-111">реализовывать сложные сценарии уведомлений таких типов, как *внутреннее полноэкранное представление* или *всплывающее окно*;</span><span class="sxs-lookup"><span data-stu-id="34362-111">Implement advanced notification scenarios of types such as *Full-screen interstitial* or *Pop-up*.</span></span>
  * <span data-ttu-id="34362-112">внедрять опросы;</span><span class="sxs-lookup"><span data-stu-id="34362-112">Implement surveys and polls.</span></span>
  * <span data-ttu-id="34362-113">реализовывать сценарии использования автоматических push-уведомлений или отправки данных.</span><span class="sxs-lookup"><span data-stu-id="34362-113">Implement silent push data and push scenarios.</span></span>   

## <a name="app-installation"></a><span data-ttu-id="34362-114">Установка приложения</span><span class="sxs-lookup"><span data-stu-id="34362-114">App installation</span></span>
<span data-ttu-id="34362-115">Это приложение доступно в следующих магазинах приложений:</span><span class="sxs-lookup"><span data-stu-id="34362-115">This app is available in the following app stores:</span></span>

* <span data-ttu-id="34362-116">**Демонстрационное приложение Windows Universal**:</span><span class="sxs-lookup"><span data-stu-id="34362-116">**Windows Universal demo app**:</span></span>
  
  * <span data-ttu-id="34362-117">Скачивание приложения из [магазина Windows](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).</span><span class="sxs-lookup"><span data-stu-id="34362-117">Download the app at the [Windows App store](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).</span></span>
  * <span data-ttu-id="34362-118">Приложение было разработано как универсальное приложение для Windows 10.</span><span class="sxs-lookup"><span data-stu-id="34362-118">The app was developed as a Windows 10 Universal app.</span></span> <span data-ttu-id="34362-119">Исходный код доступен на сайте [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).</span><span class="sxs-lookup"><span data-stu-id="34362-119">The source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).</span></span>
* <span data-ttu-id="34362-120">**Демонстрационное приложение iOS**:</span><span class="sxs-lookup"><span data-stu-id="34362-120">**iOS demo app**:</span></span>
  
  * <span data-ttu-id="34362-121">загрузка приложения из [магазина Apple](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).</span><span class="sxs-lookup"><span data-stu-id="34362-121">Download the app at the [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).</span></span>
  * <span data-ttu-id="34362-122">Приложение было разработано в iOS Swift.</span><span class="sxs-lookup"><span data-stu-id="34362-122">The app was developed in iOS Swift.</span></span> <span data-ttu-id="34362-123">Исходный код доступен на сайте [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).</span><span class="sxs-lookup"><span data-stu-id="34362-123">The source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).</span></span>
* <span data-ttu-id="34362-124">**Демонстрационное приложение Android**:</span><span class="sxs-lookup"><span data-stu-id="34362-124">**Android demo app**:</span></span>
  
  * <span data-ttu-id="34362-125">загрузка приложения из [магазина Google Play](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).</span><span class="sxs-lookup"><span data-stu-id="34362-125">Download the app at the [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).</span></span>
  * <span data-ttu-id="34362-126">Исходный код доступен на сайте [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).</span><span class="sxs-lookup"><span data-stu-id="34362-126">The source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).</span></span>

![Демонстрационное приложение Windows Universal][1]

<span data-ttu-id="34362-128">![Демонстрационное приложение iOS][2]
![Демонстрационное приложение Android][3]</span><span class="sxs-lookup"><span data-stu-id="34362-128">![iOS demo app][2]
![Android demo app][3]</span></span>

## <a name="usage"></a><span data-ttu-id="34362-129">Использование</span><span class="sxs-lookup"><span data-stu-id="34362-129">Usage</span></span>
<span data-ttu-id="34362-130">Это приложение можно использовать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="34362-130">You can use this app in the following ways:</span></span>

<span data-ttu-id="34362-131">**Загружать приложение на устройство по указанным выше ссылкам на магазин приложений.**</span><span class="sxs-lookup"><span data-stu-id="34362-131">**Download the app on your device from the application store links (provided earlier):**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34362-132">Учетная запись Azure или подключение к какой-либо серверной части не требуется.</span><span class="sxs-lookup"><span data-stu-id="34362-132">You don't need an Azure account or need to connect the app to a back end.</span></span> <span data-ttu-id="34362-133">Приложение работает независимо.</span><span class="sxs-lookup"><span data-stu-id="34362-133">The app works independently.</span></span>
> 
> 

* <span data-ttu-id="34362-134">Создав приложение на устройстве, вы сможете пройти по ссылкам в меню слева и найти все полезные ресурсы о приложении Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="34362-134">After you have the app on your device, then you can go through the links in the left-side menu to find the useful resources about Mobile Engagement.</span></span>
* <span data-ttu-id="34362-135">Мы также добавили в приложение [RSS-канал службы](https://aka.ms/azmerssfeed) , чтобы у вас всегда был доступ к последним обновлениям.</span><span class="sxs-lookup"><span data-stu-id="34362-135">We've added the [service's RSS feed](https://aka.ms/azmerssfeed) into this application so that you're always updated about the latest product updates.</span></span>
* <span data-ttu-id="34362-136">Кроме того, вы можете выполнить примеры сценариев уведомлений и проверить, какие типы уведомлений поддерживают Службы мобильного взаимодействия для каждой платформы.</span><span class="sxs-lookup"><span data-stu-id="34362-136">You can also go through the sample notification scenarios to experience the type of notifications that are supported by Mobile Engagement for each platform.</span></span> <span data-ttu-id="34362-137">Эти уведомления можно получить локально, т. е. щелкнуть кнопки на экране и получить такие же уведомления, как при отправке уведомлений с платформы Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="34362-137">These notifications can be experienced locally--that is, you can click the buttons on the screens to show you the notifications experience, which is identical to sending the notifications from the Mobile Engagement platform.</span></span>

![Меню приложения для Windows][4]

<span data-ttu-id="34362-139">![Меню приложения для iOS][5]
![меню приложения для Android][6]</span><span class="sxs-lookup"><span data-stu-id="34362-139">![App menu for iOS][5]
![App menu for Android][6]</span></span>

<span data-ttu-id="34362-140">**Загружать исходный код по указанным выше ссылкам в Github.**</span><span class="sxs-lookup"><span data-stu-id="34362-140">**Download the source code from the GitHub links (provided earlier):**</span></span>

* <span data-ttu-id="34362-141">Загрузив исходный код, откройте его в соответствующей среде разработки, такой как XCode для iOS, Android Studio для Android и Visual Studio для Windows.</span><span class="sxs-lookup"><span data-stu-id="34362-141">After you've downloaded the source code, open it in the respective development environment--XCode for iOS, Android Studio for Android, and Visual Studio for Windows.</span></span>
* <span data-ttu-id="34362-142">Затем необходимо выполнить [процедуру интеграции основного пакета SDK](mobile-engagement-windows-store-dotnet-get-started.md), чтобы подключить приложение к собственному экземпляру серверной части Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="34362-142">You should next follow our [basic SDK integration steps](mobile-engagement-windows-store-dotnet-get-started.md) so that you're able to connect this app to its own Mobile Engagement back-end instance.</span></span>
  * <span data-ttu-id="34362-143">Необходимо настроить строку подключения в приложении.</span><span class="sxs-lookup"><span data-stu-id="34362-143">You need to configure a connection string in the app.</span></span>
  * <span data-ttu-id="34362-144">Также необходимо настроить платформу push-уведомлений для приложения.</span><span class="sxs-lookup"><span data-stu-id="34362-144">You also need to configure the push notification platform for your app.</span></span>
* <span data-ttu-id="34362-145">Вы заметите, что само приложение инструментируется с помощью Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="34362-145">You'll notice that the app itself is instrumented with Mobile Engagement.</span></span> <span data-ttu-id="34362-146">В связи с этим, открыв приложение после того, как оно подключится к серверу, вы сможете просматривать сеанс пользователя, действия, события и т. д. на вкладке **Монитор**.</span><span class="sxs-lookup"><span data-stu-id="34362-146">Therefore, as you open the app after connecting it to the back end, you'll be able to see the user session, activities, events, and so on, on the **Monitor** tab.</span></span>
* <span data-ttu-id="34362-147">Кроме того, вы сможете отправлять уведомления в это приложение из собственного экземпляра Служб мобильного взаимодействия, не используя локальные уведомления.</span><span class="sxs-lookup"><span data-stu-id="34362-147">You'll also be able to send notifications to this app from your own Mobile Engagement instance, instead of using local notifications.</span></span>
  
  * <span data-ttu-id="34362-148">Здесь устройство можно добавить как тестовое, выбрав элемент меню **Получить идентификатор устройства** в приложении.</span><span class="sxs-lookup"><span data-stu-id="34362-148">Here you can add your device as a test device by using the **Get the Device ID** menu item in the app.</span></span> <span data-ttu-id="34362-149">Так вы получите идентификатор устройства и сможете зарегистрировать его как тестовое устройство в экземпляре серверной части платформы.</span><span class="sxs-lookup"><span data-stu-id="34362-149">This gives you a device ID that you then register as a test device with your platform back-end instance.</span></span>
    
    ![Идентификатор устройства в Windows][7]
    
    <span data-ttu-id="34362-151">![Идентификатор устройства в iOS][8]
    ![идентификатор устройства в Android][9]</span><span class="sxs-lookup"><span data-stu-id="34362-151">![Device ID on iOS][8]
![Device ID on Android][9]</span></span>

## <a name="key-features-of-the-demo-app"></a><span data-ttu-id="34362-152">Основные функции демонстрационного приложения</span><span class="sxs-lookup"><span data-stu-id="34362-152">Key features of the demo app</span></span>
* <span data-ttu-id="34362-153">Как уже говорилось, с этим приложением вы получаете все основные ресурсы Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="34362-153">As mentioned earlier, with this app, you have all the key resources for Mobile Engagement in your hand.</span></span> <span data-ttu-id="34362-154">Они доступны по ссылкам в меню слева.</span><span class="sxs-lookup"><span data-stu-id="34362-154">You can go through the links on the left menu.</span></span>
* <span data-ttu-id="34362-155">Взаимодействие с уведомлениями за пределами приложения для каждой платформы.</span><span class="sxs-lookup"><span data-stu-id="34362-155">You can experience out-of-app notifications for each platform.</span></span> <span data-ttu-id="34362-156">Эти уведомления могут доставляться в режиме **только уведомления**, когда щелчок по уведомлению открывает только собственный экран приложения (используя **глубокую связь**), или **веб-объявление**, когда при щелчке по уведомлению отображается дополнительное HTML-содержимое из серверной части Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="34362-156">These notifications can be delivered as **Notification only**, where clicking the notification simply opens up a native screen of the application (by using **deep linking**)--or as a **Web announcement**, where you can deliver additional HTML content from the Mobile Engagement back end to be displayed when the notification is clicked.</span></span>
  
    ![Внешние уведомления][29]
* <span data-ttu-id="34362-158">В iOS системные push-уведомления за пределами уведомлений можно увидеть, только закрыв приложение.</span><span class="sxs-lookup"><span data-stu-id="34362-158">On iOS, you have to close the app to see the out-of-app or system push notifications.</span></span> <span data-ttu-id="34362-159">Чтобы увидеть реализацию, добавьте **кнопки действий**, аналогичные кнопкам, добавленным в уведомление вне приложения (в данном случае *Отзыв* и *Поделиться*), чтобы пользователь мог выполнить действие прямо в уведомлении.</span><span class="sxs-lookup"><span data-stu-id="34362-159">You can look at the implementation here for adding **Action buttons**, like the ones that are added to this out-of-app notification for *Feedback* and *Share* (so that the user can take action right from the notification itself).</span></span>
  
    ![Внешние уведомления в iOS][11] ![Отображение внешних уведомлений в iOS][14]
* <span data-ttu-id="34362-162">В Android поддерживаются параметры добавления многострочного текста (**большой фрагмент текста**) или изображения в уведомлении (**Общая картина**), а также **кнопки действий**, как в iOS.</span><span class="sxs-lookup"><span data-stu-id="34362-162">On Android, the options that are supported are adding multiline text (**Big Text**) or a notification image (**Big Picture**) to the notification, along with the **Action buttons** (as supported by iOS).</span></span>
  
    ![Внешние уведомления в Android][12] ![Отображение внешних уведомлений в Android][15]
* <span data-ttu-id="34362-165">В Windows 10 уведомления выглядят как на компьютере.</span><span class="sxs-lookup"><span data-stu-id="34362-165">On Windows 10, you can see how the notifications look on the PC.</span></span> <span data-ttu-id="34362-166">Это уведомление будет также отображаться в **центре уведомлений**Windows 10.</span><span class="sxs-lookup"><span data-stu-id="34362-166">This notification also shows up in the Windows 10 **Notification Center**.</span></span> <span data-ttu-id="34362-167">В настоящее время пакет SDK для Windows не поддерживает добавление **кнопок действий** .</span><span class="sxs-lookup"><span data-stu-id="34362-167">There is no support for adding **Action buttons** at the moment in the Windows SDK.</span></span>
  
    ![Внешние уведомления в Windows][10] ![Отображение внешних уведомлений в Windows][13]
* <span data-ttu-id="34362-170">Взаимодействие с уведомлениями в приложении по умолчанию для каждой платформы.</span><span class="sxs-lookup"><span data-stu-id="34362-170">You can experience default "in-app" notifications for each platform.</span></span> <span data-ttu-id="34362-171">Это двухэтапная процедура, где сначала отображается окно **Уведомление** .</span><span class="sxs-lookup"><span data-stu-id="34362-171">This is a two-step experience where a **Notification** window is displayed first.</span></span> <span data-ttu-id="34362-172">Если вы щелкните это окно, откроется полноэкранное **Объявление**, как на представленном ниже снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="34362-172">When you click it, it opens up a full screen **Announcement**, as displayed in the following screenshot.</span></span> <span data-ttu-id="34362-173">Содержимое этого объявления берется из экземпляра серверной части Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="34362-173">The content of this announcement comes from your Mobile Engagement back-end instance.</span></span> <span data-ttu-id="34362-174">Пакет SDK содержит шаблоны для уведомлений и объявлений.</span><span class="sxs-lookup"><span data-stu-id="34362-174">The SDK has the templates for both notifications and announcements.</span></span> <span data-ttu-id="34362-175">Их можно легко настроить, как показано в этом демонстрационном приложении, добавив логотип и желаемые цвета.</span><span class="sxs-lookup"><span data-stu-id="34362-175">You can easily customize them, as shown in this demo app with the addition of our logo and coloring.</span></span>  
  
    ![Внутренние уведомления в Windows][16]
  
    ![Внутренние уведомления в iOS][17]  ![Внутренние уведомления в Android][18]
  
    <span data-ttu-id="34362-179">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="34362-179">**iOS**, **Android**</span></span>
* <span data-ttu-id="34362-180">Для настройки взаимодействия по умолчанию можно также использовать функцию **Категория** в Службах мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="34362-180">You can also use the **Category** feature of Mobile Engagement to customize this default experience.</span></span> <span data-ttu-id="34362-181">В демонстрационном приложении показаны два распространенных способа изменения взаимодействия с этими уведомлениями.</span><span class="sxs-lookup"><span data-stu-id="34362-181">In the demo app, we've demonstrated two common ways to change the experience of the notifications.</span></span> <span data-ttu-id="34362-182">Обратите внимание на то, что в пакете SDK для Windows эта функция пока не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="34362-182">Note that the Category feature is not yet supported in the Windows SDK.</span></span>
  
    <span data-ttu-id="34362-183">**Внутреннее полноэкранное представление**</span><span class="sxs-lookup"><span data-stu-id="34362-183">**Full-screen interstitial:**</span></span>
  
    ![Внутреннее уведомление — категория вставки][30]
  
    ![Категория вставки в iOS][21]     ![Категория вставки в Android][22]
  
    <span data-ttu-id="34362-187">**Всплывающее уведомление:**</span><span class="sxs-lookup"><span data-stu-id="34362-187">**Pop-up notification:**</span></span>
  
    ![Внутреннее уведомление — категория всплывающего сообщения][31]
  
    ![Всплывающее уведомление в iOS][19]    ![Всплывающее уведомление в Android][20]

<span data-ttu-id="34362-191">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="34362-191">**iOS**, **Android**</span></span>

* <span data-ttu-id="34362-192">Службы мобильного взаимодействия Azure также поддерживают особый тип внутренних уведомлений, которые называются **опросами**.</span><span class="sxs-lookup"><span data-stu-id="34362-192">Mobile Engagement also supports a specialized type of in-app notification called **Polls**.</span></span> <span data-ttu-id="34362-193">Они позволяют отправлять быстрые опросы пользователям сегментированных приложений.</span><span class="sxs-lookup"><span data-stu-id="34362-193">This allows you to send out quick surveys to your segmented app users.</span></span> <span data-ttu-id="34362-194">Для каждого вопроса можно добавить вопросы и варианты ответов (как показано на снимке экрана),</span><span class="sxs-lookup"><span data-stu-id="34362-194">You can add questions and options for each question as in the following screenshot.</span></span> <span data-ttu-id="34362-195">которые будут отображаться для пользователей приложения как внутренние уведомления.</span><span class="sxs-lookup"><span data-stu-id="34362-195">This will then get displayed as an in-app notification to the app user.</span></span>   
  
    ![Уведомления опросов][32]
  
    ![Опрос в Windows][26]
  
    ![Опрос в iOS][27]   ![Опрос в Android][28]

<span data-ttu-id="34362-200">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="34362-200">**iOS**, **Android**</span></span>

* <span data-ttu-id="34362-201">Службы мобильного взаимодействия также поддерживают автоматическую передачу уведомлений об **отправке данных**.</span><span class="sxs-lookup"><span data-stu-id="34362-201">Mobile Engagement also supports sending silent **Data Push** notifications.</span></span> <span data-ttu-id="34362-202">Это позволяет передавать определенные данные из службы, например данные JSON, как в приведенном ниже примере. Эти данные можно будет обработать в приложении и предпринять какие-то действия.</span><span class="sxs-lookup"><span data-stu-id="34362-202">With these notifications, you can send data from your service (like the JSON data in the following example), which you can handle in your app and take some action.</span></span> <span data-ttu-id="34362-203">Пример выборочного изменения цены на товар с использованием push-уведомлений об отправке данных.</span><span class="sxs-lookup"><span data-stu-id="34362-203">An example is how we're changing the price of an item selectively by using data push notifications.</span></span>
  
    ![Push-уведомление об отправке данных][33]
  
    ![Push-уведомление об отправке данных в Windows][23]
  
    ![Push-уведомление об отправке данных в iOS][24]  ![Push-уведомление об отправке данных в Android][25]

<span data-ttu-id="34362-208">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="34362-208">**iOS**, **Android**</span></span>

> [!NOTE]
> <span data-ttu-id="34362-209">Вы можете просмотреть пошаговые инструкции по любому из этих уведомлений по ссылке **Щелкните здесь, что увидеть инструкции по отправке уведомлений с платформы Служб мобильного взаимодействия** на любом экране с примером уведомления.</span><span class="sxs-lookup"><span data-stu-id="34362-209">You can view detailed step-by-step instructions for any of these notifications by clicking **Click here for instructions on how to send these notifications from Mobile Engagement platform** on any sample notification screen.</span></span>
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
