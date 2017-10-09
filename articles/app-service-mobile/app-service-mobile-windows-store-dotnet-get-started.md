---
title: "aaaCreate универсальной платформы Windows (UWP), использующий мобильных приложений | Документы Microsoft"
description: "Выполните этот учебник tooget работы с помощью серверных системах мобильного приложения Azure для разработки приложений универсальной платформы Windows (UWP) в C#, Visual Basic или JavaScript."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="589b3-103">Создание приложения Windows</span><span class="sxs-lookup"><span data-stu-id="589b3-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="589b3-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="589b3-104">Overview</span></span>
<span data-ttu-id="589b3-105">Этот учебник показывает, как tooadd облачную серверную службу tooa приложения универсальной платформы Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="589b3-105">This tutorial shows you how tooadd a cloud-based backend service tooa Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="589b3-106">Дополнительные сведения см. в статье [Что такое мобильные приложения?](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="589b3-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="589b3-107">Hello ниже приведены снимки экрана из приложения hello завершена.</span><span class="sxs-lookup"><span data-stu-id="589b3-107">hello following are screen captures from hello completed app:</span></span>

![Готовое классическое приложение](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="589b3-109">Выполняется на настольном компьютере.</span><span class="sxs-lookup"><span data-stu-id="589b3-109">Running on a desktop.</span></span>

![Готовое приложение для телефона](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="589b3-111">Выполняется на телефоне.</span><span class="sxs-lookup"><span data-stu-id="589b3-111">Running on a phone</span></span>

<span data-ttu-id="589b3-112">Изучение этого руководства является необходимым условием для работы со всеми остальными руководствами, посвященными мобильным приложениям UWP.</span><span class="sxs-lookup"><span data-stu-id="589b3-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="589b3-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="589b3-113">Prerequisites</span></span>
<span data-ttu-id="589b3-114">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="589b3-114">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="589b3-115">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="589b3-115">An active Azure account.</span></span> <span data-ttu-id="589b3-116">При отсутствии учетной записи, можно зарегистрироваться в пробной версии Azure и получите бесплатные too10 мобильных приложений, которые вы можете продолжать использовать даже после окончания срока действия пробной версии никакие.</span><span class="sxs-lookup"><span data-stu-id="589b3-116">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="589b3-117">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="589b3-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="589b3-118">[Visual Studio Community 2015] или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="589b3-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="589b3-119">Создание серверной части мобильного приложения Azure</span><span class="sxs-lookup"><span data-stu-id="589b3-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="589b3-120">Выполните эти шаги toocreate новую серверную часть мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="589b3-120">Follow these steps toocreate a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="589b3-121">Итак, вы подготовили серверную часть мобильного Azure, которая может использоваться мобильными клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="589b3-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="589b3-122">Затем будет загрузить проект сервера для простого «todo list» серверная часть и опубликовать его tooAzure.</span><span class="sxs-lookup"><span data-stu-id="589b3-122">Next, you will download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="589b3-123">Настройка проекта сервера hello</span><span class="sxs-lookup"><span data-stu-id="589b3-123">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a><span data-ttu-id="589b3-124">Загрузите и запустите клиентский проект hello</span><span class="sxs-lookup"><span data-stu-id="589b3-124">Download and run hello client project</span></span>
<span data-ttu-id="589b3-125">Настроив внутренний сервер приложений для мобильных устройств, можно создавать приложения для клиента или изменить существующие приложения tooAzure tooconnect.</span><span class="sxs-lookup"><span data-stu-id="589b3-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app tooconnect tooAzure.</span></span> <span data-ttu-id="589b3-126">В этом разделе загрузите шаблон проекта приложения UWP, настроенные tooconnect tooyour мобильное приложение серверной.</span><span class="sxs-lookup"><span data-stu-id="589b3-126">In this section, you download a UWP app template project that is customized tooconnect tooyour Mobile App backend.</span></span>

1. <span data-ttu-id="589b3-127">Обратно в hello **краткого** колонке серверной части мобильное приложение, нажмите кнопку **создайте новое приложение** > **загрузки**, затем извлечь hello сжатые файлы проекта tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="589b3-127">Back in hello **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract hello compressed project files tooyour local computer.</span></span>

    ![Загрузка проекта быстрого запуска Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="589b3-129">(Необязательно) Добавить toohello проекта приложения UWP hello же решении, что проект сервера hello.</span><span class="sxs-lookup"><span data-stu-id="589b3-129">(Optional) Add hello UWP app project toohello same solution as hello server project.</span></span> <span data-ttu-id="589b3-130">Это упрощает toodebug и тестирования, оба hello серверной части приложения и hello в hello того же решения Visual Studio, при выборе toodo это.</span><span class="sxs-lookup"><span data-stu-id="589b3-130">This makes it easier toodebug and test both hello app and hello backend in hello same Visual Studio solution, if you choose toodo so.</span></span> <span data-ttu-id="589b3-131">tooadd toohello решения проекта приложения UWP, необходимо использовать Visual Studio 2015 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="589b3-131">tooadd a UWP app project toohello solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="589b3-132">Приложение UWP hello hello запускаемым проектом нажмите toodeploy клавиш F5 hello и приложение hello выполнения.</span><span class="sxs-lookup"><span data-stu-id="589b3-132">With hello UWP app as hello startup project, press hello F5 key toodeploy and run hello app.</span></span>
4. <span data-ttu-id="589b3-133">В приложение hello введите значимыми текстовыми, таких как *завершения hello учебника*, в hello **Insert a TodoItem** текстовое поле и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="589b3-133">In hello app, type meaningful text, such as *Complete hello tutorial*, in hello **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Полный быстрый запуск Windows — классическая версия](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="589b3-135">Это приведет к отправке POST запроса toohello новую мобильное приложение серверную часть, размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="589b3-135">This sends a POST request toohello new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="589b3-136">(Необязательно) Остановите приложение hello и перезапустите его на другое устройство или эмулятор мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="589b3-136">(Optional) Stop hello app and restart it on a different device or mobile emulator.</span></span>

    ![Полный быстрый запуск Windows — мобильная версия](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="589b3-138">Обратите внимание, что данных, сохраненный при выполнении предыдущего шага hello загружается из Azure после запуска приложения UWP hello.</span><span class="sxs-lookup"><span data-stu-id="589b3-138">Notice that data saved from hello previous step is loaded from Azure after hello UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="589b3-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="589b3-139">Next steps</span></span>
* [<span data-ttu-id="589b3-140">Добавить приложение tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="589b3-140">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="589b3-141">Узнайте, как пользователи tooauthenticate приложения с поставщиком удостоверений.</span><span class="sxs-lookup"><span data-stu-id="589b3-141">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="589b3-142">Добавить приложение tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="589b3-142">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="589b3-143">Узнайте, как push-уведомления tooadd поддерживают tooyour приложения и настройки вашего мобильного приложения серверной toouse концентраторов уведомлений Azure toosend push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="589b3-143">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="589b3-144">Включение автономной синхронизации для приложения</span><span class="sxs-lookup"><span data-stu-id="589b3-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="589b3-145">Узнайте, как автономные tooadd поддерживают приложения с помощью внутреннего сервера мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="589b3-145">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="589b3-146">Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением&mdash;Просмотр, добавление или изменение данных&mdash;даже в том случае, если нет сетевого соединения.</span><span class="sxs-lookup"><span data-stu-id="589b3-146">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
