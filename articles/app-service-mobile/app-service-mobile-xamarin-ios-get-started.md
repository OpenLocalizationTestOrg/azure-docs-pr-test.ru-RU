---
title: "aaaGet работы с мобильные приложения службы приложений Azure для приложения Xamarin.iOS | Документы Microsoft"
description: "Выполните этот учебник tooget работы с помощью мобильных приложений для разработки Xamarin.iOS."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a>Создание приложения Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Обзор
Этот учебник показывает, как tooadd облачную серверную службу tooa Xamarin.iOS мобильного приложения с помощью внутреннего мобильного приложения Azure.  Вы создадите новую серверную часть мобильного приложения и простое приложение Xamarin.iOS *Todo list*, в котором в Azure хранятся данные приложения.

Изучения этого учебника является необходимым условием для всех других Xamarin.iOS учебников по использованию функции hello мобильные приложения в службе приложений Azure.

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника требуется hello следующие предварительные требования:

* Активная учетная запись Azure. Если у вас нет учетной записи, зарегистрируйтесь в пробной версии Azure и получите бесплатные too10 мобильных приложений, которые вы можете продолжать использовать даже после окончания срока действия пробной версии никакие. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio с Xamarin. Инструкции см. в статье об [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* Компьютер Mac с установленным ПО XCode версии 7.0 или выше и Xamarin Studio Community. См. статьи об [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) и [установке, настройке и проверке для пользователей Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-an-azure-mobile-app-backend"></a>Создание серверной части мобильного приложения Azure
Выполните эти шаги toocreate серверной мобильного приложения.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Настройка проекта сервера hello
Итак, вы подготовили серверную часть мобильного Azure, которая может использоваться мобильными клиентскими приложениями. Затем загрузить проект сервера для простого «todo list» серверная часть и опубликовать его tooAzure.

Выполните следующие шаги tooconfigure hello server проекта toouse hello либо серверной части hello .NET или Node.js.

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a>Загрузите и запустите приложение Xamarin.iOS hello
1. Откройте hello [портал Azure] в окне браузера.
2. В колонке параметров hello для мобильного приложения, нажмите кнопку **начать** > **Xamarin.iOS**. На этапе 3 нажмите кнопку **Создать приложение** (если вы еще не сделали этого).  Далее щелкните hello **загрузки** кнопки.

      Клиентское приложение, которое подключается мобильной серверной части tooyour загружается. Сохраните файл проекта сжатых hello на локальный компьютер и запишите где сохранить.
3. Извлеките hello проекта, который вы загрузили и откройте его в Xamarin Studio (или Visual Studio).

    ![][9]

    ![][8]
4. Нажмите клавишу ключа toobuild hello hello F5 проект и запустить приложение hello в эмуляторе iPhone hello.
5. В приложение hello введите значимыми текстовыми, таких как *узнать Xamarin*и нажмите кнопку hello  **+**  кнопки.

    ![][10]

    Данные из запроса hello вставляется в таблицу TodoItem hello. Элементы, хранящиеся в таблице hello возвращаются сервером мобильного приложения hello, а данные отображаются в списке hello.

> [!NOTE]
> Можно просмотреть hello код, который обращается к tooquery серверной части вашего мобильного приложения и вставить данные в файл QSTodoService.cs C# hello.
>
>

## <a name="next-steps"></a>Дальнейшие действия
* [Добавить приложение tooyour автономной синхронизации](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [Добавить приложение tooyour проверки подлинности](app-service-mobile-xamarin-ios-get-started-users.md)
* [Добавить приложение Xamarin.Android tooyour уведомлений push](app-service-mobile-xamarin-ios-get-started-push.md)
* [Управление toouse hello клиента для мобильных приложений Azure](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[портал Azure]: https://portal.azure.com/
