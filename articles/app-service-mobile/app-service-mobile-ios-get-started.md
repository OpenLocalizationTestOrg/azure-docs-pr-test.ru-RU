---
title: "Создание мобильного приложения для iOS в службе мобильных приложений Azure | Документация Майкрософт"
description: "Изучите этот учебник, чтобы начать работу с серверным частями мобильных приложений Azure для разработки приложений iOS на Objective-C или Swift"
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 6461a899-9340-42dd-b118-ffc5ba00e846
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 36936ae66c458fcbedeec95cfa2f573a40c8af53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-ios-app"></a><span data-ttu-id="4e64c-103">Создание приложения iOS</span><span class="sxs-lookup"><span data-stu-id="4e64c-103">Create an iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="4e64c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="4e64c-104">Overview</span></span>
<span data-ttu-id="4e64c-105">В этом руководстве показано, как добавить облачную серверную службу [мобильных приложений Azure](app-service-mobile-value-prop.md)в приложение iOS.</span><span class="sxs-lookup"><span data-stu-id="4e64c-105">This tutorial shows how to add [Azure Mobile Apps](app-service-mobile-value-prop.md), a cloud backend service, to an iOS app.</span></span> <span data-ttu-id="4e64c-106">Сначала мы создадим новую серверную часть мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="4e64c-106">We'll first create a new mobile backend.</span></span> <span data-ttu-id="4e64c-107">Затем мы воспользуемся простым приложением iOS *Список дел* для хранения данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="4e64c-107">Then, we'll use a simple *Todo list* iOS app to store data in Azure.</span></span>

<span data-ttu-id="4e64c-108">Для работы с этим учебником требуется [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="4e64c-108">To complete this tutorial, you need a Mac and [an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>

## <a name="step-i-create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="4e64c-109">Шаг 1. Создание серверной части мобильного приложения Azure</span><span class="sxs-lookup"><span data-stu-id="4e64c-109">Step I: Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="step-ii-configure-the-backend-project"></a><span data-ttu-id="4e64c-110">Шаг 2. Настройка проекта серверной части</span><span class="sxs-lookup"><span data-stu-id="4e64c-110">Step II: Configure the backend project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="step-iii-download-and-run-the-ios-app"></a><span data-ttu-id="4e64c-111">Шаг 3. Скачивание и запуск приложения iOS</span><span class="sxs-lookup"><span data-stu-id="4e64c-111">Step III: Download and run the iOS app</span></span>
[!INCLUDE [app-service-mobile-ios-run-app](../../includes/app-service-mobile-ios-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
