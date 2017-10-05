---
title: "Приступая к работе с мобильными приложениями Azure для приложений Xamarin.Android | Microsoft Azure"
description: "Этот учебник поможет приступить к использованию мобильных приложений Azure для разработки приложений Xamarin Android"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 6b41fd8090dd771fc40769c134bad258b3d4bd36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="e8a9e-103">Создание приложения Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="e8a9e-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="e8a9e-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="e8a9e-104">Overview</span></span>
<span data-ttu-id="e8a9e-105">В этом руководстве показано, как добавить облачную серверную службу в приложение Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.Android app.</span></span> <span data-ttu-id="e8a9e-106">Дополнительные сведения см. в статье [Что такое мобильные приложения?](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="e8a9e-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="e8a9e-107">Снимок экрана завершенного приложения приведен ниже:</span><span class="sxs-lookup"><span data-stu-id="e8a9e-107">A screenshot from the completed app is below:</span></span>

![][0]

<span data-ttu-id="e8a9e-108">Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными мобильным приложениям для приложений Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8a9e-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e8a9e-109">Prerequisites</span></span>
<span data-ttu-id="e8a9e-110">Для работы с данным руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e8a9e-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="e8a9e-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-111">An active Azure account.</span></span> <span data-ttu-id="e8a9e-112">Если у вас еще нет учетной записи, зарегистрируйтесь для использования пробной версии Azure и получите до 10 бесплатных мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-112">If you don't have an account, sign up for an Azure trial and get up to 10 free Mobile Apps.</span></span> <span data-ttu-id="e8a9e-113">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8a9e-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e8a9e-114">Visual Studio с Xamarin.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="e8a9e-115">Инструкции см. в статье об [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8a9e-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="e8a9e-116">Создание серверной части мобильного приложения Azure</span><span class="sxs-lookup"><span data-stu-id="e8a9e-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="e8a9e-117">Чтобы создать серверную часть мобильного приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-117">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="e8a9e-118">Итак, вы подготовили серверную часть мобильного Azure, которая может использоваться мобильными клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="e8a9e-119">Теперь скачайте серверный проект со списком простых задач и опубликуйте его в Azure.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-119">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="e8a9e-120">Настройка серверного проекта</span><span class="sxs-lookup"><span data-stu-id="e8a9e-120">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a><span data-ttu-id="e8a9e-121">Скачивание и запуск приложения Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="e8a9e-121">Download and run the Xamarin.Android app</span></span>
1. <span data-ttu-id="e8a9e-122">В разделе **Download and run your Xamarin.Android project** (Загрузка и запуск проекта Xamarin.Android) нажмите кнопку **Download** (Загрузить).</span><span class="sxs-lookup"><span data-stu-id="e8a9e-122">Under **Download and run your Xamarin.Android project**, click the **Download** button.</span></span>

      <span data-ttu-id="e8a9e-123">Сохраните сжатый файл проекта на локальном компьютере и запомните путь к нему.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-123">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="e8a9e-124">Нажмите клавишу **F5** , чтобы выполнить сборку проекта, после чего запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-124">Press the **F5** key to build the project and start the app.</span></span>
3. <span data-ttu-id="e8a9e-125">В приложении введите содержательный текст, например *Работа с руководством*, и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-125">In the app, type meaningful text, such as *Complete the tutorial* and then click the **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="e8a9e-126">Данные из запроса вставляются в таблицу TodoItem.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-126">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="e8a9e-127">Элементы, сохраненные в таблице, возвращаются серверной частью мобильного приложения, а данные отображаются в списке.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-127">Items stored in the table are returned by the mobile app backend, and the data appears in the list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e8a9e-128">Вы можете просмотреть код, который получает доступ к внутреннему серверу мобильного приложения для запроса и вставки данных, которые находятся в файле C# ToDoActivity.cs.</span><span class="sxs-lookup"><span data-stu-id="e8a9e-128">You can review the code that accesses your mobile app backend to query and insert data, which is found in the ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="e8a9e-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e8a9e-129">Next steps</span></span>
* [<span data-ttu-id="e8a9e-130">Включение автономной синхронизации для мобильного приложения Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="e8a9e-130">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="e8a9e-131">Добавление проверки подлинности в приложение</span><span class="sxs-lookup"><span data-stu-id="e8a9e-131">Add authentication to your app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="e8a9e-132">Добавление push-уведомлений в приложение Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="e8a9e-132">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="e8a9e-133">Использование управляемого клиента для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e8a9e-133">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
