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
# <a name="create-an-apache-cordova-app"></a>Создание приложения Apache Cordova
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Обзор
Этот учебник показывает, как tooadd облачную серверную службу мобильного приложения Apache Cordova tooan с помощью внутреннего мобильного приложения Azure.  Мы создадим серверную часть мобильного приложения и простое приложение *списка задач* (на платформе Apache Cordova), которое хранит свои данные в Azure.

Изучения этого учебника является необходимым условием для всех других Apache Cordova учебников по использованию функции hello мобильные приложения в службе приложений Azure.

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника требуется hello следующие предварительные требования:

* компьютер с [Visual Studio Community 2017] или более поздней версии;
* [набор средств Visual Studio для Apache Cordova];
* [Активная учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/).

Также можно обойти Visual Studio и непосредственно использовать hello Apache Cordova командной строки.  С помощью командной строки hello полезно при изучении hello руководства на компьютере Mac.  В этот учебник компиляции клиентских приложений Apache Cordova, с помощью командной строки hello не рассматривается.

## <a name="create-an-azure-mobile-app-backend"></a>Создание серверной части мобильного приложения Azure
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[Видео, демонстрирующее аналогичные действия](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a>Настройка проекта сервера hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a>Загрузите и запустите приложение hello Apache Cordova
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы выполнили этого краткого руководства, переместите на tooone из hello следующие учебники:

* [Добавление автономных данных](app-service-mobile-cordova-get-started-offline-data.md) tooyour приложения Apache Cordova.
* [Добавление проверки подлинности](app-service-mobile-cordova-get-started-users.md) tooyour приложения Apache Cordova.
* [Добавление Push-уведомления](app-service-mobile-cordova-get-started-push.md) tooyour приложения Apache Cordova.

Дополнительные сведения об основных понятиях, связанных со службой приложений Azure.

* [Автономные данные]
* [Аутентификация]
* [Push-уведомления]

Узнайте, как toouse hello пакетов SDK.

* [Пакет SDK для Apache Cordova]
* [Серверный пакет SDK для ASP.NET]
* [Серверный пакет SDK для Node.js]

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
