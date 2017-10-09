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
# <a name="create-a-windows-app"></a>Создание приложения Windows
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Обзор
Этот учебник показывает, как tooadd облачную серверную службу tooa приложения универсальной платформы Windows (UWP). Дополнительные сведения см. в статье [Что такое мобильные приложения?](app-service-mobile-value-prop.md). Hello ниже приведены снимки экрана из приложения hello завершена.

![Готовое классическое приложение](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
Выполняется на настольном компьютере.

![Готовое приложение для телефона](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
Выполняется на телефоне.

Изучение этого руководства является необходимым условием для работы со всеми остальными руководствами, посвященными мобильным приложениям UWP.

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника требуется hello следующие:

* Активная учетная запись Azure. При отсутствии учетной записи, можно зарегистрироваться в пробной версии Azure и получите бесплатные too10 мобильных приложений, которые вы можете продолжать использовать даже после окончания срока действия пробной версии никакие. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio Community 2015] или более поздней версии.

## <a name="create-a-new-azure-mobile-app-backend"></a>Создание серверной части мобильного приложения Azure
Выполните эти шаги toocreate новую серверную часть мобильного приложения.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Итак, вы подготовили серверную часть мобильного Azure, которая может использоваться мобильными клиентскими приложениями. Затем будет загрузить проект сервера для простого «todo list» серверная часть и опубликовать его tooAzure.

## <a name="configure-hello-server-project"></a>Настройка проекта сервера hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a>Загрузите и запустите клиентский проект hello
Настроив внутренний сервер приложений для мобильных устройств, можно создавать приложения для клиента или изменить существующие приложения tooAzure tooconnect. В этом разделе загрузите шаблон проекта приложения UWP, настроенные tooconnect tooyour мобильное приложение серверной.

1. Обратно в hello **краткого** колонке серверной части мобильное приложение, нажмите кнопку **создайте новое приложение** > **загрузки**, затем извлечь hello сжатые файлы проекта tooyour локального компьютера.

    ![Загрузка проекта быстрого запуска Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. (Необязательно) Добавить toohello проекта приложения UWP hello же решении, что проект сервера hello. Это упрощает toodebug и тестирования, оба hello серверной части приложения и hello в hello того же решения Visual Studio, при выборе toodo это. tooadd toohello решения проекта приложения UWP, необходимо использовать Visual Studio 2015 или более поздней версии.
3. Приложение UWP hello hello запускаемым проектом нажмите toodeploy клавиш F5 hello и приложение hello выполнения.
4. В приложение hello введите значимыми текстовыми, таких как *завершения hello учебника*, в hello **Insert a TodoItem** текстовое поле и нажмите кнопку **Сохранить**.

    ![Полный быстрый запуск Windows — классическая версия](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    Это приведет к отправке POST запроса toohello новую мобильное приложение серверную часть, размещенной в Azure.
5. (Необязательно) Остановите приложение hello и перезапустите его на другое устройство или эмулятор мобильных устройств.

    ![Полный быстрый запуск Windows — мобильная версия](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    Обратите внимание, что данных, сохраненный при выполнении предыдущего шага hello загружается из Azure после запуска приложения UWP hello.

## <a name="next-steps"></a>Дальнейшие действия
* [Добавить приложение tooyour проверки подлинности](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Узнайте, как пользователи tooauthenticate приложения с поставщиком удостоверений.
* [Добавить приложение tooyour уведомлений push](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Узнайте, как push-уведомления tooadd поддерживают tooyour приложения и настройки вашего мобильного приложения серверной toouse концентраторов уведомлений Azure toosend push-уведомлений.
* [Включение автономной синхронизации для приложения](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Узнайте, как автономные tooadd поддерживают приложения с помощью внутреннего сервера мобильного приложения. Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением&mdash;Просмотр, добавление или изменение данных&mdash;даже в том случае, если нет сетевого соединения.

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
