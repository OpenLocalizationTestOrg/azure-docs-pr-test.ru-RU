---
title: "Пример решения Интернета вещей Azure MyDriving: быстрый запуск | Документация Майкрософт"
description: "Начните работу с приложением, которое является примером проектирования системы IoT с помощью средств Microsoft Azure, включая Stream Analytics, машинное обучение и концентраторы событий."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 031b492df1f186087e7b91102cbb44f552999293
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="28167-103">Система IoT MyDriving: быстрый запуск</span><span class="sxs-lookup"><span data-stu-id="28167-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="28167-104">MyDriving — это система, демонстрирующая проектирование и реализацию стандартного решения [Интернета вещей](iot-suite-overview.md), которое собирает данные телеметрии с устройств, обрабатывает эти данные в облаке и применяет машинное обучение для предоставления адаптивного ответа.</span><span class="sxs-lookup"><span data-stu-id="28167-104">MyDriving is a system that demonstrates the design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in the cloud, and applies machine learning to provide an adaptive response.</span></span> <span data-ttu-id="28167-105">Демонстрация записывает сведения о ваших автомобильных поездках. Для этого используются данные с вашего мобильного телефона и адаптера, который получает информацию из системы управления вашего автомобиля.</span><span class="sxs-lookup"><span data-stu-id="28167-105">The demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="28167-106">На основе полученных данных составляется отзыв о вашем стиле вождения по сравнению с другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="28167-106">It uses this data to provide feedback on your driving style in comparison to other users.</span></span>

<span data-ttu-id="28167-107">На самом деле система MyDriving разработана для того, чтобы вы создали собственное решение IoT.</span><span class="sxs-lookup"><span data-stu-id="28167-107">The real purpose of MyDriving is to get you started in creating your own IoT solution.</span></span> <span data-ttu-id="28167-108">Так как вы являетесь участником нашей команды тестовых пользователей, сначала вам нужно ознакомиться с приложением MyDriving.</span><span class="sxs-lookup"><span data-stu-id="28167-108">But before that, let’s get you going with the MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="28167-109">Таким образом, прежде чем углубляться в изучение архитектуры, вы станете пользователем приложения и ознакомитесь с системой, с помощью которой оно создано.</span><span class="sxs-lookup"><span data-stu-id="28167-109">This gives you an experience of the app and the system behind it as a consumer, before you delve into the architecture.</span></span> <span data-ttu-id="28167-110">Кроме того, вы ознакомитесь со службой HockeyApp, с помощью которой вы сможете легко предоставлять доступ к альфа- и бета-версиям своих приложений тестовым пользователям.</span><span class="sxs-lookup"><span data-stu-id="28167-110">It also introduces you to HockeyApp, a cool way of managing the alpha and beta distributions of your apps to test users.</span></span>

## <a name="use-the-mobile-experience"></a><span data-ttu-id="28167-111">Работа с мобильным приложением</span><span class="sxs-lookup"><span data-stu-id="28167-111">Use the mobile experience</span></span>
<span data-ttu-id="28167-112">Приложение MyDriving можно использовать на устройствах Android, iOS или Windows 10.</span><span class="sxs-lookup"><span data-stu-id="28167-112">You can use the MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="28167-113">Установка на устройства Android и Windows Phone 10</span><span class="sxs-lookup"><span data-stu-id="28167-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="28167-114">На устройстве:</span><span class="sxs-lookup"><span data-stu-id="28167-114">On your device:</span></span>

