---
title: "Пример решения Интернета вещей Azure MyDriving: быстрый запуск | Документация Майкрософт"
description: "Начало работы с приложением, — это комплексный Демонстрация как tooarchitect IoT систему с помощью Microsoft Azure, включая Stream Analytics, машинное обучение и концентраторов событий."
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
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="455c0-103">Система IoT MyDriving: быстрый запуск</span><span class="sxs-lookup"><span data-stu-id="455c0-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="455c0-104">MyDriving — это система, демонстрирует hello проектирование и реализацию типовой [Интернета вещей](iot-suite-overview.md) решение (IoT), которое собирает данные телеметрии с устройств, обрабатывает эти данные в облаке hello и применяет машинного обучения tooprovide адаптивного ответа.</span><span class="sxs-lookup"><span data-stu-id="455c0-104">MyDriving is a system that demonstrates hello design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in hello cloud, and applies machine learning tooprovide an adaptive response.</span></span> <span data-ttu-id="455c0-105">Демонстрация Hello записывает данные о вашей car приема-передачи, с помощью данных из мобильного телефона и адаптер, который собирает сведения из системы управления автомобиля.</span><span class="sxs-lookup"><span data-stu-id="455c0-105">hello demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="455c0-106">Ваши отзывы tooprovide данных используются на определяющим стиль сравнения tooother пользователей.</span><span class="sxs-lookup"><span data-stu-id="455c0-106">It uses this data tooprovide feedback on your driving style in comparison tooother users.</span></span>

<span data-ttu-id="455c0-107">Hello реальные MyDriving предназначен tooget запуска при создании собственного решения IoT.</span><span class="sxs-lookup"><span data-stu-id="455c0-107">hello real purpose of MyDriving is tooget you started in creating your own IoT solution.</span></span> <span data-ttu-id="455c0-108">Однако перед этим, давайте вам начать работу с hello MyDriving самого приложения — как член нашей команды тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="455c0-108">But before that, let’s get you going with hello MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="455c0-109">Это обеспечивает интерфейс приложение hello и систему hello стоящий за ней в качестве потребителя, прежде, чем углубимся в архитектуру hello.</span><span class="sxs-lookup"><span data-stu-id="455c0-109">This gives you an experience of hello app and hello system behind it as a consumer, before you delve into hello architecture.</span></span> <span data-ttu-id="455c0-110">Оно также знакомит зрителей tooHockeyApp ожиданием способ управления hello альфа-канал и бета-распределения tootest пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="455c0-110">It also introduces you tooHockeyApp, a cool way of managing hello alpha and beta distributions of your apps tootest users.</span></span>

## <a name="use-hello-mobile-experience"></a><span data-ttu-id="455c0-111">Использовать мобильные возможности hello</span><span class="sxs-lookup"><span data-stu-id="455c0-111">Use hello mobile experience</span></span>
<span data-ttu-id="455c0-112">Приложение hello MyDriving можно использовать, если у вас устройство Android, iOS или Windows 10.</span><span class="sxs-lookup"><span data-stu-id="455c0-112">You can use hello MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="455c0-113">Установка на устройства Android и Windows Phone 10</span><span class="sxs-lookup"><span data-stu-id="455c0-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="455c0-114">На устройстве:</span><span class="sxs-lookup"><span data-stu-id="455c0-114">On your device:</span></span>

