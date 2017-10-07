---
title: "aaaCreate приложения Cordova на мобильные приложения службы приложений Azure | Документы Microsoft"
description: "Выполните этот учебник tooget работы с помощью серверных системах мобильного приложения Azure для разработки приложений Apache Cordova"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: "cordova, javascript, мобильный, клиент"
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="5a77e-104">Создание приложения Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="5a77e-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="5a77e-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="5a77e-105">Overview</span></span>
<span data-ttu-id="5a77e-106">Этот учебник показывает, как tooadd облачную серверную службу мобильного приложения Apache Cordova tooan с помощью внутреннего мобильного приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="5a77e-106">This tutorial shows you how tooadd a cloud-based backend service tooan Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="5a77e-107">Мы создадим серверную часть мобильного приложения и простое приложение *списка задач* (на платформе Apache Cordova), которое хранит свои данные в Azure.</span><span class="sxs-lookup"><span data-stu-id="5a77e-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="5a77e-108">Изучения этого учебника является необходимым условием для всех других Apache Cordova учебников по использованию функции hello мобильные приложения в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="5a77e-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a77e-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5a77e-109">Prerequisites</span></span>
<span data-ttu-id="5a77e-110">toocomplete этого учебника требуется hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="5a77e-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="5a77e-111">компьютер с [Visual Studio Community 2017] или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="5a77e-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="5a77e-112">[набор средств Visual Studio для Apache Cordova];</span><span class="sxs-lookup"><span data-stu-id="5a77e-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="5a77e-113">[Активная учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a77e-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="5a77e-114">Также можно обойти Visual Studio и непосредственно использовать hello Apache Cordova командной строки.</span><span class="sxs-lookup"><span data-stu-id="5a77e-114">You may also bypass Visual Studio and use hello Apache Cordova command line directly.</span></span>  <span data-ttu-id="5a77e-115">С помощью командной строки hello полезно при изучении hello руководства на компьютере Mac.</span><span class="sxs-lookup"><span data-stu-id="5a77e-115">Using hello command line is useful when completing hello tutorial on a Mac computer.</span></span>  <span data-ttu-id="5a77e-116">В этот учебник компиляции клиентских приложений Apache Cordova, с помощью командной строки hello не рассматривается.</span><span class="sxs-lookup"><span data-stu-id="5a77e-116">Compiling Apache Cordova client applications using hello command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="5a77e-117">Создание серверной части мобильного приложения Azure</span><span class="sxs-lookup"><span data-stu-id="5a77e-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="5a77e-118">Видео, демонстрирующее аналогичные действия</span><span class="sxs-lookup"><span data-stu-id="5a77e-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a><span data-ttu-id="5a77e-119">Настройка проекта сервера hello</span><span class="sxs-lookup"><span data-stu-id="5a77e-119">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a><span data-ttu-id="5a77e-120">Загрузите и запустите приложение hello Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="5a77e-120">Download and run hello Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="5a77e-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a77e-121">Next Steps</span></span>
<span data-ttu-id="5a77e-122">Теперь, когда вы выполнили этого краткого руководства, переместите на tooone из hello следующие учебники:</span><span class="sxs-lookup"><span data-stu-id="5a77e-122">Now that you completed this quick start tutorial, move on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="5a77e-123">[Добавление автономных данных](app-service-mobile-cordova-get-started-offline-data.md) tooyour приложения Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="5a77e-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="5a77e-124">[Добавление проверки подлинности](app-service-mobile-cordova-get-started-users.md) tooyour приложения Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="5a77e-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="5a77e-125">[Добавление Push-уведомления](app-service-mobile-cordova-get-started-push.md) tooyour приложения Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="5a77e-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.</span></span>

<span data-ttu-id="5a77e-126">Дополнительные сведения об основных понятиях, связанных со службой приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="5a77e-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="5a77e-127">[Автономные данные]</span><span class="sxs-lookup"><span data-stu-id="5a77e-127">[Offline Data]</span></span>
* <span data-ttu-id="5a77e-128">[Аутентификация]</span><span class="sxs-lookup"><span data-stu-id="5a77e-128">[Authentication]</span></span>
* <span data-ttu-id="5a77e-129">[Push-уведомления]</span><span class="sxs-lookup"><span data-stu-id="5a77e-129">[Push Notifications]</span></span>

<span data-ttu-id="5a77e-130">Узнайте, как toouse hello пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="5a77e-130">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="5a77e-131">[Пакет SDK для Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="5a77e-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="5a77e-132">[Серверный пакет SDK для ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="5a77e-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="5a77e-133">[Серверный пакет SDK для Node.js]</span><span class="sxs-lookup"><span data-stu-id="5a77e-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[набор средств Visual Studio для Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Автономные данные]: app-service-mobile-offline-data-sync.md
[Аутентификация]: app-service-mobile-auth.md
[Push-уведомления]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Пакет SDK для Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[Серверный пакет SDK для ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Серверный пакет SDK для Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
