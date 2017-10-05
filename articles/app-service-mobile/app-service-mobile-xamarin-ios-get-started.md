---
title: "Приступая к работе с мобильными приложениями службы приложений Azure для приложений Xamarin.iOS | Документация Майкрософт"
description: "Этот учебник поможет приступить к использованию мобильных приложений в разработке для Xamarin.iOS."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 8dc965df2cd45366970effb29f246b0045a94717
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="18c38-103">Создание приложения Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="18c38-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="18c38-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="18c38-104">Overview</span></span>
<span data-ttu-id="18c38-105">В этом учебнике рассказывается, как добавить облачную серверную службу в мобильное приложение Xamarin.iOS с помощью серверной части мобильного приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="18c38-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="18c38-106">Вы создадите новую серверную часть мобильного приложения и простое приложение Xamarin.iOS *Todo list*, в котором в Azure хранятся данные приложения.</span><span class="sxs-lookup"><span data-stu-id="18c38-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="18c38-107">Завершение этого учебника является необходимым условием для других учебников по Xamarin.iOS, посвященных использованию функции мобильных приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="18c38-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18c38-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="18c38-108">Prerequisites</span></span>
<span data-ttu-id="18c38-109">Для работы с данным руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="18c38-109">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="18c38-110">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="18c38-110">An active Azure account.</span></span> <span data-ttu-id="18c38-111">Если у вас нет учетной записи, зарегистрируйтесь для получения бесплатной пробной версии Azure и получите до 10 бесплатных мобильных приложений, которые можно использовать и после окончания пробного периода.</span><span class="sxs-lookup"><span data-stu-id="18c38-111">If you don't have an account, sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="18c38-112">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18c38-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="18c38-113">Visual Studio с Xamarin.</span><span class="sxs-lookup"><span data-stu-id="18c38-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="18c38-114">Инструкции см. в статье об [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="18c38-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="18c38-115">Компьютер Mac с установленным ПО XCode версии 7.0 или выше и Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="18c38-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="18c38-116">См. статьи об [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) и [установке, настройке и проверке для пользователей Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="18c38-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="18c38-117">Создание серверной части мобильного приложения Azure</span><span class="sxs-lookup"><span data-stu-id="18c38-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="18c38-118">Чтобы создать серверную часть мобильного приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="18c38-118">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="18c38-119">Настройка серверного проекта</span><span class="sxs-lookup"><span data-stu-id="18c38-119">Configure the server project</span></span>
<span data-ttu-id="18c38-120">Итак, вы подготовили серверную часть мобильного Azure, которая может использоваться мобильными клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="18c38-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="18c38-121">Теперь скачайте серверный проект со списком простых задач и опубликуйте его в Azure.</span><span class="sxs-lookup"><span data-stu-id="18c38-121">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

<span data-ttu-id="18c38-122">Выполните следующие действия, чтобы настроить серверный проект для использования серверной части .NET или Node.js.</span><span class="sxs-lookup"><span data-stu-id="18c38-122">Follow the following steps to configure the server project to use either the Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinios-app"></a><span data-ttu-id="18c38-123">Скачивание и запуск приложения Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="18c38-123">Download and run the Xamarin.iOS app</span></span>
1. <span data-ttu-id="18c38-124">В окне браузера откройте [портал Azure] .</span><span class="sxs-lookup"><span data-stu-id="18c38-124">Open the [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="18c38-125">В колонке параметров мобильного приложения щелкните **Приступая к работе** > **Xamarin.iOS**.</span><span class="sxs-lookup"><span data-stu-id="18c38-125">On the settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="18c38-126">На этапе 3 нажмите кнопку **Создать приложение** (если вы еще не сделали этого).</span><span class="sxs-lookup"><span data-stu-id="18c38-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="18c38-127">Затем нажмите кнопку **Загрузить** .</span><span class="sxs-lookup"><span data-stu-id="18c38-127">Next click the **Download** button.</span></span>

      <span data-ttu-id="18c38-128">После этого клиентское приложение, которое подключается к серверной части мобильной службы, будет скачано.</span><span class="sxs-lookup"><span data-stu-id="18c38-128">A client application that connects to your mobile backend is downloaded.</span></span> <span data-ttu-id="18c38-129">Сохраните сжатый файл проекта на локальном компьютере и запомните путь к нему.</span><span class="sxs-lookup"><span data-stu-id="18c38-129">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="18c38-130">Извлеките скачанный проект и откройте его в Xamarin Studio (или Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="18c38-130">Extract the project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="18c38-131">Нажмите клавишу F5, чтобы выполнить сборку проекта и запустить приложение в эмуляторе iPhone.</span><span class="sxs-lookup"><span data-stu-id="18c38-131">Press the F5 key to build the project and start the app in the iPhone emulator.</span></span>
5. <span data-ttu-id="18c38-132">В приложении введите содержательный текст, например *Изучение Xamarin*, и нажмите кнопку **+**.</span><span class="sxs-lookup"><span data-stu-id="18c38-132">In the app, type meaningful text, such as *Learn Xamarin*, and then click the **+** button.</span></span>

    ![][10]

    <span data-ttu-id="18c38-133">Данные из запроса вставляются в таблицу TodoItem.</span><span class="sxs-lookup"><span data-stu-id="18c38-133">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="18c38-134">Элементы, хранящиеся в таблице, возвращаются серверной частью мобильной службы, а данные отображаются в списке.</span><span class="sxs-lookup"><span data-stu-id="18c38-134">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span></span>

> [!NOTE]
> <span data-ttu-id="18c38-135">Код, который обращается к серверной части вашей мобильной службы для запроса и вставки данных, можно просмотреть в файле C# QSTodoService.cs.</span><span class="sxs-lookup"><span data-stu-id="18c38-135">You can review the code that accesses your mobile app backend to query and insert data in the QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="18c38-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18c38-136">Next steps</span></span>
* [<span data-ttu-id="18c38-137">Включение автономной синхронизации для мобильного приложения Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="18c38-137">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="18c38-138">Добавление проверки подлинности в приложение</span><span class="sxs-lookup"><span data-stu-id="18c38-138">Add authentication to your app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="18c38-139">Добавление push-уведомлений в приложение Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="18c38-139">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="18c38-140">Использование управляемого клиента для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="18c38-140">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
<span data-ttu-id="18c38-141">[портал Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="18c38-141">[Azure portal]: https://portal.azure.com/</span></span>
