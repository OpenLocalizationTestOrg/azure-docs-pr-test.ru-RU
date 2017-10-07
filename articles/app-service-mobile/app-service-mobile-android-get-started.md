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
# <a name="create-an-android-app"></a>Создание приложения Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Обзор
Этот учебник показывает, как tooadd облачную серверную службу tooan мобильное приложение Android с помощью внутреннего мобильного приложения Azure.  Мы создадим серверную часть мобильного приложения и простое приложение *списка дел* (на платформе Android), которое хранит свои данные в Azure.

Изучения этого учебника является необходимым условием для других Android учебники по использованию функции hello мобильные приложения в службе приложений Azure.

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника требуется hello следующие:

* [Инструменты разработчика Android](https://developer.android.com/sdk/index.html), включающее hello Android Studio интегрированной среды разработки, а также последнюю версию платформы Android hello.
* Azure Mobile Android SDK, она автоматически создается как часть проекта hello краткое руководство, для загрузки.
* [Активная учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-new-azure-mobile-app-backend"></a>Создание серверной части мобильного приложения Azure
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Настройка проекта сервера hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a>Загрузите и запустите приложение Android hello
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