1. <span data-ttu-id="28167-115">Разрешите установку приложений для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="28167-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="28167-116">Android: выберите **Параметры** > **Безопасность**, разрешите установку приложений из **неизвестных источников**.</span><span class="sxs-lookup"><span data-stu-id="28167-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="28167-117">Windows 10: выберите **Параметры** > **Обновления** > **Для разработчиков** и задайте значение **Режим разработчика**.</span><span class="sxs-lookup"><span data-stu-id="28167-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="28167-118">Присоединитесь к нашей группе бета-тестирования. Для этого зарегистрируйтесь на платформе [HockeyApp](https://rink.hockeyapp.net) или войдите в систему, если вы уже зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="28167-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="28167-119">HockeyApp позволит вам легко рассылать ознакомительные версии приложения тестовым пользователям.</span><span class="sxs-lookup"><span data-stu-id="28167-119">HockeyApp makes it easy to distribute early releases of your app to test users.</span></span>
   
   <span data-ttu-id="28167-120">(В Windows 10 используйте браузер Edge.)</span><span class="sxs-lookup"><span data-stu-id="28167-120">If you’re using Windows 10, use the Edge browser.</span></span>
   
   <span data-ttu-id="28167-121">Если вы участник Build 2016, войдите в систему с помощью учетной записи Майкрософт, под которой вы регистрировались для участия в конференции. Для этого нажмите соответствующую кнопку.</span><span class="sxs-lookup"><span data-stu-id="28167-121">If you were a Build 2016 attendee, sign in with the same Microsoft account email that you registered for the conference, by using one of the Microsoft buttons.</span></span> <span data-ttu-id="28167-122">Теперь вы зарегистрированы в HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="28167-122">You’re already signed up with HockeyApp.</span></span>
   
   ![Экран входа HockeyApp](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="28167-124">Скачайте и установите приложение по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="28167-124">Download and install the app from here:</span></span>
   
   * [<span data-ttu-id="28167-125">Android</span><span class="sxs-lookup"><span data-stu-id="28167-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="28167-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="28167-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="28167-127">Вы увидите два пункта.</span><span class="sxs-lookup"><span data-stu-id="28167-127">There are two items.</span></span> <span data-ttu-id="28167-128">Установите сертификат **доверенных лиц**.</span><span class="sxs-lookup"><span data-stu-id="28167-128">Install the certificate in **Trusted People**.</span></span> <span data-ttu-id="28167-129">а затем приложение.</span><span class="sxs-lookup"><span data-stu-id="28167-129">Then install the app.</span></span>

<span data-ttu-id="28167-130">*Возникли проблемы с запуском приложения на устройстве Windows 10 Mobile?*</span><span class="sxs-lookup"><span data-stu-id="28167-130">*Any issues starting the app on Windows 10 Mobile?*</span></span> <span data-ttu-id="28167-131">Возможно, вы не установили на телефон последние обновления.</span><span class="sxs-lookup"><span data-stu-id="28167-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="28167-132">Если дело в этом, установите следующие обновления:</span><span class="sxs-lookup"><span data-stu-id="28167-132">Make sure you've got the latest updates, or install:</span></span>

* [<span data-ttu-id="28167-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="28167-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="28167-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="28167-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="28167-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="28167-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="28167-136">Установка iOS</span><span class="sxs-lookup"><span data-stu-id="28167-136">iOS installation</span></span>
<span data-ttu-id="28167-137">Если вы участвовали в конференции Build 2016, скачайте приложение как участник команды тестирования HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="28167-137">If you attended Build 2016, download the app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="28167-138">На устройстве iOS войдите в [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="28167-138">On your iOS device, sign in to [HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="28167-139">Нажмите соответствующую кнопку, чтобы войти в систему с помощью учетной записи Майкрософт, под которой вы регистрировались для участия в конференции.</span><span class="sxs-lookup"><span data-stu-id="28167-139">Use one of the Microsoft sign-in buttons, and sign in with the same Microsoft account email that you registered with the conference.</span></span> <span data-ttu-id="28167-140">(Не вводите адрес электронной почты и пароль.)</span><span class="sxs-lookup"><span data-stu-id="28167-140">(Don’t use the email and password fields.)</span></span>
   
   ![Экран входа HockeyApp](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="28167-142">На панели мониторинга HockeyApp выберите приложение MyDriving и загрузите его.</span><span class="sxs-lookup"><span data-stu-id="28167-142">In the HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="28167-143">Авторизуйте бета-версию из службы HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="28167-143">Authorize the beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="28167-144">а.</span><span class="sxs-lookup"><span data-stu-id="28167-144">a.</span></span> <span data-ttu-id="28167-145">Выберите **Параметры** > **Общие** > **Profiles and Device Management** (Профили и управление устройствами).</span><span class="sxs-lookup"><span data-stu-id="28167-145">Go to **Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="28167-146">b.</span><span class="sxs-lookup"><span data-stu-id="28167-146">b.</span></span> <span data-ttu-id="28167-147">Обозначьте сертификат **Bit Stadium GmbH** как доверенный.</span><span class="sxs-lookup"><span data-stu-id="28167-147">Trust the **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="28167-148">Если вы не участвовали в конференции Build 2016, вы можете самостоятельно собрать и развернуть приложение.</span><span class="sxs-lookup"><span data-stu-id="28167-148">If you didn’t attend Build 2016, you can build and deploy the app yourself:</span></span>

1. <span data-ttu-id="28167-149">Скачайте код [из репозитория GitHub].</span><span class="sxs-lookup"><span data-stu-id="28167-149">Download the code [from GitHub].</span></span>
2. <span data-ttu-id="28167-150">Соберите и разверните приложение [с помощью Xamarin].</span><span class="sxs-lookup"><span data-stu-id="28167-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="28167-151">Дополнительные сведения см. в [справочном руководстве по MyDriving](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="28167-151">Find more details in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="28167-152">Получение адаптера OBD (необязательно)</span><span class="sxs-lookup"><span data-stu-id="28167-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="28167-153">Именно этот адаптер превращает решение в настоящую систему IoT.</span><span class="sxs-lookup"><span data-stu-id="28167-153">This is the part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="28167-154">Приложение можно использовать и без него, но с ним веселее. К тому же адаптер стоит недорого.</span><span class="sxs-lookup"><span data-stu-id="28167-154">You can use the app without one, but it’s more fun with the real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="28167-155">Бортовая диагностика (OBD) — это компонент автомобиля, который сотрудники СТО используют для настройки автомобиля, а также для проверки шумов и сигнальных ламп.</span><span class="sxs-lookup"><span data-stu-id="28167-155">On-board diagnostics (OBD) is the feature of your car that the garage uses to tune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="28167-156">Если ваша машина относительно новая, вы найдете в салоне сокет, который обычно находится за щитком панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="28167-156">Unless your car is of great antiquity, you’ll find a socket somewhere in the cabin, typically behind a flap under the dashboard.</span></span> <span data-ttu-id="28167-157">С подходящим соединителем вы сможете получать метрики характеристик двигателя и вносить необходимые корректировки.</span><span class="sxs-lookup"><span data-stu-id="28167-157">With the right connector, you can get metrics of the engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="28167-158">Соединитель OBD можно недорого купить в обычном магазине.</span><span class="sxs-lookup"><span data-stu-id="28167-158">An OBD connector can be purchased cheaply from the usual places.</span></span> <span data-ttu-id="28167-159">Он подключается к приложению в телефоне по Bluetooth или WiFi.</span><span class="sxs-lookup"><span data-stu-id="28167-159">It connects by using Bluetooth or Wi-Fi to an app on your phone.</span></span>

<span data-ttu-id="28167-160">В данном случае мы собираемся подключить автомобиль к облаку.</span><span class="sxs-lookup"><span data-stu-id="28167-160">In this case, we’re going to connect your car to the cloud.</span></span> <span data-ttu-id="28167-161">OBD подключается непосредственно к телефону, но установленное на нем приложение работает как ретранслятор.</span><span class="sxs-lookup"><span data-stu-id="28167-161">The direct connection from the OBD is to your phone, but our app works as a relay.</span></span> <span data-ttu-id="28167-162">Телеметрические данные автомобиля отправляются в центр IoT системы MyDriving, которая их обрабатывает, записывает ваши поездки и оценивает ваш стиль вождения.</span><span class="sxs-lookup"><span data-stu-id="28167-162">Your car's telemetry is sent straight to the MyDriving IoT hub, where it's processed to log your road trips and assess your driving style.</span></span>

<span data-ttu-id="28167-163">Подключение устройства OBD</span><span class="sxs-lookup"><span data-stu-id="28167-163">To connect an OBD device:</span></span>

1. <span data-ttu-id="28167-164">Убедитесь, что в вашем автомобиле есть сокет OBD.</span><span class="sxs-lookup"><span data-stu-id="28167-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="28167-165">Приобретите адаптер OBD.</span><span class="sxs-lookup"><span data-stu-id="28167-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="28167-166">Если ваш телефон работает под управлением Windows или Android, вам нужен адаптер OBD II с поддержкой Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="28167-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="28167-167">Мы использовали адаптер [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span><span class="sxs-lookup"><span data-stu-id="28167-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="28167-168">Если ваш телефон работает под управлением iOS, вам нужен адаптер OBD с поддержкой Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="28167-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="28167-169">Мы использовали адаптер OBD и сканер диагностики [ScanTool OBDLink MX Wi-Fi].</span><span class="sxs-lookup"><span data-stu-id="28167-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="28167-170">Подключите адаптер OBD к своему телефону, следуя приложенным к нему инструкциям.</span><span class="sxs-lookup"><span data-stu-id="28167-170">Follow the instructions that come with your OBD adapter to connect it to your phone.</span></span> <span data-ttu-id="28167-171">Помните о перечисленных ниже моментах.</span><span class="sxs-lookup"><span data-stu-id="28167-171">Keep the following in mind:</span></span>
   
   * <span data-ttu-id="28167-172">Адаптер Bluetooth необходимо связать с телефоном на странице **параметров** .</span><span class="sxs-lookup"><span data-stu-id="28167-172">A Bluetooth adapter must be paired with the phone, on the **Settings** page.</span></span>
   * <span data-ttu-id="28167-173">Адаптер Wi-Fi должен иметь адрес в диапазоне 192.168.xxx.xxx.</span><span class="sxs-lookup"><span data-stu-id="28167-173">A Wi-Fi adapter must have an address in the range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="28167-174">Если у вас несколько автомобилей, для каждого можно использовать отдельный адаптер (максимум 3).</span><span class="sxs-lookup"><span data-stu-id="28167-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="28167-175">Если у вас нет адаптера OBD, приложение все равно будет отправлять на сервер данные о местонахождении и скорости с GPS-приемника телефона и спросит вас, хотите ли вы активировать симуляцию OBD.</span><span class="sxs-lookup"><span data-stu-id="28167-175">If you don’t have an OBD adapter, the app will still send location and speed data from the phone's GPS receiver to the back end and will ask if you want to simulate an OBD.</span></span>

<span data-ttu-id="28167-176">Дополнительные сведения о том, каким образом приложение использует данные с адаптера OBD, а также о способах создания собственного устройства OBD см. в разделе 2.1 [справочного руководства по MyDriving](http://aka.ms/mydrivingdocs), который посвящен устройствам IoT.</span><span class="sxs-lookup"><span data-stu-id="28167-176">You can find out more about how the app uses data from the OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-the-app"></a><span data-ttu-id="28167-177">Использование приложения</span><span class="sxs-lookup"><span data-stu-id="28167-177">Use the app</span></span>
<span data-ttu-id="28167-178">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="28167-178">Start the app.</span></span> <span data-ttu-id="28167-179">Вам будет предложено краткое руководство по принципам его работы.</span><span class="sxs-lookup"><span data-stu-id="28167-179">There’s an initial Quickstart to walk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="28167-180">Отслеживание поездок</span><span class="sxs-lookup"><span data-stu-id="28167-180">Track your trips</span></span>
<span data-ttu-id="28167-181">Коснитесь кнопки записи (большой красный круг в нижней части экрана), чтобы начать поездку, а затем коснитесь ее еще раз, чтобы остановить запись.</span><span class="sxs-lookup"><span data-stu-id="28167-181">Tap the record button (big red circle at the bottom of the screen) to start a trip, and tap again to end.</span></span>

![Изображение кнопки записи для отслеживания поездки](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="28167-183">Если у вас нет устройства OBD, при каждом запуске поездки вас будут спрашивать, хотите ли вы использовать симулятор.</span><span class="sxs-lookup"><span data-stu-id="28167-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want to use the simulator.</span></span>

<span data-ttu-id="28167-184">В конце поездки нажмите кнопку остановки. Откроются сводные данные:</span><span class="sxs-lookup"><span data-stu-id="28167-184">At the end of a trip, tap the stop button, and you get a summary.</span></span>

![Пример сводки поездки](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="28167-186">Просмотр поездок</span><span class="sxs-lookup"><span data-stu-id="28167-186">Review your trips</span></span>
![Пример прошлой поездки](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="28167-188">Просмотр профиля</span><span class="sxs-lookup"><span data-stu-id="28167-188">Review your profile</span></span>
![Пример профиля стиля вождения](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="28167-190">Отправка тестового отзыва</span><span class="sxs-lookup"><span data-stu-id="28167-190">Send us your test feedback</span></span>
<span data-ttu-id="28167-191">Мы создали MyDriving, чтобы помочь вам ускорить начало работы с системами IoT, и непременно хотим узнать о ваших впечатлениях о работе этого решения.</span><span class="sxs-lookup"><span data-stu-id="28167-191">Because we created MyDriving to help jumpstart your own IoT systems, we certainly want to hear from you about how well it works.</span></span> <span data-ttu-id="28167-192">Сообщите нам, если во время использования приложения вы столкнулись с такими ситуациями.</span><span class="sxs-lookup"><span data-stu-id="28167-192">Let us know if:</span></span>

* <span data-ttu-id="28167-193">Возникли неполадки или проблемы.</span><span class="sxs-lookup"><span data-stu-id="28167-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="28167-194">У вас есть дополнительные замечания, которые помогут лучше адаптировать приложение для вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="28167-194">There is an extension point that would make it more suitable to your scenario.</span></span>
* <span data-ttu-id="28167-195">Вы нашли более эффективный способ выполнения определенных требований.</span><span class="sxs-lookup"><span data-stu-id="28167-195">You find a more efficient way to accomplish certain needs.</span></span>
* <span data-ttu-id="28167-196">У вас есть предложения по улучшению MyDriving или этой документации.</span><span class="sxs-lookup"><span data-stu-id="28167-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="28167-197">В приложении MyDriving можно использовать встроенный механизм обратной связи HockeyApp: просто встряхните свой телефон на базе iOS и Android или воспользуйтесь командой меню **Обратная связь** .</span><span class="sxs-lookup"><span data-stu-id="28167-197">Within the MyDriving app itself, you can use the built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use the **Feedback** menu command.</span></span> <span data-ttu-id="28167-198">К отзыву будет автоматически присоединен снимок экрана — так мы узнаем, о чем идет речь.</span><span class="sxs-lookup"><span data-stu-id="28167-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="28167-199">Если возникнут какие-то сбои, HockeyApp запишет их в журнал сбоев и сообщит о них нам.</span><span class="sxs-lookup"><span data-stu-id="28167-199">And if there are any unfortunate crashes, HockeyApp collects the crash logs to tell us about them.</span></span> <span data-ttu-id="28167-200">Вы также можете отправить отзыв через [портал HockeyApp].</span><span class="sxs-lookup"><span data-stu-id="28167-200">You can also give feedback through the [HockeyApp portal].</span></span>

<span data-ttu-id="28167-201">Кроме того, вы можете отправить [заявку в GitHub] или оставить комментарий ниже (на странице с английской версией статьи).</span><span class="sxs-lookup"><span data-stu-id="28167-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="28167-202">Мы будем рады узнать о ваших впечатлениях!</span><span class="sxs-lookup"><span data-stu-id="28167-202">We look forward to hearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="28167-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28167-203">Next steps</span></span>
* <span data-ttu-id="28167-204">Изучите [справочное руководство по MyDriving](http://aka.ms/mydrivingdocs) , чтобы узнать, каким образом мы разработали и собрали систему MyDriving.</span><span class="sxs-lookup"><span data-stu-id="28167-204">Explore the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) to understand how we’ve designed and built the entire MyDriving system.</span></span>
* <span data-ttu-id="28167-205">[Создайте и разверните собственную систему](iot-solution-build-system.md) , используя скрипты Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="28167-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="28167-206">В [справочном руководстве по MyDriving](http://aka.ms/mydrivingdocs) также описываются компоненты приложения, в которых регулируется большинство настроек.</span><span class="sxs-lookup"><span data-stu-id="28167-206">The [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make the most customizations.</span></span>

<span data-ttu-id="28167-207">[из репозитория GitHub]: https://github.com/Azure-Samples/MyDriving</span><span class="sxs-lookup"><span data-stu-id="28167-207">[from GitHub]: https://github.com/Azure-Samples/MyDriving</span></span>
<span data-ttu-id="28167-208">[с помощью Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/</span><span class="sxs-lookup"><span data-stu-id="28167-208">[using Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/</span></span>
<span data-ttu-id="28167-209">[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS</span><span class="sxs-lookup"><span data-stu-id="28167-209">[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS</span></span>
<span data-ttu-id="28167-210">[ScanTool OBDLink MX Wi-Fi]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP</span><span class="sxs-lookup"><span data-stu-id="28167-210">[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP</span></span>
<span data-ttu-id="28167-211">[портал HockeyApp]: https://rink.hockeyapp.org</span><span class="sxs-lookup"><span data-stu-id="28167-211">[HockeyApp portal]: https://rink.hockeyapp.org</span></span>
<span data-ttu-id="28167-212">[заявку в GitHub]: https://github.com/Azure-Samples/MyDriving/issues</span><span class="sxs-lookup"><span data-stu-id="28167-212">[issue on GitHub]: https://github.com/Azure-Samples/MyDriving/issues</span></span>
