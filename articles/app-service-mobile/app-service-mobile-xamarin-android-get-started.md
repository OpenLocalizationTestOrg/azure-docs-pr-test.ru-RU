---
title: "aaaGet работает с приложениями Azure Mobile для приложений Xamarin.Android"
description: "Выполните этот учебник tooget работы с использованием мобильных приложений Azure для разработки Xamarin Android"
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
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="6cc75-103">Создание приложения Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="6cc75-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="6cc75-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6cc75-104">Overview</span></span>
<span data-ttu-id="6cc75-105">Этот учебник показывает, как tooadd облачную серверную службу tooa Xamarin.Android приложения.</span><span class="sxs-lookup"><span data-stu-id="6cc75-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.Android app.</span></span> <span data-ttu-id="6cc75-106">Дополнительные сведения см. в статье [Что такое мобильные приложения?](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="6cc75-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="6cc75-107">Снимок экрана из приложения hello завершения используется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6cc75-107">A screenshot from hello completed app is below:</span></span>

![][0]

<span data-ttu-id="6cc75-108">Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными мобильным приложениям для приложений Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="6cc75-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cc75-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6cc75-109">Prerequisites</span></span>
<span data-ttu-id="6cc75-110">toocomplete этого учебника требуется hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="6cc75-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="6cc75-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6cc75-111">An active Azure account.</span></span> <span data-ttu-id="6cc75-112">При отсутствии учетной записи, зарегистрироваться для пробной версии Azure и приступить к too10 бесплатные приложения для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="6cc75-112">If you don't have an account, sign up for an Azure trial and get up too10 free Mobile Apps.</span></span> <span data-ttu-id="6cc75-113">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6cc75-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6cc75-114">Visual Studio с Xamarin.</span><span class="sxs-lookup"><span data-stu-id="6cc75-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="6cc75-115">Инструкции см. в статье об [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="6cc75-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="6cc75-116">Создание серверной части мобильного приложения Azure</span><span class="sxs-lookup"><span data-stu-id="6cc75-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="6cc75-117">Выполните эти шаги toocreate серверной мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="6cc75-117">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="6cc75-118">Итак, вы подготовили серверную часть мобильного Azure, которая может использоваться мобильными клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="6cc75-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="6cc75-119">Затем загрузить проект сервера для простого «todo list» серверная часть и опубликовать его tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6cc75-119">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="6cc75-120">Настройка проекта сервера hello</span><span class="sxs-lookup"><span data-stu-id="6cc75-120">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a><span data-ttu-id="6cc75-121">Загрузите и запустите приложение Xamarin.Android hello</span><span class="sxs-lookup"><span data-stu-id="6cc75-121">Download and run hello Xamarin.Android app</span></span>
1. <span data-ttu-id="6cc75-122">В разделе **загрузки и запуска проекта Xamarin.Android**, нажмите кнопку hello **загрузки** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6cc75-122">Under **Download and run your Xamarin.Android project**, click hello **Download** button.</span></span>

      <span data-ttu-id="6cc75-123">Сохраните hello проекта сжатый файл tooyour локального компьютера и запишите где его сохранить.</span><span class="sxs-lookup"><span data-stu-id="6cc75-123">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="6cc75-124">Нажмите клавишу hello **F5** ключа toobuild hello проект и запустить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="6cc75-124">Press hello **F5** key toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="6cc75-125">В приложение hello введите значимыми текстовыми, таких как *завершения hello учебника* и нажмите кнопку hello **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6cc75-125">In hello app, type meaningful text, such as *Complete hello tutorial* and then click hello **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="6cc75-126">Данные из запроса hello вставляется в таблицу TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="6cc75-126">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="6cc75-127">Элементы, хранящиеся в таблице hello возвращаются сервером мобильного приложения hello, и данные в списке hello.</span><span class="sxs-lookup"><span data-stu-id="6cc75-127">Items stored in hello table are returned by hello mobile app backend, and the data appears in hello list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6cc75-128">Можно просмотреть hello код, который обращается к tooquery серверной части вашего мобильного приложения и вставки данных, относящийся к hello файл ToDoActivity.cs C#.</span><span class="sxs-lookup"><span data-stu-id="6cc75-128">You can review hello code that accesses your mobile app backend tooquery and insert data, which is found in hello ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="6cc75-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6cc75-129">Next steps</span></span>
* [<span data-ttu-id="6cc75-130">Добавить приложение tooyour автономной синхронизации</span><span class="sxs-lookup"><span data-stu-id="6cc75-130">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="6cc75-131">Добавить приложение tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6cc75-131">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="6cc75-132">Добавить приложение Xamarin.Android tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="6cc75-132">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="6cc75-133">Управление toouse hello клиента для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="6cc75-133">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
