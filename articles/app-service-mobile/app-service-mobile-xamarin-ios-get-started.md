---
title: "aaaGet работы с мобильные приложения службы приложений Azure для приложения Xamarin.iOS | Документы Microsoft"
description: "Выполните этот учебник tooget работы с помощью мобильных приложений для разработки Xamarin.iOS."
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
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="59d27-103">Создание приложения Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="59d27-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="59d27-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="59d27-104">Overview</span></span>
<span data-ttu-id="59d27-105">Этот учебник показывает, как tooadd облачную серверную службу tooa Xamarin.iOS мобильного приложения с помощью внутреннего мобильного приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="59d27-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="59d27-106">Вы создадите новую серверную часть мобильного приложения и простое приложение Xamarin.iOS *Todo list*, в котором в Azure хранятся данные приложения.</span><span class="sxs-lookup"><span data-stu-id="59d27-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="59d27-107">Изучения этого учебника является необходимым условием для всех других Xamarin.iOS учебников по использованию функции hello мобильные приложения в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="59d27-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59d27-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="59d27-108">Prerequisites</span></span>
<span data-ttu-id="59d27-109">toocomplete этого учебника требуется hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="59d27-109">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="59d27-110">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="59d27-110">An active Azure account.</span></span> <span data-ttu-id="59d27-111">Если у вас нет учетной записи, зарегистрируйтесь в пробной версии Azure и получите бесплатные too10 мобильных приложений, которые вы можете продолжать использовать даже после окончания срока действия пробной версии никакие.</span><span class="sxs-lookup"><span data-stu-id="59d27-111">If you don't have an account, sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="59d27-112">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59d27-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="59d27-113">Visual Studio с Xamarin.</span><span class="sxs-lookup"><span data-stu-id="59d27-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="59d27-114">Инструкции см. в статье об [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="59d27-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="59d27-115">Компьютер Mac с установленным ПО XCode версии 7.0 или выше и Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="59d27-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="59d27-116">См. статьи об [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) и [установке, настройке и проверке для пользователей Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="59d27-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="59d27-117">Создание серверной части мобильного приложения Azure</span><span class="sxs-lookup"><span data-stu-id="59d27-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="59d27-118">Выполните эти шаги toocreate серверной мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="59d27-118">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="59d27-119">Настройка проекта сервера hello</span><span class="sxs-lookup"><span data-stu-id="59d27-119">Configure hello server project</span></span>
<span data-ttu-id="59d27-120">Итак, вы подготовили серверную часть мобильного Azure, которая может использоваться мобильными клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="59d27-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="59d27-121">Затем загрузить проект сервера для простого «todo list» серверная часть и опубликовать его tooAzure.</span><span class="sxs-lookup"><span data-stu-id="59d27-121">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

<span data-ttu-id="59d27-122">Выполните следующие шаги tooconfigure hello server проекта toouse hello либо серверной части hello .NET или Node.js.</span><span class="sxs-lookup"><span data-stu-id="59d27-122">Follow hello following steps tooconfigure hello server project toouse either hello Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a><span data-ttu-id="59d27-123">Загрузите и запустите приложение Xamarin.iOS hello</span><span class="sxs-lookup"><span data-stu-id="59d27-123">Download and run hello Xamarin.iOS app</span></span>
1. <span data-ttu-id="59d27-124">Откройте hello [портал Azure] в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="59d27-124">Open hello [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="59d27-125">В колонке параметров hello для мобильного приложения, нажмите кнопку **начать** > **Xamarin.iOS**.</span><span class="sxs-lookup"><span data-stu-id="59d27-125">On hello settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="59d27-126">На этапе 3 нажмите кнопку **Создать приложение** (если вы еще не сделали этого).</span><span class="sxs-lookup"><span data-stu-id="59d27-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="59d27-127">Далее щелкните hello **загрузки** кнопки.</span><span class="sxs-lookup"><span data-stu-id="59d27-127">Next click hello **Download** button.</span></span>

      <span data-ttu-id="59d27-128">Клиентское приложение, которое подключается мобильной серверной части tooyour загружается.</span><span class="sxs-lookup"><span data-stu-id="59d27-128">A client application that connects tooyour mobile backend is downloaded.</span></span> <span data-ttu-id="59d27-129">Сохраните файл проекта сжатых hello на локальный компьютер и запишите где сохранить.</span><span class="sxs-lookup"><span data-stu-id="59d27-129">Save hello compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="59d27-130">Извлеките hello проекта, который вы загрузили и откройте его в Xamarin Studio (или Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="59d27-130">Extract hello project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="59d27-131">Нажмите клавишу ключа toobuild hello hello F5 проект и запустить приложение hello в эмуляторе iPhone hello.</span><span class="sxs-lookup"><span data-stu-id="59d27-131">Press hello F5 key toobuild hello project and start hello app in hello iPhone emulator.</span></span>
5. <span data-ttu-id="59d27-132">В приложение hello введите значимыми текстовыми, таких как *узнать Xamarin*и нажмите кнопку hello  **+**  кнопки.</span><span class="sxs-lookup"><span data-stu-id="59d27-132">In hello app, type meaningful text, such as *Learn Xamarin*, and then click hello **+** button.</span></span>

    ![][10]

    <span data-ttu-id="59d27-133">Данные из запроса hello вставляется в таблицу TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="59d27-133">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="59d27-134">Элементы, хранящиеся в таблице hello возвращаются сервером мобильного приложения hello, а данные отображаются в списке hello.</span><span class="sxs-lookup"><span data-stu-id="59d27-134">Items stored in hello table are returned by hello mobile app backend, and the data is displayed in hello list.</span></span>

> [!NOTE]
> <span data-ttu-id="59d27-135">Можно просмотреть hello код, который обращается к tooquery серверной части вашего мобильного приложения и вставить данные в файл QSTodoService.cs C# hello.</span><span class="sxs-lookup"><span data-stu-id="59d27-135">You can review hello code that accesses your mobile app backend tooquery and insert data in hello QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="59d27-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59d27-136">Next steps</span></span>
* [<span data-ttu-id="59d27-137">Добавить приложение tooyour автономной синхронизации</span><span class="sxs-lookup"><span data-stu-id="59d27-137">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="59d27-138">Добавить приложение tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="59d27-138">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="59d27-139">Добавить приложение Xamarin.Android tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="59d27-139">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="59d27-140">Управление toouse hello клиента для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="59d27-140">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

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
[портал Azure]: https://portal.azure.com/
