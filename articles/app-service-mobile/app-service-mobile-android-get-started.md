---
title: "aaaCreate приложение Android на мобильные приложения службы приложений Azure | Документы Microsoft"
description: "Выполните этот учебник tooget работы с помощью серверных системах мобильного приложения Azure для разработки приложений Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="61158-103">Создание приложения Android</span><span class="sxs-lookup"><span data-stu-id="61158-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="61158-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="61158-104">Overview</span></span>
<span data-ttu-id="61158-105">Этот учебник показывает, как tooadd облачную серверную службу tooan мобильное приложение Android с помощью внутреннего мобильного приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="61158-105">This tutorial shows you how tooadd a cloud-based backend service tooan Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="61158-106">Мы создадим серверную часть мобильного приложения и простое приложение *списка дел* (на платформе Android), которое хранит свои данные в Azure.</span><span class="sxs-lookup"><span data-stu-id="61158-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="61158-107">Изучения этого учебника является необходимым условием для других Android учебники по использованию функции hello мобильные приложения в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="61158-107">Completing this tutorial is a prerequisite for all other Android tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61158-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="61158-108">Prerequisites</span></span>
<span data-ttu-id="61158-109">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="61158-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="61158-110">[Инструменты разработчика Android](https://developer.android.com/sdk/index.html), включающее hello Android Studio интегрированной среды разработки, а также последнюю версию платформы Android hello.</span><span class="sxs-lookup"><span data-stu-id="61158-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>
* <span data-ttu-id="61158-111">Azure Mobile Android SDK, она автоматически создается как часть проекта hello краткое руководство, для загрузки.</span><span class="sxs-lookup"><span data-stu-id="61158-111">Azure Mobile Android SDK, which is automatically referenced as part of hello quickstart project you download.</span></span>
* <span data-ttu-id="61158-112">[Активная учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61158-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="61158-113">Создание серверной части мобильного приложения Azure</span><span class="sxs-lookup"><span data-stu-id="61158-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="61158-114">Настройка проекта сервера hello</span><span class="sxs-lookup"><span data-stu-id="61158-114">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a><span data-ttu-id="61158-115">Загрузите и запустите приложение Android hello</span><span class="sxs-lookup"><span data-stu-id="61158-115">Download and run hello Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
