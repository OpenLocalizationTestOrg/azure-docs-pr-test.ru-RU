---
title: "aaaGet работы с приложениями для мобильных устройств с помощью Xamarin.Forms"
description: "Выполните этот учебник toostart использование мобильных приложений для разработки Xamarin.Forms"
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
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="92d53-103">Создание приложения Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="92d53-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="92d53-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="92d53-104">Overview</span></span>
<span data-ttu-id="92d53-105">Этот учебник показывает, как tooadd облачных служб tooa Xamarin.Forms мобильного приложения с помощью hello компонент службы приложения Azure в качестве серверной части hello мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="92d53-105">This tutorial shows you how tooadd a cloud-based back-end service tooa Xamarin.Forms mobile app by using hello Mobile Apps feature of Azure App Service as hello back end.</span></span> <span data-ttu-id="92d53-106">Вы создадите новую серверную часть при помощи функции "Мобильные приложения" и простое приложение Xamarin.Forms для списка дел, в котором в Azure хранятся данные приложения.</span><span class="sxs-lookup"><span data-stu-id="92d53-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="92d53-107">Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными мобильным приложениям для приложений Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="92d53-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92d53-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="92d53-108">Prerequisites</span></span>
<span data-ttu-id="92d53-109">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="92d53-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="92d53-110">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="92d53-110">An active Azure account.</span></span> <span data-ttu-id="92d53-111">При отсутствии учетной записи, можно зарегистрироваться в пробной версии Azure и получите бесплатные too10 мобильных приложений, которые вы можете продолжать использовать даже после окончания срока действия пробной версии никакие.</span><span class="sxs-lookup"><span data-stu-id="92d53-111">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="92d53-112">Дополнительные сведения см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92d53-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="92d53-113">Visual Studio с Xamarin.</span><span class="sxs-lookup"><span data-stu-id="92d53-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="92d53-114">Сведения см. в разделе hello [задать Настройка и установка Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) страницы.</span><span class="sxs-lookup"><span data-stu-id="92d53-114">For information, see hello [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="92d53-115">Компьютер Mac с установленным ПО XCode версии 7.0 или выше и Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="92d53-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="92d53-116">Сведения см. в статьях о [настройке и установке](https://msdn.microsoft.com/library/mt613162.aspx) и [программе установки, установке и проверке для пользователей Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="92d53-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="92d53-117">Создание серверной части при помощи функции "Мобильные приложения"</span><span class="sxs-lookup"><span data-stu-id="92d53-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="92d53-118">toocreate завершить Mobile новых приложений, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="92d53-118">toocreate a new Mobile Apps back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="92d53-119">Теперь при помощи функции "Мобильные приложения" мы настроили серверную часть, которую могут использовать ваши клиентские мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="92d53-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="92d53-120">Затем загрузите серверный проект для серверную часть списка простые задачи и затем опубликовать его tooAzure.</span><span class="sxs-lookup"><span data-stu-id="92d53-120">Next, you download a server project for a simple to-do list back end and then publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="92d53-121">Настройка проекта сервера hello</span><span class="sxs-lookup"><span data-stu-id="92d53-121">Configure hello server project</span></span>

<span data-ttu-id="92d53-122">tooconfigure hello server project toouse hello серверной части, Node.js или .NET, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="92d53-122">tooconfigure hello server project toouse either hello Node.js or .NET back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a><span data-ttu-id="92d53-123">Загрузите и запустите решение Xamarin.Forms hello</span><span class="sxs-lookup"><span data-stu-id="92d53-123">Download and run hello Xamarin.Forms solution</span></span>

<span data-ttu-id="92d53-124">Вы можете загрузить решение hello одним из двух способов.</span><span class="sxs-lookup"><span data-stu-id="92d53-124">You can download hello solution in either of two ways.</span></span> <span data-ttu-id="92d53-125">Загрузите его tooa Mac и откройте его в Xamarin Studio, или загрузить компьютер Windows tooa и открыть его в Visual Studio с помощью сетевых Mac для создания приложения iOS hello.</span><span class="sxs-lookup"><span data-stu-id="92d53-125">Download it tooa Mac and open it in Xamarin Studio, or download it tooa Windows computer and open it in Visual Studio by using a networked Mac for building hello iOS app.</span></span> <span data-ttu-id="92d53-126">Дополнительные ведения см. в статье о [настройке и установке](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="92d53-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="92d53-127">На компьютере Mac или Windows hello следующие:</span><span class="sxs-lookup"><span data-stu-id="92d53-127">On a Mac or Windows computer, do hello following:</span></span>

1. <span data-ttu-id="92d53-128">Go toohello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="92d53-128">Go toohello [Azure portal].</span></span>

2. <span data-ttu-id="92d53-129">На hello **параметры** колонку для мобильного приложения в разделе **Mobile**выберите **приступить к работе** > **Xamarin.Forms**.</span><span class="sxs-lookup"><span data-stu-id="92d53-129">On hello **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="92d53-130">На **шаге 3** выберите **Создание нового приложения** и нажмите **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="92d53-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="92d53-131">Это действие загружает проект, содержащий клиентское приложение, которое является подключенных tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="92d53-131">This action downloads a project that contains a client application that's connected tooyour mobile app.</span></span> <span data-ttu-id="92d53-132">Сохраните hello проекта сжатый файл tooyour локального компьютера и запишите где его сохранить.</span><span class="sxs-lookup"><span data-stu-id="92d53-132">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="92d53-133">Извлеките hello проекта, который вы загрузили и затем откройте в Visual Studio (Windows) или Xamarin Studio (Mac).</span><span class="sxs-lookup"><span data-stu-id="92d53-133">Extract hello project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Извлеченный проект в Xamarin Studio][9]

   ![Извлеченный проект в Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a><span data-ttu-id="92d53-136">(Необязательно) Запустите проект iOS hello</span><span class="sxs-lookup"><span data-stu-id="92d53-136">(Optional) Run hello iOS project</span></span>
<span data-ttu-id="92d53-137">В этом разделе вы запустите проект iOS hello Xamarin для устройств iOS.</span><span class="sxs-lookup"><span data-stu-id="92d53-137">In this section, you run hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="92d53-138">Пропустите этот раздел, если вы не работаете с устройствами iOS.</span><span class="sxs-lookup"><span data-stu-id="92d53-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="92d53-139">В Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="92d53-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="92d53-140">Щелкните правой кнопкой мыши проект iOS hello, а затем выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="92d53-140">Right-click hello iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="92d53-141">На hello **запуска** последовательно выберите пункты **начать отладку** toobuild hello проект и запустить приложение hello в эмуляторе iPhone hello.</span><span class="sxs-lookup"><span data-stu-id="92d53-141">On hello **Run** menu, select **Start Debugging** toobuild hello project and start hello app in hello iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="92d53-142">В Visual Studio</span><span class="sxs-lookup"><span data-stu-id="92d53-142">In Visual Studio</span></span>
1. <span data-ttu-id="92d53-143">Щелкните правой кнопкой мыши проект iOS hello, а затем выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="92d53-143">Right-click hello iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="92d53-144">На hello **построения** последовательно выберите пункты **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="92d53-144">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="92d53-145">В hello **Configuration Manager** диалоговое окно, выберите hello **построения** и **развернуть** проект iOS toohello Далее флажки.</span><span class="sxs-lookup"><span data-stu-id="92d53-145">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello iOS project.</span></span>

4. <span data-ttu-id="92d53-146">toobuild hello проект и запустить приложение hello в эмуляторе iPhone hello, выберите hello **F5** ключа.</span><span class="sxs-lookup"><span data-stu-id="92d53-146">toobuild hello project and start hello app in hello iPhone emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="92d53-147">Если возникают проблемы при построении проекта hello, запустите hello NuGet пакета диспетчера и обновления toohello последнюю версию пакеты поддержки Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="92d53-147">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="92d53-148">Примеры использования проектов может быть медленным tooupdate toohello последние версии.</span><span class="sxs-lookup"><span data-stu-id="92d53-148">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="92d53-149">В приложение hello введите значимыми текстовыми, таких как *узнать Xamarin*, и затем выберите Здравствуйте, "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="92d53-149">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="92d53-150">Это действие отправляет toohello запрос post, новые мобильные приложения серверной части, который размещается в Azure.</span><span class="sxs-lookup"><span data-stu-id="92d53-150">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="92d53-151">Данные из запроса hello вставляется в таблицу TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="92d53-151">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="92d53-152">Данные отображаются в списке hello элементов, хранящихся в таблице hello возвращаются по hello заканчивается обратно мобильные приложения и hello.</span><span class="sxs-lookup"><span data-stu-id="92d53-152">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="92d53-153">Вы найдете hello код, который обращается к вашей серверной части мобильных приложений в hello TodoItemManager.cs C# файл hello проекта переносимой библиотеки классов для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="92d53-153">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-android-project"></a><span data-ttu-id="92d53-154">(Необязательно) Запустите проект Android hello</span><span class="sxs-lookup"><span data-stu-id="92d53-154">(Optional) Run hello Android project</span></span>
<span data-ttu-id="92d53-155">В этом разделе выполняется hello Xamarin droid проекта для Android.</span><span class="sxs-lookup"><span data-stu-id="92d53-155">In this section, you run hello Xamarin droid project for Android.</span></span> <span data-ttu-id="92d53-156">Пропустите этот раздел, если вы не работаете с устройствами Android.</span><span class="sxs-lookup"><span data-stu-id="92d53-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="92d53-157">В Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="92d53-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="92d53-158">Щелкните правой кнопкой мыши проект Android hello, а затем выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="92d53-158">Right-click hello Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="92d53-159">toobuild hello проект и запустить приложение hello в эмуляторе Android, на hello **запуска** последовательно выберите пункты **начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="92d53-159">toobuild hello project and start hello app in an Android emulator, on hello **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="92d53-160">В Visual Studio</span><span class="sxs-lookup"><span data-stu-id="92d53-160">In Visual Studio</span></span>

1. <span data-ttu-id="92d53-161">Щелкните правой кнопкой мыши проект Android (Droid) hello, а затем выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="92d53-161">Right-click hello Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="92d53-162">На hello **построения** последовательно выберите пункты **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="92d53-162">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="92d53-163">В hello **Configuration Manager** диалоговое окно, выберите hello **построения** и **развернуть** флажки Далее toohello проекта для Android.</span><span class="sxs-lookup"><span data-stu-id="92d53-163">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Android project.</span></span>

4. <span data-ttu-id="92d53-164">toobuild hello проект и запустить приложение hello в эмуляторе Android, выберите hello **F5** ключа.</span><span class="sxs-lookup"><span data-stu-id="92d53-164">toobuild hello project and start hello app in an Android emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="92d53-165">Если возникают проблемы при построении проекта hello, запустите hello NuGet пакета диспетчера и обновления toohello последнюю версию пакеты поддержки Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="92d53-165">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="92d53-166">Примеры использования проектов может быть медленным tooupdate toohello последние версии.</span><span class="sxs-lookup"><span data-stu-id="92d53-166">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="92d53-167">В приложение hello введите значимыми текстовыми, таких как *узнать Xamarin*, и затем выберите Здравствуйте, "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="92d53-167">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="92d53-168">Это действие отправляет toohello запрос post, новые мобильные приложения серверной части, который размещается в Azure.</span><span class="sxs-lookup"><span data-stu-id="92d53-168">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="92d53-169">Данные из запроса hello вставляется в таблицу TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="92d53-169">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="92d53-170">Данные отображаются в списке hello элементов, хранящихся в таблице hello возвращаются по hello заканчивается обратно мобильные приложения и hello.</span><span class="sxs-lookup"><span data-stu-id="92d53-170">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="92d53-171">Вы найдете hello код, который обращается к вашей серверной части мобильных приложений в hello TodoItemManager.cs C# файл hello проекта переносимой библиотеки классов для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="92d53-171">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-windows-project"></a><span data-ttu-id="92d53-172">(Необязательно) Запустите проект Windows hello</span><span class="sxs-lookup"><span data-stu-id="92d53-172">(Optional) Run hello Windows project</span></span>

<span data-ttu-id="92d53-173">В этом разделе выполняется hello Xamarin WinApp проекта для устройств Windows.</span><span class="sxs-lookup"><span data-stu-id="92d53-173">In this section, you run hello Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="92d53-174">Пропустите этот раздел, если вы не работаете с устройствами Windows.</span><span class="sxs-lookup"><span data-stu-id="92d53-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="92d53-175">В Visual Studio</span><span class="sxs-lookup"><span data-stu-id="92d53-175">In Visual Studio</span></span>

1. <span data-ttu-id="92d53-176">Щелкните правой кнопкой мыши проекты Windows hello, а затем выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="92d53-176">Right-click any of hello Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="92d53-177">На hello **построения** последовательно выберите пункты **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="92d53-177">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="92d53-178">В hello **Configuration Manager** диалоговое окно, выберите hello **построения** и **развернуть** флажки Далее toohello проект Windows, выбранное.</span><span class="sxs-lookup"><span data-stu-id="92d53-178">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Windows project that you chose.</span></span>

4. <span data-ttu-id="92d53-179">toobuild hello проект и запустить приложение hello в эмуляторе Windows, выберите hello **F5** ключа.</span><span class="sxs-lookup"><span data-stu-id="92d53-179">toobuild hello project and start hello app in a Windows emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="92d53-180">Если возникают проблемы при построении проекта hello, запустите hello NuGet пакета диспетчера и обновления toohello последнюю версию пакеты поддержки Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="92d53-180">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="92d53-181">Примеры использования проектов может быть медленным tooupdate toohello последние версии.</span><span class="sxs-lookup"><span data-stu-id="92d53-181">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="92d53-182">В приложение hello введите значимыми текстовыми, таких как *узнать Xamarin*, и затем выберите Здравствуйте, "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="92d53-182">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    <span data-ttu-id="92d53-183">Это действие отправляет toohello запрос post, новые мобильные приложения серверной части, который размещается в Azure.</span><span class="sxs-lookup"><span data-stu-id="92d53-183">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="92d53-184">Данные из запроса hello вставляется в таблицу TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="92d53-184">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="92d53-185">Данные отображаются в списке hello элементов, хранящихся в таблице hello возвращаются по hello заканчивается обратно мобильные приложения и hello.</span><span class="sxs-lookup"><span data-stu-id="92d53-185">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="92d53-186">Вы найдете hello код, который обращается к вашей серверной части мобильных приложений в hello TodoItemManager.cs C# файл hello проекта переносимой библиотеки классов для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="92d53-186">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="92d53-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="92d53-187">Next steps</span></span>

* [<span data-ttu-id="92d53-188">Добавить приложение tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="92d53-188">Add authentication tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="92d53-189">Узнайте, как пользователи tooauthenticate приложения с поставщиком удостоверений.</span><span class="sxs-lookup"><span data-stu-id="92d53-189">Learn how tooauthenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="92d53-190">Добавить приложение tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="92d53-190">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="92d53-191">Узнайте, как push-уведомления tooadd поддерживают приложения tooyour и настройте ваши мобильные приложения серверной части toouse концентраторов уведомлений Azure toosend hello push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="92d53-191">Learn how tooadd push notifications support tooyour app and configure your Mobile Apps back end toouse Azure Notification Hubs toosend hello push notifications.</span></span>

* [<span data-ttu-id="92d53-192">Включение автономной синхронизации для приложения</span><span class="sxs-lookup"><span data-stu-id="92d53-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="92d53-193">Узнайте, как tooadd поддержке приложения с помощью мобильных приложений серверной части.</span><span class="sxs-lookup"><span data-stu-id="92d53-193">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="92d53-194">Автономная синхронизация позволяет просматривать, добавлять или изменять данные мобильного приложения даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="92d53-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="92d53-195">Использование hello управляемого клиента для мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="92d53-195">Use hello managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="92d53-196">Узнайте, как toowork с hello управление пакет SDK для клиента приложения Xamarin.</span><span class="sxs-lookup"><span data-stu-id="92d53-196">Learn how toowork with hello managed client SDK in your Xamarin app.</span></span>

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
