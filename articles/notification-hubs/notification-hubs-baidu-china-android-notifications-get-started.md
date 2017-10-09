---
title: "aaaGet к работе с концентраторами уведомлений Azure, с помощью Baidu | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toouse концентраторов уведомлений Azure toopush уведомления tooAndroid устройств с помощью Baidu."
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
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="661e1-103">Приступая к работе с Центрами уведомлений с помощью Baidu</span><span class="sxs-lookup"><span data-stu-id="661e1-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="661e1-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="661e1-104">Overview</span></span>
<span data-ttu-id="661e1-105">Принудительной облака Baidu является китайский облачной службы, которые можно использовать уведомления toomobile toosend принудительной устройств.</span><span class="sxs-lookup"><span data-stu-id="661e1-105">Baidu cloud push is a Chinese cloud service that you can use toosend push notifications toomobile devices.</span></span> <span data-ttu-id="661e1-106">Эта служба полезна в Китае, где push-уведомления tooAndroid является сложной задачей из-за наличия hello различных приложений в магазине и принудительной доставки служб, кроме доступности toohello устройств Android, которые не являются обычно подключенных tooGCM (Google Облачные системы обмена сообщениями).</span><span class="sxs-lookup"><span data-stu-id="661e1-106">This service is useful in China, where delivering push notifications tooAndroid is complex because of hello presence of different app stores and push services, in addition toohello availability of Android devices that are not typically connected tooGCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="661e1-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="661e1-107">Prerequisites</span></span>
<span data-ttu-id="661e1-108">Для работы с руководством требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="661e1-108">This tutorial requires:</span></span>

* <span data-ttu-id="661e1-109">Android SDK (предполагается, что используется Eclipse), который можно загрузить из hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android сайта</a></span><span class="sxs-lookup"><span data-stu-id="661e1-109">Android SDK (we assume that you use Eclipse), which you can download from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="661e1-110">[Пакет Android SDK для мобильных служб]</span><span class="sxs-lookup"><span data-stu-id="661e1-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="661e1-111">[пакета SDK для Android Push-уведомлений Baidu]</span><span class="sxs-lookup"><span data-stu-id="661e1-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="661e1-112">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="661e1-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="661e1-113">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="661e1-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="661e1-114">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="661e1-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="661e1-115">Создание учетной записи Baidu</span><span class="sxs-lookup"><span data-stu-id="661e1-115">Create a Baidu account</span></span>
<span data-ttu-id="661e1-116">toouse Baidu, необходимо иметь учетную запись Baidu.</span><span class="sxs-lookup"><span data-stu-id="661e1-116">toouse Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="661e1-117">Если это уже сделано, войдите в toohello [Baidu портала] и пропустить следующий шаг toohello.</span><span class="sxs-lookup"><span data-stu-id="661e1-117">If you already have one, log in toohello [Baidu portal] and skip toohello next step.</span></span> <span data-ttu-id="661e1-118">См. в противном случае hello в соответствии с инструкциями о том, как toocreate учетную запись Baidu.</span><span class="sxs-lookup"><span data-stu-id="661e1-118">Otherwise, see hello following instructions on how toocreate a Baidu account.</span></span>  

