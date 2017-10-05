---
title: "Создание универсальной платформы Windows (UWP) для использования в мобильных приложениях | Документация Майкрософт"
description: "Следуйте указаниям этого руководства, чтобы начать работу с серверной частью мобильных приложений Azure для разработки приложений универсальной платформы Windows (UWP) на C#, Visual Basic или JavaScript."
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
ms.openlocfilehash: 5408e032670dda7f149c442e08f52b02abe23f05
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="82e5f-103">Создание приложения Windows</span><span class="sxs-lookup"><span data-stu-id="82e5f-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="82e5f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="82e5f-104">Overview</span></span>
<span data-ttu-id="82e5f-105">В этом руководстве показано, как добавить облачную серверную службу в универсальную платформу Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="82e5f-105">This tutorial shows you how to add a cloud-based backend service to a Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="82e5f-106">Дополнительные сведения см. в статье [Общие сведения о мобильных приложениях](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="82e5f-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="82e5f-107">Ниже приведены снимки экрана готового приложения.</span><span class="sxs-lookup"><span data-stu-id="82e5f-107">The following are screen captures from the completed app:</span></span>

![Готовое классическое приложение](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="82e5f-109">Выполняется на настольном компьютере.</span><span class="sxs-lookup"><span data-stu-id="82e5f-109">Running on a desktop.</span></span>

![Готовое приложение для телефона](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="82e5f-111">Выполняется на телефоне.</span><span class="sxs-lookup"><span data-stu-id="82e5f-111">Running on a phone</span></span>

<span data-ttu-id="82e5f-112">Изучение этого руководства является необходимым условием для работы со всеми остальными руководствами, посвященными мобильным приложениям UWP.</span><span class="sxs-lookup"><span data-stu-id="82e5f-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82e5f-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="82e5f-113">Prerequisites</span></span>
<span data-ttu-id="82e5f-114">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="82e5f-114">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="82e5f-115">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="82e5f-115">An active Azure account.</span></span> <span data-ttu-id="82e5f-116">Если у вас нет учетной записи, можно зарегистрироваться для получения бесплатной пробной версии Azure и получить до 10 бесплатных мобильных приложений, которые можно использовать и после окончания пробного периода.</span><span class="sxs-lookup"><span data-stu-id="82e5f-116">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="82e5f-117">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82e5f-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="82e5f-118">[Visual Studio Community 2015] или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="82e5f-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="82e5f-119">Создание серверной части мобильного приложения Azure</span><span class="sxs-lookup"><span data-stu-id="82e5f-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="82e5f-120">Чтобы создать серверную часть мобильного приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="82e5f-120">Follow these steps to create a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="82e5f-121">Итак, вы подготовили серверную часть мобильного Azure, которая может использоваться мобильными клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="82e5f-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="82e5f-122">Теперь скачайте серверный проект со списком простых задач и опубликуйте его в Azure.</span><span class="sxs-lookup"><span data-stu-id="82e5f-122">Next, you will download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="82e5f-123">Настройка серверного проекта</span><span class="sxs-lookup"><span data-stu-id="82e5f-123">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-client-project"></a><span data-ttu-id="82e5f-124">Скачивание и выполнение клиентского проекта</span><span class="sxs-lookup"><span data-stu-id="82e5f-124">Download and run the client project</span></span>
<span data-ttu-id="82e5f-125">Настроив серверную часть мобильного приложения, можно создать новое клиентское приложение или изменить существующее приложение, чтобы подключиться к Azure.</span><span class="sxs-lookup"><span data-stu-id="82e5f-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app to connect to Azure.</span></span> <span data-ttu-id="82e5f-126">В этом разделе вы загрузите проект шаблона UWP, который настроен для подключения к серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="82e5f-126">In this section, you download a UWP app template project that is customized to connect to your Mobile App backend.</span></span>

1. <span data-ttu-id="82e5f-127">Вернитесь в колонку **Быстрый запуск** серверной части мобильного приложения и последовательно выберите элементы **Создать новое приложение** > **Загрузить**. Затем извлеките сжатые файлы проекта на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="82e5f-127">Back in the **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract the compressed project files to your local computer.</span></span>

    ![Загрузка проекта быстрого запуска Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="82e5f-129">(Необязательно) Добавьте в то же решение проект приложения UWP в качестве серверного проекта.</span><span class="sxs-lookup"><span data-stu-id="82e5f-129">(Optional) Add the UWP app project to the same solution as the server project.</span></span> <span data-ttu-id="82e5f-130">Это упрощает отладку и тестирование приложения и серверной части в одном решении Visual Studio, если вам это потребуется.</span><span class="sxs-lookup"><span data-stu-id="82e5f-130">This makes it easier to debug and test both the app and the backend in the same Visual Studio solution, if you choose to do so.</span></span> <span data-ttu-id="82e5f-131">Чтобы добавить в решение проект приложения UWP, необходимо использовать Visual Studio 2015 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="82e5f-131">To add a UWP app project to the solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="82e5f-132">Задав приложение UWP как запускаемый проект, нажмите клавишу F5, чтобы развернуть и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="82e5f-132">With the UWP app as the startup project, press the F5 key to deploy and run the app.</span></span>
4. <span data-ttu-id="82e5f-133">В приложении в поле **Insert a TodoItem** (Вставить TodoItem) введите содержательный текст, например *Работа с руководством*, и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="82e5f-133">In the app, type meaningful text, such as *Complete the tutorial*, in the **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Полный быстрый запуск Windows — классическая версия](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="82e5f-135">В результате будет отправлен запрос POST к серверной части нового мобильного приложения, размещенного в Azure.</span><span class="sxs-lookup"><span data-stu-id="82e5f-135">This sends a POST request to the new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="82e5f-136">(Необязательно) Остановите приложение и перезапустите его на другом устройстве или эмуляторе мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="82e5f-136">(Optional) Stop the app and restart it on a different device or mobile emulator.</span></span>

    ![Полный быстрый запуск Windows — мобильная версия](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="82e5f-138">Обратите внимание, что данные, сохраненные на предыдущем этапе, загружаются из Azure после запуска приложения UWP.</span><span class="sxs-lookup"><span data-stu-id="82e5f-138">Notice that data saved from the previous step is loaded from Azure after the UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82e5f-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82e5f-139">Next steps</span></span>
* [<span data-ttu-id="82e5f-140">Добавление аутентификации в приложение</span><span class="sxs-lookup"><span data-stu-id="82e5f-140">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="82e5f-141">Узнайте больше о проверке подлинности пользователей приложения с помощью поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="82e5f-141">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="82e5f-142">Добавление push-уведомлений в приложение</span><span class="sxs-lookup"><span data-stu-id="82e5f-142">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="82e5f-143">Узнайте, как добавить поддержку push-уведомлений в мобильное приложение и настроить в его серверной части использование концентраторов уведомлений Azure для отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="82e5f-143">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="82e5f-144">Включение автономной синхронизации для приложения</span><span class="sxs-lookup"><span data-stu-id="82e5f-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="82e5f-145">Узнайте, как добавить в приложение поддержку автономной работы с помощью серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="82e5f-145">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="82e5f-146">Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением &mdash; просматривать, добавлять или изменять данные &mdash; даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="82e5f-146">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
<span data-ttu-id="82e5f-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span><span class="sxs-lookup"><span data-stu-id="82e5f-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span></span>
