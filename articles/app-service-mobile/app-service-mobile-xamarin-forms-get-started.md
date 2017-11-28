---
title: "Начало работы с функцией \"Мобильные приложения\" с использованием Xamarin.Forms"
description: "Этот учебник поможет приступить к использованию функции \"Мобильные приложения\"в разработке для Xamarin.Forms"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ee12caaad4095cff6dae3282f747ae804f93db81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="7e0f2-103">Создание приложения Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="7e0f2-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="7e0f2-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="7e0f2-104">Overview</span></span>
<span data-ttu-id="7e0f2-105">В этом учебнике рассказывается, как добавить облачную серверную службу в мобильное приложение Xamarin.Forms с помощью функции "Мобильные приложения" службы приложений Azure в качестве серверной части.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-105">This tutorial shows you how to add a cloud-based back-end service to a Xamarin.Forms mobile app by using the Mobile Apps feature of Azure App Service as the back end.</span></span> <span data-ttu-id="7e0f2-106">Вы создадите новую серверную часть при помощи функции "Мобильные приложения" и простое приложение Xamarin.Forms для списка дел, в котором в Azure хранятся данные приложения.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="7e0f2-107">Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными мобильным приложениям для приложений Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e0f2-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7e0f2-108">Prerequisites</span></span>
<span data-ttu-id="7e0f2-109">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="7e0f2-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="7e0f2-110">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-110">An active Azure account.</span></span> <span data-ttu-id="7e0f2-111">Если у вас нет учетной записи, можно зарегистрироваться для получения бесплатной пробной версии Azure и получить до 10 бесплатных мобильных приложений, которые можно использовать и после окончания пробного периода.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-111">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="7e0f2-112">Дополнительные сведения см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e0f2-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="7e0f2-113">Visual Studio с Xamarin.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="7e0f2-114">Сведения см. в статье о [настройке и установке](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e0f2-114">For information, see the [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="7e0f2-115">Компьютер Mac с установленным ПО XCode версии 7.0 или выше и Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="7e0f2-116">Сведения см. в статьях о [настройке и установке](https://msdn.microsoft.com/library/mt613162.aspx) и [программе установки, установке и проверке для пользователей Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="7e0f2-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="7e0f2-117">Создание серверной части при помощи функции "Мобильные приложения"</span><span class="sxs-lookup"><span data-stu-id="7e0f2-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="7e0f2-118">Для создания серверной части при помощи функции "Мобильные приложения" выполните инструкции ниже.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-118">To create a new Mobile Apps back end, do the following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="7e0f2-119">Теперь при помощи функции "Мобильные приложения" мы настроили серверную часть, которую могут использовать ваши клиентские мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="7e0f2-120">Далее мы скачаем серверный проект со списком простых задач и опубликуем его в Azure.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-120">Next, you download a server project for a simple to-do list back end and then publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="7e0f2-121">Настройка серверного проекта</span><span class="sxs-lookup"><span data-stu-id="7e0f2-121">Configure the server project</span></span>

<span data-ttu-id="7e0f2-122">Чтобы настроить серверный проект для использования серверной части .NET или Node.js, выполните инструкции ниже.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-122">To configure the server project to use either the Node.js or .NET back end, do the following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinforms-solution"></a><span data-ttu-id="7e0f2-123">Скачивание и запуск решения Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="7e0f2-123">Download and run the Xamarin.Forms solution</span></span>

<span data-ttu-id="7e0f2-124">Есть два способа загрузки.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-124">You can download the solution in either of two ways.</span></span> <span data-ttu-id="7e0f2-125">Вы можете скачать решение на компьютер Mac и открыть в Xamarin Studio или скачать его на компьютер Windows и открыть в Visual Studio с помощью подключенного к сети компьютера Mac для создания приложения iOS.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-125">Download it to a Mac and open it in Xamarin Studio, or download it to a Windows computer and open it in Visual Studio by using a networked Mac for building the iOS app.</span></span> <span data-ttu-id="7e0f2-126">Дополнительные ведения см. в статье о [настройке и установке](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e0f2-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="7e0f2-127">На компьютере Mac или Windows выполните инструкции ниже.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-127">On a Mac or Windows computer, do the following:</span></span>

1. <span data-ttu-id="7e0f2-128">Перейдите на [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="7e0f2-128">Go to the [Azure portal].</span></span>

2. <span data-ttu-id="7e0f2-129">В колонке **Параметры** мобильного приложения в разделе **Мобильные приложения** последовательно выберите **Начало работы** > **Xamarin.Forms**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-129">On the **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="7e0f2-130">На **шаге 3** выберите **Создание нового приложения** и нажмите **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="7e0f2-131">После этого будет скачан проект, содержащий клиентское приложение, подключенное к вашему мобильному приложению.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-131">This action downloads a project that contains a client application that's connected to your mobile app.</span></span> <span data-ttu-id="7e0f2-132">Сохраните сжатый файл проекта на локальном компьютере и запомните путь к нему.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-132">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="7e0f2-133">Извлеките скачанный проект и откройте его в Xamarin Studio (Mac) или Visual Studio (Windows).</span><span class="sxs-lookup"><span data-stu-id="7e0f2-133">Extract the project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Извлеченный проект в Xamarin Studio][9]

   ![Извлеченный проект в Visual Studio][8]

## <a name="optional-run-the-ios-project"></a><span data-ttu-id="7e0f2-136">(Необязательно) Запуск проекта iOS</span><span class="sxs-lookup"><span data-stu-id="7e0f2-136">(Optional) Run the iOS project</span></span>
<span data-ttu-id="7e0f2-137">В этом разделе описано, как запустить проект Xamarin iOS для устройств под управлением iOS.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-137">In this section, you run the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="7e0f2-138">Пропустите этот раздел, если вы не работаете с устройствами iOS.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="7e0f2-139">В Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="7e0f2-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="7e0f2-140">Щелкните проект iOS правой кнопкой мыши и выберите параметр **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-140">Right-click the iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="7e0f2-141">В меню **Выполнить** выберите **Начать отладку**, чтобы выполнить сборку проекта и запустить приложение в эмуляторе iPhone.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-141">On the **Run** menu, select **Start Debugging** to build the project and start the app in the iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="7e0f2-142">В Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7e0f2-142">In Visual Studio</span></span>
1. <span data-ttu-id="7e0f2-143">Щелкните проект iOS правой кнопкой мыши и выберите параметр **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-143">Right-click the iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="7e0f2-144">В меню **Сборка** выберите пункт **Диспетчер конфигураций**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-144">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="7e0f2-145">В диалоговом окне **Диспетчер конфигураций** установите флажки **Сборка** и **Развертывание** рядом с проектом iOS.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-145">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the iOS project.</span></span>

4. <span data-ttu-id="7e0f2-146">Чтобы выполнить сборку проекта и запустить приложение в эмуляторе iPhone, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-146">To build the project and start the app in the iPhone emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7e0f2-147">При проблемах со сборкой проекта запустите диспетчер пакетов NuGet и выполните обновление до последней версии пакетов поддержки Xamarin.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-147">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="7e0f2-148">Проекты быстрого запуска могут обновляться до последних версий в течение длительного времени.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-148">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="7e0f2-149">В приложении введите содержательный текст, например *Изучение Xamarin*, и выберите знак плюса (**+**).</span><span class="sxs-lookup"><span data-stu-id="7e0f2-149">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="7e0f2-150">После этого в новую серверную часть, созданную при помощи функции "Мобильные приложения" и размещенную в Azure, будет отправлен запрос POST.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-150">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="7e0f2-151">Данные из запроса вставляются в таблицу TodoItem.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-151">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="7e0f2-152">Элементы, хранящиеся в таблице, возвращаются серверной частью, созданной при помощи функции "Мобильные приложения", а данные отображаются в списке.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-152">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7e0f2-153">Код, который обращается к серверной части, созданной при помощи функции "Мобильные приложения", можно найти в файле C# TodoItemManager.cs проекта для переносимой библиотеки классов вашего решения.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-153">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-the-android-project"></a><span data-ttu-id="7e0f2-154">(Необязательно) Запуск проекта Android</span><span class="sxs-lookup"><span data-stu-id="7e0f2-154">(Optional) Run the Android project</span></span>
<span data-ttu-id="7e0f2-155">В этом разделе описано, как запустить проект Xamarin Android для устройств под управлением Android.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-155">In this section, you run the Xamarin droid project for Android.</span></span> <span data-ttu-id="7e0f2-156">Пропустите этот раздел, если вы не работаете с устройствами Android.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="7e0f2-157">В Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="7e0f2-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="7e0f2-158">Щелкните правой кнопкой мыши проект Android и выберите пункт **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-158">Right-click the Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="7e0f2-159">Чтобы выполнить сборку проекта и запустить приложение в эмуляторе AndroidВ, щелкните пункт **Начать отладку** в меню **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-159">To build the project and start the app in an Android emulator, on the **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="7e0f2-160">В Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7e0f2-160">In Visual Studio</span></span>

1. <span data-ttu-id="7e0f2-161">Щелкните правой кнопкой мыши проект Android (Droid) и выберите пункт **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-161">Right-click the Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="7e0f2-162">В меню **Сборка** выберите пункт **Диспетчер конфигураций**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-162">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="7e0f2-163">В диалоговом окне **Диспетчер конфигураций** установите флажки **Сборка** и **Развертывание** рядом с проектом Android.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-163">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the Android project.</span></span>

4. <span data-ttu-id="7e0f2-164">Чтобы выполнить сборку проекта и запустить приложение в эмуляторе Android, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-164">To build the project and start the app in an Android emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7e0f2-165">При проблемах со сборкой проекта запустите диспетчер пакетов NuGet и выполните обновление до последней версии пакетов поддержки Xamarin.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-165">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="7e0f2-166">Проекты быстрого запуска могут обновляться до последних версий в течение длительного времени.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-166">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="7e0f2-167">В приложении введите содержательный текст, например *Изучение Xamarin*, и выберите знак плюса (**+**).</span><span class="sxs-lookup"><span data-stu-id="7e0f2-167">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="7e0f2-168">После этого в новую серверную часть, созданную при помощи функции "Мобильные приложения" и размещенную в Azure, будет отправлен запрос POST.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-168">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="7e0f2-169">Данные из запроса вставляются в таблицу TodoItem.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-169">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="7e0f2-170">Элементы, хранящиеся в таблице, возвращаются серверной частью, созданной при помощи функции "Мобильные приложения", а данные отображаются в списке.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-170">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="7e0f2-171">Код, который обращается к серверной части, созданной при помощи функции "Мобильные приложения", можно найти в файле C# TodoItemManager.cs проекта для переносимой библиотеки классов вашего решения.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-171">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-the-windows-project"></a><span data-ttu-id="7e0f2-172">(Необязательно) Запуск проекта Windows</span><span class="sxs-lookup"><span data-stu-id="7e0f2-172">(Optional) Run the Windows project</span></span>

<span data-ttu-id="7e0f2-173">В этом разделе описано, как запустить проект Xamarin WinApp для устройств под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-173">In this section, you run the Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="7e0f2-174">Пропустите этот раздел, если вы не работаете с устройствами Windows.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="7e0f2-175">В Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7e0f2-175">In Visual Studio</span></span>

1. <span data-ttu-id="7e0f2-176">Щелкните правой кнопкой мыши любой проект Windows и выберите пункт **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-176">Right-click any of the Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="7e0f2-177">В меню **Сборка** выберите пункт **Диспетчер конфигураций**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-177">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="7e0f2-178">В диалоговом окне **Диспетчер конфигураций** установите флажки **Сборка** и **Развертывание** рядом с выбранным проектом Windows.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-178">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the Windows project that you chose.</span></span>

4. <span data-ttu-id="7e0f2-179">Чтобы выполнить сборку проекта и запустить приложение в эмуляторе Windows, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-179">To build the project and start the app in a Windows emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7e0f2-180">При проблемах со сборкой проекта запустите диспетчер пакетов NuGet и выполните обновление до последней версии пакетов поддержки Xamarin.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-180">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="7e0f2-181">Проекты быстрого запуска могут обновляться до последних версий в течение длительного времени.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-181">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="7e0f2-182">В приложении введите содержательный текст, например *Изучение Xamarin*, и выберите знак плюса (**+**).</span><span class="sxs-lookup"><span data-stu-id="7e0f2-182">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    <span data-ttu-id="7e0f2-183">После этого в новую серверную часть, созданную при помощи функции "Мобильные приложения" и размещенную в Azure, будет отправлен запрос POST.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-183">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="7e0f2-184">Данные из запроса вставляются в таблицу TodoItem.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-184">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="7e0f2-185">Элементы, хранящиеся в таблице, возвращаются серверной частью, созданной при помощи функции "Мобильные приложения", а данные отображаются в списке.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-185">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="7e0f2-186">Код, который обращается к серверной части, созданной при помощи функции "Мобильные приложения", можно найти в файле C# TodoItemManager.cs проекта для переносимой библиотеки классов вашего решения.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-186">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="7e0f2-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7e0f2-187">Next steps</span></span>

* [<span data-ttu-id="7e0f2-188">Добавление аутентификации в приложение</span><span class="sxs-lookup"><span data-stu-id="7e0f2-188">Add authentication to your app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="7e0f2-189">Узнайте больше о проверке подлинности пользователей приложения с помощью поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-189">Learn how to authenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="7e0f2-190">Добавление push-уведомлений в приложение</span><span class="sxs-lookup"><span data-stu-id="7e0f2-190">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="7e0f2-191">Узнайте, как добавить в мобильное приложение поддержку push-уведомлений и настроить в серверной части, созданной при помощи функции "Мобильные приложения", концентраторы уведомлений Azure для отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-191">Learn how to add push notifications support to your app and configure your Mobile Apps back end to use Azure Notification Hubs to send the push notifications.</span></span>

* [<span data-ttu-id="7e0f2-192">Включение автономной синхронизации для приложения</span><span class="sxs-lookup"><span data-stu-id="7e0f2-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="7e0f2-193">Узнайте, как добавить в приложение поддержку автономной работы с помощью серверной части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-193">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="7e0f2-194">Автономная синхронизация позволяет просматривать, добавлять или изменять данные мобильного приложения даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="7e0f2-195">Использование управляемого клиента для функции "Мобильные приложения"</span><span class="sxs-lookup"><span data-stu-id="7e0f2-195">Use the managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="7e0f2-196">Узнайте, как работать с пакетом SDK для управляемого клиента в приложении Xamarin.</span><span class="sxs-lookup"><span data-stu-id="7e0f2-196">Learn how to work with the managed client SDK in your Xamarin app.</span></span>

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[портал Azure]: https://portal.azure.com/
