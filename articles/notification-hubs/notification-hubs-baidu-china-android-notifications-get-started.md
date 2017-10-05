---
title: "Приступая к работе с Центрами уведомлений Azure с помощью Baidu | Документация Майкрософт"
description: "Из этого учебника вы узнаете, как использовать Центры уведомлений Azure для отправки push-уведомлений на устройства Android с помощью Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: df3bbda15e1245b6068c2b8290d0c96856051f1f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="84799-103">Приступая к работе с Центрами уведомлений с помощью Baidu</span><span class="sxs-lookup"><span data-stu-id="84799-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="84799-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="84799-104">Overview</span></span>
<span data-ttu-id="84799-105">Push-облако Baidu — это китайская облачная служба, которую можно использовать для отправки push-уведомлений на мобильные устройства.</span><span class="sxs-lookup"><span data-stu-id="84799-105">Baidu cloud push is a Chinese cloud service that you can use to send push notifications to mobile devices.</span></span> <span data-ttu-id="84799-106">Эта служба особенно полезна в Китае, где доставка push-уведомлений на устройства под управлением Android усложняется наличием различных магазинов приложений и служб push-уведомлений, а также доступностью устройств Android, которые обычно не подключены к службе GCM (Google Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="84799-106">This service is useful in China, where delivering push notifications to Android is complex because of the presence of different app stores and push services, in addition to the availability of Android devices that are not typically connected to GCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84799-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="84799-107">Prerequisites</span></span>
<span data-ttu-id="84799-108">Для работы с руководством требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="84799-108">This tutorial requires:</span></span>

* <span data-ttu-id="84799-109">Пакет SDK для Android (предполагается, что вы используете Eclipse), который можно скачать с <a href="http://go.microsoft.com/fwlink/?LinkId=389797">сайта Android</a>.</span><span class="sxs-lookup"><span data-stu-id="84799-109">Android SDK (we assume that you use Eclipse), which you can download from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="84799-110">[Пакет Android SDK для мобильных служб]</span><span class="sxs-lookup"><span data-stu-id="84799-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="84799-111">[Пакет Android SDK для Baidu Push]</span><span class="sxs-lookup"><span data-stu-id="84799-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="84799-112">Для работы с этим учебником необходима активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="84799-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="84799-113">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="84799-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="84799-114">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="84799-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="84799-115">Создание учетной записи Baidu</span><span class="sxs-lookup"><span data-stu-id="84799-115">Create a Baidu account</span></span>
<span data-ttu-id="84799-116">Чтобы использовать Baidu, необходимо иметь учетную запись Baidu.</span><span class="sxs-lookup"><span data-stu-id="84799-116">To use Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="84799-117">Если она у вас уже есть, войдите на [портал Baidu] и перейдите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="84799-117">If you already have one, log in to the [Baidu portal] and skip to the next step.</span></span> <span data-ttu-id="84799-118">В противном случае создайте учетную запись Baidu, следуя приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="84799-118">Otherwise, see the following instructions on how to create a Baidu account.</span></span>  

1. <span data-ttu-id="84799-119">Откройте [портал Baidu] и перейдите по ссылке **登录** (**Вход**).</span><span class="sxs-lookup"><span data-stu-id="84799-119">Go to the [Baidu portal] and click the **登录** (**Login**) link.</span></span> <span data-ttu-id="84799-120">Щелкните **立即注册** , чтобы начать процесс регистрации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="84799-120">Click **立即注册** to start the account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="84799-121">Введите требуемые сведения — номер телефона и/или адрес электронной почты, пароль и код подтверждения, — а затем нажмите кнопку **Signup**(Зарегистрироваться).</span><span class="sxs-lookup"><span data-stu-id="84799-121">Enter the required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="84799-122">На указанный вами адрес электронной почты будет отправлено сообщение со ссылкой для активации учетной записи Baidu.</span><span class="sxs-lookup"><span data-stu-id="84799-122">You will be sent an email to the email address that you entered with a link to activate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="84799-123">Войдите в свой почтовый ящик, откройте это сообщение и перейдите по ссылке, чтобы активировать учетную запись Baidu.</span><span class="sxs-lookup"><span data-stu-id="84799-123">Log in to your email account, open the Baidu activation mail, and click the activation link to activate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="84799-124">После активации войдите на [портал Baidu]с помощью созданной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="84799-124">Once you have an activated Baidu account, log in to the [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="84799-125">Регистрация в качестве разработчика Baidu</span><span class="sxs-lookup"><span data-stu-id="84799-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="84799-126">После входа на [портал Baidu] щелкните **更多>>** (**Дополнительно**).</span><span class="sxs-lookup"><span data-stu-id="84799-126">Once you have logged in to the [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="84799-127">Прокрутите вниз раздел **站长与开发者服务 (Службы для веб-мастеров и разработчиков)** и щелкните **百度开放云平台** (**Открытая облачная платформа Baidu**).</span><span class="sxs-lookup"><span data-stu-id="84799-127">Scroll down in the **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="84799-128">В правом верхнем углу следующей страницы щелкните пункт **开发者服务** (**Службы для разработчиков**).</span><span class="sxs-lookup"><span data-stu-id="84799-128">On the next page, click **开发者服务** (**Developer Services**) on the top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="84799-129">На следующей странице в меню в правом верхнем углу щелкните пункт **注册开发者** (**Зарегистрированные разработчики**).</span><span class="sxs-lookup"><span data-stu-id="84799-129">On the next page, click **注册开发者** (**Registered Developers**) from the menu on the top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="84799-130">Введите свое имя, описание и номер мобильного телефона, чтобы получить текстовое сообщение для проверки подлинности, а затем щелкните **送验证码** (**Отправить код проверки**).</span><span class="sxs-lookup"><span data-stu-id="84799-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="84799-131">Код страны для международных номеров необходимо заключить в круглые скобки.</span><span class="sxs-lookup"><span data-stu-id="84799-131">For international phone numbers, you need to enclose the country code in parentheses.</span></span> <span data-ttu-id="84799-132">Например, номер телефона в США выглядит так: **(1)1234567890**.</span><span class="sxs-lookup"><span data-stu-id="84799-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="84799-133">После этого вы должны получить текстовое сообщение с номером проверки, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="84799-133">You should then receive a text message with a verification number, as shown in the following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="84799-134">Введите код проверки из сообщения в поле **验证码** (**Код подтверждения**).</span><span class="sxs-lookup"><span data-stu-id="84799-134">Enter the verification number from the message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="84799-135">Наконец, для завершения регистрации разработчика примите соглашение Baidu и щелкните **提交** (**Отправить**).</span><span class="sxs-lookup"><span data-stu-id="84799-135">Finally, complete the developer registration by accepting the Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="84799-136">При успешном завершении регистрации появится следующая страница:</span><span class="sxs-lookup"><span data-stu-id="84799-136">You will see the following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="84799-137">Создание облачного push-проекта Baidu</span><span class="sxs-lookup"><span data-stu-id="84799-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="84799-138">Во время создания push-проекта Baidu вы получите код приложения, ключ API и секретный ключ.</span><span class="sxs-lookup"><span data-stu-id="84799-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="84799-139">После входа на [портал Baidu] щелкните **更多>>** (**Дополнительно**).</span><span class="sxs-lookup"><span data-stu-id="84799-139">Once you have logged in to the [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="84799-140">Прокрутите вниз раздел **站长与开发者服务** (**Службы для веб-мастеров и разработчиков**) и щелкните **百度开放云平台** (**Открытая облачная платформа Baidu**).</span><span class="sxs-lookup"><span data-stu-id="84799-140">Scroll down in the **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="84799-141">В правом верхнем углу следующей страницы щелкните пункт **开发者服务** (**Службы для разработчиков**).</span><span class="sxs-lookup"><span data-stu-id="84799-141">On the next page, click **开发者服务** (**Developer Services**) on the top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="84799-142">На следующей странице щелкните **云推送** (**Служба push-уведомлений облака**) в разделе **云服务** (**Облачные службы**).</span><span class="sxs-lookup"><span data-stu-id="84799-142">On the next page, click **云推送** (**Cloud Push**) from the **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="84799-143">По завершении регистрации разработчика в верхнем меню появится пункт **管理控制台** (**Консоль управления**).</span><span class="sxs-lookup"><span data-stu-id="84799-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at the top menu.</span></span> <span data-ttu-id="84799-144">Щелкните **开发者服务管理** (**Управление службой разработки**).</span><span class="sxs-lookup"><span data-stu-id="84799-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="84799-145">На следующей странице щелкните **创建工程** (**Создать проект**).</span><span class="sxs-lookup"><span data-stu-id="84799-145">On the next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="84799-146">Введите имя приложения и щелкните **创建** (**Создать**).</span><span class="sxs-lookup"><span data-stu-id="84799-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="84799-147">После успешного создания проекта службы push-уведомлений облака Baidu отобразится страница с **идентификатором приложения**, **ключом API** и **секретным ключом**.</span><span class="sxs-lookup"><span data-stu-id="84799-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="84799-148">Запишите ключ API и секретный ключ, которые будут использоваться позже.</span><span class="sxs-lookup"><span data-stu-id="84799-148">Make a note of the API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="84799-149">Настройте проект для отправки push-уведомлений, щелкнув **云推送** (**Служба push-уведомлений облака**) на панели слева.</span><span class="sxs-lookup"><span data-stu-id="84799-149">Configure the project for push notifications by clicking **云推送** (**Cloud Push**) on the left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="84799-150">На следующей странице нажмите кнопку **推送设置** (**Параметры push-уведомлений**).</span><span class="sxs-lookup"><span data-stu-id="84799-150">On the next page, click the **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="84799-151">На странице настроек добавьте имя пакета, который вы будете использовать в своем проекте Android, в поле **应用包名** (**Пакет приложения**) и щелкните **保存设置** (**Сохранить**).</span><span class="sxs-lookup"><span data-stu-id="84799-151">On the configuration page, add the package name that you will be using in your Android project in the **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="84799-152">Отобразится сообщение: **保存成功！** (**Успешно сохранено!)**.</span><span class="sxs-lookup"><span data-stu-id="84799-152">You see the **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="84799-153">Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="84799-153">Configure your notification hub</span></span>
1. <span data-ttu-id="84799-154">Войдите на [классический портал Azure]и в нижней части экрана нажмите кнопку **+Создать** .</span><span class="sxs-lookup"><span data-stu-id="84799-154">Sign in to the [Azure Classic Portal], and then click **+NEW** at the bottom of the screen.</span></span>
2. <span data-ttu-id="84799-155">Щелкните **Службы приложений**, выберите **Служебная шина**, затем щелкните **Центр уведомлений** и нажмите кнопку **Быстро создать**.</span><span class="sxs-lookup"><span data-stu-id="84799-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="84799-156">Введите имя **центра уведомлений**, затем выберите **регион** и **пространство имен**, в котором будет создан этот центр уведомлений. После этого щелкните **Создать центр уведомлений**.</span><span class="sxs-lookup"><span data-stu-id="84799-156">Provide a name for your **Notification Hub**, select the **Region** and the **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="84799-157">Выберите пространство имен, в котором создан концентратор уведомлений, и щелкните вверху **Концентраторы уведомлений** .</span><span class="sxs-lookup"><span data-stu-id="84799-157">Click the namespace in which you created your notification hub, and then click **Notification Hubs** at the top.</span></span>
   
      ![][18]
5. <span data-ttu-id="84799-158">Выделите созданный концентратор уведомлений и в верхнем меню выберите пункт **Настройка** .</span><span class="sxs-lookup"><span data-stu-id="84799-158">Select the notification hub that you created, and then click **Configure** from the top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="84799-159">Прокрутите вниз до раздела **Параметры уведомлений Baidu** , а затем введите ключ API и секретный ключ, полученные ранее для службы передачи данных в облако Baidu из консоли Baidu.</span><span class="sxs-lookup"><span data-stu-id="84799-159">Scroll down to the **baidu notification settings** section and enter the API key and secret key that you obtained from the Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="84799-160">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="84799-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="84799-161">Откройте вкладку **Панель мониторинга** в верхней части меню центра уведомлений и щелкните **Просмотреть строку подключения**.</span><span class="sxs-lookup"><span data-stu-id="84799-161">Click the **Dashboard** tab at the top for the notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="84799-162">Запишите значения **DefaultListenSharedAccessSignature** и **DefaultFullSharedAccessSignature**, отображенные в окне **Сведения по доступу к подключению**.</span><span class="sxs-lookup"><span data-stu-id="84799-162">Make a note of the **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from the **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="84799-163">Подключение приложения к центру уведомлений</span><span class="sxs-lookup"><span data-stu-id="84799-163">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="84799-164">В ADT Eclipse создайте новый проект Android (**Файл** > **Создать** > **Проект приложения Android**).</span><span class="sxs-lookup"><span data-stu-id="84799-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="84799-165">Введите **имя приложения** и убедитесь, что для параметра **Минимальная требуемая версия пакета SDK** указано значение **API 16: Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="84799-165">Enter an **Application Name** and ensure that the **Minimum Required SDK** version is set to **API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="84799-166">Нажмите кнопку **Далее** и следуйте указаниям мастера до появления окна **Создать действие**.</span><span class="sxs-lookup"><span data-stu-id="84799-166">Click **Next** and continue following the wizard until the **Create Activity** window appears.</span></span> <span data-ttu-id="84799-167">Выберите элемент **Пустое действие** и нажмите кнопку **Готово**, чтобы создать новое приложение Android.</span><span class="sxs-lookup"><span data-stu-id="84799-167">Make sure that **Blank Activity** is selected, and finally select **Finish** to create a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="84799-168">Убедитесь, что значение параметра **Целевая сборка проекта** задано правильно.</span><span class="sxs-lookup"><span data-stu-id="84799-168">Make sure that the **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="84799-169">На странице **Notification-Hubs-Android-SDK сайта Bintray** на вкладке [Files](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4)(Файлы) скачайте файл notification-hubs-0.4.jar.</span><span class="sxs-lookup"><span data-stu-id="84799-169">Download the notification-hubs-0.4.jar file from the **Files** tab of the [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="84799-170">Добавьте файл в папку **libs** проекта Eclipse и обновите папку *libs* .</span><span class="sxs-lookup"><span data-stu-id="84799-170">Add the file to the **libs** folder of your Eclipse project, and refresh the *libs* folder.</span></span>
6. <span data-ttu-id="84799-171">Скачайте и распакуйте [Пакет Android SDK для Baidu Push], откройте папку **libs** и скопируйте JAR-файл **pushservice-x.y.z**, а также папки **armeabi** &  и **mips** в папке **libs** приложения Android.</span><span class="sxs-lookup"><span data-stu-id="84799-171">Download and unzip the [Baidu Push Android SDK], open the **libs** folder, and then copy the **pushservice-x.y.z** jar file and the **armeabi** & **mips** folders in the **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="84799-172">Откройте файл **AndroidManifest.xml** проекта Android и добавьте разрешения, требуемые пакетом SDK для Baidu.</span><span class="sxs-lookup"><span data-stu-id="84799-172">Open the **AndroidManifest.xml** file of your Android project and add the permissions that are required by the Baidu SDK.</span></span>
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. <span data-ttu-id="84799-173">Добавьте свойство **android:name** в элемент **application** файла **AndroidManifest.xml**, заменив *yourprojectname* собственным значением (например, **com.example.BaiduTest**).</span><span class="sxs-lookup"><span data-stu-id="84799-173">Add the **android:name** property to your **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="84799-174">Убедитесь, что имя этого проекта соответствует имени, заданному в консоли Baidu.</span><span class="sxs-lookup"><span data-stu-id="84799-174">Make sure that this project name matches the one that you configured in the Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="84799-175">Добавьте следующую конфигурацию в элементе приложения после элемента действия **.MainActivity**, заменив *yourprojectname* собственным значением (например, **com.example.BaiduTest**):</span><span class="sxs-lookup"><span data-stu-id="84799-175">Add the following configuration within the application element after the **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. <span data-ttu-id="84799-176">Добавьте в проект новый класс с именем **ConfigurationSettings.java** .</span><span class="sxs-lookup"><span data-stu-id="84799-176">Add a new class called **ConfigurationSettings.java** to the project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="84799-177">Добавьте в класс следующий код:</span><span class="sxs-lookup"><span data-stu-id="84799-177">Add the following code to it:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="84799-178">Присвойте параметру **API_KEY** значение, которое вы получили ранее из облачного проекта Baidu, а параметрам **NotificationHubName** и **NotificationHubConnectionString** — полученные на классическом портале Azure имя вашего центра уведомлений и значение DefaultListenSharedAccessSignature соответственно.</span><span class="sxs-lookup"><span data-stu-id="84799-178">Set the value of **API_KEY** with what you retrieved from the Baidu cloud project earlier, **NotificationHubName** with your notification hub name from the Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from the Azure Classic Portal.</span></span>
12. <span data-ttu-id="84799-179">Добавьте новый класс с именем **DemoApplication.java**, затем добавьте в него следующий код:</span><span class="sxs-lookup"><span data-stu-id="84799-179">Add a new class called **DemoApplication.java**, and add the following code to it:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="84799-180">Добавьте еще один новый класс с именем **MyPushMessageReceiver.java** и добавьте в него указанный ниже код.</span><span class="sxs-lookup"><span data-stu-id="84799-180">Add another new class called **MyPushMessageReceiver.java**, and add the following code to it.</span></span> <span data-ttu-id="84799-181">Это класс, который обрабатывает push-уведомления, полученные от push-сервера Baidu.</span><span class="sxs-lookup"><span data-stu-id="84799-181">It is the class that handles the push notifications that are received from the Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG to Log */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. <span data-ttu-id="84799-182">Откройте класс **MainActivity.java** и добавьте следующий код в метод **onCreate**.</span><span class="sxs-lookup"><span data-stu-id="84799-182">Open **MainActivity.java**, and add the following to the **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="84799-183">Затем добавьте следующие инструкции импорта в начало.</span><span class="sxs-lookup"><span data-stu-id="84799-183">Open the following import statements at the top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-to-your-app"></a><span data-ttu-id="84799-184">Отправка уведомлений в приложение</span><span class="sxs-lookup"><span data-stu-id="84799-184">Send notifications to your app</span></span>
<span data-ttu-id="84799-185">Вы можете быстро проверить получение уведомлений в приложении. Для этого отправьте уведомление на [портале Azure](https://portal.azure.com/), нажав кнопку **Отправить** в центре уведомлений, как показано на снимке экрана ниже:</span><span class="sxs-lookup"><span data-stu-id="84799-185">You can quickly test receiving notifications in your app by sending notifications in the [Azure portal](https://portal.azure.com/) using the **Send** button on the notification hub, as shown in the following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="84799-186">Push-уведомления обычно отправляются в серверной службе, например мобильными службами или ASP.NET, с помощью совместимой библиотеки.</span><span class="sxs-lookup"><span data-stu-id="84799-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="84799-187">Если для серверной части библиотека недоступна, можно напрямую использовать REST API для отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="84799-187">If a library is not available for your back-end, you can use the REST API directly to send notification messages .</span></span>

<span data-ttu-id="84799-188">В этом руководстве мы покажем простой пример тестирования клиентского приложения, в котором уведомление отправляется с помощью пакета SDK для .NET для центров уведомлений не в серверную службу, а в консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="84799-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="84799-189">В качестве следующего шага по отправке уведомлений с сервера ASP.NET рекомендуем ознакомиться с руководством [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="84799-189">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="84799-190">Можно использовать следующие способы отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="84799-190">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="84799-191">**Интерфейс REST**. [Интерфейс REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx) поддерживает уведомления на любой серверной платформе.</span><span class="sxs-lookup"><span data-stu-id="84799-191">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="84799-192">**Пакет SDK .NET для Центров уведомлений Microsoft Azure**. В диспетчере пакетов NuGet для Visual Studio выполните команду [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="84799-192">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="84799-193">**Node.js**. [Отправка push-уведомлений с помощью Центров уведомлений Azure и Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="84799-193">**Node.js**: [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="84799-194">**Мобильные приложения**. Пример отправки уведомлений с сервера мобильных приложений службы приложений Azure, интегрированного с центрами уведомлений, см. в статье [Добавление push-уведомлений в приложение iOS](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="84799-194">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="84799-195">**Java или PHP**. Примеры отправки уведомлений с использованием REST API см. в статьях "Использование концентраторов уведомлений из Java и "Использование концентраторов уведомлений из PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="84799-195">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="84799-196">(Необязательно) Отправление уведомлений из консольного приложения .NET</span><span class="sxs-lookup"><span data-stu-id="84799-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="84799-197">В этом разделе мы будем отправлять уведомление, используя консольное приложение .NET.</span><span class="sxs-lookup"><span data-stu-id="84799-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="84799-198">Создайте новое консольное приложение Visual C#.</span><span class="sxs-lookup"><span data-stu-id="84799-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="84799-199">В окне консоли диспетчера пакетов задайте свойство **Проект по умолчанию** для нового проекта консольного приложения, а затем в окне консоли выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="84799-199">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="84799-200">Эта инструкция добавляет ссылку на пакет SDK для центров уведомлений Azure с помощью <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакета NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="84799-200">This instruction adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="84799-201">Откройте файл **Program.cs** и добавьте следующую инструкцию using:</span><span class="sxs-lookup"><span data-stu-id="84799-201">Open the file **Program.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="84799-202">В классе `Program` добавьте следующий метод, а затем замените *DefaultFullSharedAccessSignatureSASConnectionString* и *NotificationHubName* своими значениями.</span><span class="sxs-lookup"><span data-stu-id="84799-202">In your `Program` class, add the following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with the values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="84799-203">Добавьте в метод **Main** следующие строки:</span><span class="sxs-lookup"><span data-stu-id="84799-203">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="84799-204">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="84799-204">Test your app</span></span>
<span data-ttu-id="84799-205">Чтобы проверить работу этого приложения на реальном устройстве, просто подключите телефон к компьютеру с помощью кабеля USB.</span><span class="sxs-lookup"><span data-stu-id="84799-205">To test this app with an actual phone, just connect the phone to your computer by using a USB cable.</span></span> <span data-ttu-id="84799-206">Это действие загрузит приложение на подключенный телефон.</span><span class="sxs-lookup"><span data-stu-id="84799-206">This action loads your app onto the attached phone.</span></span>

<span data-ttu-id="84799-207">Чтобы протестировать это приложение с помощью эмулятора, на верхней панели инструментов Eclipse нажмите кнопку **Run**(Запуск) и выберите приложение. После этого запустится эмулятор, загрузится и запустится приложение.</span><span class="sxs-lookup"><span data-stu-id="84799-207">To test this app with the emulator, on the Eclipse top toolbar, click **Run**, and then select your app: it starts the emulator, loads, and runs the app.</span></span>

<span data-ttu-id="84799-208">Приложение получает значения userId и channelId из службы push-уведомлений Baidu с последующей регистрацией в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="84799-208">The app retrieves the 'userId' and 'channelId' from the Baidu Push notification service and registers with the notification hub.</span></span>

<span data-ttu-id="84799-209">Тестовые уведомления можно отправлять на вкладке отладки на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="84799-209">To send a test notification, you can use the debug tab of the Azure Classic Portal.</span></span> <span data-ttu-id="84799-210">Если вы собрали консольное приложение .NET для Visual Studio, нажмите клавишу F5 в Visual Studio для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="84799-210">If you built the .NET console application for Visual Studio, just press the F5 key in Visual Studio to run the application.</span></span> <span data-ttu-id="84799-211">Приложение отправляет уведомление, которое отображается в верхней части области уведомлений устройства или эмулятора.</span><span class="sxs-lookup"><span data-stu-id="84799-211">The application sends a notification that appears in the top notification area of your device or emulator.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
<span data-ttu-id="84799-212">[Пакет Android SDK для мобильных служб]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="84799-212">[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409</span></span>
<span data-ttu-id="84799-213">[Пакет Android SDK для Baidu Push]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk</span><span class="sxs-lookup"><span data-stu-id="84799-213">[Baidu Push Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk</span></span>
<span data-ttu-id="84799-214">[классический портал Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="84799-214">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="84799-215">[портал Baidu]: http://www.baidu.com/</span><span class="sxs-lookup"><span data-stu-id="84799-215">[Baidu portal]: http://www.baidu.com/</span></span>