1. <span data-ttu-id="455c0-115">Разрешите установку приложений для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="455c0-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="455c0-116">Android: выберите **Параметры** > **Безопасность**, разрешите установку приложений из **неизвестных источников**.</span><span class="sxs-lookup"><span data-stu-id="455c0-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="455c0-117">Windows 10: выберите **Параметры** > **Обновления** > **Для разработчиков** и задайте значение **Режим разработчика**.</span><span class="sxs-lookup"><span data-stu-id="455c0-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="455c0-118">Присоединитесь к нашей группе бета-тестирования. Для этого зарегистрируйтесь на платформе [HockeyApp](https://rink.hockeyapp.net) или войдите в систему, если вы уже зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="455c0-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="455c0-119">HockeyApp позволяет легко toodistribute ранних выпусках tootest пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="455c0-119">HockeyApp makes it easy toodistribute early releases of your app tootest users.</span></span>
   
   <span data-ttu-id="455c0-120">Если вы используете Windows 10, используйте браузер Edge hello.</span><span class="sxs-lookup"><span data-stu-id="455c0-120">If you’re using Windows 10, use hello Edge browser.</span></span>
   
   <span data-ttu-id="455c0-121">Если участник 2016 сборки, вход hello же электронной почты учетной записи Майкрософт, зарегистрированный для конференции hello, с помощью одного из hello кнопки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="455c0-121">If you were a Build 2016 attendee, sign in with hello same Microsoft account email that you registered for hello conference, by using one of hello Microsoft buttons.</span></span> <span data-ttu-id="455c0-122">Теперь вы зарегистрированы в HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="455c0-122">You’re already signed up with HockeyApp.</span></span>
   
   ![Экран входа HockeyApp](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="455c0-124">Загрузите и установите приложение hello отсюда:</span><span class="sxs-lookup"><span data-stu-id="455c0-124">Download and install hello app from here:</span></span>
   
   * [<span data-ttu-id="455c0-125">Android</span><span class="sxs-lookup"><span data-stu-id="455c0-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="455c0-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="455c0-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="455c0-127">Вы увидите два пункта.</span><span class="sxs-lookup"><span data-stu-id="455c0-127">There are two items.</span></span> <span data-ttu-id="455c0-128">Установите сертификат hello в **доверенные лица**.</span><span class="sxs-lookup"><span data-stu-id="455c0-128">Install hello certificate in **Trusted People**.</span></span> <span data-ttu-id="455c0-129">Затем установите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="455c0-129">Then install hello app.</span></span>

<span data-ttu-id="455c0-130">*Все проблемы, начиная с Windows 10 Mobile приложение hello?*</span><span class="sxs-lookup"><span data-stu-id="455c0-130">*Any issues starting hello app on Windows 10 Mobile?*</span></span> <span data-ttu-id="455c0-131">Возможно, вы не установили на телефон последние обновления.</span><span class="sxs-lookup"><span data-stu-id="455c0-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="455c0-132">Убедитесь в том, есть последние обновления hello, или установить:</span><span class="sxs-lookup"><span data-stu-id="455c0-132">Make sure you've got hello latest updates, or install:</span></span>

* [<span data-ttu-id="455c0-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="455c0-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="455c0-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="455c0-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="455c0-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="455c0-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="455c0-136">Установка iOS</span><span class="sxs-lookup"><span data-stu-id="455c0-136">iOS installation</span></span>
<span data-ttu-id="455c0-137">Если вы ходили 2016 сборки, загрузите приложение hello членом нашей команды тестирования на HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="455c0-137">If you attended Build 2016, download hello app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="455c0-138">На устройстве iOS вход слишком[HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="455c0-138">On your iOS device, sign in too[HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="455c0-139">Используйте один из кнопки входа Microsoft hello, а вход с использованием hello же электронной почты учетной записи Майкрософт, зарегистрированный с конференции hello.</span><span class="sxs-lookup"><span data-stu-id="455c0-139">Use one of hello Microsoft sign-in buttons, and sign in with hello same Microsoft account email that you registered with hello conference.</span></span> <span data-ttu-id="455c0-140">(Не используйте поля hello электронной почты и пароль).</span><span class="sxs-lookup"><span data-stu-id="455c0-140">(Don’t use hello email and password fields.)</span></span>
   
   ![Экран входа HockeyApp](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="455c0-142">В панели мониторинга HockeyApp hello выберите MyDriving и загрузить его.</span><span class="sxs-lookup"><span data-stu-id="455c0-142">In hello HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="455c0-143">Авторизация hello бета-версию HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="455c0-143">Authorize hello beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="455c0-144">а.</span><span class="sxs-lookup"><span data-stu-id="455c0-144">a.</span></span> <span data-ttu-id="455c0-145">Go слишком**параметры** > **Общие** > **профилей и управления устройствами.**</span><span class="sxs-lookup"><span data-stu-id="455c0-145">Go too**Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="455c0-146">b.</span><span class="sxs-lookup"><span data-stu-id="455c0-146">b.</span></span> <span data-ttu-id="455c0-147">Доверять hello **GmbH стадиона бит** сертификат.</span><span class="sxs-lookup"><span data-stu-id="455c0-147">Trust hello **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="455c0-148">Если вы не смогли поступить 2016 сборки, можно построить и развернуть приложение hello самостоятельно:</span><span class="sxs-lookup"><span data-stu-id="455c0-148">If you didn’t attend Build 2016, you can build and deploy hello app yourself:</span></span>

1. <span data-ttu-id="455c0-149">Загрузка кода hello [из GitHub].</span><span class="sxs-lookup"><span data-stu-id="455c0-149">Download hello code [from GitHub].</span></span>
2. <span data-ttu-id="455c0-150">Соберите и разверните приложение [с помощью Xamarin].</span><span class="sxs-lookup"><span data-stu-id="455c0-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="455c0-151">Найти дополнительные сведения в hello [MyDriving справочник](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="455c0-151">Find more details in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="455c0-152">Получение адаптера OBD (необязательно)</span><span class="sxs-lookup"><span data-stu-id="455c0-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="455c0-153">Это часть hello, делает это в реальной системе Интернета вещей!</span><span class="sxs-lookup"><span data-stu-id="455c0-153">This is hello part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="455c0-154">Можно использовать приложение hello без одного, но это развлечений реально hello и они не являются ресурсоемким.</span><span class="sxs-lookup"><span data-stu-id="455c0-154">You can use hello app without one, but it’s more fun with hello real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="455c0-155">Встроенный диагностики (OBD) — функция hello автомобиле, hello tootune гараже использует копирование автомобиле и диагностики нечетное шумы и ламп предупреждение.</span><span class="sxs-lookup"><span data-stu-id="455c0-155">On-board diagnostics (OBD) is hello feature of your car that hello garage uses tootune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="455c0-156">Если автомобиль имеет значительные античных времен, вы найдете сокета в любом месте в камера hello, обычно за внутрь под hello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="455c0-156">Unless your car is of great antiquity, you’ll find a socket somewhere in hello cabin, typically behind a flap under hello dashboard.</span></span> <span data-ttu-id="455c0-157">С соединителем правой hello можно получить метрики производительности подсистемы hello и внести некоторые изменения.</span><span class="sxs-lookup"><span data-stu-id="455c0-157">With hello right connector, you can get metrics of hello engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="455c0-158">Соединитель OBD можно приобрести экономно из мест обычные hello.</span><span class="sxs-lookup"><span data-stu-id="455c0-158">An OBD connector can be purchased cheaply from hello usual places.</span></span> <span data-ttu-id="455c0-159">Он подключается, используя приложение tooan Bluetooth или Wi-Fi на телефоне.</span><span class="sxs-lookup"><span data-stu-id="455c0-159">It connects by using Bluetooth or Wi-Fi tooan app on your phone.</span></span>

<span data-ttu-id="455c0-160">В этом случае мы используем tooconnect облако toohello автомобиля.</span><span class="sxs-lookup"><span data-stu-id="455c0-160">In this case, we’re going tooconnect your car toohello cloud.</span></span> <span data-ttu-id="455c0-161">Hello прямое подключение от hello OBD является tooyour телефона, но работает нашего приложения в качестве ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="455c0-161">hello direct connection from hello OBD is tooyour phone, but our app works as a relay.</span></span> <span data-ttu-id="455c0-162">Телеметрии автомобиля отправляется прямой toohello центр MyDriving IoT, там, где это обработки toolog вашей пройденным и оценить определяющим стилем.</span><span class="sxs-lookup"><span data-stu-id="455c0-162">Your car's telemetry is sent straight toohello MyDriving IoT hub, where it's processed toolog your road trips and assess your driving style.</span></span>

<span data-ttu-id="455c0-163">tooconnect OBD устройства:</span><span class="sxs-lookup"><span data-stu-id="455c0-163">tooconnect an OBD device:</span></span>

1. <span data-ttu-id="455c0-164">Убедитесь, что в вашем автомобиле есть сокет OBD.</span><span class="sxs-lookup"><span data-stu-id="455c0-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="455c0-165">Приобретите адаптер OBD.</span><span class="sxs-lookup"><span data-stu-id="455c0-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="455c0-166">Если ваш телефон работает под управлением Windows или Android, вам нужен адаптер OBD II с поддержкой Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="455c0-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="455c0-167">Мы использовали адаптер [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span><span class="sxs-lookup"><span data-stu-id="455c0-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="455c0-168">Если ваш телефон работает под управлением iOS, вам нужен адаптер OBD с поддержкой Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="455c0-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="455c0-169">Мы использовали адаптер OBD и сканер диагностики [ScanTool OBDLink MX Wi-Fi].</span><span class="sxs-lookup"><span data-stu-id="455c0-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="455c0-170">Следуйте инструкциям hello, входящие в состав вашей tooconnect адаптера OBD его tooyour телефона.</span><span class="sxs-lookup"><span data-stu-id="455c0-170">Follow hello instructions that come with your OBD adapter tooconnect it tooyour phone.</span></span> <span data-ttu-id="455c0-171">Следующие hello Имейте в виду.</span><span class="sxs-lookup"><span data-stu-id="455c0-171">Keep hello following in mind:</span></span>
   
   * <span data-ttu-id="455c0-172">Адаптер Bluetooth должны составлять пару с телефона hello, на hello **параметры** страницы.</span><span class="sxs-lookup"><span data-stu-id="455c0-172">A Bluetooth adapter must be paired with hello phone, on hello **Settings** page.</span></span>
   * <span data-ttu-id="455c0-173">Адаптер Wi-Fi должны иметь адрес в диапазоне 192.168.xxx.xxx hello.</span><span class="sxs-lookup"><span data-stu-id="455c0-173">A Wi-Fi adapter must have an address in hello range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="455c0-174">Если у вас несколько автомобилей, для каждого можно использовать отдельный адаптер (максимум 3).</span><span class="sxs-lookup"><span data-stu-id="455c0-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="455c0-175">Если у вас нет OBD адаптер, приложение hello по-прежнему отправлять, расположение данных о скорости toohello приемника GPS hello phone назад и заканчиваться запросит, если toosimulate OBD.</span><span class="sxs-lookup"><span data-stu-id="455c0-175">If you don’t have an OBD adapter, hello app will still send location and speed data from hello phone's GPS receiver toohello back end and will ask if you want toosimulate an OBD.</span></span>

<span data-ttu-id="455c0-176">Дополнительная информация об использовании данных из адаптера OBD hello приложение hello и о способах создания OBD устройства в разделе 2.1, «Устройств IoT» можно найти в hello [MyDriving справочник](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="455c0-176">You can find out more about how hello app uses data from hello OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-hello-app"></a><span data-ttu-id="455c0-177">Используйте приложение hello</span><span class="sxs-lookup"><span data-stu-id="455c0-177">Use hello app</span></span>
<span data-ttu-id="455c0-178">Запуск приложения hello.</span><span class="sxs-lookup"><span data-stu-id="455c0-178">Start hello app.</span></span> <span data-ttu-id="455c0-179">Отсутствует исходный toowalk краткое руководство по работе.</span><span class="sxs-lookup"><span data-stu-id="455c0-179">There’s an initial Quickstart toowalk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="455c0-180">Отслеживание поездок</span><span class="sxs-lookup"><span data-stu-id="455c0-180">Track your trips</span></span>
<span data-ttu-id="455c0-181">Коснитесь toostart записи кнопки (большой красный кружок hello нижней части экрана приветствия) hello маршрута и снова tooend.</span><span class="sxs-lookup"><span data-stu-id="455c0-181">Tap hello record button (big red circle at hello bottom of hello screen) toostart a trip, and tap again tooend.</span></span>

![Изображение кнопки hello запись для отслеживания обработки](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="455c0-183">Каждый раз при запуске маршрута, если устройство не OBD, запросит следует toouse hello симулятора.</span><span class="sxs-lookup"><span data-stu-id="455c0-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want toouse hello simulator.</span></span>

<span data-ttu-id="455c0-184">В конце обработки hello коснитесь кнопки hello и получить сводку.</span><span class="sxs-lookup"><span data-stu-id="455c0-184">At hello end of a trip, tap hello stop button, and you get a summary.</span></span>

![Пример сводки поездки](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="455c0-186">Просмотр поездок</span><span class="sxs-lookup"><span data-stu-id="455c0-186">Review your trips</span></span>
![Пример прошлой поездки](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="455c0-188">Просмотр профиля</span><span class="sxs-lookup"><span data-stu-id="455c0-188">Review your profile</span></span>
![Пример профиля стиля вождения](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="455c0-190">Отправка тестового отзыва</span><span class="sxs-lookup"><span data-stu-id="455c0-190">Send us your test feedback</span></span>
<span data-ttu-id="455c0-191">Поскольку мы создали введение toohelp MyDriving IoT системах, мы хотим наверняка toohear от вас о того, насколько хорошо он работает.</span><span class="sxs-lookup"><span data-stu-id="455c0-191">Because we created MyDriving toohelp jumpstart your own IoT systems, we certainly want toohear from you about how well it works.</span></span> <span data-ttu-id="455c0-192">Сообщите нам, если во время использования приложения вы столкнулись с такими ситуациями.</span><span class="sxs-lookup"><span data-stu-id="455c0-192">Let us know if:</span></span>

* <span data-ttu-id="455c0-193">Возникли неполадки или проблемы.</span><span class="sxs-lookup"><span data-stu-id="455c0-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="455c0-194">Является точкой расширения, делает более подходящими tooyour сценария.</span><span class="sxs-lookup"><span data-stu-id="455c0-194">There is an extension point that would make it more suitable tooyour scenario.</span></span>
* <span data-ttu-id="455c0-195">Найти более эффективным способом tooaccomplish определенных требований.</span><span class="sxs-lookup"><span data-stu-id="455c0-195">You find a more efficient way tooaccomplish certain needs.</span></span>
* <span data-ttu-id="455c0-196">У вас есть предложения по улучшению MyDriving или этой документации.</span><span class="sxs-lookup"><span data-stu-id="455c0-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="455c0-197">Hello MyDriving само приложение, вы можете использовать hello встроенный механизм обратной связи HockeyApp: в iOS и Android, просто назначьте телефоне встряхивания или использовать hello **отзывы** команду меню.</span><span class="sxs-lookup"><span data-stu-id="455c0-197">Within hello MyDriving app itself, you can use hello built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use hello **Feedback** menu command.</span></span> <span data-ttu-id="455c0-198">К отзыву будет автоматически присоединен снимок экрана — так мы узнаем, о чем идет речь.</span><span class="sxs-lookup"><span data-stu-id="455c0-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="455c0-199">И в случае любой нежелательным сбоев HockeyApp сбор tootell журналы аварийных hello нам о них.</span><span class="sxs-lookup"><span data-stu-id="455c0-199">And if there are any unfortunate crashes, HockeyApp collects hello crash logs tootell us about them.</span></span> <span data-ttu-id="455c0-200">Можно также предоставить отзыв о программе hello [портале HockeyApp].</span><span class="sxs-lookup"><span data-stu-id="455c0-200">You can also give feedback through hello [HockeyApp portal].</span></span>

<span data-ttu-id="455c0-201">Кроме того, вы можете отправить [заявку в GitHub] или оставить комментарий ниже (на странице с английской версией статьи).</span><span class="sxs-lookup"><span data-stu-id="455c0-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="455c0-202">Мы будем toohearing вашим отзывам.</span><span class="sxs-lookup"><span data-stu-id="455c0-202">We look forward toohearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="455c0-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="455c0-203">Next steps</span></span>
* <span data-ttu-id="455c0-204">Просмотр hello [MyDriving справочник](http://aka.ms/mydrivingdocs) toounderstand как мы разрабатываются и создаются hello всей системы MyDriving.</span><span class="sxs-lookup"><span data-stu-id="455c0-204">Explore hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) toounderstand how we’ve designed and built hello entire MyDriving system.</span></span>
* <span data-ttu-id="455c0-205">[Создайте и разверните собственную систему](iot-solution-build-system.md) , используя скрипты Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="455c0-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="455c0-206">Hello [MyDriving справочник](http://aka.ms/mydrivingdocs) также поможет областей, где вы будет вносить hello большая часть настроек.</span><span class="sxs-lookup"><span data-stu-id="455c0-206">hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make hello most customizations.</span></span>

[из GitHub]: https://github.com/Azure-Samples/MyDriving
[с помощью Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[портале HockeyApp]: https://rink.hockeyapp.org
[заявку в GitHub]: https://github.com/Azure-Samples/MyDriving/issues