1. <span data-ttu-id="661e1-119">Go toohello [Baidu портала] и нажмите кнопку hello**登录**(**входа**) ссылку.</span><span class="sxs-lookup"><span data-stu-id="661e1-119">Go toohello [Baidu portal] and click hello **登录** (**Login**) link.</span></span> <span data-ttu-id="661e1-120">Нажмите кнопку**立即注册**процесс регистрации учетной записи toostart hello.</span><span class="sxs-lookup"><span data-stu-id="661e1-120">Click **立即注册** toostart hello account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="661e1-121">Введите сведения о необходимых hello — электронной почты, телефона и адрес, пароля и проверки кода и нажмите кнопку **регистрации**.</span><span class="sxs-lookup"><span data-stu-id="661e1-121">Enter hello required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="661e1-122">Будут отправляться адрес эл. почты toohello электронной почты, введенного tooactivate связи учетной записи Baidu.</span><span class="sxs-lookup"><span data-stu-id="661e1-122">You will be sent an email toohello email address that you entered with a link tooactivate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="661e1-123">Войдите в учетную запись электронной почты tooyour, откройте hello Baidu активации почты выберите учетную запись Baidu tooactivate ссылку активации hello.</span><span class="sxs-lookup"><span data-stu-id="661e1-123">Log in tooyour email account, open hello Baidu activation mail, and click hello activation link tooactivate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="661e1-124">После активации учетной записи Baidu вход toohello [Baidu портала].</span><span class="sxs-lookup"><span data-stu-id="661e1-124">Once you have an activated Baidu account, log in toohello [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="661e1-125">Регистрация в качестве разработчика Baidu</span><span class="sxs-lookup"><span data-stu-id="661e1-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="661e1-126">После входа в toohello [Baidu портала], нажмите кнопку**更多 >>** (**дополнительные**).</span><span class="sxs-lookup"><span data-stu-id="661e1-126">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="661e1-127">Прокрутите вниз hello**站长与开发者服务 (мастеру и службами для разработчиков)** и нажмите кнопку**百度开放云平台**(**Baidu откройте облачная платформа**).</span><span class="sxs-lookup"><span data-stu-id="661e1-127">Scroll down in hello **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="661e1-128">На следующей странице приветствия нажмите кнопку**开发者服务**(**службами для разработчиков**) в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="661e1-128">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="661e1-129">На следующей странице приветствия нажмите кнопку**注册开发者**(**зарегистрированные разработчики**) hello меню в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="661e1-129">On hello next page, click **注册开发者** (**Registered Developers**) from hello menu on hello top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="661e1-130">Введите свое имя, описание и номер мобильного телефона, чтобы получить текстовое сообщение для проверки подлинности, а затем щелкните **送验证码** (**Отправить код проверки**).</span><span class="sxs-lookup"><span data-stu-id="661e1-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="661e1-131">Для международных номеров требуется код страны hello tooenclose в круглые скобки.</span><span class="sxs-lookup"><span data-stu-id="661e1-131">For international phone numbers, you need tooenclose hello country code in parentheses.</span></span> <span data-ttu-id="661e1-132">Например, номер телефона в США выглядит так: **(1)1234567890**.</span><span class="sxs-lookup"><span data-stu-id="661e1-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="661e1-133">После этого должно появиться текстовое сообщение с номером проверки, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="661e1-133">You should then receive a text message with a verification number, as shown in hello following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="661e1-134">Введите номер проверки hello из сообщения hello в**验证码**(**код подтверждения**).</span><span class="sxs-lookup"><span data-stu-id="661e1-134">Enter hello verification number from hello message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="661e1-135">И, наконец, завершите регистрации разработчика hello, принятие соглашения Baidu hello команду**提交**(**отправить**).</span><span class="sxs-lookup"><span data-stu-id="661e1-135">Finally, complete hello developer registration by accepting hello Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="661e1-136">Появится следующая страница при успешном завершении регистрации hello:</span><span class="sxs-lookup"><span data-stu-id="661e1-136">You will see hello following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="661e1-137">Создание облачного push-проекта Baidu</span><span class="sxs-lookup"><span data-stu-id="661e1-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="661e1-138">Во время создания push-проекта Baidu вы получите код приложения, ключ API и секретный ключ.</span><span class="sxs-lookup"><span data-stu-id="661e1-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="661e1-139">После входа в toohello [Baidu портала], нажмите кнопку**更多 >>** (**дополнительные**).</span><span class="sxs-lookup"><span data-stu-id="661e1-139">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="661e1-140">Прокрутите вниз hello**站长与开发者服务**(**мастеру и службами для разработчиков**) и нажмите кнопку**百度开放云平台**(**Baidu откройте облачная платформа**).</span><span class="sxs-lookup"><span data-stu-id="661e1-140">Scroll down in hello **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="661e1-141">На следующей странице приветствия нажмите кнопку**开发者服务**(**службами для разработчиков**) в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="661e1-141">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="661e1-142">На следующей странице приветствия нажмите кнопку**云推送**(**Push облака**) из hello**云服务**(**облачные службы**) раздела.</span><span class="sxs-lookup"><span data-stu-id="661e1-142">On hello next page, click **云推送** (**Cloud Push**) from hello **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="661e1-143">После зарегистрированным разработчиком, вы видите**管理控制台**(**консоли управления**) в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="661e1-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at hello top menu.</span></span> <span data-ttu-id="661e1-144">Щелкните **开发者服务管理** (**Управление службой разработки**).</span><span class="sxs-lookup"><span data-stu-id="661e1-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="661e1-145">На следующей странице приветствия нажмите кнопку**创建工程**(**Создание проекта**).</span><span class="sxs-lookup"><span data-stu-id="661e1-145">On hello next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="661e1-146">Введите имя приложения и щелкните **创建** (**Создать**).</span><span class="sxs-lookup"><span data-stu-id="661e1-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="661e1-147">После успешного создания проекта службы push-уведомлений облака Baidu отобразится страница с **идентификатором приложения**, **ключом API** и **секретным ключом**.</span><span class="sxs-lookup"><span data-stu-id="661e1-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="661e1-148">Запишите ключ API hello и секретный ключ, который будет использоваться позже.</span><span class="sxs-lookup"><span data-stu-id="661e1-148">Make a note of hello API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="661e1-149">Настройка проекта hello для push-уведомлений, щелкнув**云推送**(**принудительной облака**) на левой панели hello.</span><span class="sxs-lookup"><span data-stu-id="661e1-149">Configure hello project for push notifications by clicking **云推送** (**Cloud Push**) on hello left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="661e1-150">На следующей странице приветствия нажмите кнопку hello**推送设置**(**Push параметры**) кнопки.</span><span class="sxs-lookup"><span data-stu-id="661e1-150">On hello next page, click hello **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="661e1-151">На странице приветствия конфигурации добавьте hello имя пакета, который будет использоваться в проекте Android в hello**应用包名**(**пакета приложения**), а затем щелкните**保存设置**() **Сохранить**).</span><span class="sxs-lookup"><span data-stu-id="661e1-151">On hello configuration page, add hello package name that you will be using in your Android project in hello **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="661e1-152">Вы видите hello**保存成功!** (**Успешно сохранено!)**.</span><span class="sxs-lookup"><span data-stu-id="661e1-152">You see hello **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="661e1-153">Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="661e1-153">Configure your notification hub</span></span>
1. <span data-ttu-id="661e1-154">Вход toohello [классический портал Azure], а затем нажмите кнопку **+ создать** hello нижней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="661e1-154">Sign in toohello [Azure Classic Portal], and then click **+NEW** at hello bottom of hello screen.</span></span>
2. <span data-ttu-id="661e1-155">Щелкните **Службы приложений**, выберите **Служебная шина**, затем щелкните **Центр уведомлений** и нажмите кнопку **Быстро создать**.</span><span class="sxs-lookup"><span data-stu-id="661e1-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="661e1-156">Введите имя для вашей **концентратора уведомлений**выберите hello **область** и hello **пространства имен** где этот концентратор уведомлений будет создан и нажмите кнопку  **Создать новый узел уведомлений**.</span><span class="sxs-lookup"><span data-stu-id="661e1-156">Provide a name for your **Notification Hub**, select hello **Region** and hello **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="661e1-157">Выберите пространство имен hello, в котором вы создали концентратор уведомлений и нажмите кнопку **концентраторы уведомлений** вверху hello.</span><span class="sxs-lookup"><span data-stu-id="661e1-157">Click hello namespace in which you created your notification hub, and then click **Notification Hubs** at hello top.</span></span>
   
      ![][18]
5. <span data-ttu-id="661e1-158">Выберите hello концентратор уведомлений, который был создан и нажмите кнопку **Настройка** hello верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="661e1-158">Select hello notification hub that you created, and then click **Configure** from hello top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="661e1-159">Прокрутите вниз toohello **параметры уведомлений baidu** статьи и введите ключ hello API и секретный ключ, полученный из Baidu в консоли hello ранее проекта принудительной облака Baidu.</span><span class="sxs-lookup"><span data-stu-id="661e1-159">Scroll down toohello **baidu notification settings** section and enter hello API key and secret key that you obtained from hello Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="661e1-160">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="661e1-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="661e1-161">Нажмите кнопку hello **мониторинга** вверху hello для концентратора уведомлений hello, а затем щелкните **Просмотр строки подключения**.</span><span class="sxs-lookup"><span data-stu-id="661e1-161">Click hello **Dashboard** tab at hello top for hello notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="661e1-162">Запишите hello **DefaultListenSharedAccessSignature** и **DefaultFullSharedAccessSignature** из hello **доступ к сведения о соединении** окна.</span><span class="sxs-lookup"><span data-stu-id="661e1-162">Make a note of hello **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from hello **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="661e1-163">Подключение приложения toohello концентратор уведомлений</span><span class="sxs-lookup"><span data-stu-id="661e1-163">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="661e1-164">В ADT Eclipse создайте новый проект Android (**Файл** > **Создать** > **Проект приложения Android**).</span><span class="sxs-lookup"><span data-stu-id="661e1-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="661e1-165">Введите **имя_приложения** и убедитесь, что hello **SDK требуется минимум** версии задано слишком**API 16: Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="661e1-165">Enter an **Application Name** and ensure that hello **Minimum Required SDK** version is set too**API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="661e1-166">Нажмите кнопку **Далее** и продолжить следующие мастера hello до hello **создать действие** появится окно.</span><span class="sxs-lookup"><span data-stu-id="661e1-166">Click **Next** and continue following hello wizard until hello **Create Activity** window appears.</span></span> <span data-ttu-id="661e1-167">Убедитесь, что **пустое действие** выбранного, а затем выберите **Готово** toocreate приложения Android.</span><span class="sxs-lookup"><span data-stu-id="661e1-167">Make sure that **Blank Activity** is selected, and finally select **Finish** toocreate a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="661e1-168">Убедитесь в том, что hello **цели построения проекта** задано правильно.</span><span class="sxs-lookup"><span data-stu-id="661e1-168">Make sure that hello **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="661e1-169">Загрузите файл уведомления концентраторов 0.4.jar hello из hello **файлы** вкладка hello [уведомления-концентраторы-Android-SDK на Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span><span class="sxs-lookup"><span data-stu-id="661e1-169">Download hello notification-hubs-0.4.jar file from hello **Files** tab of hello [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="661e1-170">Добавьте файл toohello hello **библиотеки** папки проектов Eclipse и обновления hello *библиотеки* папки.</span><span class="sxs-lookup"><span data-stu-id="661e1-170">Add hello file toohello **libs** folder of your Eclipse project, and refresh hello *libs* folder.</span></span>
6. <span data-ttu-id="661e1-171">Загрузите и распакуйте hello [пакета SDK для Android Push-уведомлений Baidu]откройте hello **библиотеки** папку, а затем копировать hello **pushservice x.y.z** jar-файл и hello **armeabi**  &  **mips** папки в hello **библиотеки** папку приложения Android.</span><span class="sxs-lookup"><span data-stu-id="661e1-171">Download and unzip hello [Baidu Push Android SDK], open hello **libs** folder, and then copy hello **pushservice-x.y.z** jar file and hello **armeabi** & **mips** folders in hello **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="661e1-172">Откройте hello **AndroidManifest.xml** Android файл проекта и добавьте hello разрешений, необходимых для hello Baidu SDK.</span><span class="sxs-lookup"><span data-stu-id="661e1-172">Open hello **AndroidManifest.xml** file of your Android project and add hello permissions that are required by hello Baidu SDK.</span></span>
   
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
8. <span data-ttu-id="661e1-173">Добавить hello **android: имя** tooyour свойство **приложения** элемент в **AndroidManifest.xml**, заменив *yourprojectname* (для Пример, **com.example.BaiduTest**).</span><span class="sxs-lookup"><span data-stu-id="661e1-173">Add hello **android:name** property tooyour **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="661e1-174">Убедитесь, это имя проекта соответствует hello один, настроенный в hello Baidu в консоли.</span><span class="sxs-lookup"><span data-stu-id="661e1-174">Make sure that this project name matches hello one that you configured in hello Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="661e1-175">Добавить hello следующая конфигурация в элементе приложения hello после hello **. MainActivity** элемент действия, заменив *yourprojectname* (например, **com.example.BaiduTest**):</span><span class="sxs-lookup"><span data-stu-id="661e1-175">Add hello following configuration within hello application element after hello **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
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
10. <span data-ttu-id="661e1-176">Добавьте новый класс с именем **ConfigurationSettings.java** toohello проекта.</span><span class="sxs-lookup"><span data-stu-id="661e1-176">Add a new class called **ConfigurationSettings.java** toohello project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="661e1-177">Добавьте следующий код tooit hello:</span><span class="sxs-lookup"><span data-stu-id="661e1-177">Add hello following code tooit:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="661e1-178">Задайте значение hello **API_KEY** с что было извлечено из проекта облака Baidu hello раньше, **NotificationHubName** с вашим именем концентратора уведомлений из классического портала Azure hello и  **NotificationHubConnectionString** с DefaultListenSharedAccessSignature из hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="661e1-178">Set hello value of **API_KEY** with what you retrieved from hello Baidu cloud project earlier, **NotificationHubName** with your notification hub name from hello Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from hello Azure Classic Portal.</span></span>
12. <span data-ttu-id="661e1-179">Добавьте новый класс с именем **DemoApplication.java**и добавьте следующий код tooit hello:</span><span class="sxs-lookup"><span data-stu-id="661e1-179">Add a new class called **DemoApplication.java**, and add hello following code tooit:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="661e1-180">Добавьте другой новый класс с именем **MyPushMessageReceiver.java**и добавьте следующий код tooit hello.</span><span class="sxs-lookup"><span data-stu-id="661e1-180">Add another new class called **MyPushMessageReceiver.java**, and add hello following code tooit.</span></span> <span data-ttu-id="661e1-181">Это класс hello, дескрипторы hello push-уведомлений, полученных от сервера принудительной hello Baidu.</span><span class="sxs-lookup"><span data-stu-id="661e1-181">It is hello class that handles hello push notifications that are received from hello Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
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
14. <span data-ttu-id="661e1-182">Откройте **MainActivity.java**и добавьте следующие toohello hello **onCreate** метод:</span><span class="sxs-lookup"><span data-stu-id="661e1-182">Open **MainActivity.java**, and add hello following toohello **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="661e1-183">Откройте следующие инструкции импорта вверху hello hello:</span><span class="sxs-lookup"><span data-stu-id="661e1-183">Open hello following import statements at hello top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a><span data-ttu-id="661e1-184">Отправлять уведомления tooyour приложения</span><span class="sxs-lookup"><span data-stu-id="661e1-184">Send notifications tooyour app</span></span>
<span data-ttu-id="661e1-185">Можно быстро проверить получение уведомлений в приложение путем отправки уведомления в hello [портал Azure](https://portal.azure.com/) с помощью hello **отправки** кнопку на концентраторе уведомлений hello, как показано в следующих экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="661e1-185">You can quickly test receiving notifications in your app by sending notifications in hello [Azure portal](https://portal.azure.com/) using hello **Send** button on hello notification hub, as shown in hello following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="661e1-186">Push-уведомления обычно отправляются в серверной службе, например мобильными службами или ASP.NET, с помощью совместимой библиотеки.</span><span class="sxs-lookup"><span data-stu-id="661e1-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="661e1-187">Если библиотека недоступна для серверной части, можно использовать API-интерфейса REST hello непосредственно toosend сообщений уведомления.</span><span class="sxs-lookup"><span data-stu-id="661e1-187">If a library is not available for your back-end, you can use hello REST API directly toosend notification messages .</span></span>

<span data-ttu-id="661e1-188">В этом учебнике мы должен быть простым и просто демонстрации тестирование приложения клиента путем отправки уведомлений с использованием hello .NET SDK для концентраторов уведомлений в консольном приложении, а не серверной службы.</span><span class="sxs-lookup"><span data-stu-id="661e1-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="661e1-189">Мы рекомендуем hello [toousers уведомления toopush использования концентраторов уведомлений](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) учебника hello на следующем шаге для отправки уведомлений из серверной части ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="661e1-189">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="661e1-190">Тем не менее можно использовать следующие подходы hello для отправки уведомлений:</span><span class="sxs-lookup"><span data-stu-id="661e1-190">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="661e1-191">**Интерфейс REST**: может поддерживать уведомления на любой платформе серверной части, с помощью hello [интерфейс REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="661e1-191">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="661e1-192">**Пакета SDK .NET концентраторы уведомлений Microsoft Azure**: В hello диспетчера пакетов Nuget для Visual Studio, запустите [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="661e1-192">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="661e1-193">**Node.js**: [как концентраторы уведомлений из Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="661e1-193">**Node.js**: [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="661e1-194">**Мобильные приложения**: пример того, как toosend уведомления от мобильные приложения службы приложений Azure серверную платформу, которая интегрируется с концентраторами уведомлений в разделе [добавить push tooyour уведомления мобильного приложения](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="661e1-194">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="661e1-195">**Java / PHP**: пример как toosend уведомления с помощью hello API-интерфейс REST, в разделе «как toouse концентраторы уведомлений из Java и PHP» ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="661e1-195">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="661e1-196">(Необязательно) Отправление уведомлений из консольного приложения .NET</span><span class="sxs-lookup"><span data-stu-id="661e1-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="661e1-197">В этом разделе мы будем отправлять уведомление, используя консольное приложение .NET.</span><span class="sxs-lookup"><span data-stu-id="661e1-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="661e1-198">Создайте новое консольное приложение Visual C#.</span><span class="sxs-lookup"><span data-stu-id="661e1-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="661e1-199">В hello в окне консоли диспетчера пакетов, задайте hello **проекта по умолчанию** tooyour нового консольного приложения проекта, а затем в окне консоли hello, выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="661e1-199">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="661e1-200">Эта инструкция добавляет ссылку toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="661e1-200">This instruction adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="661e1-201">Привет открыть файл **Program.cs** и добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="661e1-201">Open hello file **Program.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="661e1-202">В вашей `Program` , добавьте следующий метод hello и замените *DefaultFullSharedAccessSignatureSASConnectionString* и *NotificationHubName* со значениями hello, у вас есть.</span><span class="sxs-lookup"><span data-stu-id="661e1-202">In your `Program` class, add hello following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with hello values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="661e1-203">Добавьте следующие строки в hello вашей **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="661e1-203">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="661e1-204">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="661e1-204">Test your app</span></span>
<span data-ttu-id="661e1-205">tootest подключения с фактическое телефоном, точно так же, это приложение hello phone tooyour компьютера с помощью USB-кабеля.</span><span class="sxs-lookup"><span data-stu-id="661e1-205">tootest this app with an actual phone, just connect hello phone tooyour computer by using a USB cable.</span></span> <span data-ttu-id="661e1-206">Это действие загружает приложение на телефон подключен hello.</span><span class="sxs-lookup"><span data-stu-id="661e1-206">This action loads your app onto hello attached phone.</span></span>

<span data-ttu-id="661e1-207">tootest это приложение в эмуляторе hello, на hello Eclipse верхней панели инструментов, нажмите кнопку **запуска**и затем выберите приложение: он запускает эмулятор hello, загрузки, и приложение hello запусков.</span><span class="sxs-lookup"><span data-stu-id="661e1-207">tootest this app with hello emulator, on hello Eclipse top toolbar, click **Run**, and then select your app: it starts hello emulator, loads, and runs hello app.</span></span>

<span data-ttu-id="661e1-208">приложение Hello извлекает userId «hello» и «channelId» из hello служба Baidu Push-уведомлений и регистрирует hello концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="661e1-208">hello app retrieves hello 'userId' and 'channelId' from hello Baidu Push notification service and registers with hello notification hub.</span></span>

<span data-ttu-id="661e1-209">toosend тестовое уведомление, можно использовать вкладки отладки hello hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="661e1-209">toosend a test notification, you can use hello debug tab of hello Azure Classic Portal.</span></span> <span data-ttu-id="661e1-210">При построении приложения консоли hello .NET для Visual Studio, просто нажмите клавишу hello F5 в приложение hello toorun Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="661e1-210">If you built hello .NET console application for Visual Studio, just press hello F5 key in Visual Studio toorun hello application.</span></span> <span data-ttu-id="661e1-211">приложение Hello отправляет уведомление, которое появляется в области уведомлений в верхней hello устройства или эмулятора.</span><span class="sxs-lookup"><span data-stu-id="661e1-211">hello application sends a notification that appears in hello top notification area of your device or emulator.</span></span>

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
[Пакет Android SDK для мобильных служб]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[пакета SDK для Android Push-уведомлений Baidu]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[классический портал Azure]: https://manage.windowsazure.com/
[Baidu портала]: http://www.baidu.com/
